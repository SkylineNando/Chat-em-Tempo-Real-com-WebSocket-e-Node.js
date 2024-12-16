# Chat em Tempo Real com WebSocket e Node.js

Um projeto de chat em tempo real usando **HTML**, **CSS**, **JavaScript** e **Node.js** com **WebSocket** para comunicação em tempo real.

---

## 🚀 **Funcionalidades**

- **Apelido do Usuário**: Antes de entrar no chat, o usuário pode definir um apelido.
- **Mensagens em Tempo Real**: Envio e recebimento de mensagens em tempo real entre múltiplos usuários conectados.
- **Interface Simples**: Interface amigável e responsiva para a interação do usuário.
- **Servidor WebSocket**: Servidor em Node.js para gerenciar conexões WebSocket.

---

## 🛠️ **Tecnologias Utilizadas**

- **Frontend**:
  - HTML5
  - CSS3
  - JavaScript (ES6)
  - WebSocket API

- **Backend**:
  - Node.js
  - WebSocket (ws)

---

## 📁 **Estrutura do Projeto**

```
chat-realtime/
│-- index.html
│-- server.js
└-- README.md
```

- **`index.html`**: Interface do usuário para o chat.
- **`server.js`**: Servidor WebSocket em Node.js.
- **`README.md`**: Documentação do projeto.

---

## 💻 **Instalação e Execução**

### 1. **Clone o Repositório**

```bash
git clone https://github.com/Skylinenando/chat-realtime.git
cd chat-realtime
```

### 2. **Instale as Dependências**

```bash
npm install ws
```

### 3. **Execute o Servidor**

```bash
node server.js
```

### 4. **Abra o Chat no Navegador**

Acesse o seguinte link no seu navegador:

```
http://localhost:8080
```

---

## 🔧 **Configuração do WebSocket**

O servidor WebSocket é configurado para rodar na porta `8080`. Se desejar alterar a porta, edite o arquivo `server.js`:

```javascript
const wss = new WebSocket.Server({ port: 8080 });
```

---

## 📜 **Código de Exemplo**

### **Frontend (`index.html`)**

```html
<!DOCTYPE html>
<html lang="pt-br">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Chat em Tempo Real</title>
  <style>
    body { font-family: Arial, sans-serif; margin: 0; padding: 20px; background-color: #f4f4f4; }
    #chat { max-width: 500px; margin: 0 auto; border: 1px solid #ccc; border-radius: 5px; background: #fff; display: flex; flex-direction: column; height: 500px; }
    #messages { flex: 1; padding: 10px; overflow-y: scroll; border-bottom: 1px solid #ccc; }
    #message-input { display: flex; }
    #message-input input { flex: 1; padding: 10px; border: none; border-top: 1px solid #ccc; }
    #message-input button { padding: 10px; border: none; background: #28a745; color: #fff; cursor: pointer; }
  </style>
</head>
<body>

  <h2>Chat em Tempo Real</h2>
  <div id="chat">
    <div id="messages"></div>
    <div id="message-input">
      <input type="text" id="input" placeholder="Digite sua mensagem..." />
      <button onclick="sendMessage()">Enviar</button>
    </div>
  </div>

  <script>
    const ws = new WebSocket('ws://localhost:8080');
    const messagesDiv = document.getElementById('messages');
    const input = document.getElementById('input');

    ws.onmessage = (event) => {
      const messageElement = document.createElement('div');
      messageElement.textContent = event.data;
      messagesDiv.appendChild(messageElement);
      messagesDiv.scrollTop = messagesDiv.scrollHeight;
    };

    function sendMessage() {
      if (input.value.trim()) {
        ws.send(input.value);
        input.value = '';
      }
    }
  </script>

</body>
</html>
```

### **Backend (`server.js`)**

```javascript
const WebSocket = require('ws');
const wss = new WebSocket.Server({ port: 8080 });

wss.on('connection', (ws) => {
  console.log('Novo cliente conectado');

  ws.on('message', (message) => {
    console.log(`Mensagem recebida: ${message}`);
    wss.clients.forEach((client) => {
      if (client.readyState === WebSocket.OPEN) {
        client.send(message);
      }
    });
  });

  ws.on('close', () => {
    console.log('Cliente desconectado');
  });
});

console.log('Servidor WebSocket rodando em ws://localhost:8080');
```

---

## 🌐 **Hospedagem no GitHub Pages**

Se você deseja hospedar apenas o frontend (`index.html`) no **GitHub Pages**:

1. **Faça o push do repositório** para o GitHub.
2. Vá até **Configurações > GitHub Pages**.
3. Selecione a branch `main` ou `master` e clique em **Save**.
4. Acesse o seu site em:

   ```
   https://Skylinenando.github.io/chat-realtime
   ```

> **Nota**: O servidor WebSocket (`server.js`) precisa rodar em um servidor Node.js separado, pois o GitHub Pages não suporta Node.js.

---

## 🤝 **Contribuição**

Sinta-se à vontade para contribuir com melhorias para este projeto! Abra uma **issue** ou envie um **pull request**.

---

## 📄 **Licença**

Este projeto está licenciado sob a **MIT License**. Consulte o arquivo [LICENSE](LICENSE) para mais informações.

---

## 📞 **Contato**

- **GitHub**: [Skylinenando](https://github.com/Skylinenando)

---

Espero que essa documentação esteja clara e útil para o seu projeto! Se precisar de mais ajustes, estou à disposição. 😊🚀
