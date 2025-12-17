<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8" />
  <title>IA Apprenante Simple</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #111827;
      color: #f9fafb;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
    }
    .chatbox {
      width: 400px;
      background: #1f2933;
      border-radius: 12px;
      padding: 16px;
      box-shadow: 0 10px 30px rgba(0,0,0,0.4);
    }
    .messages {
      height: 300px;
      overflow-y: auto;
      margin-bottom: 10px;
    }
    .msg {
      margin: 6px 0;
    }
    .user { color: #60a5fa; }
    .bot { color: #34d399; }
    input {
      width: 100%;
      padding: 8px;
      border-radius: 8px;
      border: none;
      outline: none;
    }
  </style>
</head>
<body>
  <div class="chatbox">
    <div class="messages" id="messages"></div>
    <input type="text" id="input" placeholder="Parle à l'IA et appuie sur Entrée..." />
  </div>

  <script>
    const input = document.getElementById("input");
    const messages = document.getElementById("messages");

    // Mémoire locale (apprentissage simple)
    let memory = JSON.parse(localStorage.getItem("ia_memory")) || {};

    function addMessage(text, sender) {
      const div = document.createElement("div");
      div.className = "msg " + sender;
      div.textContent = text;
      messages.appendChild(div);
      messages.scrollTop = messages.scrollHeight;
    }

    function getResponse(text) {
      const lower = text.toLowerCase();

      if (memory[lower]) {
        return memory[lower];
      }

      return "Je ne sais pas encore répondre à ça. Apprends-moi en répondant 🙂";
    }

    input.addEventListener("keydown", (e) => {
      if (e.key === "Enter" && input.value.trim() !== "") {
        const userText = input.value.trim();
        addMessage("Toi : " + userText, "user");

        const response = getResponse(userText);
        addMessage("IA : " + response, "bot");

        // Si l'IA ne sait pas, elle apprend à la prochaine réponse
        if (response.startsWith("Je ne sais pas")) {
          setTimeout(() => {
            const teach = prompt("Quelle réponse dois-je donner à : \"" + userText + "\" ?");
            if (teach) {
              memory[userText.toLowerCase()] = teach;
              localStorage.setItem("ia_memory", JSON.stringify(memory));
              addMessage("IA : Merci ! J'ai appris quelque chose de nouveau 🤖", "bot");
            }
          }, 200);
        }

        input.value = "";
      }
    });

    addMessage("IA : Bonjour ! Je peux apprendre de toi.", "bot");
  </script>
</body>
</html>
