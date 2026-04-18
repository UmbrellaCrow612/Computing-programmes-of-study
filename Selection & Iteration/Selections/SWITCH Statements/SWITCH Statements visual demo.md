

Add to HTML file or code pen


```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Switch Statement Flow</title>
    <style>
        :root {
            --bg: #0d1117;
            --panel: #161b22;
            --text: #c9d1d9;
            --match: #79c0ff;  /* Blue for the variable being checked */
            --case-hit: #7ee787; /* Green for the matching case */
            --case-miss: #484f58; /* Grey for ignored cases */
            --keyword: #ff7b72;
            --break: #d2a8ff;
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
            width: 580px;
            padding: 30px;
            border-radius: 12px;
            border: 1px solid #30363d;
            box-shadow: 0 20px 60px rgba(0,0,0,0.7);
        }

        .line {
            padding: 6px 15px;
            border-radius: 4px;
            transition: all 0.4s ease;
            opacity: 0.3;
            margin: 1px 0;
        }

        /* Logic Highlighting */
        .active-match { 
            opacity: 1; 
            background: rgba(121, 192, 255, 0.15); 
            border-left: 4px solid var(--match);
        }
        
        .active-execute { 
            opacity: 1; 
            background: rgba(126, 231, 135, 0.15); 
            border-left: 4px solid var(--case-hit);
            transform: translateX(10px);
        }

        .active-break {
            opacity: 1;
            color: var(--break);
            font-weight: bold;
        }

        .ignored { opacity: 0.1; filter: blur(0.5px); }

        .dashboard {
            margin-top: 25px;
            padding: 15px;
            border-top: 1px solid #30363d;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        #status-msg { color: #58a6ff; font-style: italic; }
        .day-label { color: var(--match); font-weight: bold; font-size: 1.2rem; }
    </style>
</head>
<body>

<div class="editor">
    <div style="margin-bottom: 15px;">
        <span style="color: var(--keyword)">let</span> day = <span class="day-label" id="day-val">2</span>; 
        <span style="color: #8b949e">// (2 = Tuesday)</span>
    </div>
    
    <div id="line-switch" class="line">
        <span style="color: var(--keyword)">switch</span> (day) {
    </div>

    <div id="case-1" class="line">&nbsp;&nbsp;<span style="color: var(--keyword)">case</span> 1: console.log("Monday"); <span class="break-text">break;</span></div>
    
    <div id="case-2" class="line">&nbsp;&nbsp;<span style="color: var(--keyword)">case</span> 2: console.log("Tuesday"); <span id="break-2" class="break-text">break;</span></div>
    
    <div id="case-3" class="line">&nbsp;&nbsp;<span style="color: var(--keyword)">case</span> 3: console.log("Wednesday"); <span class="break-text">break;</span></div>
    
    <div id="case-default" class="line">&nbsp;&nbsp;<span style="color: var(--keyword)">default</span>: console.log("Other day");</div>

    <div class="line">}</div>

    <div class="dashboard">
        <div id="status-msg">Initializing machine...</div>
    </div>
</div>

<script>
    let day = 1;
    let step = 0;

    const el = {
        sw: document.getElementById('line-switch'),
        c1: document.getElementById('case-1'),
        c2: document.getElementById('case-2'),
        c3: document.getElementById('case-3'),
        def: document.getElementById('case-default'),
        brk2: document.getElementById('break-2'),
        msg: document.getElementById('status-msg'),
        dayDisplay: document.getElementById('day-val')
    };

    function reset() {
        Object.values(el).forEach(item => {
            if(item.classList) item.classList.remove('active-match', 'active-execute', 'ignored', 'active-break');
        });
    }

    function animate() {
        reset();
        
        switch(step) {
            case 0:
                el.dayDisplay.innerText = day;
                el.sw.classList.add('active-match');
                el.msg.innerText = `Looking for case ${day}...`;
                step = 1;
                break;

            case 1:
                // Simulate the "jump" to the correct case
                if (day === 1) { el.c1.classList.add('active-execute'); el.c2.classList.add('ignored'); el.c3.classList.add('ignored'); el.def.classList.add('ignored'); }
                if (day === 2) { el.c2.classList.add('active-execute'); el.c1.classList.add('ignored'); el.c3.classList.add('ignored'); el.def.classList.add('ignored'); }
                if (day === 3) { el.c3.classList.add('active-execute'); el.c1.classList.add('ignored'); el.c2.classList.add('ignored'); el.def.classList.add('ignored'); }
                el.msg.innerText = `MATCH FOUND! Jumping to Case ${day}.`;
                step = 2;
                break;

            case 2:
                // Highlight the break specifically
                if (day === 2) el.brk2.classList.add('active-break');
                el.msg.innerText = "Hit 'break' - exiting the switch.";
                step = 3;
                break;

            case 3:
                // Change day for next cycle
                day = day >= 3 ? 1 : day + 1;
                el.msg.innerText = "Resetting with new value...";
                step = 0;
                break;
        }
    }

    setInterval(animate, 2000);
    animate();
</script>

</body>
</html>
```