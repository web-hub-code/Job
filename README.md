<html lang="ur" dir="ltr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Global Earning & Job Portal - App</title>
    <!-- Google Fonts & FontAwesome -->
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --primary: #0f172a;
            --accent: #10b981;
            --bg: #f1f5f9;
            --card: #ffffff;
            --text: #1e293b;
            --border: #e2e8f0;
        }
        * { box-sizing: border-box; margin: 0; padding: 0; font-family: 'Poppins', sans-serif; -webkit-tap-highlight-color: transparent; }
        body { background-color: var(--bg); color: var(--text); padding-bottom: 70px; padding-top: 60px; }
        
        /* App Top Bar (Navbar) */
        .app-header { position: fixed; top: 0; left: 0; width: 100%; background: var(--primary); color: #fff; padding: 12px 15px; display: flex; justify-content: space-between; align-items: center; z-index: 1000; box-shadow: 0 2px 8px rgba(0,0,0,0.15); }
        .app-logo { cursor: pointer; font-size: 18px; font-weight: 700; color: var(--accent); user-select: none; display: flex; align-items: center; gap: 8px; }
        .app-user-status { font-size: 11px; background: rgba(255,255,255,0.1); padding: 4px 8px; border-radius: 12px; color: #cbd5e1; }

        .container { max-width: 500px; margin: 0 auto; padding: 12px; }
        .hidden { display: none !important; }

        /* App Cards */
        .app-card { background: var(--card); border-radius: 14px; padding: 16px; margin-bottom: 14px; box-shadow: 0 4px 12px rgba(0,0,0,0.03); border: 1px solid var(--border); }
        .admin-card { border: 2px dashed var(--accent); }

        input, select, textarea { width: 100%; padding: 10px 14px; margin-bottom: 10px; border: 1px solid var(--border); border-radius: 10px; font-size: 13px; outline: none; background: #f8fafc; }
        input:focus, select:focus, textarea:focus { border-color: var(--accent); background: #fff; }
        textarea { resize: none; height: 75px; }

        .btn { background: var(--accent); color: white; border: none; padding: 10px; border-radius: 10px; font-size: 13px; font-weight: 600; cursor: pointer; width: 100%; transition: opacity 0.2s; }
        .btn:active { transform: scale(0.98); }
        .btn-danger { background: #ef4444; }

        /* Categories App Pills */
        .app-filters { display: flex; gap: 6px; overflow-x: auto; padding: 4px 0 12px 0; scrollbar-width: none; }
        .app-filters::-webkit-scrollbar { display: none; }
        .pill-btn { background: #fff; border: 1px solid var(--border); padding: 6px 12px; border-radius: 20px; font-size: 11px; cursor: pointer; white-space: nowrap; font-weight: 500; color: #64748b; box-shadow: 0 2px 4px rgba(0,0,0,0.02); }
        .pill-btn.active { background: var(--primary); color: white; border-color: var(--primary); }

        /* Post Item Layout */
        .post-top { display: flex; justify-content: space-between; align-items: flex-start; margin-bottom: 6px; }
        .post-heading { font-size: 15px; font-weight: 700; color: var(--primary); line-height: 1.3; }
        .app-badge { background: #e0f2fe; color: #0284c7; font-size: 9px; padding: 3px 8px; border-radius: 6px; font-weight: 600; }
        .post-time { font-size: 10px; color: #94a3b8; margin-bottom: 8px; }
        .post-body { font-size: 13px; color: #475569; margin-bottom: 12px; line-height: 1.5; white-space: pre-line; }
        
        .post-action-bar { display: flex; justify-content: space-between; align-items: center; border-top: 1px solid #f1f5f9; padding-top: 10px; margin-top: 8px; }
        .app-action-btn { background: #f8fafc; border: 1px solid var(--border); padding: 6px 12px; border-radius: 8px; cursor: pointer; font-size: 12px; font-weight: 600; display: inline-flex; align-items: center; gap: 5px; color: #475569; }
        .app-action-btn:hover { background: #f1f5f9; }
        .join-btn { background: #eff6ff; color: #2563eb; border-color: #dbeafe; }

        /* Bottom App Navigation Bar */
        .app-bottom-nav { position: fixed; bottom: 0; left: 0; width: 100%; background: #fff; border-top: 1px solid var(--border); display: flex; justify-content: space-around; padding: 8px 0; z-index: 1000; box-shadow: 0 -4px 12px rgba(0,0,0,0.05); }
        .nav-item { text-align: center; color: #64748b; font-size: 10px; cursor: pointer; background: none; border: none; flex: 1; font-weight: 500; }
        .nav-item i { font-size: 16px; display: block; margin-bottom: 2px; }
        .nav-item.active { color: var(--accent); }
    </style>
</head>
<body>

    <!-- Top App Bar -->
    <header class="app-header">
        <div class="app-logo" onclick="handleLogoTap()">
            <i class="fa-solid fa-bolt" style="color: var(--accent);"></i> Global Portal
        </div>
        <div id="headerStatus" class="app-user-status">Guest Mode</div>
    </header>

    <div class="container">
        
        <!-- Tab 1: Home Feed View -->
        <div id="tabHome">
            <!-- Filter Pills -->
            <div class="app-filters">
                <button class="pill-btn active" onclick="filterPosts('All', this)">All Feeds</button>
                <button class="pill-btn" onclick="filterPosts('Free Earning', this)">Free Earning</button>
                <button class="pill-btn" onclick="filterPosts('Investment', this)">Investment</button>
                <button class="pill-btn" onclick="filterPosts('Apps & Games', this)">Apps & Games</button>
                <button class="pill-btn" onclick="filterPosts('Social Media Tasks', this)">Social Media Tasks</button>
            </div>

            <div id="feedContainer">
                <div style="text-align: center; color: #94a3b8; padding: 40px; font-size: 13px;">Loading live updates...</div>
            </div>
        </div>

        <!-- Tab 2: Account / Auth View -->
        <div id="tabAccount" class="hidden">
            <div class="app-card">
                <h3 id="authTitle" style="font-size: 16px; margin-bottom: 12px; color: var(--primary);">Account Login</h3>
                <input type="email" id="authEmail" placeholder="Email Address">
                <input type="password" id="authPassword" placeholder="Password">
                <button class="btn" id="authSubmitBtn" onclick="submitAuth()">Login</button>
                <div style="text-align: center; margin-top: 10px; font-size: 12px; color: #64748b; cursor: pointer;" onclick="toggleAuthMode()">
                    Don't have an account? <span style="color: var(--accent); font-weight: 600;">Sign Up</span>
                </div>
            </div>

            <div id="userProfileBox" class="app-card hidden" style="text-align: center;">
                <div style="font-size: 35px; color: var(--accent); margin-bottom: 8px;"><i class="fa-solid fa-circle-user"></i></div>
                <div id="profileEmail" style="font-size: 13px; font-weight: 600; margin-bottom: 15px;"></div>
                <button class="btn btn-danger" onclick="logoutUser()">Logout Session</button>
            </div>
        </div>

        <!-- Tab 3: Eagle Eye Admin Panel (Hidden until 5 taps on logo + 5426) -->
        <div id="tabAdmin" class="hidden">
            <div class="app-card admin-card">
                <h3 style="font-size: 15px; margin-bottom: 12px; color: var(--primary); display: flex; align-items: center; gap: 6px;">
                    <i class="fa-solid fa-shield-halved" style="color: var(--accent);"></i> Eagle Eye Admin Panel
                </h3>
                <input type="text" id="postTitleInput" placeholder="Post Title">
                <select id="postCategory">
                    <option value="Free Earning">Free Earning</option>
                    <option value="Investment">Investment</option>
                    <option value="Apps & Games">Apps & Games</option>
                    <option value="Social Media Tasks">Social Media Tasks</option>
                </select>
                <textarea id="postDescInput" placeholder="Write description & instructions..."></textarea>
                <input type="text" id="postUrlInput" placeholder="Target Joining Link (https://...)">
                <button class="btn" onclick="uploadPost()"><i class="fa-solid fa-paper-plane"></i> Publish Live Post</button>
                
                <hr style="margin: 15px 0; border:0; border-top:1px solid var(--border);">
                <h4 style="font-size: 13px; margin-bottom: 8px;">Active Posts Control</h4>
                <div id="adminDeleteList" style="max-height: 180px; overflow-y: auto;"></div>
            </div>
        </div>

    </div>

    <!-- Bottom App Navigation Bar -->
    <nav class="app-bottom-nav">
        <button class="nav-item active" onclick="switchTab('Home', this)">
            <i class="fa-solid fa-house"></i>Home
        </button>
        <button class="nav-item" onclick="switchTab('Account', this)">
            <i class="fa-solid fa-user"></i>Account
        </button>
    </nav>

    <!-- Firebase Script SDKs -->
    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
        import { getAuth, createUserWithEmailAndPassword, signInWithEmailAndPassword, onAuthStateChanged, signOut } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-auth.js";
        import { getDatabase, ref, push, set, remove, onValue, update } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-database.js";

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

        // --- App Tab Switcher ---
        window.switchTab = (tabName, btnElement) => {
            document.getElementById('tabHome').classList.add('hidden');
            document.getElementById('tabAccount').classList.add('hidden');
            document.getElementById('tabAdmin').classList.add('hidden');

            document.querySelectorAll('.nav-item').forEach(el => el.classList.remove('active'));
            btnElement.classList.add('active');

            if(tabName === 'Home') document.getElementById('tabHome').classList.remove('hidden');
            if(tabName === 'Account') document.getElementById('tabAccount').classList.remove('hidden');
            if(tabName === 'Admin') document.getElementById('tabAdmin').classList.remove('hidden');
        };

        // --- Secret Eagle Eye Trigger on Logo (5 Taps + Code 5426) ---
        let tapCount = 0;
        window.handleLogoTap = () => {
            tapCount++;
            if (tapCount === 5) {
                let code = prompt("Enter Eagle Eye Secret Code:");
                if (code === "5426") {
                    // Add Admin button dynamically to bottom nav if unlocked
                    const navBar = document.querySelector('.app-bottom-nav');
                    if(!document.getElementById('adminNavBtn')) {
                        navBar.innerHTML += `
                            <button id="adminNavBtn" class="nav-item" onclick="switchTab('Admin', this)">
                                <i class="fa-solid fa-shield-halved"></i>Admin
                            </button>
                        `;
                    }
                    switchTab('Admin', document.getElementById('adminNavBtn'));
                    alert("Eagle Eye App Mode Activated!");
                } else {
                    alert("Wrong Code!");
                }
                tapCount = 0;
            }
        };

        // --- Auth System ---
        window.toggleAuthMode = () => {
            isSignUpMode = !isSignUpMode;
            document.getElementById('authTitle').innerText = isSignUpMode ? "Create New Account" : "Account Login";
            document.getElementById('authSubmitBtn').innerText = isSignUpMode ? "Sign Up" : "Login";
        };

        window.submitAuth = () => {
            const email = document.getElementById('authEmail').value;
            const pass = document.getElementById('authPassword').value;
            if(!email || !pass) { alert("Enter email and password sweetie!"); return; }

            if(isSignUpMode) {
                createUserWithEmailAndPassword(auth, email, pass).then(() => alert("Account created!")).catch(e => alert(e.message));
            } else {
                signInWithEmailAndPassword(auth, email, pass).then(() => alert("Logged in!")).catch(e => alert(e.message));
            }
        };

        window.logoutUser = () => { signOut(auth).then(() => alert("Logged out!")); };

        onAuthStateChanged(auth, (user) => {
            const status = document.getElementById('headerStatus');
            const profileBox = document.getElementById('userProfileBox');
            const authCard = document.querySelector('#tabAccount .app-card:first-child');
            
            if (user) {
                status.innerText = "Online";
                authCard.classList.add('hidden');
                profileBox.classList.remove('hidden');
                document.getElementById('profileEmail').innerText = user.email;
            } else {
                status.innerText = "Guest Mode";
                authCard.classList.remove('hidden');
                profileBox.classList.add('hidden');
            }
        });

        // --- Post System ---
        window.uploadPost = () => {
            const title = document.getElementById('postTitleInput').value.trim();
            const category = document.getElementById('postCategory').value;
            const description = document.getElementById('postDescInput').value.trim();
            const url = document.getElementById('postUrlInput').value.trim();

            if(!title || !url) { alert("Title and Link are required sweetie!"); return; }

            push(ref(db, 'posts'), { title, category, description, url, likes: 0, timestamp: Date.now() })
                .then(() => {
                    document.getElementById('postTitleInput').value = '';
                    document.getElementById('postDescInput').value = '';
                    document.getElementById('postUrlInput').value = '';
                    alert("Posted live successfully!");
                    switchTab('Home', document.querySelector('.app-bottom-nav .nav-item'));
                });
        };

        window.deletePost = (id) => { if(confirm("Delete this post?")) remove(ref(db, 'posts/' + id)); };
        window.likePost = (id, likes) => update(ref(db, 'posts/' + id), { likes: (likes || 0) + 1 });
        window.copyPostLink = (url) => { navigator.clipboard.writeText(url); alert("Link copied to clipboard!"); };

        window.filterPosts = (cat, btn) => {
            currentFilter = cat;
            document.querySelectorAll('.pill-btn').forEach(b => b.classList.remove('active'));
            btn.classList.add('active');
            renderFeed();
        };

        // --- Realtime Sync ---
        onValue(ref(db, 'posts'), (snapshot) => {
            const data = snapshot.val();
            allPostsData = [];
            const deleteList = document.getElementById('adminDeleteList');
            deleteList.innerHTML = '';

            if(data) {
                Object.keys(data).forEach(key => {
                    allPostsData.push({ id: key, ...data[key] });
                    deleteList.innerHTML += `
                        <div style="display:flex; justify-content:space-between; align-items:center; padding:6px 0; border-bottom:1px solid #f1f5f9; font-size:11px;">
                            <span>${escapeHtml(data[key].title)}</span>
                            <button class="btn btn-danger" style="width:auto; padding:2px 8px; font-size:10px;" onclick="deletePost('${key}')">Delete</button>
                        </div>
                    `;
                });
            }
            renderFeed();
        });

        function renderFeed() {
            const container = document.getElementById('feedContainer');
            container.innerHTML = '';
            let filtered = currentFilter === 'All' ? allPostsData : allPostsData.filter(p => p.category === currentFilter);
            filtered.sort((a, b) => b.timestamp - a.timestamp);

            if(filtered.length === 0) {
                container.innerHTML = '<div style="text-align: center; color: #94a3b8; padding: 40px; font-size: 13px;">No updates found!</div>';
                return;
            }

            filtered.forEach(post => {
                let timeStr = new Date(post.timestamp).toLocaleDateString() + ' ' + new Date(post.timestamp).toLocaleTimeString([], {hour: '2-digit', minute:'2-digit'});
                container.innerHTML += `
                    <div class="app-card">
                        <div class="post-top">
                            <div class="post-heading">${escapeHtml(post.title)}</div>
                            <span class="app-badge">${escapeHtml(post.category || 'General')}</span>
                        </div>
                        <div class="post-time">${timeStr}</div>
                        <div class="post-body">${escapeHtml(post.description)}</div>
                        
                        <div style="margin-bottom: 10px;">
                            <a href="${escapeHtml(post.url)}" target="_blank" class="app-action-btn join-btn" style="text-decoration:none; display:inline-flex;">
                                <i class="fa-solid fa-arrow-up-right-from-square"></i> Visit Link / Join Now
                            </a>
                        </div>

                        <div class="post-action-bar">
                            <button class="app-action-btn" onclick="likePost('${post.id}', ${post.likes || 0})">
                                <i class="fa-solid fa-heart" style="color: #ef4444;"></i> (${post.likes || 0})
                            </button>
                            <button class="app-action-btn" onclick="copyPostLink('${escapeHtml(post.url)}')">
                                <i class="fa-solid fa-copy"></i> Copy Link
                            </button>
                        </div>
                    </div>
                `;
            });
        }

        function escapeHtml(text) {
            if (!text) return '';
            return text.replace(/&/g, "&amp;").replace(/</g, "&lt;").replace(/>/g, "&gt;").replace(/"/g, "&quot;").replace(/'/g, "&#039;");
        }
    </script>
</body>
</html>
