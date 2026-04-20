
```html

html_content = '''<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Array Visualizer - Interactive</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background: #0a0a0a;
            color: #e0e0e0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            min-height: 100vh;
            overflow-x: hidden;
        }

        /* Animated background particles */
        .bg-particles {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 0;
        }

        .particle {
            position: absolute;
            width: 2px;
            height: 2px;
            background: rgba(0, 255, 255, 0.3);
            border-radius: 50%;
            animation: float 15s infinite;
        }

        @keyframes float {
            0%, 100% { transform: translateY(100vh) rotate(0deg); opacity: 0; }
            10% { opacity: 1; }
            90% { opacity: 1; }
            100% { transform: translateY(-10vh) rotate(720deg); opacity: 0; }
        }

        .container {
            position: relative;
            z-index: 1;
            max-width: 1400px;
            margin: 0 auto;
            padding: 20px;
        }

        header {
            text-align: center;
            padding: 40px 0;
            margin-bottom: 30px;
        }

        h1 {
            font-size: 3em;
            background: linear-gradient(135deg, #00ffff, #ff00ff, #ffff00);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            animation: gradientShift 5s ease infinite;
            text-shadow: 0 0 30px rgba(0, 255, 255, 0.3);
        }

        @keyframes gradientShift {
            0%, 100% { filter: hue-rotate(0deg); }
            50% { filter: hue-rotate(180deg); }
        }

        .subtitle {
            color: #888;
            font-size: 1.2em;
            margin-top: 10px;
        }

        .controls-section {
            background: rgba(20, 20, 30, 0.8);
            border: 1px solid rgba(255, 255, 255, 0.1);
            border-radius: 16px;
            padding: 25px;
            margin-bottom: 30px;
            backdrop-filter: blur(10px);
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.4);
        }

        .control-group {
            display: flex;
            gap: 15px;
            align-items: center;
            flex-wrap: wrap;
            margin-bottom: 15px;
        }

        .control-group:last-child {
            margin-bottom: 0;
        }

        label {
            color: #aaa;
            font-weight: 600;
            min-width: 120px;
        }

        input[type="text"], input[type="number"], select {
            background: rgba(30, 30, 40, 0.9);
            border: 2px solid rgba(100, 100, 120, 0.3);
            color: #fff;
            padding: 12px 16px;
            border-radius: 8px;
            font-size: 16px;
            transition: all 0.3s ease;
            outline: none;
        }

        input[type="text"]:focus, input[type="number"]:focus, select:focus {
            border-color: #00ffff;
            box-shadow: 0 0 15px rgba(0, 255, 255, 0.2);
        }

        input[type="text"].error {
            border-color: #ff4444;
            animation: shake 0.5s ease;
        }

        @keyframes shake {
            0%, 100% { transform: translateX(0); }
            25% { transform: translateX(-10px); }
            75% { transform: translateX(10px); }
        }

        button {
            background: linear-gradient(135deg, #00a8ff, #0066ff);
            border: none;
            color: white;
            padding: 12px 24px;
            border-radius: 8px;
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
        }

        button:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 20px rgba(0, 168, 255, 0.4);
        }

        button:active {
            transform: translateY(0);
        }

        button.danger {
            background: linear-gradient(135deg, #ff4444, #cc0000);
        }

        button.danger:hover {
            box-shadow: 0 5px 20px rgba(255, 68, 68, 0.4);
        }

        button.success {
            background: linear-gradient(135deg, #00ff88, #00aa66);
        }

        button.success:hover {
            box-shadow: 0 5px 20px rgba(0, 255, 136, 0.4);
        }

        .array-container {
            background: rgba(20, 20, 30, 0.8);
            border: 1px solid rgba(255, 255, 255, 0.1);
            border-radius: 16px;
            padding: 30px;
            margin-bottom: 30px;
            backdrop-filter: blur(10px);
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.4);
        }

        .array-title {
            font-size: 1.5em;
            margin-bottom: 20px;
            color: #00ffff;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .array-title::before {
            content: '';
            width: 4px;
            height: 24px;
            background: linear-gradient(to bottom, #00ffff, #ff00ff);
            border-radius: 2px;
        }

        .array-1d {
            display: flex;
            gap: 0;
            justify-content: center;
            flex-wrap: wrap;
            margin: 20px 0;
        }

        .array-cell {
            position: relative;
            width: 80px;
            height: 80px;
            background: linear-gradient(135deg, rgba(40, 40, 60, 0.9), rgba(30, 30, 45, 0.9));
            border: 2px solid rgba(100, 100, 120, 0.3);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.2em;
            font-weight: bold;
            transition: all 0.3s ease;
            cursor: pointer;
        }

        .array-cell:first-child {
            border-radius: 12px 0 0 12px;
        }

        .array-cell:last-child {
            border-radius: 0 12px 12px 0;
        }

        .array-cell:only-child {
            border-radius: 12px;
        }

        .array-cell:hover {
            background: linear-gradient(135deg, rgba(60, 60, 90, 0.9), rgba(50, 50, 70, 0.9));
            transform: scale(1.05);
            z-index: 10;
            box-shadow: 0 0 20px rgba(0, 255, 255, 0.3);
        }

        .array-cell.highlighted {
            background: linear-gradient(135deg, rgba(255, 200, 0, 0.3), rgba(255, 150, 0, 0.3));
            border-color: #ffcc00;
            box-shadow: 0 0 30px rgba(255, 200, 0, 0.5);
            animation: pulse 1.5s ease infinite;
        }

        .array-cell.accessed {
            background: linear-gradient(135deg, rgba(0, 255, 136, 0.3), rgba(0, 200, 100, 0.3));
            border-color: #00ff88;
            box-shadow: 0 0 30px rgba(0, 255, 136, 0.5);
            animation: pulse 1.5s ease infinite;
        }

        .array-cell.error {
            background: linear-gradient(135deg, rgba(255, 68, 68, 0.3), rgba(200, 0, 0, 0.3));
            border-color: #ff4444;
            box-shadow: 0 0 30px rgba(255, 68, 68, 0.5);
            animation: shake 0.5s ease;
        }

        @keyframes pulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.05); }
        }

        .cell-index {
            position: absolute;
            bottom: -25px;
            left: 50%;
            transform: translateX(-50%);
            font-size: 0.75em;
            color: #888;
            font-weight: normal;
        }

        .cell-value {
            font-family: 'Courier New', monospace;
            color: #fff;
        }

        .array-2d {
            display: flex;
            flex-direction: column;
            gap: 4px;
            align-items: center;
            margin: 20px 0;
        }

        .array-row {
            display: flex;
            gap: 0;
        }

        .array-row .array-cell {
            border-radius: 0;
        }

        .array-row:first-child .array-cell:first-child {
            border-radius: 12px 0 0 0;
        }

        .array-row:first-child .array-cell:last-child {
            border-radius: 0 12px 0 0;
        }

        .array-row:last-child .array-cell:first-child {
            border-radius: 0 0 0 12px;
        }

        .array-row:last-child .array-cell:last-child {
            border-radius: 0 0 12px 0;
        }

        .array-row:only-child .array-cell:first-child {
            border-radius: 12px 0 0 12px;
        }

        .array-row:only-child .array-cell:last-child {
            border-radius: 0 12px 12px 0;
        }

        .cell-coords {
            position: absolute;
            top: -25px;
            left: 50%;
            transform: translateX(-50%);
            font-size: 0.65em;
            color: #666;
            font-weight: normal;
            white-space: nowrap;
        }

        .console-output {
            background: rgba(10, 10, 15, 0.9);
            border: 1px solid rgba(255, 255, 255, 0.1);
            border-radius: 12px;
            padding: 20px;
            margin-top: 20px;
            min-height: 100px;
            font-family: 'Courier New', monospace;
            font-size: 0.9em;
            max-height: 200px;
            overflow-y: auto;
        }

        .console-line {
            padding: 4px 0;
            border-left: 3px solid transparent;
            padding-left: 10px;
            margin: 2px 0;
            animation: fadeIn 0.3s ease;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateX(-10px); }
            to { opacity: 1; transform: translateX(0); }
        }

        .console-line.info { border-left-color: #00a8ff; color: #aaddff; }
        .console-line.success { border-left-color: #00ff88; color: #aaffcc; }
        .console-line.error { border-left-color: #ff4444; color: #ffaaaa; }
        .console-line.warning { border-left-color: #ffcc00; color: #ffeeaa; }

        .console-timestamp {
            color: #666;
            margin-right: 8px;
        }

        .tabs {
            display: flex;
            gap: 10px;
            margin-bottom: 20px;
        }

        .tab {
            padding: 10px 20px;
            background: rgba(40, 40, 60, 0.5);
            border: 2px solid rgba(100, 100, 120, 0.2);
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.3s ease;
            color: #aaa;
        }

        .tab.active {
            background: linear-gradient(135deg, rgba(0, 168, 255, 0.2), rgba(0, 102, 255, 0.2));
            border-color: #00a8ff;
            color: #fff;
        }

        .tab:hover:not(.active) {
            border-color: rgba(100, 100, 120, 0.5);
            color: #ddd;
        }

        .tab-content {
            display: none;
        }

        .tab-content.active {
            display: block;
            animation: fadeIn 0.5s ease;
        }

        .stats-bar {
            display: flex;
            gap: 20px;
            margin-bottom: 20px;
            flex-wrap: wrap;
        }

        .stat-item {
            background: rgba(30, 30, 45, 0.8);
            padding: 10px 20px;
            border-radius: 8px;
            border: 1px solid rgba(255, 255, 255, 0.1);
        }

        .stat-label {
            color: #888;
            font-size: 0.8em;
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        .stat-value {
            color: #00ffff;
            font-size: 1.2em;
            font-weight: bold;
            font-family: 'Courier New', monospace;
        }

        .toast {
            position: fixed;
            bottom: 30px;
            right: 30px;
            padding: 16px 24px;
            border-radius: 12px;
            color: white;
            font-weight: 600;
            z-index: 1000;
            animation: slideIn 0.3s ease, fadeOut 0.3s ease 2.7s;
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.1);
        }

        @keyframes slideIn {
            from { transform: translateX(100%); opacity: 0; }
            to { transform: translateX(0); opacity: 1; }
        }

        @keyframes fadeOut {
            from { opacity: 1; }
            to { opacity: 0; }
        }

        .toast.success { background: rgba(0, 200, 100, 0.9); }
        .toast.error { background: rgba(255, 68, 68, 0.9); }
        .toast.info { background: rgba(0, 168, 255, 0.9); }

        .divider {
            height: 1px;
            background: linear-gradient(to right, transparent, rgba(255, 255, 255, 0.2), transparent);
            margin: 20px 0;
        }

        .mode-toggle {
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .toggle-switch {
            position: relative;
            width: 50px;
            height: 26px;
            background: rgba(100, 100, 120, 0.3);
            border-radius: 13px;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .toggle-switch.active {
            background: linear-gradient(135deg, #00a8ff, #0066ff);
        }

        .toggle-switch::after {
            content: '';
            position: absolute;
            width: 22px;
            height: 22px;
            background: white;
            border-radius: 50%;
            top: 2px;
            left: 2px;
            transition: all 0.3s ease;
        }

        .toggle-switch.active::after {
            left: 26px;
        }

        @media (max-width: 768px) {
            h1 { font-size: 2em; }
            .array-cell { width: 60px; height: 60px; font-size: 1em; }
            .control-group { flex-direction: column; align-items: stretch; }
            label { min-width: auto; }
        }
    </style>
</head>
<body>
    <div class="bg-particles" id="particles"></div>
    
    <div class="container">
        <header>
            <h1>Array Visualizer</h1>
            <p class="subtitle">Interactive 1D & 2D Array Visualization Engine</p>
        </header>

        <div class="controls-section">
            <div class="tabs">
                <div class="tab active" onclick="switchTab('1d')">1D Array</div>
                <div class="tab" onclick="switchTab('2d')">2D Array</div>
            </div>

            <!-- 1D Array Controls -->
            <div id="tab-1d" class="tab-content active">
                <div class="control-group">
                    <label>Array Size:</label>
                    <input type="number" id="size-1d" value="8" min="1" max="20" placeholder="Size">
                    <button onclick="initArray1D()">Initialize</button>
                    <button class="danger" onclick="clearArray1D()">Clear</button>
                    <button class="success" onclick="randomizeArray1D()">Randomize</button>
                </div>
                <div class="control-group">
                    <label>Access Index:</label>
                    <input type="number" id="index-1d" placeholder="0-7" min="0">
                    <button onclick="accessIndex1D()">Access</button>
                </div>
                <div class="control-group">
                    <label>Assign Value:</label>
                    <input type="number" id="assign-index-1d" placeholder="Index" min="0">
                    <input type="text" id="assign-value-1d" placeholder="Value">
                    <button class="success" onclick="assignValue1D()">Assign</button>
                </div>
                <div class="stats-bar">
                    <div class="stat-item">
                        <div class="stat-label">Length</div>
                        <div class="stat-value" id="length-1d">8</div>
                    </div>
                    <div class="stat-item">
                        <div class="stat-label">Type</div>
                        <div class="stat-value">Int32[]</div>
                    </div>
                </div>
            </div>

            <!-- 2D Array Controls -->
            <div id="tab-2d" class="tab-content">
                <div class="control-group">
                    <label>Dimensions:</label>
                    <input type="number" id="rows-2d" value="4" min="1" max="10" placeholder="Rows">
                    <span style="color: #888;">×</span>
                    <input type="number" id="cols-2d" value="5" min="1" max="10" placeholder="Cols">
                    <button onclick="initArray2D()">Initialize</button>
                    <button class="danger" onclick="clearArray2D()">Clear</button>
                    <button class="success" onclick="randomizeArray2D()">Randomize</button>
                </div>
                <div class="control-group">
                    <label>Access Index:</label>
                    <input type="number" id="row-2d" placeholder="Row" min="0">
                    <input type="number" id="col-2d" placeholder="Col" min="0">
                    <button onclick="accessIndex2D()">Access</button>
                </div>
                <div class="control-group">
                    <label>Assign Value:</label>
                    <input type="number" id="assign-row-2d" placeholder="Row" min="0">
                    <input type="number" id="assign-col-2d" placeholder="Col" min="0">
                    <input type="text" id="assign-value-2d" placeholder="Value">
                    <button class="success" onclick="assignValue2D()">Assign</button>
                </div>
                <div class="stats-bar">
                    <div class="stat-item">
                        <div class="stat-label">Dimensions</div>
                        <div class="stat-value" id="dims-2d">4×5</div>
                    </div>
                    <div class="stat-item">
                        <div class="stat-label">Total</div>
                        <div class="stat-value" id="total-2d">20</div>
                    </div>
                </div>
            </div>
        </div>

        <!-- 1D Array Display -->
        <div id="display-1d" class="array-container">
            <div class="array-title">1D Array Visualization</div>
            <div class="array-1d" id="array-1d"></div>
            <div class="console-output" id="console-1d">
                <div class="console-line info">
                    <span class="console-timestamp">[00:00:00]</span>
                    Ready. Initialize an array to begin.
                </div>
            </div>
        </div>

        <!-- 2D Array Display -->
        <div id="display-2d" class="array-container" style="display: none;">
            <div class="array-title">2D Array Visualization</div>
            <div class="array-2d" id="array-2d"></div>
            <div class="console-output" id="console-2d">
                <div class="console-line info">
                    <span class="console-timestamp">[00:00:00]</span>
                    Ready. Initialize a 2D array to begin.
                </div>
            </div>
        </div>
    </div>

    <script>
        // State
        let array1D = [];
        let array2D = [];
        let currentTab = '1d';

        // Initialize particles
        function initParticles() {
            const container = document.getElementById('particles');
            for (let i = 0; i < 50; i++) {
                const particle = document.createElement('div');
                particle.className = 'particle';
                particle.style.left = Math.random() * 100 + '%';
                particle.style.animationDelay = Math.random() * 15 + 's';
                particle.style.animationDuration = (10 + Math.random() * 10) + 's';
                container.appendChild(particle);
            }
        }

        // Utility functions
        function getTimestamp() {
            const now = new Date();
            return `[${String(now.getHours()).padStart(2, '0')}:${String(now.getMinutes()).padStart(2, '0')}:${String(now.getSeconds()).padStart(2, '0')}]`;
        }

        function log(message, type = 'info', tab = '1d') {
            const console = document.getElementById(`console-${tab}`);
            const line = document.createElement('div');
            line.className = `console-line ${type}`;
            line.innerHTML = `<span class="console-timestamp">${getTimestamp()}</span>${message}`;
            console.appendChild(line);
            console.scrollTop = console.scrollHeight;
            
            // Keep only last 50 lines
            while (console.children.length > 50) {
                console.removeChild(console.firstChild);
            }
        }

        function showToast(message, type = 'info') {
            const toast = document.createElement('div');
            toast.className = `toast ${type}`;
            toast.textContent = message;
            document.body.appendChild(toast);
            setTimeout(() => toast.remove(), 3000);
        }

        function clearHighlights(tab) {
            const cells = document.querySelectorAll(`#array-${tab} .array-cell`);
            cells.forEach(cell => {
                cell.classList.remove('highlighted', 'accessed', 'error');
            });
        }

        // 1D Array Functions
        function initArray1D() {
            const size = parseInt(document.getElementById('size-1d').value);
            if (isNaN(size) || size < 1 || size > 20) {
                log('Invalid size. Must be between 1 and 20.', 'error', '1d');
                showToast('Invalid array size!', 'error');
                return;
            }

            array1D = new Array(size).fill(0);
            for (let i = 0; i < size; i++) {
                array1D[i] = Math.floor(Math.random() * 100);
            }

            renderArray1D();
            document.getElementById('length-1d').textContent = size;
            log(`Initialized array of size ${size} with random values`, 'success', '1d');
            showToast(`Array initialized [${size}]`, 'success');
        }

        function renderArray1D() {
            const container = document.getElementById('array-1d');
            container.innerHTML = '';
            
            array1D.forEach((value, index) => {
                const cell = document.createElement('div');
                cell.className = 'array-cell';
                cell.id = `cell-1d-${index}`;
                cell.innerHTML = `
                    <span class="cell-value">${value}</span>
                    <span class="cell-index">[${index}]</span>
                `;
                cell.onclick = () => {
                    document.getElementById('index-1d').value = index;
                    accessIndex1D();
                };
                container.appendChild(cell);
            });
        }

        function clearArray1D() {
            array1D = [];
            document.getElementById('array-1d').innerHTML = '';
            document.getElementById('length-1d').textContent = '0';
            log('Array cleared', 'warning', '1d');
            showToast('Array cleared', 'info');
        }

        function randomizeArray1D() {
            if (array1D.length === 0) {
                log('No array initialized', 'error', '1d');
                showToast('Initialize array first!', 'error');
                return;
            }
            for (let i = 0; i < array1D.length; i++) {
                array1D[i] = Math.floor(Math.random() * 100);
            }
            renderArray1D();
            log('Array randomized with new values', 'success', '1d');
            showToast('Values randomized!', 'success');
        }

        function accessIndex1D() {
            const indexInput = document.getElementById('index-1d');
            const index = parseInt(indexInput.value);

            clearHighlights('1d');

            if (isNaN(index)) {
                log('Invalid index format', 'error', '1d');
                showToast('Enter a valid index!', 'error');
                return;
            }

            if (array1D.length === 0) {
                log('No array initialized', 'error', '1d');
                showToast('Initialize array first!', 'error');
                return;
            }

            if (index < 0 || index >= array1D.length) {
                log(`Index out of bounds: ${index} (valid: 0-${array1D.length - 1})`, 'error', '1d');
                showToast(`Index out of bounds!`, 'error');
                
                // Highlight nearest valid index or show error on input
                indexInput.classList.add('error');
                setTimeout(() => indexInput.classList.remove('error'), 500);
                return;
            }

            const cell = document.getElementById(`cell-1d-${index}`);
            if (cell) {
                cell.classList.add('accessed');
                setTimeout(() => cell.classList.remove('accessed'), 2000);
            }

            log(`Accessed array[${index}] = ${array1D[index]}`, 'success', '1d');
            showToast(`array[${index}] = ${array1D[index]}`, 'success');
        }

        function assignValue1D() {
            const indexInput = document.getElementById('assign-index-1d');
            const valueInput = document.getElementById('assign-value-1d');
            const index = parseInt(indexInput.value);
            const value = valueInput.value;

            clearHighlights('1d');

            if (isNaN(index) || value === '') {
                log('Invalid index or value', 'error', '1d');
                showToast('Enter valid index and value!', 'error');
                return;
            }

            if (array1D.length === 0) {
                log('No array initialized', 'error', '1d');
                showToast('Initialize array first!', 'error');
                return;
            }

            if (index < 0 || index >= array1D.length) {
                log(`Assignment failed: Index ${index} out of bounds (0-${array1D.length - 1})`, 'error', '1d');
                showToast('Index out of bounds!', 'error');
                indexInput.classList.add('error');
                setTimeout(() => indexInput.classList.remove('error'), 500);
                return;
            }

            const oldValue = array1D[index];
            const numericValue = parseFloat(value);
            array1D[index] = isNaN(numericValue) ? value : numericValue;

            renderArray1D();
            
            const cell = document.getElementById(`cell-1d-${index}`);
            if (cell) {
                cell.classList.add('highlighted');
                setTimeout(() => cell.classList.remove('highlighted'), 2000);
            }

            log(`Assigned: array[${index}] = ${array1D[index]} (was ${oldValue})`, 'success', '1d');
            showToast(`array[${index}] = ${array1D[index]}`, 'success');
            
            valueInput.value = '';
            indexInput.value = '';
        }

        // 2D Array Functions
        function initArray2D() {
            const rows = parseInt(document.getElementById('rows-2d').value);
            const cols = parseInt(document.getElementById('cols-2d').value);

            if (isNaN(rows) || isNaN(cols) || rows < 1 || rows > 10 || cols < 1 || cols > 10) {
                log('Invalid dimensions. Must be 1-10 for both rows and columns.', 'error', '2d');
                showToast('Invalid dimensions!', 'error');
                return;
            }

            array2D = [];
            for (let i = 0; i < rows; i++) {
                array2D[i] = [];
                for (let j = 0; j < cols; j++) {
                    array2D[i][j] = Math.floor(Math.random() * 100);
                }
            }

            renderArray2D();
            document.getElementById('dims-2d').textContent = `${rows}×${cols}`;
            document.getElementById('total-2d').textContent = rows * cols;
            log(`Initialized 2D array [${rows}][${cols}] with random values`, 'success', '2d');
            showToast(`2D Array [${rows}][${cols}] initialized`, 'success');
        }

        function renderArray2D() {
            const container = document.getElementById('array-2d');
            container.innerHTML = '';

            array2D.forEach((row, i) => {
                const rowDiv = document.createElement('div');
                rowDiv.className = 'array-row';
                
                row.forEach((value, j) => {
                    const cell = document.createElement('div');
                    cell.className = 'array-cell';
                    cell.id = `cell-2d-${i}-${j}`;
                    cell.innerHTML = `
                        <span class="cell-coords">[${i}][${j}]</span>
                        <span class="cell-value">${value}</span>
                    `;
                    cell.onclick = () => {
                        document.getElementById('row-2d').value = i;
                        document.getElementById('col-2d').value = j;
                        accessIndex2D();
                    };
                    rowDiv.appendChild(cell);
                });
                
                container.appendChild(rowDiv);
            });
        }

        function clearArray2D() {
            array2D = [];
            document.getElementById('array-2d').innerHTML = '';
            document.getElementById('dims-2d').textContent = '0×0';
            document.getElementById('total-2d').textContent = '0';
            log('2D Array cleared', 'warning', '2d');
            showToast('2D Array cleared', 'info');
        }

        function randomizeArray2D() {
            if (array2D.length === 0) {
                log('No 2D array initialized', 'error', '2d');
                showToast('Initialize 2D array first!', 'error');
                return;
            }
            for (let i = 0; i < array2D.length; i++) {
                for (let j = 0; j < array2D[i].length; j++) {
                    array2D[i][j] = Math.floor(Math.random() * 100);
                }
            }
            renderArray2D();
            log('2D Array randomized with new values', 'success', '2d');
            showToast('2D Values randomized!', 'success');
        }

        function accessIndex2D() {
            const rowInput = document.getElementById('row-2d');
            const colInput = document.getElementById('col-2d');
            const row = parseInt(rowInput.value);
            const col = parseInt(colInput.value);

            clearHighlights('2d');

            if (isNaN(row) || isNaN(col)) {
                log('Invalid row or column format', 'error', '2d');
                showToast('Enter valid coordinates!', 'error');
                return;
            }

            if (array2D.length === 0) {
                log('No 2D array initialized', 'error', '2d');
                showToast('Initialize 2D array first!', 'error');
                return;
            }

            if (row < 0 || row >= array2D.length || col < 0 || col >= array2D[0].length) {
                let errorMsg = '';
                if (row < 0 || row >= array2D.length) {
                    errorMsg = `Row ${row} out of bounds (0-${array2D.length - 1})`;
                } else {
                    errorMsg = `Col ${col} out of bounds (0-${array2D[0].length - 1})`;
                }
                log(`Access failed: ${errorMsg}`, 'error', '2d');
                showToast('Index out of bounds!', 'error');
                
                rowInput.classList.add('error');
                colInput.classList.add('error');
                setTimeout(() => {
                    rowInput.classList.remove('error');
                    colInput.classList.remove('error');
                }, 500);
                return;
            }

            const cell = document.getElementById(`cell-2d-${row}-${col}`);
            if (cell) {
                cell.classList.add('accessed');
                setTimeout(() => cell.classList.remove('accessed'), 2000);
            }

            log(`Accessed array[${row}][${col}] = ${array2D[row][col]}`, 'success', '2d');
            showToast(`array[${row}][${col}] = ${array2D[row][col]}`, 'success');
        }

        function assignValue2D() {
            const rowInput = document.getElementById('assign-row-2d');
            const colInput = document.getElementById('assign-col-2d');
            const valueInput = document.getElementById('assign-value-2d');
            const row = parseInt(rowInput.value);
            const col = parseInt(colInput.value);
            const value = valueInput.value;

            clearHighlights('2d');

            if (isNaN(row) || isNaN(col) || value === '') {
                log('Invalid coordinates or value', 'error', '2d');
                showToast('Enter valid coordinates and value!', 'error');
                return;
            }

            if (array2D.length === 0) {
                log('No 2D array initialized', 'error', '2d');
                showToast('Initialize 2D array first!', 'error');
                return;
            }

            if (row < 0 || row >= array2D.length || col < 0 || col >= array2D[0].length) {
                let errorMsg = '';
                if (row < 0 || row >= array2D.length) {
                    errorMsg = `Row ${row} out of bounds (0-${array2D.length - 1})`;
                } else {
                    errorMsg = `Col ${col} out of bounds (0-${array2D[0].length - 1})`;
                }
                log(`Assignment failed: ${errorMsg}`, 'error', '2d');
                showToast('Index out of bounds!', 'error');
                
                rowInput.classList.add('error');
                colInput.classList.add('error');
                setTimeout(() => {
                    rowInput.classList.remove('error');
                    colInput.classList.remove('error');
                }, 500);
                return;
            }

            const oldValue = array2D[row][col];
            const numericValue = parseFloat(value);
            array2D[row][col] = isNaN(numericValue) ? value : numericValue;

            renderArray2D();
            
            const cell = document.getElementById(`cell-2d-${row}-${col}`);
            if (cell) {
                cell.classList.add('highlighted');
                setTimeout(() => cell.classList.remove('highlighted'), 2000);
            }

            log(`Assigned: array[${row}][${col}] = ${array2D[row][col]} (was ${oldValue})`, 'success', '2d');
            showToast(`array[${row}][${col}] = ${array2D[row][col]}`, 'success');
            
            valueInput.value = '';
            rowInput.value = '';
            colInput.value = '';
        }

        // Tab switching
        function switchTab(tab) {
            currentTab = tab;
            
            // Update tab buttons
            document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
            event.target.classList.add('active');
            
            // Update content
            document.querySelectorAll('.tab-content').forEach(c => c.classList.remove('active'));
            document.getElementById(`tab-${tab}`).classList.add('active');
            
            // Update displays
            document.getElementById('display-1d').style.display = tab === '1d' ? 'block' : 'none';
            document.getElementById('display-2d').style.display = tab === '2d' ? 'block' : 'none';
        }

        // Keyboard shortcuts
        document.addEventListener('keydown', (e) => {
            if (e.key === 'Enter') {
                if (currentTab === '1d') {
                    if (document.activeElement.id === 'index-1d') accessIndex1D();
                    else if (document.activeElement.id === 'assign-value-1d') assignValue1D();
                } else {
                    if (document.activeElement.id === 'col-2d') accessIndex2D();
                    else if (document.activeElement.id === 'assign-value-2d') assignValue2D();
                }
            }
        });

        // Initialize
        initParticles();
        initArray1D();
        initArray2D();
    </script>
</body>
</html>
```