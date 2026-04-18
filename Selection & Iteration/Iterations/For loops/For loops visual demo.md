
Just run this in live server or code pen 


```html
<!DOCTYPE html>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>For Loop Flow Visualizer</title>
    <style>
        :root {
            --bg: #0d1117;
            --panel: #161b22;
            --text: #c9d1d9;
            --init: #79c0ff;   /* Blue */
            --check: #ff7b72;  /* Red/Coral */
            --step: #d2a8ff;   /* Purple */
            --body: #7ee787;   /* Green */
        }

        body {
            background-color: var(--bg);
            color: var(--text);
            font-family: 'Fira Code', 'Courier New', monospace;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            overflow: hidden;
        }

        .editor {
            background: var(--panel);
            width: 550px;
            padding: 40px;
            border-radius: 16px;
            border: 1px solid #30363d;
            box-shadow: 0 20px 50px rgba(0,0,0,0.6);
        }

        .line {
            font-size: 1.2rem;
            padding: 8px 12px;
            border-radius: 6px;
            margin: 4px 0;
            transition: all 0.4s ease;
            display: flex;
            gap: 8px;
            opacity: 0.8;
        }

        /* Logic Piece Highlighting */
        .part {
            padding: 2px 6px;
            border-radius: 4px;
            transition: all 0.3s ease;
        }

        /* Active States */
        .active-line { opacity: 1; background: rgba(255,255,255,0.05); }
        
        .active-init { background: var(--init); color: #000; box-shadow: 0 0 15px var(--init); }
        .active-check { background: var(--check); color: #000; box-shadow: 0 0 15px var(--check); }
        .active-body { background: var(--body); color: #000; box-shadow: 0 0 15px var(--body); }
        .active-step { background: var(--step); color: #000; box-shadow: 0 0 15px var(--step); }

        .dashboard {
            margin-top: 40px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-top: 1px solid #30363d;
            padding-top: 20px;
        }

        .monitor {
            font-size: 0.9rem;
            color: #8b949e;
        }

        #explanation {
            font-weight: bold;
            color: #58a6ff;
            min-height: 1.2em;
        }
    </style>
</head>
<body>

<div class="editor">
    <div id="l1" class="line">
        <span style="color: #ff7b72">for</span> ( 
        <span id="p-init" class="part">let i = 0;</span> 
        <span id="p-check" class="part">i < 3;</span> 
        <span id="p-step" class="part">i++</span> 
        ) {
    </div>
    
    <div id="l2" class="line">
        &nbsp;&nbsp;&nbsp;&nbsp;<span id="p-body" class="part">console.log("Looping...");</span>
    </div>

    <div id="l3" class="line">}</div>

    <div class="dashboard">
        <div class="monitor">
            VALUE OF i: <span id="val-i" style="color: var(--init); font-size: 1.4rem;">0</span>
        </div>
        <div id="explanation">Ready...</div>
    </div>
</div>

<script>
    let i = 0;
    let state = 'INIT'; // INIT -> CHECK -> BODY -> STEP -> CHECK ...
    
    const pInit = document.getElementById('p-init');
    const pCheck = document.getElementById('p-check');
    const pBody = document.getElementById('p-body');
    const pStep = document.getElementById('p-step');
    const valI = document.getElementById('val-i');
    const exp = document.getElementById('explanation');

    function clear() {
        [pInit, pCheck, pBody, pStep].forEach(el => el.className = 'part');
    }

    function animate() {
        clear();
        
        switch(state) {
            case 'INIT':
                pInit.classList.add('active-init');
                exp.innerText = "1. Setup variable 'i'";
                i = 0;
                valI.innerText = i;
                state = 'CHECK';
                break;

            case 'CHECK':
                pCheck.classList.add('active-check');
                if (i < 3) {
                    exp.innerText = `2. Check: Is ${i} < 3? (TRUE)`;
                    state = 'BODY';
                } else {
                    exp.innerText = `2. Check: Is ${i} < 3? (FALSE) - STOP!`;
                    state = 'INIT'; // Restart loop demo
                }
                break;

            case 'BODY':
                pBody.classList.add('active-body');
                exp.innerText = "3. Run the code inside";
                state = 'STEP';
                break;

            case 'STEP':
                pStep.classList.add('active-step');
                i++;
                exp.innerText = `4. Increment: i becomes ${i}`;
                valI.innerText = i;
                state = 'CHECK';
                break;
        }
    }

    // Set interval to 1800ms for readability
    setInterval(animate, 1800);
    animate(); // Start immediately
</script>

</body>
</html>
```