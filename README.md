<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Cows and Bulls Game</title>

<style>
body{
  margin:0;
  font-family:'Segoe UI',sans-serif;
  background:linear-gradient(135deg,#f5f7fa,#c3cfe2);
  text-align:center;
  padding:30px;
}

h1{
  font-size:2.5em;
  color:#2c3e50;
}

.images{
  margin:20px;
}

.images img{
  width:120px;
  margin:0 15px;
}

input{
  font-size:20px;
  padding:10px;
  width:150px;
  margin:10px;
  border-radius:6px;
  border:1px solid #ccc;
}

button{
  font-size:20px;
  padding:10px 20px;
  margin:10px;
  border-radius:6px;
  background:#27ae60;
  color:white;
  border:none;
  cursor:pointer;
}

button:hover{
  background:#219150;
}

.history{
  margin-top:30px;
  max-width:500px;
  margin-left:auto;
  margin-right:auto;
  text-align:left;
}

.entry{
  background:#ecf0f1;
  padding:10px;
  border-radius:5px;
  margin-bottom:8px;
  border-left:5px solid #3498db;
}
</style>
</head>

<body>

<h1>🐄 Cows and Bulls Game 🐂</h1>

<div class="images">
<img src="https://cdn-icons-png.flaticon.com/512/1998/1998610.png">
<img src="https://cdn-icons-png.flaticon.com/512/616/616408.png">
</div>

<p>Enter a 4 digit number</p>

<input type="text" id="guess" maxlength="4" placeholder="1234">

<br>

<button onclick="checkGuess()">Guess</button>
<button onclick="restartGame()">Restart</button>

<div class="history" id="history"></div>

<script>

let secret="1234"; // demo number
let historyDiv=document.getElementById("history");

function checkGuess(){

let guess=document.getElementById("guess").value;

let bulls=0;
let cows=0;

for(let i=0;i<4;i++){

if(guess[i]===secret[i]){
bulls++;
}
else if(secret.includes(guess[i])){
cows++;
}

}

let entry=document.createElement("div");
entry.className="entry";
entry.innerText=`Guess: ${guess} | Bulls: ${bulls} | Cows: ${cows}`;

historyDiv.prepend(entry);

}

function restartGame(){
historyDiv.innerHTML="";
document.getElementById("guess").value="";
}

</script>

</body>
</html>
