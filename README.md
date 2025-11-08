# Toolivox
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Word Counter — Fast & Unlimited</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
            background: linear-gradient(135deg, #2563eb 0%, #1e40af 100%);
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            color: #1f2937;
            overflow-x: hidden;
        }

        /* Header */
        .header {
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(10px);
            padding: 1.5rem 0;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
            position: relative;
            z-index: 10;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 1.5rem;
        }

        .nav {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .logo {
            font-size: 1.75rem;
            font-weight: 700;
            color: white;
            text-decoration: none;
            display: flex;
            align-items: center;
            gap: 0.5rem;
        }

        .features {
            display: flex;
            gap: 2rem;
            color: white;
            font-size: 0.875rem;
        }

        .feature-badge {
            display: flex;
            align-items: center;
            gap: 0.5rem;
        }

        /* Main Content */
        .main {
            flex: 1;
            display: flex;
            align-items: flex-start;
            padding: 2rem 0;
            position: relative;
        }

        .hero-section {
            text-align: center;
            color: white;
            margin-bottom: 2rem;
        }

        .hero-title {
            font-size: 2.5rem;
            font-weight: 700;
            margin-bottom: 1rem;
            text-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
        }

        .hero-subtitle {
            font-size: 1.125rem;
            opacity: 0.95;
            margin-bottom: 1rem;
        }

        .badges {
            display: flex;
            justify-content: center;
            gap: 1.5rem;
            flex-wrap: wrap;
            margin-bottom: 2rem;
        }

        .badge {
            background: rgba(255, 255, 255, 0.2);
            backdrop-filter: blur(10px);
            padding: 0.5rem 1rem;
            border-radius: 9999px;
            font-size: 0.875rem;
            display: flex;
            align-items: center;
            gap: 0.5rem;
        }

        /* Counter Card */
        .counter-card {
            background: white;
            border-radius: 1rem;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.15);
            overflow: hidden;
            width: 100%;
            max-width: 800px;
            margin: 0 auto;
        }

        .input-section {
            padding: 2rem;
            border-bottom: 1px solid #f3f4f6;
        }

        .input-header {
            font-size: 1.25rem;
            font-weight: 600;
            color: #1f2937;
            margin-bottom: 1rem;
            display: flex;
            align-items: center;
            gap: 0.5rem;
        }

        #textInput {
            width: 100%;
            min-height: 120px;
            padding: 1.5rem;
            border: 2px solid #e5e7eb;
            border-radius: 0.75rem;
            font-size: 1rem;
            line-height: 1.6;
            resize: vertical;
            transition: all 0.3s ease;
            font-family: inherit;
        }

        #textInput:focus {
            outline: none;
            border-color: #3b82f6;
            box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.1);
        }

        .toolbar {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 1rem 2rem;
            background: #f9fafb;
            border-top: 1px solid #e5e7eb;
        }

        .btn {
            padding: 0.625rem 1.25rem;
            border-radius: 0.5rem;
            font-size: 0.875rem;
            font-weight: 500;
            cursor: pointer;
            transition: all 0.3s ease;
            border: none;
            display: inline-flex;
            align-items: center;
            gap: 0.5rem;
        }

        .btn-primary {
            background: linear-gradient(135deg, #3b82f6 0%, #2563eb 100%);
            color: white;
        }

        .btn-primary:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 20px rgba(59, 130, 246, 0.3);
        }

        .btn-secondary {
            background: white;
            color: #6b7280;
            border: 1px solid #e5e7eb;
        }

        .btn-secondary:hover {
            background: #f9fafb;
        }

        /* Additional Stats (kept — deeper insights) */
        .additional-stats {
            background: white;
            border-radius: 1rem;
            padding: 2rem;
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 1.5rem;
            box-shadow: 0 10px 40px rgba(0, 0, 0, 0.1);
            max-width: 800px;
            margin: 2rem auto 0;
        }

        .stat-item {
            padding: 1rem;
            background: #f9fafb;
            border-radius: 0.75rem;
            border-left: 4px solid #3b82f6;
        }

        .stat-item-value {
            font-size: 1.5rem;
            font-weight: 600;
            color: #1f2937;
            margin-bottom: 0.25rem;
        }

        .stat-item-label {
            font-size: 0.875rem;
            color: #6b7280;
        }

        /* Floating Stats Panel — Only ONE stats display */
        #floatingStats {
            position: fixed;
            top: 20px;
            right: 20px;
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(12px);
            border-radius: 1rem;
            padding: 1.25rem;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.15);
            z-index: 100;
            min-width: 240px;
            border: 1px solid rgba(229, 231, 235, 0.6);
        }

        .floating-stat {
            display: flex;
            justify-content: space-between;
            padding: 0.5rem 0;
            border-bottom: 1px solid #f3f4f6;
        }

        .floating-stat:last-child {
            border-bottom: none;
        }

        .floating-label {
            font-size: 0.875rem;
            color: #6b7280;
        }

        .floating-value {
            font-weight: 700;
            color: #1e40af;
            font-size: 1.125rem;
        }

        .floating-title {
            font-size: 0.875rem;
            font-weight: 700;
            text-transform: uppercase;
            letter-spacing: 1px;
            color: #3b82f6;
            margin-bottom: 0.75rem;
            display: flex;
            align-items: center;
            gap: 0.5rem;
        }

        /* Hide floating panel on mobile/tablet */
        @media (max-width: 900px) {
            #floatingStats {
                display: none;
            }
        }

        /* Mobile adjustments */
        @media (max-width: 768px) {
            .features { display: none; }
            .hero-title { font-size: 2rem; }
            .toolbar { flex-direction: column; gap: 1rem; }
            .main { padding: 1rem 0; }
        }

        .icon {
            width: 20px;
            height: 20px;
            display: inline-block;
            vertical-align: middle;
            fill: currentColor;
        }

        .mobile-hint {
            text-align: center;
            margin-top: 1.5rem;
            color: rgba(255, 255, 255, 0.8);
            font-size: 0.875rem;
            max-width: 600px;
            margin-left: auto;
            margin-right: auto;
        }
    </style>
</head>
<body>
    <!-- Header -->
    <header class="header">
        <div class="container">
            <nav class="nav">
                <a href="#" class="logo">
                    <svg class="icon" style="width: 32px; height: 32px;" viewBox="0 0 24 24">
                        <path d="M19,5H5A2,2 0 0,0 3,7V17A2,2 0 0,0 5,19H19A2,2 0 0,0 21,17V7A2,2 0 0,0 19,5M19,17H5V7H19V17M16.5,15H14.5V12.5H16.5V15M12,15H10V9H12V15M7.5,15H5.5V10.5H7.5V15Z" fill="white"/>
                    </svg>
                    WordCounter
                </a>
                <div class="features">
                    <div class="feature-badge">
                        <svg class="icon" viewBox="0 0 20 20"><path d="M10 12a2 2 0 100-4 2 2 0 000 4z"/><path fill-rule="evenodd" d="M.458 10C1.732 5.943 5.522 3 10 3s8.268 2.943 9.542 7c-1.274 4.057-5.064 7-9.542 7S1.732 14.057.458 10zM14 10a4 4 0 11-8 0 4 4 0 018 0z"/></svg>
                        No Login
                    </div>
                    <div class="feature-badge">
                        <svg class="icon" viewBox="0 0 20 20"><path fill-rule="evenodd" d="M11.3 1.046A1 1 0 0112 2v5h4a1 1 0 01.82 1.573l-7 10A1 1 0 018 18v-5H4a1 1 0 01-.82-1.573l7-10a1 1 0 011.12-.38z"/></svg>
                        Fast
                    </div>
                    <div class="feature-badge">
                        <svg class="icon" viewBox="0 0 20 20"><path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zM4.332 8.027a6.012 6.012 0 011.912-2.706C6.512 5.73 6.974 6 7.5 6A1.5 1.5 0 019 7.5V8a2 2 0 004 0 2 2 0 011.523-1.943A5.977 5.977 0 0116 10c0 .34-.028.675-.083 1.002c-.27.194-.432.487-.432.998a.75.75 0 01-.75.75h-1.508a.75.75 0 01-.745-.75v-.11.002a.75.75 0 01-.75-.75 2.25 2.25 0 00-2.25-2.25H8.75a.75.75 0 01-.75-.75V7.5a.75.75 0 00-.75-.75A.75.75 0 006.5 6a.75.75 0 00-.745.73 5.98 5.98 0 00-1.423 1.297z"/></svg>
                        Unlimited
                    </div>
                </div>
            </nav>
        </div>
    </header>

    <!-- ✅ ONLY ONE STATS DISPLAY: Floating Panel -->
    <div id="floatingStats">
        <div class="floating-title">
            <svg class="icon" viewBox="0 0 20 20"><path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm1-12a1 1 0 10-2 0v4a1 1 0 00.293.707l2.828 2.829a1 1 0 101.415-1.415L11 9.586V6z"/></svg>
            Live Stats
        </div>
        <div class="floating-stat">
            <span class="floating-label">Words</span>
            <span class="floating-value" id="floatingWordCount">0</span>
        </div>
        <div class="floating-stat">
            <span class="floating-label">Characters</span>
            <span class="floating-value" id="floatingCharCount">0</span>
        </div>
        <div class="floating-stat">
            <span class="floating-label">Reading Time</span>
            <span class="floating-value" id="floatingReadingTime">0 min</span>
        </div>
    </div>

    <!-- Main Content -->
    <main class="main">
        <div class="container">
            <div class="hero-section">
                <h1 class="hero-title">Free Online Word Counter</h1>
                <p class="hero-subtitle">Real-time stats in the floating panel (desktop)</p>
                <div class="badges">
                    <div class="badge">✨ 100% Free</div>
                    <div class="badge">🔒 No Sign Up</div>
                    <div class="badge">⚡ Real-time</div>
                    <div class="badge">♾️ Unlimited</div>
                </div>
            </div>

            <div class="counter-card">
                <div class="input-section">
                    <h2 class="input-header">
                        <svg class="icon" viewBox="0 0 20 20"><path fill-rule="evenodd" d="M3 4a1 1 0 011-1h12a1 1 0 011 1v2a1 1 0 01-1 1H4a1 1 0 01-1-1V4zm0 4a1 1 0 011-1h6a1 1 0 110 2H4a1 1 0 01-1-1zm0 4a1 1 0 011-1h6a1 1 0 110 2H4a1 1 0 01-1-1zm10 2a1 1 0 11-2 0 1 1 0 012 0z"/></svg>
                        Type or paste your text below
                    </h2>
                    <textarea 
                        id="textInput" 
                        placeholder="Start typing or paste your text here... Your live stats (words, chars, reading time) will appear in the top-right panel on desktop."
                        autocomplete="off"
                        spellcheck="true"
                    ></textarea>
                </div>

                <div class="toolbar">
                    <div>
                        <button class="btn btn-secondary" onclick="copyText(this)">
                            <svg class="icon" viewBox="0 0 20 20"><path d="M8 3a1 1 0 011-1h2a1 1 0 110 2H9a1 1 0 01-1-1z"/><path d="M6 3a2 2 0 00-2 2v11a2 2 0 002 2h8a2 2 0 002-2V5a2 2 0 00-2-2 3 3 0 01-3 3H9a3 3 0 01-3-3z"/></svg>
                            Copy Text
                        </button>
                        <button class="btn btn-secondary" onclick="clearText()">
                            <svg class="icon" viewBox="0 0 20 20"><path fill-rule="evenodd" d="M9 2a1 1 0 00-.894.553L7.382 4H4a1 1 0 000 2v10a2 2 0 002 2h8a2 2 0 002-2V6a1 1 0 100-2h-3.382l-.724-1.447A1 1 0 0011 2H9zM7 8a1 1 0 012 0v6a1 1 0 11-2 0V8zm5-1a1 1 0 00-1 1v6a1 1 0 102 0V8a1 1 0 00-1-1z"/></svg>
                            Clear
                        </button>
                    </div>
                    <button class="btn btn-primary" onclick="downloadText()">
                        <svg class="icon" viewBox="0 0 20 20"><path fill-rule="evenodd" d="M3 17a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1zm3.293-7.707a1 1 0 011.414 0L9 10.586V3a1 1 0 112 0v7.586l1.293-1.293a1 1 0 111.414 1.414l-3 3a1 1 0 01-1.414 0l-3-3a1 1 0 010-1.414z"/></svg>
                        Download Text
                    </button>
                </div>
            </div>

            <!-- Advanced stats (optional but useful) -->
            <div class="additional-stats">
                <div class="stat-item">
                    <div class="stat-item-value" id="avgWordLength">0</div>
                    <div class="stat-item-label">Avg. Word Length</div>
                </div>
                <div class="stat-item">
                    <div class="stat-item-value" id="longestWord">—</div>
                    <div class="stat-item-label">Longest Word</div>
                </div>
                <div class="stat-item">
                    <div class="stat-item-value" id="speakingTime">0 min</div>
                    <div class="stat-item-label">Speaking Time</div>
                </div>
                <div class="stat-item">
                    <div class="stat-item-value" id="uniqueWords">0</div>
                    <div class="stat-item-label">Unique Words</div>
                </div>
            </div>

            <div class="mobile-hint">
                💡 <em>Real-time word, character, and reading time stats appear in the top-right floating panel on desktop. On mobile, use the advanced stats below.</em>
            </div>
        </div>
    </main>

    <script>
        const textInput = document.getElementById('textInput');
        const avgWordLength = document.getElementById('avgWordLength');
        const longestWord = document.getElementById('longestWord');
        const speakingTime = document.getElementById('speakingTime');
        const uniqueWords = document.getElementById('uniqueWords');
        
        // Floating stats
        const floatingWordCount = document.getElementById('floatingWordCount');
        const floatingCharCount = document.getElementById('floatingCharCount');
        const floatingReadingTime = document.getElementById('floatingReadingTime');

        function updateCounts() {
            const text = textInput.value;
            
            // Words
            const words = text.trim() ? text.trim().split(/\s+/).filter(w => w.length > 0) : [];
            const wordsCount = words.length;
            const formattedWords = wordsCount.toLocaleString();
            if (floatingWordCount) floatingWordCount.textContent = formattedWords;
            
            // Characters
            const chars = text.length;
            const formattedChars = chars.toLocaleString();
            if (floatingCharCount) floatingCharCount.textContent = formattedChars;
            
            // Reading time (200 wpm)
            const readingMinutes = wordsCount < 1 ? 0 : Math.ceil(wordsCount / 200);
            const readingTimeText = readingMinutes === 0 ? '<1 min' : `${readingMinutes} min`;
            if (floatingReadingTime) floatingReadingTime.textContent = readingTimeText;
            
            // Speaking time (150 wpm)
            const speakingMinutes = wordsCount < 1 ? 0 : Math.ceil(wordsCount / 150);
            speakingTime.textContent = speakingMinutes === 0 ? '<1 min' : `${speakingMinutes} min`;
            
            // Advanced stats
            if (words.length > 0) {
                // Clean words (remove punctuation for analysis)
                const cleanWords = words.map(w => w.replace(/[^\w]/g, '').toLowerCase()).filter(w => w);
                const totalLength = cleanWords.reduce((sum, word) => sum + word.length, 0);
                const avgLength = cleanWords.length ? (totalLength / cleanWords.length).toFixed(1) : 0;
                avgWordLength.textContent = avgLength;
                
                const longest = cleanWords.reduce((a, b) => b.length > a.length ? b : a, '');
                longestWord.textContent = longest.length > 20 ? longest.substring(0, 17) + '...' : longest || '—';
                
                const uniqueWordsSet = new Set(cleanWords);
                uniqueWords.textContent = uniqueWordsSet.size.toLocaleString();
            } else {
                avgWordLength.textContent = '0';
                longestWord.textContent = '—';
                uniqueWords.textContent = '0';
            }
        }

        async function copyText(button) {
            const originalHTML = button.innerHTML;
            const successIcon = `<svg class="icon" viewBox="0 0 20 20" style="width:16px;height:16px"><path fill="currentColor" fill-rule="evenodd" d="M16.707 5.293a1 1 0 010 1.414l-8 8a1 1 0 01-1.414 0l-4-4a1 1 0 011.414-1.414L8 12.586l7.293-7.293a1 1 0 011.414 0z"/></svg>`;
            
            try {
                await navigator.clipboard.writeText(textInput.value);
                button.innerHTML = `${successIcon} Copied!`;
                button.disabled = true;
                setTimeout(() => {
                    button.innerHTML = originalHTML;
                    button.disabled = false;
                }, 2000);
            } catch (err) {
                // Fallback
                textInput.select();
                textInput.setSelectionRange(0, 99999);
                try {
                    if (document.execCommand && document.execCommand('copy')) {
                        button.innerHTML = `${successIcon} Copied!`;
                        button.disabled = true;
                        setTimeout(() => {
                            button.innerHTML = originalHTML;
                            button.disabled = false;
                        }, 2000);
                    } else {
                        button.innerHTML = `✗ Failed`;
                        setTimeout(() => button.innerHTML = originalHTML, 2000);
                    }
                } catch (e) {
                    button.innerHTML = `✗ Failed`;
                    setTimeout(() => button.innerHTML = originalHTML, 2000);
                }
            }
        }

        function clearText() {
            textInput.value = '';
            updateCounts();
            textInput.focus();
        }

        function downloadText() {
            const text = textInput.value;
            if (!text.trim()) return;
            const blob = new Blob([text], { type: 'text/plain' });
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = `wordcounter-${new Date().toISOString().slice(0,10)}.txt`;
            a.click();
            URL.revokeObjectURL(url);
        }

        function resizeTextarea() {
            textInput.style.height = 'auto';
            const newHeight = Math.min(Math.max(120, textInput.scrollHeight), 600);
            textInput.style.height = newHeight + 'px';
        }

        // Init
        textInput.addEventListener('input', () => {
            resizeTextarea();
            updateCounts();
        });

        window.addEventListener('load', () => {
            textInput.focus();
            updateCounts();
        });
    </script>
</body>
</html>
