

Create file and add this in html file and open it in the browser:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Smooth Bubble Sort Visualizer</title>
    <style>
        :root {
            --bg: #000000;
            --card: #111111;
            --border: #333333;
            --text: #ededed;
            --accent: #0070f3;
            --code-bg: #0a0a0a;
            --highlight: rgba(0, 112, 243, 0.3);
            --compare-color: #f5a623; /* Orange */
            --swap-color: #7ed321;   /* Green */
            --lock-color: #333333;
            
            /* Visualizer specific settings */
            --bar-width: 50px;
            --bar-gap: 10px;
            --container-height: 180px;
        }

        body {
            background-color: var(--bg);
            color: var(--text);
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            margin: 0;
            overflow: hidden;
        }

        .container {
            width: 95%;
            max-width: 800px;
            background: var(--card);
            border: 1px solid var(--border);
            border-radius: 12px;
            padding: 30px;
            box-shadow: 0 20px 50px rgba(0,0,0,0.5);
        }

        h2 { text-align: center; margin-bottom: 25px; font-weight: 600; letter-spacing: -0.5px;}

        /* --- Smooth Visualizer Area --- */
        #array-container {
            position: relative; /* Crucial for absolute children */
            display: flex;
            justify-content: center;
            height: var(--container-height);
            margin-bottom: 25px;
            /* width needs to be set dynamically based on array size */
        }

        .bar {
            position: absolute;
            bottom: 0;
            width: var(--bar-width);
            background: var(--accent);
            color: white;
            display: flex;
            align-items: center;
            justify-content: center;
            border-radius: 6px 6px 2px 2px;
            font-weight: bold;
            font-size: 1.1rem;
            
            /* THIS IS THE SECRET SAUCE: Smoothes movement AND color changes */
            transition: left 0.5s ease-out, background-color 0.3s ease, transform 0.2s ease;
            
            box-shadow: 0 2px 5px rgba(0,0,0,0.2);
        }

        /* States (Classes added by JavaScript) */
        .bar.comparing { 
            background-color: var(--compare-color); 
            transform: scale(1.05); 
            z-index: 2; /* Put compared bars on top */
        }
        
        .bar.swapping { 
            background-color: var(--swap-color); 
            z-index: 3; /* Swap bars are on VERY top */
        }
        
        .bar.sorted { 
            background-color: var(--lock-color); 
            border: 1px solid #555;
            color: #888;
        }

        /* --- Code & Status Area --- */
        .code-window {
            background: var(--code-bg);
            border: 1px solid var(--border);
            border-radius: 8px;
            padding: 20px;
            font-family: 'SFMono-Regular', Consolas, Menlo, monospace;
            font-size: 0.95rem;
            line-height: 1.7;
            margin-bottom: 20px;
        }

        .code-line { transition: all 0.2s ease; display: block; padding: 0 8px; border-left: 3px solid transparent; }
        .active { background: var(--highlight); color: #3291ff; border-left: 3px solid var(--accent); }

        .status-bar { text-align: center; font-size: 1rem; color: #aaa; height: 30px; font-weight: 500;}
        .var-display { color: #ff0080; font-weight: bold; }
    </style>
</head>
<body>

<div class="container">
    <h2>Bubble Sort Live Tracer</h2>
    
    <div id="array-container"></div>

    <div class="code-window">
        <span id="line-1" class="code-line">for (let i = 0; i < n - 1; i++) {</span>
        <span id="line-2" class="code-line" style="padding-left: 20px;">for (let j = 0; j < n - i - 1; j++) {</span>
        <span id="line-3" class="code-line" style="padding-left: 40px;">if (list[j] > list[j+1]) {</span>
        <span id="line-4" class="code-line" style="padding-left: 60px;">swap(list[j], list[j+1]);</span>
        <span class="code-line" style="padding-left: 40px;">}</span>
        <span class="code-line" style="padding-left: 20px;">}</span>
        <span class="code-line">}</span>
    </div>
    
    <div class="status-bar" id="status-text">Ready...</div>
</div>

<script>
    const container = document.getElementById('array-container');
    const statusText = document.getElementById('status-text');
    
    // Configurable Initial Data
    let initialData = [45, 20, 80, 15, 50];
    let barElements = []; // To store references to the DOM objects

    // 1. CREATE DOM BARS ONCE (absolute positioning initialized)
    function createInitialBars(data) {
        container.innerHTML = ''; // Clear container
        barElements = []; // Reset references

        const numBars = data.length;
        // Total container width needed = (barWidth + gap) * numBars - lastGap
        const totalWidth = (60 * numBars) - 10;
        container.style.width = `${totalWidth}px`;

        data.forEach((value, index) => {
            const bar = document.createElement('div');
            bar.className = 'bar';
            bar.innerText = value;
            bar.id = `bar-${index}`; // Add unique ID for tracing
            
            // Set Height based on Value (max height 160px)
            bar.style.height = `${(value / 100) * 160}px`;
            
            // Initial Position (left value is crucial for transitions)
            bar.style.left = `${index * 60}px`;

            container.appendChild(bar);
            barElements.push(bar); // Store the reference
        });
    }

    // 2. HELPER: Move a specific DOM element to a new index smoothly
    function moveBarToPosition(barElement, newIndex) {
        // Since we use left: index * width_plus_gap, 
        // the CSS transition handles the rest.
        barElement.style.left = `${newIndex * 60}px`;
    }

    async function bubbleSort() {
        while (true) {
            let workingData = [...initialData]; // Clone initial array
            createInitialBars(workingData);
            let n = workingData.length;
            let sortedIndices = [];

            await wait(2000); // Intro pause

            for (let i = 0; i < n - 1; i++) {
                highlight('line-1');
                statusText.innerHTML = `Outer Loop Pass: <span class='var-display'>${i + 1}</span>`;
                await wait(1500);

                for (let j = 0; j < n - i - 1; j++) {
                    // Update Highlights
                    highlight('line-2');
                    // Add .comparing class smoothly via JS
                    barElements[j].classList.add('comparing');
                    barElements[j+1].classList.add('comparing');
                    
                    statusText.innerHTML = `Inner Loop: Checking if <span class='var-display'>${workingData[j]} > ${workingData[j+1]}</span>`;
                    await wait(1800); // Time to read

                    highlight('line-3');
                    if (workingData[j] > workingData[j + 1]) {
                        statusText.innerHTML = `Yes! <span class='var-display'>${workingData[j]} > ${workingData[j+1]}</span>. Swap!`;
                        
                        // Switch to .swapping color state
                        barElements[j].classList.remove('comparing');
                        barElements[j+1].classList.remove('comparing');
                        barElements[j].classList.add('swapping');
                        barElements[j+1].classList.add('swapping');
                        
                        highlight('line-4');
                        await wait(600); // Noticeable color change before move

                        // --- THE ACTUAL PHYSICAL SWAP ---
                        // Swap data in the logical array
                        [workingData[j], workingData[j + 1]] = [workingData[j + 1], workingData[j]];
                        
                        // Swap DOM element references in our tracking list
                        [barElements[j], barElements[j + 1]] = [barElements[j + 1], barElements[j]];

                        // Update their visual 'left' positions
                        moveBarToPosition(barElements[j], j);
                        moveBarToPosition(barElements[j+1], j+1);

                        await wait(1500); // Time for the movement transition to complete
                        
                        // Clean up state
                        barElements[j].classList.remove('swapping');
                        barElements[j+1].classList.remove('swapping');
                    } else {
                        statusText.innerHTML = `No. <span class='var-display'>${workingData[j]}</span> is smaller. No swap.`;
                        
                        await wait(1200);
                        // Clean up comparing state
                        barElements[j].classList.remove('comparing');
                        barElements[j+1].classList.remove('comparing');
                    }
                }
                
                // End of pass: Lock the last element
                const lockIndex = n - 1 - i;
                barElements[lockIndex].classList.add('sorted');
                statusText.innerHTML = `Pass finished. <span class='var-display'>${workingData[lockIndex]}</span> is sorted.`;
                await wait(1500);
            }
            
            // Full Complete State
            highlight(null);
            barElements.forEach(bar => bar.classList.add('sorted'));
            statusText.innerHTML = "List is Sorted! (Press Reset to Restart)";
            
            // Keep completed sort visible, then restart demo
            await wait(5000); 
        }
    }

    function highlight(id) {
        document.querySelectorAll('.code-line').forEach(el => el.classList.remove('active'));
        if(id) document.getElementById(id).classList.add('active');
    }

    function wait(ms) {
        return new Promise(resolve => setTimeout(resolve, ms));
    }

    // Start Automatically
    bubbleSort();
</script>

</body>
</html>
```