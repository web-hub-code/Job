<html lang="ur" dir="ltr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vestify Pro - Online Job Hub & Realtime Feed</title>
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;700&display=swap" rel="stylesheet">
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --primary-color: #0f172a;
            --accent-color: #10b981;
            --bg-color: #f8fafc;
            --card-bg: #ffffff;
            --text-color: #334155;
            --border-color: #e2e8f0;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Poppins', sans-serif;
        }

        body {
            background-color: var(--bg-color);
            color: var(--text-color);
            line-height: 1.6;
            padding-bottom: 50px;
        }

        header {
            background: var(--primary-color);
            color: #fff;
            padding: 20px;
            text-align: center;
            box-shadow: 0 4px 6px -1px rgba(0,0,0,0.1);
        }

        header h1 {
            font-size: 24px;
            color: var(--accent-color);
            margin-bottom: 5px;
        }

        header p {
            font-size: 14px;
            color: #94a3b8;
        }

        .container {
            max-width: 800px;
            margin: 20px auto;
            padding: 0 15px;
        }

        /* Admin Panel Styling */
        .admin-card {
            background: var(--card-bg);
            border: 2px dashed var(--accent-color);
            padding: 20px;
            border-radius: 12px;
            margin-bottom: 30px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.05);
        }

        .admin-card h2 {
            font-size: 18px;
            margin-bottom: 15px;
            color: var(--primary-color);
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .form-group {
            margin-bottom: 12px;
        }

        .form-group input, .form-group textarea {
            width: 100%;
            padding: 10px 14px;
            border: 1px solid var(--border-color);
            border-radius: 8px;
            font-size: 14px;
            outline: none;
            transition: border-color 0.3s;
        }

        .form-group input:focus, .form-group textarea:focus {
            border-color: var(--accent-color);
        }

        .form-group textarea {
            resize: vertical;
            height: 80px;
        }

        .btn {
            background: var(--accent-color);
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 8px;
            font-size: 14px;
            font-weight: 600;
            cursor: pointer;
            width: 100%;
            transition: opacity 0.2s;
        }

        .btn:hover {
            opacity: 0.9;
        }

        /* Feed Posts Styling */
        .feed-title {
            font-size: 20px;
            margin-bottom: 15px;
            color: var(--primary-color);
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .post-card {
            background: var(--card-bg);
            border: 1px solid var(--border-color);
            border-radius: 12px;
            padding: 20px;
            margin-bottom: 20px;
            box-shadow: 0 4px 6px -1px rgba(0,0,0,0.02);
            transition: transform 0.2s;
        }

        .post-card:hover {
            transform: translateY(-2px);
        }

        .post-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 10px;
        }

        .post-title {
            font-size: 18px;
            font-weight: 700;
            color: var(--primary-color);
        }

        .post-time {
            font-size: 12px;
            color: #64748b;
        }

        .post-desc {
            font-size: 14px;
            color: #475569;
            margin-bottom: 15px;
            white-space: pre-line;
        }

        .post-link {
            display: inline-flex;
            align-items: center;
            gap: 6px;
            background: #eff6ff;
            color: #2563eb;
            padding: 8px 14px;
            border-radius: 6px;
            text-decoration: none;
            font-size: 13px;
            font-weight: 600;
        }

        .post-link:hover {
            background: #dbeafe;
        }

        .no-posts {
            text-align: center;
            color: #64748b;
            padding: 40px;
            background: var(--card-bg);
            border-radius: 12px;
            border: 1px solid var(--border-color);
        }
    </style>
</head>
<body>

    <header>
        <h1><i class="fa-solid fa-globe"></i> Vestify Pro Job Hub</h1>
        <p>Live Realtime Updates & Earning Links Feed</p>
    </header>

    <div class="container">
        <!-- Eagle Eye Admin Panel -->
        <div class="admin-card">
            <h2><i class="fa-solid fa-shield-halved" style="color: var(--accent-color);"></i> Eagle Eye Admin Panel</h2>
            <div class="form-group">
                <input type="text" id="postTitle" placeholder="Post Title (e.g. Vestify Pro New Offer)">
            </div>
            <div class="form-group">
                <textarea id="postDesc" placeholder="Write details about the job or link..."></textarea>
            </div>
            <div class="form-group">
                <input type="text" id="postUrl" placeholder="Target Link (https://...)">
            </div>
            <button class="btn" onclick="uploadPost()"><i class="fa-solid fa-paper-plane"></i> Publish Live Post</button>
        </div>

        <!-- Live Feed Section -->
        <h2 class="feed-title"><i class="fa-solid fa-rss" style="color: #2563eb;"></i> Live Feed</h2>
        <div id="feedContainer">
            <div class="no-posts">Loading posts in real-time...</div>
        </div>
    </div>

    <!-- Firebase SDK Scripts -->
    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
        import { getDatabase, ref, push, set, onValue } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-database.js";

        // Aapki Firebase Configuration
        const firebaseConfig = {
            apiKey: "AIzaSyBe5Q5jXpx3UvrHC9WOky9UWeDnP9SPfZI",
            authDomain: "verbose-6c008.firebaseapp.com",
            databaseURL: "https://verbose-6c008-default-rtdb.firebaseio.com",
            projectId: "verbose-6c008",
            storageBucket: "verbose-6c008.firebasestorage.app",
            messagingSenderId: "867100945312",
            appId: "1:867100945312:web:315dfb48fb34496cee12c5"
        };

        // Initialize Firebase
        const app = initializeApp(firebaseConfig);
        const db = getDatabase(app);

        // Publish Post Function (Admin Action)
        window.uploadPost = function() {
            const title = document.getElementById('postTitle').value.trim();
            const desc = document.getElementById('postDesc').value.trim();
            const url = document.getElementById('postUrl').value.trim();

            if(!title || !url) {
                alert("Please fill in at least the Title and Link sweetie!");
                return;
            }

            const postsRef = ref(db, 'posts');
            const newPostRef = push(postsRef);

            set(newPostRef, {
                title: title,
                description: desc,
                url: url,
                timestamp: Date.now()
            }).then(() => {
                document.getElementById('postTitle').value = '';
                document.getElementById('postDesc').value = '';
                document.getElementById('postUrl').value = '';
                alert("Post published successfully in real-time!");
            }).catch((error) => {
                alert("Error: " + error.message);
            });
        };

        // Fetch & Listen Posts in Real-Time
        const feedContainer = document.getElementById('feedContainer');
        const postsRef = ref(db, 'posts');

        onValue(postsRef, (snapshot) => {
            const data = snapshot.val();
            feedContainer.innerHTML = '';

            if (!data) {
                feedContainer.innerHTML = '<div class="no-posts">No posts available yet. Be the first to add one!</div>';
                return;
            }

            // Convert object to array and sort latest on top
            let postsArray = Object.keys(data).map(key => ({
                id: key,
                ...data[key]
            }));

            postsArray.sort((a, b) => b.timestamp - a.timestamp);

            postsArray.forEach(post => {
                let dateString = new Date(post.timestamp).toLocaleDateString() + ' ' + new Date(post.timestamp).toLocaleTimeString([], {hour: '2-digit', minute:'2-digit'});
                
                let postHTML = `
                    <div class="post-card">
                        <div class="post-header">
                            <div class="post-title">${escapeHtml(post.title)}</div>
                            <div class="post-time">${dateString}</div>
                        </div>
                        <div class="post-desc">${escapeHtml(post.description)}</div>
                        <a href="${escapeHtml(post.url)}" target="_blank" class="post-link">
                            <i class="fa-solid fa-external-link-alt"></i> Visit Link / Join Now
                        </a>
                    </div>
                `;
                feedContainer.innerHTML += postHTML;
            });
        });

        // Helper to prevent HTML injection
        function escapeHtml(text) {
            if (!text) return '';
            return text.replace(/&/g, "&amp;").replace(/</g, "&lt;").replace(/>/g, "&gt;").replace(/"/g, "&quot;").replace(/'/g, "&#039;");
        }
    </script>
</body>
</html>
