# PRODIGY_WD_01
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Stopwatch App</title>

    <style>
        body {
            margin: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background: #111;
            font-family: Arial, sans-serif;
            color: #fff;
        }

        .container {
            text-align: center;
        }

        .time {
            font-size: 4rem;
            margin-bottom: 20px;
        }

        button {
            padding: 10px 20px;
            margin: 10px;
            font-size: 1rem;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }

        #start { background: #1abc9c; }
        #pause  { background: #e67e22; }
        #reset  { background: #e74c3c; }
        #lap    { background: #3498db; }

        ul {
            list-style: none;
            padding: 0;
            margin-top: 20px;
            max-height: 200px;
            overflow-y: auto;
        }

        li {
            background: #222;
            padding: 8px;
            margin: 5px 0;
            border-radius: 4px;
        }
    </style>
</head>

<body>

    <div class="container">
        <div class="time" id="display">00:00:00</div>

        <button id="start">Start</button>
        <button id="pause">Pause</button>
        <button id="lap">Lap</button>
        <button id="reset">Reset</button>

        <ul id="laps"></ul>
    </div>

    <script>
        let milliseconds = 0;
        let timer = null;

        function updateDisplay() {
            let secs = Math.floor(milliseconds / 1000);
            let mins = Math.floor(secs / 60);
            let hrs = Math.floor(mins / 60);

            secs %= 60;
            mins %= 60;

            document.getElementById("display").innerText =
                `${String(hrs).padStart(2, '0')}:${String(mins).padStart(2, '0')}:${String(secs).padStart(2, '0')}`;
        }

        document.getElementById("start").addEventListener("click", () => {
            if (timer !== null) return; // already running

            timer = setInterval(() => {
                milliseconds += 1000;
                updateDisplay();
            }, 1000);
        });

        document.getElementById("pause").addEventListener("click", () => {
            clearInterval(timer);
            timer = null;
        });

        document.getElementById("reset").addEventListener("click", () => {
            clearInterval(timer);
            timer = null;
            milliseconds = 0;
            updateDisplay();
            document.getElementById("laps").innerHTML = "";
        });

        document.getElementById("lap").addEventListener("click", () => {
            const lapList = document.getElementById("laps");
            const li = document.createElement("li");
            li.textContent = document.getElementById("display").innerText;
            lapList.appendChild(li);
        });

        updateDisplay();
    </script>

</body>
</html>
