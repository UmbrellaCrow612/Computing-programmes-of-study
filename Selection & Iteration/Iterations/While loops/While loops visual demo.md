
Create a html file add this and open it in browser:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Code Execution Flow</title>
    <style>
        :root {
            --bg-color: #1e1e1e;
            --container-bg: #252526;
            --text-main: #d4d4d4;
            --keyword: #569cd6;
            --control: #c586c0;
            --string: #ce9178;
            --numeric: #b5cea8;
            --comment: #6a9955;
            /* Highlight Glows */
            --check-glow: rgba(224, 108, 117, 0.3);
            --run-glow: rgba(152, 195, 121, 0.3);
            --update-glow: rgba(97, 175, 239, 0.3);
        }

        body {
            background-color: var(--bg-color);
            color: var(--text-main);
            font-family: 'Consolas', 'Monaco', monospace;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
        }

        .editor-container {
            background: var(--container-bg);
            width: 500px;
            padding: 30px;
            border-radius: 12px;
            box-shadow: 0 10px 40px rgba(0,0,0,0.5);
            border: 1px solid #333;
        }

        .window-controls {
            display: flex;
            gap: 8px;
            margin-bottom: 20px;
        }

        .dot { width: 12px; height: 12px; border-radius: 50%; }
        .red { background: #ff5f56; }
        .yellow { background: #ffbd2e; }
        .green { background: #27c93f; }

        .code-line {
            padding: 4px 12px;
            border-radius: 4px;
            transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
            border: 1px solid transparent;
            margin: 2px 0;
            position: relative;
        }

        /* Syntax Highlighting */
        .kw { color: var(--keyword); }
        .cf { color: var(--control); }
        .st { color: var(--string); }
        .nm { color: var(--numeric); }

        /* Step Highlighting States */
        .active-check { 
            background: var(--check-glow); 
            border-color: #e06c75;
            transform: scale(1.02);
        }
        .active-run { 
            background: var(--run-glow); 
            border-color: #98c379;
            transform: scale(1.02);
        }
        .active-update { 
            background: var(--update-glow); 
            border-color: #61afef;
            transform: scale(1.02);
        }

        .status-bar {
            margin-top: 30px;
            padding-top: 15px;
            border-top: 1px solid #3c3c3c;
            font-size: 0.9rem;
            display: flex;
            justify-content: space-between;
            color: #858585;
        }

        .explanation {
            color: #9cdcfe;
            font-style: italic;
        }
    </style>
</head>
<body>

<div class="editor-container">
    <div class="window-controls">
        <div class="dot red"></div>
        <div class="dot yellow"></div>
        <div class="dot green"></div>
    </div>

    <div id="line-initial" class="code-line">
        <span class="kw">let</span> i = <span class="nm">0</span>;
    </div>
    
    <div id="line-check" class="code-line">
        <span class="cf">while</span> (i &lt; <span class="nm">3</span>) {
    </div>

    <div id="line-run" class="code-line">
        &nbsp;&nbsp;console.<span class="kw">log</span>(<span class="st">"Iteration "</span> + i);
    </div>

    <div id="line-update" class="code-line">
        &nbsp;&nbsp;i = i + <span class="nm">1</span>;
    </div>

    <div id="line-end" class="code-line">
        }
    </div>

    <div class="status-bar">
        <span>VARIABLE: i = <span id="val-i" style="color: var(--numeric)">0</span></span>
        <span id="label" class="explanation">Initializing...</span>
    </div>
</div>

<script>
    const lines = {
        initial: document.getElementById('line-initial'),
        check: document.getElementById('line-check'),
        run: document.getElementById('line-run'),
        update: document.getElementById('line-update')
    };
    const valDisplay = document.getElementById('val-i');
    const label = document.getElementById('label');

    let i = 0;
    let step = 0; // 0: Check, 1: Run, 2: Update

    function clearAll() {
        Object.values(lines).forEach(line => {
            line.classList.remove('active-check', 'active-run', 'active-update');
        });
    }

    function runLoop() {
        clearAll();

        if (i < 3) {
            if (step === 0) {
                // PHASE: CHECK
                lines.check.classList.add('active-check');
                label.innerText = `Checking: Is ${i} < 3? (True)`;
                step = 1;
            } 
            else if (step === 1) {
                // PHASE: RUN
                lines.run.classList.add('active-run');
                label.innerText = "Executing loop body...";
                step = 2;
            } 
            else if (step === 2) {
                // PHASE: UPDATE
                lines.update.classList.add('active-update');
                i++;
                valDisplay.innerText = i;
                label.innerText = `Incrementing i to ${i}`;
                step = 0;
            }
        } else {
            // FINISHED - SHOW TERMINATION
            lines.check.classList.add('active-check');
            label.innerText = `Checking: Is ${i} < 3? (False) -> EXIT`;
            
            // Restart after a delay
            setTimeout(() => {
                i = 0;
                step = 0;
                valDisplay.innerText = i;
                label.innerText = "Restarting Demo...";
            }, 2000);
        }
    }

    // Run every 1.5 seconds for easy following
    setInterval(runLoop, 2500);
</script>

</body>
</html>
```