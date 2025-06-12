<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Cows and Bulls Game</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <style>
    body {
      margin: 0;
      font-family: 'Segoe UI', sans-serif;
      background: linear-gradient(to right, #f5f7fa, #c3cfe2);
      text-align: center;
      padding: 30px;
    }

    h1 {
      font-size: 2.5em;
      color: #2c3e50;
    }

    .images {
      margin: 20px;
    }

    .images img {
      width: 120px;
      margin: 0 15px;
    }

    input {
      font-size: 20px;
      padding: 10px;
      width: 150px;
      margin: 10px;
      border-radius: 6px;
    }

    button {
      font-size: 20px;
      padding: 10px 20px;
      margin: 10px;
      border-radius: 6px;
      background: #27ae60;
      color: white;
      border: none;
      cursor: pointer;
    }

    button:hover {
      background: #219150;
    }

    .history {
      margin-top: 30px;
      max-width: 500px;
      margin-left: auto;
      margin-right: auto;
      text-align: left;
    }

    .entry {
      background: #ecf0f1;
      padding: 10px;
      border-radius: 5px;
      margin-bottom: 8px;
      border-left: 5px solid #3498db;
    }
  </style>
</head>
<body>
  <h1>Cows and Bulls Game</h1>
  <div class="images">
    <img src="https://cdn.pixabay.com/photo/2013/07/13/12/43/bull-160190_960_720.png" alt="Bull">
    <img src="https://cdn.pixabay.com/photo/2021/08/02/09/54/cow-6514220_1280.png" alt="Cow">
  </div>
  <p>Guess a 4-digit number (1–9, no repeats). You have 7 tries!</p>
  <input id="guessInput" maxlength="4" placeholder="1234" />
  <button onclick="makeGuess()">Guess</button>
  <button onclick="startGame()">Restart</button>
  <div class="history" id="history"></div>

  <script>
    let target = "";
    let tries = 0;
    const maxTries = 7;

    function startGame() {
      target = generateNumber();
      tries = 0;
      document.getElementById("history").innerHTML = "";
      document.getElementById("guessInput").value = "";
    }

    function generateNumber() {
      const digits = [];
      for (let a = 1; a <= 9; a++) {
        for (let b = 1; b <= 9; b++) {
          if (b === a) continue;
          for (let c = 1; c <= 9; c++) {
            if (c === a || c === b) continue;
            for (let d = 1; d <= 9; d++) {
              if (d === a || d === b || d === c) continue;
              digits.push(`${a}${b}${c}${d}`);
            }
          }
        }
      }
      return digits[Math.floor(Math.random() * digits.length)];
    }

    function makeGuess() {
      const input = document.getElementById("guessInput");
      const guess = input.value.trim();
      if (!/^[1-9]{4}$/.test(guess) || new Set(guess).size !== 4) {
        alert("Enter a 4-digit number with non-repeating digits (1–9).");
        return;
      }

      tries++;
      const result = checkGuess(target, guess);
      const history = document.getElementById("history");

      const div = document.createElement("div");
      div.className = "entry";
      div.textContent = `${tries}. ${guess} — ${result.bulls} Bulls 🐂, ${result.cows} Cows 🐄`;
      history.appendChild(div);

      if (result.bulls === 4) {
        alert("🎉 Congratulations! You guessed it!");
        tries = maxTries;
      } else if (tries >= maxTries) {
        alert("❌ Game over! The correct number was: " + target);
      }

      input.value = "";
    }

    function checkGuess(answer, guess) {
      let bulls = 0, cows = 0;
      for (let i = 0; i < 4; i++) {
        const ch = guess[i];
        if (answer[i] === ch) bulls++;
        else if (answer.includes(ch)) cows++;
      }
      return { bulls, cows };
    }

    startGame();
  </script>
</body>
</html>
