<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <!-- Viewport meta tag is crucial for mobile scaling and preventing zoom -->
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>ABI 6TH FORM: THE GAME (Mobile)</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/tone/14.8.49/Tone.js"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Press+Start+2P&display=swap');
        :root {
            --bg-color: #101015;
            --ui-bg: #ffffff;
            --ui-border: #404040;
            --text-color: #000000;
            --accent: #f0db4f;
            --danger: #ff4444;
            --success: #44ff44;
        }
        body {
            background-color: #050505;
            color: var(--text-color);
            font-family: 'Press Start 2P', cursive;
            margin: 0;
            height: 100vh;
            width: 100vw;
            overflow: hidden;
            user-select: none;
            -webkit-user-select: none; 
            touch-action: none;
        }

        /* --- NEW LAYOUT STRUCTURE --- */
        #game-wrapper {
            display: flex;
            flex-direction: column;
            width: 100%;
            height: 100%;
        }

        /* Top Section: The Game Screen */
        #screen-area {
            flex: 1; /* Takes up remaining space */
            display: flex;
            justify-content: center;
            align-items: center;
            background: #111;
            padding: 10px;
            overflow: hidden;
            position: relative;
        }

        #game-container {
            position: relative;
            /* Maintain 4:3 Aspect Ratio */
            aspect-ratio: 4/3;
            /* Fit within the screen area, leaving room for controls */
            width: 100%;
            max-height: 100%;
            max-width: 100vh; /* Prevent it getting too wide on landscape */
            
            background-color: var(--bg-color);
            border: 4px solid #333;
            box-shadow: 0 0 20px rgba(0,0,0,0.5);
            outline: none;
        }

        canvas {
            display: block;
            width: 100%;
            height: 100%;
            image-rendering: pixelated;
        }

        /* Bottom Section: The Controller */
        #mobile-controls {
            height: 240px; /* Fixed height for controls */
            min-height: 35vh; /* Ensure it's tall enough on tall phones */
            background: #222;
            border-top: 4px solid #444;
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 0 30px;
            box-sizing: border-box;
            z-index: 1000;
        }

        /* Button Styling Update for "Physical" feel */
        .dpad {
            display: grid;
            grid-template-columns: 70px 70px 70px;
            grid-template-rows: 70px 70px;
            gap: 5px;
        }
        
        .dpad-btn {
            width: 70px;
            height: 70px;
            background: #444;
            border-bottom: 4px solid #222;
            border-radius: 8px;
            color: #aaa;
            font-size: 24px;
            display: flex;
            justify-content: center;
            align-items: center;
            user-select: none;
            box-shadow: 0 4px 0 #111;
        }
        .dpad-btn:active, .dpad-btn.active {
            background: #666;
            transform: translateY(4px);
            box-shadow: 0 0 0 #111;
            border-bottom: none;
        }

        /* Positioning D-Pad buttons in grid */
        #btn-up { grid-column: 2; grid-row: 1; }
        #btn-left { grid-column: 1; grid-row: 2; }
        #btn-down { grid-column: 2; grid-row: 2; }
        #btn-right { grid-column: 3; grid-row: 2; }

        /* Action Button Styling */
        .action-btn-container {
            display: flex;
            align-items: center;
            justify-content: center;
        }
        #btn-action {
            width: 90px;
            height: 90px;
            border-radius: 50%;
            background: #d82020; /* Red button */
            border: 4px solid #900;
            box-shadow: 0 6px 0 #500;
            color: white;
            font-size: 24px;
            font-family: 'Press Start 2P', cursive;
            display: flex;
            justify-content: center;
            align-items: center;
        }
        #btn-action:active, #btn-action.active {
            transform: translateY(6px);
            box-shadow: 0 0 0 #500;
        }


        /* --- INTRO SCREEN & UI --- */
        #intro-screen {
            position: absolute;
            top:0; left:0; width:100%; height:100%;
            background: #000;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            z-index: 100;
            text-align: center;
            color: white;
            overflow: hidden;
        }
        .glitch-title {
            font-size: 30px; /* Slightly smaller for mobile constraint */
            position: relative;
            color: #44ff44;
            text-shadow: 4px 4px #000;
            margin-bottom: 10px;
            animation: glitch 1s infinite;
        }
        /* ... (Existing Glitch CSS) ... */
        .glitch-title::before, .glitch-title::after {
            content: "ABI 6TH FORM";
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: #000;
        }
        .glitch-title::before {
            left: 2px;
            text-shadow: -2px 0 #ff00c1;
            clip: rect(44px, 450px, 56px, 0);
            animation: glitch-anim-1 5s infinite linear alternate-reverse;
        }
        .glitch-title::after {
            left: -2px;
            text-shadow: -2px 0 #00fff9;
            clip: rect(44px, 450px, 56px, 0);
            animation: glitch-anim-2 5s infinite linear alternate-reverse;
        }
        @keyframes glitch-anim-1 {
            0% { clip: rect(30px, 9999px, 10px, 0); }
            20% { clip: rect(80px, 9999px, 90px, 0); }
            40% { clip: rect(10px, 9999px, 50px, 0); }
            60% { clip: rect(40px, 9999px, 20px, 0); }
            80% { clip: rect(70px, 9999px, 90px, 0); }
            100% { clip: rect(20px, 9999px, 60px, 0); }
        }
        @keyframes glitch-anim-2 {
            0% { clip: rect(10px, 9999px, 30px, 0); }
            20% { clip: rect(50px, 9999px, 20px, 0); }
            40% { clip: rect(90px, 9999px, 70px, 0); }
            60% { clip: rect(20px, 9999px, 40px, 0); }
            80% { clip: rect(60px, 9999px, 10px, 0); }
            100% { clip: rect(80px, 9999px, 90px, 0); }
        }
        .subtitle {
            font-size: 10px;
            color: #ccc;
            margin-bottom: 20px;
            letter-spacing: 2px;
        }
        .mission-box {
            border: 2px solid #44ff44;
            padding: 10px;
            background: rgba(0, 50, 0, 0.8);
            margin-bottom: 20px;
            width: 80%;
        }
        .press-start {
            font-size: 14px;
            color: #f0db4f;
            animation: blinker 0.8s linear infinite;
            cursor: pointer;
        }
        @keyframes blinker { 50% { opacity: 0; } }
        
        #focus-overlay {
            position: absolute;
            top:0; left:0; width:100%; height:100%;
            background: rgba(0,0,0,0.9);
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 200;
            cursor: pointer;
            color: #4f4;
            flex-direction: column;
            text-align: center;
        }
        #dialogue-box {
            position: absolute;
            display: none;
            bottom: 10px;
            left: 10px;
            right: 10px;
            height: 100px;
            z-index: 10;
            padding: 10px;
            border: 4px double #000;
            background-color: #fff;
            border-radius: 4px;
            line-height: 1.6;
            font-size: 12px;
            color: black;
        }
        #dialogue-name {
            color: #d00;
            margin-bottom: 5px;
            text-transform: uppercase;
            font-size: 12px;
        }
        #room-name {
            position: absolute;
            top: 20px;
            left: 20px;
            color: white;
            background: rgba(0,0,0,0.5);
            padding: 5px 10px;
            border: 2px solid white;
            display: none; /* Shown via JS */
        }
        #scanlines {
            position: absolute;
            top: 0; left: 0; width: 100%; height: 100%;
            background: linear-gradient(to bottom, rgba(255,255,255,0), rgba(255,255,255,0) 50%, rgba(0,0,0,0.1) 50%, rgba(0,0,0,0.1));
            background-size: 100% 4px;
            pointer-events: none;
            z-index: 999;
            opacity: 0.3;
        }
        /* --- JBR GAMES LOGO --- */
        .logo-box {
            border: 4px solid #fff;
            padding: 15px 20px;
            background: #000;
            margin-bottom: 40px;
            box-shadow: 6px 6px 0px #444;
            display: flex;
            flex-direction: column;
            align-items: center;
            transform: scale(1.2);
        }
        .logo-jbr {
            font-size: 40px;
            color: #f0db4f;
            text-shadow: 4px 4px 0px #d82020;
            line-height: 1;
            font-weight: bold;
        }
        .logo-games {
            font-size: 12px;
            color: #44ff44;
            letter-spacing: 8px;
            margin-top: 5px;
            border-top: 2px solid #333;
            padding-top: 5px;
            width: 100%;
            text-align: center;
        }
    </style>
</head>
<body>
<div id="game-wrapper">
    <!-- TOP SECTION: THE SCREEN -->
    <div id="screen-area">
        <div id="game-container" tabindex="0">
            <canvas id="gameCanvas" width="800" height="600"></canvas>
            <div id="scanlines"></div>
            <div id="room-name">COMMON ROOM</div>
            
            <div id="focus-overlay" onclick="initAudio(); this.style.display='none'; document.getElementById('game-container').focus();">
                <div class="logo-box">
                    <div class="logo-jbr">JBR</div>
                    <div class="logo-games">GAMES</div>
                </div>
                <div class="blink" style="color:#f0db4f">Tap to Start</div>
            </div>
            <div id="intro-screen">
                <div class="glitch-title">ABI 6TH FORM</div>
                <div class="subtitle">THE GAME</div>
                
                <div class="mission-box">
                    <p style="color:#ff4444; margin-bottom:10px;">ALERT: BUG RELEASE</p>
                    <p style="font-size: 8px; line-height: 1.5;">
                        The Main Glitch has stolen the JCQ Exam and AI guidance.<br>
                        You need to recover it so you can spread good practice.<br><br>
                        CONTROLS:<br>
                        Use Buttons Below
                    </p>
                </div>
                <div class="press-start">TAP 'A' BUTTON</div>
            </div>
            <div id="dialogue-box">
                <div id="dialogue-name">System</div>
                <div id="dialogue-text">...</div>
                <div style="font-size: 10px; text-align: right; margin-top: 10px; opacity: 0.7;">[A]</div>
            </div>
        </div>
    </div>

    <!-- BOTTOM SECTION: THE CONTROLLER -->
    <div id="mobile-controls">
        <div class="control-group dpad">
            <div class="dpad-btn" id="btn-up">▲</div>
            <div class="dpad-btn" id="btn-left">◀</div>
            <div class="dpad-btn" id="btn-down">▼</div>
            <div class="dpad-btn" id="btn-right">▶</div>
        </div>
        <div class="control-group action-btn-container">
            <div id="btn-action">A</div>
        </div>
    </div>
</div>

<script>
const canvas = document.getElementById('gameCanvas');
const ctx = canvas.getContext('2d');
// --- PIXEL ART SPRITE SYSTEM ---
const PALETTE = {
    '.': null,
    'x': '#000000', 's': '#ffccaa', 'w': '#ffffff', 'r': '#d82020',
    'b': '#2040d8', 'g': '#44aa44', 'y': '#ffee00', 'h': '#663300',
    'c': '#888888', 'p': '#aa00aa', 'm': '#00aa00', 'd': '#222222',
    'D': '#664400', // Door Brown
    'T': '#8b4513', // Table Brown
    'C': '#666666', // Chair Grey
    'L': '#228b22', // Plant Green
    'O': '#ff9900'  // Orange (Alert or Chair Orange)
};
const SPRITE_DATA = {
    player: [
        "....xxxxxx......", "...xhhhhhhx.....", "..xhhhhhhhhx....", "..xhssxxsshx....",
        "..xhs.xx.shx....", "..xhsssssshx....", "....xxxxxx......", "...xppppppx.....",
        "..xppppppppx....", ".xppwwwwwwppx...", ".xppwwwwwwppx...", ".xppppppppppx...",
        "..xccccccccx....", "..xccccccccx....", "...xx....xx.....", "...xx....xx....."
    ],
    grant: [
        "....xxxxxx......", "...xhhhhhhx.....", "..xhhhhhhhhx....", "..xhssxxsshx....",
        "..xhsxwwxshx....", "..xhsssssshx....", "....xxxxxx......", "...xrrwwrrx.....",
        "..xrrwwwwrrx....", ".xrrwwwwwwrrx...", ".xrrwwwwwwrrx...", ".xrrrrrrrrrrx...",
        "..xccccccccx....", "..xccccccccx....", "...xx....xx.....", "...xx....xx....."
    ],
    brookes: [
        "....xxxxxx......", "...xbbbbbbx.....", "..xbbbbbbbbx....", "..xhssxxsshx....",
        "..xhs.xx.shx....", "..xhshhhshhx....", "....xxxxxx......", "...xggggggx.....",
        "..xggggggggx....", ".xggccccccggx...", ".xggccccccggx...", ".xggggggggggx...",
        "..xccccccccx....", "..xccccccccx....", "...xx....xx.....", "...xx....xx....."
    ],
    botwright: [
        "....xxxxxx......", "...xhhhhhhx.....", "..xhhhhhhhhx....", "..xhssxxsshx....",
        "..xhs.xx.shx....", "..xhsssssshx....", "....xxxxxx......", "...xccccccx.....",
        "..xccwwwwccx....", ".xccwwrrwwccx...", ".xccwwrrwwccx...", ".xccccccccccx...",
        "..xddddddddx....", "..xddddddddx....", "...xx....xx.....", "...xx....xx....."
    ],
    mcmahon: [
        "....xxxxxx......", "...xyyyyyyx.....", "..xyyyyyyyyx....", "..xyssxxssyx....",
        "..xys.xx.syx....", "..xyssssssyx....", "....xxxxxx......", "...xppppppx.....",
        "..xppppppppx....", ".xppwwwwwwppx...", ".xppwwwwwwppx...", ".xppppppppppx...",
        "..xccccccccx....", "..xccccccccx....", "...xx....xx.....", "...xx....xx....."
    ],
    oneill: [
        "....xxxxxx......", "...xhhhhhhx.....", "..xhhhhhhhhx....", "..xhssxxsshx....",
        "..xhs.xx.shx....", "..xhsssssshx....", "....xxxxxx......", "...xbbbbbbx.....",
        "..xbbbbbbbbx....", ".xbbwwwwwwbbx...", ".xbbwwyywwbbx...", ".xbbbbbbbbbbx...",
        "..xccccccccx....", "..xccccccccx....", "...xx....xx.....", "...xx....xx....."
    ],
    oneill_strict: [ // Strict Mrs O'Neill - red outfit
        "....xxxxxx......", "...xhhhhhhx.....", "..xhhhhhhhhx....", "..xhssxxsshx....",
        "..xhs.xx.shx....", "..xhsssssshx....", "....xxxxxx......", "...xrrrrrrx.....",
        "..xrrrrrrrrx....", ".xrrwwwwwwrrx...", ".xrrwwwwwwrrx...", ".xrrrrrrrrrrx...",
        "..xccccccccx....", "..xccccccccx....", "...xx....xx.....", "...xx....xx....."
    ],
    julie: [ // Apron
        "....xxxxxx......", "...xhhhhhhx.....", "..xhhhhhhhhx....", "..xhssxxsshx....",
        "..xhs.xx.shx....", "..xhsssssshx....", "....xxxxxx......", "...xwwwwwwx.....",
        "..xwwwwwwwwx....", ".xwwwwwwwwwwx...", ".xwwwwwwwwwwx...", ".xwwwwwwwwwwx...",
        "..xccccccccx....", "..xccccccccx....", "...xx....xx.....", "...xx....xx....."
    ],
    deacon: [ // Black suit, clerical collar
        "....xxxxxx......", "...xhhhhhhx.....", "..xhhhhhhhhx....", "..xhssxxsshx....",
        "..xhs.xx.shx....", "..xhsssssshx....", "....xxxxxx......", "...xddddddx.....",
        "..xddddddddx....", ".xddddwwddddx...", ".xddddwwddddx...", ".xddddddddddx...",
        "..xddddddddx....", "..xddddddddx....", "...xx....xx.....", "...xx....xx....."
    ],
    jones: [ // History Teacher (Mr Jones) - Tweed
        "....xxxxxx......", "...xhhhhhhx.....", "..xhhhhhhhhx....", "..xhssxxsshx....",
        "..xhs.xx.shx....", "..xhsssssshx....", "....xxxxxx......", "...xTTTTTTx.....",
        "..xTTTTTTTTx....", ".xTTTTTTTTTTx...", ".xTTwwwwwwTTx...", ".xTTTTTTTTTTx...",
        "..xccccccccx....", "..xccccccccx....", "...xx....xx.....", "...xx....xx....."
    ],
    russell: [ // Science Teacher (Miss Russell) - Lab Coat
        "....xxxxxx......", "...xhhhhhhx.....", "..xhhhhhhhhx....", "..xhssxxsshx....",
        "..xhs.xx.shx....", "..xhsssssshx....", "....xxxxxx......", "...xwwwwwwx.....",
        "..xwwwwwwwwx....", ".xwwwwwwwwwwx...", ".xwwbbwwbbwwx...", ".xwwwwwwwwwwx...",
        "..xccccccccx....", "..xccccccccx....", "...xx....xx.....", "...xx....xx....."
    ],
    mckeown: [ // English Teacher (Mrs McKeown) - Cardigan
        "....xxxxxx......", "...xhhhhhhx.....", "..xhhhhhhhhx....", "..xhssxxsshx....",
        "..xhsxwwxshx....", "..xhsssssshx....", "....xxxxxx......", "...xppppppx.....",
        "..xppppppppx....", ".xppwwwwwwppx...", ".xppwwwwwwppx...", ".xppppppppppx...",
        "..xccccccccx....", "..xccccccccx....", "...xx....xx.....", "...xx....xx....."
    ],
    clinton: [ // Head Teacher (Mr Clinton) - Dark formal suit
        "....xxxxxx......", "...xhhhhhhx.....", "..xhhhhhhhhx....", "..xhssxxsshx....",
        "..xhs.xx.shx....", "..xhsssssshx....", "....xxxxxx......", "...xddddddx.....",
        "..xddddddddx....", ".xddddddddddx...", ".xddwwwwwdddx...", ".xddddddddddx...",
        "..xddddddddx....", "..xddddddddx....", "...xx....xx.....", "...xx....xx....."
    ],
    // --- NEW SPRITES: MCDONALD (Yellow Hi-Viz) & LAKIN (Blue Coat) ---
    mcdonald: [ 
        "....xxxxxx......", "...xhhhhhhx.....", "..xhhhhhhhhx....", "..xhssxxsshx....",
        "..xhs.xx.shx....", "..xhsssssshx....", "....xxxxxx......", "...xyyyyyyx.....",
        "..xyyyyyyyyx....", ".xyywwwwwwyyx...", ".xyywwwwwwyyx...", ".xyyyyyyyyyyx...",
        "..xccccccccx....", "..xccccccccx....", "...xx....xx.....", "...xx....xx....."
    ],
    lakin: [ 
        "....xxxxxx......", "...xhhhhhhx.....", "..xhhhhhhhhx....", "..xhssxxsshx....",
        "..xhs.xx.shx....", "..xhsssssshx....", "....xxxxxx......", "...xbbbbbbx.....",
        "..xbbbbbbbbx....", ".xbbwwwwwwbbx...", ".xbbwwwwwwbbx...", ".xbbbbbbbbbbx...",
        "..xccccccccx....", "..xccccccccx....", "...xx....xx.....", "...xx....xx....."
    ],
    // ------------------------------------------------------------------
    student: [ // Generic Student
        "....xxxxxx......", "...xhhhhhhx.....", "..xhhhhhhhhx....", "..xhssxxsshx....",
        "..xhs.xx.shx....", "..xhsssssshx....", "....xxxxxx......", "...xbbbbbbx.....",
        "..xbbbbbbbbx....", ".xbbwwwwwwbbx...", ".xbbwwwwwwbbx...", ".xbbbbbbbbbbx...",
        "..xccccccccx....", "..xccccccccx....", "...xx....xx.....", "...xx....xx....."
    ],
    glitch: [
        "....mmmmmm......", "...mm.mm.mm.....", "..mmmmmmmmmm....", "..m.m.mm.m.m....",
        "..mmmmmmmmmm....", "..m.mmmmmm.m....", "....mmmmmm......", "...mxmxmxmx.....",
        "..mxmxmxmxmx....", ".xmxmxmxmxmxm...", ".mxmxmxmxmxmx...", ".xmxmxmxmxmxm...",
        "..xmxmxmxmx.....", "..mxmxmxmxm.....", "...m......m.....", "...m......m....."
    ],
    bug: [
        "................", "................", "................", "................",
        "......mm........", "....mmmmmm......", "...mmxmmxmm.....", "...mmmmmmmm.....",
        "....mmmmmm......", "....m....m......", "....m....m......", "................",
        "................", "................", "................", "................"
    ],
    door: [
        "xxxxx......xxxxx", "xDDDx......xDDDx", "xDDDx......xDDDx", "xDDDx......xDDDx",
        "xDDDx......xDDDx", "xDDDx......xDDDx", "xDDDx......xDDDx", "xDDDx......xDDDx",
        "xDDDx......xDDDx", "xDDDx......xDDDx", "xDDDx......xDDDx", "xDDDx......xDDDx",
        "xDDDx......xDDDx", "xDDDx......xDDDx", "xDDDx......xDDDx", "xDDDx......xDDDx"
    ],
    chair: [
        "................", "................", "................", "................",
        "......xxxx......", "......xOOx......", "......xOOx......", "......xOOx......",
        "......xOOx......", "....xxxOOxxx....", "...xOOOOOOOOx...", "...xOOOOOOOOx...",
        "...xOOOOOOOOx...", "...xxxxxxxxxx...", "...x.x....x.x...", "...x.x....x.x..."
    ],
    table: [
        "................", "................", "................", "................",
        "................", "................", "................", "................",
        ".xxxxxxxxxxxxxx.", ".xTTTTTTTTTTTTx.", ".xTTTTTTTTTTTTx.", ".xTTTTTTTTTTTTx.",
        ".xTTTTTTTTTTTTx.", ".xxxxxxxxxxxxxx.", ".xx..........xx.", ".xx..........xx."
    ],
    plant: [
        "................", "......LLLL......", "....LLLLLLLL....", "...LLLLLLLLLL...",
        "..LLLLLLLLLLLL..", "..LLLLLLLLLLLL..", "..LLLLLLLLLLLL..", "...LLLLLLLLLL...",
        "....LLLLLLLL....", "......LLLL......", ".......xx.......", "......xDDx......",
        "......xDDx......", "......xDDx......", "......xDDx......", "......xxxx......"
    ],
    alert: [ // "!" Icon
        "................", ".......OO.......", "......OOOO......", "......OOOO......",
        "......OOOO......", "......OOOO......", ".......OO.......", ".......OO.......",
        ".......OO.......", "................", ".......OO.......", "......OOOO......",
        ".......OO.......", "................", "................", "................"
    ]
};
function drawSprite(ctx, key, x, y, size, facingRight = true, bob = 0, opacity = 1.0) {
    const data = SPRITE_DATA[key];
    if (!data) return;
    const pixelSize = size / 16;
    const bobOffset = Math.sin(bob) * 2; 
    ctx.globalAlpha = opacity;
    for (let r = 0; r < 16; r++) {
        for (let c = 0; c < 16; c++) {
            let char = data[r][c];
            if (char !== '.') {
                ctx.fillStyle = PALETTE[char];
                let drawX = facingRight ? x + (15 - c) * pixelSize : x + c * pixelSize;
                let drawY = y + r * pixelSize + bobOffset;
                ctx.fillRect(drawX, drawY, pixelSize, pixelSize);
            }
        }
    }
    ctx.globalAlpha = 1.0;
}
function wrapText(context, text, x, y, maxWidth, lineHeight) {
    if (!text) return;
    const words = text.split(' ');
    let line = '';
    for(let n = 0; n < words.length; n++) {
        const testLine = line + words[n] + ' ';
        const metrics = context.measureText(testLine);
        if (metrics.width > maxWidth && n > 0) {
            context.fillText(line, x, y);
            line = words[n] + ' ';
            y += lineHeight;
        }
        else line = testLine;
    }
    context.fillText(line, x, y);
}
// --- AUDIO SYSTEM ---
let audioCtx, bgmOscillators = [], isMuted = false, currentSong = 'NONE'; 
let battleInit = false, battleLead, battleBass, battleKick, battleNoise, battleLeadSeq, battleBassSeq, battleDrumSeq;
// Town music
let townInit = false, townSynth, townBass, townMelodySeq, townBassSeq;
// Chapel music
let chapelInit = false, chapelSynth, chapelMelodySeq;
// Victory music
let victoryMusicInit = false, victoryMusicSynth, victoryMusicBass, victoryMelodySeq, victoryBassSeq;
// NEW: ENEMY DOWN SFX
let enemyDownInit = false;
let downNoise, downHit;
// NEW: ENCOUNTER ALARM SFX
let encounterInit = false;
let encounterSynth;
// NEW: VICTORY FANFARE
let victoryInit = false;
let victorySynth;
function initVictoryFanfare() {
    if (victoryInit) return;
    victorySynth = new Tone.Synth({
        oscillator: { type: "triangle" },
        envelope: { attack: 0.01, decay: 0.1, sustain: 0.3, release: 0.2 }
    }).toDestination();
    victorySynth.volume.value = -8;
    victoryInit = true;
}
function playVictoryFanfare() {
    if (Tone.context.state !== 'running') return;
    initVictoryFanfare();
    const now = Tone.now();
    // Upbeat victory jingle: da da da daaaa!
    const melody = [
        { note: "C5", time: 0, duration: "8n" },
        { note: "E5", time: 0.15, duration: "8n" },
        { note: "G5", time: 0.3, duration: "8n" },
        { note: "C6", time: 0.45, duration: "4n" },
        // Extra flourish
        { note: "G5", time: 0.75, duration: "16n" },
        { note: "C6", time: 0.85, duration: "4n" }
    ];
    
    melody.forEach(({note, time, duration}) => {
        victorySynth.triggerAttackRelease(note, duration, now + time);
    });
}
function initEncounterSfx() {
  if (encounterInit) return;
  encounterSynth = new Tone.Synth({
      oscillator: { type: "square" },
      envelope: { attack: 0.001, decay: 0.1, sustain: 0.3, release: 0.1 }
  }).toDestination();
  encounterSynth.volume.value = -8;
  encounterInit = true;
}
function playEncounterSfx() {
  if (Tone.context.state !== 'running') return;
  initEncounterSfx();
  const now = Tone.now();
  // Siren-style alarm: alternating high and low pitches
  const siren = [
      { note: "E5", time: 0 },
      { note: "C5", time: 0.15 },
      { note: "E5", time: 0.3 },
      { note: "C5", time: 0.45 },
      { note: "E5", time: 0.6 },
      { note: "C5", time: 0.75 },
      { note: "E5", time: 0.9 },
      { note: "C5", time: 1.05 },
      // Dramatic rise at the end
      { note: "G5", time: 1.2 },
      { note: "C6", time: 1.35 }
  ];
  
  siren.forEach(({note, time}) => {
      encounterSynth.triggerAttackRelease(note, "8n", now + time);
  });
}
function initEnemyDownSfx() {
  if (enemyDownInit) return;
  downNoise = new Tone.NoiseSynth({ noise: { type: "white" }, envelope: { attack: 0.001, decay: 0.45, sustain: 0 } }).toDestination(); downNoise.volume.value = -8;
  downHit = new Tone.Synth({ oscillator: { type: "square" }, envelope: { attack: 0.001, decay: 0.2, sustain: 0, release: 0.1 } }).toDestination(); downHit.volume.value = -6;
  enemyDownInit = true;
}
function playEnemyDownSfx() {
  if (Tone.context.state !== 'running') return;
  initEnemyDownSfx();
  const now = Tone.now();
  downNoise.triggerAttackRelease("4n", now);
  const fallNotes = ["C3", "G2", "C2"];
  fallNotes.forEach((n, i) => { downHit.triggerAttackRelease(n, "16n", now + 0.15 + i*0.08); });
  downHit.triggerAttackRelease("C1", "8n", now + 0.45);
}
async function initAudio() {
    if (!audioCtx) audioCtx = new (window.AudioContext || window.webkitAudioContext)();
    await Tone.start();
    playMusic('ROAM');
}
function initTownMusic() {
  if (townInit) return;
  // Upbeat Town Theme
  townSynth = new Tone.Synth({ 
      oscillator: { type: "triangle" }, 
      envelope: { attack: 0.02, decay: 0.1, sustain: 0.3, release: 0.5 }
  }).toDestination(); 
  townSynth.volume.value = -10; 
  townBass = new Tone.Synth({ 
      oscillator: { type: "square" }, 
      envelope: { attack: 0.05, decay: 0.2, sustain: 0.5, release: 0.5 }
  }).toDestination(); 
  townBass.volume.value = -8;
  const melodyNotes = ["C5", null, "E5", "G5", "A5", "G5", "E5", "C5", "D5", null, "F5", "A5", "G5", "F5", "D5", "B4"];
  const bassNotes = ["C3", null, "C3", null, "F3", null, "F3", null, "G3", null, "G3", null, "C3", null, "C3", null];
  townMelodySeq = new Tone.Sequence((t, n) => n && townSynth.triggerAttackRelease(n, "8n", t), melodyNotes, "8n");
  townBassSeq = new Tone.Sequence((t, n) => n && townBass.triggerAttackRelease(n, "8n", t), bassNotes, "4n");
  
  townMelodySeq.loop = true;
  townBassSeq.loop = true;
  townInit = true;
}
function initChapelMusic() {
    if (chapelInit) return;
    chapelSynth = new Tone.PolySynth(Tone.Synth, {
        oscillator: { type: "sine" },
        envelope: { attack: 0.5, decay: 1, sustain: 0.8, release: 1 }
    }).toDestination();
    chapelSynth.volume.value = -12;
    const chords = [
        ["C4", "E4", "G4"], null, ["F4", "A4", "C5"], null,
        ["G4", "B4", "D5"], null, ["C4", "E4", "G4"], null
    ];
    
    chapelMelodySeq = new Tone.Sequence((t, notes) => {
        if (notes) chapelSynth.triggerAttackRelease(notes, "2n", t);
    }, chords, "2n");
    
    chapelMelodySeq.loop = true;
    chapelInit = true;
}
function initVictoryMusic() {
    if (victoryMusicInit) return;
    // Upbeat victory theme
    victoryMusicSynth = new Tone.Synth({
        oscillator: { type: "triangle" },
        envelope: { attack: 0.01, decay: 0.1, sustain: 0.4, release: 0.3 }
    }).toDestination();
    victoryMusicSynth.volume.value = -10;
    victoryMusicBass = new Tone.Synth({
        oscillator: { type: "square" },
        envelope: { attack: 0.05, decay: 0.2, sustain: 0.5, release: 0.5 }
    }).toDestination();
    victoryMusicBass.volume.value = -8;
    // Celebratory melody
    const melodyNotes = [
        "C5", "E5", "G5", "C6", "G5", "E5", "C5", "E5",
        "D5", "F5", "A5", "D6", "A5", "F5", "D5", "F5",
        "E5", "G5", "C6", "E6", "C6", "G5", "E5", "G5",
        "C5", "E5", "G5", "C6", null, null, null, null
    ];
    
    const bassNotes = [
        "C3", "C3", "C3", "C3", "F3", "F3", "F3", "F3",
        "G3", "G3", "G3", "G3", "C3", "C3", "C3", "C3"
    ];
    victoryMelodySeq = new Tone.Sequence((t, n) => n && victoryMusicSynth.triggerAttackRelease(n, "8n", t), melodyNotes, "8n");
    victoryBassSeq = new Tone.Sequence((t, n) => n && victoryMusicBass.triggerAttackRelease(n, "8n", t), bassNotes, "4n");
    victoryMelodySeq.loop = true;
    victoryBassSeq.loop = true;
    victoryMusicInit = true;
}
function initBattleMusic() {
  if (battleInit) return;
  battleLead = new Tone.Synth({ oscillator: { type: "square" }, envelope: { attack: 0.01, decay: 0.1, sustain: 0.3, release: 0.2 }}).toDestination(); battleLead.volume.value = -10; 
  battleBass = new Tone.Synth({ oscillator: { type: "square" }, envelope: { attack: 0.01, decay: 0.1, sustain: 0.4, release: 0.2 }}).toDestination(); battleBass.volume.value = -8;
  battleKick = new Tone.MembraneSynth().toDestination(); battleKick.volume.value = -6;
  battleNoise = new Tone.NoiseSynth({ noise: { type: "white" }, envelope: { attack: 0.001, decay: 0.12, sustain: 0 }}).toDestination(); battleNoise.volume.value = -12;
  const bassNotes = ["C2", "C2", "C2", "C2", "Ab1", "Ab1", "Ab1", "Ab1", "Bb1", "Bb1", "Bb1", "Bb1", "G1", "G1", "G1", "G1"];
  battleBassSeq = new Tone.Sequence((t, n) => n && battleBass.triggerAttackRelease(n, "8n", t), bassNotes, "8n");
  const leadA = ["C5", null, "Eb5", null, "G5", null, "F5", null, "Eb5", null, "D5", null, "C5", null, null, null];
  const leadB = ["G5", null, "F5", null, "Eb5", null, "C5", null, "Bb4", null, "C5", null, "D5", null, null, null];
  battleLeadSeq = new Tone.Sequence((t, n) => n && battleLead.triggerAttackRelease(n, "16n", t), [...leadA,...leadA,...leadB,...leadA], "16n");
  const drum = ["K", null, null, null, "K", null, null, null, "K", null, null, null, "K", null, null, null];
  battleDrumSeq = new Tone.Sequence((t, h) => { if (h === "K") battleKick.triggerAttackRelease("C1", "16n", t); }, drum, "16n");
  
  battleBassSeq.loop = true;
  battleLeadSeq.loop = true;
  battleDrumSeq.loop = true;
  
  battleInit = true;
}
function stopAllMusic() {
    // --- ROBUST CLEANUP ---
    // Instead of just stopping sequences, we dispose them and the synths.
    // This guarantees a "fresh start" every time a track loads, preventing
    // the RangeError (scheduling in past) and timing issues.
    // 1. Battle Music Cleanup
    if (battleBassSeq) { battleBassSeq.dispose(); battleBassSeq = null; }
    if (battleLeadSeq) { battleLeadSeq.dispose(); battleLeadSeq = null; }
    if (battleDrumSeq) { battleDrumSeq.dispose(); battleDrumSeq = null; }
    if (battleLead) { battleLead.dispose(); battleLead = null; }
    if (battleBass) { battleBass.dispose(); battleBass = null; }
    if (battleKick) { battleKick.dispose(); battleKick = null; }
    if (battleNoise) { battleNoise.dispose(); battleNoise = null; }
    battleInit = false;
    // 2. Town Music Cleanup
    if (townMelodySeq) { townMelodySeq.dispose(); townMelodySeq = null; }
    if (townBassSeq) { townBassSeq.dispose(); townBassSeq = null; }
    if (townSynth) { townSynth.dispose(); townSynth = null; }
    if (townBass) { townBass.dispose(); townBass = null; }
    townInit = false;
    // 3. Chapel Music Cleanup
    if (chapelMelodySeq) { chapelMelodySeq.dispose(); chapelMelodySeq = null; }
    if (chapelSynth) { chapelSynth.dispose(); chapelSynth = null; }
    chapelInit = false;
    // 4. Victory Music Cleanup
    if (victoryMelodySeq) { victoryMelodySeq.dispose(); victoryMelodySeq = null; }
    if (victoryBassSeq) { victoryBassSeq.dispose(); victoryBassSeq = null; }
    if (victoryMusicSynth) { victoryMusicSynth.dispose(); victoryMusicSynth = null; }
    if (victoryMusicBass) { victoryMusicBass.dispose(); victoryMusicBass = null; }
    victoryMusicInit = false;
    // 5. Reset Transport
    try {
        Tone.Transport.stop();
        Tone.Transport.cancel(); // Clear all scheduled events
        Tone.Transport.position = 0; // Reset timeline
    } catch(e) {
        console.log("Error stopping transport:", e);
    }
    
    currentSong = 'NONE';
}
async function startBattleMusic() {
  if (Tone.context.state !== 'running') await Tone.start();
  Tone.Transport.bpm.value = 150;
  initBattleMusic(); // Will recreate synths/sequences because init flag was reset
  battleBassSeq.start(0); battleLeadSeq.start(0); battleDrumSeq.start(0);
  Tone.Transport.start();
}
async function startTownMusic() {
    if (Tone.context.state !== 'running') await Tone.start();
    Tone.Transport.bpm.value = 120;
    initTownMusic(); // Will recreate
    townMelodySeq.start(0);
    townBassSeq.start(0);
    Tone.Transport.start();
}
async function startChapelMusic() {
    if (Tone.context.state !== 'running') await Tone.start();
    Tone.Transport.bpm.value = 80;
    initChapelMusic(); // Will recreate
    chapelMelodySeq.start(0);
    Tone.Transport.start();
}
async function startVictoryMusic() {
    if (Tone.context.state !== 'running') await Tone.start();
    Tone.Transport.bpm.value = 140;
    initVictoryMusic(); // Will recreate
    victoryMelodySeq.start(0);
    victoryBassSeq.start(0);
    Tone.Transport.start();
}
function playMusic(track) {
    // Don't restart if already playing this track
    if (currentSong === track) return;
    
    stopAllMusic();
    currentSong = track;
    
    if (track === 'BATTLE') { 
        startBattleMusic(); 
    } else if (track === 'ROAM') {
        startTownMusic();
    } else if (track === 'CHAPEL') {
        startChapelMusic();
    } else if (track === 'WIN') {
        startVictoryMusic();
    }
}
function playSound(type) {
    if (isMuted) return;
    if(Tone && Tone.context.state === 'running') {
        const synth = new Tone.Synth().toDestination();
        const noise = new Tone.NoiseSynth().toDestination();
        if (type === 'SELECT') synth.triggerAttackRelease("C6", "32n");
        if (type === 'CORRECT') synth.triggerAttackRelease("E6", "16n");
        if (type === 'WRONG') { noise.noise.type = 'pink'; noise.triggerAttackRelease("8n"); }
        if (type === 'HIT') { noise.noise.type = 'white'; noise.triggerAttackRelease("16n"); }
        if (type === 'ALERT') synth.triggerAttackRelease("C7", "32n"); // High ping for alert
    }
}
// --- GAME DATA ---
const COLORS = { 
    floor: '#222', wall: '#444', 
    mediaFloor: '#203020', libraryFloor: '#202040', examFloor: '#302020' 
};
const QUIZ_DATA = [
    { q: "1. According to JCQ, what must a school's malpractice policy include?", options: ["Instructions for improving AI writing quality", "Rules for AI use in assessments", "A list of AI tools teachers recommend"], correct: 1 },
    { q: "2. What are teachers responsible for confirming?", options: ["That AI tools have been used efficiently", "That students enjoyed the task", "The authenticity of each student's work"], correct: 2 },
    { q: "3. What must students do if they use AI in permitted coursework?", options: ["Paraphrase the AI output", "Reference the AI tool clearly", "Email the awarding body"], correct: 1 },
    { q: "4. When can students earn marks for content produced solely by AI?", options: ["Only if they reference it correctly", "Only if the teacher supervises the AI use", "Never—AI-generated content cannot earn marks"], correct: 2 },
    { q: "5. What is AI misuse according to the JCQ guidance?", options: ["Using AI to check your spelling", "Using AI to generate ideas only", "Taking AI-produced work and presenting it as your own"], correct: 2 },
    { q: "6. What should teachers compare work against if they suspect AI misuse?", options: ["The student's favourite writing style", "Previous work for differences in tone, quality, and formatting", "The student's mock exam results only"], correct: 1 },
    { q: "7. What should students do before signing the declaration on coursework?", options: ["Remove all references to AI", "Double-check all AI usage has been referenced", "Submit anonymously"], correct: 1 },
    { q: "8. If a student misuses AI, what is a possible consequence?", options: ["A warning with no grade impact", "Extra time on their next assessment", "They may lose marks or be disqualified"], correct: 2 },
    { q: "9. What is one indicator of AI-generated text?", options: ["Clear references", "Lack of local knowledge or confidently wrong statements", "Use of British spelling"], correct: 1 },
    { q: "10. If AI misuse is found after a declaration form has been signed, what must teachers do?", options: ["Ask the student to redo the work", "Report it to the awarding body", "Remove the mark and move on"], correct: 1 },
    { q: "11. What is the safest way to interact with AI tools?", options: ["Share personal data to get better answers", "Avoid sharing sensitive information", "Use AI only on public computers"], correct: 1 },
    { q: "12. Why is it important to check AI outputs?", options: ["AI always provides verified facts", "AI often guesses and can generate inaccurate content", "AI can only give answers written by experts"], correct: 1 },
    { q: "13. Which example demonstrates ethical AI use?", options: ["Using AI to impersonate someone online", "Using AI to support ideas but citing it properly", "Submitting AI-written work as your own"], correct: 1 },
    { q: "14. What is a responsible approach when using AI for decision-making?", options: ["Rely entirely on AI recommendations", "Treat AI suggestions critically and verify them", "Ignore human judgment in favour of AI"], correct: 1 },
    { q: "15. Why must AI-generated content be acknowledged in academic work?", options: ["To hide how much AI was used", "Because it helps boost the grade", "Because transparency prevents plagiarism and maintains integrity"], correct: 2 }
];

// --- QUESTION POOL SYSTEM ---
let questionPool = [];
function getNextQuestion() {
    if (questionPool.length === 0) {
        questionPool = [...QUIZ_DATA]; // Refill if empty
    }
    const randomIndex = Math.floor(Math.random() * questionPool.length);
    const question = questionPool[randomIndex];
    questionPool.splice(randomIndex, 1); // Remove used question so it doesn't repeat immediately
    return question;
}

// --- MAP SYSTEM ---
const TILE_SIZE = 40;
const COLS = 20;
const ROWS = 15;
// FURNITURE MAPPING: 3=Table, 4=Chair, 5=Plant
const MAP_LAYOUTS = {
    'COMMON_ROOM': {
        name: "COMMON ROOM (HUB)",
        color: '#333344',
        data: [
            [1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
            [1,5,0,0,0,0,0,4,3,3,4,0,0,0,0,0,0,0,5,1], // Top center-ish group
            [1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],
            [1,0,0,4,3,4,0,0,0,0,0,0,0,4,3,4,0,0,0,1], // Left group + New Right Group
            [1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],
            [1,0,0,0,0,0,4,3,3,4,0,0,4,3,3,4,0,0,0,1], // FIXED Row 5: Split central group (Gap at 10,11)
            [1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],
            [1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],
            [1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],
            [1,0,0,4,3,4,0,0,0,0,0,0,0,4,3,4,0,0,0,1], // Bottom Left + New Bottom Right
            [1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],
            [1,5,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,5,1], // Added corner plants
            [1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],
            [1,0,0,0,0,0,0,0,0,2,2,0,0,0,0,0,0,0,0,1], // Door South to Corridor
            [1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1]
        ],
        npcs: [
            { id: 'mcmahon_intro', name: 'Mrs McMahon', role: 'Teacher', spriteKey: 'oneill', color: '#5555ff', gridX: 10, gridY: 3, dialogue: ["Improper use of AI is sweeping Archbishop Ilsley.", "The bugs have locked Mrs Grant in her office with a Glitch.", "You need to help the school by destroying three bugs to unlock her office then fight the Glitch.", "Good Luck."] },
            { id: 'clinton', name: 'Mr Clinton', role: 'Head Teacher', spriteKey: 'clinton', color: '#333333', gridX: 5, gridY: 5, dialogue: ["I am Mr Clinton, the head teacher.", "We have some bugs."] },
            { id: 'oneill_strict_cr', name: 'Mrs O\'Neill', role: 'Head of Behaviour', spriteKey: 'oneill_strict', color: '#ff0000', gridX: 15, gridY: 8, dialogue: [], autoInteract: true, damage: 10, messages: ["You are being too loud!", "I told you to get to lesson!"] },
            { id: 'brookes', name: 'Mr Brookes', role: 'Media & Film', spriteKey: 'brookes', color: '#44aa44', gridX: 2, gridY: 5, dialogue: ["*SIGH* I told them we needed more AI and Media Literacy training...", "But would they listen... No!", "Anyways, you might want to avoid Ms O'Neill.", "If you need some health points, visit the canteen or chapel."] }
        ],
        minions: [],
        doors: [
            { x: 9, y: 13, target: 'CORRIDOR', targetX: 9, targetY: 2 },
            { x: 10, y: 13, target: 'CORRIDOR', targetX: 10, targetY: 2 }
        ],
        crowd: []
    },
    'CORRIDOR': {
        name: "MAIN CORRIDOR",
        color: '#222222',
        data: [
            [1,1,1,1,1,1,1,1,1,2,2,1,1,1,1,1,1,1,1,1], // Door North to Common Room
            [1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],
            [1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],
            [1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,2], // East to Canteen
            [1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],
            [2,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1], // West to Chapel
            [1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],
            [1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],
            [1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],
            [1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],
            [1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],
            [1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],
            [1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],
            [1,0,0,0,0,0,0,0,0,2,2,0,0,0,0,0,0,0,0,1], // South to Classrooms
            [1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1]
        ],
        npcs: [
            { id: 'botwright', name: 'Mr Botwright', role: 'Tutor', spriteKey: 'botwright', color: '#5555ff', gridX: 12, gridY: 8, dialogue: ["Lots of kids in the corridor today, they must be looking for the glitch!"] },
            { id: 'oneill_strict', name: 'Mrs O\'Neill', role: 'Head of Behaviour', spriteKey: 'oneill_strict', color: '#ff0000', gridX: 5, gridY: 6, dialogue: [], autoInteract: true, damage: 10, messages: ["You are being too loud!", "I told you to get to lesson!"] },
            { id: 'foley', name: 'Mr Foley', role: 'Teacher', spriteKey: 'clinton', color: '#00aaaa', gridX: 8, gridY: 4, dialogue: ["Come on now, walk with purpose, every minute matters!"] }
        ],
        minions: [],
        doors: [
            { x: 9, y: 0, target: 'COMMON_ROOM', targetX: 9, targetY: 12 },
            { x: 10, y: 0, target: 'COMMON_ROOM', targetX: 10, targetY: 12 },
            { x: 19, y: 3, target: 'CANTEEN', targetX: 2, targetY: 7 },
            { x: 0, y: 5, target: 'CHAPEL', targetX: 18, targetY: 7 },
            { x: 9, y: 13, target: 'CLASSROOM_HALL', targetX: 9, targetY: 1 },
            { x: 10, y: 13, target: 'CLASSROOM_HALL', targetX: 10, targetY: 1 }
        ],
        crowd: [
            { gridX: 4, gridY: 3, spriteKey: 'student', facingRight: true },
            { gridX: 16, gridY: 4, spriteKey: 'student', facingRight: false },
            { gridX: 8, gridY: 10, spriteKey: 'student', facingRight: true },
            { gridX: 14, gridY: 11, spriteKey: 'student', facingRight: false },
            { gridX: 2, gridY: 7, spriteKey: 'student', facingRight: true },
            { gridX: 18, gridY: 6, spriteKey: 'student', facingRight: false }
        ]
    },
    'CANTEEN': {
        name: "THE CANTEEN",
        color: '#302020',
        data: [
            [1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
            [1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],
            [1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],
            [1,3,3,3,3,0,0,3,3,3,3,0,0,3,3,3,3,0,0,1],
            [1,4,4,4,4,0,0,4,4,4,4,0,0,4,4,4,4,0,0,1],
            [1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],
            [1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],
            [2,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1], // Door West
            [1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],
            [1,3,3,3,3,0,0,3,3,3,3,0,0,3,3,3,3,0,0,1],
            [1,4,4,4,4,0,0,4,4,4,4,0,0,4,4,4,4,0,0,1],
            [1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],
            [1,0,0,0,0,0,6,6,6,6,6,6,6,0,0,0,0,0,0,1], // Serving Counter
            [1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],
            [1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1]
        ],
        npcs: [
            { id: 'julie', name: 'Julie', role: 'Canteen Staff', spriteKey: 'julie', color: '#ffffff', gridX: 10, gridY: 11, dialogue: ["Hi love! Need a break?", "Here, have a hot meal. It's on the house."], heal: true },
            { id: 'student_chicken', name: 'Student', role: 'Year 12', spriteKey: 'student', color: '#ddddff', gridX: 8, gridY: 10, dialogue: ["Do the bugs know it is Chicken Burger day?"] },
            { id: 'mcdonald', name: 'Mr McDonald', role: 'Teacher', spriteKey: 'mcdonald', color: '#ffff00', gridX: 5, gridY: 8, dialogue: ["I am on duty. I hope the bugs do not mess with Bromcom today"] },
            { id: 'lakin', name: 'Mr Lakin', role: 'Teacher', spriteKey: 'lakin', color: '#8888ff', gridX: 15, gridY: 8, dialogue: ["The glitch best not break the laser cutter."] }
        ],
        minions: [],
        doors: [
            { x: 0, y: 7, target: 'CORRIDOR', targetX: 18, targetY: 3 } 
        ],
        crowd: [
            { gridX: 2, gridY: 4, spriteKey: 'student', facingRight: true, static: true },
            { gridX: 14, gridY: 4, spriteKey: 'student', facingRight: false, static: true }
        ]
    },
    'CHAPEL': {
        name: "THE CHAPEL",
        color: '#202040',
        data: [
            [1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
            [1,0,0,0,0,0,0,0,0,6,0,0,0,0,0,0,0,0,0,1], // Altar
            [1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],
            [1,0,0,4,4,4,4,0,0,0,0,0,4,4,4,4,0,0,0,1],
            [1,0,0,4,4,4,4,0,0,0,0,0,4,4,4,4,0,0,0,1],
            [1,0,0,4,4,4,4,0,0,0,0,0,4,4,4,4,0,0,0,1],
            [1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],
            [1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,2], // Door East
            [1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],
            [1,0,0,4,4,4,4,0,0,0,0,0,4,4,4,4,0,0,0,1],
            [1,0,0,4,4,4,4,0,0,0,0,0,4,4,4,4,0,0,0,1],
            [1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],
            [1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],
            [1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],
            [1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1]
        ],
        npcs: [
            { id: 'deacon', name: 'Deacon Martin', role: 'Chaplain', spriteKey: 'deacon', color: '#aaaaaa', gridX: 9, gridY: 2, dialogue: ["Peace be with you.", "Let me heal your weary soul."], heal: true },
            { id: 'student_praying', name: 'Student', role: 'Year 13', spriteKey: 'student', color: '#ddddff', gridX: 12, gridY: 4, dialogue: ["Please let the bugs go away...", "Amen."] }
        ],
        minions: [],
        doors: [
            { x: 19, y: 7, target: 'CORRIDOR', targetX: 1, targetY: 5 }
        ],
        crowd: [
            { gridX: 4, gridY: 4, spriteKey: 'student', facingRight: true, static: true },
            { gridX: 4, gridY: 10, spriteKey: 'student', facingRight: true, static: true }
        ]
    },
    'CLASSROOM_HALL': {
        name: "LOWER CORRIDOR",
        color: '#222222',
        data: [
            [1,1,1,1,1,1,1,1,1,2,2,1,1,1,1,1,1,1,1,1], // North to Main Corridor
            [1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],
            [1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],
            [1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],
            [2,0,0,0,0,0,2,0,0,0,0,0,2,0,0,0,0,0,0,2], // West(C1), Mid(C2), East(C3), FarEast(Boss)
            [1,0,0,0,0,0,1,0,0,0,0,0,1,0,0,0,0,0,0,1],
            [1,0,0,0,0,0,1,0,0,0,0,0,1,0,0,0,0,0,0,1],
            [1,0,0,0,0,0,1,0,0,0,0,0,1,0,0,0,0,0,0,1],
            [1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
            [0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0],
            [0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0],
            [0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0],
            [0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0],
            [0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0],
            [0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0]
        ],
        npcs: [
            { id: 'oneill_strict_ch', name: 'Mrs O\'Neill', role: 'Head of Behaviour', spriteKey: 'oneill_strict', color: '#ff0000', gridX: 3, gridY: 3, dialogue: [], autoInteract: true, damage: 10, messages: ["You are being too loud!", "I told you to get to lesson!"] }
        ],
        minions: [],
        doors: [
            { x: 9, y: 0, target: 'CORRIDOR', targetX: 9, targetY: 12 },
            { x: 10, y: 0, target: 'CORRIDOR', targetX: 10, targetY: 12 },
            { x: 0, y: 4, target: 'CLASSROOM_1', targetX: 18, targetY: 7 },
            { x: 6, y: 4, target: 'CLASSROOM_2', targetX: 9, targetY: 13 }, 
            { x: 12, y: 4, target: 'CLASSROOM_3', targetX: 9, targetY: 13 },
            { x: 19, y: 4, target: 'OFFICE', targetX: 1, targetY: 7 } // Boss Room
        ],
        crowd: []
    },
    'CLASSROOM_1': {
        name: "CLASSROOM 1", color: '#252525',
        data: [[1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],[1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],[1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],[1,3,3,0,3,3,0,3,3,0,3,3,0,0,0,0,0,0,0,1],[1,4,4,0,4,4,0,4,4,0,4,4,0,0,0,0,0,0,0,1],[1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],[1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],[1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,2],[1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],[1,3,3,0,3,3,0,3,3,0,3,3,0,0,0,0,0,0,0,1],[1,4,4,0,4,4,0,4,4,0,4,4,0,0,0,0,0,0,0,1],[1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],[1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],[1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],[1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1]],
        npcs: [
            { id: 'jones', name: 'Mr Jones', role: 'History', spriteKey: 'jones', color: '#aaffaa', gridX: 15, gridY: 2, dialogue: ["AI keeps hallucinating facts about the Tudors.", "I need real sources!"] }
        ],
        minions: [{gridX:5,gridY:5,spriteKey:'bug',active:true}], doors: [{x:19,y:7,target:'CLASSROOM_HALL',targetX:1,targetY:4}],
        crowd: [
            { gridX: 2, gridY: 4, spriteKey: 'student', facingRight: true, static: true },
            { gridX: 5, gridY: 4, spriteKey: 'student', facingRight: true, static: true },
            { gridX: 8, gridY: 10, spriteKey: 'student', facingRight: true, static: true }
        ]
    },
    'CLASSROOM_2': {
        name: "CLASSROOM 2", color: '#252525',
        data: [[1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],[1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],[1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],[1,3,3,0,3,3,0,3,3,0,3,3,0,0,0,0,0,0,0,1],[1,4,4,0,4,4,0,4,4,0,4,4,0,0,0,0,0,0,0,1],[1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],[1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],[1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],[1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],[1,3,3,0,3,3,0,3,3,0,3,3,0,0,0,0,0,0,0,1],[1,4,4,0,4,4,0,4,4,0,4,4,0,0,0,0,0,0,0,1],[1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],[1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],[1,0,0,0,0,0,0,0,0,2,0,0,0,0,0,0,0,0,0,1],[1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1]],
        npcs: [
             { id: 'russell', name: 'Miss Russell', role: 'Science', spriteKey: 'russell', color: '#aaaaff', gridX: 2, gridY: 2, dialogue: ["Data must be verified.", "Don't let AI make up your results."] }
        ],
        minions: [{gridX:10,gridY:8,spriteKey:'bug',active:true}], doors: [{x:9,y:13,target:'CLASSROOM_HALL',targetX:6,targetY:5}],
        crowd: [
            { gridX: 4, gridY: 4, spriteKey: 'student', facingRight: true, static: true },
            { gridX: 10, gridY: 4, spriteKey: 'student', facingRight: true, static: true },
            { gridX: 2, gridY: 10, spriteKey: 'student', facingRight: true, static: true }
        ]
    },
    'CLASSROOM_3': {
        name: "CLASSROOM 3", color: '#252525',
        data: [[1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],[1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],[1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],[1,3,3,0,3,3,0,3,3,0,3,3,0,0,0,0,0,0,0,1],[1,4,4,0,4,4,0,4,4,0,4,4,0,0,0,0,0,0,0,1],[1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],[1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],[1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],[1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],[1,3,3,0,3,3,0,3,3,0,3,3,0,0,0,0,0,0,0,1],[1,4,4,0,4,4,0,4,4,0,4,4,0,0,0,0,0,0,0,1],[1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],[1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],[1,0,0,0,0,0,0,0,0,2,0,0,0,0,0,0,0,0,0,1],[1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1]],
        npcs: [
            { id: 'mckeown', name: 'Mrs McKeown', role: 'English', spriteKey: 'mckeown', color: '#ffaaaa', gridX: 15, gridY: 2, dialogue: ["Where is your voice?", "This essay sounds like a robot wrote it."] }
        ],
        minions: [{gridX:14,gridY:5,spriteKey:'bug',active:true}], doors: [{x:9,y:13,target:'CLASSROOM_HALL',targetX:12,targetY:5}],
        crowd: [
            { gridX: 1, gridY: 4, spriteKey: 'student', facingRight: true, static: true },
            { gridX: 7, gridY: 4, spriteKey: 'student', facingRight: true, static: true },
            { gridX: 5, gridY: 10, spriteKey: 'student', facingRight: true, static: true }
        ]
    },
    'OFFICE': {
        name: "MRS GRANT'S OFFICE",
        color: '#301010',
        data: [
            [1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
            [1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],
            [1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],
            [1,0,0,0,0,0,0,0,0,6,0,0,0,0,0,0,0,0,0,1], // Big Desk
            [1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],
            [1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],
            [1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],
            [2,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1], // Door West - FIXED to type 2
            [1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],
            [1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],
            [1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],
            [1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],
            [1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],
            [1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],
            [1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1]
        ],
        npcs: [
            { id: 'grant_final', name: 'Mrs Grant', role: 'Head of Sixth Form', spriteKey: 'grant', color: '#ff5555', gridX: 16, gridY: 7, dialogue: ["The Main Glitch is right there!", "Defeat it to recover the JCQ Guidance data!"] }
        ],
        minions: [],
        doors: [
            { x: 0, y: 7, target: 'CLASSROOM_HALL', targetX: 18, targetY: 4 }
        ],
        boss: { active: true, gridX: 9, gridY: 5, spriteKey: 'glitch', hp: 200 },
        crowd: []
    }
};
const STATE = { INTRO: 0, ROAM: 1, DIALOGUE: 2, BATTLE: 3, GAMEOVER: 4, WIN: 5, TRANSITION: 6 };
let currentState = STATE.INTRO;
let frames = 0;
let winTimer = 0; // New timer for victory screen
let transitionTimer = 0; 
let introCutsceneActive = false;
let introCutsceneFinished = false;
let officeCutsceneActive = false; // NEW: Office cutscene flag
let officeCutscenePlayed = false; // Ensure it only happens once

const player = { 
    gridX: 10, gridY: 7, // Start center of Common Room
    x: 400, y: 280, 
    targetX: 400, targetY: 280,
    isMoving: false,
    facingRight: true,
    bobFrame: 0,
    
    hp: 100, maxHp: 100, auth: 100, maxAuth: 100, 
    spriteKey: 'player', inventory: [], interactionCooldown: 0,
    autoInteractCooldown: 0, // Cooldown for Mrs O'Neill auto-interactions
    currentRoom: 'COMMON_ROOM'
};
// Variables for the current room state
let activeRoom = MAP_LAYOUTS['COMMON_ROOM'];
let activeMap = activeRoom.data;
let activeNPCs = activeRoom.npcs;
let activeMinions = activeRoom.minions;
let activeCrowd = activeRoom.crowd || [];
let activeBoss = null;

// --- FIX START ---
// Initialize pixel coordinates for start (Fixes vanishing Ms O'Neill)
activeNPCs.forEach(n => {
    n.pixelX = n.gridX * TILE_SIZE;
    n.pixelY = n.gridY * TILE_SIZE;
    n.targetPixelX = n.pixelX;
    n.targetPixelY = n.pixelY;
    n.isMoving = false;
});
// --- FIX END ---

let battleState = 'MENU';
let battleTurn = 'PLAYER';
let activeBattleEnemy = {};
let battleMenuIdx = 0;
let battleMsg = "";
let battleEffects = [];
let battleShake = 0;
let matrixRain = [];
let currentQuestion = null;
let selectedOptionIdx = 0;
let pendingAction = ''; 
// INPUT HANDLING FIX: Add keyProcessed flag
const keys = { ArrowUp: false, ArrowDown: false, ArrowLeft: false, ArrowRight: false, " ": false };
let keyProcessed = { ArrowUp: false, ArrowDown: false, ArrowLeft: false, ArrowRight: false, " ": false };

// --- KEYBOARD LISTENERS ---
window.addEventListener('keydown', e => { 
    if(keys.hasOwnProperty(e.key) || e.key === " ") {
        keys[e.key] = true; 
    }
});
window.addEventListener('keyup', e => { 
    if(keys.hasOwnProperty(e.key) || e.key === " ") {
        keys[e.key] = false;
        keyProcessed[e.key] = false; // Reset flag on release
    }
});

// --- MOBILE TOUCH LISTENERS (NEW) ---
function setupMobileControls() {
    const btnUp = document.getElementById('btn-up');
    const btnDown = document.getElementById('btn-down');
    const btnLeft = document.getElementById('btn-left');
    const btnRight = document.getElementById('btn-right');
    const btnAction = document.getElementById('btn-action');

    const handleTouch = (key, pressed) => {
        if (pressed) {
            keys[key] = true;
        } else {
            keys[key] = false;
            keyProcessed[key] = false; 
        }
    };

    // Helper to add listeners to buttons
    const addBtnListener = (btn, key) => {
        if(!btn) return;
        // Touch events
        btn.addEventListener('touchstart', (e) => { e.preventDefault(); handleTouch(key, true); btn.classList.add('active'); }, {passive: false});
        btn.addEventListener('touchend', (e) => { e.preventDefault(); handleTouch(key, false); btn.classList.remove('active'); }, {passive: false});
        // Mouse events for testing on desktop
        btn.addEventListener('mousedown', (e) => { e.preventDefault(); handleTouch(key, true); btn.classList.add('active'); });
        btn.addEventListener('mouseup', (e) => { e.preventDefault(); handleTouch(key, false); btn.classList.remove('active'); });
        btn.addEventListener('mouseleave', (e) => { e.preventDefault(); handleTouch(key, false); btn.classList.remove('active'); });
    };

    addBtnListener(btnUp, 'ArrowUp');
    addBtnListener(btnDown, 'ArrowDown');
    addBtnListener(btnLeft, 'ArrowLeft');
    addBtnListener(btnRight, 'ArrowRight');
    addBtnListener(btnAction, ' ');
}

// Initialize controls when DOM is ready
setupMobileControls();


function initMatrixRain() {
    matrixRain = [];
    for(let i=0; i<50; i++) {
        matrixRain.push({ x: Math.random() * canvas.width, y: Math.random() * canvas.height, speed: Math.random() * 5 + 2, chars: "101010 AI ERROR JCQ" });
    }
}
// --- ROOM SWITCHING WITH IMPROVED LOCK SYSTEM ---
function switchRoom(roomKey, startX, startY) {
    // Check Room Key Exists (Safety Check)
    if (!MAP_LAYOUTS[roomKey]) {
        console.error("INVALID ROOM KEY:", roomKey);
        return false;
    }

    // Store previous room for music logic
    const previousRoom = player.currentRoom;
    
    // Check Lock for OFFICE - IMPROVED VERSION
    if (roomKey === 'OFFICE') {
        const c1Cleared = MAP_LAYOUTS['CLASSROOM_1'].minions.every(m => !m.active);
        const c2Cleared = MAP_LAYOUTS['CLASSROOM_2'].minions.every(m => !m.active);
        const c3Cleared = MAP_LAYOUTS['CLASSROOM_3'].minions.every(m => !m.active);
        
        if (!c1Cleared || !c2Cleared || !c3Cleared) {
            playSound('ALERT');
            const status = `C1: ${c1Cleared ? '✓' : ' ✗ '} | C2: ${c2Cleared ? '✓' : ' ✗ '} | C3: ${c3Cleared ? '✓' : ' ✗ '}`;
            startDialogue({ 
                name: 'SECURITY SYSTEM', 
                role: 'LOCKDOWN', 
                color: '#ff0000', 
                dialogue: [
                    ">>> ACCESS DENIED <<<",
                    "You must clear the bugs in ALL 3 Classrooms first.",
                    status
                ],
                heal: false 
            });
            return false; 
        }
        // Trigger cutscene if entering office for the first time
        if (!officeCutscenePlayed) {
            officeCutsceneActive = true;
        }
    }
    player.currentRoom = roomKey;
    activeRoom = MAP_LAYOUTS[roomKey];
    activeMap = activeRoom.data;
    activeNPCs = activeRoom.npcs;
    activeMinions = activeRoom.minions;
    activeCrowd = activeRoom.crowd || [];
    activeBoss = activeRoom.boss || null;
    
    // Initialize smooth movement properties for crowd AND NPCs (like Ms. O'Neill)
    activeCrowd.forEach(c => {
        c.pixelX = c.gridX * TILE_SIZE;
        c.pixelY = c.gridY * TILE_SIZE;
        c.targetPixelX = c.pixelX;
        c.targetPixelY = c.pixelY;
        c.isMoving = false;
    });
    
    // Also init NPCs for smooth movement (specifically for Ms. O'Neill)
    activeNPCs.forEach(n => {
        n.pixelX = n.gridX * TILE_SIZE;
        n.pixelY = n.gridY * TILE_SIZE;
        n.targetPixelX = n.pixelX;
        n.targetPixelY = n.pixelY;
        n.isMoving = false;
    });
    
    player.gridX = startX;
    player.gridY = startY;
    player.x = startX * TILE_SIZE;
    player.y = startY * TILE_SIZE;
    player.targetX = player.x;
    player.targetY = player.y;
    
    document.getElementById('room-name').innerText = activeRoom.name;
    document.getElementById('room-name').style.display = 'block';
    setTimeout(() => document.getElementById('room-name').style.display = 'none', 2000);
    
    // Only change music when entering or leaving chapel
    if (roomKey === 'CHAPEL') {
        playMusic('CHAPEL');
    } else if (previousRoom === 'CHAPEL') {
        // Leaving chapel, return to roam music
        playMusic('ROAM');
    }
    // Otherwise keep current music playing (ROAM continues between rooms)
    
    return true;
}
// --- MOVEMENT LOGIC ---
function tryMove(dx, dy) {
    if (player.isMoving) return;
    
    const nextX = player.gridX + dx;
    const nextY = player.gridY + dy;
    if (nextX < 0 || nextX >= COLS || nextY < 0 || nextY >= ROWS) return;
    const tile = activeMap[nextY][nextX];
    if (tile === 1) return; // Wall
    // Furniture Blocking (3=Table, 4=Chair, 5=Plant, 6=Altar) - Treat as walls
    if (tile >= 3 && tile <= 6) return; 
    // Check Encounter on target tile BEFORE moving
    for(let i=0; i<activeMinions.length; i++) {
        let m = activeMinions[i];
        if (m.active && m.gridX === nextX && m.gridY === nextY) {
            startBattle('minion', i);
            return; // Cancel move, start battle
        }
    }
    if (activeBoss && activeBoss.active && activeBoss.gridX === nextX && activeBoss.gridY === nextY) {
        startBattle('boss', -1);
        return;
    }
    // Check Door
    for (let door of activeRoom.doors) {
        if (door.x === nextX && door.y === nextY) {
            if(!switchRoom(door.target, door.targetX, door.targetY)) {
                // Lock message handled in switchRoom
            }
            return; 
        }
    }
    for(let npc of activeNPCs) {
        if (npc.gridX === nextX && npc.gridY === nextY) return;
    }
    player.gridX = nextX;
    player.gridY = nextY;
    player.targetX = nextX * TILE_SIZE;
    player.targetY = nextY * TILE_SIZE;
    player.isMoving = true;
    player.bobFrame = 0;
    
    if (dx > 0) player.facingRight = true;
    if (dx < 0) player.facingRight = false;
}
function update() {
    frames++;
    if (currentState === STATE.INTRO) {
        if (keys[" "] && !keyProcessed[" "]) { 
            keyProcessed[" "] = true;
            currentState = STATE.ROAM; 
            player.interactionCooldown = 20; 
            document.getElementById('intro-screen').style.display = 'none'; 
            
            // TRIGGER CUTSCENE
            if (!introCutsceneFinished) introCutsceneActive = true;
        }
        return;
    }
    if (currentState === STATE.TRANSITION) {
        transitionTimer--;
        if (transitionTimer <= 0) {
            currentState = STATE.BATTLE;
            // Small delay to let encounter alarm finish
            setTimeout(() => {
                playMusic('BATTLE');
            }, 100);
        }
        return;
    }
    // Update Win Timer
    if (currentState === STATE.WIN) {
        winTimer++;
    }

    if (currentState === STATE.ROAM) {
        if (player.interactionCooldown > 0) player.interactionCooldown--;
        if (player.autoInteractCooldown > 0) player.autoInteractCooldown--;
        
        // 1. Handle Crowd Smooth Movement
        activeCrowd.forEach(p => {
            if (p.static) return; // Static students don't move

            // Move towards target if moving
            if (p.isMoving) {
                const speed = 2; // Slower than player
                const dx = p.targetPixelX - p.pixelX;
                const dy = p.targetPixelY - p.pixelY;

                if (Math.abs(dx) <= speed && Math.abs(dy) <= speed) {
                    p.pixelX = p.targetPixelX;
                    p.pixelY = p.targetPixelY;
                    p.isMoving = false;
                } else {
                    p.pixelX += Math.sign(dx) * speed;
                    p.pixelY += Math.sign(dy) * speed;
                }
            } 
            // Decide new move if not moving
            else if (Math.random() < 0.02) { 
                const dir = Math.floor(Math.random() * 4);
                let dx = 0, dy = 0;
                if (dir===0) dy=-1; else if(dir===1) dy=1; else if(dir===2) dx=-1; else dx=1;
                
                const nx = p.gridX + dx;
                const ny = p.gridY + dy;
                
                // Collision checks
                if (nx >= 0 && nx < COLS && ny >= 0 && ny < ROWS) {
                    if (activeMap[ny][nx] === 0 && !(nx===player.gridX && ny===player.gridY)) {
                         let hitNPC = activeNPCs.some(n => n.gridX === nx && n.gridY === ny);
                         let hitCrowd = activeCrowd.some(c => c !== p && c.gridX === nx && c.gridY === ny);
                         
                         if (!hitNPC && !hitCrowd) {
                             p.gridX = nx;
                             p.gridY = ny;
                             p.targetPixelX = nx * TILE_SIZE;
                             p.targetPixelY = ny * TILE_SIZE;
                             p.isMoving = true;
                             p.facingRight = dx > 0; 
                         }
                    }
                }
            }
        });

        // 2. Handle NPC (Ms. O'Neill) Smooth Movement
        activeNPCs.forEach(n => {
            // ONLY move Ms. O'Neill (spriteKey: 'oneill_strict') or Mrs Grant during cutscene
            if (n.spriteKey !== 'oneill_strict' && n.id !== 'grant_final') return;

            // Move towards target if moving
            if (n.isMoving) {
                const speed = 2;
                const dx = n.targetPixelX - n.pixelX;
                const dy = n.targetPixelY - n.pixelY;

                if (Math.abs(dx) <= speed && Math.abs(dy) <= speed) {
                    n.pixelX = n.targetPixelX;
                    n.pixelY = n.targetPixelY;
                    n.isMoving = false;
                } else {
                    n.pixelX += Math.sign(dx) * speed;
                    n.pixelY += Math.sign(dy) * speed;
                }
            } 
            // Decide new move if not moving (Slightly more aggressive patrol than students)
            // Only apply to O'Neill, Grant is controlled by cutscene logic below
            else if (n.spriteKey === 'oneill_strict' && Math.random() < 0.03) { 
                const dir = Math.floor(Math.random() * 4);
                let dx = 0, dy = 0;
                if (dir===0) dy=-1; else if(dir===1) dy=1; else if(dir===2) dx=-1; else dx=1;
                
                const nx = n.gridX + dx;
                const ny = n.gridY + dy;
                
                // Collision checks
                if (nx >= 0 && nx < COLS && ny >= 0 && ny < ROWS) {
                    // Basic wall/furniture check
                    const tile = activeMap[ny][nx];
                    // Don't walk into walls(1) or furniture(3,4,5,6)
                    if (tile !== 1 && (tile < 3 || tile > 6)) {
                         // Don't walk into player (that feels unfair, let player walk into her)
                         if (!(nx === player.gridX && ny === player.gridY)) {
                             // Check other NPCs
                             let hitNPC = activeNPCs.some(other => other !== n && other.gridX === nx && other.gridY === ny);
                             // Check Crowd
                             let hitCrowd = activeCrowd.some(c => c.gridX === nx && c.gridY === ny);
                             
                             if (!hitNPC && !hitCrowd) {
                                 n.gridX = nx;
                                 n.gridY = ny;
                                 n.targetPixelX = nx * TILE_SIZE;
                                 n.targetPixelY = ny * TILE_SIZE;
                                 n.isMoving = true;
                                 // Doesn't need facingRight update as sprites are front-facing mostly, but can add if needed
                             }
                         }
                    }
                }
            }
        });

        // --- INTRO CUTSCENE LOGIC ---
        if (introCutsceneActive) {
            if (!player.isMoving) {
                // Move Up until y=4
                if (player.gridY > 4) {
                    tryMove(0, -1);
                } else {
                    // Arrived
                    introCutsceneActive = false;
                    introCutsceneFinished = true;
                    player.facingRight = true;
                    const npc = activeNPCs.find(n => n.id === 'mcmahon_intro');
                    if(npc) {
                        player.interactionCooldown = 0; 
                        startDialogue(npc);
                    }
                }
            }
        } 
        // --- NEW: OFFICE CUTSCENE LOGIC ---
        else if (officeCutsceneActive) {
            // Find Mrs Grant
            const grant = activeNPCs.find(n => n.id === 'grant_final');
            if (grant) {
                // Run towards player until close (gridX 2 or 3)
                // Player is likely at gridX 1 after entering
                const targetDistance = 2; 
                
                // Calculate pixel distance
                const dist = Math.abs(grant.gridX - player.gridX);
                
                if (dist > targetDistance) {
                    // Move Grant smoothly
                    if (!grant.isMoving) {
                        grant.gridX -= 1; // Move left
                        grant.targetPixelX = grant.gridX * TILE_SIZE;
                        grant.isMoving = true;
                        grant.facingRight = false;
                    }
                } else if (!grant.isMoving) {
                    // Arrived at player
                    officeCutsceneActive = false;
                    officeCutscenePlayed = true;
                    player.interactionCooldown = 0;
                    startDialogue({
                        name: grant.name,
                        role: grant.role,
                        color: grant.color,
                        dialogue: [
                            "Thank you for unlocking the door.",
                            "The bugs have been terrible.",
                            "I know you will know the answers to defeat the glitch.",
                            "I believe in you!"
                        ]
                    });
                }
            } else {
                // Fallback if she's missing for some reason
                officeCutsceneActive = false;
            }
        }
        // Normal Auto-Interact Logic (only if not in cutscene)
        else if (player.autoInteractCooldown === 0 && !player.isMoving) {
            const adjacentPositions = [
                {x: player.gridX, y: player.gridY - 1}, {x: player.gridX, y: player.gridY + 1},
                {x: player.gridX - 1, y: player.gridY}, {x: player.gridX + 1, y: player.gridY},
                {x: player.gridX, y: player.gridY} // Same tile
            ];
            
            for (let pos of adjacentPositions) {
                for (let npc of activeNPCs) {
                    if (npc.autoInteract && npc.gridX === pos.x && npc.gridY === pos.y) {
                        // Trigger auto-interaction
                        const randomMessage = npc.messages[Math.floor(Math.random() * npc.messages.length)];
                        player.hp -= npc.damage;
                        playSound('ALERT');
                        
                        // Check for game over
                        if (player.hp <= 0) {
                            loseGame("Caught by Mrs O'Neill!");
                            return;
                        }
                        
                        startDialogue({
                            name: npc.name,
                            role: npc.role,
                            color: npc.color,
                            dialogue: [randomMessage, `[-${npc.damage} HP]`]
                        });
                        player.autoInteractCooldown = 180; // 3 seconds at 60fps
                        break;
                    }
                }
            }
        }
        // MOVEMENT ANIMATION (Applies to both cutscene and manual movement)
        if (player.isMoving) {
            const speed = 4; 
            const dx = player.targetX - player.x;
            const dy = player.targetY - player.y;
            
            if (Math.abs(dx) <= speed && Math.abs(dy) <= speed) {
                player.x = player.targetX;
                player.y = player.targetY;
                player.isMoving = false;
            } else {
                player.x += Math.sign(dx) * speed;
                player.y += Math.sign(dy) * speed;
                player.bobFrame += 0.2;
            }
        } 
        // MANUAL INPUT (Only if not moving and not cutscene)
        else if (!introCutsceneActive && !officeCutsceneActive) {
            if (keys.ArrowUp) tryMove(0, -1);
            else if (keys.ArrowDown) tryMove(0, 1);
            else if (keys.ArrowLeft) tryMove(-1, 0);
            else if (keys.ArrowRight) tryMove(1, 0);
        }
        // INTERACTION KEY (Only if not cutscene)
        if (keys[" "] && !keyProcessed[" "] && !player.isMoving && player.interactionCooldown === 0 && !introCutsceneActive && !officeCutsceneActive) {
            keyProcessed[" "] = true;
            let interact = false;
            const adjacentPositions = [
                {x: player.gridX, y: player.gridY - 1}, {x: player.gridX, y: player.gridY + 1},
                {x: player.gridX - 1, y: player.gridY}, {x: player.gridX + 1, y: player.gridY}
            ];
            
            for (let pos of adjacentPositions) {
                for (let npc of activeNPCs) {
                    if (npc.gridX === pos.x && npc.gridY === pos.y) {
                        if (npc.heal) player.hp = player.maxHp;
                        startDialogue(npc);
                        interact = true;
                        break;
                    }
                }
                if (interact) break;
            }
        }
    }
    if (currentState === STATE.DIALOGUE) {
        if (keys[" "] && !keyProcessed[" "] && player.interactionCooldown === 0) { 
            keyProcessed[" "] = true;
            advanceDialogue(); 
        }
        if (player.interactionCooldown > 0) player.interactionCooldown--;
    }
    if (currentState === STATE.BATTLE) updateBattle();
}
let dialogueQueue = []; let dialogueSpeaker = "";
function startDialogue(npc) {
    if (player.interactionCooldown > 0) return;
    playSound('SELECT');
    dialogueQueue = [...npc.dialogue];
    if (npc.heal) dialogueQueue.push("[HP RESTORED]");
    
    dialogueSpeaker = npc.name;
    currentState = STATE.DIALOGUE;
    document.getElementById('dialogue-box').style.display = 'block';
    document.getElementById('dialogue-name').innerText = dialogueSpeaker;
    document.getElementById('dialogue-text').innerText = dialogueQueue[0];
    player.interactionCooldown = 15;
}
function advanceDialogue() {
    dialogueQueue.shift();
    if (dialogueQueue.length === 0) { currentState = STATE.ROAM; document.getElementById('dialogue-box').style.display = 'none'; player.interactionCooldown = 20; }
    else { document.getElementById('dialogue-text').innerText = dialogueQueue[0]; player.interactionCooldown = 15; }
}
function startBattle(type, index) {
    playEncounterSfx(); // Play encounter alarm!
    currentState = STATE.TRANSITION; // Wipe effect first
    transitionTimer = 90; // frames (increased for longer siren)
    battleState = 'MENU';
    battleTurn = 'PLAYER';
    battleMenuIdx = 0;
    initMatrixRain();
    player.interactionCooldown = 20;
    if (type === 'minion') {
        activeBattleEnemy = { type: 'minion', name: 'MINOR BUG', hp: 50, maxHp: 50, spriteKey: 'bug', minionIndex: index, lvl: 5 };
        battleMsg = "A wild BUG appeared!";
    } else {
        activeBattleEnemy = { type: 'boss', name: 'THE GLITCH', hp: 200, maxHp: 200, spriteKey: 'glitch', minionIndex: -1, lvl: 50 };
        battleMsg = "THE GLITCH wants to battle!";
    }
}
function updateBattle() {
    if (battleShake > 0) battleShake *= 0.9; if (battleShake < 0.5) battleShake = 0;
    for (let i = battleEffects.length - 1; i >= 0; i--) {
        let p = battleEffects[i]; p.x += p.vx; p.y += p.vy; p.life--;
        if (p.life <= 0) battleEffects.splice(i, 1);
    }
    
    if (battleState === 'FAINT_ANIM') {
       return; 
    }
    if (battleState === 'MENU') {
        if (player.interactionCooldown > 0) player.interactionCooldown--;
        // Use keyProcessed check for menu navigation to prevent rapid firing
        if (keys.ArrowUp && !keyProcessed.ArrowUp && player.interactionCooldown === 0) { 
            keyProcessed.ArrowUp = true;
            battleMenuIdx = Math.max(0, battleMenuIdx - 1); 
            player.interactionCooldown = 5; 
            playSound('SELECT'); 
        }
        if (keys.ArrowDown && !keyProcessed.ArrowDown && player.interactionCooldown === 0) { 
            keyProcessed.ArrowDown = true;
            battleMenuIdx = Math.min(2, battleMenuIdx + 1); 
            player.interactionCooldown = 5; 
            playSound('SELECT'); 
        }
        if (keys[" "] && !keyProcessed[" "] && player.interactionCooldown === 0) { 
            keyProcessed[" "] = true;
            player.interactionCooldown = 20; 
            selectBattleAction(battleMenuIdx); 
        }
    } else if (battleState === 'QUESTION') {
        if (player.interactionCooldown > 0) player.interactionCooldown--;
        if (keys.ArrowUp && !keyProcessed.ArrowUp && player.interactionCooldown === 0) { 
            keyProcessed.ArrowUp = true;
            selectedOptionIdx = Math.max(0, selectedOptionIdx - 1); 
            player.interactionCooldown = 5; 
            playSound('SELECT'); 
        }
        if (keys.ArrowDown && !keyProcessed.ArrowDown && player.interactionCooldown === 0) { 
            keyProcessed.ArrowDown = true;
            selectedOptionIdx = Math.min(2, selectedOptionIdx + 1); 
            player.interactionCooldown = 5; 
            playSound('SELECT'); 
        }
        if (keys[" "] && !keyProcessed[" "] && player.interactionCooldown === 0) { 
            keyProcessed[" "] = true;
            player.interactionCooldown = 20; 
            checkAnswer(); 
        }
    }
    
    if (battleState === 'VICTORY_WAIT') {
        if (keys[" "] && !keyProcessed[" "] && player.interactionCooldown === 0) {
             keyProcessed[" "] = true;
             player.hp = Math.min(player.maxHp, player.hp + 10); 
             if (activeBattleEnemy.type === 'minion') {
                activeMinions[activeBattleEnemy.minionIndex].active = false;
                currentState = STATE.ROAM; 
                player.interactionCooldown = 30; 
                // Only play chapel music if in chapel, otherwise return to roam
                if (player.currentRoom === 'CHAPEL') playMusic('CHAPEL');
                else playMusic('ROAM');
            } else winGame();
        }
        if (player.interactionCooldown > 0) player.interactionCooldown--;
    }
}
function selectBattleAction(idx) {
    if (idx === 1) { 
        pendingAction = 'AI'; 
        battleMsg = "Used AI Shortcut..."; 
        battleState = 'BUSY'; // LOCK INPUT
        setTimeout(executeAction, 1000); 
    } else if (idx === 2) { // RUN
        battleMsg = "Got away safely!";
        battleState = 'BUSY';
        setTimeout(() => {
             currentState = STATE.ROAM;
             player.interactionCooldown = 30;
             // Only play chapel music if in chapel, otherwise return to roam
             if (player.currentRoom === 'CHAPEL') playMusic('CHAPEL');
             else playMusic('ROAM');
        }, 1000);
    } else {
        // idx 0 (QUESTION)
        pendingAction = 'DRAFT';
        currentQuestion = getNextQuestion(); // Use the pool system instead of raw random
        selectedOptionIdx = 0;
        battleState = 'QUESTION';
    }
}
function checkAnswer() {
    const isCorrect = selectedOptionIdx === currentQuestion.correct;
    if (isCorrect) { 
        battleMsg = "It's super effective!"; 
        playSound('CORRECT'); 
        battleState = 'BUSY'; // LOCK INPUT
        setTimeout(executeAction, 1000); 
    } else {
        battleMsg = "It wasn't very effective..."; 
        playSound('WRONG');
        battleState = 'ANIMATION';
        setTimeout(() => {
            player.hp -= 20; battleShake = 20;
            battleEffects.push({x: 150, y: 300, vx:0, vy:-2, life:60, type:'text', text:'-20', color:'#f44'});
            if(player.hp <= 0) loseGame("You blacked out!"); else endPlayerTurn();
        }, 1000);
    }
}
function executeAction() {
    battleState = 'ANIMATION';
    let dmg = 0;
    if (pendingAction === 'DRAFT') {
        dmg = 30 + Math.floor(Math.random()*10);
        battleMsg = "Player used CRITICAL THINKING!";
        battleEffects.push({x: 200, y: 350, targetX: 550, targetY: 150, vx: 10, vy: -5, life: 40, type: 'projectile', icon: ' 📄 '});
        setTimeout(() => hitEnemy(dmg), 500);
    } else if (pendingAction === 'AI') {
        dmg = 60; player.auth -= 30;
        battleMsg = "INCORRECT INFO! AI HALLUCINATED!";
        battleEffects.push({x: 200, y: 350, targetX: 550, targetY: 150, vx: 10, vy: -5, life: 40, type: 'projectile', icon: ' 🤖 '});
        setTimeout(() => {
             player.hp -= 10;
             battleEffects.push({x: 150, y: 300, vx:0, vy:-2, life:60, type:'text', text:'-10', color:'#f44'});
             hitEnemy(dmg);
        }, 500);
    }
}
function hitEnemy(dmg) {
    activeBattleEnemy.hp -= dmg;
    battleEffects.push({x: 550, y: 100, vx:0, vy:-2, life:60, type:'text', text:dmg, color:'#fff'});
    battleShake = 10; playSound('HIT');
    
    if (activeBattleEnemy.hp <= 0) {
        playEnemyDownSfx(); 
        battleState = 'FAINT_ANIM';
        setTimeout(() => {
            stopAllMusic(); // Stop battle music
            playVictoryFanfare(); // Celebration fanfare
            battleMsg = `${activeBattleEnemy.name} was destroyed!`;
            // Start victory music after fanfare finishes
            setTimeout(() => {
                playMusic('WIN'); // Start victory music loop
            }, 1200); // Wait for fanfare to play
            setTimeout(() => {
                battleMsg = "You gained 50 EXP & HP!";
                playSound('CORRECT');
                battleState = 'VICTORY_WAIT';
                player.interactionCooldown = 20;
            }, 1500);
        }, 1000);
    } else if (player.auth <= 0) loseGame("Disqualified for Malpractice!");
    else setTimeout(endPlayerTurn, 1000);
}
function endPlayerTurn() {
    battleState = 'ENEMY_TURN';
    battleMsg = `${activeBattleEnemy.name} used HALLUCINATION!`;
    setTimeout(enemyAttack, 1500);
}
function enemyAttack() {
    let dmg = 10 + Math.floor(Math.random()*10);
    if (activeBattleEnemy.type === 'minion') dmg = 5;
    battleEffects.push({x: 550, y: 150, targetX: 200, targetY: 350, vx: -10, vy: 5, life: 40, type: 'projectile', spriteKey: 'bug'});
    setTimeout(() => {
        player.hp -= dmg; playSound('HIT');
        battleEffects.push({x: 150, y: 300, vx:0, vy:-2, life:60, type:'text', text:`-${dmg}`, color:'#f44'});
        battleShake = 10;
        if (player.hp <= 0) loseGame("You blacked out!");
        else { battleState = 'MENU'; battleMsg = "What will PLAYER do?"; player.interactionCooldown = 10; }
    }, 500);
}
function winGame() { 
    // Mark boss as defeated in the map data (not just local reference)
    if (MAP_LAYOUTS['OFFICE'].boss) {
        MAP_LAYOUTS['OFFICE'].boss.active = false;
    }
    if (activeBoss) {
        activeBoss.active = false;
    }
    currentState = STATE.WIN; 
    winTimer = 0; // Reset timer
    playMusic('WIN'); 
}
function loseGame(reason) { currentState = STATE.GAMEOVER; battleMsg = reason; playMusic('NONE'); }
function draw() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    
    if (currentState === STATE.TRANSITION) {
        drawMapScreen();
        const p = 1 - (transitionTimer / 90); 
        const shutterHeight = (canvas.height / 2) * p;
        ctx.fillStyle = '#000';
        ctx.fillRect(0, 0, canvas.width, shutterHeight); 
        ctx.fillRect(0, canvas.height - shutterHeight, canvas.width, shutterHeight); 
        if (transitionTimer % 4 < 2) {
            ctx.fillStyle = 'rgba(255, 255, 255, 0.5)';
            ctx.fillRect(0, 0, canvas.width, canvas.height);
        }
        return;
    }
    if (currentState === STATE.BATTLE) { drawBattle(); return; }
    if (currentState === STATE.WIN || currentState === STATE.GAMEOVER) { drawEndScreen(); return; }
    drawMapScreen();
}
function drawMapScreen() {
    ctx.fillStyle = activeRoom.color || COLORS.floor;
    ctx.fillRect(0, 0, canvas.width, canvas.height);
    
    for (let y = 0; y < ROWS; y++) {
        for (let x = 0; x < COLS; x++) {
            const tile = activeMap[y][x];
            if (tile === 1) {
                ctx.fillStyle = COLORS.wall;
                ctx.fillRect(x * TILE_SIZE, y * TILE_SIZE, TILE_SIZE, TILE_SIZE);
                ctx.strokeStyle = '#222';
                ctx.strokeRect(x * TILE_SIZE, y * TILE_SIZE, TILE_SIZE, TILE_SIZE);
            } else if (tile === 2) { // Door
                drawSprite(ctx, 'door', x*TILE_SIZE, y*TILE_SIZE, TILE_SIZE, true);
            } else if (tile === 3) { // Table
                drawSprite(ctx, 'table', x*TILE_SIZE, y*TILE_SIZE, TILE_SIZE, true);
            } else if (tile === 4) { // Chair
                drawSprite(ctx, 'chair', x*TILE_SIZE, y*TILE_SIZE, TILE_SIZE, true);
            } else if (tile === 5) { // Plant
                drawSprite(ctx, 'plant', x*TILE_SIZE, y*TILE_SIZE, TILE_SIZE, true);
            } else if (tile === 6) { // Altar/Counter (Using door sprite tinted or just as is for now, or specialized if we add one)
                // Reusing table for now or door if generic
                drawSprite(ctx, 'table', x*TILE_SIZE, y*TILE_SIZE, TILE_SIZE, true);
            }
        }
    }
    ctx.textAlign = 'center';
    
    // Draw Crowd
    activeCrowd.forEach(c => {
         // Use pixel coordinates if available (initialized in switchRoom), else fallback
         const drawX = (c.pixelX !== undefined) ? c.pixelX : c.gridX * TILE_SIZE;
         const drawY = (c.pixelY !== undefined) ? c.pixelY : c.gridY * TILE_SIZE;
         
         // Add bobbing effect if moving
         const bob = c.isMoving ? (frames / 5) : 0; 
         
         drawSprite(ctx, c.spriteKey, drawX, drawY, TILE_SIZE, c.facingRight, bob);
    });
    activeMinions.forEach(m => { 
        if(m.active) drawSprite(ctx, m.spriteKey, m.gridX * TILE_SIZE, m.gridY * TILE_SIZE, TILE_SIZE, true); 
    });
    
    activeNPCs.forEach(npc => {
        // Use pixel coordinates if available (initialized in switchRoom), else fallback
        const drawX = (npc.pixelX !== undefined) ? npc.pixelX : npc.gridX * TILE_SIZE;
        const drawY = (npc.pixelY !== undefined) ? npc.pixelY : npc.gridY * TILE_SIZE;
        
        // Add bobbing effect if moving
        const bob = npc.isMoving ? (frames / 5) : 0; 
        
        drawSprite(ctx, npc.spriteKey, drawX, drawY, TILE_SIZE, false, bob);
        
        // Draw exclamation mark if boss is defeated
        if (npc.id === 'grant_final' && activeBoss && !activeBoss.active) {
           drawSprite(ctx, 'alert', npc.gridX * TILE_SIZE, (npc.gridY - 1) * TILE_SIZE, TILE_SIZE, false);
        }
    });
    if (activeBoss && activeBoss.active) { 
        drawSprite(ctx, activeBoss.spriteKey, activeBoss.gridX * TILE_SIZE, activeBoss.gridY * TILE_SIZE, 50, false); 
    }
    drawSprite(ctx, player.spriteKey, player.x, player.y, TILE_SIZE, player.facingRight, player.isMoving ? player.bobFrame : 0);
    ctx.fillStyle = '#fff'; ctx.textAlign = 'left'; ctx.font = '12px "Press Start 2P"';
    ctx.fillText(`HP: ${player.hp}`, 10, 20); 
}
function drawBattle() {
    ctx.save();
    if (battleShake > 0) ctx.translate((Math.random()-0.5)*battleShake, (Math.random()-0.5)*battleShake);
    // Background
    ctx.fillStyle = '#f8f8f8'; ctx.fillRect(0,0,800,600); // Light BG
    ctx.fillStyle = '#d0e0f0'; ctx.beginPath(); ctx.moveTo(0,600); ctx.lineTo(800,600); ctx.lineTo(800,300); ctx.lineTo(0,450); ctx.fill(); // Ground
    // Platforms
    ctx.fillStyle = '#c0c0c0'; 
    ctx.beginPath(); ctx.ellipse(580, 200, 120, 40, 0, 0, Math.PI*2); ctx.fill(); // Enemy Base
    ctx.beginPath(); ctx.ellipse(200, 450, 120, 40, 0, 0, Math.PI*2); ctx.fill(); // Player Base
    // Sprites
    
    // Player
    drawSprite(ctx, player.spriteKey, 140, 370, 128, true);
    // Enemy - Handle Fainting Logic
    let enemyY = 120;
    let enemyOpacity = 1.0;
    
    if (battleState === 'FAINT_ANIM' || battleState === 'VICTORY_WAIT') {
        enemyY += 50; 
        enemyOpacity = 0; 
    }
    
    if (battleState !== 'VICTORY_WAIT') { 
       if (activeBattleEnemy.hp > 0) {
           drawSprite(ctx, activeBattleEnemy.spriteKey, 520, 120, 128, false);
       }
    }
    if (activeBattleEnemy.hp > 0) {
        drawHealthBox(50, 50, activeBattleEnemy.name, activeBattleEnemy.lvl, activeBattleEnemy.hp, activeBattleEnemy.maxHp, false);
    }
    
    drawHealthBox(450, 350, "PLAYER", 13, player.hp, player.maxHp, true);
    battleEffects.forEach(p => {
        if (p.type === 'projectile') { 
            if (p.spriteKey) {
                // Draw sprite projectile
                drawSprite(ctx, p.spriteKey, p.x, p.y, 40, true);
            } else {
                // Draw icon projectile
                ctx.font='40px Arial'; 
                ctx.fillText(p.icon, p.x, p.y); 
            }
        }
        else { ctx.font='20px "Press Start 2P"'; ctx.fillStyle=p.color; ctx.fillText(p.text, p.x, p.y); }
    });
    // UI
    ctx.fillStyle = '#222'; ctx.fillRect(0, 480, 800, 120);
    ctx.fillStyle = '#fff'; ctx.lineWidth = 4; ctx.strokeStyle = '#666'; ctx.strokeRect(10, 490, 780, 100); ctx.fillRect(10, 490, 780, 100);
    ctx.fillStyle = '#000'; ctx.textAlign = 'left'; ctx.font = '14px "Press Start 2P"';
    if (battleState === 'MENU') {
        // Dynamic Left Box Text based on Selection
        let desc = "";
        if (battleMenuIdx === 0) desc = "QUESTION: Answer JCQ quiz.";
        else if (battleMenuIdx === 1) desc = "GEN-AI: Negative use (Risky)";
        else if (battleMenuIdx === 2) desc = "RUN: Escape battle.";
        ctx.fillStyle = '#000'; 
        wrapText(ctx, desc, 35, 535, 350, 20); // Wrapped description
        // Menu Box
        ctx.fillStyle = '#fff'; ctx.strokeStyle = '#000'; ctx.fillRect(400, 490, 390, 100); ctx.strokeRect(400, 490, 390, 100);
        ctx.fillStyle = '#000';
        // Modified Menu Options per Request
        // 0: QUESTION, 1: GEN-AI, 2: RUN
        const opts = ["QUESTION", "GEN-AI", "RUN"];
        ctx.fillText((battleMenuIdx===0?">":" ")+opts[0], 420, 530);
        ctx.fillText((battleMenuIdx===1?">":" ")+opts[1], 620, 530);
        ctx.fillText((battleMenuIdx===2?">":" ")+opts[2], 420, 560);
    } else if (battleState === 'QUESTION') {
        ctx.font = '12px "Press Start 2P"';
        ctx.fillStyle = '#000';
        // Use wrapText for questions too!
        wrapText(ctx, currentQuestion.q, 30, 505, 740, 18);
        
        currentQuestion.options.forEach((o, i) => {
            ctx.fillStyle = i === selectedOptionIdx ? '#d00' : '#000';
            // Ensure options don't clip if wrapping pushes them down (simplified vertical stack)
            let yPos = 545 + (i*20);
            ctx.fillText((i===selectedOptionIdx?"> ":"  ")+o, 30, yPos);
        });
    } else {
        ctx.fillStyle = '#000';
        wrapText(ctx, battleMsg, 35, 535, 740, 20);
        if (battleState === 'VICTORY_WAIT') {
             ctx.fillStyle = '#d00'; 
             ctx.fillText("[PRESS SPACE TO CONTINUE]", 450, 570);
        }
    }
    ctx.restore();
}
function drawHealthBox(x, y, name, lvl, hp, maxHp, showNumbers) {
    // Box Body
    ctx.fillStyle = '#fff'; ctx.strokeStyle='#000'; ctx.lineWidth=3;
    ctx.fillRect(x, y, 300, 80); ctx.strokeRect(x, y, 300, 80);
    
    // Text
    ctx.fillStyle = '#000'; ctx.font = '14px "Press Start 2P"'; ctx.textAlign = 'left';
    ctx.fillText(name, x + 10, y + 30);
    ctx.fillText("Lv" + lvl, x + 220, y + 30);
    // HP Bar
    ctx.fillStyle = '#555'; ctx.fillRect(x + 60, y + 45, 200, 15); // Back
    const pct = Math.max(0, hp / maxHp);
    ctx.fillStyle = pct > 0.5 ? '#4f4' : (pct > 0.2 ? '#fd0' : '#f44');
    ctx.fillRect(x + 60, y + 45, 200 * pct, 15); // Front
    
    ctx.fillStyle = '#000'; ctx.font = '10px "Press Start 2P"'; ctx.fillText("HP", x + 30, y + 57);
    
    if (showNumbers) {
        ctx.fillText(`${Math.floor(hp)}/ ${maxHp}`, x + 150, y + 70);
    }
}
function drawEndScreen() {
    ctx.fillStyle = currentState === STATE.WIN ? '#000' : '#200'; ctx.fillRect(0,0,800,600);
    ctx.textAlign = 'center'; 
    
    if (currentState === STATE.WIN) {
        ctx.font = '30px "Press Start 2P"';
        ctx.fillStyle = '#44ff44';
        ctx.fillText("INTEGRITY RESTORED!", 400, 60);

        ctx.font = '14px "Press Start 2P"';
        ctx.fillStyle = '#ffffff';
        ctx.fillText("Great job! You have purged the glitches.", 400, 110);
        
        ctx.fillStyle = '#f0db4f';
        ctx.fillText("REMEMBER THE AI CODE:", 400, 160);
        
        ctx.textAlign = 'left';
        ctx.fillStyle = '#ffffff';
        ctx.fillText("1. AUTHENTICITY: Your work must be your own.", 80, 210);
        ctx.fillText("2. TRANSPARENCY: Reference AI tools used.", 80, 250);
        ctx.fillText("3. VERIFICATION: Check AI facts.", 80, 290);
        ctx.fillText("4. CONSEQUENCES: Misuse = Disqualification.", 80, 330);
        
        ctx.textAlign = 'center';
        ctx.fillStyle = '#cccccc';
        ctx.fillText("Use AI as a tool, not a replacement.", 400, 380); 
        
        ctx.fillStyle = '#ffffff';
        ctx.fillText("Press SPACE to Restart", 400, 560);

        // Mr Clinton Pop-up (10 seconds = 600 frames at 60fps)
        if (winTimer > 600) {
            // Draw Box
            ctx.fillStyle = '#333';
            ctx.strokeStyle = '#fff';
            ctx.lineWidth = 4;
            ctx.fillRect(150, 420, 500, 100);
            ctx.strokeRect(150, 420, 500, 100);
            
            // Draw Clinton
            drawSprite(ctx, 'clinton', 170, 440, 60, false);
            
            // Draw Text
            ctx.fillStyle = '#fff';
            ctx.textAlign = 'left';
            ctx.font = '12px "Press Start 2P"';
            ctx.fillText("Mr Clinton:", 250, 450);
            wrapText(ctx, "\"You did a really really brilliant job!\"", 250, 480, 380, 20);
        }

    } else {
        ctx.fillStyle = '#f44';
        ctx.font = '30px "Press Start 2P"';
        ctx.fillText("GAME OVER", 400, 250);
        ctx.fillStyle = '#fff'; ctx.font = '14px "Press Start 2P"';
        ctx.fillText(battleMsg, 400, 320);
        ctx.fillText("Press SPACE to restart.", 400, 450);
    }
}
window.addEventListener('keydown', e => { if ((currentState === STATE.WIN || currentState === STATE.GAMEOVER) && e.key === " ") location.reload(); });
function loop() { update(); draw(); requestAnimationFrame(loop); }
loop();
</script>
</body>
</html>
