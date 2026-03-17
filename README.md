
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Anonymous Message Board</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: Arial, sans-serif;
        }

        body {
            background: #f0f2f5;
            padding: 20px;
        }

        .container {
            max-width: 800px;
            margin: 0 auto;
        }

        .header {
            background: white;
            padding: 20px;
            border-radius: 8px;
            margin-bottom: 20px;
            text-align: center;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
        }

        .header h1 {
            color: #1a73e8;
            margin-bottom: 10px;
        }

        .online-users {
            background: #e8f5e9;
            color: #2e7d32;
            padding: 5px 15px;
            border-radius: 20px;
            display: inline-block;
            font-size: 14px;
            margin-top: 10px;
        }

        .stats {
            display: flex;
            gap: 10px;
            margin-bottom: 20px;
        }

        .stat-box {
            background: white;
            padding: 15px;
            border-radius: 8px;
            flex: 1;
            text-align: center;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
        }

        .stat-number {
            font-size: 24px;
            font-weight: bold;
            color: #1a73e8;
        }

        .form-box {
            background: white;
            padding: 20px;
            border-radius: 8px;
            margin-bottom: 20px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
        }

        textarea {
            width: 100%;
            height: 100px;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 4px;
            margin-bottom: 10px;
            font-size: 14px;
            resize: vertical;
        }

        textarea:focus {
            outline: none;
            border-color: #1a73e8;
        }

        .form-footer {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        button {
            background: #1a73e8;
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 4px;
            cursor: pointer;
            font-size: 14px;
        }

        button:hover {
            background: #1557b0;
        }

        .clear-btn {
            background: #6c757d;
        }

        .filters {
            background: white;
            padding: 15px;
            border-radius: 8px;
            margin-bottom: 20px;
            display: flex;
            gap: 10px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
        }

        .filter-btn {
            background: #e9ecef;
            color: #333;
            border: none;
            padding: 8px 16px;
            border-radius: 4px;
            cursor: pointer;
        }

        .filter-btn.active {
            background: #1a73e8;
            color: white;
        }

        .messages-box {
            background: white;
            padding: 20px;
            border-radius: 8px;
            margin-bottom: 20px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
            min-height: 200px;
        }

        .message {
            background: #f8f9fa;
            padding: 15px;
            margin-bottom: 10px;
            border-radius: 4px;
            border-left: 3px solid #1a73e8;
        }

        .message-text {
            margin-bottom: 10px;
            word-wrap: break-word;
        }

        .message-footer {
            display: flex;
            justify-content: space-between;
            align-items: center;
            font-size: 12px;
            color: #666;
        }

        .message-info {
            display: flex;
            gap: 10px;
        }

        .message-id {
            background: #e9ecef;
            padding: 2px 8px;
            border-radius: 4px;
        }

        .message-actions {
            display: flex;
            gap: 5px;
        }

        .like-btn, .delete-btn {
            background: none;
            border: none;
            cursor: pointer;
            padding: 2px 5px;
            font-size: 12px;
        }

        .like-btn {
            color: #dc3545;
        }

        .delete-btn {
            color: #6c757d;
        }

        .empty-state {
            text-align: center;
            padding: 40px;
            color: #999;
        }

        .contact {
            background: white;
            padding: 20px;
            border-radius: 8px;
            text-align: center;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
        }

        .facebook-link {
            display: inline-block;
            background: #1877f2;
            color: white;
            text-decoration: none;
            padding: 10px 20px;
            border-radius: 4px;
            margin: 10px 0;
        }

        .copyright {
            color: #666;
            font-size: 12px;
            margin-top: 10px;
            padding-top: 10px;
            border-top: 1px solid #eee;
        }

        .loading {
            text-align: center;
            padding: 40px;
            color: #666;
        }

        .error-message {
            background: #ffebee;
            color: #c62828;
            padding: 10px;
            border-radius: 4px;
            margin-bottom: 10px;
            text-align: center;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>📝 Anonymous Message Board</h1>
            <p>Share your thoughts anonymously</p>
            <div class="online-users" id="onlineUsers">🟢 0 users online</div>
        </div>

        <div class="stats">
            <div class="stat-box">
                <div class="stat-number" id="totalMessages">0</div>
                <div>Total Messages</div>
            </div>
            <div class="stat-box">
                <div class="stat-number" id="todayMessages">0</div>
                <div>Today</div>
            </div>
            <div class="stat-box">
                <div class="stat-number" id="totalLikes">0</div>
                <div>Total Likes</div>
            </div>
        </div>

        <div class="form-box">
            <div id="errorDisplay" class="error-message" style="display: none;"></div>
            <textarea id="messageInput" placeholder="Type your message here..." maxlength="500"></textarea>
            <div class="form-footer">
                <div>
                    <button class="clear-btn" onclick="clearInput()">Clear</button>
                    <button onclick="postMessage()" id="postBtn">Post Message</button>
                </div>
                <span id="charCount">0/500</span>
            </div>
        </div>

        <div class="filters">
            <button class="filter-btn active" onclick="filterMessages('all', this)">All Messages</button>
            <button class="filter-btn" onclick="filterMessages('today', this)">Today's Messages</button>
            <button class="filter-btn" onclick="filterMessages('popular', this)">Most Liked</button>
        </div>

        <div class="messages-box">
            <div id="messageList">
                <div class="loading">Loading messages...</div>
            </div>
        </div>

        <div class="contact">
            <h3>Contact Information</h3>
            <a href="https://www.facebook.com/share/17RCyCLQHs/" target="_blank" class="facebook-link">
                📘 Facebook Page
            </a>
            <p>Please report any bugs or glitches you encounter.</p>
            <div class="copyright">
                © 2026 All Rights Reserved
            </div>
        </div>
    </div>

    <!-- Firebase SDK -->
    <script src="https://www.gstatic.com/firebasejs/8.10.1/firebase-app.js"></script>
    <script src="https://www.gstatic.com/firebasejs/8.10.1/firebase-database.js"></script>

    <script>
        // Your web app's Firebase configuration
        const firebaseConfig = {
            apiKey: "AIzaSyDy1xqI7QqzLrU8F9W9W9W9W9W9W9W9W9W9",
            authDomain: "anonymous-board-12345.firebaseapp.com",
            databaseURL: "https://anonymous-board-12345-default-rtdb.firebaseio.com",
            projectId: "anonymous-board-12345",
            storageBucket: "anonymous-board-12345.appspot.com",
            messagingSenderId: "123456789012",
            appId: "1:123456789012:web:abc123def456ghi789"
        };

        // Initialize Firebase with error handling
        let database;
        try {
            firebase.initializeApp(firebaseConfig);
            database = firebase.database();
            console.log("Firebase initialized successfully");
        } catch (error) {
            console.error("Firebase initialization error:", error);
            showError("Failed to connect to database. Please refresh the page.");
        }

        // Global variables
        let messages = [];
        let currentFilter = 'all';
        let userId = 'user_' + Math.floor(Math.random() * 1000000);

        // Show error message
        function showError(message) {
            const errorDiv = document.getElementById('errorDisplay');
            errorDiv.style.display = 'block';
            errorDiv.textContent = message;
            setTimeout(() => {
                errorDiv.style.display = 'none';
            }, 5000);
        }

        // Load messages from Firebase
        function loadMessages() {
            if (!database) {
                showError("Database not connected");
                return;
            }

            database.ref('messages').on('value', (snapshot) => {
                const data = snapshot.val();
                console.log("Data received:", data);
                
                if (data) {
                    // Convert object to array
                    messages = Object.keys(data).map(key => ({
                        id: key,
                        ...data[key]
                    }));
                    // Sort by timestamp (newest first)
                    messages.sort((a, b) => b.timestamp - a.timestamp);
                } else {
                    messages = [];
                }
                
                updateDisplay();
                updateStats();
            }, (error) => {
                console.error("Firebase error:", error);
                showError("Failed to load messages. Please refresh.");
            });
        }

        // Post message
        function postMessage() {
            const input = document.getElementById('messageInput');
            const text = input.value.trim();
            
            if (!database) {
                showError("Database not connected");
                return;
            }
            
            if (text === '') {
                showError('Please enter a message');
                return;
            }
            
            if (text.length > 500) {
                showError('Message too long (max 500 characters)');
                return;
            }

            // Disable post button temporarily
            const postBtn = document.getElementById('postBtn');
            postBtn.disabled = true;
            postBtn.textContent = 'Posting...';

            const newMessage = {
                text: text,
                author: 'Anon' + Math.floor(Math.random() * 10000),
                likes: 0,
                timestamp: Date.now(),
                time: new Date().toISOString()
            };

            console.log("Posting message:", newMessage);

            // Save to Firebase
            database.ref('messages').push(newMessage)
                .then(() => {
                    console.log("Message posted successfully");
                    input.value = '';
                    document.getElementById('charCount').innerHTML = '0/500';
                    postBtn.disabled = false;
                    postBtn.textContent = 'Post Message';
                })
                .catch((error) => {
                    console.error("Error posting message:", error);
                    showError('Error posting message. Please try again.');
                    postBtn.disabled = false;
                    postBtn.textContent = 'Post Message';
                });
        }

        // Delete message
        function deleteMessage(id) {
            if (!database) {
                showError("Database not connected");
                return;
            }
            
            if (confirm('Delete this message?')) {
                database.ref('messages/' + id).remove()
                    .then(() => {
                        console.log("Message deleted successfully");
                    })
                    .catch((error) => {
                        console.error("Error deleting message:", error);
                        showError('Error deleting message');
                    });
            }
        }

        // Like message
        function likeMessage(id) {
            if (!database) {
                showError("Database not connected");
                return;
            }
            
            const messageRef = database.ref('messages/' + id);
            messageRef.once('value', (snapshot) => {
                const message = snapshot.val();
                if (message) {
                    messageRef.update({
                        likes: (message.likes || 0) + 1
                    }).catch((error) => {
                        console.error("Error liking message:", error);
                        showError('Error liking message');
                    });
                }
            });
        }

        // Clear input
        function clearInput() {
            document.getElementById('messageInput').value = '';
            document.getElementById('charCount').innerHTML = '0/500';
        }

        // Filter messages
        function filterMessages(filter, element) {
            currentFilter = filter;
            
            // Update active button
            document.querySelectorAll('.filter-btn').forEach(btn => {
                btn.classList.remove('active');
            });
            element.classList.add('active');
            
            updateDisplay();
        }

        // Update display
        function updateDisplay() {
            const list = document.getElementById('messageList');
            
            if (!messages || messages.length === 0) {
                list.innerHTML = '<div class="empty-state">No messages yet. Be the first to post!</div>';
                return;
            }

            // Apply filter
            let filteredMessages = [...messages];
            
            if (currentFilter === 'today') {
                const today = new Date().toDateString();
                filteredMessages = messages.filter(m => {
                    return m.time && new Date(m.time).toDateString() === today;
                });
            } else if (currentFilter === 'popular') {
                filteredMessages = [...messages].sort((a, b) => (b.likes || 0) - (a.likes || 0));
            }
            
            if (filteredMessages.length === 0) {
                list.innerHTML = '<div class="empty-state">No messages in this filter</div>';
                return;
            }
            
            let html = '';
            filteredMessages.forEach(message => {
                html += `
                    <div class="message">
                        <div class="message-text">${escapeHtml(message.text || '')}</div>
                        <div class="message-footer">
                            <div class="message-info">
                                <span class="message-id">${escapeHtml(message.author || 'Anonymous')}</span>
                                <span>${formatTime(message.time)}</span>
                            </div>
                            <div class="message-actions">
                                <button class="like-btn" onclick="likeMessage('${message.id}')">❤️ ${message.likes || 0}</button>
                                <button class="delete-btn" onclick="deleteMessage('${message.id}')">🗑️</button>
                            </div>
                        </div>
                    </div>
                `;
            });
            
            list.innerHTML = html;
        }

        // Update stats
        function updateStats() {
            document.getElementById('totalMessages').innerHTML = messages.length;
            
            const today = new Date().toDateString();
            const todayCount = messages.filter(m => {
                return m.time && new Date(m.time).toDateString() === today;
            }).length;
            document.getElementById('todayMessages').innerHTML = todayCount;
            
            const totalLikes = messages.reduce((sum, m) => sum + (m.likes || 0), 0);
            document.getElementById('totalLikes').innerHTML = totalLikes;
        }

        // Format time
        function formatTime(timestamp) {
            if (!timestamp) return 'Unknown';
            
            const date = new Date(timestamp);
            const now = new Date();
            const diff = Math.floor((now - date) / 60000);
            
            if (diff < 1) return 'Just now';
            if (diff < 60) return diff + ' min ago';
            if (diff < 1440) return Math.floor(diff / 60) + ' hours ago';
            return date.toLocaleDateString();
        }

        // Escape HTML
        function escapeHtml(text) {
            if (!text) return '';
            const div = document.createElement('div');
            div.textContent = text;
            return div.innerHTML;
        }

        // Character counter
        document.getElementById('messageInput').addEventListener('input', function() {
            document.getElementById('charCount').innerHTML = this.value.length + '/500';
        });

        // Enter key to post
        document.getElementById('messageInput').addEventListener('keydown', function(e) {
            if (e.key === 'Enter' && !e.shiftKey) {
                e.preventDefault();
                postMessage();
            }
        });

        // Track online users
        function updateOnlineStatus() {
            if (!database) return;
            
            const userRef = database.ref('online/' + userId);
            
            userRef.set({
                online: true,
                lastSeen: Date.now()
            });

            window.addEventListener('beforeunload', () => {
                userRef.remove();
            });

            database.ref('online').on('value', (snapshot) => {
                const users = snapshot.val();
                const count = users ? Object.keys(users).length : 0;
                document.getElementById('onlineUsers').innerHTML = `🟢 ${count} users online`;
            });
        }

        // Initialize
        if (database) {
            loadMessages();
            updateOnlineStatus();
        } else {
            document.getElementById('messageList').innerHTML = '<div class="error-message">Failed to connect to database. Please refresh the page.</div>';
        }
    </script>
</body>
</html>
