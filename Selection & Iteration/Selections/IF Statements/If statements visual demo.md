

Add into html file and view in browser or code pen:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>If Statement Chain Flow</title>
    <style>
        :root {
            --bg: #0d1117;
            --panel: #161b22;
            --text: #c9d1d9;
            --check: #ff7b72;  /* Red for Condition */
            --run: #7ee787;    /* Green for Execution */
            --skip: #484f58;   /* Grey for Skipped */
            --numeric: #d2a8ff;
        }

        body {
            background-color: var(--bg);
            color: var(--text);
            font-family: 'Fira Code', monospace;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
        }

        .editor {
            background: var(--panel);
            width: 500px;
            padding: 35px;
            border-radius: 12px;
            border: 1px solid #30363d;
            box-shadow: 0 15px 40px rgba(0,0,0,0.5);
        }

        .code-block { margin-bottom: 20px; border-left: 2px solid #30363d; padding-left: 15px; }

        .line {
            padding: 6px 12px;
            border-radius: 4px;
            transition: all 0.4s ease;
            margin: 2px 0;
            opacity: 0.4;
        }

        /* Active Styles */
        .active-check { 
            opacity: 1; 
            background: rgba(255, 123, 114, 0.15); 
            border: 1px solid var(--check);
            transform: translateX(10px);
        }
        
        .active-run { 
            opacity: 1; 
            background: rgba(126, 231, 135, 0.15); 
            border: 1px solid var(--run);
            transform: translateX(10px);
        }

        .skipped { opacity: 0.2; transform: scale(0.98); }

        .dashboard {
            margin-top: 30px;
            padding-top: 15px;
            border-top: 1px solid #30363d;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        #status-msg { color: #58a6ff; font-weight: bold; }
        .val { color: var(--numeric); font-weight: bold; }
    </style>
</head>
<body>

<div class="editor">
    <div style="color: #8b949e; margin-bottom: 10px;">// Input: score = <span class="val" id="score-val">85</span></div>
    
    <div id="block1" class="code-block">
        <div id="if1" class="line"><span style="color: #ff7b72">if</span> (score >= <span class="val">50</span>) {</div>
        <div id="run1" class="line">&nbsp;&nbsp;console.log(<span style="color: #a5d6ff">"Pass!"</span>);</div>
        <div class="line">}</div>
    </div>

    <div id="block2" class="code-block">
        <div id="if2" class="line"><span style="color: #ff7b72">if</span> (score >= <span class="val">80</span>) {</div>
        <div id="run2" class="line">&nbsp;&nbsp;console.log(<span style="color: #a5d6ff">"Distinction!"</span>);</div>
        <div class="line">}</div>
    </div>

    <div id="block3" class="code-block">
        <div id="if3" class="line"><span style="color: #ff7b72">if</span> (score < <span class="val">20</span>) {</div>
        <div id="run3" class="line">&nbsp;&nbsp;console.log(<span style="color: #a5d6ff">"Retake."</span>);</div>
        <div class="line">}</div>
    </div>

    <div class="dashboard">
        <div id="status-msg">Initializing...</div>
    </div>
</div>

<script>
    const score = 85;
    let step = 0;

    const elements = {
        if1: document.getElementById('if1'),
        run1: document.getElementById('run1'),
        if2: document.getElementById('if2'),
        run2: document.getElementById('run2'),
        if3: document.getElementById('if3'),
        run3: document.getElementById('run3'),
        msg: document.getElementById('status-msg')
    };

    function clear() {
        Object.values(elements).forEach(el => {
            if(el.classList) el.classList.remove('active-check', 'active-run', 'skipped');
        });
    }

    function animate() {
        clear();
        
        switch(step) {
            case 0:
                elements.if1.classList.add('active-check');
                elements.msg.innerText = "Check 1: Is 85 >= 50? (YES)";
                step = 1;
                break;
            case 1:
                elements.run1.classList.add('active-run');
                elements.msg.innerText = "Condition met! Running Block 1...";
                step = 2;
                break;
            case 2:
                elements.if2.classList.add('active-check');
                elements.msg.innerText = "Check 2: Is 85 >= 80? (YES)";
                step = 3;
                break;
            case 3:
                elements.run2.classList.add('active-run');
                elements.msg.innerText = "Condition met! Running Block 2...";
                step = 4;
                break;
            case 4:
                elements.if3.classList.add('active-check');
                elements.msg.innerText = "Check 3: Is 85 < 20? (NO)";
                step = 5;
                break;
            case 5:
                elements.run3.classList.add('skipped');
                elements.msg.innerText = "False. Skipping Block 3 code.";
                step = 6;
                break;
            default:
                elements.msg.innerText = "End of chain. Restarting...";
                step = 0;
        }
    }

    setInterval(animate, 2000);
    animate();
</script>

</body>
</html>
```