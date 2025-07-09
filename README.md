# Live-chat
Online friend chat
<!DOCTYPE html>
<html>
<head>
  <title>🔥Simple Chat App</title>
  <style>
    body { font-family: Arial; background: #f2f2f2; padding: 20px; text-align: center; }
    #messages { max-width: 600px; margin: 20px auto; background: #fff; border: 1px solid #ccc; padding: 10px; height: 300px; overflow-y: scroll; text-align: left; }
    input, button { padding: 10px; margin: 5px; border-radius: 5px; border: 1px solid #ccc; }
    input { width: 200px; }
    button { background-color: #4CAF50; color: white; border: none; }
  </style>
</head>
<body>
  <h1>🔥Simple Chat</h1>
  <div id="messages"></div>
  <input id="username" placeholder="Your name">
  <input id="message" placeholder="Type a message">
  <button onclick="sendMessage()">Send</button>

  <!-- Firebase SDK -->
  <script src="https://www.gstatic.com/firebasejs/8.10.1/firebase-app.js"></script>
  <script src="https://www.gstatic.com/firebasejs/8.10.1/firebase-database.js"></script>

  <script>
    // 🛠️ Replace with your own Firebase config
    const firebaseConfig = {
      apiKey: "YOUR_API_KEY",
      authDomain: "YOUR_PROJECT_ID.firebaseapp.com",
      databaseURL: "https://YOUR_PROJECT_ID.firebaseio.com",
      projectId: "YOUR_PROJECT_ID",
      storageBucket: "YOUR_PROJECT_ID.appspot.com",
      messagingSenderId: "YOUR_SENDER_ID",
      appId: "YOUR_APP_ID"
    };

    firebase.initializeApp(firebaseConfig);
    const db = firebase.database();

    // Send Message
    function sendMessage() {
      const username = document.getElementById('username').value.trim();
      const message = document.getElementById('message').value.trim();
      if (username && message) {
        db.ref('messages').push({ name: username, text: message });
        document.getElementById('message').value = '';
      }
    }

    // Display Messages
    db.ref('messages').on('value', function(snapshot) {
      const messagesDiv = document.getElementById('messages');
      messagesDiv.innerHTML = '';
      snapshot.forEach(function(childSnapshot) {
        const data = childSnapshot.val();
        const msg = `<p><strong>${data.name}:</strong> ${data.text}</p>`;
        messagesDiv.innerHTML += msg;
      });
      messagesDiv.scrollTop = messagesDiv.scrollHeight;
    });
  </script>
</body>
</html>
