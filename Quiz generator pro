<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Advanced Quiz Video Generator with Screen Recorder</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }
        
        body {
            font-family: 'Arial', sans-serif;
            padding: 15px;
            background-color: #f5f5f5;
            color: #333;
            overflow-x: hidden;
        }
        
        .container {
            max-width: 100%;
            margin: 0 auto;
            display: flex;
            flex-direction: column;
            gap: 15px;
        }
        
        h1, h2 {
            text-align: center;
            color: #2c3e50;
            margin-bottom: 10px;
        }
        
        h1 {
            font-size: 1.8rem;
        }
        
        h2 {
            font-size: 1.3rem;
            margin-top: 5px;
        }
        
        .section {
            background-color: white;
            padding: 15px;
            border-radius: 8px;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
        }
        
        textarea {
            width: 100%;
            min-height: 150px;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 4px;
            font-family: monospace;
            resize: vertical;
            font-size: 14px;
        }
        
        .preview-container {
            position: relative;
            margin: 15px auto;
            overflow: hidden;
            background-size: cover;
            background-position: center;
            width: 100%;
            aspect-ratio: 16/9;
        }
        
        .video-frame {
            position: relative;
            width: 100%;
            height: 100%;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            gap: 20px;
        }
        
        .question-box, .answer-box {
            margin: 10px;
            padding: 15px;
            border-radius: 8px;
            text-align: center;
            max-width: 90%;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
            transition: all 0.5s ease;
            position: relative;
            width: 80%;
        }
        
        .question-box {
            background-color: #3498db;
            color: white;
            opacity: 0;
            transform: scale(0.9);
        }
        
        .question-box.visible {
            opacity: 1;
            transform: scale(1);
        }
        
        .answer-box {
            background-color: #2ecc71;
            color: white;
            opacity: 0;
            transform: scale(0.9);
        }
        
        .answer-box.visible {
            opacity: 1;
            transform: scale(1);
        }
        
        .countdown {
            font-size: 2rem;
            font-weight: bold;
            color: #e74c3c;
            position: absolute;
            opacity: 0;
            transition: opacity 0.3s ease;
        }
        
        .countdown.visible {
            opacity: 1;
        }
        
        .controls {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
            gap: 15px;
            margin-bottom: 15px;
        }
        
        .control-group {
            display: flex;
            flex-direction: column;
        }
        
        label {
            margin-bottom: 5px;
            font-weight: bold;
            font-size: 0.9rem;
        }
        
        select, input, button {
            padding: 8px;
            border: 1px solid #ddd;
            border-radius: 4px;
            margin-bottom: 8px;
            font-size: 0.9rem;
            width: 100%;
        }
        
        button {
            background-color: #3498db;
            color: white;
            border: none;
            cursor: pointer;
            font-weight: bold;
            transition: background-color 0.3s;
            padding: 10px;
        }
        
        button:hover {
            background-color: #2980b9;
        }
        
        /* Screen recorder styles */
        .recorder-controls {
            display: flex;
            gap: 10px;
            margin-top: 15px;
            flex-wrap: wrap;
        }
        
        .recorder-btn {
            background-color: #e74c3c;
        }
        
        .recorder-btn:hover {
            background-color: #c0392b;
        }
        
        .recorder-btn.start {
            background-color: #2ecc71;
        }
        
        .recorder-btn.start:hover {
            background-color: #27ae60;
        }
        
        .recorder-btn.restart {
            background-color: #f39c12;
        }
        
        .recorder-btn.restart:hover {
            background-color: #d35400;
        }
        
        .recording-indicator {
            display: flex;
            align-items: center;
            gap: 5px;
            color: #e74c3c;
            font-weight: bold;
        }
        
        .recording-dot {
            width: 10px;
            height: 10px;
            background-color: #e74c3c;
            border-radius: 50%;
            animation: pulse 1.5s infinite;
        }
        
        @keyframes pulse {
            0% { opacity: 1; }
            50% { opacity: 0.5; }
            100% { opacity: 1; }
        }
        
        .recording-container {
            margin-top: 30px;
            display: none;
        }
        
        .recording-container video {
            width: 100%;
            max-width: 800px;
            border-radius: 8px;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
            margin: 0 auto;
            display: block;
        }
        
        .recording-timer {
            font-weight: bold;
            margin-left: auto;
        }
        
        .screen-selector {
            margin-top: 15px;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 4px;
            background-color: #f9f9f9;
        }
        
        .screen-selector label {
            display: block;
            margin-bottom: 10px;
        }
        
        .screen-selector-options {
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
        }
        
        .screen-selector-option {
            padding: 8px 12px;
            background-color: #eee;
            border-radius: 4px;
            cursor: pointer;
        }
        
        .screen-selector-option.selected {
            background-color: #3498db;
            color: white;
        }
        
        /* Font size controls */
        .font-size-controls {
            display: flex;
            gap: 10px;
            align-items: center;
            margin-top: 10px;
        }
        
        .font-size-btn {
            width: 40px;
            height: 40px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
            background-color: #3498db;
            color: white;
            border-radius: 4px;
            cursor: pointer;
        }
        
        .font-size-value {
            min-width: 40px;
            text-align: center;
            font-weight: bold;
        }
        
        @media (max-width: 768px) {
            .preview-container {
                aspect-ratio: 9/16;
            }
            
            .question-box, .answer-box {
                font-size: 1rem;
                padding: 10px;
            }
            
            .recorder-controls {
                flex-direction: column;
            }
        }
        
        @media (max-width: 600px) {
            .controls {
                grid-template-columns: 1fr;
            }
            
            button, select, input {
                padding: 12px;
                font-size: 1rem;
            }
            
            .countdown {
                font-size: 1.5rem;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Advanced Quiz Video Generator with Screen Recorder</h1>
        
        <div class="section">
            <h2>Enter Questions and Answers</h2>
            <p>Format: One question and answer per line, separated by "|"</p>
            <textarea id="qa-input" placeholder="What is the capital of France?|Paris
How many continents are there?|7
What is 2+2?|4"></textarea>
        </div>
        
        <div class="section">
            <h2>Video Settings</h2>
            <div class="controls">
                <div class="control-group">
                    <label for="aspect-ratio">Aspect Ratio</label>
                    <select id="aspect-ratio">
                        <option value="16/9">Horizontal (16:9)</option>
                        <option value="9/16">Vertical (9:16)</option>
                        <option value="1/1">Square (1:1)</option>
                    </select>
                    
                    <label for="layout">Layout</label>
                    <select id="layout">
                        <option value="stacked">Stacked (Vertical)</option>
                        <option value="side-by-side">Side by Side (Horizontal)</option>
                    </select>
                    
                    <label for="question-time">Question Time (seconds)</label>
                    <input type="number" id="question-time" min="1" max="60" value="5">
                    
                    <label for="answer-time">Answer Time (seconds)</label>
                    <input type="number" id="answer-time" min="1" max="60" value="5">
                    
                    <label for="countdown-time">Countdown Time (seconds)</label>
                    <input type="number" id="countdown-time" min="1" max="10" value="3">
                </div>
                
                <div class="control-group">
                    <label for="bg-type">Background</label>
                    <select id="bg-type">
                        <option value="color">Color</option>
                        <option value="image">Image</option>
                        <option value="gradient">Gradient</option>
                    </select>
                    
                    <div id="bg-color-control">
                        <label for="bg-color">Background Color</label>
                        <input type="color" id="bg-color" value="#ffffff">
                    </div>
                    
                    <div id="bg-image-control" style="display:none">
                        <label>Background Image</label>
                        <input type="file" id="bg-image" accept="image/*">
                    </div>
                    
                    <div id="bg-gradient-control" style="display:none">
                        <label for="gradient-color1">Gradient Color 1</label>
                        <input type="color" id="gradient-color1" value="#3498db">
                        <label for="gradient-color2">Gradient Color 2</label>
                        <input type="color" id="gradient-color2" value="#2ecc71">
                    </div>
                </div>
                
                <div class="control-group">
                    <label for="question-color">Question Box Color</label>
                    <input type="color" id="question-color" value="#3498db">
                    
                    <label for="answer-color">Answer Box Color</label>
                    <input type="color" id="answer-color" value="#2ecc71">
                    
                    <label for="text-color">Text Color</label>
                    <input type="color" id="text-color" value="#ffffff">
                    
                    <label>Text Size</label>
                    <div class="font-size-controls">
                        <button id="font-decrease" class="font-size-btn">-</button>
                        <div id="font-size-value" class="font-size-value">1.2rem</div>
                        <button id="font-increase" class="font-size-btn">+</button>
                    </div>
                    
                    <label for="countdown-enabled">Show Countdown</label>
                    <input type="checkbox" id="countdown-enabled" checked>
                    
                    <label for="countdown-position">Countdown Position</label>
                    <select id="countdown-position">
                        <option value="below">Below Question</option>
                        <option value="top-right">Top Right</option>
                        <option value="top-left">Top Left</option>
                    </select>
                    
                    <label for="countdown-color">Countdown Color</label>
                    <input type="color" id="countdown-color" value="#e74c3c">
                </div>
            </div>
            
            <div style="display: flex; gap: 10px; margin-top: 15px;">
                <button id="preview-btn">Preview First QA</button>
                <button id="start-preview-btn">Start Full Preview</button>
                <button id="stop-preview-btn" disabled>Stop Preview</button>
            </div>
        </div>
        
        <div class="section">
            <h2>Preview</h2>
            <div class="preview-container" id="preview-container">
                <div class="video-frame" id="video-frame">
                    <div class="question-box" id="question-box"></div>
                    <div class="answer-box" id="answer-box"></div>
                    <div class="countdown" id="countdown"></div>
                </div>
            </div>
            
            <!-- Screen Recorder Section -->
            <div class="screen-selector" id="screen-selector">
                <label>Select what to record:</label>
                <div class="screen-selector-options">
                    <div class="screen-selector-option selected" data-type="preview">Preview Only</div>
                    <div class="screen-selector-option" data-type="window">Application Window</div>
                    <div class="screen-selector-option" data-type="screen">Full Screen</div>
                    <div class="screen-selector-option" data-type="tab">Browser Tab</div>
                </div>
            </div>
            
            <div class="recorder-controls">
                <button id="start-recording-btn" class="recorder-btn start">Start Recording</button>
                <button id="stop-recording-btn" class="recorder-btn" disabled>Stop Recording</button>
                <button id="restart-recording-btn" class="recorder-btn restart" disabled>Restart Recording</button>
                <button id="download-recording-btn" class="recorder-btn" disabled>Download Video</button>
                
                <div class="recording-indicator" id="recording-indicator" style="display: none;">
                    <div class="recording-dot"></div>
                    <span>Recording</span>
                    <div class="recording-timer" id="recording-timer">00:00</div>
                </div>
            </div>
        </div>
        
        <!-- Recording Preview Container -->
        <div class="section recording-container" id="recording-container">
            <h2>Recorded Video</h2>
            <video id="recorded-video" controls></video>
        </div>
    </div>

    <script>
        // DOM Elements
        const elements = {
            qaInput: document.getElementById('qa-input'),
            aspectRatio: document.getElementById('aspect-ratio'),
            layout: document.getElementById('layout'),
            questionTime: document.getElementById('question-time'),
            answerTime: document.getElementById('answer-time'),
            countdownTime: document.getElementById('countdown-time'),
            bgType: document.getElementById('bg-type'),
            bgColor: document.getElementById('bg-color'),
            bgImage: document.getElementById('bg-image'),
            gradientColor1: document.getElementById('gradient-color1'),
            gradientColor2: document.getElementById('gradient-color2'),
            questionColor: document.getElementById('question-color'),
            answerColor: document.getElementById('answer-color'),
            textColor: document.getElementById('text-color'),
            countdownEnabled: document.getElementById('countdown-enabled'),
            countdownPosition: document.getElementById('countdown-position'),
            countdownColor: document.getElementById('countdown-color'),
            previewBtn: document.getElementById('preview-btn'),
            startPreviewBtn: document.getElementById('start-preview-btn'),
            stopPreviewBtn: document.getElementById('stop-preview-btn'),
            previewContainer: document.getElementById('preview-container'),
            videoFrame: document.getElementById('video-frame'),
            questionBox: document.getElementById('question-box'),
            answerBox: document.getElementById('answer-box'),
            countdown: document.getElementById('countdown'),
            bgColorControl: document.getElementById('bg-color-control'),
            bgImageControl: document.getElementById('bg-image-control'),
            bgGradientControl: document.getElementById('bg-gradient-control'),
            // Screen recorder elements
            startRecordingBtn: document.getElementById('start-recording-btn'),
            stopRecordingBtn: document.getElementById('stop-recording-btn'),
            restartRecordingBtn: document.getElementById('restart-recording-btn'),
            downloadRecordingBtn: document.getElementById('download-recording-btn'),
            recordingIndicator: document.getElementById('recording-indicator'),
            recordingTimer: document.getElementById('recording-timer'),
            recordedVideo: document.getElementById('recorded-video'),
            recordingContainer: document.getElementById('recording-container'),
            screenSelectorOptions: document.querySelectorAll('.screen-selector-option'),
            // Font size controls
            fontDecreaseBtn: document.getElementById('font-decrease'),
            fontIncreaseBtn: document.getElementById('font-increase'),
            fontSizeValue: document.getElementById('font-size-value')
        };

        // State
        let state = {
            qaPairs: [],
            isPreviewing: false,
            currentIndex: 0,
            backgroundImage: null,
            previewInterval: null,
            countdownInterval: null,
            audioContext: null,
            // Screen recorder state
            mediaRecorder: null,
            recordedChunks: [],
            recordingStartTime: null,
            recordingTimerInterval: null,
            recordingType: 'preview',
            // Font size state
            currentFontSize: 1.2 // in rem
        };

        // Initialize
        function init() {
            // Check if screen recording is supported
            if (!navigator.mediaDevices || !navigator.mediaDevices.getDisplayMedia) {
                alert("Screen recording is not supported in your browser or you're not in a secure context (try https:// or localhost)");
                elements.startRecordingBtn.disabled = true;
                elements.startRecordingBtn.title = "Screen recording not supported";
                return;
            }

            setupEventListeners();
            updateBackgroundControls();
            updatePreview();
            updateFontSizeDisplay();
            
            // Initialize Web Audio API
            try {
                state.audioContext = new (window.AudioContext || window.webkitAudioContext)();
            } catch (e) {
                console.error("Web Audio API not supported");
            }
        }

        // Event Listeners
        function setupEventListeners() {
            // Existing event listeners
            elements.bgType.addEventListener('change', updateBackgroundControls);
            elements.previewBtn.addEventListener('click', previewFirstQA);
            elements.startPreviewBtn.addEventListener('click', startFullPreview);
            elements.stopPreviewBtn.addEventListener('click', stopFullPreview);
            elements.bgImage.addEventListener('change', handleImageUpload);
            
            // Screen recorder event listeners
            elements.startRecordingBtn.addEventListener('click', startRecording);
            elements.stopRecordingBtn.addEventListener('click', stopRecording);
            elements.restartRecordingBtn.addEventListener('click', restartRecording);
            elements.downloadRecordingBtn.addEventListener('click', downloadRecording);
            
            // Screen selector options
            elements.screenSelectorOptions.forEach(option => {
                option.addEventListener('click', () => {
                    elements.screenSelectorOptions.forEach(opt => opt.classList.remove('selected'));
                    option.classList.add('selected');
                    state.recordingType = option.dataset.type;
                });
            });
            
            // Font size controls
            elements.fontDecreaseBtn.addEventListener('click', decreaseFontSize);
            elements.fontIncreaseBtn.addEventListener('click', increaseFontSize);
            
            // Update preview when settings change
            const previewUpdateElements = [
                elements.aspectRatio, elements.layout,
                elements.questionColor, elements.answerColor,
                elements.textColor, elements.bgColor,
                elements.gradientColor1, elements.gradientColor2,
                elements.countdownEnabled, elements.countdownPosition,
                elements.countdownColor
            ];
            
            previewUpdateElements.forEach(el => {
                el.addEventListener('input', updatePreview);
                el.addEventListener('change', updatePreview);
            });
        }

        // Font size functions
        function updateFontSizeDisplay() {
            elements.fontSizeValue.textContent = `${state.currentFontSize}rem`;
            elements.questionBox.style.fontSize = `${state.currentFontSize}rem`;
            elements.answerBox.style.fontSize = `${state.currentFontSize}rem`;
        }

        function decreaseFontSize() {
            if (state.currentFontSize > 0.8) {
                state.currentFontSize -= 0.1;
                updateFontSizeDisplay();
            }
        }

        function increaseFontSize() {
            if (state.currentFontSize < 2.5) {
                state.currentFontSize += 0.1;
                updateFontSizeDisplay();
            }
        }

        // Screen recorder functions
        async function startRecording() {
            try {
                let stream;
                
                if (state.recordingType === 'preview') {
                    // For preview only, we'll use the display capture API
                    stream = await navigator.mediaDevices.getDisplayMedia({
                        video: {
                            displaySurface: 'window'
                        },
                        audio: false
                    });
                } else {
                    // Use browser's screen capture API
                    const displayMediaOptions = {
                        audio: false,
                        video: {
                            displaySurface: state.recordingType === 'window' ? 'window' : 
                                           state.recordingType === 'tab' ? 'browser' : 'monitor'
                        }
                    };
                    
                    stream = await navigator.mediaDevices.getDisplayMedia(displayMediaOptions);
                }
                
                state.mediaRecorder = new MediaRecorder(stream, {
                    mimeType: 'video/webm;codecs=vp9'
                });
                
                state.recordedChunks = [];
                state.mediaRecorder.ondataavailable = handleDataAvailable;
                state.mediaRecorder.onstop = handleRecordingStop;
                
                state.mediaRecorder.start(100); // Collect data every 100ms
                
                // Start recording timer
                state.recordingStartTime = Date.now();
                updateRecordingTimer();
                state.recordingTimerInterval = setInterval(updateRecordingTimer, 1000);
                
                // Update UI
                elements.startRecordingBtn.disabled = true;
                elements.stopRecordingBtn.disabled = false;
                elements.restartRecordingBtn.disabled = false;
                elements.downloadRecordingBtn.disabled = true;
                elements.recordingIndicator.style.display = 'flex';
                elements.recordingContainer.style.display = 'none';
                
                // When the stream ends (user stops sharing)
                stream.getVideoTracks()[0].onended = () => {
                    stopRecording();
                };
                
            } catch (err) {
                console.error("Error starting recording:", err);
                alert("Could not start recording: " + err.message);
            }
        }
        
        function handleDataAvailable(event) {
            if (event.data.size > 0) {
                state.recordedChunks.push(event.data);
            }
        }
        
        function handleRecordingStop() {
            clearInterval(state.recordingTimerInterval);
            
            const blob = new Blob(state.recordedChunks, {
                type: 'video/webm'
            });
            
            const videoURL = URL.createObjectURL(blob);
            elements.recordedVideo.src = videoURL;
            elements.recordingContainer.style.display = 'block';
            
            // Clean up
            if (state.mediaRecorder && state.mediaRecorder.stream) {
                state.mediaRecorder.stream.getTracks().forEach(track => track.stop());
            }
            
            // Update UI
            elements.startRecordingBtn.disabled = false;
            elements.stopRecordingBtn.disabled = true;
            elements.restartRecordingBtn.disabled = false;
            elements.downloadRecordingBtn.disabled = false;
            elements.recordingIndicator.style.display = 'none';
        }
        
        function stopRecording() {
            if (state.mediaRecorder && state.mediaRecorder.state !== 'inactive') {
                state.mediaRecorder.stop();
            }
        }
        
        function restartRecording() {
            stopRecording();
            setTimeout(startRecording, 500);
        }
        
        function downloadRecording() {
            const blob = new Blob(state.recordedChunks, {
                type: 'video/webm'
            });
            
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.style.display = 'none';
            a.href = url;
            a.download = `quiz-video-${new Date().toISOString().slice(0, 10)}.webm`;
            document.body.appendChild(a);
            a.click();
            
            setTimeout(() => {
                document.body.removeChild(a);
                window.URL.revokeObjectURL(url);
            }, 100);
        }
        
        function updateRecordingTimer() {
            const elapsed = Math.floor((Date.now() - state.recordingStartTime) / 1000);
            const minutes = Math.floor(elapsed / 60).toString().padStart(2, '0');
            const seconds = (elapsed % 60).toString().padStart(2, '0');
            elements.recordingTimer.textContent = `${minutes}:${seconds}`;
        }

        // Quiz functionality functions
        function updateBackgroundControls() {
            const type = elements.bgType.value;
            elements.bgColorControl.style.display = type === 'color' ? 'block' : 'none';
            elements.bgImageControl.style.display = type === 'image' ? 'block' : 'none';
            elements.bgGradientControl.style.display = type === 'gradient' ? 'block' : 'none';
            updatePreview();
        }

        function handleImageUpload(e) {
            const file = e.target.files[0];
            if (file) {
                const reader = new FileReader();
                reader.onload = (event) => {
                    state.backgroundImage = event.target.result;
                    updatePreview();
                };
                reader.readAsDataURL(file);
            }
        }

        function playSound(type) {
            if (!state.audioContext) return;
            
            const oscillator = state.audioContext.createOscillator();
            const gainNode = state.audioContext.createGain();
            
            oscillator.connect(gainNode);
            gainNode.connect(state.audioContext.destination);
            
            if (type === 'question') {
                oscillator.frequency.value = 880;
            } else if (type === 'answer') {
                oscillator.frequency.value = 440;
            } else if (type === 'tick') {
                oscillator.frequency.value = 660;
            }
            
            gainNode.gain.setValueAtTime(0.5, state.audioContext.currentTime);
            oscillator.start();
            gainNode.gain.exponentialRampToValueAtTime(0.01, state.audioContext.currentTime + 0.3);
            oscillator.stop(state.audioContext.currentTime + 0.3);
        }

        function updatePreview() {
            // Aspect ratio
            elements.previewContainer.style.aspectRatio = elements.aspectRatio.value;
            
            // Layout
            if (elements.layout.value === 'stacked') {
                elements.videoFrame.style.flexDirection = 'column';
                elements.videoFrame.style.gap = '20px';
            } else {
                elements.videoFrame.style.flexDirection = 'row';
                elements.videoFrame.style.gap = '40px';
            }
            
            // Colors
            elements.questionBox.style.backgroundColor = elements.questionColor.value;
            elements.answerBox.style.backgroundColor = elements.answerColor.value;
            elements.questionBox.style.color = elements.textColor.value;
            elements.answerBox.style.color = elements.textColor.value;
            
            // Background
            switch(elements.bgType.value) {
                case 'color':
                    elements.previewContainer.style.background = elements.bgColor.value;
                    break;
                case 'image':
                    if (state.backgroundImage) {
                        elements.previewContainer.style.background = `url('${state.backgroundImage}')`;
                        elements.previewContainer.style.backgroundSize = 'cover';
                    }
                    break;
                case 'gradient':
                    elements.previewContainer.style.background = 
                        `linear-gradient(${elements.gradientColor1.value}, ${elements.gradientColor2.value})`;
                    break;
            }
            
            // Countdown styling
            elements.countdown.style.color = elements.countdownColor.value;
            
            // Position countdown
            positionCountdown();
        }

        function positionCountdown() {
            elements.countdown.style.top = '';
            elements.countdown.style.bottom = '';
            elements.countdown.style.left = '';
            elements.countdown.style.right = '';
            elements.countdown.style.transform = '';
            
            if (elements.countdownPosition.value === 'below') {
                elements.countdown.style.top = 'calc(50% + 60px)';
                elements.countdown.style.left = '50%';
                elements.countdown.style.transform = 'translateX(-50%)';
            } else if (elements.countdownPosition.value === 'top-right') {
                elements.countdown.style.top = '10px';
                elements.countdown.style.right = '10px';
            } else if (elements.countdownPosition.value === 'top-left') {
                elements.countdown.style.top = '10px';
                elements.countdown.style.left = '10px';
            }
        }

        function parseQAInput() {
            const lines = elements.qaInput.value.split('\n');
            state.qaPairs = lines
                .filter(line => line.trim() !== '')
                .map(line => {
                    const [question, answer] = line.split('|').map(part => part.trim());
                    return { question, answer };
                })
                .filter(qa => qa.question && qa.answer);
            
            return state.qaPairs.length > 0;
        }

        function showQuestion(index) {
            if (index < 0 || index >= state.qaPairs.length) return false;
            
            hideQA();
            hideCountdown();
            
            elements.questionBox.textContent = state.qaPairs[index].question;
            elements.questionBox.classList.add('visible');
            
            playSound('question');
            
            return true;
        }

        function showAnswer(index) {
            if (index < 0 || index >= state.qaPairs.length) return false;
            
            elements.answerBox.textContent = state.qaPairs[index].answer;
            elements.answerBox.classList.add('visible');
            
            playSound('answer');
            
            return true;
        }

        function hideQA() {
            elements.questionBox.classList.remove('visible');
            elements.answerBox.classList.remove('visible');
        }

        function showCountdown(seconds, callback) {
            if (!elements.countdownEnabled.checked) {
                if (callback) setTimeout(callback, seconds * 1000);
                return;
            }
            
            let remaining = seconds;
            elements.countdown.textContent = remaining;
            elements.countdown.classList.add('visible');
            
            state.countdownInterval = setInterval(() => {
                remaining--;
                elements.countdown.textContent = remaining;
                
                playSound('tick');
                
                if (remaining <= 0) {
                    clearInterval(state.countdownInterval);
                    hideCountdown();
                    if (callback) callback();
                }
            }, 1000);
        }

        function hideCountdown() {
            elements.countdown.classList.remove('visible');
        }

        function previewFirstQA() {
            if (!parseQAInput()) {
                alert('Please enter valid questions and answers.');
                return;
            }
            
            updatePreview();
            showQuestion(0);
            
            setTimeout(() => {
                showCountdown(elements.countdownTime.value, () => {
                    showAnswer(0);
                    
                    setTimeout(() => {
                        hideQA();
                    }, elements.answerTime.value * 1000);
                });
            }, elements.questionTime.value * 1000);
        }

        function startFullPreview() {
            if (!parseQAInput()) {
                alert('Please enter valid questions and answers.');
                return;
            }
            
            state.isPreviewing = true;
            state.currentIndex = 0;
            elements.startPreviewBtn.disabled = true;
            elements.stopPreviewBtn.disabled = false;
            updatePreview();
            
            runPreviewSequence();
        }

        function runPreviewSequence() {
            if (!state.isPreviewing || state.currentIndex >= state.qaPairs.length) {
                stopFullPreview();
                return;
            }
            
            showQuestion(state.currentIndex);
            
            setTimeout(() => {
                showCountdown(elements.countdownTime.value, () => {
                    showAnswer(state.currentIndex);
                    
                    setTimeout(() => {
                        hideQA();
                        state.currentIndex++;
                        
                        setTimeout(() => {
                            runPreviewSequence();
                        }, 1000);
                    }, elements.answerTime.value * 1000);
                });
            }, elements.questionTime.value * 1000);
        }

        function stopFullPreview() {
            state.isPreviewing = false;
            clearInterval(state.countdownInterval);
            hideCountdown();
            elements.startPreviewBtn.disabled = false;
            elements.stopPreviewBtn.disabled = true;
            hideQA();
        }

        // Initialize
        init();
    </script>
</body>
</html>
