
Just run this in live server or code pen 


```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>For Loop Live Tracer</title>
    <style>
        :root {
            --bg: #000000;
            --card: #111111;
            --border: #333333;
            --text: #ededed;
            --accent: #0070f3; /* Vercel Blue */
            --code-bg: #0a0a0a;
            --highlight: rgba(0, 112, 243, 0.3);
        }

        body {
            background-color: var(--bg);
            color: var(--text);
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            overflow: hidden;
        }

        .container {
            width: 90%;
            max-width: 700px;
            background: var(--card);
            border: 1px solid var(--border);
            border-radius: 12px;
            padding: 40px;
            box-shadow: 0 20px 50px rgba(0,0,0,0.5);
        }

        h2 {
            margin-top: 0;
            font-weight: 600;
            letter-spacing: -0.5px;
            color: #fff;
            text-align: center;
        }

        /* Code Block Styling */
        .code-window {
            background: var(--code-bg);
            border: 1px solid var(--border);
            border-radius: 8px;
            padding: 24px;
            font-family: 'SFMono-Regular', Consolas, 'Liberation Mono', Menlo, monospace;
            font-size: 1.1rem;
            line-height: 1.8;
            margin-bottom: 30px;
            position: relative;
        }

        .code-line {
            transition: all 0.2s ease;
            display: inline-block;
            border-radius: 4px;
            padding: 0 4px;
        }

        .active {
            background: var(--highlight);
            color: #3291ff;
            box-shadow: 0 0 15px rgba(0, 112, 243, 0.2);
            transform: translateX(5px);
        }

        /* Visual Output Area */
        #output-grid {
            display: flex;
            gap: 12px;
            justify-content: center;
            min-height: 80px;
            margin-bottom: 20px;
        }

        .box {
            width: 50px;
            height: 50px;
            border: 1px solid var(--accent);
            background: rgba(0, 112, 243, 0.1);
            color: var(--accent);
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
            border-radius: 6px;
            animation: fadeIn 0.4s ease forwards;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* Status Text */
        .status-bar {
            text-align: center;
            font-size: 0.9rem;
            color: #888;
            height: 24px;
            font-style: italic;
        }

        .var-display {
            color: #ff0080; /* Vercel Pink for variables */
            font-weight: bold;
        }
    </style>
</head>
<body>

<div class="container">
    <h2>Loop Visualizer</h2>
    
    <div class="code-window">
        <div>
            <span id="step-init" class="code-line">for (let i = 0;</span>
            <span id="step-cond" class="code-line">i < 5;</span>
            <span id="step-inc" class="code-line">i++) {</span>
        </div>
        <div style="padding-left: 25px;">
            <span id="step-body" class="code-line">drawBox(i);</span>
        </div>
        <div>}</div>
    </div>

    <div id="output-grid"></div>
    
    <div class="status-bar" id="status-text">Initializing...</div>
</div>

<script>
    const statusText = document.getElementById('status-text');
    const outputGrid = document.getElementById('output-grid');

    async function playLoop() {
        while (true) { // Continuous Loop
            outputGrid.innerHTML = '';
            
            // 1. Initialization
            highlight('step-init');
            statusText.innerHTML = "Step 1: Set variable <span class='var-display'>i</span> to 0";
            await wait(2000);

            for (let i = 0; i < 5; i++) {
                // 2. Condition Check
                highlight('step-cond');
                statusText.innerHTML = `Step 2: Is <span class='var-display'>${i} < 5</span>? Yes! Keep going.`;
                await wait(2000);

                // 3. Run Body
                highlight('step-body');
                const box = document.createElement('div');
                box.className = 'box';
                box.innerText = i;
                outputGrid.appendChild(box);
                statusText.innerHTML = `Step 3: Running the code inside. Drawing box <span class='var-display'>${i}</span>`;
                await wait(2000);

                // 4. Increment
                highlight('step-inc');
                statusText.innerHTML = `Step 4: <span class='var-display'>i++</span> makes i become ${i + 1}`;
                await wait(2000);
            }

            // End State
            highlight('step-cond');
            statusText.innerHTML = "Step 5: Is <span class='var-display'>5 < 5</span>? No. Loop Ends!";
            await wait(3000);
            
            statusText.innerHTML = "Restarting demo...";
            await wait(1500);
        }
    }

    function highlight(id) {
        document.querySelectorAll('.code-line').forEach(el => el.classList.remove('active'));
        document.getElementById(id).classList.add('active');
    }

    function wait(ms) {
        return new Promise(resolve => setTimeout(resolve, ms));
    }

    // Start automatically
    playLoop();
</script>

</body>
</html>
```