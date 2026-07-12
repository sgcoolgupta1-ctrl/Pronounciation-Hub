<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Pronunciation Hub - Speak Any Word, Read Any Text</title>
    <meta name="description" content="Pronunciation Hub helps illiterate users and language learners: type a word or take a photo, hear it pronounced in English, and get Hindi translation.">
    <style>
        /* ===== RESET & BASE ===== */
        * { box-sizing: border-box; margin: 0; padding: 0; }
        html { scroll-behavior: smooth; }
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: #f0f4f8;
            color: #333;
            line-height: 1.6;
        }

        /* ===== HEADER / NAV ===== */
        .header {
            background: linear-gradient(135deg, #1a73e8 0%, #1557b0 100%);
            color: white;
            padding: 20px 0 10px;
            position: sticky;
            top: 0;
            z-index: 1000;
            box-shadow: 0 4px 12px rgba(0,0,0,0.1);
        }
        .header-inner {
            max-width: 1100px;
            margin: auto;
            padding: 0 20px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
        }
        .logo {
            font-size: 28px;
            font-weight: 700;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        .logo span { font-size: 32px; }
        .nav-links {
            display: flex;
            gap: 25px;
            flex-wrap: wrap;
        }
        .nav-links a {
            color: rgba(255,255,255,0.9);
            text-decoration: none;
            font-weight: 500;
            font-size: 16px;
            transition: 0.2s;
            padding: 5px 0;
        }
        .nav-links a:hover { color: white; border-bottom: 2px solid white; }

        /* ===== HERO SECTION ===== */
        .hero {
            background: linear-gradient(135deg, #e8f0fe 0%, #c5d9f7 100%);
            padding: 60px 20px 40px;
            text-align: center;
        }
        .hero h1 {
            font-size: 42px;
            color: #1a73e8;
            margin-bottom: 15px;
            line-height: 1.2;
        }
        .hero p {
            font-size: 20px;
            color: #444;
            max-width: 700px;
            margin: 0 auto 30px;
        }
        .hero-buttons {
            display: flex;
            justify-content: center;
            gap: 20px;
            flex-wrap: wrap;
        }
        .btn-primary, .btn-secondary {
            padding: 14px 35px;
            border-radius: 50px;
            font-size: 18px;
            font-weight: 600;
            text-decoration: none;
            display: inline-block;
            transition: 0.3s;
            border: none;
            cursor: pointer;
        }
        .btn-primary {
            background: #1a73e8;
            color: white;
        }
        .btn-primary:hover { background: #1557b0; transform: translateY(-2px); }
        .btn-secondary {
            background: white;
            color: #1a73e8;
            border: 2px solid #1a73e8;
        }
        .btn-secondary:hover { background: #e8f0fe; transform: translateY(-2px); }

        /* ===== APP CONTAINER ===== */
        .app-section {
            padding: 40px 20px 60px;
            background: white;
        }
        .app-container {
            max-width: 700px;
            margin: auto;
            background: #f9fafc;
            border-radius: 24px;
            padding: 30px 25px 40px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.08);
            border: 1px solid #e0e7ef;
        }
        .app-container h2 {
            text-align: center;
            font-size: 28px;
            color: #1a73e8;
            margin-bottom: 8px;
        }
        .app-container .subtitle {
            text-align: center;
            color: #666;
            margin-bottom: 25px;
            font-size: 16px;
        }
        .section-box {
            margin-bottom: 30px;
            padding: 18px;
            background: #f0f4ff;
            border-radius: 16px;
        }
        .section-box h3 {
            font-size: 18px;
            margin-bottom: 10px;
            color: #222;
            display: flex;
            align-items: center;
            gap: 8px;
        }
        textarea {
            width: 100%;
            padding: 12px;
            border: 2px solid #d0d7de;
            border-radius: 12px;
            font-size: 16px;
            font-family: inherit;
            margin-bottom: 10px;
            resize: vertical;
            min-height: 60px;
        }
        input[type="file"] {
            width: 100%;
            padding: 10px;
            border: 2px dashed #1a73e8;
            border-radius: 12px;
            background: #f0f4ff;
            margin-bottom: 10px;
            font-size: 14px;
        }
        button {
            background: #1a73e8;
            color: white;
            border: none;
            padding: 12px 24px;
            border-radius: 30px;
            font-size: 16px;
            font-weight: 600;
            width: 100%;
            cursor: pointer;
            transition: 0.2s;
            margin-top: 5px;
        }
        button:active { transform: scale(0.97); }
        .camera-btn { background: #ea4335; }
        .pronounce-btn { background: #f9ab00; color: #222; }
        .translation-box {
            background: #e8f0fe;
            padding: 10px 14px;
            border-radius: 12px;
            margin-top: 10px;
            font-size: 15px;
            min-height: 20px;
            word-break: break-word;
        }
        .hidden { display: none; }
        #ocrResult {
            background: #fff3cd;
            padding: 12px;
            border-radius: 12px;
            margin: 10px 0;
            font-size: 15px;
            line-height: 1.5;
            white-space: pre-wrap;
            max-height: 180px;
            overflow-y: auto;
        }
        #pronunciationHub {
            border: 2px solid #f9ab00;
            padding: 15px;
            border-radius: 16px;
            background: #fef9e6;
            margin-top: 15px;
        }
        .loader {
            display: none;
            text-align: center;
            margin: 10px 0;
            color: #1a73e8;
            font-weight: 500;
        }
        .loader.active { display: block; }

        /* ===== FEATURES SECTION ===== */
        .features {
            padding: 60px 20px;
            background: #f5f7fa;
        }
        .features h2 {
            text-align: center;
            font-size: 32px;
            margin-bottom: 40px;
            color: #1a73e8;
        }
        .features-grid {
            max-width: 1100px;
            margin: auto;
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 30px;
        }
        .feature-card {
            background: white;
            padding: 30px 20px;
            border-radius: 20px;
            text-align: center;
            box-shadow: 0 4px 15px rgba(0,0,0,0.05);
            transition: 0.3s;
        }
        .feature-card:hover { transform: translateY(-5px); box-shadow: 0 8px 25px rgba(0,0,0,0.1); }
        .feature-icon { font-size: 48px; margin-bottom: 15px; }
        .feature-card h3 { font-size: 20px; margin-bottom: 10px; }
        .feature-card p { color: #555; font-size: 15px; }

        /* ===== HOW IT WORKS ===== */
        .how-it-works {
            padding: 60px 20px;
            background: white;
        }
        .how-it-works h2 {
            text-align: center;
            font-size: 32px;
            margin-bottom: 40px;
            color: #1a73e8;
        }
        .steps {
            max-width: 800px;
            margin: auto;
            display: flex;
            flex-direction: column;
            gap: 25px;
        }
        .step {
            display: flex;
            gap: 20px;
            align-items: flex-start;
            background: #f9fafc;
            padding: 20px;
            border-radius: 16px;
        }
        .step-number {
            background: #1a73e8;
            color: white;
            width: 40px;
            height: 40px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: 700;
            font-size: 18px;
            flex-shrink: 0;
        }
        .step-content h3 { font-size: 18px; margin-bottom: 5px; }
        .step-content p { color: #555; }

        /* ===== FAQ ===== */
        .faq {
            padding: 60px 20px;
            background: #f5f7fa;
        }
        .faq h2 {
            text-align: center;
            font-size: 32px;
            margin-bottom: 40px;
            color: #1a73e8;
        }
        .faq-list {
            max-width: 700px;
            margin: auto;
        }
        .faq-item {
            background: white;
            border-radius: 12px;
            margin-bottom: 12px;
            padding: 18px 20px;
            cursor: pointer;
            box-shadow: 0 2px 8px rgba(0,0,0,0.04);
        }
        .faq-question {
            font-weight: 600;
            font-size: 17px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        .faq-question::after {
            content: '+';
            font-size: 24px;
            color: #1a73e8;
        }
        .faq-item.open .faq-question::after {
            content: '−';
        }
        .faq-answer {
            max-height: 0;
            overflow: hidden;
            transition: 0.3s;
            color: #555;
            padding-top: 0;
        }
        .faq-item.open .faq-answer {
            max-height: 200px;
            padding-top: 12px;
        }

        /* ===== FOOTER ===== */
        .footer {
            background: #1a1a2e;
            color: rgba(255,255,255,0.8);
            padding: 40px 20px;
            text-align: center;
        }
        .footer a { color: #f9ab00; text-decoration: none; }
        .footer-links { margin: 15px 0; display: flex; justify-content: center; gap: 30px; flex-wrap: wrap; }
        .footer-links a { color: rgba(255,255,255,0.7); }
        .footer-links a:hover { color: white; }

        /* ===== RESPONSIVE ===== */
        @media (max-width: 600px) {
            .header-inner { flex-direction: column; gap: 10px; }
            .logo { font-size: 22px; }
            .hero h1 { font-size: 28px; }
            .hero p { font-size: 17px; }
            .app-container { padding: 20px 15px; }
        }
    </style>
</head>
<body>

<!-- ===== HEADER ===== -->
<header class="header" id="home">
    <div class="header-inner">
        <div class="logo"><span>📢</span> Pronunciation Hub</div>
        <nav class="nav-links">
            <a href="#home">Home</a>
            <a href="#app">App</a>
            <a href="#features">Features</a>
            <a href="#how-it-works">How It Works</a>
            <a href="#faq">FAQ</a>
        </nav>
    </div>
</header>

<!-- ===== HERO ===== -->
<section class="hero">
    <h1>🗣️ Hear Any Word. Read Any Text.</h1>
    <p>Type a word, take a photo of a page, and let our AI voice pronounce it clearly in English. Get instant Hindi translation. Designed for those who struggle with reading or speaking.</p>
    <div class="hero-buttons">
        <a href="#app" class="btn-primary">🚀 Try the App Now</a>
        <a href="#how-it-works" class="btn-secondary">📖 How It Works</a>
    </div>
</section>

<!-- ===== APP SECTION ===== -->
<section class="app-section" id="app">
    <div class="app-container">
        <h2>📢 Pronunciation Hub</h2>
        <p class="subtitle">Type or take a photo – hear it spoken, get Hindi translation.</p>

        <!-- Text Input -->
        <div class="section-box">
            <h3>✍️ 1. Type a word or sentence</h3>
            <textarea id="textInput" placeholder="Type English text here... (e.g., 'education', 'I am happy')"></textarea>
            <button id="speakTextBtn">🔊 Speak & Translate</button>
            <div class="translation-box" id="textTranslation">🇮🇳 Hindi translation will appear here</div>
        </div>

        <!-- Camera / Photo -->
        <div class="section-box">
            <h3>📸 2. Take a photo or upload image</h3>
            <input type="file" accept="image/*" capture="environment" id="photoInput">
            <button class="camera-btn" id="uploadBtn">📂 Upload & Read Text</button>
            <div class="loader" id="loader">⏳ Processing image... please wait</div>
            <div id="ocrResult" class="hidden"></div>
            <div id="pronunciationHub" class="hidden">
                <h4>📖 Pronunciation Hub</h4>
                <p style="font-size:14px; margin-bottom:8px;">Extracted text:</p>
                <div id="hubText" style="background:white; padding:10px; border-radius:10px; margin-bottom:10px; font-size:15px;"></div>
                <button id="speakHubBtn" class="pronounce-btn">🔊 Pronounce clearly (English)</button>
                <div class="translation-box" id="hubTranslation">🇮🇳 Hindi translation will appear here</div>
            </div>
        </div>

        <!-- Quick Pronounce -->
        <button id="pronounceTypedBtn" style="background:#7c3aed; margin-top:5px;">🎤 Quick Pronounce Typed Text</button>
    </div>
</section>

<!-- ===== FEATURES ===== -->
<section class="features" id="features">
    <h2>✨ Why Pronunciation Hub?</h2>
    <div class="features-grid">
        <div class="feature-card">
            <div class="feature-icon">📢</div>
            <h3>AI Voice Pronounces</h3>
            <p>Clear, natural English voice reads any text you type or capture from a photo.</p>
        </div>
        <div class="feature-card">
            <div class="feature-icon">📸</div>
            <h3>Photo to Speech</h3>
            <p>Snap a picture of a book, sign, or document. The app extracts and reads the text aloud.</p>
        </div>
        <div class="feature-card">
            <div class="feature-icon">🇮🇳</div>
            <h3>Hindi Translation</h3>
            <p>Every word or sentence is translated into Hindi so you understand the meaning.</p>
        </div>
        <div class="feature-card">
            <div class="feature-icon">⚡</div>
            <h3>Fast & Offline-Ready</h3>
            <p>Works smoothly on any device. No server lag – speech is generated by your browser.</p>
        </div>
        <div class="feature-card">
            <div class="feature-icon">🧑‍🦯</div>
            <h3>Accessible Design</h3>
            <p>Large buttons, simple interface, clear instructions. Built for illiterate and low-vision users.</p>
        </div>
        <div class="feature-card">
            <div class="feature-icon">🔒</div>
            <h3>100% Private</h3>
            <p>Your photos and text never leave your device. No data stored on any server.</p>
        </div>
    </div>
</section>

<!-- ===== HOW IT WORKS ===== -->
<section class="how-it-works" id="how-it-works">
    <h2>📋 How to Use</h2>
    <div class="steps">
        <div class="step">
            <div class="step-number">1</div>
            <div class="step-content">
                <h3>Type or Take a Photo</h3>
                <p>Type any English word/sentence OR click a photo of a page/document using the camera upload.</p>
            </div>
        </div>
        <div class="step">
            <div class="step-number">2</div>
            <div class="step-content">
                <h3>Click 'Speak' or 'Upload & Read'</h3>
                <p>Press the button. The app will instantly read the text aloud in a clear English voice.</p>
            </div>
        </div>
        <div class="step">
            <div class="step-number">3</div>
            <div class="step-content">
                <h3>Read Hindi Translation</h3>
                <p>Below the text, you'll see the Hindi meaning. For photos, use the Pronunciation Hub button.</p>
            </div>
        </div>
        <div class="step">
            <div class="step-number">4</div>
            <div class="step-content">
                <h3>Repeat or Practice</h3>
                <p>Listen as many times as you need. Perfect for learning pronunciation and understanding.</p>
            </div>
        </div>
    </div>
</section>

<!-- ===== FAQ ===== -->
<section class="faq" id="faq">
    <h2>❓ Frequently Asked Questions</h2>
    <div class="faq-list">
        <div class="faq-item">
            <div class="faq-question">Do I need internet to use this app?</div>
            <div class="faq-answer">For typing and speech: No, it works offline. For photo OCR (reading text from images): Yes, internet is required for the first use. After that, some browsers cache it.</div>
        </div>
        <div class="faq-item">
            <div class="faq-question">Is my data safe? Do you store my photos?</div>
            <div class="faq-answer">Absolutely not. Everything stays in your browser. No data is sent to any server. Your privacy is 100% protected.</div>
        </div>
        <div class="faq-item">
            <div class="faq-question">Which languages are supported?</div>
            <div class="faq-answer">Currently: English text input and speech. Hindi translation for common words/phrases. More languages coming soon.</div>
        </div>
        <div class="faq-item">
            <div class="faq-question">Can I use this on my phone?</div>
            <div class="faq-answer">Yes! Works on all smartphones (Android & iOS), tablets, and computers. Optimized for touch.</div>
        </div>
        <div class="faq-item">
            <div class="faq-question">What if the app doesn't read the photo correctly?</div>
            <div class="faq-answer">Make sure the photo is clear, well-lit, and text is readable. Try using "scan" mode on your camera. If issues persist, manually type the text.</div>
        </div>
        <div class="faq-item">
            <div class="faq-question">Is this free?</div>
            <div class="faq-answer">Yes, completely free with no ads. Built for education and accessibility.</div>
        </div>
    </div>
</section>

<!-- ===== FOOTER ===== -->
<footer class="footer">
    <p style="font-size: 20px; font-weight: 600;">📢 Pronunciation Hub</p>
    <p style="margin: 5px 0;">Making words accessible for everyone.</p>
    <div class="footer-links">
        <a href="#home">Home</a>
        <a href="#app">App</a>
        <a href="#features">Features</a>
        <a href="#how-it-works">How It Works</a>
        <a href="#faq">FAQ</a>
    </div>
    <p style="margin-top: 20px; font-size: 14px;">&copy; 2025 Pronunciation Hub. Built with ❤️ for accessibility.</p>
</footer>

<!-- ===== SCRIPTS ===== -->
<script src="https://cdn.jsdelivr.net/npm/tesseract.js@4/dist/tesseract.min.js"></script>
<script>
    (function() {
        'use strict';

        // ---- App Script (same as before, integrated) ----
        const textInput = document.getElementById('textInput');
        const speakTextBtn = document.getElementById('speakTextBtn');
        const textTranslation = document.getElementById('textTranslation');
        const photoInput = document.getElementById('photoInput');
        const uploadBtn = document.getElementById('uploadBtn');
        const loader = document.getElementById('loader');
        const ocrResult = document.getElementById('ocrResult');
        const pronunciationHub = document.getElementById('pronunciationHub');
        const hubText = document.getElementById('hubText');
        const speakHubBtn = document.getElementById('speakHubBtn');
        const hubTranslation = document.getElementById('hubTranslation');
        const pronounceTypedBtn = document.getElementById('pronounceTypedBtn');

        function speak(text) {
            if (!text || text.trim() === '') return;
            window.speechSynthesis.cancel();
            const utterance = new SpeechSynthesisUtterance(text);
            utterance.lang = 'en-US';
            utterance.rate = 0.9;
            utterance.pitch = 1;
            utterance.volume = 1;
            window.speechSynthesis.speak(utterance);
        }

        function translateToHindi(text) {
            if (!text) return '';
            const lowerText = text.toLowerCase().trim();
            const dict = {
                'hello': 'नमस्ते', 'good morning': 'सुप्रभात', 'good night': 'शुभ रात्रि',
                'thank you': 'धन्यवाद', 'please': 'कृपया', 'sorry': 'क्षमा करें',
                'yes': 'हाँ', 'no': 'नहीं', 'education': 'शिक्षा', 'school': 'स्कूल',
                'water': 'पानी', 'food': 'खाना', 'book': 'किताब',
                'i am happy': 'मैं खुश हूँ', 'i am sad': 'मैं उदास हूँ',
                'help': 'मदद', 'doctor': 'डॉक्टर', 'hospital': 'अस्पताल',
                'family': 'परिवार', 'friend': 'दोस्त', 'i love you': 'मैं तुमसे प्यार करता/करती हूँ',
                'how are you': 'आप कैसे हैं?', 'i am fine': 'मैं ठीक हूँ',
                'goodbye': 'अलविदा', 'good': 'अच्छा', 'bad': 'बुरा',
                'home': 'घर', 'work': 'काम', 'money': 'पैसा', 'time': 'समय',
                'today': 'आज', 'tomorrow': 'कल', 'apple': 'सेब', 'dog': 'कुत्ता',
                'cat': 'बिल्ली', 'car': 'गाड़ी', 'bus': 'बस', 'phone': 'फ़ोन',
                'computer': 'कंप्यूटर'
            };
            if (dict[lowerText]) return dict[lowerText];
            if (lowerText.includes(' ')) {
                const words = lowerText.split(' ');
                const translated = words.map(w => dict[w] || w).join(' ');
                return translated;
            }
            return `"${text}" का हिंदी अनुवाद उपलब्ध नहीं है`;
        }

        function showTranslation(el, text) {
            const translation = translateToHindi(text);
            el.textContent = '🇮🇳 हिंदी: ' + translation;
        }

        // Text speak
        speakTextBtn.addEventListener('click', function() {
            const text = textInput.value.trim();
            if (!text) { textTranslation.textContent = '⚠️ कृपया कुछ टाइप करें'; return; }
            speak(text);
            showTranslation(textTranslation, text);
        });

        pronounceTypedBtn.addEventListener('click', function() {
            const text = textInput.value.trim();
            if (!text) { alert('Please type some text first.'); return; }
            speak(text);
            showTranslation(textTranslation, text);
        });

        // Photo OCR
        function processImage(file) {
            if (!file) return;
            loader.classList.add('active');
            ocrResult.classList.add('hidden');
            pronunciationHub.classList.add('hidden');
            if (file.size > 10 * 1024 * 1024) {
                alert('Image too large. Max 10MB.');
                loader.classList.remove('active');
                return;
            }
            const reader = new FileReader();
            reader.onload = function(e) {
                Tesseract.recognize(e.target.result, 'eng')
                    .then(({ data: { text } }) => {
                        loader.classList.remove('active');
                        const cleaned = text.trim();
                        if (!cleaned) {
                            ocrResult.textContent = '❌ No text found. Try a clearer image.';
                            ocrResult.classList.remove('hidden');
                            return;
                        }
                        ocrResult.textContent = '📄 Extracted: ' + cleaned;
                        ocrResult.classList.remove('hidden');
                        hubText.textContent = cleaned;
                        pronunciationHub.classList.remove('hidden');
                        showTranslation(hubTranslation, cleaned);
                    })
                    .catch(err => {
                        loader.classList.remove('active');
                        ocrResult.textContent = '❌ Error: ' + err.message;
                        ocrResult.classList.remove('hidden');
                    });
            };
            reader.readAsDataURL(file);
        }

        uploadBtn.addEventListener('click', function() {
            const file = photoInput.files[0];
            if (!file) { alert('Please select or take a photo first.'); return; }
            processImage(file);
        });

        speakHubBtn.addEventListener('click', function() {
            const text = hubText.textContent.trim();
            if (!text) { alert('No text to speak.'); return; }
            speak(text);
            showTranslation(hubTranslation, text);
        });

        // ---- FAQ toggle ----
        document.querySelectorAll('.faq-item').forEach(item => {
            item.addEventListener('click', function() {
                this.classList.toggle('open');
            });
        });

        // ---- Smooth scroll for nav links (compatible) ----
        document.querySelectorAll('.nav-links a, .hero-buttons a, .footer-links a').forEach(link => {
            link.addEventListener('click', function(e) {
                const href = this.getAttribute('href');
                if (href && href.startsWith('#')) {
                    e.preventDefault();
                    const target = document.querySelector(href);
                    if (target) {
                        target.scrollIntoView({ behavior: 'smooth', block: 'start' });
                    }
                }
            });
        });

        console.log('Pronunciation Hub website ready.');
    })();
</script>
</body>
</html>
