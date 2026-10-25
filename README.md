# JARVIS-AI
My personal AI ASSISTANT 
<!DOCTYPE html><html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>JARVIS AI</title>
<style>
* { box-sizing: border-box; }
body {
  margin: 0;
  min-height: 100vh;
  background: #030811;
  color: #00d9ff;
  font-family: Arial, sans-serif;
  display: flex;
  flex-direction: column;
  align-items: center;
}
header {
  width: 100%;
  padding: 22px;
  text-align: center;
  border-bottom: 1px solid #06445e;
  letter-spacing: 5px;
}
h1 { text-shadow: 0 0 15px #00d9ff; }
#orb {
  width: 145px;
  height: 145px;
  margin: 35px auto 15px;
  border: 3px solid #00d9ff;
  border-radius: 50%;
  box-shadow: 0 0 25px #007caa, inset 0 0 25px #007caa;
  display: grid;
  place-items: center;
  animation: pulse 2s infinite alternate;
}
#orb span { font-size: 45px; }
@keyframes pulse {
  from { box-shadow: 0 0 15px #007caa; }
  to { box-shadow: 0 0 40px #00d9ff, inset 0 0 25px #007caa; }
}
#status { color: #8beaff; margin: 10px; }
#chat {
  width: 90%;
  max-width: 600px;
  height: 280px;
  overflow-y: auto;
  border: 1px solid #07506a;
  padding: 15px;
  border-radius: 12px;
  background: #07111e;
}
.message { margin: 12px 0; line-height: 1.5; overflow-wrap: anywhere; }
.user { color: white; }
.bot { color: #00d9ff; }
.controls {
  width: 90%;
  max-width: 600px;
  display: flex;
  gap: 8px;
  margin: 15px 0;
}
input {
  flex: 1;
  min-width: 0;
  padding: 14px;
  background: #07111e;
  border: 1px solid #00aaca;
  border-radius: 8px;
  color: white;
}
button {
  padding: 12px;
  background: #00374a;
  color: #00d9ff;
  border: 1px solid #00d9ff;
  border-radius: 8px;
}
footer { color: #7799aa; font-size: 12px; padding: 15px; }
</style>
</head>
<body>
<header>
  <h1>J.A.R.V.I.S</h1>
  <div>PERSONAL AI INTERFACE</div>
</header><div id="orb"><span>◉</span></div>
<div id="status">SYSTEM ONLINE · DEMO MODE</div><div id="chat" aria-live="polite">
  <div class="message bot">JARVIS: Hello! Welcome, sir. I am ready to assist you.</div>
  <div class="message bot">Note: My AI brain is not connected yet.</div>
</div><div class="controls">
  <input id="input" placeholder="Ask JARVIS something..." />
  <button onclick="sendMessage()">SEND</button>
</div>
<div class="controls">
  <button onclick="startVoice()">🎤 SPEAK</button>
  <button onclick="clearChat()">CLEAR CHAT</button>
</div>
<footer>JARVIS AI · Interface Demo · AI backend not connected</footer><script>
const input = document.getElementById('input');
const chat = document.getElementById('chat');
const statusText = document.getElementById('status');

function addMessage(who, text, cls) {
  const div = document.createElement('div');
  div.className = 'message ' + cls;
  div.textContent = who + ': ' + text;
  chat.appendChild(div);
  chat.scrollTop = chat.scrollHeight;
}

function sendMessage() {
  const text = input.value.trim();
  if (!text) return;
  addMessage('YOU', text, 'user');
  input.value = '';

  let reply = 'I received your message, sir. My AI brain is not connected yet.';

  if (/hello|hi|vanakkam/i.test(text)) {
    reply = 'Hello, sir! Welcome to JARVIS.';
  } else if (/your name|who are you/i.test(text)) {
    reply = 'I am JARVIS, your personal AI assistant interface.';
  } else if (/time|date/i.test(text)) {
    reply = 'Current device time: ' + new Date().toLocaleString();
  } else if (/tamil/i.test(text)) {
    reply = 'Vanakkam sir! Tamil support interface is ready. Real AI connection is still needed.';
  }

  setTimeout(() => addMessage('JARVIS', reply, 'bot'), 400);
}

input.addEventListener('keydown', e => {
  if (e.key === 'Enter') sendMessage();
});

function startVoice() {
  const SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;
  if (!SpeechRecognition) {
    statusText.textContent = 'Voice recognition is not supported in this browser.';
    return;
  }
  const recognition = new SpeechRecognition();
  recognition.lang = 'en-IN';
  recognition.onstart = () => statusText.textContent = 'LISTENING...';
  recognition.onresult = e => {
    input.value = e.results[0][0].transcript;
    sendMessage();
  };
  recognition.onerror = () => statusText.textContent = 'Voice input unavailable.';
  recognition.onend = () => statusText.textContent = 'SYSTEM ONLINE · DEMO MODE';
  recognition.start();
}

function clearChat() {
  chat.replaceChildren();
  addMessage('JARVIS', 'Chat cleared, sir.', 'bot');
}
</script></body>
</html>
