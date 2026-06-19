<!DOCTYPE html>
<html lang="hi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>QB Type Board - मोबाइल टाइपिंग गेम</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            touch-action: manipulation;
            -webkit-tap-highlight-color: transparent;
        }
        
        body {
            font-family: 'Segoe UI', 'Roboto', sans-serif;
            background: linear-gradient(135deg, #1a2a6c, #b21f1f, #1a2a6c);
            color: #fff;
            min-height: 100vh;
            padding: 10px;
            overflow-x: hidden;
        }
        
        .mobile-container {
            max-width: 100%;
            background: rgba(0, 0, 0, 0.8);
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5);
            overflow: hidden;
            margin: 0 auto;
        }
        
        /* मोबाइल हेडर */
        .mobile-header {
            background: rgba(0, 0, 0, 0.9);
            padding: 15px;
            text-align: center;
            border-bottom: 3px solid #ff9900;
            position: sticky;
            top: 0;
            z-index: 100;
        }
        
        h1 {
            font-size: 1.8rem;
            margin-bottom: 5px;
            color: #ff9900;
            text-shadow: 0 0 10px rgba(255, 153, 0, 0.5);
        }
        
        .tagline {
            font-size: 0.9rem;
            opacity: 0.9;
        }
        
        /* मोबाइल मुख्य सामग्री */
        .mobile-content {
            padding: 15px;
            display: flex;
            flex-direction: column;
            gap: 15px;
        }
        
        /* स्टैट्स कंटेनर - मोबाइल अनुकूलित */
        .mobile-stats {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 10px;
            background: rgba(0, 0, 0, 0.5);
            padding: 10px;
            border-radius: 15px;
            border: 1px solid #444;
        }
        
        .stat-box {
            text-align: center;
            padding: 10px;
        }
        
        .stat-value {
            font-size: 1.8rem;
            font-weight: bold;
            color: #ff9900;
        }
        
        .stat-label {
            font-size: 0.8rem;
            opacity: 0.8;
        }
        
        /* टेक्स्ट डिस्प्ले - मोबाइल के लिए अनुकूलित */
        .mobile-text-display {
            background: rgba(0, 0, 0, 0.5);
            border-radius: 15px;
            padding: 20px 15px;
            font-size: 1.3rem;
            line-height: 1.8rem;
            border: 1px solid #444;
            min-height: 180px;
            overflow: hidden;
        }
        
        .mobile-text-display span {
            transition: all 0.2s;
            padding: 1px 0;
            border-radius: 2px;
        }
        
        .mobile-text-display .current {
            background: #ff9900;
            color: #000;
            animation: pulse 1.5s infinite;
        }
        
        .mobile-text-display .correct {
            color: #4caf50;
        }
        
        .mobile-text-display .incorrect {
            color: #f44336;
            text-decoration: underline;
        }
        
        /* टाइपिंग इनपुट - मोबाइल के लिए अनुकूलित */
        .mobile-typing-input {
            width: 100%;
            padding: 15px;
            font-size: 1.2rem;
            background: rgba(0, 0, 0, 0.6);
            border: 2px solid #444;
            border-radius: 15px;
            color: white;
            outline: none;
            transition: border-color 0.3s;
            resize: none;
            height: 100px;
        }
        
        .mobile-typing-input:focus {
            border-color: #ff9900;
        }
        
        /* मोबाइल नियंत्रण */
        .mobile-controls {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 10px;
            margin-top: 10px;
        }
        
        .mobile-btn {
            padding: 14px 10px;
            border: none;
            border-radius: 12px;
            font-size: 1rem;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
        }
        
        .start-btn {
            background: #ff9900;
            color: #000;
        }
        
        .reset-btn {
            background: rgba(255, 255, 255, 0.1);
            color: white;
        }
        
        .mobile-btn i {
            font-size: 1.2rem;
        }
        
        /* मोबाइल सेटिंग्स */
        .mobile-settings {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 10px;
            margin-top: 10px;
        }
        
        .setting-group {
            background: rgba(0, 0, 0, 0.4);
            padding: 12px;
            border-radius: 12px;
            border: 1px solid #444;
        }
        
        .setting-group label {
            display: block;
            font-size: 0.9rem;
            margin-bottom: 8px;
            color: #ff9900;
        }
        
        .setting-group select {
            width: 100%;
            padding: 10px;
            background: rgba(0, 0, 0, 0.6);
            border: 1px solid #444;
            border-radius: 8px;
            color: white;
            font-size: 1rem;
        }
        
        /* मोबाइल कीबोर्ड डिस्प्ले */
        .mobile-keyboard-display {
            background: rgba(0, 0, 0, 0.5);
            border-radius: 15px;
            padding: 15px;
            margin-top: 15px;
            border: 1px solid #444;
            display: grid;
            grid-template-columns: repeat(10, 1fr);
            gap: 5px;
        }
        
        .key {
            width: 100%;
            aspect-ratio: 1;
            display: flex;
            justify-content: center;
            align-items: center;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 8px;
            font-weight: bold;
            font-size: 0.9rem;
            transition: all 0.2s;
        }
        
        .key.active {
            background: #ff9900;
            color: #000;
            transform: scale(1.1);
            box-shadow: 0 0 10px rgba(255, 153, 0, 0.7);
        }
        
        /* मोबाइल प्रगति बार */
        .mobile-progress {
            margin-top: 15px;
            text-align: center;
        }
        
        .progress-bar {
            height: 10px;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 5px;
            margin-top: 8px;
            overflow: hidden;
        }
        
        .progress-fill {
            height: 100%;
            background: #ff9900;
            width: 0%;
            transition: width 0.5s;
        }
        
        /* मोबाइल फुटर */
        .mobile-footer {
            text-align: center;
            padding: 15px;
            background: rgba(0, 0, 0, 0.8);
            border-top: 1px solid #444;
            font-size: 0.8rem;
            opacity: 0.8;
            margin-top: 15px;
        }
        
        .highlight {
            color: #ff9900;
            font-weight: bold;
        }
        
        /* कीफ्रेम्स और मीडिया क्वेरीज़ */
        @keyframes pulse {
            0% { background: #ff9900; }
            50% { background: #ffaa33; }
            100% { background: #ff9900; }
        }
        
        @media (max-width: 480px) {
            .mobile-text-display {
                font-size: 1.1rem;
                line-height: 1.6rem;
                padding: 15px 10px;
            }
            
            .mobile-keyboard-display {
                grid-template-columns: repeat(8, 1fr);
            }
            
            h1 {
                font-size: 1.5rem;
            }
        }
        
        @media (max-width: 360px) {
            .mobile-keyboard-display {
                grid-template-columns: repeat(6, 1fr);
            }
            
            .mobile-stats {
                grid-template-columns: 1fr;
            }
            
            .mobile-settings {
                grid-template-columns: 1fr;
            }
        }
        
        /* मोबाइल कीबोर्ड के लिए विशेष समायोजन */
        @media (max-height: 700px) {
            .mobile-text-display {
                min-height: 130px;
                font-size: 1.1rem;
                line-height: 1.5rem;
            }
            
            .mobile-typing-input {
                height: 80px;
                font-size: 1rem;
            }
        }
        
        /* वर्टिकल मोड के लिए समायोजन */
        @media (orientation: portrait) {
            .mobile-container {
                max-width: 100%;
            }
        }
        
        /* होरिजॉन्टल मोड के लिए समायोजन */
        @media (orientation: landscape) {
            .mobile-container {
                max-width: 700px;
            }
            
            .mobile-content {
                flex-direction: row;
                flex-wrap: wrap;
            }
            
            .mobile-text-container {
                width: 100%;
            }
            
            .mobile-stats {
                width: calc(50% - 8px);
            }
            
            .mobile-settings {
                width: calc(50% - 8px);
                margin-top: 0;
            }
        }
    </style>
</head>
<body>
    <div class="mobile-container">
        <div class="mobile-header">
            <h1><i class="fas fa-keyboard"></i> QB Type Board</h1>
            <p class="tagline">अपनी टाइपिंग स्पीड बढ़ाएं - कहीं भी, कभी भी!</p>
        </div>
        
        <div class="mobile-content">
            <div class="mobile-text-container">
                <div class="mobile-stats">
                    <div class="stat-box">
                        <div class="stat-value" id="wpm">0</div>
                        <div class="stat-label">WPM</div>
                    </div>
                    <div class="stat-box">
                        <div class="stat-value" id="accuracy">100%</div>
                        <div class="stat-label">शुद्धता</div>
                    </div>
                    <div class="stat-box">
                        <div class="stat-value" id="timer">60</div>
                        <div class="stat-label">सेकंड</div>
                    </div>
                    <div class="stat-box">
                        <div class="stat-value" id="score">0</div>
                        <div class="stat-label">स्कोर</div>
                    </div>
                </div>
                
                <div class="mobile-text-display" id="text-display">
                    <!-- टेक्स्ट यहां जेनरेट होगा -->
                </div>
                
                <textarea 
                    class="mobile-typing-input" 
                    id="typing-input" 
                    placeholder="यहां टाइप करना शुरू करें..." 
                    autocomplete="off"
                    autocorrect="off"
                    autocapitalize="off"
                    spellcheck="false"
                    disabled
                ></textarea>
            </div>
            
            <div class="mobile-controls">
                <button id="start-btn" class="mobile-btn start-btn">
                    <i class="fas fa-play"></i> शुरू करें
                </button>
                <button id="reset-btn" class="mobile-btn reset-btn">
                    <i class="fas fa-redo"></i> रीसेट
                </button>
            </div>
            
            <div class="mobile-settings">
                <div class="setting-group">
                    <label for="time-setting"><i class="fas fa-clock"></i> समय:</label>
                    <select id="time-setting">
                        <option value="30">30 सेकंड</option>
                        <option value="60" selected>60 सेकंड</option>
                        <option value="120">120 सेकंड</option>
                    </select>
                </div>
                
                <div class="setting-group">
                    <label for="difficulty"><i class="fas fa-cogs"></i> कठिनाई:</label>
                    <select id="difficulty">
                        <option value="easy">आसान</option>
                        <option value="medium" selected>मध्यम</option>
                        <option value="hard">कठिन</option>
                    </select>
                </div>
            </div>
            
            <div class="mobile-keyboard-display" id="keyboard">
                <!-- कीज़ यहां जेनरेट होंगी -->
            </div>
            
            <div class="mobile-progress">
                <div>प्रगति: <span id="progress-text">0%</span></div>
                <div class="progress-bar">
                    <div class="progress-fill" id="progress-fill"></div>
                </div>
            </div>
        </div>
        
        <div class="mobile-footer">
            <p>QB Type Board &copy; 2023 | मोबाइल के लिए अनुकूलित | <span class="highlight">शुरू करें</span> बटन दबाकर अभ्यास शुरू करें</p>
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            // DOM elements
            const textDisplay = document.getElementById('text-display');
            const typingInput = document.getElementById('typing-input');
            const startBtn = document.getElementById('start-btn');
            const resetBtn = document.getElementById('reset-btn');
            const wpmDisplay = document.getElementById('wpm');
            const accuracyDisplay = document.getElementById('accuracy');
            const timerDisplay = document.getElementById('timer');
            const scoreDisplay = document.getElementById('score');
            const difficultySelect = document.getElementById('difficulty');
            const timeSetting = document.getElementById('time-setting');
            const keyboard = document.getElementById('keyboard');
            const progressFill = document.getElementById('progress-fill');
            const progressText = document.getElementById('progress-text');
            
            // Practice variables
            let practiceText = '';
            let timer = 60;
            let timerInterval;
            let startTime;
            let totalChars = 0;
            let correctChars = 0;
            let isActive = false;
            let score = 0;
            
            // Initialize the keyboard
            initKeyboard();
            
            // Generate initial practice text
            generatePracticeText('medium');
            
            // Event listeners
            startBtn.addEventListener('click', startPractice);
            resetBtn.addEventListener('click', resetPractice);
            typingInput.addEventListener('input', handleTypingInput);
            difficultySelect.addEventListener('change', () => {
                generatePracticeText(difficultySelect.value);
                if (!isActive) resetPractice();
            });
            timeSetting.addEventListener('change', () => {
                timer = parseInt(timeSetting.value);
                timerDisplay.textContent = timer;
            });
            
            // Initialize the keyboard display
            function initKeyboard() {
                const keys = [
                    'Q','W','E','R','T','Y','U','I','O','P',
                    'A','S','D','F','G','H','J','K','L',
                    'Z','X','C','V','B','N','M'
                ];
                
                keyboard.innerHTML = '';
                keys.forEach(key => {
                    const keyElement = document.createElement('div');
                    keyElement.className = 'key';
                    keyElement.textContent = key;
                    keyElement.id = `key-${key}`;
                    keyboard.appendChild(keyElement);
                });
            }
            
            // Highlight a key on the keyboard
            function highlightKey(key) {
                // Remove active class from all keys
                document.querySelectorAll('.key').forEach(k => {
                    k.classList.remove('active');
                });
                
                // Highlight the pressed key if it's a letter
                if (key.length === 1 && /[A-Z]/i.test(key)) {
                    const keyElement = document.getElementById(`key-${key.toUpperCase()}`);
                    if (keyElement) {
                        keyElement.classList.add('active');
                    }
                }
            }
            
            // Generate practice text based on difficulty
            function generatePracticeText(difficulty) {
                let words = [];
                const easyWords = [
                    'और', 'है', 'कर', 'ने', 'को', 'से', 'पर', 'यह', 'वह', 'तो',
                    'में', 'की', 'हो', 'था', 'ही', 'या', 'उस', 'इस', 'कर', 'गया',
                    'होता', 'किया', 'लिया', 'दिया', 'बहुत', 'फिर', 'कुछ', 'सब', 'अपने', 'उनके',
                    'होने', 'करने', 'देने', 'लेने', 'जाने', 'आने', 'पड़ा', 'रहा', 'देखा', 'सुना'
                ];
                
                const mediumWords = [
                    'प्रयोग', 'व्यक्ति', 'सरकार', 'प्रणाली', 'विकास', 'संस्था', 'अनुभव', 'प्रक्रिया', 
                    'जानकारी', 'अवसर', 'पर्यावरण', 'विशेष', 'संगठन', 'अंतर्राष्ट्रीय', 'शिक्षा', 
                    'प्रौद्योगिकी', 'समुदाय', 'प्रबंधन', 'प्रभाव', 'संभावना', 'उद्देश्य', 'सुरक्षा', 
                    'प्रदर्शन', 'संचार', 'संसाधन', 'प्रतिस्पर्धा', 'अनुसंधान', 'प्रशिक्षण', 'परियोजना'
                ];
                
                const hardWords = [
                    'उपलब्धि', 'जिम्मेदारी', 'परिस्थिति', 'व्यावसायिक', 'अनुकूलन', 'स्वतंत्रता', 
                    'संवैधानिक', 'पर्यटन', 'असाधारण', 'सहयोग', 'व्यक्तित्व', 'सुविधा', 'प्रशासनिक', 
                    'उत्साह', 'उपकरण', 'प्रतिभागी', 'परंपरा', 'अनुशासन', 'प्रतिक्रिया', 'संरचना'
                ];
                
                // Select word list based on difficulty
                switch(difficulty) {
                    case 'easy':
                        words = easyWords;
                        break;
                    case 'hard':
                        words = hardWords;
                        break;
                    default:
                        words = mediumWords;
                }
                
                // Generate text with 20-30 words for mobile
                const wordCount = 20 + Math.floor(Math.random() * 11);
                practiceText = '';
                
                for (let i = 0; i < wordCount; i++) {
                    const randomIndex = Math.floor(Math.random() * words.length);
                    practiceText += words[randomIndex];
                    if (i < wordCount - 1) practiceText += ' ';
                }
                
                // Display the text
                displayPracticeText();
            }
            
            // Display the practice text with spans
            function displayPracticeText() {
                textDisplay.innerHTML = '';
                practiceText.split('').forEach(char => {
                    const charSpan = document.createElement('span');
                    charSpan.innerText = char;
                    textDisplay.appendChild(charSpan);
                });
                
                // Reset current character highlight
                if (textDisplay.firstChild) {
                    textDisplay.firstChild.classList.add('current');
                }
            }
            
            // Start the practice session
            function startPractice() {
                if (isActive) return;
                
                isActive = true;
                typingInput.disabled = false;
                typingInput.focus();
                startBtn.disabled = true;
                
                // Reset stats
                totalChars = 0;
                correctChars = 0;
                score = 0;
                timer = parseInt(timeSetting.value);
                updateStats();
                
                // Clear input
                typingInput.value = '';
                
                // Start timer
                startTime = new Date();
                timerInterval = setInterval(updateTimer, 1000);
            }
            
            // Update the timer
            function updateTimer() {
                timer--;
                timerDisplay.textContent = timer;
                
                if (timer <= 0) {
                    endPractice();
                }
                
                // Update WPM and accuracy every second
                updateStats();
            }
            
            // Handle typing input
            function handleTypingInput() {
                if (!isActive) return;
                
                const typedText = typingInput.value;
                const practiceTextChars = practiceText.split('');
                const typedChars = typedText.split('');
                
                // Update character highlighting
                textDisplay.querySelectorAll('span').forEach((charSpan, index) => {
                    const typedChar = typedChars[index];
                    
                    // Reset classes
                    charSpan.classList.remove('correct', 'incorrect', 'current');
                    
                    if (typedChar === undefined) {
                        // Not typed yet
                        if (index === typedChars.length) {
                            charSpan.classList.add('current');
                        }
                    } else if (typedChar === practiceTextChars[index]) {
                        // Correct character
                        charSpan.classList.add('correct');
                    } else {
                        // Incorrect character
                        charSpan.classList.add('incorrect');
                    }
                });
                
                // Highlight next key if needed
                if (typedChars.length < practiceTextChars.length) {
                    const nextChar = practiceTextChars[typedChars.length];
                    highlightKey(nextChar);
                }
                
                // Calculate stats
                totalChars = typedChars.length;
                correctChars = 0;
                
                for (let i = 0; i < typedChars.length; i++) {
                    if (typedChars[i] === practiceTextChars[i]) {
                        correctChars++;
                    }
                }
                
                // Update progress
                const progress = Math.min(100, Math.floor((typedChars.length / practiceTextChars.length) * 100));
                progressFill.style.width = `${progress}%`;
                progressText.textContent = `${progress}%`;
                
                // Update stats
                updateStats();
                
                // Check if all text is typed
                if (typedText.length >= practiceText.length) {
                    // Add to score and generate new text
                    score += Math.floor(correctChars * 2);
                    generatePracticeText(difficultySelect.value);
                    typingInput.value = '';
                }
            }
            
            // Update statistics display
            function updateStats() {
                // Calculate accuracy
                const accuracy = totalChars > 0 ? Math.floor((correctChars / totalChars) * 100) : 100;
                accuracyDisplay.textContent = `${accuracy}%`;
                
                // Calculate WPM
                const currentTime = new Date();
                const elapsedTime = (currentTime - startTime) / 1000 / 60; // in minutes
                const wpm = elapsedTime > 0 ? Math.floor((correctChars / 5) / elapsedTime) : 0;
                wpmDisplay.textContent = wpm;
                
                // Update score
                scoreDisplay.textContent = score;
            }
            
            // End the practice session
            function endPractice() {
                clearInterval(timerInterval);
                isActive = false;
                typingInput.disabled = true;
                startBtn.disabled = false;
                
                // Show final stats
                updateStats();
                
                // Add final score bonus
                score += Math.floor(correctChars * 0.5);
                scoreDisplay.textContent = score;
                
                // Show completion message
                const finalWPM = wpmDisplay.textContent;
                alert(`अभ्यास पूरा हुआ!\nआपकी टाइपिंग स्पीड: ${finalWPM} WPM\nशुद्धता: ${accuracyDisplay.textContent}\nअंतिम स्कोर: ${score}`);
            }
            
            // Reset the practice session
            function resetPractice() {
                clearInterval(timerInterval);
                isActive = false;
                typingInput.disabled = false;
                startBtn.disabled = false;
                typingInput.value = '';
                timer = parseInt(timeSetting.value);
                
                // Reset stats
                totalChars = 0;
                correctChars = 0;
                score = 0;
                updateStats();
                
                // Generate new text
                generatePracticeText(difficultySelect.value);
                
                // Update timer display
                timerDisplay.textContent = timer;
            }
        });
    </script>
</body>
</html>
