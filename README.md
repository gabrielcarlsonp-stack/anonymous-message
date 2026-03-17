# anonymous-message
<!DOCTYPE html>
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

        /* Header */
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

        /* Stats */
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

        /* Form */
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

        /* Filters */
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

        /* Messages */
        .messages-box {
            background: white;
            padding: 20px;
            border-radius: 8px;
            margin-bottom: 20px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
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

        /* Contact Section */
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
    </style>
</head>
<body>
    <div class="container">
        <!-- Header -->
        <div class="header">
            <h1>📝 Anonymous Message Board</h1>
            <p>Share your thoughts anonymously</p>
        </div>

        <!-- Stats -->
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

        <!-- Post Form -->
        <div class="form-box">
            <textarea id="messageInput" placeholder="Type your message here..." maxlength="500"></textarea>
            <div class="form-footer">
                <div>
                    <button class="clear-btn" onclick="clearInput()">Clear</button>
                    <button onclick="postMessage()">Post</button>
                </div>
                <span id="charCount">0/500</span>
            </div>
        </div>

        <!-- Filters -->
        <div class="filters">
            <button class="filter-btn active" onclick="filterMessages('all', this)">All</button>
            <button class="filter-btn" onclick="filterMessages('today', this)">Today</button>
            <button class="filter-btn" onclick="filterMessages('popular', this)">Popular</button>
        </div>

        <!-- Messages -->
        <div class="messages-box">
            <div id="messageList"></div>
        </div>

        <!-- Contact -->
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

    <script>
        // Initialize
        let messages = [];
        let currentFilter = 'all';

        // Load messages
        function loadMessages() {
            let saved = localStorage.getItem('messages');
            if (saved) {
                messages = JSON.parse(saved);
            } else {
                // Sample messages
                messages = [
                    {
                        id: 1,
                        text: "Hello! This is a sample message.",
                        time: new Date().toISOString(),
                        author: "Anon1234",
                        likes: 5
                    },
                    {
                        id: 2,
                        text: "Having a great day!",
                        time: new Date(Date.now() - 3600000).toISOString(),
                        author: "Anon5678",
                        likes: 3
                    }
                ];
                saveMessages();
            }
            updateAll();
        }

        // Save messages
        function saveMessages() {
            localStorage.setItem('messages', JSON.stringify(messages));
        }

        // Post message
        function postMessage() {
            let input = document.getElementById('messageInput');
            let text = input.value.trim();
            
            if (text === '') {
                alert('Please enter a message');
                return;
            }
            
            if (text.length > 500) {
                alert('Message too long');
                return;
            }
            
            // Create new message
            let newMessage = {
                id: Date.now(),
                text: text,
                time: new Date().toISOString(),
                author: 'Anon' + Math.floor(Math.random() * 10000),
                likes: 0
            };
            
            messages.unshift(newMessage);
            saveMessages();
            
            // Clear input
            input.value = '';
            document.getElementById('charCount').innerHTML = '0/500';
            
            updateAll();
            alert('Message posted!');
        }

        // Delete message
        function deleteMessage(id) {
            if (confirm('Delete this message?')) {
                messages = messages.filter(m => m.id !== id);
                saveMessages();
                updateAll();
            }
        }

        // Like message
        function likeMessage(id) {
            let message = messages.find(m => m.id === id);
            if (message) {
                message.likes++;
                saveMessages();
                updateAll();
            }
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

        // Update all
        function updateAll() {
            updateDisplay();
            updateStats();
        }

        // Update display
        function updateDisplay() {
            let list = document.getElementById('messageList');
            let filtered = [];
            
            // Apply filter
            if (currentFilter === 'all') {
                filtered = messages;
            } 
            else if (currentFilter === 'today') {
                let today = new Date().toDateString();
                filtered = messages.filter(m => {
                    return new Date(m.time).toDateString() === today;
                });
            }
            else if (currentFilter === 'popular') {
                filtered = [...messages].sort((a, b) => b.likes - a.likes);
            }
            
            // Show messages
            if (filtered.length === 0) {
                list.innerHTML = '<div class="empty-state">No messages to display</div>';
                return;
            }
            
            let html = '';
            for (let i = 0; i < filtered.length; i++) {
                let m = filtered[i];
                html += `
                    <div class="message">
                        <div class="message-text">${escapeHtml(m.text)}</div>
                        <div class="message-footer">
                            <div class="message-info">
                                <span class="message-id">${m.author}</span>
                                <span>${formatTime(m.time)}</span>
                            </div>
                            <div class="message-actions">
                                <button class="like-btn" onclick="likeMessage(${m.id})">❤️ ${m.likes}</button>
                                <button class="delete-btn" onclick="deleteMessage(${m.id})">🗑️</button>
                            </div>
                        </div>
                    </div>
                `;
            }
            
            list.innerHTML = html;
        }

        // Update stats
        function updateStats() {
            document.getElementById('totalMessages').innerHTML = messages.length;
            
            let today = new Date().toDateString();
            let todayCount = 0;
            for (let i = 0; i < messages.length; i++) {
                if (new Date(messages[i].time).toDateString() === today) {
                    todayCount++;
                }
            }
            document.getElementById('todayMessages').innerHTML = todayCount;
            
            let totalLikes = 0;
            for (let i = 0; i < messages.length; i++) {
                totalLikes += messages[i].likes;
            }
            document.getElementById('totalLikes').innerHTML = totalLikes;
        }

        // Format time
        function formatTime(timestamp) {
            let date = new Date(timestamp);
            let now = new Date();
            let diff = Math.floor((now - date) / 60000); // minutes
            
            if (diff < 1) return 'Just now';
            if (diff < 60) return diff + ' min ago';
            if (diff < 1440) return Math.floor(diff / 60) + ' hours ago';
            return date.toLocaleDateString();
        }

        // Escape HTML
        function escapeHtml(text) {
            return text
                .replace(/&/g, '&amp;')
                .replace(/</g, '&lt;')
                .replace(/>/g, '&gt;')
                .replace(/"/g, '&quot;')
                .replace(/'/g, '&#039;');
        }

        // Character counter
        document.getElementById('messageInput').addEventListener('input', function() {
            document.getElementById('charCount').innerHTML = this.value.length + '/500';
        });

        // Load on start
        loadMessages();

        // Check for updates from other tabs
        window.addEventListener('storage', function(e) {
            if (e.key === 'messages') {
                messages = JSON.parse(e.newValue);
                updateAll();
            }
        });
    </script>
</body>
</html>
