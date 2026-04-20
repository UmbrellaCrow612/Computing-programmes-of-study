
Paste in code pen 

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Variables vs Constants Demo</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: #f4f4f9;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
        }
        .container {
            background: white;
            padding: 2rem;
            border-radius: 12px;
            box-shadow: 0 10px 25px rgba(0,0,0,0.1);
            text-align: center;
            width: 400px;
        }
        .box {
            margin: 20px 0;
            padding: 15px;
            border: 2px solid #ddd;
            border-radius: 8px;
            transition: all 0.3s;
        }
        .variable-box { border-color: #3498db; background-color: #ebf5fb; }
        .constant-box { border-color: #e74c3c; background-color: #fdedec; }
        
        h1 { color: #2c3e50; font-size: 1.5rem; }
        .label { font-weight: bold; display: block; margin-bottom: 5px; }
        .value { font-size: 2rem; font-family: monospace; color: #333; }
        
        button {
            padding: 10px 20px;
            margin: 5px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-weight: bold;
            transition: opacity 0.2s;
        }
        .btn-var { background-color: #3498db; color: white; }
        .btn-const { background-color: #e74c3c; color: white; }
        button:hover { opacity: 0.8; }
        button:disabled { background-color: #ccc; cursor: not-allowed; }

        .status-msg {
            height: 20px;
            font-size: 0.9rem;
            margin-top: 10px;
            color: #e74c3c;
            font-weight: bold;
        }
    </style>
</head>
<body>

<div class="container">
    <h1>Memory Simulation</h1>
    
    <div class="box variable-box">
        <span class="label">VARIABLE: <code>playerScore</code></span>
        <div id="scoreValue" class="value">0</div>
        <button class="btn-var" onclick="increaseScore()">Update Value</button>
    </div>

    <div class="box constant-box">
        <span class="label">CONSTANT: <code>GRAVITY</code></span>
        <div id="gravityValue" class="value">9.81</div>
        <button class="btn-const" onclick="tryChangeConstant()">Attempt Change</button>
    </div>

    <div id="statusMsg" class="status-msg"></div>
    
    <p style="font-size: 0.8rem; color: #666; margin-top: 20px;">
        Variables can be rewritten. Constants are "Read-Only" after assignment.
    </p>
</div>

<script>
    // --- The Logic ---
    
    // 1. Defining a Variable (Use 'let')
    let playerScore = 0;

    // 2. Defining a Constant (Use 'const')
    const GRAVITY = 9.81;

    // Function to change the variable
    function increaseScore() {
        playerScore += 10; // This is allowed!
        document.getElementById('scoreValue').innerText = playerScore;
        document.getElementById('statusMsg').innerText = "Variable updated successfully.";
        document.getElementById('statusMsg').style.color = "#27ae60";
    }

    // Function to demonstrate the constant restriction
    function tryChangeConstant() {
        try {
            // This line would normally crash the script if not in a try-catch block
            // GRAVITY = 10; 
            
            document.getElementById('statusMsg').innerText = "ERROR: Cannot reassign a Constant!";
            document.getElementById('statusMsg').style.color = "#e74c3c";
            
            // Visual feedback of a "failed" attempt
            const box = document.querySelector('.constant-box');
            box.style.shake; // (Logic simulated for visual effect)
            box.animate([
                { transform: 'translateX(0px)' },
                { transform: 'translateX(5px)' },
                { transform: 'translateX(-5px)' },
                { transform: 'translateX(0px)' }
            ], { duration: 200, iterations: 2 });

        } catch (err) {
            console.error("Assignment to constant variable caught!");
        }
    }
</script>

</body>
</html>
```