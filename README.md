<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Pesan Rahasia</title>

<style>

*{
    margin:0;
    padding:0;
    box-sizing:border-box;
    font-family:'Poppins',sans-serif;
}

body{
    height:100vh;
    display:flex;
    justify-content:center;
    align-items:center;
    overflow:hidden;
    background: linear-gradient(135deg,#6a11cb,#2575fc,#ff4ecd);
    position:relative;
}

/* efek cahaya background */
.glow{
    position:absolute;
    width:350px;
    height:350px;
    border-radius:50%;
    background:rgba(255,255,255,0.15);
    filter:blur(90px);
    animation:gerak 8s infinite alternate;
}

.glow:nth-child(1){
    top:-100px;
    left:-100px;
}

.glow:nth-child(2){
    bottom:-100px;
    right:-100px;
}

@keyframes gerak{
    from{
        transform:translateY(0px);
    }
    to{
        transform:translateY(50px);
    }
}

.container{
    width:90%;
    max-width:520px;
    padding:35px;
    border-radius:28px;
    background:rgba(255,255,255,0.12);
    backdrop-filter:blur(16px);
    box-shadow:0 8px 35px rgba(0,0,0,0.35);
    text-align:center;
    color:white;
    z-index:2;
    animation:muncul 1s ease;
}

@keyframes muncul{
    from{
        opacity:0;
        transform:translateY(40px);
    }
    to{
        opacity:1;
        transform:translateY(0);
    }
}

.lock{
    font-size:65px;
    margin-bottom:10px;
    animation:goyang 2s infinite;
}

@keyframes goyang{
    0%{transform:rotate(0deg);}
    25%{transform:rotate(10deg);}
    50%{transform:rotate(0deg);}
    75%{transform:rotate(-10deg);}
    100%{transform:rotate(0deg);}
}

h1{
    font-size:2.4em;
    margin-bottom:10px;
}

p{
    opacity:0.9;
    margin-bottom:20px;
}

textarea,
input{
    width:100%;
    padding:15px;
    margin:10px 0;
    border:none;
    border-radius:16px;
    outline:none;
    font-size:16px;
    background:rgba(255,255,255,0.18);
    color:white;
}

textarea::placeholder,
input::placeholder{
    color:#f1f1f1;
}

button{
    width:100%;
    padding:14px;
    margin-top:10px;
    border:none;
    border-radius:16px;
    background:linear-gradient(135deg,#ff4ecd,#7f5cff);
    color:white;
    font-size:16px;
    font-weight:bold;
    cursor:pointer;
    transition:0.3s;
}

button:hover{
    transform:scale(1.03);
    box-shadow:0 5px 20px rgba(255,255,255,0.3);
}

.output{
    margin-top:18px;
    padding:15px;
    border-radius:16px;
    background:rgba(255,255,255,0.14);
    min-height:70px;
    word-wrap:break-word;
    font-size:18px;
    animation:fade 0.5s;
}

@keyframes fade{
    from{
        opacity:0;
    }
    to{
        opacity:1;
    }
}

.footer{
    margin-top:18px;
    font-size:13px;
    opacity:0.8;
}

</style>
</head>

<body>

<div class="glow"></div>
<div class="glow"></div>

<div class="container">

    <div class="lock">🔐</div>

    <h1>Pesan Rahasia</h1>

    <p>
        Kirim pesan rahasia yang hanya bisa dibuka
        dengan kata kunci spesial 💜
    </p>

    <textarea
        id="messageInput"
        rows="5"
        placeholder="Tulis pesan rahasiamu..."
    ></textarea>

    <button onclick="encryptMessage()">
        🔒 Rahasiakan Pesan
    </button>

    <div class="output" id="encryptedOutput">
        Hasil pesan rahasia muncul di sini...
    </div>

    <input
        type="password"
        id="keyInput"
        placeholder="Masukkan kata kunci"
    >

    <button onclick="decryptMessage()">
        🔓 Buka Pesan
    </button>

    <div class="output" id="realMessage">
        Pesan asli akan muncul di sini...
    </div>

    <div class="footer">
        Kelompok 4 • Website Interaktif
    </div>

</div>

<script>

let originalMessage = "";

// kata kunci
const secretKey = "i love you";

// ubah pesan jadi emoji
function encryptMessage(){

    const input =
    document.getElementById("messageInput").value;

    originalMessage = input;

    let encrypted = "";

    const emojis = [
        "💜","✨","🦋","🌸","🎀","💎",
        "🌙","☁️","💫","🧸","🎵",
        "⚡","🍓","🌈","🔥"
    ];

    for(let i = 0; i < input.length; i++){

        encrypted +=
        emojis[Math.floor(Math.random() * emojis.length)];
    }

    document.getElementById("encryptedOutput")
    .innerHTML = encrypted;

    speak("Pesan berhasil dirahasiakan");
}

// membuka pesan
function decryptMessage(){

    const key =
    document.getElementById("keyInput").value;

    if(key.toLowerCase() === secretKey){

        document.getElementById("realMessage")
        .innerHTML =
        "💌 Pesan Asli:<br><br>" + originalMessage;

        speak("Pesan berhasil dibuka");

    }else{

        document.getElementById("realMessage")
        .innerHTML =
        "❌ Kata kunci salah!";

        speak("Kata kunci salah");
    }
}

// speaker suara
function speak(text){

    const speech =
    new SpeechSynthesisUtterance(text);

    speech.lang = "id-ID";
    speech.rate = 1;

    window.speechSynthesis.speak(speech);
}

</script>

</body>
</html>
