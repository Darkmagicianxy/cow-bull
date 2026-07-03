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

