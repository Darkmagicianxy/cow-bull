<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Cows and Bulls Game</title>

<style>
body{
    margin:0;
    font-family:'Segoe UI',sans-serif;
    background:linear-gradient(135deg,#4facfe,#00f2fe);
    display:flex;
    justify-content:center;
    align-items:center;
    height:100vh;
}

.game-card{
    background:white;
    padding:30px;
    border-radius:12px;
    width:350px;
    box-shadow:0 10px 25px rgba(0,0,0,0.2);
    text-align:center;
}

h1{
    margin-top:0;
    color:#2c3e50;
}

.images{
    display:flex;
    justify-content:center;
    gap:15px;
    margin-bottom:10px;
}

.images span{
    font-size:70px;
}

input{
    font-size:20px;
    padding:10px;
    width:140px;
    margin:10px;
    border-radius:6px;
    border:1px solid #ccc;
    text-align:center;
}

button{
    font-size:16px;
    padding:10px 15px;
    margin:5px;
    border-radius:6px;
    border:none;
    background:#27ae60;
    color:white;
    cursor:pointer;
}

button:hover{
    background:#219150;
}

.history{
    margin-top:20px;
    max-height:200px;
    overflow-y:auto;
    text-align:left;
}

.entry{
    background:#f1f1f1;
    padding:8px;
    border-radius:5px;
    margin-bottom:5px;
    border-left:4px solid #3498db;
    font-size:14px;
}

#tries{
    font-weight:bold;
    color:#555;
}
</style>
</head>

<body>

<div class="game-card">
    <h1>Cows & Bulls</h1>

    <div class="images">
        <span>🐄</span>
        <span>🐂</span>
    </div>

    <p>Guess the 4-digit number</p>
    <p id="tries">Tries left: 7</p>

    <input id="guess" maxlength="4" placeholder="1234">
    <br>
    
    <button id="submitBtn">Submit Guess</button>
    <button id="restartBtn" style="background:#e74c3c; display:none;">Play Again</button>

    <div class="history" id="historyLog"></div>
</div>

<script>
    let secretCode = "";
    let maxTries = 7;
    let triesLeft = maxTries;

    const guessInput = document.getElementById("guess");
    const submitBtn = document.getElementById("submitBtn");
    const restartBtn = document.getElementById("restartBtn");
    const triesDisplay = document.getElementById("tries");
    const historyLog = document.getElementById("historyLog");

    // Generate a random 4-digit code with unique digits
    function generateSecretCode() {
        let digits = [];
        while (digits.length < 4) {
            let r = Math.floor(Math.random() * 10).toString();
            if (!digits.includes(r)) {
                digits.push(r);
            }
        }
        return digits.join("");
    }

    // Initialize/Restart Game
    function initGame() {
        secretCode = generateSecretCode();
        triesLeft = maxTries;
        triesDisplay.textContent = `Tries left: ${triesLeft}`;
        historyLog.innerHTML = "";
        guessInput.value = "";
        guessInput.disabled = false;
        submitBtn.style.display = "inline-block";
        restartBtn.style.display = "none";
        // console.log("Secret Code (Cheater!):", secretCode); // Debugging
    }

    // Handle Guess Submission
    function checkGuess() {
        const guess = guessInput.value.trim();

        // Basic validation
        if (guess.length !== 4 || isNaN(guess)) {
            alert("Please enter a valid 4-digit number.");
            return;
        }

        // Check for unique digits in user guess (standard rules)
        if (new Set(guess).size !== 4) {
            alert("All 4 digits must be unique!");
            return;
        }

        triesLeft--;
        triesDisplay.textContent = `Tries left: ${triesLeft}`;

        let bulls = 0; // Right digit, right place
        let cows = 0;  // Right digit, wrong place

        for (let i = 0; i < 4; i++) {
            if (guess[i] === secretCode[i]) {
                bulls++;
            } else if (secretCode.includes(guess[i])) {
                cows++;
            }
        }

        // Create log entry
        const entry = document.createElement("div");
        entry.className = "entry";
        entry.textContent = `Guess: ${guess} ➔ 🐂 ${bulls} Bulls, 🐄 ${cows} Cows`;
        historyLog.insertBefore(entry, historyLog.firstChild);

        // Clear input field
        guessInput.value = "";

        // Check win/loss states
        if (bulls === 4) {
            triesDisplay.textContent = "🎉 You Won! Amazing job!";
            endGame();
        } else if (triesLeft === 0) {
            triesDisplay.textContent = `💥 Game Over! The code was ${secretCode}.`;
            endGame();
        }
    }

    function endGame() {
        guessInput.disabled = true;
        submitBtn.style.display = "none";
        restartBtn.style.display = "inline-block";
    }

    // Event Listeners
    submitBtn.addEventListener("click", checkGuess);
    
    // Also allow submitting by pressing "Enter"
    guessInput.addEventListener("keyup", function(event) {
        if (event.key === "Enter" && triesLeft > 0 && !guessInput.disabled) {
            checkGuess();
        }
    });

    restartBtn.addEventListener("click", initGame);

    // Start the game loop on load
    initGame();
</script>

</body>
</html>
