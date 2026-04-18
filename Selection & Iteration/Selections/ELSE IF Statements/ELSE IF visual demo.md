
Add to html file and view or in code pen:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>If-Else Execution Flow</title>
    <style>
        :root {
            --bg: #0d1117;
            --panel: #161b22;
            --text: #c9d1d9;
            --check: #ff7b72;  /* Red for Condition */
            --run: #7ee787;    /* Green for Execution */
            --skip: #484f58;   /* Grey for Skipped */
            --keyword: #d2a8ff;
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
            width: 550px;
            padding: 35px;
            border-radius: 12px;
            border: 1px solid #30363d;
            box-shadow: 0 15px 40px rgba(0,0,0,0.5);
            position: relative;
        }

        .line {
            padding: 8px 15px;
            border-radius: 6px;
            transition: all 0.5s cubic-bezier(0.4, 0, 0.2, 1);
            margin: 4px 0;
            opacity: 0.3;
            border-left: 4px solid transparent;
        }

        /* Active Highlighting */
        .active-check { 
            opacity: 1; 
            background: rgba(255, 123, 114, 0.1); 
            border-left-color: var(--check);
            transform: scale(1.02);
        }
        
        .active-run { 
            opacity: 1; 
            background: rgba(126, 231, 135, 0.15); 
            border-left-color: var(--run);
            transform: scale(1.02);
        }

        .skipped { 
            opacity: 0.1; 
            filter: grayscale(1);
        }

        .dashboard {
            margin-top: 30px;
            padding: 15px;
            background: rgba(0,0,0,0.2);
            border-radius: 8px;
            border: 1px solid #30363d;
        }

        #status-msg { color: #58a6ff; font-weight: bold; font-size: 1.1rem; }
        .val-badge { 
            background: #238636; 
            color: white; 
            padding: 2px 8px; 
            border-radius: 10px; 
            font-size: 0.9rem;
        }
    </style>
</head>
<body>

<div class="editor">
    <div style="margin-bottom: 20px;">
        <span style="color: #8b949e">// Input variable</span><br>
        <span style="color: #ff7b72">let</span> age = <span id="age-val" style="color: #79c0ff; font-weight: bold;">15</span>;
    </div>
    
    <div id="line-if" class="line">
        <span style="color: #ff7b72">if</span> (age >= <span style="color: #79c0ff">18</span>) {
    </div>

    <div id="line-if-body" class="line">
        &nbsp;&nbsp;console.log(<span style="color: #a5d6ff">"Access Granted ✅"</span>);
    </div>

    <div id="line-else" class="line">
        } <span style="color: #ff7b72">else</span> {
    </div>

    <div id="line-else-body" class="line">
        &nbsp;&nbsp;console.log(<span style="color: #a5d6ff">"Access Denied ❌"</span>);
    </div>

    <div id="line-end" class="line">
        }
    </div>

    <div class="dashboard">
        <div id="status-msg">Ready to check...</div>
    </div>
</div>

<script>
    let age = 15;
    let step = 0;

    const el = {
        ifHead: document.getElementById('line-if'),
        ifBody: document.getElementById('line-if-body'),
        elseHead: document.getElementById('line-else'),
        elseBody: document.getElementById('line-else-body'),
        end: document.getElementById('line-end'),
        msg: document.getElementById('status-msg'),
        ageDisplay: document.getElementById('age-val')
    };

    function resetStyles() {
        Object.values(el).forEach(item => {
            if(item.classList) item.classList.remove('active-check', 'active-run', 'skipped');
        });
    }

    function animate() {
        resetStyles();
        
        switch(step) {
            case 0:
                el.ageDisplay.innerText = age;
                el.ifHead.classList.add('active-check');
                el.msg.innerText = `Check: Is ${age} >= 18?`;
                step = 1;
                break;

            case 1:
                if (age >= 18) {
                    el.ifBody.classList.add('active-run');
                    el.elseHead.classList.add('skipped');
                    el.elseBody.classList.add('skipped');
                    el.msg.innerText = "True! Running the IF block.";
                } else {
                    el.ifBody.classList.add('skipped');
                    el.elseHead.classList.add('active-check');
                    el.elseBody.classList.add('active-run');
                    el.msg.innerText = "False! Jumping to the ELSE block.";
                }
                step = 2;
                break;

            case 2:
                el.end.classList.add('active-check');
                el.msg.innerText = "Logic finished. Moving on.";
                step = 3;
                break;

            case 3:
                // Toggle age for next run to show both paths
                age = (age === 15) ? 21 : 15;
                el.msg.innerText = `Updating age to ${age} for next demo...`;
                step = 0;
                break;
        }
    }

    // Run every 2 seconds
    setInterval(animate, 2000);
    animate();
</script>

</body>
</html>
```