<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mendham Golf & Tennis - Hole 10 Enhancements</title>
    <style>
        /* --- Reset & Base Styles --- */
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body, html {
            height: 100%;
            width: 100%;
            overflow: hidden;
            background-color: #1a1a1a;
            color: white;
        }

        /* --- 1. Login & Intro Shared Styles --- */
        .full-screen-bg {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: 1000;
            display: flex;
            justify-content: center;
            align-items: center;
            background-size: cover;
            background-position: center;
        }

        /* Background specific classes */
        #landing-page { background-image: url('Approach_01_After.jpg'); }
        #intro-page-1 { background-image: url('Photo_01.jpg'); display: none; }
        #intro-page-2 { background-image: url('Photo_02.jpg'); display: none; }

        .full-screen-bg::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.4);
            z-index: 1;
        }

        .content-box {
            position: relative;
            z-index: 2;
            background: rgba(255, 255, 255, 0.95);
            padding: 40px;
            border-radius: 8px;
            box-shadow: 0 10px 25px rgba(0,0,0,0.5);
            text-align: center;
            max-width: 600px;
            width: 90%;
            color: #333;
        }

        .content-box h1 {
            color: #2c3e50;
            margin-bottom: 20px;
            font-size: 28px;
            border-bottom: 2px solid #27ae60;
            display: inline-block;
            padding-bottom: 10px;
        }

        .content-box p {
            line-height: 1.6;
            margin-bottom: 20px;
            font-size: 16px;
            color: #444;
        }

        /* Specific Login Styles */
        .input-group {
            margin-bottom: 20px;
            max-width: 300px;
            margin-left: auto;
            margin-right: auto;
        }

        input[type="password"] {
            width: 100%;
            padding: 12px;
            border: 1px solid #ddd;
            border-radius: 4px;
            font-size: 16px;
            margin-bottom: 10px;
        }

        button.action-btn {
            background-color: #27ae60;
            color: white;
            border: none;
            padding: 12px 30px;
            font-size: 16px;
            border-radius: 4px;
            cursor: pointer;
            transition: background 0.3s;
            min-width: 150px;
        }

        button.action-btn:hover {
            background-color: #219150;
        }

        .error-msg {
            color: #c0392b;
            font-size: 14px;
            margin-top: 10px;
            display: none;
        }

        /* --- Main Website Styles --- */
        #main-site {
            display: none; /* Hidden until continued */
            width: 100%;
            height: 100%;
            position: relative;
            background: #222;
        }

        .site-header {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            z-index: 100;
            padding: 20px;
            background: linear-gradient(to bottom, rgba(0,0,0,0.8), transparent);
            pointer-events: none;
        }
        
        .site-header h2 {
            color: white;
            text-shadow: 0 2px 4px rgba(0,0,0,0.8);
            pointer-events: auto;
        }

        .instruction-note {
            position: absolute;
            bottom: 20px;
            width: 100%;
            text-align: center;
            color: rgba(255, 255, 255, 0.9);
            font-size: 16px;
            pointer-events: none;
            z-index: 100;
            text-shadow: 0 1px 4px rgba(0,0,0,0.9);
            font-style: italic;
        }

        /* Comparison Slider Container */
        .comparison-container {
            position: relative;
            width: 100%;
            height: 100%;
            overflow: hidden;
            user-select: none;
        }

        .comparison-image {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            object-fit: contain;
            object-position: center;
            user-select: none;
            pointer-events: none;
        }

        .img-after { z-index: 1; }

        .img-before-container {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: 2;
            overflow: hidden;
            width: 50%;
            border-right: 3px solid white;
            box-shadow: 5px 0 15px rgba(0,0,0,0.3);
            pointer-events: none;
        }

        .img-before {
            position: absolute;
            top: 0;
            left: 0;
            height: 100%;
            object-fit: contain;
            object-position: center;
            user-select: none;
        }

        .slider-handle {
            position: absolute;
            top: 50%;
            right: -20px;
            width: 40px;
            height: 40px;
            background: white;
            border-radius: 50%;
            z-index: 3;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: ew-resize;
            box-shadow: 0 2px 5px rgba(0,0,0,0.4);
            color: #333;
            font-weight: bold;
            transform: translateY(-50%);
            pointer-events: auto;
        }

        .slider-label {
            position: absolute;
            top: 50%;
            transform: translateY(-50%);
            background: rgba(0,0,0,0.7);
            color: white;
            padding: 5px 10px;
            border-radius: 4px;
            font-size: 14px;
            pointer-events: none;
        }
        .label-before { left: 20px; z-index: 10; }
        .label-after { right: 20px; z-index: 10; }

        /* --- Hotspots --- */
        .hotspot-layer {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: 50;
            pointer-events: none;
        }

        .hotspot {
            position: absolute;
            width: 36px;
            height: 36px;
            background-color: rgba(231, 76, 60, 0.9);
            border: 2px solid white;
            border-radius: 50%;
            color: white;
            font-weight: bold;
            font-size: 16px;
            display: flex;
            justify-content: center;
            align-items: center;
            cursor: pointer;
            pointer-events: auto;
            transition: transform 0.2s, background-color 0.2s;
            box-shadow: 0 4px 10px rgba(0,0,0,0.5);
        }

        .hotspot:hover {
            transform: scale(1.2);
            background-color: #c0392b;
            z-index: 100;
        }

        /* --- Tooltip / Preview Image --- */
        .hotspot .preview-box {
            display: none;
            position: absolute;
            bottom: 45px;
            left: 50%;
            transform: translateX(-50%);
            width: 250px;
            background: white;
            padding: 8px;
            border-radius: 8px;
            box-shadow: 0 10px 25px rgba(0,0,0,0.5);
            text-align: center;
            z-index: 101;
            pointer-events: none; 
        }

        .hotspot:hover .preview-box {
            display: block;
            animation: fadeIn 0.3s ease;
        }

        .preview-box img {
            width: 100%;
            height: 140px; 
            object-fit: cover;
            border-radius: 4px;
            display: block;
            margin-bottom: 5px;
        }

        .preview-box p {
            color: #333;
            font-size: 14px;
            font-weight: normal;
            margin: 0;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateX(-50%) translateY(10px); }
            to { opacity: 1; transform: translateX(-50%) translateY(0); }
        }

        /* --- Detailed View Overlay --- */
        #detail-view {
            display: none;
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: #1a1a1a;
            z-index: 2000;
            overflow: hidden;
        }

        .detail-content {
            display: flex;
            height: 100%;
            width: 100%;
        }

        .detail-text-panel {
            width: 40%;
            background: #2c3e50;
            padding: 60px 40px;
            display: flex;
            flex-direction: column;
            justify-content: center;
            box-shadow: 5px 0 15px rgba(0,0,0,0.3);
            z-index: 2;
            position: relative;
        }

        .detail-image-panel {
            width: 60%;
            position: relative;
            background: #000;
        }

        .detail-image-panel img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            display: block;
        }

        .detail-title {
            font-size: 48px;
            color: #27ae60;
            margin-bottom: 20px;
            font-weight: bold;
        }

        .detail-description {
            font-size: 20px;
            line-height: 1.6;
            color: #ecf0f1;
            margin-bottom: 40px;
        }

        .back-btn {
            align-self: flex-start;
            background: transparent;
            color: white;
            border: 2px solid white;
            padding: 10px 30px;
            font-size: 16px;
            border-radius: 30px;
            cursor: pointer;
            transition: all 0.3s ease;
            text-transform: uppercase;
            letter-spacing: 1px;
            margin-top: auto;
        }

        .back-btn:hover {
            background: white;
            color: #2c3e50;
        }

        /* Hotspot Positions */
        .hs-f { top: 23%; left: 24%; }
        .hs-e { top: 38%; left: 20%; }
        .hs-a { top: 60%; left: 50%; }
        .hs-d { top: 58%; left: 42%; }
        .hs-c { top: 38%; left: 40%; }
        .hs-b { top: 41%; left: 53%; }

        /* Mobile Responsive */
        @media (max-width: 900px) {
            .detail-content { flex-direction: column-reverse; }
            .detail-text-panel { width: 100%; height: 50%; padding: 20px; }
            .detail-image-panel { width: 100%; height: 50%; }
            .detail-title { font-size: 32px; }
            .detail-description { font-size: 16px; margin-bottom: 20px; }
            .hotspot .preview-box { display: none !important; }
            .content-box h1 { font-size: 24px; }
        }

    </style>
</head>
<body>

    <!-- 1. LANDING PAGE (LOGIN) -->
    <div id="landing-page" class="full-screen-bg">
        <div class="content-box">
            <div style="margin-bottom: 20px;">
                <h1>Mendham Golf & Tennis</h1>
                <p style="color: #666;">Hole 10 Improvement Plan</p>
            </div>
            
            <div class="input-group">
                <input type="password" id="passwordInput" placeholder="Enter Password">
                <p class="error-msg" id="errorMsg">Incorrect password. Please try again.</p>
            </div>
            <button class="action-btn" onclick="checkLogin()">Login</button>
        </div>
    </div>

    <!-- 2. INTRODUCTION PAGE 1 -->
    <div id="intro-page-1" class="full-screen-bg">
        <div class="content-box">
            <h1>The 2021 Master Plan</h1>
            <p>
                In 2021 the Mendham Golf & Tennis Club approved a master plan, presented by Robert McNeil, ASGCA, of the Northeast Golf Company. 
                Robert McNeil, alongside contractors at NMP Golf, have now completed nearly all of the proposed improvements to the course.
            </p>
            <button class="action-btn" onclick="nextIntro()">Continue</button>
        </div>
    </div>

    <!-- 3. INTRODUCTION PAGE 2 -->
    <div id="intro-page-2" class="full-screen-bg">
        <div class="content-box">
            <h1>Hole 10 Improvements</h1>
            <p>
                One of the major projects that has yet to be completed is the work on the 10th hole, improving the par 5's aesthetics, strategy, agronomy, and playability. 
                This interactive guide explains the proposed enhancements to the 10th hole, along with the planning and goals that have guided these proposals.
            </p>
            <button class="action-btn" onclick="startExperience()">Continue</button>
        </div>
    </div>

    <!-- 4. MAIN WEBSITE (SLIDER) -->
    <div id="main-site">
        <div class="site-header">
            <h2>Hole 10 Proposed Enhancements</h2>
        </div>

        <div class="comparison-container" id="comparisonContainer">
            <!-- Images -->
            <img src="Aerial_PR.png" class="comparison-image img-after" alt="Proposed Design" draggable="false">
            <div class="slider-label label-after">PROPOSED</div>

            <div class="img-before-container" id="beforeContainer">
                <img src="Aerial_EX.png" class="img-before" id="imgBefore" alt="Existing Conditions" draggable="false">
                <div class="slider-handle"><span>&#8644;</span></div>
            </div>
            <div class="slider-label label-before">EXISTING</div>

            <!-- INSTRUCTION NOTE -->
            <div class="instruction-note">Click on each note for a more detailed view</div>

            <!-- HOTSPOTS -->
            <div class="hotspot-layer">
                <div class="hotspot hs-a" onclick="openDetail('A')">
                    A
                    <div class="preview-box">
                        <img src="PR_Image02.jpg" alt="Preview">
                        <p>Fairway Bunkers</p>
                    </div>
                </div>
                <div class="hotspot hs-b" onclick="openDetail('B')">
                    B
                    <div class="preview-box">
                        <img src="PR_Image01.jpg" alt="Preview">
                        <p>Tree Removal</p>
                    </div>
                </div>
                <div class="hotspot hs-c" onclick="openDetail('C')">
                    C
                    <div class="preview-box">
                        <img src="PR_Image03.jpg" alt="Preview">
                        <p>Large Bunker</p>
                    </div>
                </div>
                <div class="hotspot hs-d" onclick="openDetail('D')">
                    D
                    <div class="preview-box">
                        <img src="Approach_01_After.jpg" alt="Preview">
                        <p>Fairway Expansion</p>
                    </div>
                </div>
                <div class="hotspot hs-e" onclick="openDetail('E')">
                    E
                    <div class="preview-box">
                        <img src="PR_Image04.jpg" alt="Preview">
                        <p>Green Surrounds</p>
                    </div>
                </div>
                <div class="hotspot hs-f" onclick="openDetail('F')">
                    F
                    <div class="preview-box">
                        <img src="PR_Image05.jpg" alt="Preview">
                        <p>Tee Connection</p>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- 5. DETAIL VIEW OVERLAY -->
    <div id="detail-view">
        <div class="detail-content">
            <div class="detail-text-panel">
                <h1 id="detailTitle" class="detail-title">Feature A</h1>
                <p id="detailDesc" class="detail-description">Description text goes here...</p>
                <button class="back-btn" onclick="closeDetail()">Back to Map</button>
            </div>
            <div class="detail-image-panel">
                <img id="detailImage" src="" alt="Detail View">
            </div>
        </div>
    </div>

    <script>
        // --- DATA FOR HOTSPOTS ---
        const hotspotData = {
            'A': {
                title: "A. Fairway Bunkers",
                desc: "Reconstructing and reshaping the three fairway bunkers 75-150 yards from the green.",
                img: "PR_Image02.jpg"
            },
            'B': {
                title: "B. Tree Removal",
                desc: "The removal of approximately 10 trees to improve turf health. The removal of these trees will incidentally allow for new, strategic lines of play and improved views into the 10th green.",
                img: "PR_Image01.jpg"
            },
            'C': {
                title: "C. Large Bunker",
                desc: "The addition of a new, large bunker, spanning nearly 40 yards, beginning nearly 30 yards short of the green.",
                img: "PR_Image03.jpg"
            },
            'D': {
                title: "D. Fairway Expansion",
                desc: "Fairway expansions to allow more angles of play from the left side of the hole, as well as an access fairway to the right of the new, large bunker to allow heroic run-on shots from the right.",
                img: "Approach_01_After.jpg"
            },
            'E': {
                title: "E. Green Surrounds",
                desc: "Reshaping green surrounds, eliminating the back left greenside bunker, and reshaping and slightly repositioning the remaining greenside bunkers in congruence with the new angles of play from the fairway.",
                img: "PR_Image04.jpg"
            },
            'F': {
                title: "F. Tee Connection",
                desc: "Tying the existing 11th tee to 10th green with continuous short grass, doubling as a pitch area for shots that miss the green.",
                img: "PR_Image05.jpg"
            }
        };

        // --- NAVIGATION LOGIC ---
        function checkLogin() {
            const pass = document.getElementById('passwordInput').value;
            const error = document.getElementById('errorMsg');
            const landing = document.getElementById('landing-page');
            const intro1 = document.getElementById('intro-page-1');

            if (pass === "password") {
                // Fade out login, fade in intro 1
                landing.style.opacity = '0';
                landing.style.transition = 'opacity 0.5s ease';
                setTimeout(() => {
                    landing.style.display = 'none';
                    intro1.style.display = 'flex'; // Use flex to center content
                    // Trigger fade in for intro
                    intro1.style.opacity = '0';
                    setTimeout(() => {
                        intro1.style.transition = 'opacity 0.5s ease';
                        intro1.style.opacity = '1';
                    }, 50);
                }, 500);
            } else {
                error.style.display = 'block';
                const container = document.querySelector('.content-box');
                container.style.transform = 'translateX(10px)';
                setTimeout(() => container.style.transform = 'translateX(-10px)', 100);
                setTimeout(() => container.style.transform = 'translateX(0)', 200);
            }
        }

        function nextIntro() {
            const intro1 = document.getElementById('intro-page-1');
            const intro2 = document.getElementById('intro-page-2');

            intro1.style.opacity = '0';
            intro1.style.transition = 'opacity 0.5s ease';
            
            setTimeout(() => {
                intro1.style.display = 'none';
                intro2.style.display = 'flex';
                intro2.style.opacity = '0';
                setTimeout(() => {
                    intro2.style.transition = 'opacity 0.5s ease';
                    intro2.style.opacity = '1';
                }, 50);
            }, 500);
        }

        function startExperience() {
            const intro2 = document.getElementById('intro-page-2');
            const main = document.getElementById('main-site');

            intro2.style.opacity = '0';
            intro2.style.transition = 'opacity 0.5s ease';
            
            setTimeout(() => {
                intro2.style.display = 'none';
                main.style.display = 'block';
                // Trigger resize for slider logic
                updateImageWidth();
                const containerWidth = document.getElementById('comparisonContainer').offsetWidth;
                slide(containerWidth / 2);
            }, 500);
        }

        document.getElementById('passwordInput').addEventListener('keypress', function (e) {
            if (e.key === 'Enter') checkLogin();
        });

        // --- DETAIL VIEW LOGIC ---
        function openDetail(id) {
            const data = hotspotData[id];
            if(!data) return;

            document.getElementById('detailTitle').innerText = data.title;
            document.getElementById('detailDesc').innerText = data.desc;
            document.getElementById('detailImage').src = data.img;

            const detailView = document.getElementById('detail-view');
            detailView.style.display = 'block';
            detailView.style.opacity = '0';
            
            setTimeout(() => {
                detailView.style.transition = 'opacity 0.3s ease';
                detailView.style.opacity = '1';
            }, 10);
        }

        function closeDetail() {
            const detailView = document.getElementById('detail-view');
            detailView.style.opacity = '0';
            setTimeout(() => {
                detailView.style.display = 'none';
            }, 300);
        }

        // --- SLIDER LOGIC ---
        const container = document.getElementById('comparisonContainer');
        const beforeContainer = document.getElementById('beforeContainer');
        const imgBefore = document.getElementById('imgBefore');
        let active = false;

        function updateImageWidth() {
            if(container) {
                const w = container.offsetWidth;
                imgBefore.style.width = w + "px";
            }
        }
        window.addEventListener('resize', updateImageWidth);

        container.addEventListener('mousedown', () => active = true);
        window.addEventListener('mouseup', () => active = false);
        window.addEventListener('mousemove', (e) => { if (active) slide(e.pageX); });

        container.addEventListener('touchstart', () => active = true);
        window.addEventListener('touchend', () => active = false);
        window.addEventListener('touchmove', (e) => { if (active) slide(e.touches[0].pageX); });

        function slide(x) {
            let transformX = x - container.getBoundingClientRect().left;
            let width = container.offsetWidth;
            if (transformX < 0) transformX = 0;
            if (transformX > width) transformX = width;
            beforeContainer.style.width = transformX + "px";
        }
    </script>
</body>
</html>
