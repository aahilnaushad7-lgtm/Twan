<!DOCTYPE html>
<html>
<head>
<title>THE TWAN FILES</title>
<style>
body {
    margin:0;
    background:black;
    color:#00ff88;
    font-family: "Courier New", monospace;
    overflow:hidden;
}

/* Glitch Background */
body::before {
    content:"";
    position:absolute;
    top:0; left:0;
    width:100%; height:100%;
    background: repeating-linear-gradient(
        0deg,
        rgba(0,255,100,0.05),
        rgba(0,255,100,0.05) 2px,
        transparent 2px,
        transparent 4px
    );
    animation: flicker 0.2s infinite;
    pointer-events:none;
}

@keyframes flicker {
    0% { opacity: 0.9; }
    50% { opacity: 1; }
    100% { opacity: 0.9; }
}

.center {
    position:absolute;
    top:50%;
    left:50%;
    transform:translate(-50%, -50%);
    text-align:center;
}

input {
    background:black;
    border:1px solid #00ff88;
    color:#00ff88;
    padding:8px;
    text-align:center;
}

button {
    background:black;
    border:1px solid #00ff88;
    color:#00ff88;
    padding:6px 15px;
    cursor:pointer;
    margin-top:10px;
}

.hidden { display:none; }

.terminal {
    padding:30px;
    height:100vh;
    overflow-y:auto;
}

.file {
    cursor:pointer;
    margin:10px 0;
}

.file:hover {
    color:white;
}
</style>
</head>

<body>

<div id="login" class="center">
    <h1>▓▓▓ THE TWAN FILES ▓▓▓</h1>
    <p>ACCESS GATEWAY INITIALIZED</p>
    <p>Enter Passphrase:</p>
    <input type="password" id="passwordInput">
    <br>
    <button onclick="checkPassword()">ENTER</button>
    <p id="error"></p>
</div>

<div id="terminal" class="hidden terminal"></div>

<script>

function checkPassword() {
    var password = document.getElementById("passwordInput").value;
    if(password === "region"){
        document.getElementById("login").classList.add("hidden");
        document.getElementById("terminal").classList.remove("hidden");
        startTerminal();
    } else {
        document.getElementById("error").innerText = "ACCESS DENIED — TRACE INITIATED.";
    }
}

function typeWriter(text, element, speed = 30) {
    let i = 0;
    function typing() {
        if (i < text.length) {
            element.innerHTML += text.charAt(i);
            i++;
            setTimeout(typing, speed);
        }
    }
    typing();
}

function startTerminal() {
    var term = document.getElementById("terminal");
    var intro = document.createElement("div");
    term.appendChild(intro);

    let text = 
"> Decrypting archive...\n" +
"> Bypassing firewall...\n" +
"> Identity confirmed.\n" +
"> ACCESS GRANTED.\n\n" +
"> Loading TWAN Directory...\n\n";

    typeWriter(text, intro, 25);

    setTimeout(loadFiles, 4000);
}

function loadFiles(){
    var term = document.getElementById("terminal");

    let files = [
        "THE CONSTITUTIONAL VALUE OF TWAN",
        "PUNISHMENTS..",
        "THE MEMBERS"
    ];

    files.forEach(fileName => {
        let file = document.createElement("div");
        file.className = "file";
        file.innerText = "📁 " + fileName;
        file.onclick = function(){
            openFile(fileName);
        };
        term.appendChild(file);
    });
}

function openFile(name){
    var term = document.getElementById("terminal");
    var content = document.createElement("div");
    content.innerHTML = "\n\n> Opening file: " + name + "\n---------------------------------\n";

    if(name === "THE CONSTITUTIONAL VALUE OF TWAN"){
        content.innerHTML += 
        "• Loyalty above all.\n" +
        "• Secrecy is survival.\n" +
        "• Unity ensures power.\n";
    }

    if(name === "PUNISHMENTS.."){
        content.innerHTML += 
        "• Betrayal results in permanent removal.\n" +
        "• Leaks trigger immediate isolation.\n" +
        "• Disobedience is logged.\n";
    }

    if(name === "THE MEMBERS"){
        content.innerHTML += 
        "• Operator Alpha\n" +
        "• Operator Sigma\n" +
        "• Operator Ghost\n";
    }

    term.appendChild(content);
    term.scrollTop = term.scrollHeight;
}

</script>

</body>
</html>
