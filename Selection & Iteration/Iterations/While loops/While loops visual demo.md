
Create a html file add this and open it in browser:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>While Loop Live Tracer</title>
    <style>
        :root {
            --bg: #000000;
            --card: #111111;
            --border: #333333;
            --text: #ededed;
            --accent: #0070f3;
            --code-bg: #0a0a0a;
            --highlight: rgba(0, 112, 243, 0.3);
            --var-color: #ff0080;
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
            text-align: center;
            color: #fff;
        }

        .code-window {
            background: var(--code-bg);
            border: 1px solid var(--border);
            border-radius: 8px;
            padding: 24px;
            font-family: 'SFMono-Regular', Consolas, monospace;
            font-size: 1.1rem;
            line-height: 1.9;
            margin-bottom: 30px;
        }

        .code-line {
            transition: all 0.3s ease;
            display: block; /* Each part on its own line for while loops */
            padding: 2px 8px;
            border-left: 3px solid transparent;
        }

        .active {
            background: var(--highlight);
            color: #3291ff;
            border-left: 3px solid var(--accent);
        }

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
            animation: pop 0.4s ease forwards;
        }

        @keyframes pop {
            0% { transform: scale(0.5); opacity: 0; }
            100% { transform: scale(1); opacity: 1; }
        }

        .status-bar {
            text-align: center;
            font-size: 1rem;
            color: #888;
            height: 30px;
        }

        .var-display {
            color: var(--var-color);
            font-weight: bold;
        }
    </style>
</head>
<body>

<div class="container">
    <h2>While Loop Visualizer</h2>
    
    <div class="code-window">
        <span id="w-init" class="code-line">let count = 0;</span>
        <span id="w-cond" class="code-line">while (count < 5) {</span>
        <span id="w-body" class="code-line" style="padding-left: 30px;">addBox(count);</span>
        <span id="w-inc" class="code-line" style="padding-left: 30px;">count = count + 1;</span>
        <span class="code-line">}</span>
    </div>

    <div id="output-grid"></div>
    
    <div class="status-bar" id="status-text">Ready...</div>
</div>

<script>
    const statusText = document.getElementById('status-text');
    const outputGrid = document.getElementById('output-grid');

    async function playWhileLoop() {
        while (true) {
            outputGrid.innerHTML = '';
            let count = 0;

            // 1. Initialization
            highlight('w-init');
            statusText.innerHTML = "Set <span class='var-display'>count</span> to 0";
            await wait(2500);

            while (count < 5) {
                // 2. Condition Check
                highlight('w-cond');
                statusText.innerHTML = `Check: Is <span class='var-display'>${count} < 5</span>? True!`;
                await wait(2500);

                // 3. Body
                highlight('w-body');
                const box = document.createElement('div');
                box.className = 'box';
                box.innerText = count;
                outputGrid.appendChild(box);
                statusText.innerHTML = `Action: Drawing box <span class='var-display'>${count}</span>`;
                await wait(2500);

                // 4. Increment
                highlight('w-inc');
                count++;
                statusText.innerHTML = `Update: <span class='var-display'>count</span> is now ${count}`;
                await wait(2500);
            }

            // Exit
            highlight('w-cond');
            statusText.innerHTML = `Check: Is <span class='var-display'>5 < 5</span>? False. Exit Loop!`;
            await wait(4000);
            
            statusText.innerHTML = "Restarting...";
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

    playWhileLoop();
</script>

</body>
</html>
```