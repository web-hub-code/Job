<html lang="ur" dir="ltr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Global Earning & Job Portal - Pro Feed</title>
    <!-- Google Fonts & FontAwesome -->
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --primary: #0f172a;
            --accent: #10b981;
            --bg: #f8fafc;
            --card: #ffffff;
            --text: #334155;
            --border: #e2e8f0;
        }
        * { box-sizing: border-box; margin: 0; padding: 0; font-family: 'Poppins', sans-serif; }
        body { background-color: var(--bg); color: var(--text); padding-bottom: 50px; }
        
        header { background: var(--primary); color: #fff; padding: 20px; text-align: center; box-shadow: 0 4px 6px rgba(0,0,0,0.1); }
        .logo { cursor: pointer; font-size: 22px; font-weight: 700; color: var(--accent); margin-bottom: 5px; display: inline-block; user-select: none; }
        header p { font-size: 13px; color: #94a3b8; }

        .container { max-width: 650px; margin: 20px auto; padding: 0 15px; }
        .hidden { display: none !important; }

        /* Auth Box */
        .auth-card, .admin-card, .post-card { background: var(--card); border: 1px solid var(--border); border-radius: 12px; padding: 20px; margin-bottom: 20px; box-shadow: 0 2px 4px rgba(0,0,0,0.02); }
        .admin-card { border: 2px dashed var(--accent); }
        
        input, select, textarea { width: 100%; padding: 10px 14px; margin-bottom: 12px; border: 1px solid var(--border); border-radius: 8px; font-size: 14px; outline: none; }
        input:focus, select:focus, textarea:focus { border-color: var(--accent); }
        textarea { resize: vertical; height: 80px; }

        .btn { background: var(--accent); color: white; border: none; padding: 10px 15px; border-radius: 8px; font-size: 14px; font-weight: 600; cursor: pointer; width: 100%; transition: opacity 0.2s; }
        .btn:hover { opacity: 0.9; }
        .btn-danger { background: #ef4444; }

        /* Categories Filter */
        .filter-container { display: flex; gap: 8px; overflow-x: auto; padding-bottom: 10px; margin-bottom: 15px; }
        .filter-btn { background: #e2e8f0; border: none; padding: 6px 14px; border-radius: 20px; font-size: 12px; cursor: pointer; white-space: nowrap; font-weight: 600; color: #475569; }
        .filter-btn.active { background: var(--accent); color: white; }

        /* Post Styling */
        .post-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 8px; }
        .post-title { font-size: 16px; font-weight: 700; color: var(--primary); }
        .badge { background: #dbeafe; color: #2563eb; font-size: 10px; padding: 3px 8px; border-radius: 4px; font-weight: 600; }
        .post-desc { font-size: 14px; color: #475569; margin-bottom: 12px; white-space: pre-line; }
        
        .post-footer { display: flex; justify-content: space-between; align-items: center; border-top: 1px solid var(--border); padding-top: 10px; margin-top: 10px; }
        .action-btn { background: none; border: none; cursor: pointer; font-size: 13px; font-weight: 600; display: inline-flex; align-items: center; gap: 5px; color: #64748b; }
        .action-btn:hover { color: var(--accent); }
        .post-link-btn { background: #eff6ff; color: #2563eb; padding: 6px 12px; border-radius: 6px; text-decoration: none; font-size: 12px; font-weight: 600; }

        .auth-toggle { text-align: center; margin-top: 10px; font-size: 13px; color: #64748b; cursor: pointer; }
        .auth-toggle span { color: var(--accent); font-weight: 600; }
    </style>
</head>
<body>

    <header>
        <!-- Secret Trigger on Logo (5 taps) -->
        <div class="logo" onclick="handleLogoTap()"><i class="fa-solid fa-globe"></i> Global Earning & Job Portal</div>
        <p>Your Trusted Gateway to Online Work & Real-Time Financial Opportunities</p>
    </header>

    <div class="container">
        
        <!-- Auth Section -->
        <div id="authCard" class="auth-card">
            <h3 id="authTitle" style="margin-bottom: 15px; color: var(--primary);">Login to Portal</h3>
            <input type="email" id="authEmail" placeholder="Enter Email">
            <input type="password" id="authPassword" placeholder="Enter Password">
            <button class="btn" id="authSubmitBtn" onclick="submitAuth()">Login</button>
            <div class="auth-toggle" onclick="toggleAuthMode()">Don't have an account? <span>Sign Up</span></div>
        </div>

        <!-- Logged In User Info Bar -->
        <div id="userInfoBar" class="hidden" style="display:none; justify-content:space-between; align-items:center; background:#fff; padding:10px 15px; border-radius:8px; margin-bottom:20px; border:1px solid var(--border);">
            <span id="userEmailDisplay" style="font-size:13px; font-weight:600;"></span>
            <button class="btn" style="width:auto; padding:5px 10px; font-size:11px; background:#ef4444;" onclick="logoutUser()">Logout</button>
        </div>

        <!-- Eagle Eye Admin Panel (Hidden by default) -->
        <div id="adminPanel" class="admin-card hidden">
            <h2><i class="fa-solid fa-shield-halved" style="color: var(--accent);"></i> Eagle Eye Admin Panel</h2>
            <input type="text" id="postTitleInput" placeholder="Post Title (e.g. Vestify Pro Bonus)">
            <select id="postCategory">
                <option value="Free Earning">Free Earning</option>
                <option value="Investment">Investment</option>
                <option value="Apps & Games">Apps & Games</option>
                <option value="Social Media Tasks">Social Media Tasks</option>
            </select>
            <textarea id="postDescInput" placeholder="Write description, guidelines or rules..."></textarea>
            <input type="text" id="postUrlInput" placeholder="Target Joining Link (https://...)">
            <button class="btn" onclick="uploadPost()"><i class="fa-solid fa-paper-plane"></i> Publish Post Live</button>
            
            <hr style="margin: 15px 0; border:0; border-top:1px solid var(--border);">
            <h4 style="font-size:14px; margin-bottom:10px;">Manage Existing Posts (Delete)</h4>
            <div id="adminDeleteList" style="max-height: 150px; overflow-y: auto;"></div>
        </div>

        <!-- Filter Buttons -->
        <div class="filter-container">
            <button class="filter-btn active" onclick="filterPosts('All', this)">All Updates</button>
            <button class="filter-btn" onclick="filterPosts('Free Earning', this)">Free Earning</button>
            <button class="filter-btn" onclick="filterPosts('Investment', this)">Investment</button>
            <button class="filter-btn" onclick="filterPosts('Apps & Games', this)">Apps & Games</button>
            <button class="filter-btn" onclick="filterPosts('Social Media Tasks', this)">Social Media Tasks</button>
        </div>

        <!-- Live Feed Container -->
        <div id="feedContainer">
            <div style="text-align: center; color: #64748b; padding: 30px;">Loading live posts...</div>
        </div>

    </div>

    <!-- Firebase SDK Scripts -->
    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
        import { getAuth, createUserWithEmailAndPassword, signInWithEmailAndPassword, onAuthStateChanged, signOut } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-auth.js";
        import { getDatabase, ref, push, set, remove, onValue, update } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-database.js";

        // Apna Firebase Configuration yahan dalein
        const firebaseConfig = {
            apiKey: "AIzaSyBe5Q5jXpx3UvrHC9WOky9UWeDnP9SPfZI",
            authDomain: "verbose-6c008.firebaseapp.com",
            databaseURL: "https://verbose-6c008-default-rtdb.firebaseio.com",
            projectId: "verbose-6c008",
            storageBucket: "verbose-6c008.firebasestorage.app",
            messagingSenderId: "867100945312",
            appId: "1:867100945312:web:315dfb48fb34496cee12c5"
        };

        const app = initializeApp(firebaseConfig);
        const auth = getAuth(app);
        const db = getDatabase(app);

        let isSignUpMode = false;
        let allPostsData = [];
        let currentFilter = 'All';

        // --- Auth Mode Toggle ---
        window.toggleAuthMode = () => {
            isSignUpMode = !isSignUpMode;
            document.getElementById('authTitle').innerText = isSignUpMode ? "Create an Account" : "Login to Portal";
            document.getElementById('authSubmitBtn').innerText = isSignUpMode ? "Sign Up" : "Login";
        };

        // --- Auth Submission ---
        window.submitAuth = () => {
            const email = document.getElementById('authEmail').value;
            const pass = document.getElementById('authPassword').value;
            if(!email || !pass) { alert("Please fill email and password sweetie!"); return; }

            if(isSignUpMode) {
                createUserWithEmailAndPassword(auth, email, pass)
                    .then(() => alert("Account created successfully!"))
                    .catch(e => alert(e.message));
            } else {
                signInWithEmailAndPassword(auth, email, pass)
                    .then(() => alert("Logged in successfully!"))
                    .catch(e => alert(e.message));
            }
        };

        window.logoutUser = () => {
            signOut(auth).then(() => alert("Logged out!"));
        };

        // Track Auth State
        onAuthStateChanged(auth, (user) => {
            const authCard = document.getElementById('authCard');
            const userInfoBar = document.getElementById('userInfoBar');
            if (user) {
                authCard.classList.add('hidden');
                userInfoBar.style.display = 'flex';
                document.getElementById('userEmailDisplay').innerText = "Logged in as: " + user.email;
            } else {
                authCard.classList.remove('hidden');
                userInfoBar.style.display = 'none';
                document.getElementById('adminPanel').classList.add('hidden');
            }
        });

        // --- Secret Eagle Eye Admin Trigger (5 Taps & Code 5426) ---
        let tapCount = 0;
        window.handleLogoTap = () => {
            tapCount++;
            if (tapCount === 5) {
                let code = prompt("Enter Eagle Eye Secret Code:");
                if (code === "5426") {
                    document.getElementById('adminPanel').classList.remove('hidden');
                    alert("Eagle Eye Admin Panel Activated!");
                } else {
                    alert("Incorrect secret code!");
                }
                tapCount = 0;
            }
        };

        // --- Upload Post (Admin) ---
        window.uploadPost = () => {
            const title = document.getElementById('postTitleInput').value.trim();
            const category = document.getElementById('postCategory').value;
            const description = document.getElementById('postDescInput').value.trim();
            const url = document.getElementById('postUrlInput').value.trim();

            if(!title || !url) { alert("Title and Link are required sweetie!"); return; }

            const newRef = push(ref(db, 'posts'));
            set(newRef, {
                title, category, description, url,
                likes: 0,
                timestamp: Date.now()
            }).then(() => {
                document.getElementById('postTitleInput').value = '';
                document.getElementById('postDescInput').value = '';
                document.getElementById('postUrlInput').value = '';
                alert("Post published live!");
            }).catch(e => alert(e.message));
        };

        // --- Delete Post (Admin) ---
        window.deletePost = (id) => {
            if(confirm("Are you sure you want to delete this post?")) {
                remove(ref(db, 'posts/' + id));
            }
        };

        // --- Like System ---
        window.likePost = (id, currentLikes) => {
            update(ref(db, 'posts/' + id), { likes: (currentLikes || 0) + 1 });
        };

        // --- Copy Link System ---
        window.copyPostLink = (url) => {
            navigator.clipboard.writeText(url);
            alert("Link copied to clipboard! Share it with friends sweetie.");
        };

        // --- Filter System ---
        window.filterPosts = (category, btnElement) => {
            currentFilter = category;
            document.querySelectorAll('.filter-btn').forEach(b => b.classList.remove('active'));
            btnElement.classList.add('active');
            renderFeed();
        };

        // --- Realtime Data Fetching ---
        onValue(ref(db, 'posts'), (snapshot) => {
            const data = snapshot.val();
            allPostsData = [];
            const adminDeleteList = document.getElementById('adminDeleteList');
            adminDeleteList.innerHTML = '';

            if (data) {
                Object.keys(data).forEach(key => {
                    allPostsData.push({ id: key, ...data[key] });
                    // Populate Admin Delete panel list
                    adminDeleteList.innerHTML += `
                        <div style="display:flex; justify-content:space-between; align-items:center; padding:5px 0; border-bottom:1px solid #f1f5f9; font-size:12px;">
                            <span>${escapeHtml(data[key].title)}</span>
                            <button class="btn btn-danger" style="width:auto; padding:2px 8px; font-size:10px;" onclick="deletePost('${key}')">Delete</button>
                        </div>
                    `;
                });
            }
            renderFeed();
        });

        // --- Render Feed Function ---
        function renderFeed() {
            const feedContainer = document.getElementById('feedContainer');
            feedContainer.innerHTML = '';

            let filtered = allPostsData;
            if(currentFilter !== 'All') {
                filtered = allPostsData.filter(p => p.category === currentFilter);
            }

            filtered.sort((a, b) => b.timestamp - a.timestamp);

            if(filtered.length === 0) {
                feedContainer.innerHTML = '<div style="text-align: center; color: #64748b; padding: 40px; background: #fff; border-radius: 12px; border:1px solid var(--border);">No updates found in this category yet!</div>';
                return;
            }

            filtered.forEach(post => {
                let dateStr = new Date(post.timestamp).toLocaleDateString() + ' ' + new Date(post.timestamp).toLocaleTimeString([], {hour: '2-digit', minute:'2-digit'});
                let postHTML = `
                    <div class="post-card">
                        <div class="post-header">
                            <div class="post-title">${escapeHtml(post.title)}</div>
                            <span class="badge">${escapeHtml(post.category || 'General')}</span>
                        </div>
                        <div style="font-size: 11px; color: #94a3b8; margin-bottom: 8px;">${dateStr}</div>
                        <div class="post-desc">${escapeHtml(post.description)}</div>
                        
                        <div style="margin-bottom: 12px;">
                            <a href="${escapeHtml(post.url)}" target="_blank" class="post-link-btn">
                                <i class="fa-solid fa-external-link-alt"></i> Visit Link / Join Now
                            </a>
                        </div>

                        <div class="post-footer">
                            <button class="action-btn" onclick="likePost('${post.id}', ${post.likes || 0})">
                                <i class="fa-solid fa-heart" style="color: #ef4444;"></i> Like (${post.likes || 0})
                            </button>
                            <button class="action-btn" onclick="copyPostLink('${escapeHtml(post.url)}')">
                                <i class="fa-solid fa-copy"></i> Copy Link
                            </button>
                        </div>
                    </div>
                `;
                feedContainer.innerHTML += postHTML;
            });
        }

        function escapeHtml(text) {
            if (!text) return '';
            return text.replace(/&/g, "&amp;").replace(/</g, "&lt;").replace(/>/g, "&gt;").replace(/"/g, "&quot;").replace(/'/g, "&#039;");
        }
    </script>
</body>
</html>
