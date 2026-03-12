<script>

let secret = Math.floor(1000 + Math.random() * 9000).toString();
let historyDiv = document.getElementById("history");

let tries = 0;
let maxTries = 7;
let gameOver = false;

function checkGuess(){

if(gameOver) return;

let guess = document.getElementById("guess").value;

if(guess.length !== 4){
alert("Enter a 4 digit number");
return;
}

tries++;

let bulls = 0;
let cows = 0;

for(let i=0;i<4;i++){

if(guess[i] === secret[i]){
bulls++;
}
else if(secret.includes(guess[i])){
cows++;
}

}

let entry = document.createElement("div");
entry.className = "entry";
entry.innerText = `Try ${tries}: ${guess} | Bulls: ${bulls} | Cows: ${cows}`;
historyDiv.prepend(entry);


if(bulls === 4){
alert("🎉 You guessed it!");
gameOver = true;
return;
}

if(tries === maxTries){
alert("❌ Game Over! The number was " + secret);
gameOver = true;
}

}

function restartGame(){

secret = Math.floor(1000 + Math.random() * 9000).toString();
tries = 0;
gameOver = false;

historyDiv.innerHTML = "";
document.getElementById("guess").value = "";

}

</script>
