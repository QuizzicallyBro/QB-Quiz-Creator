<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>SkillConnect – Complete Platform</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">
    <link rel="stylesheet" href="css/style.css">
    <link rel="icon" href="assets/icons/favicon.ico">
</head>
<body>

    <!-- Toast -->
    <div id="toast"></div>

    <!-- App -->
    <div id="app">
        <!-- Header -->
        <header class="app-header">
            <div class="logo">
                <i class="fas fa-bolt"></i>
                <span>SkillConnect</span>
            </div>
            <div class="header-actions">
                <button class="theme-toggle" id="themeToggle" title="Toggle Dark Mode">
                    <i class="fas fa-moon"></i>
                </button>
                <button id="notifHeaderBtn" onclick="openNotifications()" title="Notifications">
                    <i class="fas fa-bell"></i>
                    <span class="badge-dot" id="notifDot" style="display:none;"></span>
                </button>
                <button class="lang-btn" id="langBtn" onclick="toggleLanguage()">🇮🇳 हिंदी</button>
            </div>
        </header>

        <!-- Main Content -->
        <div class="main-content" id="mainContent">
            <!-- Screens will be injected here -->
        </div>

        <!-- Bottom Navigation -->
        <nav class="bottom-nav" id="bottomNav">
            <button class="nav-item active" data-screen="home" onclick="navigateTo('home')">
                <i class="fas fa-home"></i>
                <span id="navHomeLabel">Home</span>
            </button>
            <button class="nav-item" data-screen="search" onclick="navigateTo('search')">
                <i class="fas fa-search"></i>
                <span id="navSearchLabel">Search</span>
            </button>
            <button class="nav-item nav-post" data-screen="postjob" onclick="navigateTo('postjob')">
                <i class="fas fa-plus"></i>
            </button>
            <button class="nav-item" data-screen="chat" onclick="navigateTo('chat')">
                <i class="fas fa-envelope"></i>
                <span id="navChatLabel">Chat</span>
                <span class="nav-badge" id="chatBadge" style="display:none;">0</span>
            </button>
            <button class="nav-item" data-screen="profile" onclick="navigateTo('profile')">
                <i class="fas fa-user"></i>
                <span id="navProfileLabel">Profile</span>
            </button>
        </nav>
    </div>

    <!-- Modal -->
    <div class="modal-overlay" id="modalOverlay" onclick="if(event.target===this)closeModal()">
        <div class="modal-content" id="modalContent">
            <div class="modal-handle"></div>
            <button class="modal-close" onclick="closeModal()"><i class="fas fa-times"></i></button>
            <div id="modalBody"></div>
        </div>
    </div>

    <!-- JavaScript Modules -->
    <script src="js/storage.js"></script>
    <script src="js/auth.js"></script>
    <script src="js/workers.js"></script>
    <script src="js/jobs.js"></script>
    <script src="js/admin.js"></script>
    <script src="js/notifications.js"></script>
    <script src="js/ai.js"></script>
    <script src="js/app.js"></script>
</body>
</html>
/* ============================================================
   CSS VARIABLES & RESET
   ============================================================ */
:root {
    --primary: #1A5F7A;
    --primary-light: #2A7F9A;
    --primary-dark: #0F3F4F;
    --secondary: #F8B500;
    --secondary-light: #FFD44D;
    --success: #2A9D8F;
    --danger: #E63946;
    --warning: #F4A261;
    --bg: #F0F2F5;
    --card: #FFFFFF;
    --text: #1D1D1F;
    --text-secondary: #6C757D;
    --border: #E9ECEF;
    --shadow: 0 2px 12px rgba(0,0,0,0.06);
    --radius: 16px;
    --radius-sm: 10px;
    --transition: 0.3s cubic-bezier(0.4, 0, 0.2, 1);
    --font: 'Segoe UI', system-ui, -apple-system, sans-serif;
    --nav-height: 64px;
    --header-height: 56px;
}

[data-theme="dark"] {
    --bg: #121212;
    --card: #1E1E1E;
    --text: #E8E8E8;
    --text-secondary: #9CA3AF;
    --border: #2D2D2D;
    --shadow: 0 2px 12px rgba(0,0,0,0.3);
}

* { margin: 0; padding: 0; box-sizing: border-box; }
body {
    font-family: var(--font);
    background: var(--bg);
    color: var(--text);
    transition: background var(--transition), color var(--transition);
    display: flex;
    justify-content: center;
    min-height: 100vh;
    overflow-x: hidden;
}

/* ============================================================
   APP CONTAINER
   ============================================================ */
#app {
    max-width: 430px;
    width: 100%;
    min-height: 100vh;
    background: var(--bg);
    position: relative;
    display: flex;
    flex-direction: column;
    transition: background var(--transition);
    box-shadow: 0 0 40px rgba(0,0,0,0.05);
}

/* ============================================================
   HEADER
   ============================================================ */
.app-header {
    background: var(--card);
    padding: 12px 16px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    border-bottom: 1px solid var(--border);
    position: sticky;
    top: 0;
    z-index: 100;
    min-height: var(--header-height);
    transition: background var(--transition), border var(--transition);
}
.app-header .logo {
    font-size: 20px;
    font-weight: 800;
    color: var(--primary);
    display: flex;
    align-items: center;
    gap: 8px;
}
.app-header .logo i { font-size: 22px; }
.header-actions { display: flex; align-items: center; gap: 12px; }
.header-actions button {
    background: none;
    border: none;
    font-size: 20px;
    color: var(--text-secondary);
    cursor: pointer;
    padding: 4px;
    transition: color var(--transition);
    position: relative;
}
.header-actions button:hover { color: var(--text); }
.badge-dot {
    position: absolute;
    top: 0; right: 0;
    width: 8px; height: 8px;
    background: var(--danger);
    border-radius: 50%;
    border: 2px solid var(--card);
}
.lang-btn {
    font-size: 13px;
    font-weight: 600;
    padding: 4px 10px;
    border-radius: 20px;
    background: var(--bg);
    border: 1px solid var(--border);
    cursor: pointer;
    color: var(--text);
    transition: all var(--transition);
}
.lang-btn:hover { background: var(--border); }

/* ============================================================
   MAIN CONTENT
   ============================================================ */
.main-content {
    flex: 1;
    overflow-y: auto;
    padding: 0 0 80px 0;
    transition: background var(--transition);
}
.main-content::-webkit-scrollbar { width: 0; }

/* ============================================================
   SCREENS
   ============================================================ */
.screen {
    display: none;
    animation: fadeIn 0.3s ease;
    padding: 16px;
}
.screen.active { display: block; }

@keyframes fadeIn {
    from { opacity: 0; transform: translateY(12px); }
    to { opacity: 1; transform: translateY(0); }
}

/* ============================================================
   BOTTOM NAV
   ============================================================ */
.bottom-nav {
    position: fixed;
    bottom: 0;
    left: 50%;
    transform: translateX(-50%);
    width: 100%;
    max-width: 430px;
    background: var(--card);
    border-top: 1px solid var(--border);
    display: flex;
    justify-content: space-around;
    align-items: center;
    padding: 6px 0 env(safe-area-inset-bottom);
    z-index: 200;
    height: var(--nav-height);
    transition: background var(--transition), border var(--transition);
}
.nav-item {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 2px;
    background: none;
    border: none;
    color: var(--text-secondary);
    font-size: 10px;
    cursor: pointer;
    padding: 4px 12px;
    border-radius: 30px;
    transition: all var(--transition);
    position: relative;
}
.nav-item i { font-size: 22px; transition: color var(--transition); }
.nav-item span { font-weight: 500; }
.nav-item.active { color: var(--primary); }
.nav-item.active i { color: var(--primary); }
.nav-item .nav-badge {
    position: absolute;
    top: 0; right: 4px;
    background: var(--danger);
    color: #fff;
    font-size: 9px;
    font-weight: 700;
    border-radius: 50%;
    width: 18px; height: 18px;
    display: flex;
    align-items: center;
    justify-content: center;
}
.nav-post {
    background: var(--primary);
    color: #fff !important;
    width: 48px;
    height: 48px;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    margin-top: -16px;
    box-shadow: 0 4px 16px rgba(26,95,122,0.35);
}
.nav-post i { color: #fff !important; font-size: 26px; }
.nav-post.active { background: var(--primary-dark); }

/* ============================================================
   COMMON COMPONENTS
   ============================================================ */
.card {
    background: var(--card);
    border-radius: var(--radius);
    padding: 16px;
    box-shadow: var(--shadow);
    border: 1px solid var(--border);
    transition: all var(--transition);
}
.card-clickable { cursor: pointer; }
.card-clickable:active { transform: scale(0.98); }

.btn {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
    padding: 10px 20px;
    border-radius: 30px;
    font-weight: 600;
    font-size: 14px;
    border: none;
    cursor: pointer;
    transition: all var(--transition);
    width: 100%;
    font-family: var(--font);
}
.btn:active { transform: scale(0.96); }
.btn-primary { background: var(--primary); color: #fff; }
.btn-primary:hover { background: var(--primary-light); }
.btn-secondary { background: var(--secondary); color: #1D1D1F; }
.btn-secondary:hover { background: var(--secondary-light); }
.btn-success { background: var(--success); color: #fff; }
.btn-danger { background: var(--danger); color: #fff; }
.btn-outline { background: transparent; border: 2px solid var(--primary); color: var(--primary); }
.btn-outline:hover { background: var(--primary); color: #fff; }
.btn-sm { padding: 6px 14px; font-size: 12px; width: auto; }
.btn-block { width: 100%; }
.btn:disabled { opacity: 0.6; cursor: not-allowed; }

.input-group {
    margin-bottom: 14px;
}
.input-group label {
    display: block;
    font-weight: 600;
    font-size: 13px;
    margin-bottom: 4px;
    color: var(--text-secondary);
}
.input-group input,
.input-group textarea,
.input-group select {
    width: 100%;
    padding: 12px 14px;
    border: 1.5px solid var(--border);
    border-radius: var(--radius-sm);
    font-size: 15px;
    background: var(--bg);
    color: var(--text);
    transition: all var(--transition);
    font-family: var(--font);
    outline: none;
}
.input-group input:focus,
.input-group textarea:focus,
.input-group select:focus {
    border-color: var(--primary);
    box-shadow: 0 0 0 3px rgba(26,95,122,0.15);
}
.input-group textarea { min-height: 80px; resize: vertical; }
.input-group select { appearance: auto; }

.chip-group {
    display: flex;
    gap: 8px;
    flex-wrap: wrap;
    margin: 8px 0;
}
.chip {
    padding: 6px 16px;
    border-radius: 30px;
    font-size: 13px;
    font-weight: 500;
    background: var(--bg);
    border: 1.5px solid var(--border);
    cursor: pointer;
    transition: all var(--transition);
    color: var(--text-secondary);
}
.chip.active {
    background: var(--primary);
    color: #fff;
    border-color: var(--primary);
}
.chip:hover:not(.active) { border-color: var(--primary); }

.avatar {
    width: 48px;
    height: 48px;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-weight: 700;
    font-size: 20px;
    color: #fff;
    flex-shrink: 0;
    background: var(--primary);
    overflow: hidden;
    object-fit: cover;
}
.avatar-lg { width: 72px; height: 72px; font-size: 28px; }
.avatar-sm { width: 32px; height: 32px; font-size: 14px; }

.empty-state {
    text-align: center;
    padding: 40px 20px;
    color: var(--text-secondary);
}
.empty-state i { font-size: 48px; margin-bottom: 12px; opacity: 0.3; }
.empty-state h3 { font-size: 18px; color: var(--text); margin-bottom: 4px; }

.badge {
    display: inline-block;
    padding: 2px 10px;
    border-radius: 30px;
    font-size: 11px;
    font-weight: 600;
}
.badge-success { background: #D4EDDA; color: #155724; }
.badge-danger { background: #F8D7DA; color: #721C24; }
.badge-warning { background: #FFF3CD; color: #856404; }
.badge-info { background: #D1ECF1; color: #0C5460; }
.badge-primary { background: #D6EAF8; color: #1A5276; }
.badge-gold { background: #F8B500; color: #1D1D1F; }

.rating-stars {
    color: var(--secondary);
    letter-spacing: 1px;
}
.rating-stars .empty { color: var(--border); }

.divider {
    height: 1px;
    background: var(--border);
    margin: 16px 0;
}

.flex { display: flex; }
.flex-col { flex-direction: column; }
.items-center { align-items: center; }
.justify-between { justify-content: space-between; }
.gap-2 { gap: 8px; }
.gap-3 { gap: 12px; }
.gap-4 { gap: 16px; }
.flex-1 { flex: 1; }
.text-center { text-align: center; }
.text-muted { color: var(--text-secondary); }
.text-sm { font-size: 13px; }
.text-xs { font-size: 11px; }
.font-bold { font-weight: 700; }
.mt-2 { margin-top: 8px; }
.mt-3 { margin-top: 12px; }
.mt-4 { margin-top: 16px; }
.mb-2 { margin-bottom: 8px; }
.mb-3 { margin-bottom: 12px; }
.mb-4 { margin-bottom: 16px; }
.p-2 { padding: 8px; }
.p-3 { padding: 12px; }
.p-4 { padding: 16px; }
.w-full { width: 100%; }
.relative { position: relative; }

.grid-2 { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; }
.grid-3 { display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 10px; }

/* ============================================================
   TOAST
   ============================================================ */
#toast {
    position: fixed;
    top: 20px;
    left: 50%;
    transform: translateX(-50%);
    background: var(--text);
    color: var(--bg);
    padding: 12px 24px;
    border-radius: 30px;
    font-weight: 500;
    font-size: 14px;
    z-index: 9999;
    box-shadow: 0 8px 30px rgba(0,0,0,0.2);
    display: none;
    max-width: 90%;
    text-align: center;
    transition: all var(--transition);
}
#toast.show { display: block; animation: slideDown 0.3s ease; }
@keyframes slideDown {
    from { opacity: 0; transform: translateX(-50%) translateY(-20px); }
    to { opacity: 1; transform: translateX(-50%) translateY(0); }
}

/* ============================================================
   MODAL
   ============================================================ */
.modal-overlay {
    position: fixed;
    top: 0; left: 0; right: 0; bottom: 0;
    background: rgba(0,0,0,0.5);
    backdrop-filter: blur(4px);
    z-index: 500;
    display: none;
    align-items: flex-end;
    justify-content: center;
    animation: fadeIn 0.2s ease;
}
.modal-overlay.show { display: flex; }
.modal-content {
    background: var(--card);
    width: 100%;
    max-width: 430px;
    max-height: 88vh;
    border-radius: 24px 24px 0 0;
    padding: 20px 20px 30px;
    overflow-y: auto;
    animation: slideUp 0.3s ease;
    transition: background var(--transition);
}
@keyframes slideUp {
    from { transform: translateY(40px); opacity: 0; }
    to { transform: translateY(0); opacity: 1; }
}
.modal-handle {
    width: 40px;
    height: 4px;
    background: var(--border);
    border-radius: 4px;
    margin: 0 auto 16px;
}
.modal-close {
    float: right;
    background: none;
    border: none;
    font-size: 24px;
    color: var(--text-secondary);
    cursor: pointer;
    padding: 4px;
}
.modal-close:hover { color: var(--text); }

/* ============================================================
   SCREEN SPECIFIC STYLES
   ============================================================ */

/* Auth */
.auth-screen {
    display: flex;
    flex-direction: column;
    justify-content: center;
    min-height: 70vh;
    padding: 20px 0;
}
.auth-screen .logo-big {
    font-size: 48px;
    font-weight: 800;
    color: var(--primary);
    text-align: center;
    margin-bottom: 8px;
}
.auth-screen .subtitle {
    text-align: center;
    color: var(--text-secondary);
    margin-bottom: 30px;
}
.auth-toggle {
    text-align: center;
    margin-top: 16px;
    font-size: 14px;
    color: var(--text-secondary);
}
.auth-toggle a {
    color: var(--primary);
    font-weight: 600;
    cursor: pointer;
    text-decoration: none;
}

/* Worker Card */
.worker-card {
    background: var(--card);
    border-radius: var(--radius);
    padding: 14px;
    border: 1px solid var(--border);
    display: flex;
    gap: 14px;
    align-items: center;
    transition: all var(--transition);
    cursor: pointer;
}
.worker-card:active { transform: scale(0.98); }
.worker-card .info { flex: 1; }
.worker-card .info h4 {
    font-size: 15px;
    font-weight: 700;
    display: flex;
    align-items: center;
    gap: 6px;
}
.worker-card .info .skill {
    font-size: 13px;
    color: var(--text-secondary);
}
.worker-card .info .rating {
    font-size: 13px;
    color: var(--secondary);
}
.worker-card .info .price {
    font-size: 14px;
    font-weight: 700;
    color: var(--primary);
}
.worker-card .status-dot {
    width: 10px; height: 10px;
    border-radius: 50%;
    display: inline-block;
}
.status-dot.available { background: var(--success); }
.status-dot.busy { background: var(--warning); }
.status-dot.offline { background: var(--text-secondary); }

/* Job Card */
.job-card {
    background: var(--card);
    border-radius: var(--radius);
    padding: 14px;
    border: 1px solid var(--border);
    transition: all var(--transition);
    cursor: pointer;
}
.job-card:active { transform: scale(0.98); }
.job-card .top {
    display: flex;
    justify-content: space-between;
    align-items: start;
}
.job-card .top h4 { font-size: 15px; font-weight: 700; }
.job-card .meta {
    font-size: 13px;
    color: var(--text-secondary);
    margin-top: 4px;
}
.job-card .bottom {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-top: 10px;
}
.job-card .bottom .budget {
    font-weight: 700;
    color: var(--primary);
}

/* Profile */
.profile-header {
    text-align: center;
    padding: 16px 0;
}
.profile-header .name {
    font-size: 22px;
    font-weight: 700;
    margin-top: 8px;
}
.profile-header .role {
    color: var(--text-secondary);
    font-size: 14px;
}
.profile-stats {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 8px;
    margin: 16px 0;
}
.profile-stats .stat {
    background: var(--bg);
    padding: 12px;
    border-radius: var(--radius-sm);
    text-align: center;
}
.profile-stats .stat .num { font-size: 20px; font-weight: 700; }
.profile-stats .stat .label { font-size: 12px; color: var(--text-secondary); }

.tab-bar {
    display: flex;
    gap: 4px;
    background: var(--bg);
    border-radius: var(--radius-sm);
    padding: 4px;
    margin: 12px 0;
}
.tab-bar .tab {
    flex: 1;
    padding: 8px;
    text-align: center;
    border-radius: 8px;
    font-weight: 600;
    font-size: 13px;
    cursor: pointer;
    transition: all var(--transition);
    color: var(--text-secondary);
    border: none;
    background: none;
}
.tab-bar .tab.active {
    background: var(--card);
    color: var(--text);
    box-shadow: 0 2px 8px rgba(0,0,0,0.06);
}
.tab-bar .tab:hover:not(.active) { color: var(--text); }

/* Chat */
.chat-list .chat-item {
    display: flex;
    align-items: center;
    gap: 12px;
    padding: 12px 0;
    border-bottom: 1px solid var(--border);
    cursor: pointer;
}
.chat-list .chat-item:last-child { border-bottom: none; }
.chat-list .chat-item .preview {
    flex: 1;
    font-size: 14px;
    color: var(--text-secondary);
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
}
.chat-list .chat-item .time {
    font-size: 11px;
    color: var(--text-secondary);
}

.chat-messages {
    height: 340px;
    overflow-y: auto;
    padding: 8px 0;
    display: flex;
    flex-direction: column;
    gap: 6px;
}
.chat-messages .msg {
    max-width: 80%;
    padding: 10px 14px;
    border-radius: 18px;
    font-size: 14px;
    word-wrap: break-word;
}
.chat-messages .msg.sent {
    align-self: flex-end;
    background: var(--primary);
    color: #fff;
    border-radius: 18px 18px 4px 18px;
}
.chat-messages .msg.received {
    align-self: flex-start;
    background: var(--bg);
    color: var(--text);
    border-radius: 18px 18px 18px 4px;
}
.chat-input {
    display: flex;
    gap: 10px;
    padding: 10px 0;
}
.chat-input input {
    flex: 1;
    padding: 10px 16px;
    border: 1.5px solid var(--border);
    border-radius: 30px;
    font-size: 14px;
    background: var(--bg);
    color: var(--text);
    outline: none;
    font-family: var(--font);
}
.chat-input input:focus { border-color: var(--primary); }
.chat-input button {
    width: 44px; height: 44px;
    border-radius: 50%;
    background: var(--primary);
    color: #fff;
    border: none;
    font-size: 18px;
    cursor: pointer;
    transition: all var(--transition);
    flex-shrink: 0;
}
.chat-input button:active { transform: scale(0.92); }

/* Notifications */
.notif-item {
    display: flex;
    gap: 12px;
    padding: 12px 0;
    border-bottom: 1px solid var(--border);
    align-items: start;
}
.notif-item:last-child { border-bottom: none; }
.notif-item .icon {
    width: 36px; height: 36px;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-shrink: 0;
    font-size: 16px;
    background: var(--bg);
}
.notif-item .body { flex: 1; }
.notif-item .body .title { font-weight: 600; font-size: 14px; }
.notif-item .body .desc { font-size: 13px; color: var(--text-secondary); }
.notif-item .time { font-size: 11px; color: var(--text-secondary); }
.notif-item.unread .body .title { color: var(--primary); }

/* Emergency */
.emergency-banner {
    background: linear-gradient(135deg, var(--danger), #C0392B);
    color: #fff;
    border-radius: var(--radius);
    padding: 20px;
    text-align: center;
    margin-bottom: 16px;
}
.emergency-banner i { font-size: 32px; margin-bottom: 8px; }
.emergency-banner h3 { font-size: 18px; }

/* AI Assistant */
.ai-bubble {
    background: var(--card);
    border-radius: var(--radius);
    padding: 16px;
    border: 1px solid var(--border);
    margin-bottom: 12px;
    box-shadow: var(--shadow);
}
.ai-bubble .bot {
    display: flex;
    gap: 10px;
    align-items: start;
}
.ai-bubble .bot .icon {
    width: 36px; height: 36px;
    border-radius: 50%;
    background: var(--primary);
    color: #fff;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-shrink: 0;
}
.ai-bubble .bot .text {
    background: var(--bg);
    padding: 10px 14px;
    border-radius: 14px;
    font-size: 14px;
    flex: 1;
}
.ai-bubble .user {
    display: flex;
    gap: 10px;
    align-items: start;
    justify-content: flex-end;
    margin-top: 8px;
}
.ai-bubble .user .text {
    background: var(--primary);
    color: #fff;
    padding: 10px 14px;
    border-radius: 14px;
    font-size: 14px;
    max-width: 80%;
}

/* Admin */
.admin-stat-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 12px;
    margin-bottom: 16px;
}
.admin-stat {
    background: var(--card);
    border-radius: var(--radius-sm);
    padding: 14px;
    border: 1px solid var(--border);
    text-align: center;
}
.admin-stat .num { font-size: 24px; font-weight: 700; color: var(--primary); }
.admin-stat .label { font-size: 12px; color: var(--text-secondary); }

/* Wallet */
.wallet-balance {
    background: linear-gradient(135deg, var(--primary), var(--primary-dark));
    color: #fff;
    border-radius: var(--radius);
    padding: 24px;
    text-align: center;
    margin-bottom: 16px;
}
.wallet-balance .amount { font-size: 36px; font-weight: 800; }
.wallet-balance .label { font-size: 14px; opacity: 0.8; }

/* Subscription */
.plan-card {
    background: var(--card);
    border-radius: var(--radius);
    padding: 16px;
    border: 2px solid var(--border);
    text-align: center;
    transition: all var(--transition);
    cursor: pointer;
}
.plan-card:hover { border-color: var(--primary); }
.plan-card.popular { border-color: var(--secondary); }
.plan-card .name { font-size: 18px; font-weight: 700; }
.plan-card .price { font-size: 24px; font-weight: 800; color: var(--primary); margin: 8px 0; }
.plan-card .features { font-size: 13px; color: var(--text-secondary); }
.plan-card .badge-popular {
    background: var(--secondary);
    color: #1D1D1F;
    padding: 2px 12px;
    border-radius: 30px;
    font-size: 11px;
    font-weight: 700;
    display: inline-block;
    margin-bottom: 8px;
}

/* ============================================================
   RESPONSIVE
   ============================================================ */
@media (max-width: 430px) {
    #app { max-width: 100%; }
    .bottom-nav { max-width: 100%; }
    .modal-content { max-width: 100%; border-radius: 20px 20px 0 0; }
}
@media (min-width: 431px) {
    body { padding: 20px; background: #E8EAED; }
    #app { border-radius: 32px; box-shadow: 0 20px 60px rgba(0,0,0,0.12); overflow: hidden; min-height: 90vh; max-height: 95vh; }
    .bottom-nav { border-radius: 0 0 32px 32px; }
    .main-content { max-height: calc(95vh - var(--header-height) - var(--nav-height)); }
}

/* ============================================================
   SCROLLBAR
   ============================================================ */
::-webkit-scrollbar { width: 4px; }
::-webkit-scrollbar-track { background: var(--bg); }
::-webkit-scrollbar-thumb { background: var(--border); border-radius: 4px; }
::-webkit-scrollbar-thumb:hover { background: var(--text-secondary); }

/* ============================================================
   DARK MODE TOGGLE
   ============================================================ */
.theme-toggle {
    background: none;
    border: none;
    font-size: 20px;
    color: var(--text-secondary);
    cursor: pointer;
    padding: 4px;
    transition: color var(--transition);
}
.theme-toggle:hover { color: var(--text); }
// ============================================================
// STORAGE MODULE – localStorage helpers & demo data
// ============================================================

const DB = {
    getUsers() {
        return JSON.parse(localStorage.getItem('skillconnect_users') || '[]');
    },
    setUsers(users) {
        localStorage.setItem('skillconnect_users', JSON.stringify(users));
    },
    getWorkers() {
        return JSON.parse(localStorage.getItem('skillconnect_workers') || '[]');
    },
    setWorkers(workers) {
        localStorage.setItem('skillconnect_workers', JSON.stringify(workers));
    },
    getJobs() {
        return JSON.parse(localStorage.getItem('skillconnect_jobs') || '[]');
    },
    setJobs(jobs) {
        localStorage.setItem('skillconnect_jobs', JSON.stringify(jobs));
    },
    getBids() {
        return JSON.parse(localStorage.getItem('skillconnect_bids') || '[]');
    },
    setBids(bids) {
        localStorage.setItem('skillconnect_bids', JSON.stringify(bids));
    },
    getReviews() {
        return JSON.parse(localStorage.getItem('skillconnect_reviews') || '[]');
    },
    setReviews(reviews) {
        localStorage.setItem('skillconnect_reviews', JSON.stringify(reviews));
    },
    getNotifications() {
        return JSON.parse(localStorage.getItem('skillconnect_notifications') || '[]');
    },
    setNotifications(notifs) {
        localStorage.setItem('skillconnect_notifications', JSON.stringify(notifs));
    },
    getTransactions() {
        return JSON.parse(localStorage.getItem('skillconnect_transactions') || '[]');
    },
    setTransactions(txns) {
        localStorage.setItem('skillconnect_transactions', JSON.stringify(txns));
    },
    getSubscriptions() {
        return JSON.parse(localStorage.getItem('skillconnect_subscriptions') || '[]');
    },
    setSubscriptions(subs) {
        localStorage.setItem('skillconnect_subscriptions', JSON.stringify(subs));
    },
    getChats() {
        return JSON.parse(localStorage.getItem('skillconnect_chats') || '[]');
    },
    setChats(chats) {
        localStorage.setItem('skillconnect_chats', JSON.stringify(chats));
    },
    getEmergency() {
        return JSON.parse(localStorage.getItem('skillconnect_emergency') || '[]');
    },
    setEmergency(emerg) {
        localStorage.setItem('skillconnect_emergency', JSON.stringify(emerg));
    },
    getSavedWorkers() {
        return JSON.parse(localStorage.getItem('skillconnect_saved') || '[]');
    },
    setSavedWorkers(saved) {
        localStorage.setItem('skillconnect_saved', JSON.stringify(saved));
    },
    getCurrentUser() {
        return JSON.parse(localStorage.getItem('skillconnect_current_user') || 'null');
    },
    setCurrentUser(user) {
        localStorage.setItem('skillconnect_current_user', JSON.stringify(user));
    },
    getLanguage() {
        return localStorage.getItem('skillconnect_lang') || 'en';
    },
    setLanguage(lang) {
        localStorage.setItem('skillconnect_lang', lang);
    },
    getTheme() {
        return localStorage.getItem('skillconnect_theme') || 'light';
    },
    setTheme(theme) {
        localStorage.setItem('skillconnect_theme', theme);
    }
};

function genId() {
    return Date.now().toString(36) + Math.random().toString(36).substr(2, 6);
}

function toast(msg, duration = 3000) {
    const el = document.getElementById('toast');
    el.textContent = msg;
    el.classList.add('show');
    clearTimeout(el._timer);
    el._timer = setTimeout(() => el.classList.remove('show'), duration);
}

function openModal(html) {
    document.getElementById('modalBody').innerHTML = html;
    document.getElementById('modalOverlay').classList.add('show');
}

function closeModal() {
    document.getElementById('modalOverlay').classList.remove('show');
}

function showScreen(id) {
    document.querySelectorAll('.screen').forEach(s => s.classList.remove('active'));
    const target = document.getElementById('screen-' + id);
    if (target) target.classList.add('active');
    document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
    const navBtn = document.querySelector(`.nav-item[data-screen="${id}"]`);
    if (navBtn) navBtn.classList.add('active');
    if (id === 'postjob') {
        document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
        document.querySelector('.nav-post')?.classList.add('active');
    }
    document.getElementById('mainContent').scrollTop = 0;
}

function loadDemoData() {
    if (DB.getUsers().length > 0) return;
    // Create demo users
    const demoUsers = [
        { id: 'u1', name: 'Suresh Kumar', phone: '9876543210', password: 'password123', role: 'worker',
            createdAt: new Date().toISOString() },
        { id: 'u2', name: 'Priya Singh', phone: '9876543211', password: 'password123', role: 'customer',
            createdAt: new Date().toISOString() },
        { id: 'u3', name: 'Rajesh Verma', phone: '9876543212', password: 'password123', role: 'worker',
            createdAt: new Date().toISOString() },
        { id: 'u4', name: 'Aisha Patel', phone: '9876543213', password: 'password123', role: 'customer',
            createdAt: new Date().toISOString() },
        { id: 'u5', name: 'Vikram Reddy', phone: '9876543214', password: 'password123', role: 'worker',
            createdAt: new Date().toISOString() },
        { id: 'admin1', name: 'Admin', phone: '9999999999', password: 'admin123', role: 'admin',
            createdAt: new Date().toISOString() }
    ];
    DB.setUsers(demoUsers);

    const workers = [
        { userId: 'u1', category: 'Plumber', experience: 8, about: 'Expert plumber with 8+ years experience.',
            hourlyRate: 400, availability: 'available', location: 'Indiranagar, Bangalore', portfolio: [
                'https://picsum.photos/seed/plumb1/200/200', 'https://picsum.photos/seed/plumb2/200/200'
            ], certificates: ['Certified Plumber - Govt of India'], isPremium: true, isFeatured: true,
            rating: 4.9, totalJobs: 142, earnings: 56000 },
        { userId: 'u3', category: 'Electrician', experience: 5, about: 'Licensed electrician. Residential and commercial.',
            hourlyRate: 500, availability: 'busy', location: 'Koramangala, Bangalore', portfolio: [
                'https://picsum.photos/seed/elec1/200/200'
            ], certificates: ['BEE Certified Electrician'], isPremium: false, isFeatured: false,
            rating: 4.7, totalJobs: 98, earnings: 42000 },
        { userId: 'u5', category: 'Carpenter', experience: 12, about: 'Master carpenter with 12+ years.',
            hourlyRate: 350, availability: 'available', location: 'Whitefield, Bangalore', portfolio: [
                'https://picsum.photos/seed/carp1/200/200', 'https://picsum.photos/seed/carp2/200/200'
            ], certificates: ['Advanced Carpentry - IIT'], isPremium: true, isFeatured: true, rating: 4.8,
            totalJobs: 210, earnings: 78000 }
    ];
    DB.setWorkers(workers);

    const jobs = [
        { id: 'j1', customerId: 'u2', title: 'Fix leaking kitchen tap', description: 'Kitchen sink tap leaking.',
            category: 'Plumber', location: 'Indiranagar, Bangalore', budget: 500, urgency: 'urgent',
            status: 'open', createdAt: new Date(Date.now() - 3600000).toISOString() },
        { id: 'j2', customerId: 'u4', title: 'AC service and gas refill', description: 'Split AC not cooling.',
            category: 'AC Repair', location: 'Koramangala, Bangalore', budget: 800, urgency: 'normal',
            status: 'in_progress', createdAt: new Date(Date.now() - 7200000).toISOString() },
        { id: 'j3', customerId: 'u2', title: 'New wardrobe installation', description: 'Need a carpenter.',
            category: 'Carpenter', location: 'Whitefield, Bangalore', budget: 1200, urgency: 'normal',
            status: 'open', createdAt: new Date(Date.now() - 86400000).toISOString() }
    ];
    DB.setJobs(jobs);

    const bids = [
        { id: 'b1', jobId: 'j1', workerId: 'u1', amount: 450, message: 'I can fix this in 1 hour.',
            status: 'pending', createdAt: new Date(Date.now() - 1800000).toISOString() },
        { id: 'b2', jobId: 'j1', workerId: 'u3', amount: 400, message: 'Available immediately.',
            status: 'pending', createdAt: new Date(Date.now() - 1200000).toISOString() },
        { id: 'b3', jobId: 'j2', workerId: 'u5', amount: 750, message: 'Can do AC service today.',
            status: 'accepted', createdAt: new Date(Date.now() - 3600000).toISOString() }
    ];
    DB.setBids(bids);

    const reviews = [
        { id: 'r1', fromUserId: 'u2', toUserId: 'u1', jobId: 'j1', rating: 5,
            comment: 'Excellent work! Very professional.', createdAt: new Date(Date.now() - 172800000)
            .toISOString() },
        { id: 'r2', fromUserId: 'u4', toUserId: 'u3', jobId: 'j2', rating: 4,
            comment: 'Good but a bit late.', createdAt: new Date(Date.now() - 86400000).toISOString() }
    ];
    DB.setReviews(reviews);

    const notifs = [
        { id: 'n1', userId: 'u2', title: 'New Bid', message: 'Suresh placed a bid on your job',
            read: false, createdAt: new Date(Date.now() - 600000).toISOString() },
        { id: 'n2', userId: 'u1', title: 'Bid Accepted', message: 'Your bid was accepted',
            read: false, createdAt: new Date(Date.now() - 1800000).toISOString() }
    ];
    DB.setNotifications(notifs);

    const txns = [
        { id: 't1', userId: 'u2', amount: 500, type: 'deposit', description: 'Wallet top-up',
            createdAt: new Date(Date.now() - 86400000).toISOString() },
        { id: 't2', userId: 'u1', amount: 450, type: 'earnings', description: 'Job payment - Fix leaking tap',
            createdAt: new Date(Date.now() - 172800000).toISOString() }
    ];
    DB.setTransactions(txns);

    const subs = [
        { id: 's1', workerId: 'u1', plan: 'pro', startDate: new Date(Date.now() - 2592000000).toISOString(),
            endDate: new Date(Date.now() + 2592000000).toISOString(), active: true },
        { id: 's2', workerId: 'u5', plan: 'business', startDate: new Date(Date.now() - 5184000000)
                .toISOString(), endDate: new Date(Date.now() + 5184000000).toISOString(),
            active: true }
    ];
    DB.setSubscriptions(subs);

    const chats = [
        { id: 'c1', jobId: 'j1', participants: ['u2', 'u1'], messages: [
                { senderId: 'u1', content: 'Hi, I can fix your tap today. Is 2 PM good?', timestamp: new Date(
                        Date.now() - 900000).toISOString() },
                { senderId: 'u2', content: 'Yes, 2 PM works.', timestamp: new Date(Date.now() - 600000)
                    .toISOString() }
            ] },
        { id: 'c2', jobId: 'j2', participants: ['u4', 'u3'], messages: [
                { senderId: 'u3', content: 'I can service your AC tomorrow morning.', timestamp: new Date(
                        Date.now() - 3600000).toISOString() },
                { senderId: 'u4', content: 'Great! Please come by 9 AM.', timestamp: new Date(Date.now() -
                        3000000).toISOString() }
            ] }
    ];
    DB.setChats(chats);

    const saved = [{ customerId: 'u2', workerId: 'u1' }, { customerId: 'u2', workerId: 'u5' }];
    DB.setSavedWorkers(saved);

    const emergency = [
        { id: 'e1', userId: 'u4', description: 'Water pipe burst', location: 'Koramangala',
            status: 'resolved', createdAt: new Date(Date.now() - 86400000).toISOString() }
    ];
    DB.setEmergency(emergency);
}
// ============================================================
// AUTH MODULE – Login, Register, OTP, Logout
// ============================================================

function handleLogin() {
    const phone = document.getElementById('loginPhone').value.trim();
    const password = document.getElementById('loginPassword').value.trim();
    if (!phone || !password) return toast('Please fill all fields');
    const users = DB.getUsers();
    const user = users.find(u => u.phone === phone && u.password === password);
    if (!user) return toast('Invalid credentials');
    DB.setCurrentUser(user);
    toast('Welcome back, ' + user.name + '!');
    loadDemoData();
    navigateTo('home');
}

function handleOTPLogin() {
    const phone = document.getElementById('loginPhone').value.trim();
    if (!phone) return toast('Enter phone number');
    const otp = prompt('Enter OTP (demo: 123456)');
    if (otp === '123456') {
        let users = DB.getUsers();
        let user = users.find(u => u.phone === phone);
        if (!user) {
            user = { id: genId(), name: 'User', phone, password: '', role: 'customer', createdAt: new Date()
                    .toISOString() };
            users.push(user);
            DB.setUsers(users);
        }
        DB.setCurrentUser(user);
        toast('OTP verified! Welcome.');
        loadDemoData();
        navigateTo('home');
    } else {
        toast('Invalid OTP. Use 123456');
    }
}

function handleRegister() {
    const name = document.getElementById('regName').value.trim();
    const phone = document.getElementById('regPhone').value.trim();
    const password = document.getElementById('regPassword').value.trim();
    const role = document.getElementById('regRole').value;
    if (!name || !phone || !password) return toast('Please fill all fields');
    const users = DB.getUsers();
    if (users.find(u => u.phone === phone)) return toast('Phone already registered');
    const user = { id: genId(), name, phone, password, role, createdAt: new Date().toISOString() };
    users.push(user);
    DB.setUsers(users);
    if (role === 'worker') {
        const workers = DB.getWorkers();
        workers.push({
            userId: user.id,
            category: '',
            experience: 0,
            about: '',
            hourlyRate: 0,
            availability: 'available',
            location: 'Bangalore',
            portfolio: [],
            certificates: [],
            isPremium: false,
            isFeatured: false,
            rating: 0,
            totalJobs: 0,
            earnings: 0
        });
        DB.setWorkers(workers);
    }
    DB.setCurrentUser(user);
    toast('Account created! Welcome ' + name);
    loadDemoData();
    navigateTo('home');
}

function logout() {
    DB.setCurrentUser(null);
    toast('Logged out');
    showScreen('login');
}
// ============================================================
// WORKERS MODULE – Display, Search, Profile, Save, Hire
// ============================================================

function workerCardHTML(w, lang) {
    const user = DB.getUsers().find(u => u.id === w.userId);
    const name = user ? user.name : 'Worker';
    const rating = w.rating || 0;
    const stars = '★'.repeat(Math.floor(rating)) + '☆'.repeat(5 - Math.floor(rating));
    const statusText = lang === 'hi' ? { available: 'उपलब्ध', busy: 'व्यस्त', offline: 'ऑफलाइन' } : { available: 'Available',
        busy: 'Busy', offline: 'Offline' };
    const statusClass = w.availability || 'offline';
    return `
        <div class="worker-card" onclick="viewWorkerProfile('${w.userId}')">
            <div class="avatar" style="background:${w.isPremium ? 'var(--secondary)' : 'var(--primary)'};">
                ${name.charAt(0)}
            </div>
            <div class="info">
                <h4>
                    ${name}
                    ${w.isPremium ? '<span style="font-size:12px;color:var(--secondary);"><i class="fas fa-crown"></i></span>' : ''}
                    ${w.isFeatured ? '<span style="font-size:12px;color:var(--primary);"><i class="fas fa-star"></i></span>' : ''}
                </h4>
                <div class="skill">${w.category || 'Skilled'} • ${w.location || 'Bangalore'}</div>
                <div>
                    <span class="rating">${stars} ${rating.toFixed(1)}</span>
                    <span class="price" style="margin-left:10px;">₹${w.hourlyRate || 0}/hr</span>
                </div>
            </div>
            <div style="text-align:right;">
                <span class="status-dot ${statusClass}"></span>
                <div style="font-size:11px;color:var(--text-secondary);">${statusText[statusClass] || statusClass}</div>
            </div>
        </div>
    `;
}

function viewWorkerProfile(userId) {
    const user = DB.getUsers().find(u => u.id === userId);
    const worker = DB.getWorkers().find(w => w.userId === userId);
    if (!user || !worker) return toast('Worker not found');
    const lang = DB.getLanguage();
    const t = lang === 'hi' ? {
        about: 'के बारे में',
        experience: 'अनुभव',
        years: 'साल',
        rate: 'दर',
        availability: 'उपलब्धता',
        portfolio: 'पोर्टफोलियो',
        certificates: 'प्रमाणपत्र',
        reviews: 'समीक्षाएँ',
        hire: 'काम पर रखें',
        save: 'सेव करें',
        message: 'संदेश भेजें',
        rating: 'रेटिंग',
        jobsDone: 'काम पूरे किए'
    } : {
        about: 'About',
        experience: 'Experience',
        years: 'years',
        rate: 'Rate',
        availability: 'Availability',
        portfolio: 'Portfolio',
        certificates: 'Certificates',
        reviews: 'Reviews',
        hire: 'Hire',
        save: 'Save',
        message: 'Message',
        rating: 'Rating',
        jobsDone: 'Jobs Done'
    };

    const reviews = DB.getReviews().filter(r => r.toUserId === userId);
    const avgRating = reviews.length > 0 ? (reviews.reduce((s, r) => s + r.rating, 0) / reviews.length) : 0;
    const stars = '★'.repeat(Math.floor(avgRating)) + '☆'.repeat(5 - Math.floor(avgRating));
    const isSaved = DB.getSavedWorkers().some(s => s.customerId === DB.getCurrentUser()?.id && s.workerId === userId);

    const html = `
        <div style="display:flex;align-items:center;gap:12px;margin-bottom:16px;">
            <button onclick="navigateTo('home')" style="background:none;border:none;font-size:20px;color:var(--text-secondary);cursor:pointer;"><i class="fas fa-arrow-left"></i></button>
            <h2 style="font-size:20px;font-weight:700;">${user.name}</h2>
        </div>
        <div class="card" style="text-align:center;padding:20px;">
            <div class="avatar avatar-lg" style="margin:0 auto;background:${worker.isPremium ? 'var(--secondary)' : 'var(--primary)'};font-size:32px;">
                ${user.name.charAt(0)}
            </div>
            <h3 style="font-size:20px;font-weight:700;margin-top:8px;">${user.name}</h3>
            <div style="color:var(--text-secondary);">${worker.category || 'Skilled Worker'}</div>
            <div style="margin-top:4px;">
                <span class="status-dot ${worker.availability || 'offline'}"></span>
                <span style="font-size:13px;color:var(--text-secondary);">${worker.availability || 'Offline'}</span>
                ${worker.isPremium ? '<span style="margin-left:8px;font-size:13px;color:var(--secondary);"><i class="fas fa-crown"></i> Premium</span>' : ''}
                ${worker.isFeatured ? '<span style="margin-left:8px;font-size:13px;color:var(--primary);"><i class="fas fa-star"></i> Featured</span>' : ''}
            </div>
            <div style="margin-top:8px;">
                <span style="color:var(--secondary);font-size:18px;">${stars}</span>
                <span style="font-size:13px;color:var(--text-secondary);">(${reviews.length} ${t.reviews})</span>
            </div>
        </div>

        <div style="display:grid;grid-template-columns:1fr 1fr 1fr;gap:8px;margin:12px 0;">
            <div class="card" style="text-align:center;padding:12px;"><div style="font-weight:700;font-size:18px;">${worker.experience || 0}</div><div style="font-size:12px;color:var(--text-secondary);">${t.years}</div></div>
            <div class="card" style="text-align:center;padding:12px;"><div style="font-weight:700;font-size:18px;">₹${worker.hourlyRate || 0}</div><div style="font-size:12px;color:var(--text-secondary);">${t.rate}/hr</div></div>
            <div class="card" style="text-align:center;padding:12px;"><div style="font-weight:700;font-size:18px;">${worker.totalJobs || 0}</div><div style="font-size:12px;color:var(--text-secondary);">${t.jobsDone}</div></div>
        </div>

        ${worker.about ? `<div class="card" style="margin:8px 0;"><strong>${t.about}</strong><p style="color:var(--text-secondary);font-size:14px;margin-top:4px;">${worker.about}</p></div>` : ''}

        ${worker.portfolio && worker.portfolio.length > 0 ? `
            <div style="margin:8px 0;">
                <strong>${t.portfolio}</strong>
                <div style="display:grid;grid-template-columns:1fr 1fr;gap:8px;margin-top:6px;">
                    ${worker.portfolio.map(url => `<img src="${url}" style="width:100%;height:120px;object-fit:cover;border-radius:var(--radius-sm);border:1px solid var(--border);" onerror="this.style.display='none'">`).join('')}
                </div>
            </div>
        ` : ''}

        ${worker.certificates && worker.certificates.length > 0 ? `
            <div style="margin:8px 0;">
                <strong>${t.certificates}</strong>
                <div style="display:flex;flex-wrap:wrap;gap:6px;margin-top:4px;">
                    ${worker.certificates.map(c => `<span style="background:var(--bg);padding:4px 12px;border-radius:30px;font-size:13px;">📜 ${c}</span>`).join('')}
                </div>
            </div>
        ` : ''}

        <div style="display:flex;gap:8px;margin-top:16px;flex-wrap:wrap;">
            <button class="btn btn-primary" style="flex:1;" onclick="hireWorker('${userId}')"><i class="fas fa-handshake"></i> ${t.hire}</button>
            <button class="btn btn-outline" style="flex:1;" onclick="toggleSaveWorker('${userId}')">
                <i class="fas ${isSaved ? 'fa-heart' : 'fa-heart-o'}"></i> ${isSaved ? 'Saved' : t.save}
            </button>
            <button class="btn btn-secondary" style="flex:1;" onclick="messageWorker('${userId}')"><i class="fas fa-comment"></i> ${t.message}</button>
        </div>

        <div style="margin-top:16px;">
            <strong>${t.reviews}</strong>
            ${reviews.map(r => {
                const from = DB.getUsers().find(u => u.id === r.fromUserId);
                const s = '★'.repeat(r.rating) + '☆'.repeat(5 - r.rating);
                return `
                    <div style="background:var(--card);border-radius:var(--radius-sm);padding:10px;border:1px solid var(--border);margin-top:6px;">
                        <div style="display:flex;justify-content:space-between;align-items:center;">
                            <span style="font-weight:600;">${from ? from.name : 'User'}</span>
                            <span style="color:var(--secondary);">${s}</span>
                        </div>
                        <div style="font-size:13px;color:var(--text-secondary);">${r.comment || ''}</div>
                    </div>
                `;
            }).join('')}
            ${reviews.length === 0 ? '<div style="color:var(--text-secondary);font-size:13px;margin-top:4px;">No reviews yet</div>' : ''}
        </div>
    `;
    document.getElementById('workerProfileContent').innerHTML = html;
    showScreen('workerprofile');
}

function toggleSaveWorker(workerId) {
    const user = DB.getCurrentUser();
    if (!user) return toast('Please login');
    let saved = DB.getSavedWorkers();
    const exists = saved.some(s => s.customerId === user.id && s.workerId === workerId);
    if (exists) {
        saved = saved.filter(s => !(s.customerId === user.id && s.workerId === workerId));
        toast('Removed from saved');
    } else {
        saved.push({ customerId: user.id, workerId });
        toast('Saved!');
    }
    DB.setSavedWorkers(saved);
    viewWorkerProfile(workerId);
}

function hireWorker(workerId) {
    const user = DB.getCurrentUser();
    if (!user) return toast('Please login');
    if (user.role === 'worker') return toast('Workers can\'t hire');
    navigateTo('postjob');
    toast('Post a job to hire this worker');
}

function messageWorker(workerId) {
    const user = DB.getCurrentUser();
    if (!user) return toast('Please login');
    const worker = DB.getUsers().find(u => u.id === workerId);
    if (!worker) return toast('Worker not found');
    let chats = DB.getChats();
    let chat = chats.find(c => c.participants.includes(user.id) && c.participants.includes(workerId));
    if (!chat) {
        chat = { id: genId(), jobId: null, participants: [user.id, workerId], messages: [] };
        chats.push(chat);
        DB.setChats(chats);
    }
    toast('Chat opened!');
    navigateTo('chat');
    setTimeout(() => {
        const found = DB.getChats().find(c => c.participants.includes(user.id) && c.participants.includes(workerId));
        if (found) {
            renderChat();
            openChatRoom(found.id);
        }
    }, 100);
}
// ============================================================
// JOBS MODULE – Post, View, Edit, Delete, Bidding
// ============================================================

function jobCardHTML(j, lang) {
    const statusMap = { open: 'Open', in_progress: 'In Progress', completed: 'Completed', cancelled: 'Cancelled' };
    const statusMapHi = { open: 'खुला', in_progress: 'प्रगति में', completed: 'पूरा हुआ', cancelled: 'रद्द' };
    const isHi = DB.getLanguage() === 'hi';
    const status = isHi ? statusMapHi[j.status] || j.status : statusMap[j.status] || j.status;
    const urgencyColor = j.urgency === 'emergency' ? 'var(--danger)' : j.urgency === 'urgent' ? 'var(--warning)' :
    'var(--success)';
    return `
        <div class="job-card" onclick="viewJobDetail('${j.id}')">
            <div class="top">
                <h4>${j.title}</h4>
                <span style="font-size:11px;background:var(--bg);padding:2px 10px;border-radius:30px;">${status}</span>
            </div>
            <div class="meta">${j.category} • ${j.location || 'Bangalore'}</div>
            <div class="bottom">
                <span class="budget">₹${j.budget}</span>
                <span style="font-size:11px;color:${urgencyColor};font-weight:600;">
                    ${j.urgency === 'emergency' ? '🚨 Emergency' : j.urgency === 'urgent' ? '⚠️ Urgent' : '📋 Normal'}
                </span>
            </div>
        </div>
    `;
}

function submitJob() {
    const user = DB.getCurrentUser();
    if (!user) return toast('Please login');
    const title = document.getElementById('jobTitle').value.trim();
    const category = document.getElementById('jobCategory').value;
    const description = document.getElementById('jobDesc').value.trim();
    const budget = parseFloat(document.getElementById('jobBudget').value) || 0;
    const location = document.getElementById('jobLocation').value.trim() || 'Bangalore';
    const urgent = document.getElementById('jobUrgent').checked;
    if (!title) return toast('Please enter a job title');
    const jobs = DB.getJobs();
    const job = {
        id: genId(),
        customerId: user.id,
        title,
        category,
        description: description || 'No description provided',
        location,
        budget,
        urgency: urgent ? 'emergency' : 'normal',
        status: 'open',
        createdAt: new Date().toISOString()
    };
    jobs.unshift(job);
    DB.setJobs(jobs);
    toast('✅ Job posted successfully!');
    const workers = DB.getWorkers();
    workers.forEach(w => {
        const notifs = DB.getNotifications();
        notifs.push({
            id: genId(),
            userId: w.userId,
            title: 'New Job Posted',
            message: `New job: ${title} - ₹${budget}`,
            read: false,
            createdAt: new Date().toISOString()
        });
        DB.setNotifications(notifs);
    });
    navigateTo('home');
}

function viewJobDetail(jobId) {
    const job = DB.getJobs().find(j => j.id === jobId);
    if (!job) return toast('Job not found');
    const user = DB.getCurrentUser();
    const lang = DB.getLanguage();
    const t = lang === 'hi' ? {
        budget: 'बजट',
        location: 'स्थान',
        status: 'स्थिति',
        urgency: 'आपातकालीन',
        bids: 'बोलियाँ',
        noBids: 'अभी कोई बोली नहीं',
        placeBid: 'बोली लगाएं',
        accept: 'स्वीकार करें',
        reject: 'अस्वीकार करें',
        amount: 'राशि (₹)',
        time: 'समय',
        message: 'संदेश',
        submit: 'बोली भेजें',
        edit: 'संपादित करें',
        delete: 'हटाएं',
        confirmDelete: 'क्या आप यह काम हटाना चाहते हैं?'
    } : {
        budget: 'Budget',
        location: 'Location',
        status: 'Status',
        urgency: 'Urgency',
        bids: 'Bids',
        noBids: 'No bids yet',
        placeBid: 'Place a Bid',
        accept: 'Accept',
        reject: 'Reject',
        amount: 'Amount (₹)',
        time: 'Time',
        message: 'Message',
        submit: 'Submit Bid',
        edit: 'Edit',
        delete: 'Delete',
        confirmDelete: 'Are you sure you want to delete this job?'
    };

    const customer = DB.getUsers().find(u => u.id === job.customerId);
    const bids = DB.getBids().filter(b => b.jobId === jobId);

    const html = `
        <div style="display:flex;align-items:center;gap:12px;margin-bottom:12px;">
            <button onclick="navigateTo('home')" style="background:none;border:none;font-size:20px;color:var(--text-secondary);cursor:pointer;"><i class="fas fa-arrow-left"></i></button>
            <h2 style="font-size:18px;font-weight:700;flex:1;">${job.title}</h2>
            ${user && (user.id === job.customerId || user.role === 'admin') ? `
                <button onclick="editJob('${jobId}')" style="background:none;border:none;color:var(--primary);cursor:pointer;"><i class="fas fa-edit"></i></button>
                <button onclick="deleteJob('${jobId}')" style="background:none;border:none;color:var(--danger);cursor:pointer;"><i class="fas fa-trash"></i></button>
            ` : ''}
        </div>

        <div class="card" style="margin-bottom:12px;">
            <div style="display:flex;justify-content:space-between;flex-wrap:wrap;gap:8px;">
                <div><span style="color:var(--text-secondary);">${t.status}:</span> <span class="badge badge-${job.status === 'open' ? 'success' : job.status === 'in_progress' ? 'warning' : 'info'}">${job.status}</span></div>
                <div><span style="color:var(--text-secondary);">${t.urgency}:</span> <span style="color:${job.urgency === 'emergency' ? 'var(--danger)' : 'var(--warning)'};">${job.urgency}</span></div>
            </div>
            <div style="margin-top:8px;"><span style="color:var(--text-secondary);">${t.budget}:</span> <strong>₹${job.budget}</strong></div>
            <div><span style="color:var(--text-secondary);">${t.location}:</span> ${job.location || 'Bangalore'}</div>
            <div><span style="color:var(--text-secondary);">Posted by:</span> ${customer ? customer.name : 'Unknown'}</div>
            <div style="margin-top:8px;padding:8px;background:var(--bg);border-radius:var(--radius-sm);font-size:14px;color:var(--text-secondary);">${job.description || 'No description'}</div>
        </div>

        <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:8px;">
            <h3 style="font-size:16px;font-weight:700;">${t.bids} (${bids.length})</h3>
            ${user && user.id !== job.customerId && user.role !== 'admin' ? `<button class="btn btn-primary btn-sm" onclick="openBidModal('${jobId}')">${t.placeBid}</button>` : ''}
        </div>

        <div id="bidsList" style="display:flex;flex-direction:column;gap:8px;">
            ${bids.map(b => {
                const worker = DB.getUsers().find(u => u.id === b.workerId);
                const w = DB.getWorkers().find(w => w.userId === b.workerId);
                return `
                    <div class="card" style="padding:12px;">
                        <div style="display:flex;justify-content:space-between;align-items:center;">
                            <div>
                                <strong>${worker ? worker.name : 'Worker'}</strong>
                                <div style="font-size:13px;color:var(--text-secondary);">${w?.category || 'Skilled'}</div>
                            </div>
                            <div style="text-align:right;">
                                <div style="font-weight:700;color:var(--primary);">₹${b.amount}</div>
                                <div style="font-size:12px;color:var(--text-secondary);">${b.estimatedTime || '1 hr'}</div>
                            </div>
                        </div>
                        ${b.message ? `<div style="font-size:13px;color:var(--text-secondary);margin-top:4px;">"${b.message}"</div>` : ''}
                        <div style="display:flex;gap:6px;margin-top:6px;flex-wrap:wrap;">
                            <span class="badge badge-${b.status === 'pending' ? 'warning' : b.status === 'accepted' ? 'success' : 'danger'}">${b.status}</span>
                            ${user && user.id === job.customerId && b.status === 'pending' ? `
                                <button class="btn btn-success btn-sm" onclick="acceptBid('${b.id}','${jobId}')">${t.accept}</button>
                                <button class="btn btn-danger btn-sm" onclick="rejectBid('${b.id}','${jobId}')">${t.reject}</button>
                            ` : ''}
                        </div>
                    </div>
                `;
            }).join('')}
            ${bids.length === 0 ? `<div class="empty-state"><i class="fas fa-gavel"></i><h3>${t.noBids}</h3></div>` : ''}
        </div>
    `;
    document.getElementById('jobDetailContent').innerHTML = html;
    showScreen('jobdetail');
}

function openBidModal(jobId) {
    const lang = DB.getLanguage();
    const t = lang === 'hi' ? {
        amount: 'राशि (₹)',
        time: 'अनुमानित समय',
        message: 'संदेश (वैकल्पिक)',
        submit: 'बोली भेजें'
    } : {
        amount: 'Amount (₹)',
        time: 'Estimated Time',
        message: 'Message (optional)',
        submit: 'Submit Bid'
    };
    openModal(`
        <h3 style="font-size:18px;font-weight:700;margin-bottom:12px;">Place a Bid</h3>
        <div class="input-group">
            <label>${t.amount}</label>
            <input id="bidAmount" type="number" placeholder="500">
        </div>
        <div class="input-group">
            <label>${t.time}</label>
            <input id="bidTime" placeholder="e.g. 2 hours">
        </div>
        <div class="input-group">
            <label>${t.message}</label>
            <textarea id="bidMessage" rows="2" placeholder="Your message..."></textarea>
        </div>
        <button class="btn btn-primary" onclick="submitBid('${jobId}')">${t.submit}</button>
    `);
}

function submitBid(jobId) {
    const user = DB.getCurrentUser();
    if (!user) return toast('Please login');
    const amount = parseFloat(document.getElementById('bidAmount').value);
    const estimatedTime = document.getElementById('bidTime').value.trim() || '1 hour';
    const message = document.getElementById('bidMessage').value.trim();
    if (!amount || amount <= 0) return toast('Please enter a valid amount');
    const bids = DB.getBids();
    if (bids.find(b => b.jobId === jobId && b.workerId === user.id)) {
        return toast('You already bid on this job');
    }
    bids.push({
        id: genId(),
        jobId,
        workerId: user.id,
        amount,
        estimatedTime,
        message,
        status: 'pending',
        createdAt: new Date().toISOString()
    });
    DB.setBids(bids);
    const job = DB.getJobs().find(j => j.id === jobId);
    if (job) {
        const notifs = DB.getNotifications();
        notifs.push({
            id: genId(),
            userId: job.customerId,
            title: 'New Bid',
            message: `${user.name} placed a bid of ₹${amount} on "${job.title}"`,
            read: false,
            createdAt: new Date().toISOString()
        });
        DB.setNotifications(notifs);
    }
    closeModal();
    toast('✅ Bid placed successfully!');
    viewJobDetail(jobId);
}

function acceptBid(bidId, jobId) {
    const bids = DB.getBids();
    const bid = bids.find(b => b.id === bidId);
    if (!bid) return toast('Bid not found');
    bid.status = 'accepted';
    DB.setBids(bids);
    const jobs = DB.getJobs();
    const job = jobs.find(j => j.id === jobId);
    if (job) job.status = 'in_progress';
    DB.setJobs(jobs);
    const notifs = DB.getNotifications();
    notifs.push({
        id: genId(),
        userId: bid.workerId,
        title: 'Bid Accepted!',
        message: `Your bid for "${job?.title || 'job'}" has been accepted.`,
        read: false,
        createdAt: new Date().toISOString()
    });
    DB.setNotifications(notifs);
    toast('✅ Bid accepted!');
    viewJobDetail(jobId);
}

function rejectBid(bidId, jobId) {
    const bids = DB.getBids();
    const bid = bids.find(b => b.id === bidId);
    if (!bid) return toast('Bid not found');
    bid.status = 'rejected';
    DB.setBids(bids);
    toast('Bid rejected');
    viewJobDetail(jobId);
}

function editJob(jobId) {
    const job = DB.getJobs().find(j => j.id === jobId);
    if (!job) return toast('Job not found');
    openModal(`
        <h3 style="font-size:18px;font-weight:700;margin-bottom:12px;">Edit Job</h3>
        <div class="input-group"><label>Title</label><input id="editJobTitle" value="${job.title}"></div>
        <div class="input-group"><label>Category</label><select id="editJobCategory">
            <option ${job.category==='Plumber'?'selected':''}>Plumber</option>
            <option ${job.category==='Electrician'?'selected':''}>Electrician</option>
            <option ${job.category==='Carpenter'?'selected':''}>Carpenter</option>
            <option ${job.category==='Painter'?'selected':''}>Painter</option>
            <option ${job.category==='Cleaner'?'selected':''}>Cleaner</option>
            <option ${job.category==='AC Repair'?'selected':''}>AC Repair</option>
        </select></div>
        <div class="input-group"><label>Description</label><textarea id="editJobDesc" rows="3">${job.description}</textarea></div>
        <div class="input-group"><label>Budget (₹)</label><input id="editJobBudget" type="number" value="${job.budget}"></div>
        <div class="input-group"><label>Location</label><input id="editJobLocation" value="${job.location}"></div>
        <button class="btn btn-primary" onclick="saveJobEdit('${jobId}')">Save Changes</button>
    `);
}

function saveJobEdit(jobId) {
    const jobs = DB.getJobs();
    const job = jobs.find(j => j.id === jobId);
    if (!job) return toast('Job not found');
    const title = document.getElementById('editJobTitle').value.trim();
    const category = document.getElementById('editJobCategory').value;
    const description = document.getElementById('editJobDesc').value.trim();
    const budget = parseFloat(document.getElementById('editJobBudget').value) || 0;
    const location = document.getElementById('editJobLocation').value.trim() || 'Bangalore';
    if (!title) return toast('Title is required');
    job.title = title;
    job.category = category;
    job.description = description;
    job.budget = budget;
    job.location = location;
    DB.setJobs(jobs);
    closeModal();
    toast('✅ Job updated!');
    viewJobDetail(jobId);
}

function deleteJob(jobId) {
    if (!confirm('Are you sure you want to delete this job?')) return;
    let jobs = DB.getJobs();
    jobs = jobs.filter(j => j.id !== jobId);
    DB.setJobs(jobs);
    toast('Job deleted');
    navigateTo('home');
}
// ============================================================
// ADMIN MODULE – Dashboard, Users, Workers, Data Reset
// ============================================================

function renderAdmin() {
    const user = DB.getCurrentUser();
    if (!user || user.role !== 'admin') {
        document.getElementById('adminContent').innerHTML =
            '<div class="empty-state"><i class="fas fa-lock"></i><h3>Admin Access Only</h3></div>';
        return;
    }
    const users = DB.getUsers();
    const workers = DB.getWorkers();
    const jobs = DB.getJobs();
    const bids = DB.getBids();
    const reviews = DB.getReviews();
    const txns = DB.getTransactions();
    const totalEarnings = txns.filter(t => t.type === 'earnings').reduce((s, t) => s + t.amount, 0);

    const lang = DB.getLanguage();
    const t = lang === 'hi' ? {
        dashboard: '📊 डैशबोर्ड',
        users: 'उपयोगकर्ता',
        workers: 'कर्मचारी',
        jobs: 'काम',
        bids: 'बोलियाँ',
        reviews: 'समीक्षाएँ',
        earnings: 'कमाई',
        recent: 'हाल की गतिविधि'
    } : {
        dashboard: '📊 Dashboard',
        users: 'Users',
        workers: 'Workers',
        jobs: 'Jobs',
        bids: 'Bids',
        reviews: 'Reviews',
        earnings: 'Earnings',
        recent: 'Recent Activity'
    };

    const html = `
        <h2 style="font-size:20px;font-weight:700;">${t.dashboard}</h2>
        <div class="admin-stat-grid">
            <div class="admin-stat"><div class="num">${users.length}</div><div class="label">${t.users}</div></div>
            <div class="admin-stat"><div class="num">${workers.length}</div><div class="label">${t.workers}</div></div>
            <div class="admin-stat"><div class="num">${jobs.length}</div><div class="label">${t.jobs}</div></div>
            <div class="admin-stat"><div class="num">${bids.length}</div><div class="label">${t.bids}</div></div>
            <div class="admin-stat"><div class="num">${reviews.length}</div><div class="label">${t.reviews}</div></div>
            <div class="admin-stat"><div class="num">₹${totalEarnings.toFixed(0)}</div><div class="label">${t.earnings}</div></div>
        </div>

        <div style="margin-top:12px;">
            <h4 style="font-weight:600;margin-bottom:8px;">${t.recent}</h4>
            ${jobs.slice(0,5).map(j => `
                <div style="display:flex;justify-content:space-between;padding:8px 0;border-bottom:1px solid var(--border);font-size:14px;">
                    <span>${j.title}</span>
                    <span class="badge badge-${j.status === 'open' ? 'success' : j.status === 'in_progress' ? 'warning' : 'info'}">${j.status}</span>
                </div>
            `).join('')}
            ${jobs.length === 0 ? '<div style="color:var(--text-secondary);">No jobs yet</div>' : ''}
        </div>

        <div style="margin-top:12px;display:flex;gap:8px;flex-wrap:wrap;">
            <button class="btn btn-primary btn-sm" onclick="viewAllUsers()"><i class="fas fa-users"></i> View Users</button>
            <button class="btn btn-secondary btn-sm" onclick="viewAllWorkers()"><i class="fas fa-hard-hat"></i> View Workers</button>
            <button class="btn btn-outline btn-sm" onclick="clearAllData()"><i class="fas fa-trash"></i> Reset Data</button>
        </div>
    `;
    document.getElementById('adminContent').innerHTML = html;
}

function viewAllUsers() {
    const users = DB.getUsers();
    const html = `
        <h3 style="font-size:18px;font-weight:700;">All Users</h3>
        ${users.map(u => `
            <div style="display:flex;justify-content:space-between;padding:8px 0;border-bottom:1px solid var(--border);">
                <div><strong>${u.name}</strong> (${u.role})</div>
                <div style="font-size:13px;color:var(--text-secondary);">${u.phone}</div>
            </div>
        `).join('')}
    `;
    openModal(html);
}

function viewAllWorkers() {
    const workers = DB.getWorkers();
    const html = `
        <h3 style="font-size:18px;font-weight:700;">All Workers</h3>
        ${workers.map(w => {
            const u = DB.getUsers().find(u => u.id === w.userId);
            return `
                <div style="display:flex;justify-content:space-between;padding:8px 0;border-bottom:1px solid var(--border);">
                    <div><strong>${u ? u.name : 'Unknown'}</strong> - ${w.category || 'Skilled'}</div>
                    <div style="font-size:13px;color:var(--text-secondary);">₹${w.hourlyRate}/hr • ${w.availability}</div>
                </div>
            `;
        }).join('')}
    `;
    openModal(html);
}

function clearAllData() {
    if (confirm('Are you sure you want to delete all data? This cannot be undone.')) {
        localStorage.clear();
        toast('All data cleared. Reloading...');
        setTimeout(() => location.reload(), 1000);
    }
}
// ============================================================
// NOTIFICATIONS MODULE
// ============================================================

function openNotifications() {
    const user = DB.getCurrentUser();
    if (!user) return toast('Please login');
    const notifs = DB.getNotifications().filter(n => n.userId === user.id);
    const lang = DB.getLanguage();
    const t = lang === 'hi' ? {
        title: '🔔 सूचनाएँ',
        noNotifs: 'कोई सूचना नहीं',
        markRead: 'सभी पढ़ें'
    } : {
        title: '🔔 Notifications',
        noNotifs: 'No notifications',
        markRead: 'Mark all read'
    };

    const html = `
        <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:12px;">
            <h3 style="font-size:18px;font-weight:700;">${t.title}</h3>
            ${notifs.filter(n => !n.read).length > 0 ? `<button class="btn btn-sm btn-primary" onclick="markAllRead()">${t.markRead}</button>` : ''}
        </div>
        ${notifs.map(n => `
            <div class="notif-item ${n.read ? '' : 'unread'}" style="${n.read ? '' : 'border-left:3px solid var(--primary);padding-left:10px;'}">
                <div class="icon" style="background:${n.read ? 'var(--bg)' : 'var(--primary)'};color:${n.read ? 'var(--text-secondary)' : '#fff'};">
                    <i class="fas ${n.title.includes('Bid') ? 'fa-gavel' : n.title.includes('Message') ? 'fa-comment' : n.title.includes('Payment') ? 'fa-money' : 'fa-bell'}"></i>
                </div>
                <div class="body">
                    <div class="title">${n.title}</div>
                    <div class="desc">${n.message}</div>
                    <div class="time">${new Date(n.createdAt).toLocaleDateString()} ${new Date(n.createdAt).toLocaleTimeString([],{hour:'2-digit',minute:'2-digit'})}</div>
                </div>
            </div>
        `).join('')}
        ${notifs.length === 0 ? `<div class="empty-state"><i class="fas fa-bell-slash"></i><h3>${t.noNotifs}</h3></div>` : ''}
    `;
    openModal(html);
}

function markAllRead() {
    const user = DB.getCurrentUser();
    if (!user) return;
    const notifs = DB.getNotifications();
    notifs.forEach(n => { if (n.userId === user.id) n.read = true; });
    DB.setNotifications(notifs);
    document.getElementById('notifDot').style.display = 'none';
    updateChatBadge();
    toast('All notifications marked as read');
    openNotifications();
}

function updateChatBadge() {
    const user = DB.getCurrentUser();
    if (!user) return;
    const notifs = DB.getNotifications().filter(n => n.userId === user.id && !n.read);
    const badge = document.getElementById('chatBadge');
    if (notifs.length > 0) {
        badge.style.display = 'flex';
        badge.textContent = notifs.length;
    } else {
        badge.style.display = 'none';
    }
}
// ============================================================
// AI ASSISTANT MODULE
// ============================================================

function openAI() {
    const lang = DB.getLanguage();
    const t = lang === 'hi' ? {
        title: '🤖 AI सहायक',
        welcome: 'नमस्ते! मैं SkillConnect AI हूँ। मैं आपकी कैसे मदद कर सकता हूँ?',
        recommend: 'मैं आपको नज़दीकी कर्मचारी ढूंढने में मदद कर सकता हूँ',
        ask: 'कुछ पूछें...',
        send: 'भेजें',
        suggestions: 'सुझाव:',
        suggestion1: 'मुझे एक प्लंबर चाहिए',
        suggestion2: 'AC रिपेयर का कितना खर्च है?',
        suggestion3: 'मेरे नज़दीकी कर्मचारी दिखाओ'
    } : {
        title: '🤖 AI Assistant',
        welcome: 'Hello! I\'m SkillConnect AI. How can I help you today?',
        recommend: 'I can help you find nearby workers',
        ask: 'Ask me anything...',
        send: 'Send',
        suggestions: 'Suggestions:',
        suggestion1: 'I need a plumber',
        suggestion2: 'How much does AC repair cost?',
        suggestion3: 'Show me nearby workers'
    };

    openModal(`
        <h3 style="font-size:18px;font-weight:700;">${t.title}</h3>
        <div id="aiChatContainer" style="background:var(--bg);border-radius:var(--radius-sm);padding:16px;margin:12px 0;min-height:120px;max-height:300px;overflow-y:auto;">
            <div style="display:flex;gap:10px;align-items:start;margin-bottom:10px;">
                <div style="width:32px;height:32px;border-radius:50%;background:var(--primary);color:#fff;display:flex;align-items:center;justify-content:center;flex-shrink:0;"><i class="fas fa-robot"></i></div>
                <div style="background:var(--card);padding:10px 14px;border-radius:14px;font-size:14px;flex:1;">${t.welcome}</div>
            </div>
            <div style="display:flex;gap:10px;align-items:start;justify-content:flex-end;">
                <div style="background:var(--primary);color:#fff;padding:10px 14px;border-radius:14px;font-size:14px;max-width:80%;">${t.recommend}</div>
            </div>
        </div>
        <div style="display:flex;gap:8px;flex-wrap:wrap;margin-bottom:12px;">
            <span style="font-size:12px;color:var(--text-secondary);">${t.suggestions}</span>
            <button class="chip" onclick="aiSuggestion('${t.suggestion1}')">${t.suggestion1}</button>
            <button class="chip" onclick="aiSuggestion('${t.suggestion2}')">${t.suggestion2}</button>
            <button class="chip" onclick="aiSuggestion('${t.suggestion3}')">${t.suggestion3}</button>
        </div>
        <div class="chat-input" style="padding:0;">
            <input id="aiInput" placeholder="${t.ask}">
            <button onclick="askAI()"><i class="fas fa-paper-plane"></i></button>
        </div>
    `);
}

function askAI() {
    const input = document.getElementById('aiInput');
    const query = input.value.trim();
    if (!query) return toast('Please ask something');
    const lang = DB.getLanguage();
    const responses = lang === 'hi' ? {
        plumber: 'मैंने आपके नज़दीक एक प्लंबर ढूंढा है। सुरेश (4.9⭐, ₹400/घंटा) उपलब्ध हैं। क्या आप उन्हें हायर करना चाहेंगे?',
        ac: 'AC रिपेयर की औसत लागत ₹500-₹800 है। विक्रम (4.6⭐, ₹550/घंटा) आपके नज़दीक हैं।',
        nearby: 'यहाँ आपके नज़दीकी कर्मचारी हैं: सुरेश (प्लंबर), प्रिया (इलेक्ट्रीशियन), रमेश (कारपेंटर)',
        default: 'मुझे आपकी मदद करके खुशी हुई! क्या आप किसी विशेष कौशल की तलाश कर रहे हैं?'
    } : {
        plumber: 'I found a plumber near you. Suresh (4.9⭐, ₹400/hr) is available. Would you like to hire him?',
        ac: 'The average cost for AC repair is ₹500-₹800. Vikram (4.6⭐, ₹550/hr) is near you.',
        nearby: 'Nearby workers: Suresh (Plumber), Priya (Electrician), Ramesh (Carpenter)',
        default: 'I\'m happy to help! Are you looking for a specific skill?'
    };

    let reply = responses.default;
    if (query.toLowerCase().includes('plumber') || query.toLowerCase().includes('प्लंबर')) reply = responses.plumber;
    else if (query.toLowerCase().includes('ac') || query.toLowerCase().includes('रिपेयर')) reply = responses.ac;
    else if (query.toLowerCase().includes('nearby') || query.toLowerCase().includes('नज़दीक')) reply = responses
    .nearby;

    const container = document.getElementById('aiChatContainer');
    if (container) {
        const userMsg = document.createElement('div');
        userMsg.style.cssText =
            'display:flex;gap:10px;align-items:start;justify-content:flex-end;margin-top:8px;';
        userMsg.innerHTML =
            `<div style="background:var(--primary);color:#fff;padding:10px 14px;border-radius:14px;font-size:14px;max-width:80%;">${query}</div>`;
        container.appendChild(userMsg);

        const botMsg = document.createElement('div');
        botMsg.style.cssText = 'display:flex;gap:10px;align-items:start;margin-top:8px;';
        botMsg.innerHTML =
            `<div style="width:32px;height:32px;border-radius:50%;background:var(--primary);color:#fff;display:flex;align-items:center;justify-content:center;flex-shrink:0;"><i class="fas fa-robot"></i></div><div style="background:var(--card);padding:10px 14px;border-radius:14px;font-size:14px;flex:1;">${reply}</div>`;
        container.appendChild(botMsg);
        container.scrollTop = container.scrollHeight;
    }
    input.value = '';
}

function aiSuggestion(text) {
    document.getElementById('aiInput').value = text;
    askAI();
}
// ============================================================
// APP MODULE – Core routing, rendering, and initialisation
// ============================================================

function navigateTo(screen) {
    const user = DB.getCurrentUser();
    if (!user && !['login', 'register'].includes(screen)) {
        showScreen('login');
        return;
    }
    if (screen === 'admin' && user?.role !== 'admin') {
        toast('Admin access only');
        return;
    }
    showScreen(screen);
    switch (screen) {
        case 'home':
            renderHome();
            break;
        case 'search':
            renderSearch();
            break;
        case 'postjob':
            renderPostJob();
            break;
        case 'chat':
            renderChat();
            break;
        case 'profile':
            renderProfile();
            break;
        case 'admin':
            renderAdmin();
            break;
    }
}

// ============================================================
// RENDER HOME
// ============================================================

function renderHome() {
    const user = DB.getCurrentUser();
    if (!user) return;
    const workers = DB.getWorkers();
    const jobs = DB.getJobs();
    const notifs = DB.getNotifications().filter(n => n.userId === user.id && !n.read);
    document.getElementById('notifDot').style.display = notifs.length > 0 ? 'block' : 'none';

    const lang = DB.getLanguage();
    const t = lang === 'hi' ? {
        greeting: 'नमस्ते',
        find: 'अपने नज़दीकी कर्मचारी खोजें',
        nearby: '🌟 नज़दीकी कर्मचारी',
        seeAll: 'सभी देखें',
        recent: '📋 हाल ही के काम',
        postNew: 'नया पोस्ट करें',
        searchPlaceholder: 'क्या सेवा चाहिए?'
    } : {
        greeting: 'Hello',
        find: 'Find the best workers near you',
        nearby: '🌟 Nearby Workers',
        seeAll: 'See all',
        recent: '📋 Recent Jobs',
        postNew: 'Post new',
        searchPlaceholder: 'What service do you need?'
    };

    const html = `
        <div class="flex justify-between items-start">
            <div>
                <div style="font-size:20px;font-weight:700;">${t.greeting}, ${user.name}! 👋</div>
                <div style="font-size:14px;color:var(--text-secondary);">${t.find}</div>
            </div>
        </div>

        <div style="display:flex;align-items:center;background:var(--card);border:1px solid var(--border);border-radius:30px;padding:10px 16px;margin:12px 0;gap:10px;">
            <i class="fas fa-search" style="color:var(--text-secondary);"></i>
            <input id="homeSearchInput" placeholder="${t.searchPlaceholder}" style="flex:1;border:none;outline:none;background:transparent;font-size:15px;color:var(--text);font-family:var(--font);" oninput="filterHomeWorkers(this.value)">
        </div>

        <div class="chip-group" id="homeChips">
            <span class="chip active" onclick="filterHomeCategory('all',this)">All</span>
            <span class="chip" onclick="filterHomeCategory('Plumber',this)"><i class="fas fa-wrench"></i> Plumber</span>
            <span class="chip" onclick="filterHomeCategory('Electrician',this)"><i class="fas fa-bolt"></i> Electrician</span>
            <span class="chip" onclick="filterHomeCategory('Carpenter',this)"><i class="fas fa-hammer"></i> Carpenter</span>
            <span class="chip" onclick="filterHomeCategory('Painter',this)"><i class="fas fa-paint-roller"></i> Painter</span>
            <span class="chip" onclick="filterHomeCategory('AC Repair',this)"><i class="fas fa-snowflake"></i> AC Repair</span>
        </div>

        <div style="margin-top:8px;">
            <div class="flex justify-between items-center">
                <h3 style="font-size:17px;font-weight:700;">${t.nearby}</h3>
                <a href="#" onclick="navigateTo('search')" style="font-size:13px;color:var(--primary);text-decoration:none;">${t.seeAll}</a>
            </div>
            <div id="homeWorkersList" style="margin-top:8px;display:flex;flex-direction:column;gap:10px;">
                ${workers.filter(w => w.availability === 'available').slice(0,5).map(w => workerCardHTML(w, lang)).join('')}
                ${workers.filter(w => w.availability === 'available').length === 0 ? '<div class="empty-state"><i class="fas fa-user-slash"></i><h3>No workers available</h3></div>' : ''}
            </div>
        </div>

        <div style="margin-top:20px;">
            <div class="flex justify-between items-center">
                <h3 style="font-size:17px;font-weight:700;">${t.recent}</h3>
                <a href="#" onclick="openModal(renderAllJobsModal())" style="font-size:13px;color:var(--primary);text-decoration:none;">${t.seeAll}</a>
            </div>
            <div style="margin-top:8px;display:flex;flex-direction:column;gap:8px;">
                ${jobs.slice(0,3).map(j => jobCardHTML(j, lang)).join('')}
                ${jobs.length === 0 ? '<div class="empty-state"><i class="fas fa-briefcase"></i><h3>No jobs posted yet</h3></div>' : ''}
            </div>
        </div>

        <div style="position:fixed;bottom:80px;right:16px;max-width:430px;display:flex;flex-direction:column;gap:10px;align-items:flex-end;z-index:50;">
            <button onclick="openAI()" style="width:52px;height:52px;border-radius:50%;background:var(--primary);color:#fff;border:none;box-shadow:0 6px 20px rgba(26,95,122,0.3);font-size:22px;cursor:pointer;transition:all var(--transition);">
                <i class="fas fa-robot"></i>
            </button>
            <button onclick="openEmergency()" style="width:56px;height:56px;border-radius:50%;background:var(--danger);color:#fff;border:none;box-shadow:0 6px 20px rgba(230,57,70,0.4);font-size:22px;cursor:pointer;transition:all var(--transition);">
                <i class="fas fa-phone-alt"></i>
            </button>
        </div>
    `;
    document.getElementById('homeContent').innerHTML = html;
}

let homeFilter = 'all';

function filterHomeCategory(cat, el) {
    document.querySelectorAll('#homeChips .chip').forEach(c => c.classList.remove('active'));
    el.classList.add('active');
    homeFilter = cat;
    applyHomeFilter();
}

function filterHomeWorkers(val) {
    const cards = document.querySelectorAll('#homeWorkersList .worker-card');
    cards.forEach(card => {
        const text = card.textContent.toLowerCase();
        card.style.display = text.includes(val.toLowerCase()) ? 'flex' : 'none';
    });
}

function applyHomeFilter() {
    const workers = DB.getWorkers();
    const filtered = homeFilter === 'all' ? workers : workers.filter(w => w.category === homeFilter);
    const container = document.getElementById('homeWorkersList');
    const lang = DB.getLanguage();
    container.innerHTML = filtered.filter(w => w.availability === 'available').slice(0, 5).map(w => workerCardHTML(w,
        lang)).join('') || '<div class="empty-state"><i class="fas fa-user-slash"></i><h3>No workers found</h3></div>';
}

// ============================================================
// RENDER SEARCH
// ============================================================

function renderSearch() {
    const lang = DB.getLanguage();
    const t = lang === 'hi' ? {
        title: '🔍 कर्मचारी खोजें',
        placeholder: 'नाम या कौशल से खोजें...',
        all: 'सभी',
        noResults: 'कोई कर्मचारी नहीं मिला'
    } : {
        title: '🔍 Search Workers',
        placeholder: 'Search by name or skill...',
        all: 'All',
        noResults: 'No workers found'
    };

    const workers = DB.getWorkers();
    const html = `
        <h2 style="font-size:20px;font-weight:700;margin-bottom:8px;">${t.title}</h2>
        <div style="display:flex;align-items:center;background:var(--card);border:1px solid var(--border);border-radius:30px;padding:10px 16px;margin:8px 0 12px;gap:10px;">
            <i class="fas fa-search" style="color:var(--text-secondary);"></i>
            <input id="searchInput" placeholder="${t.placeholder}" style="flex:1;border:none;outline:none;background:transparent;font-size:15px;color:var(--text);font-family:var(--font);" oninput="applySearch()">
        </div>
        <div class="chip-group" id="searchChips">
            <span class="chip active" onclick="filterSearchCategory('all',this)">${t.all}</span>
            <span class="chip" onclick="filterSearchCategory('Plumber',this)"><i class="fas fa-wrench"></i> Plumber</span>
            <span class="chip" onclick="filterSearchCategory('Electrician',this)"><i class="fas fa-bolt"></i> Electrician</span>
            <span class="chip" onclick="filterSearchCategory('Carpenter',this)"><i class="fas fa-hammer"></i> Carpenter</span>
            <span class="chip" onclick="filterSearchCategory('Painter',this)"><i class="fas fa-paint-roller"></i> Painter</span>
            <span class="chip" onclick="filterSearchCategory('AC Repair',this)"><i class="fas fa-snowflake"></i> AC Repair</span>
        </div>
        <div id="searchResults" style="margin-top:12px;display:flex;flex-direction:column;gap:10px;">
            ${workers.map(w => workerCardHTML(w, lang)).join('')}
            ${workers.length === 0 ? `<div class="empty-state"><i class="fas fa-search"></i><h3>${t.noResults}</h3></div>` : ''}
        </div>
    `;
    document.getElementById('searchContent').innerHTML = html;
    window._searchFilter = 'all';
}

function filterSearchCategory(cat, el) {
    document.querySelectorAll('#searchChips .chip').forEach(c => c.classList.remove('active'));
    el.classList.add('active');
    window._searchFilter = cat;
    applySearch();
}

function applySearch() {
    const val = document.getElementById('searchInput')?.value?.toLowerCase() || '';
    const cat = window._searchFilter || 'all';
    const workers = DB.getWorkers();
    const filtered = workers.filter(w => {
        const user = DB.getUsers().find(u => u.id === w.userId);
        const name = (user?.name || '').toLowerCase();
        const category = (w.category || '').toLowerCase();
        const matchName = name.includes(val);
        const matchCat = category.includes(val);
        const matchFilter = cat === 'all' || category === cat.toLowerCase();
        return (matchName || matchCat) && matchFilter;
    });
    const container = document.getElementById('searchResults');
    const lang = DB.getLanguage();
    container.innerHTML = filtered.map(w => workerCardHTML(w, lang)).join('') ||
        '<div class="empty-state"><i class="fas fa-search"></i><h3>No workers found</h3></div>';
}

// ============================================================
// RENDER POST JOB
// ============================================================

function renderPostJob() {
    const lang = DB.getLanguage();
    const t = lang === 'hi' ? {
        title: '📝 काम पोस्ट करें',
        sub: 'विश्वसनीय कर्मचारियों से बोली प्राप्त करें',
        titleLabel: 'काम का शीर्षक',
        titlePlaceholder: 'जैसे: नल ठीक करें',
        category: 'श्रेणी',
        desc: 'विवरण',
        descPlaceholder: 'काम के बारे में बताएं...',
        budget: 'बजट (₹)',
        location: 'स्थान',
        locationPlaceholder: 'आपका पता',
        emergency: 'आपातकालीन',
        submit: 'काम पोस्ट करें'
    } : {
        title: '📝 Post a Job',
        sub: 'Get bids from trusted workers',
        titleLabel: 'Job Title',
        titlePlaceholder: 'e.g. Fix leaking tap',
        category: 'Category',
        desc: 'Description',
        descPlaceholder: 'Describe the work...',
        budget: 'Budget (₹)',
        location: 'Location',
        locationPlaceholder: 'Your address',
        emergency: 'Emergency',
        submit: 'Post Job'
    };

    const html = `
        <h2 style="font-size:20px;font-weight:700;">${t.title}</h2>
        <p style="color:var(--text-secondary);font-size:14px;margin-bottom:16px;">${t.sub}</p>
        <div class="input-group">
            <label>${t.titleLabel}</label>
            <input id="jobTitle" placeholder="${t.titlePlaceholder}">
        </div>
        <div class="input-group">
            <label>${t.category}</label>
            <select id="jobCategory">
                <option>Plumber</option><option>Electrician</option><option>Carpenter</option>
                <option>Painter</option><option>Cleaner</option><option>AC Repair</option>
                <option>Mechanic</option><option>Driver</option><option>Welder</option>
            </select>
        </div>
        <div class="input-group">
            <label>${t.desc}</label>
            <textarea id="jobDesc" rows="3" placeholder="${t.descPlaceholder}"></textarea>
        </div>
        <div class="input-group">
            <label>${t.budget}</label>
            <input id="jobBudget" type="number" placeholder="500">
        </div>
        <div class="input-group">
            <label>${t.location}</label>
            <input id="jobLocation" placeholder="${t.locationPlaceholder}" value="Bangalore">
        </div>
        <div style="display:flex;align-items:center;gap:10px;margin-bottom:16px;">
            <input type="checkbox" id="jobUrgent" style="width:18px;height:18px;">
            <label for="jobUrgent" style="font-weight:600;color:var(--danger);">${t.emergency}</label>
        </div>
        <button class="btn btn-primary" onclick="submitJob()"><i class="fas fa-paper-plane"></i> ${t.submit}</button>
    `;
    document.getElementById('postJobContent').innerHTML = html;
}

// ============================================================
// RENDER CHAT
// ============================================================

function renderChat() {
    const user = DB.getCurrentUser();
    if (!user) return;
    const lang = DB.getLanguage();
    const t = lang === 'hi' ? {
        title: '💬 संदेश',
        noChats: 'कोई चैट नहीं',
        noChatsSub: 'काम पोस्ट करें और चैट शुरू करें',
        typeMsg: 'संदेश लिखें...'
    } : {
        title: '💬 Messages',
        noChats: 'No chats yet',
        noChatsSub: 'Post a job and start chatting',
        typeMsg: 'Type a message...'
    };

    const chats = DB.getChats().filter(c => c.participants.includes(user.id));
    const html = `
        <h2 style="font-size:20px;font-weight:700;margin-bottom:8px;">${t.title}</h2>
        <div id="chatList" class="chat-list" style="margin-top:8px;">
            ${chats.map(c => {
                const otherId = c.participants.find(p => p !== user.id);
                const otherUser = DB.getUsers().find(u => u.id === otherId);
                const lastMsg = c.messages.length > 0 ? c.messages[c.messages.length-1] : null;
                const job = DB.getJobs().find(j => j.id === c.jobId);
                return `
                    <div class="chat-item" onclick="openChatRoom('${c.id}')">
                        <div class="avatar" style="background:var(--secondary);color:#1D1D1F;">${otherUser ? otherUser.name.charAt(0) : '?'}</div>
                        <div style="flex:1;">
                            <div style="font-weight:600;">${otherUser ? otherUser.name : 'Unknown'}</div>
                            <div class="preview">${lastMsg ? lastMsg.content : (job ? job.title : 'Chat')}</div>
                        </div>
                        <div class="time">${lastMsg ? new Date(lastMsg.timestamp).toLocaleTimeString([],{hour:'2-digit',minute:'2-digit'}) : ''}</div>
                    </div>
                `;
            }).join('')}
            ${chats.length === 0 ? `<div class="empty-state"><i class="fas fa-comments"></i><h3>${t.noChats}</h3><p style="font-size:13px;">${t.noChatsSub}</p></div>` : ''}
        </div>
        <div id="chatRoomView" style="display:none;margin-top:8px;">
            <div style="display:flex;align-items:center;gap:10px;margin-bottom:8px;">
                <button onclick="closeChatRoom()" style="background:none;border:none;font-size:20px;color:var(--text-secondary);cursor:pointer;"><i class="fas fa-arrow-left"></i></button>
                <span id="chatRoomTitle" style="font-weight:700;font-size:16px;">Chat</span>
            </div>
            <div id="chatMessages" class="chat-messages"></div>
            <div class="chat-input">
                <input id="chatInput" placeholder="${t.typeMsg}">
                <button onclick="sendChatMessage()"><i class="fas fa-paper-plane"></i></button>
            </div>
        </div>
    `;
    document.getElementById('chatContent').innerHTML = html;
    updateChatBadge();
}

let currentChatId = null;

function openChatRoom(chatId) {
    currentChatId = chatId;
    const chat = DB.getChats().find(c => c.id === chatId);
    if (!chat) return toast('Chat not found');
    const user = DB.getCurrentUser();
    const otherId = chat.participants.find(p => p !== user.id);
    const otherUser = DB.getUsers().find(u => u.id === otherId);
    document.getElementById('chatList').style.display = 'none';
    document.getElementById('chatRoomView').style.display = 'block';
    document.getElementById('chatRoomTitle').textContent = otherUser ? otherUser.name : 'Chat';
    renderChatMessages(chat);
    const notifs = DB.getNotifications();
    notifs.forEach(n => {
        if (n.userId === user.id && n.message.includes(chatId)) n.read = true;
    });
    DB.setNotifications(notifs);
}

function renderChatMessages(chat) {
    const container = document.getElementById('chatMessages');
    const user = DB.getCurrentUser();
    container.innerHTML = chat.messages.map(m => `
        <div class="msg ${m.senderId === user.id ? 'sent' : 'received'}">
            ${m.content}
            <div style="font-size:10px;opacity:0.6;margin-top:2px;">${new Date(m.timestamp).toLocaleTimeString([],{hour:'2-digit',minute:'2-digit'})}</div>
        </div>
    `).join('');
    container.scrollTop = container.scrollHeight;
}

function sendChatMessage() {
    const input = document.getElementById('chatInput');
    const content = input.value.trim();
    if (!content || !currentChatId) return;
    const user = DB.getCurrentUser();
    const chats = DB.getChats();
    const chat = chats.find(c => c.id === currentChatId);
    if (!chat) return toast('Chat not found');
    chat.messages.push({ senderId: user.id, content, timestamp: new Date().toISOString() });
    DB.setChats(chats);
    renderChatMessages(chat);
    input.value = '';
    const otherId = chat.participants.find(p => p !== user.id);
    if (otherId) {
        const notifs = DB.getNotifications();
        notifs.push({
            id: genId(),
            userId: otherId,
            title: 'New Message',
            message: `${user.name}: ${content.substring(0,50)}`,
            read: false,
            createdAt: new Date().toISOString()
        });
        DB.setNotifications(notifs);
        updateChatBadge();
    }
}

function closeChatRoom() {
    document.getElementById('chatList').style.display = 'block';
    document.getElementById('chatRoomView').style.display = 'none';
    currentChatId = null;
}

// ============================================================
// RENDER PROFILE
// ============================================================

function renderProfile() {
    const user = DB.getCurrentUser();
    if (!user) return;
    const lang = DB.getLanguage();
    const t = lang === 'hi' ? {
        profile: 'प्रोफ़ाइल',
        switchTo: 'कर्मचारी बनें',
        switchToCust: 'ग्राहक बनें',
        logout: 'लॉगआउट',
        wallet: 'वॉलेट',
        saved: 'सेव किए गए',
        reviews: 'समीक्षाएँ',
        settings: 'सेटिंग्स',
        edit: 'संपादित करें',
        jobsPosted: 'काम पोस्ट किए',
        completed: 'पूरे किए',
        rating: 'रेटिंग'
    } : {
        profile: 'Profile',
        switchTo: 'Switch to Worker',
        switchToCust: 'Switch to Customer',
        logout: 'Logout',
        wallet: 'Wallet',
        saved: 'Saved',
        reviews: 'Reviews',
        settings: 'Settings',
        edit: 'Edit',
        jobsPosted: 'Jobs Posted',
        completed: 'Completed',
        rating: 'Rating'
    };

    const workers = DB.getWorkers();
    const worker = workers.find(w => w.userId === user.id);
    const isWorker = user.role === 'worker' || !!worker;

    const jobs = DB.getJobs().filter(j => j.customerId === user.id);
    const completedJobs = jobs.filter(j => j.status === 'completed').length;
    const reviews = DB.getReviews().filter(r => r.toUserId === user.id);
    const avgRating = reviews.length > 0 ? reviews.reduce((s, r) => s + r.rating, 0) / reviews.length : 0;

    const html = `
        <div class="profile-header">
            <div class="avatar avatar-lg" style="margin:0 auto;background:${isWorker ? 'var(--secondary)' : 'var(--primary)'};">
                ${user.name.charAt(0)}
            </div>
            <div class="name">${user.name}</div>
            <div class="role">${isWorker ? (worker?.category || 'Skilled Worker') : 'Customer'} ${isWorker && worker?.isPremium ? '⭐' : ''}</div>
            <div style="font-size:13px;color:var(--text-secondary);">${user.phone}</div>
        </div>

        <div class="profile-stats">
            <div class="stat"><div class="num">${jobs.length}</div><div class="label">${t.jobsPosted}</div></div>
            <div class="stat"><div class="num">${completedJobs}</div><div class="label">${t.completed}</div></div>
            <div class="stat"><div class="num">${avgRating > 0 ? avgRating.toFixed(1) : '—'}</div><div class="label">${t.rating}</div></div>
        </div>

        <div class="tab-bar">
            <button class="tab active" onclick="profileTab('saved', this)">${t.saved}</button>
            <button class="tab" onclick="profileTab('reviews', this)">${t.reviews}</button>
            <button class="tab" onclick="profileTab('settings', this)">${t.settings}</button>
        </div>

        <div id="profileTabContent">
            ${renderProfileTab('saved')}
        </div>

        <div style="margin-top:16px;display:flex;flex-direction:column;gap:8px;">
            <button class="btn btn-primary" onclick="openWallet()"><i class="fas fa-wallet"></i> ${t.wallet}</button>
            ${isWorker ? `<button class="btn btn-secondary" onclick="openSubscription()"><i class="fas fa-crown"></i> Subscription</button>` : ''}
            <button class="btn btn-outline" onclick="logout()">${t.logout}</button>
        </div>
    `;
    document.getElementById('profileContent').innerHTML = html;
}

function profileTab(tab, el) {
    document.querySelectorAll('.tab-bar .tab').forEach(t => t.classList.remove('active'));
    if (el) el.classList.add('active');
    document.getElementById('profileTabContent').innerHTML = renderProfileTab(tab);
}

function renderProfileTab(tab) {
    const user = DB.getCurrentUser();
    if (!user) return '';
    const lang = DB.getLanguage();
    const t = lang === 'hi' ? {
        noSaved: 'कोई सेव किए गए कर्मचारी नहीं',
        noReviews: 'कोई समीक्षा नहीं',
        name: 'नाम',
        phone: 'फोन',
        editProfile: 'प्रोफ़ाइल संपादित करें',
        save: 'सेव करें'
    } : {
        noSaved: 'No saved workers',
        noReviews: 'No reviews yet',
        name: 'Name',
        phone: 'Phone',
        editProfile: 'Edit Profile',
        save: 'Save'
    };

    if (tab === 'saved') {
        const saved = DB.getSavedWorkers().filter(s => s.customerId === user.id);
        const workers = DB.getWorkers();
        const savedWorkers = saved.map(s => workers.find(w => w.userId === s.workerId)).filter(Boolean);
        return savedWorkers.map(w => {
            const u = DB.getUsers().find(u => u.id === w.userId);
            return `
                <div class="worker-card" onclick="viewWorkerProfile('${w.userId}')" style="margin-bottom:8px;">
                    <div class="avatar" style="background:var(--primary);">${u ? u.name.charAt(0) : 'W'}</div>
                    <div class="info">
                        <h4>${u ? u.name : 'Worker'}</h4>
                        <div class="skill">${w.category || 'Skilled'} • ₹${w.hourlyRate || 0}/hr</div>
                    </div>
                    <button onclick="event.stopPropagation();unsaveWorker('${w.userId}')" style="background:none;border:none;color:var(--danger);cursor:pointer;font-size:16px;"><i class="fas fa-heart"></i></button>
                </div>
            `;
        }).join('') || `<div class="empty-state"><i class="fas fa-heart"></i><h3>${t.noSaved}</h3></div>`;
    } else if (tab === 'reviews') {
        const reviews = DB.getReviews().filter(r => r.toUserId === user.id);
        return reviews.map(r => {
            const from = DB.getUsers().find(u => u.id === r.fromUserId);
            const stars = '★'.repeat(r.rating) + '☆'.repeat(5 - r.rating);
            return `
                <div style="background:var(--card);border-radius:var(--radius-sm);padding:12px;border:1px solid var(--border);margin-bottom:8px;">
                    <div style="display:flex;justify-content:space-between;align-items:center;">
                        <span style="font-weight:600;">${from ? from.name : 'User'}</span>
                        <span style="color:var(--secondary);">${stars}</span>
                    </div>
                    <div style="font-size:14px;color:var(--text-secondary);margin-top:4px;">${r.comment || ''}</div>
                    <div style="font-size:11px;color:var(--text-secondary);margin-top:4px;">${new Date(r.createdAt).toLocaleDateString()}</div>
                </div>
            `;
        }).join('') || `<div class="empty-state"><i class="fas fa-star"></i><h3>${t.noReviews}</h3></div>`;
    } else {
        return `
            <div class="input-group">
                <label>${t.name}</label>
                <input id="editName" value="${user.name}">
            </div>
            <div class="input-group">
                <label>${t.phone}</label>
                <input id="editPhone" value="${user.phone}">
            </div>
            <button class="btn btn-primary" onclick="saveProfile()">${t.save}</button>
            <div style="margin-top:8px;">
                <button class="btn btn-outline" onclick="toggleDarkMode()"><i class="fas fa-moon"></i> Toggle Dark Mode</button>
            </div>
        `;
    }
}

function saveProfile() {
    const user = DB.getCurrentUser();
    if (!user) return;
    const name = document.getElementById('editName').value.trim();
    const phone = document.getElementById('editPhone').value.trim();
    if (!name || !phone) return toast('Please fill all fields');
    const users = DB.getUsers();
    const idx = users.findIndex(u => u.id === user.id);
    if (idx > -1) {
        users[idx].name = name;
        users[idx].phone = phone;
        DB.setUsers(users);
        DB.setCurrentUser(users[idx]);
        toast('Profile updated!');
        renderProfile();
    }
}

function unsaveWorker(workerId) {
    const user = DB.getCurrentUser();
    if (!user) return;
    let saved = DB.getSavedWorkers();
    saved = saved.filter(s => !(s.customerId === user.id && s.workerId === workerId));
    DB.setSavedWorkers(saved);
    toast('Removed from saved');
    renderProfile();
}

// ============================================================
// WALLET
// ============================================================

function openWallet() {
    const user = DB.getCurrentUser();
    if (!user) return toast('Please login');
    const txns = DB.getTransactions().filter(t => t.userId === user.id);
    const balance = txns.reduce((s, t) => {
        if (t.type === 'deposit' || t.type === 'earnings') return s + t.amount;
        if (t.type === 'withdrawal' || t.type === 'payment') return s - t.amount;
        return s;
    }, 0);
    const lang = DB.getLanguage();
    const t = lang === 'hi' ? {
        title: '💳 वॉलेट',
        balance: 'शेष राशि',
        addMoney: 'पैसे जोड़ें',
        history: 'लेन-देन इतिहास',
        noTxns: 'कोई लेन-देन नहीं',
        amount: 'राशि (₹)',
        add: 'जोड़ें'
    } : {
        title: '💳 Wallet',
        balance: 'Balance',
        addMoney: 'Add Money',
        history: 'Transaction History',
        noTxns: 'No transactions',
        amount: 'Amount (₹)',
        add: 'Add'
    };

    const html = `
        <h3 style="font-size:18px;font-weight:700;">${t.title}</h3>
        <div class="wallet-balance">
            <div class="label">${t.balance}</div>
            <div class="amount">₹${balance.toFixed(2)}</div>
        </div>
        <button class="btn btn-secondary" onclick="addMoney()"><i class="fas fa-plus"></i> ${t.addMoney}</button>
        <div style="margin-top:16px;">
            <h4 style="font-weight:600;margin-bottom:8px;">${t.history}</h4>
            ${txns.map(txn => `
                <div style="display:flex;justify-content:space-between;padding:8px 0;border-bottom:1px solid var(--border);">
                    <div>
                        <div style="font-weight:500;">${txn.description}</div>
                        <div style="font-size:12px;color:var(--text-secondary);">${new Date(txn.createdAt).toLocaleDateString()}</div>
                    </div>
                    <div style="font-weight:600;color:${txn.type === 'deposit' || txn.type === 'earnings' ? 'var(--success)' : 'var(--danger)'};">
                        ${txn.type === 'deposit' || txn.type === 'earnings' ? '+' : '-'}₹${txn.amount}
                    </div>
                </div>
            `).join('')}
            ${txns.length === 0 ? `<div class="empty-state"><i class="fas fa-wallet"></i><h3>${t.noTxns}</h3></div>` : ''}
        </div>
    `;
    openModal(html);
}

function addMoney() {
    const lang = DB.getLanguage();
    const t = lang === 'hi' ? {
        amount: 'राशि (₹)',
        add: 'जोड़ें'
    } : {
        amount: 'Amount (₹)',
        add: 'Add'
    };
    openModal(`
        <h3 style="font-size:18px;font-weight:700;">Add Money</h3>
        <div class="input-group">
            <label>${t.amount}</label>
            <input id="addAmount" type="number" placeholder="500">
        </div>
        <button class="btn btn-primary" onclick="processAddMoney()">${t.add}</button>
    `);
}

function processAddMoney() {
    const user = DB.getCurrentUser();
    if (!user) return;
    const amount = parseFloat(document.getElementById('addAmount').value);
    if (!amount || amount <= 0) return toast('Enter a valid amount');
    const txns = DB.getTransactions();
    txns.push({
        id: genId(),
        userId: user.id,
        amount: amount,
        type: 'deposit',
        description: 'Wallet top-up',
        createdAt: new Date().toISOString()
    });
    DB.setTransactions(txns);
    closeModal();
    toast('✅ ₹' + amount + ' added to wallet');
    openWallet();
}

// ============================================================
// SUBSCRIPTION
// ============================================================

function openSubscription() {
    const user = DB.getCurrentUser();
    if (!user) return toast('Please login');
    const lang = DB.getLanguage();
    const t = lang === 'hi' ? {
        title: '🌟 सदस्यता',
        current: 'वर्तमान योजना',
        free: 'मुफ्त',
        pro: 'प्रो',
        business: 'बिजनेस',
        features: 'सुविधाएँ',
        subscribe: 'सब्सक्राइब करें'
    } : {
        title: '🌟 Subscription',
        current: 'Current Plan',
        free: 'Free',
        pro: 'Pro',
        business: 'Business',
        features: 'Features',
        subscribe: 'Subscribe'
    };

    const subs = DB.getSubscriptions();
    const active = subs.find(s => s.workerId === user.id && s.active);

    const plans = [
        { id: 'free', name: t.free, price: 0, features: ['Basic Profile', '5 Bids/month', 'Standard Listing'] },
        { id: 'pro', name: t.pro, price: 199, features: ['Featured Profile', '50 Bids/month', 'Priority Support',
                'Lower Commission'
            ] },
        { id: 'business', name: t.business, price: 499, features: ['Premium Badge', 'Unlimited Bids',
                'Analytics Dashboard', 'Ad Credits'
            ] }
    ];

    const html = `
        <h3 style="font-size:18px;font-weight:700;">${t.title}</h3>
        <div style="margin:12px 0;">
            <span style="color:var(--text-secondary);">${t.current}:</span>
            <span style="font-weight:700;color:var(--primary);">${active ? (plans.find(p => p.id === active.plan)?.name || 'Pro') : t.free}</span>
        </div>
        <div style="display:grid;gap:12px;">
            ${plans.map(p => `
                <div class="plan-card ${p.id === 'pro' ? 'popular' : ''}" onclick="subscribePlan('${p.id}')">
                    ${p.id === 'pro' ? '<div class="badge-popular">⭐ Most Popular</div>' : ''}
                    <div class="name">${p.name}</div>
                    <div class="price">${p.price === 0 ? 'Free' : '₹'+p.price+'/mo'}</div>
                    <div class="features">${p.features.join(' • ')}</div>
                    ${p.price > 0 ? `<button class="btn btn-primary btn-sm" style="margin-top:8px;">${t.subscribe}</button>` : '<button class="btn btn-outline btn-sm" style="margin-top:8px;">Current</button>'}
                </div>
            `).join('')}
        </div>
    `;
    openModal(html);
}

function subscribePlan(planId) {
    const user = DB.getCurrentUser();
    if (!user) return toast('Please login');
    if (planId === 'free') return toast('You are already on the Free plan');
    const subs = DB.getSubscriptions();
    subs.forEach(s => { if (s.workerId === user.id) s.active = false; });
    subs.push({
        id: genId(),
        workerId: user.id,
        plan: planId,
        startDate: new Date().toISOString(),
        endDate: new Date(Date.now() + 30 * 24 * 60 * 60 * 1000).toISOString(),
        active: true
    });
    DB.setSubscriptions(subs);
    const workers = DB.getWorkers();
    const worker = workers.find(w => w.userId === user.id);
    if (worker) {
        worker.isPremium = true;
        if (planId === 'business') worker.isFeatured = true;
        DB.setWorkers(workers);
    }
    closeModal();
    toast('✅ Subscribed to ' + planId + ' plan!');
    openSubscription();
}

// ============================================================
// EMERGENCY
// ============================================================

function openEmergency() {
    const user = DB.getCurrentUser();
    if (!user) return toast('Please login');
    const lang = DB.getLanguage();
    const t = lang === 'hi' ? {
        title: '🚨 आपातकालीन सेवा',
        desc: 'अपनी आपातकालीन स्थिति का वर्णन करें',
        location: 'स्थान',
        submit: 'अलर्ट भेजें',
        placeholder: 'जैसे: पानी का पाइप फट गया'
    } : {
        title: '🚨 Emergency Service',
        desc: 'Describe your emergency situation',
        location: 'Location',
        submit: 'Send Alert',
        placeholder: 'e.g. Water pipe burst'
    };

    openModal(`
        <h3 style="font-size:18px;font-weight:700;color:var(--danger);">${t.title}</h3>
        <p style="font-size:14px;color:var(--text-secondary);margin-bottom:12px;">${t.desc}</p>
        <div class="input-group">
            <label>${t.desc}</label>
            <textarea id="emergDesc" rows="3" placeholder="${t.placeholder}"></textarea>
        </div>
        <div class="input-group">
            <label>${t.location}</label>
            <input id="emergLocation" value="${user.location || 'Bangalore'}">
        </div>
        <button class="btn btn-danger" onclick="sendEmergency()"><i class="fas fa-phone-alt"></i> ${t.submit}</button>
    `);
}

function sendEmergency() {
    const user = DB.getCurrentUser();
    if (!user) return;
    const desc = document.getElementById('emergDesc').value.trim();
    const location = document.getElementById('emergLocation').value.trim() || 'Bangalore';
    if (!desc) return toast('Please describe the emergency');
    const emerg = DB.getEmergency();
    emerg.push({
        id: genId(),
        userId: user.id,
        description: desc,
        location,
        status: 'pending',
        createdAt: new Date().toISOString()
    });
    DB.setEmergency(emerg);
    const workers = DB.getWorkers();
    const notifs = DB.getNotifications();
    workers.slice(0, 5).forEach(w => {
        notifs.push({
            id: genId(),
            userId: w.userId,
            title: '🚨 Emergency Alert',
            message: `${user.name} needs immediate help: ${desc.substring(0,50)}`,
            read: false,
            createdAt: new Date().toISOString()
        });
    });
    DB.setNotifications(notifs);
    closeModal();
    toast('🚨 Emergency alert sent! Nearby workers notified.');
}

// ============================================================
// LANGUAGE & THEME
// ============================================================

function toggleLanguage() {
    const current = DB.getLanguage();
    const next = current === 'en' ? 'hi' : 'en';
    DB.setLanguage(next);
    const btn = document.getElementById('langBtn');
    btn.textContent = next === 'en' ? '🇮🇳 हिंदी' : '🇬🇧 English';
    toast(next === 'hi' ? 'हिंदी में बदला गया' : 'Switched to English');
    const active = document.querySelector('.screen.active');
    if (active) {
        const id = active.id.replace('screen-', '');
        if (['home', 'search', 'postjob', 'chat', 'profile', 'admin'].includes(id)) {
            navigateTo(id);
        }
    }
}

function toggleDarkMode() {
    const current = DB.getTheme();
    const next = current === 'light' ? 'dark' : 'light';
    DB.setTheme(next);
    applyTheme(next);
    toast(next === 'dark' ? '🌙 Dark mode enabled' : '☀️ Light mode enabled');
}

function applyTheme(theme) {
    if (theme === 'dark') {
        document.documentElement.setAttribute('data-theme', 'dark');
        document.querySelector('.theme-toggle i').className = 'fas fa-sun';
    } else {
        document.documentElement.removeAttribute('data-theme');
        document.querySelector('.theme-toggle i').className = 'fas fa-moon';
    }
}

// ============================================================
// MODAL – ALL JOBS
// ============================================================

function renderAllJobsModal() {
    const jobs = DB.getJobs();
    const lang = DB.getLanguage();
    const t = lang === 'hi' ? {
        allJobs: '📋 सभी काम',
        noJobs: 'कोई काम नहीं',
        open: 'खुला',
        inProgress: 'प्रगति में',
        completed: 'पूरा हुआ'
    } : {
        allJobs: '📋 All Jobs',
        noJobs: 'No jobs',
        open: 'Open',
        inProgress: 'In Progress',
        completed: 'Completed'
    };
    return `
        <h3 style="font-size:18px;font-weight:700;">${t.allJobs}</h3>
        ${jobs.map(j => `
            <div class="job-card" onclick="closeModal();viewJobDetail('${j.id}')" style="margin-bottom:8px;">
                <div class="top"><h4>${j.title}</h4><span class="badge badge-${j.status === 'open' ? 'success' : j.status === 'in_progress' ? 'warning' : 'info'}">${j.status}</span></div>
                <div class="meta">${j.category} • ₹${j.budget}</div>
            </div>
        `).join('')}
        ${jobs.length === 0 ? `<div class="empty-state"><i class="fas fa-briefcase"></i><h3>${t.noJobs}</h3></div>` : ''}
    `;
}

// ============================================================
// INIT
// ============================================================

function init() {
    // Load theme
    const theme = DB.getTheme();
    applyTheme(theme);

    // Load language
    const lang = DB.getLanguage();
    document.getElementById('langBtn').textContent = lang === 'en' ? '🇮🇳 हिंदी' : '🇬🇧 English';

    // Load demo data
    loadDemoData();

    // Check if user is logged in
    const user = DB.getCurrentUser();
    if (user) {
        showScreen('home');
        renderHome();
    } else {
        showScreen('login');
    }

    // Notification badge
    if (user) {
        const notifs = DB.getNotifications().filter(n => n.userId === user.id && !n.read);
        document.getElementById('notifDot').style.display = notifs.length > 0 ? 'block' : 'none';
        updateChatBadge();
    }

    // Nav listeners
    document.querySelectorAll('.nav-item').forEach(btn => {
        btn.addEventListener('click', function() {
            const screen = this.dataset.screen;
            if (screen) navigateTo(screen);
        });
    });

    console.log('🚀 SkillConnect initialized');
    console.log('📦 Data in localStorage:', {
        users: DB.getUsers().length,
        workers: DB.getWorkers().length,
        jobs: DB.getJobs().length,
        chats: DB.getChats().length
    });
}

// Start the app when DOM ready
document.addEventListener('DOMContentLoaded', init);
# SkillConnect – Complete Platform

SkillConnect is a full-featured platform that connects skilled workers (plumbers, electricians, carpenters, etc.) with customers. It is a static web application that runs entirely in the browser using **HTML, CSS, and JavaScript** with **LocalStorage** for data persistence.

## ✨ Features

- **User Authentication** – Register, Login, OTP (demo), Logout  
- **Role-based** – Customer and Worker profiles  
- **Job Management** – Post, Edit, Delete, View jobs  
- **Bidding System** – Workers place bids; customers accept/reject  
- **Worker Discovery** – Search, filter by category, nearby workers (simulated)  
- **Worker Profiles** – Portfolio, certificates, ratings, availability  
- **Saved Workers** – Bookmark favourite workers  
- **Reviews & Ratings** – Leave and view reviews  
- **Chat** – Real‑time (simulated with LocalStorage)  
- **Notifications** – In-app notifications with badge  
- **Emergency Alerts** – Send SOS to nearby workers (simulated)  
- **AI Assistant** – Demo chatbot for recommendations  
- **Wallet & Earnings** – Simulated wallet with transaction history  
- **Subscription Plans** – Premium and Business tiers  
- **Admin Dashboard** – Overview, user/worker lists, data reset  
- **Dark Mode** – Toggle light/dark theme  
- **Multilingual** – English and Hindi support  
- **Mobile Responsive** – Optimised for all screen sizes  

## 🚀 Live Demo

This project is designed to be hosted on **GitHub Pages**.  
After deployment, it will be available at:  
`https://<your-username>.github.io/<repository-name>/`

## 📁 Project Structure

## 🛠️ How to Run Locally

1. **Clone** this repository or download the files.
2. Open `index.html` in any modern browser (Chrome, Edge, Firefox, etc.).
3. No server needed – everything works offline.

## 👥 Demo Accounts

- **Worker**: `9876543210` / `password123`  
- **Customer**: `9876543211` / `password123`  
- **Admin**: `9999999999` / `admin123`

> **OTP Login**: Use `123456` as the OTP (demo mode).

## 🧪 Data Persistence

All data is stored in your browser's **LocalStorage**.  
To reset the app to its initial demo state, use the **"Reset Data"** button inside the Admin Dashboard.

## 🎨 Customisation

- **Dark Mode**: Toggle from Profile → Settings  
- **Language**: Switch between English and Hindi using the button in the top‑right corner.

## 🌐 Deployment to GitHub Pages

1. Push this project to a GitHub repository.
2. Go to repository **Settings → Pages**.
3. Select the branch (e.g., `main`) and root folder.
4. Your site will be live at `https://<username>.github.io/<repo>/`.

## 📦 Browser Support

Works on all modern browsers that support ES6 and LocalStorage (Chrome 60+, Firefox 60+, Edge 79+, Safari 12+).

## 📝 License

This project is open‑source and available under the MIT License.
