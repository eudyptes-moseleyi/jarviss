```html
<!DOCTYPE html>
<html lang="pt-PT">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>J.A.R.V.I.S.</title>

    <style>
        * {
            box-sizing: border-box;
        }

        body {
            margin: 0;
            min-height: 100vh;
            background:
                radial-gradient(circle at center, #0b2433 0%, #050b14 45%, #02050a 100%);
            color: #d8f7ff;
            font-family: Consolas, monospace;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        .container {
            width: min(850px, 94vw);
            height: min(850px, 94vh);
            display: flex;
            flex-direction: column;
            padding: 25px;
            border: 1px solid #0e3f4f;
            border-radius: 20px;
            background: rgba(5, 11, 20, 0.94);
            box-shadow:
                0 0 30px rgba(38, 224, 255, 0.12),
                inset 0 0 40px rgba(38, 224, 255, 0.03);
        }

        .title {
            text-align: center;
            color: #26e0ff;
            font-size: 36px;
            font-weight: bold;
            letter-spacing: 7px;
            text-shadow: 0 0 15px #26e0ff;
        }

        .subtitle {
            text-align: center;
            color: #0e7c91;
            font-size: 12px;
            letter-spacing: 5px;
            margin-top: 5px;
        }

        .core-area {
            height: 230px;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        .core {
            width: 145px;
            height: 145px;
            border: 2px solid #26e0ff;
            border-radius: 50%;
            display: flex;
            justify-content: center;
            align-items: center;
            position: relative;
            box-shadow:
                0 0 20px #26e0ff,
                inset 0 0 20px #26e0ff55;
            animation: pulse 2.5s infinite;
        }

        .core::before {
            content: "";
            position: absolute;
            width: 105px;
            height: 105px;
            border: 1px solid #26e0ff;
            border-radius: 50%;
        }

        .core::after {
            content: "";
            width: 45px;
            height: 45px;
            background: #26e0ff;
            border-radius: 50%;
            box-shadow:
                0 0 15px #26e0ff,
                0 0 40px #26e0ff;
        }

        @keyframes pulse {
            0%, 100% {
                transform: scale(1);
            }

            50% {
                transform: scale(1.08);
            }
        }

        .status {
            text-align: center;
            color: #26e0ff;
            font-size: 15px;
            font-weight: bold;
            margin-bottom: 15px;
            text-shadow: 0 0 8px #26e0ff;
        }

        .chat {
            flex: 1;
            overflow-y: auto;
            background: #081522;
            border: 1px solid #0e3f4f;
            border-radius: 12px;
            padding: 15px;
            margin-bottom: 15px;
        }

        .message {
            margin: 10px 0;
            padding: 9px 12px;
            border-radius: 8px;
            line-height: 1.5;
            word-wrap: break-word;
        }

        .user {
            color: #ffffff;
            background: #102332;
            border-left: 3px solid #ffffff;
        }

        .jarvis {
            color: #26e0ff;
            background: #09202b;
            border-left: 3px solid #26e0ff;
        }

        .error {
            color: #ff5c5c;
        }

        .controls {
            display: flex;
            gap: 8px;
        }

        #input {
            flex: 1;
            min-width: 0;
            padding: 13px;
            border: 1px solid #0e3f4f;
            border-radius: 9px;
            outline: none;
            background: #07111c;
            color: #d8f7ff;
            font-family: Consolas, monospace;
            font-size: 14px;
        }

        #input:focus {
            border-color: #26e0ff;
            box-shadow: 0 0 10px #26e0ff33;
        }

        button {
            border: none;
            border-radius: 9px;
            padding: 12px 16px;
            background: #26e0ff;
            color: #00131a;
            font-family: Consolas, monospace;
            font-weight: bold;
            cursor: pointer;
        }

        button:hover {
            filter: brightness(1.2);
        }

        #mic {
            min-width: 55px;
        }

        #mic.listening {
            background: #ff5c5c;
            color: white;
            animation: micPulse 1s infinite;
        }

        @keyframes micPulse {
            50% {
                box-shadow: 0 0 20px #ff5c5c;
            }
        }

        .commands {
            text-align: center;
            color: #506b78;
            font-size: 10px;
            margin-top: 10px;
        }

        @media (max-width: 600px) {
            .container {
                height: 96vh;
                padding: 15px;
            }

            .title {
                font-size: 26px;
            }

            .core-area {
                height: 180px;
            }

            .core {
                width: 110px;
                height: 110px;
            }

            .core::before {
                width: 80px;
                height: 80px;
            }

            .core::after {
                width: 32px;
                height: 32px;
            }

            .controls {
                flex-wrap: wrap;
            }

            #input {
                width: 100%;
                flex-basis: 100%;
            }
        }
    </style>
</head>

<body>

<div class="container">

    <div class="title">J.A.R.V.I.S.</div>

    <div class="subtitle">
        ASSISTENTE PESSOAL
    </div>

    <div class="core-area">
        <div class="core"></div>
    </div>

    <div id="status" class="status">
        SISTEMA EM ESPERA
    </div>

    <div id="chat" class="chat"></div>

    <div class="controls">

        <input
            id="input"
            type="text"
            placeholder="Fala comigo ou escreve uma pergunta..."
            autocomplete="off"
        >

        <button id="send">
            ENVIAR
        </button>

        <button id="mic">
            🎙️
        </button>

    </div>

    <div class="commands">
        Comandos: horas · data · pesquisa · Google · YouTube · piada · ajuda
    </div>

</div>

<script>

const chat = document.getElementById("chat");
const input = document.getElementById("input");
const send = document.getElementById("send");
const mic = document.getElementById("mic");
const status = document.getElementById("status");


// ----------------------------------------------------
// CHAT
// ----------------------------------------------------

function adicionarMensagem(remetente, texto, classe) {

    const mensagem = document.createElement("div");

    mensagem.className = "message " + classe;

    mensagem.innerHTML =
        "<strong>" + remetente + ":</strong> " +
        escapeHTML(texto);

    chat.appendChild(mensagem);

    chat.scrollTop = chat.scrollHeight;
}


function escapeHTML(texto) {

    const div = document.createElement("div");

    div.textContent = texto;

    return div.innerHTML;
}


// ----------------------------------------------------
// VOZ
// ----------------------------------------------------

function falar(texto) {

    if (!("speechSynthesis" in window)) {
        return;
    }

    speechSynthesis.cancel();

    const voz = new SpeechSynthesisUtterance(texto);

    voz.lang = "pt-PT";
    voz.rate = 0.95;
    voz.pitch = 1;

    speechSynthesis.speak(voz);
}


// ----------------------------------------------------
// RESPOSTA
// ----------------------------------------------------

function responder(texto) {

    adicionarMensagem(
        "JARVIS",
        texto,
        "jarvis"
    );

    falar(texto);
}


// ----------------------------------------------------
// DATA
// ----------------------------------------------------

function obterData() {

    return new Date().toLocaleDateString(
        "pt-PT",
        {
            weekday: "long",
            day: "numeric",
            month: "long",
            year: "numeric"
        }
    );
}


// ----------------------------------------------------
// HORA
// ----------------------------------------------------

function obterHora() {

    return new Date().toLocaleTimeString(
        "pt-PT",
        {
            hour: "2-digit",
            minute: "2-digit"
        }
    );
}


// ----------------------------------------------------
// COMANDOS
// ----------------------------------------------------

function processarComando(comando) {

    comando = comando.trim();

    if (!comando) {
        return;
    }

    adicionarMensagem(
        "TU",
        comando,
        "user"
    );

    input.value = "";

    status.textContent = "A PROCESSAR...";

    const texto = comando.toLowerCase();


    // SAIR

    if (
        texto.includes("sair") ||
        texto.includes("adeus") ||
        texto.includes("desligar")
    ) {

        responder("Até já.");

        status.textContent = "SISTEMA EM ESPERA";

        return;
    }


    // HORA

    if (
        texto.includes("hora") ||
        texto.includes("horas")
    ) {

        responder(
            "São " + obterHora() + "."
        );

        status.textContent = "SISTEMA EM ESPERA";

        return;
    }


    // DATA

    if (
        texto.includes("data") ||
        texto.includes("dia é hoje") ||
        texto.includes("dia de hoje")
    ) {

        responder(
            "Hoje é " + obterData() + "."
        );

        status.textContent = "SISTEMA EM ESPERA";

        return;
    }


    // YOUTUBE

    if (
        texto.includes("youtube") ||
        texto.includes("abre o youtube") ||
        texto.includes("abrir youtube")
    ) {

        window.open(
            "https://www.youtube.com/",
            "_blank"
        );

        responder(
            "A abrir o YouTube."
        );

        status.textContent = "SISTEMA EM ESPERA";

        return;
    }


    // GOOGLE

    if (
        texto === "google" ||
        texto.includes("abre o google") ||
        texto.includes("abrir google")
    ) {

        window.open(
            "https://www.google.com/",
            "_blank"
        );

        responder(
            "A abrir o Google."
        );

        status.textContent = "SISTEMA EM ESPERA";

        return;
    }


    // PESQUISA

    if (
        texto.includes("pesquisa") ||
        texto.includes("pesquisar") ||
        texto.includes("procura")
    ) {

        let pesquisa = comando
            .replace(/pesquisa/gi, "")
            .replace(/pesquisar/gi, "")
            .replace(/procura/gi, "")
            .replace(/no google/gi, "")
            .trim();


        if (!pesquisa) {

            responder(
                "O que queres que eu pesquise?"
            );

        } else {

            window.open(
                "https://www.google.com/search?q=" +
                encodeURIComponent(pesquisa),
                "_blank"
            );

            responder(
                "A pesquisar " +
                pesquisa +
                " no Google."
            );
        }

        status.textContent = "SISTEMA EM ESPERA";

        return;
    }


    // PIADA

    if (texto.includes("piada")) {

        responder(
            "Porque é que o computador foi ao médico? Porque tinha um vírus."
        );

        status.textContent = "SISTEMA EM ESPERA";

        return;
    }


    // AJUDA

    if (
        texto.includes("ajuda") ||
        texto.includes("comandos")
    ) {

        responder(
            "Posso dizer-te as horas e a data, pesquisar no Google, abrir o YouTube e o Google, contar uma piada e ouvir comandos por voz."
        );

        status.textContent = "SISTEMA EM ESPERA";

        return;
    }


    // OLÁ

    if (
        texto === "olá" ||
        texto === "ola" ||
        texto.includes("bom dia") ||
        texto.includes("boa tarde") ||
        texto.includes("boa noite")
    ) {

        responder(
            "Olá. Eu sou o JARVIS. Como posso ajudar?"
        );

        status.textContent = "SISTEMA EM ESPERA";

        return;
    }


    // RESPOSTA PADRÃO

    responder(
        "Ainda não tenho uma resposta de inteligência artificial ligada ao site. Posso executar os comandos disponíveis. Diz ajuda para veres o que consigo fazer."
    );

    status.textContent = "SISTEMA EM ESPERA";
}


// ----------------------------------------------------
// BOTÃO ENVIAR
// ----------------------------------------------------

send.addEventListener(
    "click",
    function () {

        processarComando(
            input.value
        );

    }
);


// ----------------------------------------------------
// ENTER
// ----------------------------------------------------

input.addEventListener(
    "keydown",
    function (evento) {

        if (evento.key === "Enter") {

            processarComando(
                input.value
            );

        }

    }
);


// ----------------------------------------------------
// RECONHECIMENTO DE VOZ
// ----------------------------------------------------

const SpeechRecognition =
    window.SpeechRecognition ||
    window.webkitSpeechRecognition;


let reconhecimento = null;


if (SpeechRecognition) {

    reconhecimento =
        new SpeechRecognition();

    reconhecimento.lang = "pt-PT";

    reconhecimento.interimResults = false;

    reconhecimento.continuous = false;


    reconhecimento.onstart = function () {

        status.textContent =
            "A OUVIR...";

        mic.classList.add(
            "listening"
        );

    };


    reconhecimento.onend = function () {

        status.textContent =
            "SISTEMA EM ESPERA";

        mic.classList.remove(
            "listening"
        );

    };


    reconhecimento.onerror = function () {

        status.textContent =
            "ERRO NO MICROFONE";

        mic.classList.remove(
            "listening"
        );

    };


    reconhecimento.onresult =
        function (evento) {

            const texto =
                evento.results[0][0].transcript;

            processarComando(
                texto
            );

        };


    mic.addEventListener(
        "click",
        function () {

            try {

                reconhecimento.start();

            } catch (erro) {

                console.log(erro);

            }

        }
    );

} else {

    mic.disabled = true;

    mic.title =
        "O teu navegador não suporta reconhecimento de voz.";

}


// ----------------------------------------------------
// MENSAGEM INICIAL
// ----------------------------------------------------

adicionarMensagem(
    "JARVIS",
    "Boa noite. Eu sou o JARVIS. Como posso ajudar?",
    "jarvis"
);

</script>

</body>
</html>
```
