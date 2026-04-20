
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Array Visualizer (Minimal Dark)</title>
    <style>
        :root {
            --bg: #121212;
            --surface: #1e1e1e;
            --border: #333;
            --text-primary: #e0e0e0;
            --text-secondary: #a0a0a0;
            --accent: #bb86fc; /* Purple */
            --accent-green: #03dac6; /* Teal */
            --accent-red: #cf6679; /* Pinkish-Red */
            --transition-speed: 0.3s;
        }

        * { box-sizing: border-box; }

        body {
            font-family: 'SF Mono', 'Roboto Mono', 'Consolas', monospace;
            background-color: var(--bg);
            color: var(--text-primary);
            margin: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            width: 100%;
            max-width: 900px;
            text-align: center;
        }

        h1 { font-size: 1.5rem; margin-bottom: 2rem; color: var(--accent); }
        h2 { font-size: 1rem; color: var(--text-secondary); margin-top: 1.5rem; text-align: left;}

        /* --- Global Styles --- */
        .controls {
            margin-top: 20px;
            display: flex;
            gap: 10px;
            justify-content: center;
        }

        button {
            background-color: transparent;
            border: 1px solid var(--border);
            color: var(--text-secondary);
            padding: 8px 16px;
            cursor: pointer;
            border-radius: 4px;
            transition: all var(--transition-speed) ease;
        }

        button:hover {
            border-color: var(--accent);
            color: var(--accent);
            background-color: rgba(187, 134, 252, 0.05);
        }

        button.active {
            background-color: var(--accent);
            color: var(--bg);
            border-color: var(--accent);
        }

        /* --- Section Styling --- */
        section {
            background-color: var(--surface);
            border: 1px solid var(--border);
            padding: 2rem;
            border-radius: 8px;
            margin-bottom: 2rem;
        }

        /* --- 1D Array Structure --- */
        .array-structure {
            display: flex;
            justify-content: center;
            gap: 5px;
            margin: 20px 0;
        }

        .array-element-container {
            display: flex;
            flex-direction: column;
            align-items: center;
            width: 60px;
        }

        .array-element {
            width: 60px;
            height: 60px;
            background-color: var(--surface);
            border: 2px solid var(--border);
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 1.2rem;
            color: var(--text-primary);
            transition: all var(--transition-speed) ease;
            position: relative;
        }

        .array-element.active-element {
            border-color: var(--accent);
            transform: scale(1.05);
            background-color: rgba(187, 134, 252, 0.1);
        }

        .array-index {
            color: var(--text-secondary);
            font-size: 0.8rem;
            margin-top: 5px;
            transition: color var(--transition-speed);
        }

        .active-element + .array-index {
            color: var(--accent);
            font-weight: bold;
        }

        /* --- 2D Array Structure --- */
        .grid-structure {
            display: flex;
            justify-content: center;
            flex-direction: column;
            align-items: center;
            gap: 5px;
            margin: 20px 0;
        }

        .grid-row { display: flex; gap: 5px; }

        .grid-element {
            width: 50px;
            height: 50px;
            border: 2px solid var(--border);
            display: flex;
            justify-content: center;
            align-items: center;
            transition: all var(--transition-speed) ease;
        }

        .grid-element.highlight-2d {
            border-color: var(--accent-green);
            transform: scale(1.1);
            background-color: rgba(3, 218, 198, 0.1);
        }

        /* --- Annotations --- */
        .label {
            color: var(--accent);
            font-size: 0.9rem;
            margin-bottom: 10px;
            display: block;
        }

        #status-display {
            color: var(--text-secondary);
            font-style: italic;
            height: 1.2rem;
            margin-bottom: 1rem;
        }

        /* Animations */
        @keyframes pulseSuccess {
            0% { border-color: var(--accent); }
            50% { border-color: var(--accent-green); }
            100% { border-color: var(--accent); }
        }

        .element-updated { animation: pulseSuccess 0.6s ease; }

    </style>
</head>
<body>

<div class="container">
    <h1>Array & Grid Visualization</h1>
    <div id="status-display">Demo initialized.</div>

    <section>
        <h2>1. One-Dimensional Array (Sequential Access)</h2>
        <span class="label">numbers[ ]</span>
        <div class="array-structure" id="oneDArray">
            </div>
        <div class="controls">
            <button onclick="startSequentialScan()">Sequentially Scan</button>
            <button onclick="accessIndex(2)">Access Index 2</button>
            <button onclick="updateValue(4)">Update Index 4</button>
            <button onclick="reset1D()">Reset</button>
        </div>
    </section>

    <section>
        <h2>2. Two-Dimensional Array (Grid System)</h2>
        <span class="label">board[row][column]</span>
        <div class="grid-structure" id="gridArray">
            </div>
        <div class="controls">
            <button onclick="accessCoord(0,0)">Access [0][0]</button>
            <button onclick="accessCoord(1,2)">Access [1][2]</button>
            <button onclick="accessCoord(2,1)">Access [2][1]</button>
            <button onclick="resetGrid()">Reset</button>
        </div>
    </section>

</div>

<script>
    const status = document.getElementById('status-display');

    // ==========================================
    // --- 1D Array (Visual & Logical) ---
    // ==========================================
    const logicalArray = [5, 10, 15, 20, 25, 30];
    let scanInterval;

    function render1DArray() {
        const container = document.getElementById('oneDArray');
        container.innerHTML = '';
        logicalArray.forEach((val, index) => {
            const elContainer = document.createElement('div');
            elContainer.className = 'array-element-container';

            const el = document.createElement('div');
            el.className = 'array-element';
            el.id = `el-1d-${index}`;
            el.innerText = val;

            const idx = document.createElement('div');
            idx.className = 'array-index';
            idx.innerText = index;

            elContainer.appendChild(el);
            elContainer.appendChild(idx);
            container.appendChild(elContainer);
        });
    }

    function reset1DVisuals() {
        clearInterval(scanInterval);
        document.querySelectorAll('.array-element').forEach(e => e.classList.remove('active-element'));
    }

    // 1. Sequential Scan
    function startSequentialScan() {
        reset1DVisuals();
        let currentIndex = 0;
        status.innerText = "Scanning: accessing element at current index...";

        scanInterval = setInterval(() => {
            if (currentIndex > 0) {
                document.getElementById(`el-1d-${currentIndex - 1}`).classList.remove('active-element');
            }

            if (currentIndex < logicalArray.length) {
                document.getElementById(`el-1d-${currentIndex}`).classList.add('active-element');
                currentIndex++;
            } else {
                clearInterval(scanInterval);
                status.innerText = "Scan complete. All elements accessed.";
            }
        }, 500);
    }

    // 2. Direct Index Access
    function accessIndex(idx) {
        reset1DVisuals();
        status.innerText = `Direct Access: Reading memory location numbers[${idx}]. Value: ${logicalArray[idx]}.`;
        document.getElementById(`el-1d-${idx}`).classList.add('active-element');
    }

    // 3. Update Value (Mutation)
    function updateValue(idx) {
        reset1DVisuals();
        const newVal = logicalArray[idx] + 99;
        logicalArray[idx] = newVal; // Logical Update
        
        const visualElement = document.getElementById(`el-1d-${idx}`);
        visualElement.innerText = newVal; // Visual Update
        status.innerText = `Updated location numbers[${idx}] to ${newVal}.`;
        visualElement.classList.add('element-updated'); // Animation trigger

        setTimeout(() => visualElement.classList.remove('element-updated'), 600);
    }

    function reset1D() {
        logicalArray.splice(0, logicalArray.length, 5, 10, 15, 20, 25, 30);
        reset1DVisuals();
        render1DArray();
        status.innerText = "1D Array reset.";
    }

    // ==========================================
    // --- 2D Array (Visual & Logical) ---
    // ==========================================
    const logicalGrid = [
        ['X', 'O', 'O'],
        ['O', 'X', ' '],
        ['X', ' ', 'O']
    ];

    function renderGrid() {
        const container = document.getElementById('gridArray');
        container.innerHTML = '';
        logicalGrid.forEach((row, rowIndex) => {
            const rowDiv = document.createElement('div');
            rowDiv.className = 'grid-row';
            row.forEach((cell, colIndex) => {
                const cellDiv = document.createElement('div');
                cellDiv.className = 'grid-element';
                cellDiv.id = `grid-${rowIndex}-${colIndex}`;
                cellDiv.innerText = cell;
                rowDiv.appendChild(cellDiv);
            });
            container.appendChild(rowDiv);
        });
    }

    function accessCoord(r, c) {
        // Remove prior grid highlight
        document.querySelectorAll('.grid-element').forEach(e => e.classList.remove('highlight-2d'));
        
        // Highlight new target
        const target = document.getElementById(`grid-${r}-${c}`);
        target.classList.add('highlight-2d');
        status.innerText = `Grid Access: accessing board[row ${r}][column ${c}]. Value: '${logicalGrid[r][c]}'.`;
    }

    function resetGrid() {
        document.querySelectorAll('.grid-element').forEach(e => e.classList.remove('highlight-2d'));
        status.innerText = "Grid reset.";
    }

    // Initialization
    render1DArray();
    renderGrid();

</script>

</body>
</html>
```