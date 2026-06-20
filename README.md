// ============================================================
// SKILLCONNECT – COMPLETE SINGLE FILE PLATFORM (SERVER.JS)
// ============================================================
// Run: npm install express jsonwebtoken bcryptjs socket.io cors
// Run: node server.js
// ============================================================

const express = require('express');
const http = require('http');
const socketIo = require('socket.io');
const cors = require('cors');
const jwt = require('jsonwebtoken');
const bcrypt = require('bcryptjs');

// ---------- APP SETUP ----------
const app = express();
const server = http.createServer(app);
const io = socketIo(server, { cors: { origin: '*' } });

app.use(cors());
app.use(express.json({ limit: '50mb' }));
app.use(express.urlencoded({ extended: true, limit: '50mb' }));

const PORT = process.env.PORT || 3000;
const JWT_SECRET = 'your_super_secret_key_change_in_production';

// ---------- IN-MEMORY DATABASE ----------
const DB = {
  users: [],
  workers: [],
  jobs: [],
  bids: [],
  chats: [],
  notifications: [],
  reviews: [],
  transactions: [],
  wallet: {},
  _otpStore: {}
};

// Helper to generate IDs
const genId = () => Date.now().toString(36) + Math.random().toString(36).substr(2, 5);

// ---------- AUTH MIDDLEWARE ----------
const authenticate = (req, res, next) => {
  const token = req.headers.authorization?.split(' ')[1];
  if (!token) return res.status(401).json({ error: 'Unauthorized' });
  try {
    const decoded = jwt.verify(token, JWT_SECRET);
    req.userId = decoded.id;
    req.userRole = decoded.role;
    next();
  } catch (err) {
    res.status(401).json({ error: 'Invalid token' });
  }
};

// ---------- API ROUTES ----------

// --- Auth ---
app.post('/api/auth/register', async (req, res) => {
  const { phone, password, name, role } = req.body;
  if (DB.users.find(u => u.phone === phone)) {
    return res.status(400).json({ error: 'Phone already registered' });
  }
  const hashed = await bcrypt.hash(password, 10);
  const user = {
    id: genId(),
    phone,
    passwordHash: hashed,
    name: name || 'User',
    role: role || 'customer',
    isVerified: false,
    profilePic: null,
    location: null,
    createdAt: new Date().toISOString(),
  };
  DB.users.push(user);
  if (role === 'worker') {
    DB.workers.push({
      userId: user.id,
      category: '',
      experience: 0,
      about: '',
      hourlyRate: 0,
      availability: 'available',
      location: null,
      portfolio: [],
      isPremium: false,
      isFeatured: false,
    });
  }
  DB.wallet[user.id] = { balance: 0, hold: 0 };
  const token = jwt.sign({ id: user.id, role: user.role }, JWT_SECRET, { expiresIn: '7d' });
  res.json({ token, user: { id: user.id, name: user.name, role: user.role } });
});

app.post('/api/auth/login', async (req, res) => {
  const { phone, password } = req.body;
  const user = DB.users.find(u => u.phone === phone);
  if (!user) return res.status(401).json({ error: 'User not found' });
  const valid = await bcrypt.compare(password, user.passwordHash);
  if (!valid) return res.status(401).json({ error: 'Invalid password' });
  const token = jwt.sign({ id: user.id, role: user.role }, JWT_SECRET, { expiresIn: '7d' });
  res.json({ token, user: { id: user.id, name: user.name, role: user.role } });
});

app.post('/api/auth/send-otp', (req, res) => {
  const { phone } = req.body;
  const otp = Math.floor(100000 + Math.random() * 900000);
  DB._otpStore[phone] = { otp, expires: Date.now() + 300000 };
  console.log(`✅ OTP for ${phone}: ${otp}`); // OTP console में दिखेगा
  res.json({ success: true });
});

app.post('/api/auth/verify-otp', (req, res) => {
  const { phone, otp } = req.body;
  const stored = DB._otpStore?.[phone];
  if (!stored || stored.otp != otp || stored.expires < Date.now()) {
    return res.status(401).json({ error: 'Invalid or expired OTP' });
  }
  let user = DB.users.find(u => u.phone === phone);
  if (!user) {
    user = {
      id: genId(),
      phone,
      passwordHash: null,
      name: 'User',
      role: 'customer',
      isVerified: true,
      profilePic: null,
      location: null,
      createdAt: new Date().toISOString(),
    };
    DB.users.push(user);
    DB.wallet[user.id] = { balance: 0, hold: 0 };
  } else {
    user.isVerified = true;
  }
  const token = jwt.sign({ id: user.id, role: user.role }, JWT_SECRET, { expiresIn: '7d' });
  res.json({ token, user: { id: user.id, name: user.name, role: user.role } });
});

// --- Workers ---
app.get('/api/workers', (req, res) => {
  const allWorkers = DB.workers.map(w => {
    const user = DB.users.find(u => u.id === w.userId);
    return { ...w, user: user ? { name: user.name, phone: user.phone, profilePic: user.profilePic } : null };
  });
  res.json(allWorkers);
});

app.get('/api/workers/:userId', (req, res) => {
  const worker = DB.workers.find(w => w.userId === req.params.userId);
  if (!worker) return res.status(404).json({ error: 'Worker not found' });
  const user = DB.users.find(u => u.id === worker.userId);
  res.json({ ...worker, user });
});

// --- Jobs ---
app.post('/api/jobs', authenticate, (req, res) => {
  const { title, description, category, location, budget, urgency } = req.body;
  const job = {
    id: genId(),
    customerId: req.userId,
    title,
    description,
    category,
    location: location || { address: 'Bangalore' },
    budget: parseFloat(budget) || 0,
    urgency: urgency || 'normal',
    status: 'open',
    createdAt: new Date().toISOString(),
    bids: [],
  };
  DB.jobs.push(job);
  io.emit('new-job', job);
  res.json({ job });
});

app.get('/api/jobs', (req, res) => {
  const jobs = DB.jobs.map(j => {
    const customer = DB.users.find(u => u.id === j.customerId);
    return { ...j, customer: customer ? { name: customer.name } : null };
  });
  res.json(jobs);
});

app.get('/api/jobs/:id', (req, res) => {
  const job = DB.jobs.find(j => j.id === req.params.id);
  if (!job) return res.status(404).json({ error: 'Job not found' });
  const customer = DB.users.find(u => u.id === job.customerId);
  const bids = DB.bids.filter(b => b.jobId === job.id).map(b => {
    const worker = DB.workers.find(w => w.userId === b.workerId);
    const user = worker ? DB.users.find(u => u.id === worker.userId) : null;
    return { ...b, worker: user ? { name: user.name } : null };
  });
  res.json({ ...job, customer: customer ? { name: customer.name } : null, bids });
});

// --- Bids ---
app.post('/api/bids', authenticate, (req, res) => {
  const { jobId, amount, estimatedTime, message } = req.body;
  const job = DB.jobs.find(j => j.id === jobId);
  if (!job) return res.status(404).json({ error: 'Job not found' });
  const existing = DB.bids.find(b => b.jobId === jobId && b.workerId === req.userId);
  if (existing) return res.status(400).json({ error: 'Already bid' });
  const bid = {
    id: genId(),
    jobId,
    workerId: req.userId,
    amount: parseFloat(amount) || 0,
    estimatedTime: estimatedTime || '1 hour',
    message: message || '',
    status: 'pending',
    createdAt: new Date().toISOString(),
  };
  DB.bids.push(bid);
  const customer = DB.users.find(u => u.id === job.customerId);
  if (customer) {
    io.to(`user-${customer.id}`).emit('new-bid', { jobId, bid });
  }
  res.json({ bid });
});

app.put('/api/bids/:id/accept', authenticate, (req, res) => {
  const bid = DB.bids.find(b => b.id === req.params.id);
  if (!bid) return res.status(404).json({ error: 'Bid not found' });
  const job = DB.jobs.find(j => j.id === bid.jobId);
  if (!job || job.customerId !== req.userId) return res.status(403).json({ error: 'Forbidden' });
  bid.status = 'accepted';
  job.status = 'in_progress';
  const chat = {
    jobId: job.id,
    participants: [job.customerId, bid.workerId],
    messages: [],
  };
  DB.chats.push(chat);
  io.to(`user-${bid.workerId}`).emit('bid-accepted', { jobId: job.id });
  res.json({ success: true });
});

// --- Wallet ---
app.get('/api/wallet', authenticate, (req, res) => {
  const wallet = DB.wallet[req.userId] || { balance: 0, hold: 0 };
  res.json(wallet);
});

app.post('/api/wallet/add', authenticate, (req, res) => {
  const { amount } = req.body;
  const wallet = DB.wallet[req.userId];
  if (!wallet) return res.status(404).json({ error: 'Wallet not found' });
  wallet.balance += parseFloat(amount);
  DB.transactions.push({
    id: genId(),
    userId: req.userId,
    amount: parseFloat(amount),
    type: 'deposit',
    status: 'completed',
    description: 'Wallet top-up',
    createdAt: new Date().toISOString(),
  });
  res.json({ wallet });
});

// --- Emergency ---
app.post('/api/emergency', authenticate, (req, res) => {
  const { description, location } = req.body;
  const nearbyWorkers = DB.workers.slice(0, 3);
  nearbyWorkers.forEach(w => {
    const user = DB.users.find(u => u.id === w.userId);
    if (user) {
      DB.notifications.push({
        userId: user.id,
        title: '🚨 Emergency Alert',
        body: `Customer needs immediate help: ${description}`,
        read: false,
        createdAt: new Date().toISOString(),
      });
      io.to(`user-${user.id}`).emit('emergency-alert', { description, location });
    }
  });
  res.json({ success: true, dispatched: nearbyWorkers.length });
});

// ---------- SOCKET.IO (REALTIME CHAT) ----------
io.on('connection', (socket) => {
  console.log('🟢 New client connected');
  
  socket.on('join-room', (data) => {
    const { jobId, userId } = data;
    const room = `job-${jobId}`;
    socket.join(room);
    const chat = DB.chats.find(c => c.jobId === jobId);
    if (chat) {
      socket.emit('chat-history', chat.messages);
    }
  });

  socket.on('send-message', (data) => {
    const { jobId, senderId, content } = data;
    let chat = DB.chats.find(c => c.jobId === jobId);
    if (!chat) {
      chat = { jobId, participants: [], messages: [] };
      DB.chats.push(chat);
    }
    const msg = { senderId, content, timestamp: new Date().toISOString() };
    chat.messages.push(msg);
    io.to(`job-${jobId}`).emit('new-message', msg);
  });

  socket.on('disconnect', () => {
    console.log('🔴 Client disconnected');
  });
});

// ---------- SERVE FRONTEND (HTML + CSS + JS) ----------
app.get('*', (req, res) => {
  res.send(`
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
  <title>SkillConnect – Complete Platform</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">
  <script src="https://cdn.socket.io/4.7.2/socket.io.min.js"></script>
  <style>
    body { font-family: 'Inter', system-ui, sans-serif; background: #f0f2f5; }
    .container-custom { max-width: 420px; margin: 0 auto; background: white; min-height: 100vh; box-shadow: 0 0 40px rgba(0,0,0,0.08); }
    .nav-item { display: flex; flex-direction: column; align-items: center; font-size: 11px; color: #9ca3af; padding: 4px 12px; border-radius: 30px; cursor: pointer; transition: 0.2s; }
    .nav-item.active { color: #1A5F7A; background: #E8F0FE; font-weight: 600; }
    .nav-item i { font-size: 22px; margin-bottom: 2px; }
    .worker-card { background: white; border-radius: 16px; padding: 12px; box-shadow: 0 2px 8px rgba(0,0,0,0.04); border: 1px solid #f1f3f5; cursor: pointer; transition: 0.2s; }
    .worker-card:active { transform: scale(0.98); }
    .chip { background: #f1f3f5; border-radius: 30px; padding: 6px 16px; font-size: 13px; white-space: nowrap; cursor: pointer; transition: 0.2s; border: 1px solid transparent; }
    .chip.active { background: #1A5F7A; color: white; border-color: #1A5F7A; }
    .btn-primary { background: #1A5F7A; color: white; border: none; border-radius: 30px; padding: 12px; font-weight: 700; width: 100%; cursor: pointer; transition: 0.2s; }
    .btn-primary:active { transform: scale(0.97); }
    .btn-outline { background: transparent; border: 2px solid #1A5F7A; color: #1A5F7A; border-radius: 30px; padding: 12px; font-weight: 700; width: 100%; cursor: pointer; }
    .emergency-btn { background: #E63946; color: white; border-radius: 50%; width: 56px; height: 56px; display: flex; align-items: center; justify-content: center; box-shadow: 0 6px 20px rgba(230,57,70,0.4); cursor: pointer; border: none; }
    .ai-btn { background: #1A5F7A; color: white; border-radius: 50%; width: 52px; height: 52px; display: flex; align-items: center; justify-content: center; box-shadow: 0 6px 20px rgba(26,95,122,0.3); cursor: pointer; border: none; }
    .form-group { margin-bottom: 16px; }
    .form-group label { font-weight: 600; font-size: 14px; display: block; margin-bottom: 4px; color: #1D1D1F; }
    input, textarea, select { width: 100%; padding: 12px; border: 1px solid #dee2e6; border-radius: 14px; font-size: 15px; font-family: inherit; outline: none; }
    input:focus, textarea:focus, select:focus { border-color: #1A5F7A; ring: 2px solid #1A5F7A; }
    .toast { position: fixed; top: 20px; left: 50%; transform: translateX(-50%); background: #1D1D1F; color: white; padding: 12px 24px; border-radius: 30px; z-index: 9999; box-shadow: 0 8px 30px rgba(0,0,0,0.2); display: none; font-weight: 500; white-space: nowrap; max-width: 90%; text-align: center; }
    .hide-scrollbar::-webkit-scrollbar { display: none; }
    .hide-scrollbar { -ms-overflow-style: none; scrollbar-width: none; }
    .chat-bubble-user { background: #1A5F7A; color: white; border-radius: 18px 18px 4px 18px; padding: 10px 16px; max-width: 80%; align-self: flex-end; }
    .chat-bubble-other { background: #f1f3f5; color: #1D1D1F; border-radius: 18px 18px 18px 4px; padding: 10px 16px; max-width: 80%; align-self: flex-start; }
  </style>
</head>
<body>

<div class="toast" id="toast"></div>

<div class="container-custom" id="app">
  <!-- Status Bar -->
  <div class="flex justify-between items-center px-4 py-2 text-xs font-semibold bg-white border-b">
    <span>9:41</span>
    <span><i class="fas fa-signal"></i> <i class="fas fa-wifi"></i> <i class="fas fa-battery-full"></i></span>
  </div>

  <!-- Screen Container -->
  <div id="screenContainer" class="overflow-y-auto" style="height: calc(100vh - 130px);">
    <div id="screenContent"></div>
  </div>

  <!-- Bottom Navigation -->
  <div class="bg-white border-t flex justify-around items-center py-1 fixed bottom-0 left-0 right-0" style="max-width:420px;margin:0 auto;">
    <button class="nav-item active" data-screen="home"><i class="fas fa-home"></i><span>Home</span></button>
    <button class="nav-item" data-screen="search"><i class="fas fa-search"></i><span>Search</span></button>
    <button class="nav-item" data-screen="post"><i class="fas fa-plus-circle text-3xl text-[#1A5F7A] -mt-2"></i><span>Post</span></button>
    <button class="nav-item" data-screen="chat"><i class="fas fa-envelope"></i><span>Chat</span></button>
    <button class="nav-item" data-screen="profile"><i class="fas fa-user"></i><span>Profile</span></button>
  </div>
</div>

<script>
// ============================================================
// FRONTEND APPLICATION
// ============================================================

// ---------- STATE ----------
let currentUser = null;
let token = null;
let socket = null;
let currentScreen = 'home';
let currentChatJobId = null;
let workers = [];
let jobs = [];
let _chatMessages = {};

// ---------- DOM REFS ----------
const screenContainer = document.getElementById('screenContent');
const toastEl = document.getElementById('toast');

// ---------- API HELPERS ----------
async function apiCall(method, url, data) {
  const headers = { 'Content-Type': 'application/json' };
  if (token) headers['Authorization'] = `Bearer ${token}`;
  const res = await fetch(url, { method, headers, body: data ? JSON.stringify(data) : undefined });
  return res.json();
}

function showToast(msg) {
  toastEl.textContent = msg;
  toastEl.style.display = 'block';
  setTimeout(() => toastEl.style.display = 'none', 3000);
}

// ---------- AUTH ----------
async function register(phone, password, name, role) {
  const data = await apiCall('POST', '/api/auth/register', { phone, password, name, role });
  if (data.token) {
    token = data.token;
    currentUser = data.user;
    localStorage.setItem('token', token);
    localStorage.setItem('user', JSON.stringify(currentUser));
    initSocket();
    showToast('✅ Registration successful!');
    navigate('home');
  } else {
    showToast(data.error || 'Registration failed');
  }
}

async function login(phone, password) {
  const data = await apiCall('POST', '/api/auth/login', { phone, password });
  if (data.token) {
    token = data.token;
    currentUser = data.user;
    localStorage.setItem('token', token);
    localStorage.setItem('user', JSON.stringify(currentUser));
    initSocket();
    showToast('👋 Welcome back!');
    navigate('home');
  } else {
    showToast(data.error || 'Login failed');
  }
}

function logout() {
  localStorage.removeItem('token');
  localStorage.removeItem('user');
  token = null;
  currentUser = null;
  if (socket) socket.disconnect();
  navigate('login');
}

// ---------- SOCKET.IO ----------
function initSocket() {
  if (socket) socket.disconnect();
  socket = io();
  socket.on('connect', () => {
    console.log('Socket connected');
  });
  socket.on('new-bid', (data) => {
    showToast('📩 New bid received on your job!');
    if (currentScreen === 'home') loadHome();
  });
  socket.on('bid-accepted', (data) => {
    showToast('🎉 Your bid was accepted!');
    loadChats();
  });
  socket.on('new-message', (msg) => {
    if (currentScreen === 'chat' && currentChatJobId) {
      appendMessage(msg);
    } else {
      showToast('💬 New message received');
    }
  });
  socket.on('emergency-alert', (data) => {
    showToast('🚨 Emergency request nearby!');
  });
  socket.on('chat-history', (msgs) => {
    if (currentChatJobId) {
      _chatMessages[currentChatJobId] = msgs || [];
      renderMessages(currentChatJobId);
    }
  });
}

// ---------- NAVIGATION ----------
function navigate(screen, params) {
  currentScreen = screen;
  document.querySelectorAll('.nav-item').forEach(b => b.classList.remove('active'));
  const navBtn = document.querySelector(`.nav-item[data-screen="${screen}"]`);
  if (navBtn) navBtn.classList.add('active');
  renderScreen(screen, params);
  document.getElementById('screenContainer').scrollTop = 0;
}

function renderScreen(screen, params) {
  switch(screen) {
    case 'login': renderLogin(); break;
    case 'register': renderRegister(); break;
    case 'home': loadHome(); break;
    case 'search': loadSearch(); break;
    case 'post': renderPostJob(); break;
    case 'chat': loadChats(params); break;
    case 'profile': loadProfile(); break;
    default: screenContainer.innerHTML = '<div class="p-4 text-center">Page not found</div>';
  }
}

// ---------- RENDER LOGIN ----------
function renderLogin() {
  screenContainer.innerHTML = \`
    <div class="p-6 flex flex-col items-center justify-center h-full">
      <div class="text-4xl font-bold text-[#1A5F7A] mb-2">SkillConnect</div>
      <p class="text-gray-500 mb-8">Login to continue</p>
      <div class="w-full space-y-4">
        <input id="loginPhone" placeholder="Phone Number" class="w-full p-3 border rounded-xl">
        <input id="loginPassword" type="password" placeholder="Password" class="w-full p-3 border rounded-xl">
        <button onclick="doLogin()" class="btn-primary">Login</button>
        <p class="text-center text-sm">Don't have an account? <a href="#" onclick="navigate('register')" class="text-[#1A5F7A] font-bold">Register</a></p>
        <button onclick="sendOtp()" class="btn-outline">Login with OTP</button>
      </div>
    </div>
  \`;
}

async function doLogin() {
  const phone = document.getElementById('loginPhone').value;
  const pass = document.getElementById('loginPassword').value;
  if (!phone || !pass) return showToast('Please fill all fields');
  await login(phone, pass);
}

async function sendOtp() {
  const phone = document.getElementById('loginPhone').value;
  if (!phone) return showToast('Enter phone number');
  await apiCall('POST', '/api/auth/send-otp', { phone });
  showToast('📱 OTP sent! Check terminal console.');
  const otp = prompt('Enter OTP (check terminal for code)');
  if (otp) {
    const data = await apiCall('POST', '/api/auth/verify-otp', { phone, otp });
    if (data.token) {
      token = data.token;
      currentUser = data.user;
      localStorage.setItem('token', token);
      localStorage.setItem('user', JSON.stringify(currentUser));
      initSocket();
      showToast('✅ Login successful');
      navigate('home');
    } else {
      showToast('❌ Invalid OTP');
    }
  }
}

// ---------- RENDER REGISTER ----------
function renderRegister() {
  screenContainer.innerHTML = \`
    <div class="p-6 flex flex-col items-center justify-center h-full">
      <h2 class="text-2xl font-bold mb-4">Create Account</h2>
      <div class="w-full space-y-3">
        <input id="regName" placeholder="Full Name" class="w-full p-3 border rounded-xl">
        <input id="regPhone" placeholder="Phone Number" class="w-full p-3 border rounded-xl">
        <input id="regPassword" type="password" placeholder="Password" class="w-full p-3 border rounded-xl">
        <select id="regRole" class="w-full p-3 border rounded-xl">
          <option value="customer">Customer</option>
          <option value="worker">Worker</option>
        </select>
        <button onclick="doRegister()" class="btn-primary">Register</button>
        <p class="text-center text-sm">Already have an account? <a href="#" onclick="navigate('login')" class="text-[#1A5F7A] font-bold">Login</a></p>
      </div>
    </div>
  \`;
}

async function doRegister() {
  const name = document.getElementById('regName').value;
  const phone = document.getElementById('regPhone').value;
  const password = document.getElementById('regPassword').value;
  const role = document.getElementById('regRole').value;
  if (!name || !phone || !password) return showToast('Please fill all fields');
  await register(phone, password, name, role);
}

// ---------- HOME ----------
async function loadHome() {
  const workersData = await apiCall('GET', '/api/workers');
  workers = workersData;
  const jobsData = await apiCall('GET', '/api/jobs');
  jobs = jobsData;
  renderHome(workers, jobs);
}

function renderHome(workers, jobs) {
  const user = currentUser;
  screenContainer.innerHTML = \`
    <div class="p-4">
      <div class="flex justify-between items-start">
        <div>
          <div class="text-xl font-bold">Hello, \${user?.name || 'User'} 👋</div>
          <div class="text-gray-500 text-sm">Find the best workers near you</div>
        </div>
        <div>
          <button onclick="showNotifications()" class="ml-2"><i class="fas fa-bell text-xl"></i></button>
        </div>
      </div>

      <div class="flex items-center bg-white border rounded-full px-4 py-2 mt-3 shadow-sm">
        <i class="fas fa-search text-gray-400"></i>
        <input id="homeSearch" placeholder="What service do you need?" class="flex-1 outline-none ml-2" oninput="filterWorkers(this.value)">
      </div>

      <div class="flex gap-2 overflow-x-auto hide-scrollbar mt-3" id="categoryChips">
        <span class="chip active" onclick="filterCategory('all', this)">All</span>
        <span class="chip" onclick="filterCategory('plumber', this)"><i class="fas fa-wrench"></i> Plumber</span>
        <span class="chip" onclick="filterCategory('electrician', this)"><i class="fas fa-bolt"></i> Electrician</span>
        <span class="chip" onclick="filterCategory('carpenter', this)"><i class="fas fa-hammer"></i> Carpenter</span>
        <span class="chip" onclick="filterCategory('painter', this)"><i class="fas fa-paint-roller"></i> Painter</span>
      </div>

      <div class="mt-4">
        <div class="flex justify-between items-center">
          <h3 class="font-bold text-lg">🌟 Nearby Workers</h3>
          <a href="#" onclick="navigate('search')" class="text-sm text-[#1A5F7A]">See all</a>
        </div>
        <div id="workersList" class="space-y-3 mt-2">
          \${workers.slice(0,5).map(w => workerCard(w)).join('')}
        </div>
      </div>

      <div class="mt-6">
        <div class="flex justify-between items-center">
          <h3 class="font-bold text-lg">📋 Recent Jobs</h3>
          <a href="#" onclick="navigate('post')" class="text-sm text-[#1A5F7A]">Post new</a>
        </div>
        <div id="jobsList" class="space-y-2 mt-2">
          \${jobs.slice(0,3).map(j => jobCard(j)).join('')}
        </div>
      </div>

      <div class="fixed bottom-24 right-4 space-y-3" style="max-width:420px;margin-left:auto;">
        <button class="ai-btn" onclick="openAI()"><i class="fas fa-robot"></i></button>
        <button class="emergency-btn" onclick="openEmergency()"><i class="fas fa-phone-alt"></i></button>
      </div>
    </div>
  \`;
}

function workerCard(w) {
  const user = w.user || { name: 'Worker' };
  return \`
    <div class="worker-card flex items-center gap-3" onclick="viewWorker('\${w.userId}')">
      <div class="w-12 h-12 rounded-full bg-gray-200 flex items-center justify-center font-bold text-xl text-[#1A5F7A]">\${user.name ? user.name[0] : 'W'}</div>
      <div class="flex-1">
        <div class="font-semibold flex items-center gap-1">\${user.name} <i class="fas fa-check-circle text-green-500 text-sm"></i></div>
        <div class="text-sm text-gray-500">\${w.category || 'Skilled'} • ₹\${w.hourlyRate || 0}/hr</div>
        <div class="text-sm text-yellow-500"><i class="fas fa-star"></i> 4.8</div>
      </div>
      <div class="text-right text-sm text-gray-500">\${w.availability || 'available'}</div>
    </div>
  \`;
}

function jobCard(j) {
  return \`
    <div class="worker-card cursor-pointer" onclick="viewJob('\${j.id}')">
      <div class="font-semibold">\${j.title}</div>
      <div class="text-sm text-gray-500">\${j.category} • \${j.location?.address || 'Bangalore'}</div>
      <div class="flex justify-between mt-1">
        <span class="text-sm">₹\${j.budget}</span>
        <span class="text-xs bg-gray-200 px-2 py-1 rounded-full">\${j.status}</span>
      </div>
    </div>
  \`;
}

function filterCategory(cat, el) {
  document.querySelectorAll('#categoryChips .chip').forEach(c => c.classList.remove('active'));
  el.classList.add('active');
}

function filterWorkers(val) {
  const cards = document.querySelectorAll('#workersList .worker-card');
  cards.forEach(card => {
    const text = card.textContent.toLowerCase();
    card.style.display = text.includes(val.toLowerCase()) ? 'flex' : 'none';
  });
}

function viewWorker(userId) {
  showToast('👤 Viewing worker profile (demo)');
}

function viewJob(jobId) {
  showToast('📋 Viewing job details (demo)');
}

// ---------- SEARCH ----------
async function loadSearch() {
  const data = await apiCall('GET', '/api/workers');
  workers = data;
  screenContainer.innerHTML = \`
    <div class="p-4">
      <h2 class="text-xl font-bold">🔍 Search Workers</h2>
      <div class="flex items-center bg-white border rounded-full px-4 py-2 mt-3 shadow-sm">
        <i class="fas fa-search text-gray-400"></i>
        <input id="searchInput" placeholder="Search by name or skill..." class="flex-1 outline-none ml-2" oninput="filterSearch(this.value)">
      </div>
      <div id="searchResults" class="mt-3 space-y-3">
        \${workers.map(w => workerCard(w)).join('')}
      </div>
    </div>
  \`;
}

async function filterSearch(val) {
  const data = await apiCall('GET', '/api/workers');
  const filtered = data.filter(w => (w.user?.name || '').toLowerCase().includes(val.toLowerCase()) || (w.category || '').toLowerCase().includes(val.toLowerCase()));
  document.getElementById('searchResults').innerHTML = filtered.map(w => workerCard(w)).join('');
}

// ---------- POST JOB ----------
function renderPostJob() {
  screenContainer.innerHTML = \`
    <div class="p-4">
      <h2 class="text-xl font-bold">📝 Post a Job</h2>
      <p class="text-gray-500 text-sm mb-4">Get bids from trusted workers</p>
      <div class="form-group">
        <label>Job Title</label>
        <input id="jobTitle" placeholder="e.g. Fix leaking tap">
      </div>
      <div class="form-group">
        <label>Category</label>
        <select id="jobCategory">
          <option>Plumber</option><option>Electrician</option><option>Carpenter</option><option>Painter</option><option>Cleaner</option>
        </select>
      </div>
      <div class="form-group">
        <label>Description</label>
        <textarea id="jobDesc" rows="3" placeholder="Describe the work..."></textarea>
      </div>
      <div class="form-group">
        <label>Budget (₹)</label>
        <input id="jobBudget" type="number" placeholder="500">
      </div>
      <div class="flex items-center gap-2 mb-4">
        <input type="checkbox" id="jobUrgent">
        <label for="jobUrgent" class="text-red-500 font-semibold">Emergency</label>
      </div>
      <button onclick="submitJob()" class="btn-primary"><i class="fas fa-paper-plane"></i> Post Job</button>
    </div>
  \`;
}

async function submitJob() {
  const title = document.getElementById('jobTitle').value;
  const category = document.getElementById('jobCategory').value;
  const description = document.getElementById('jobDesc').value;
  const budget = document.getElementById('jobBudget').value;
  const urgency = document.getElementById('jobUrgent').checked ? 'emergency' : 'normal';
  if (!title) return showToast('Please enter a title');
  const data = await apiCall('POST', '/api/jobs', { title, category, description, budget, location: {address:'Bangalore'}, urgency });
  if (data.job) {
    showToast('✅ Job posted successfully!');
    navigate('home');
  } else {
    showToast('Failed to post job');
  }
}

// ---------- CHAT ----------
async function loadChats(jobId) {
  const jobsData = await apiCall('GET', '/api/jobs');
  const userJobs = jobsData.filter(j => j.customerId === currentUser?.id);
  screenContainer.innerHTML = \`
    <div class="p-4">
      <h2 class="text-xl font-bold">💬 Messages</h2>
      <div id="chatList" class="mt-3 space-y-3">
        \${userJobs.map(j => \`
          <div class="worker-card cursor-pointer" onclick="openChatRoom('\${j.id}')">
            <div class="font-semibold">\${j.title}</div>
            <div class="text-sm text-gray-500">\${j.status} • \${j.bids?.length || 0} bids</div>
          </div>
        \`).join('')}
        \${userJobs.length === 0 ? '<p class="text-gray-500">No active jobs. Post a job to start chatting!</p>' : ''}
      </div>
      <div id="chatRoom" style="display:none;" class="mt-4">
        <div class="flex items-center gap-2">
          <button onclick="closeChatRoom()" class="text-xl"><i class="fas fa-arrow-left"></i></button>
          <h3 id="chatJobTitle" class="font-bold">Chat</h3>
        </div>
        <div id="messagesContainer" class="h-64 overflow-y-auto bg-gray-50 rounded-xl p-3 mt-2 flex flex-col space-y-2"></div>
        <div class="flex gap-2 mt-2">
          <input id="chatInput" placeholder="Type message..." class="flex-1 p-2 border rounded-xl">
          <button onclick="sendMessage()" class="bg-[#1A5F7A] text-white px-4 rounded-xl"><i class="fas fa-paper-plane"></i></button>
        </div>
      </div>
    </div>
  \`;
  if (jobId) {
    openChatRoom(jobId);
  }
}

function openChatRoom(jobId) {
  currentChatJobId = jobId;
  document.getElementById('chatList').style.display = 'none';
  document.getElementById('chatRoom').style.display = 'block';
  if (socket) {
    socket.emit('join-room', { jobId, userId: currentUser.id });
  }
  const job = jobs.find(j => j.id === jobId);
  document.getElementById('chatJobTitle').textContent = job ? job.title : 'Chat';
  renderMessages(jobId);
}

function renderMessages(jobId) {
  const msgs = _chatMessages[jobId] || [];
  const container = document.getElementById('messagesContainer');
  container.innerHTML = msgs.map(m => \`
    <div class="flex \${m.senderId === currentUser.id ? 'justify-end' : 'justify-start'}">
      <span class="\${m.senderId === currentUser.id ? 'chat-bubble-user' : 'chat-bubble-other'}">
        \${m.content}
      </span>
    </div>
  \`).join('');
  container.scrollTop = container.scrollHeight;
}

function appendMessage(msg) {
  if (!currentChatJobId) return;
  if (!_chatMessages[currentChatJobId]) _chatMessages[currentChatJobId] = [];
  _chatMessages[currentChatJobId].push(msg);
  renderMessages(currentChatJobId);
}

function sendMessage() {
  const input = document.getElementById('chatInput');
  const content = input.value.trim();
  if (!content || !currentChatJobId) return;
  const msg = { senderId: currentUser.id, content, timestamp: new Date().toISOString() };
  if (socket) {
    socket.emit('send-message', { jobId: currentChatJobId, senderId: currentUser.id, content });
  }
  appendMessage(msg);
  input.value = '';
}

function closeChatRoom() {
  document.getElementById('chatList').style.display = 'block';
  document.getElementById('chatRoom').style.display = 'none';
  currentChatJobId = null;
}

// ---------- PROFILE ----------
async function loadProfile() {
  const user = currentUser;
  let workerData = null;
  if (user?.role === 'worker') {
    const w = workers.find(w => w.userId === user.id);
    workerData = w;
  }
  screenContainer.innerHTML = \`
    <div class="p-4">
      <div class="flex justify-between items-start">
        <h2 class="text-xl font-bold">Profile</h2>
        <button onclick="toggleRole()" class="bg-gray-100 px-3 py-1 rounded-full text-sm">\${user?.role === 'worker' ? 'Switch to Customer' : 'Switch to Worker'}</button>
      </div>
      <div class="text-center mt-4">
        <div class="w-20 h-20 bg-gray-200 rounded-full mx-auto flex items-center justify-center text-3xl font-bold text-[#1A5F7A]">\${user?.name?.[0] || 'U'}</div>
        <h3 class="font-bold text-xl">\${user?.name}</h3>
        <p class="text-gray-500 text-sm">\${user?.role === 'worker' ? (workerData?.category || 'Skilled Worker') : 'Customer'}</p>
        <p class="text-sm text-gray-400">\${user?.phone}</p>
      </div>
      <div class="mt-4 grid grid-cols-3 gap-2 text-center">
        <div class="bg-gray-50 p-2 rounded-xl"><div class="font-bold">\${user?.role === 'worker' ? workerData?.experience || 0 : 0}</div><div class="text-xs text-gray-500">Years Exp</div></div>
        <div class="bg-gray-50 p-2 rounded-xl"><div class="font-bold">4.8</div><div class="text-xs text-gray-500">Rating</div></div>
        <div class="bg-gray-50 p-2 rounded-xl"><div class="font-bold">₹\${workerData?.hourlyRate || 0}</div><div class="text-xs text-gray-500">Rate/hr</div></div>
      </div>
      <div class="mt-6 space-y-2">
        <button onclick="viewWallet()" class="btn-primary"><i class="fas fa-wallet"></i> Wallet</button>
        <button onclick="logout()" class="btn-outline">Logout</button>
      </div>
    </div>
  \`;
}

async function viewWallet() {
  const data = await apiCall('GET', '/api/wallet');
  if (data.balance !== undefined) {
    showToast(\`💰 Wallet balance: ₹\${data.balance}\`);
  } else {
    showToast('Wallet not available');
  }
}

function toggleRole() {
  showToast('🔄 Role switched (demo)');
  loadProfile();
}

// ---------- UTILITIES ----------
function openAI() {
  showToast('🤖 AI Assistant: I can help you find the best worker!');
}

function openEmergency() {
  if (!currentUser) return showToast('Please login first');
  const desc = prompt('Describe your emergency:');
  if (desc) {
    apiCall('POST', '/api/emergency', { description: desc, location: 'Bangalore' });
    showToast('🚨 Emergency alert sent! Nearby workers notified.');
  }
}

function showNotifications() {
  showToast('🔔 You have 3 new notifications');
}

// ---------- INIT ----------
async function init() {
  const savedToken = localStorage.getItem('token');
  const savedUser = localStorage.getItem('user');
  if (savedToken && savedUser) {
    token = savedToken;
    currentUser = JSON.parse(savedUser);
    initSocket();
    navigate('home');
  } else {
    navigate('login');
  }
  document.querySelectorAll('.nav-item').forEach(btn => {
    btn.addEventListener('click', function() {
      const screen = this.dataset.screen;
      if (screen) navigate(screen);
    });
  });
}

init();
console.log('🚀 SkillConnect frontend loaded');
</script>
</body>
</html>
  \`);
});

// ---------- START SERVER ----------
server.listen(PORT, () => {
  console.log(`\n🚀 SkillConnect is LIVE at http://localhost:${PORT}`);
  console.log(`📦 In-memory database – data will reset on restart`);
  console.log(`🔑 Quick login: Use OTP (check terminal console) or register new account.\n`);
});
