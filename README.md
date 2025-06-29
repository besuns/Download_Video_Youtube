# Download_Video_Youtube
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>VidGrab - YouTube Downloader</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 20px;
            position: relative;
            overflow-x: hidden;
        }

        .background-animation {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
            opacity: 0.1;
        }

        .floating-shape {
            position: absolute;
            border-radius: 50%;
            background: rgba(255, 255, 255, 0.1);
            animation: float 6s ease-in-out infinite;
        }

        .floating-shape:nth-child(1) {
            width: 80px;
            height: 80px;
            top: 20%;
            left: 10%;
            animation-delay: 0s;
        }

        .floating-shape:nth-child(2) {
            width: 120px;
            height: 120px;
            top: 60%;
            right: 15%;
            animation-delay: 2s;
        }

        .floating-shape:nth-child(3) {
            width: 60px;
            height: 60px;
            bottom: 20%;
            left: 20%;
            animation-delay: 4s;
        }

        @keyframes float {
            0%, 100% { transform: translateY(0px) rotate(0deg); }
            33% { transform: translateY(-20px) rotate(120deg); }
            66% { transform: translateY(10px) rotate(240deg); }
        }

        .container {
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(20px);
            border-radius: 20px;
            padding: 40px;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.1);
            width: 100%;
            max-width: 600px;
            border: 1px solid rgba(255, 255, 255, 0.2);
            animation: slideUp 0.8s ease-out;
        }

        @keyframes slideUp {
            from {
                opacity: 0;
                transform: translateY(30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .header {
            text-align: center;
            margin-bottom: 30px;
        }

        .logo {
            font-size: 2.5rem;
            font-weight: bold;
            background: linear-gradient(135deg, #ff6b6b, #ee5a24);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            margin-bottom: 10px;
        }

        .subtitle {
            color: #666;
            font-size: 1.1rem;
            margin-bottom: 20px;
        }

        .features {
            display: flex;
            justify-content: space-around;
            margin-bottom: 30px;
            flex-wrap: wrap;
            gap: 10px;
        }

        .feature {
            background: linear-gradient(135deg, #a8edea, #fed6e3);
            padding: 8px 16px;
            border-radius: 20px;
            font-size: 0.9rem;
            font-weight: 500;
            color: #333;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
        }

        .input-section {
            margin-bottom: 30px;
        }

        .input-group {
            position: relative;
            margin-bottom: 20px;
        }

        .input-field {
            width: 100%;
            padding: 15px 20px;
            border: 2px solid #e0e0e0;
            border-radius: 15px;
            font-size: 1rem;
            transition: all 0.3s ease;
            outline: none;
            background: rgba(255, 255, 255, 0.9);
        }

        .input-field:focus {
            border-color: #667eea;
            box-shadow: 0 0 20px rgba(102, 126, 234, 0.2);
            transform: translateY(-2px);
        }

        .quality-selector {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(120px, 1fr));
            gap: 15px;
            margin-bottom: 20px;
        }

        .quality-option {
            position: relative;
        }

        .quality-radio {
            display: none;
        }

        .quality-label {
            display: block;
            padding: 12px 16px;
            border: 2px solid #e0e0e0;
            border-radius: 12px;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s ease;
            background: rgba(255, 255, 255, 0.7);
            font-weight: 500;
        }

        .quality-radio:checked + .quality-label {
            border-color: #667eea;
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            transform: translateY(-2px);
            box-shadow: 0 8px 25px rgba(102, 126, 234, 0.3);
        }

        .format-selector {
            display: flex;
            gap: 15px;
            margin-bottom: 25px;
            flex-wrap: wrap;
        }

        .format-btn {
            flex: 1;
            min-width: 100px;
            padding: 12px 20px;
            border: 2px solid #e0e0e0;
            border-radius: 12px;
            background: rgba(255, 255, 255, 0.7);
            cursor: pointer;
            transition: all 0.3s ease;
            font-weight: 500;
            text-align: center;
        }

        .format-btn.active,
        .format-btn:hover {
            border-color: #667eea;
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            transform: translateY(-2px);
            box-shadow: 0 8px 25px rgba(102, 126, 234, 0.3);
        }

        .download-btn {
            width: 100%;
            padding: 18px;
            background: linear-gradient(135deg, #ff6b6b, #ee5a24);
            border: none;
            border-radius: 15px;
            color: white;
            font-size: 1.1rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 10px 30px rgba(255, 107, 107, 0.4);
            position: relative;
            overflow: hidden;
        }

        .download-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 15px 40px rgba(255, 107, 107, 0.5);
        }

        .download-btn:active {
            transform: translateY(-1px);
        }

        .download-btn:disabled {
            opacity: 0.6;
            cursor: not-allowed;
            transform: none;
        }

        .progress-bar {
            width: 100%;
            height: 6px;
            background: #e0e0e0;
            border-radius: 3px;
            margin-top: 20px;
            overflow: hidden;
            display: none;
        }

        .progress-fill {
            height: 100%;
            background: linear-gradient(90deg, #667eea, #764ba2);
            width: 0%;
            transition: width 0.3s ease;
            border-radius: 3px;
        }

        .status-message {
            margin-top: 15px;
            padding: 12px;
            border-radius: 8px;
            text-align: center;
            display: none;
        }

        .status-success {
            background: #d4edda;
            color: #155724;
            border: 1px solid #c3e6cb;
        }

        .status-error {
            background: #f8d7da;
            color: #721c24;
            border: 1px solid #f5c6cb;
        }

        .advanced-options {
            margin-top: 25px;
            padding: 20px;
            background: rgba(102, 126, 234, 0.05);
            border-radius: 15px;
            border: 1px solid rgba(102, 126, 234, 0.1);
        }

        .advanced-title {
            font-weight: 600;
            color: #333;
            margin-bottom: 15px;
            display: flex;
            align-items: center;
            cursor: pointer;
        }

        .advanced-content {
            display: none;
        }

        .advanced-content.show {
            display: block;
            animation: slideDown 0.3s ease-out;
        }

        @keyframes slideDown {
            from {
                opacity: 0;
                max-height: 0;
            }
            to {
                opacity: 1;
                max-height: 200px;
            }
        }

        .checkbox-group {
            display: flex;
            align-items: center;
            margin-bottom: 15px;
        }

        .checkbox {
            margin-right: 10px;
            width: 18px;
            height: 18px;
            accent-color: #667eea;
        }

        .footer {
            text-align: center;
            margin-top: 30px;
            color: #666;
            font-size: 0.9rem;
        }

        @media (max-width: 600px) {
            .container {
                padding: 25px;
                margin: 10px;
            }
            
            .quality-selector {
                grid-template-columns: repeat(2, 1fr);
            }
            
            .format-selector {
                flex-direction: column;
            }
        }
    </style>
</head>
<body>
    <div class="background-animation">
        <div class="floating-shape"></div>
        <div class="floating-shape"></div>
        <div class="floating-shape"></div>
    </div>

    <div class="container">
        <div class="header">
            <div class="logo">VidGrab</div>
            <div class="subtitle">Fast & Free YouTube Video Downloader</div>
            <div class="features">
                <span class="feature">HD Quality</span>
                <span class="feature">Multiple Formats</span>
                <span class="feature">Audio Only</span>
                <span class="feature">No Watermarks</span>
            </div>
        </div>

        <div class="input-section">
            <div class="input-group">
                <input type="text" class="input-field" id="videoUrl" placeholder="Paste YouTube video URL here..." />
            </div>

            <div class="quality-selector">
                <div class="quality-option">
                    <input type="radio" name="quality" value="highest" id="quality-highest" class="quality-radio" checked>
                    <label for="quality-highest" class="quality-label">Best Quality</label>
                </div>
                <div class="quality-option">
                    <input type="radio" name="quality" value="720p" id="quality-720p" class="quality-radio">
                    <label for="quality-720p" class="quality-label">720p HD</label>
                </div>
                <div class="quality-option">
                    <input type="radio" name="quality" value="480p" id="quality-480p" class="quality-radio">
                    <label for="quality-480p" class="quality-label">480p</label>
                </div>
                <div class="quality-option">
                    <input type="radio" name="quality" value="360p" id="quality-360p" class="quality-radio">
                    <label for="quality-360p" class="quality-label">360p</label>
                </div>
            </div>

            <div class="format-selector">
                <div class="format-btn active" data-format="mp4">MP4 Video</div>
                <div class="format-btn" data-format="mp3">MP3 Audio</div>
                <div class="format-btn" data-format="webm">WebM</div>
            </div>

            <div class="advanced-options">
                <div class="advanced-title" onclick="toggleAdvanced()">
                    ⚙️ Advanced Options
                </div>
                <div class="advanced-content" id="advancedContent">
                    <div class="checkbox-group">
                        <input type="checkbox" id="extractAudio" class="checkbox">
                        <label for="extractAudio">Extract audio track separately</label>
                    </div>
                    <div class="checkbox-group">
                        <input type="checkbox" id="includeSubs" class="checkbox">
                        <label for="includeSubs">Download subtitles (if available)</label>
                    </div>
                    <div class="checkbox-group">
                        <input type="checkbox" id="customName" class="checkbox">
                        <label for="customName">Use video title as filename</label>
                    </div>
                </div>
            </div>

            <button class="download-btn" onclick="downloadVideo()">
                <span id="downloadText">🚀 Download Video</span>
            </button>

            <div class="progress-bar" id="progressBar">
                <div class="progress-fill" id="progressFill"></div>
            </div>

            <div class="status-message" id="statusMessage"></div>
        </div>

        <div class="footer">
            <p>⚡ Fast downloads • 🔒 Secure • 💯 Free forever</p>
            <p style="margin-top: 10px; font-size: 0.8rem;">Supports YouTube, YouTube Music, and YouTube Shorts</p>
        </div>
    </div>

    <script>
        let selectedFormat = 'mp4';
        let downloadHistory = [];

        // Format selection
        document.querySelectorAll('.format-btn').forEach(btn => {
            btn.addEventListener('click', function() {
                document.querySelectorAll('.format-btn').forEach(b => b.classList.remove('active'));
                this.classList.add('active');
                selectedFormat = this.dataset.format;
                updateDownloadButton();
            });
        });

        function updateDownloadButton() {
            const btn = document.getElementById('downloadText');
            const icons = {
                'mp4': '🎬',
                'mp3': '🎵',
                'webm': '📹'
            };
            btn.innerHTML = `${icons[selectedFormat]} Download ${selectedFormat.toUpperCase()}`;
        }

        function toggleAdvanced() {
            const content = document.getElementById('advancedContent');
            content.classList.toggle('show');
        }

        function isValidYouTubeUrl(url) {
            const regex = /^(https?\:\/\/)?(www\.)?(youtube\.com|youtu\.be)\/.+/;
            return regex.test(url);
        }

        function extractVideoId(url) {
            const regex = /(?:youtube\.com\/watch\?v=|youtu\.be\/|youtube\.com\/embed\/)([^&\n?#]+)/;
            const match = url.match(regex);
            return match ? match[1] : null;
        }

        function showStatus(message, type) {
            const statusEl = document.getElementById('statusMessage');
            statusEl.textContent = message;
            statusEl.className = `status-message status-${type}`;
            statusEl.style.display = 'block';
            
            setTimeout(() => {
                statusEl.style.display = 'none';
            }, 5000);
        }

        function simulateProgress() {
            const progressBar = document.getElementById('progressBar');
            const progressFill = document.getElementById('progressFill');
            
            progressBar.style.display = 'block';
            let progress = 0;
            
            const interval = setInterval(() => {
                progress += Math.random() * 20;
                if (progress > 100) progress = 100;
                
                progressFill.style.width = progress + '%';
                
                if (progress >= 100) {
                    clearInterval(interval);
                    setTimeout(() => {
                        progressBar.style.display = 'none';
                        progressFill.style.width = '0%';
                    }, 1000);
                }
            }, 300);
        }

        async function downloadVideo() {
            const url = document.getElementById('videoUrl').value.trim();
            const downloadBtn = document.querySelector('.download-btn');
            
            if (!url) {
                showStatus('Please enter a YouTube video URL', 'error');
                return;
            }
            
            if (!isValidYouTubeUrl(url)) {
                showStatus('Please enter a valid YouTube URL', 'error');
                return;
            }
            
            const videoId = extractVideoId(url);
            if (!videoId) {
                showStatus('Could not extract video ID from URL', 'error');
                return;
            }
            
            // Get selected options
            const quality = document.querySelector('input[name="quality"]:checked').value;
            const extractAudio = document.getElementById('extractAudio').checked;
            const includeSubs = document.getElementById('includeSubs').checked;
            const customName = document.getElementById('customName').checked;
            
            // Disable button and show loading
            downloadBtn.disabled = true;
            downloadBtn.innerHTML = '⏳ Processing...';
            
            try {
                // Simulate download process
                simulateProgress();
                
                // Store download in history
                const downloadInfo = {
                    url: url,
                    format: selectedFormat,
                    quality: quality,
                    timestamp: new Date().toLocaleString(),
                    options: {
                        extractAudio,
                        includeSubs,
                        customName
                    }
                };
                
                downloadHistory.push(downloadInfo);
                
                // Simulate processing time
                await new Promise(resolve => setTimeout(resolve, 3000));
                
                // In a real implementation, you would:
                // 1. Send the video URL to a backend service
                // 2. The backend would use libraries like youtube-dl or yt-dlp
                // 3. Process the video according to selected options
                // 4. Return download links or stream the file
                
                // For demo purposes, create a sample download link
                const downloadUrl = `https://example.com/download/${videoId}.${selectedFormat}`;
                
                // Create a temporary download link (this would be the actual file in production)
                const a = document.createElement('a');
                a.href = '#'; // In production, this would be the actual download URL
                a.download = `video.${selectedFormat}`;
                
                showStatus(`✅ Download prepared! Format: ${selectedFormat.toUpperCase()}, Quality: ${quality}`, 'success');
                
                // Log download attempt
                console.log('Download initiated:', downloadInfo);
                
            } catch (error) {
                showStatus('Download failed. Please try again.', 'error');
                console.error('Download error:', error);
            } finally {
                // Re-enable button
                downloadBtn.disabled = false;
                updateDownloadButton();
            }
        }

        // Auto-detect URL from clipboard on focus
        document.getElementById('videoUrl').addEventListener('focus', async function() {
            try {
                const text = await navigator.clipboard.readText();
                if (isValidYouTubeUrl(text) && !this.value) {
                    this.value = text;
                    showStatus('YouTube URL detected from clipboard!', 'success');
                }
            } catch (err) {
                // Clipboard access not available or denied
            }
        });

        // Enter key to download
        document.getElementById('videoUrl').addEventListener('keypress', function(e) {
            if (e.key === 'Enter') {
                downloadVideo();
            }
        });

        // Initialize
        updateDownloadButton();
    </script>
</body>
</html>
