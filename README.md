<html lang="ur" dir="ltr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Prime Solutions - Global Earning & Service Portal</title>
    <!-- Google Fonts & FontAwesome -->
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --primary: #0f172a;
            --accent: #10b981;
            --bg: #f8fafc;
            --card: #ffffff;
            --text: #1e293b;
            --border: #e2e8f0;
            --input-bg: #f8fafc;
        }
        body.dark-mode {
            --primary: #1e293b;
            --accent: #34d399;
            --bg: #0f172a;
            --card: #1e293b;
            --text: #f8fafc;
            --border: #334155;
            --input-bg: #0f172a;
        }
        * { box-sizing: border-box; margin: 0; padding: 0; font-family: 'Poppins', sans-serif; -webkit-tap-highlight-color: transparent; }
        body { background-color: var(--bg); color: var(--text); padding-bottom: 75px; padding-top: 60px; transition: background 0.3s, color 0.3s; }
        
        /* App Top Bar */
        .app-header { position: fixed; top: 0; left: 0; width: 100%; background: var(--primary); color: #fff; padding: 12px 15px; display: flex; justify-content: space-between; align-items: center; z-index: 1000; box-shadow: 0 2px 8px rgba(0,0,0,0.15); }
        .app-logo { cursor: pointer; font-size: 16px; font-weight: 700; color: var(--accent); user-select: none; display: flex; align-items: center; gap: 8px; }
        .header-actions { display: flex; align-items: center; gap: 8px; }
        .app-user-status { font-size: 11px; background: rgba(255,255,255,0.1); padding: 4px 10px; border-radius: 12px; color: #cbd5e1; }
        .theme-toggle-btn { background: none; border: none; color: #cbd5e1; font-size: 16px; cursor: pointer; padding: 4px; }

        .container { max-width: 500px; margin: 0 auto; padding: 12px; }
        .hidden { display: none !important; }

        /* Cards & UI */
        .app-card { background: var(--card); border-radius: 14px; padding: 16px; margin-bottom: 14px; box-shadow: 0 4px 12px rgba(0,0,0,0.03); border: 1px solid var(--border); transition: background 0.3s, border 0.3s; }
        .admin-card { border: 2px dashed var(--accent); }

        input, select, textarea { width: 100%; padding: 10px 14px; margin-bottom: 10px; border: 1px solid var(--border); border-radius: 10px; font-size: 13px; outline: none; background: var(--input-bg); color: var(--text); }
        input:focus, select:focus, textarea:focus { border-color: var(--accent); background: var(--card); }
        textarea { resize: none; height: 75px; }

        .btn { background: var(--accent); color: white; border: none; padding: 10px; border-radius: 10px; font-size: 13px; font-weight: 600; cursor: pointer; width: 100%; transition: opacity 0.2s; display: flex; align-items: center; justify-content: center; gap: 6px; text-decoration: none; }
        .btn:active { transform: scale(0.98); }
        .btn-danger { background: #ef4444; }
        .btn-google { background: #db4437; margin-top: 8px; }
        .btn-whatsapp { background: #25d366; color: white; margin-bottom: 12px; }

        /* Loading Spinner Overlay */
        #loadingOverlay { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(15,23,42,0.6); z-index: 99999; display: flex; flex-direction: column; justify-content: center; align-items: center; color: #fff; gap: 10px; }
        .spinner { border: 4px solid rgba(255,255,255,0.3); border-top: 4px solid var(--accent); border-radius: 50%; width: 40px; height: 40px; animation: spin 0.8s linear infinite; }
        @keyframes spin { 0% { transform: rotate(0deg); } 100% { transform: rotate(360deg); } }

        /* Fake Notifications Toast */
        #fakeNotification { position: fixed; top: 70px; right: 15px; background: var(--primary); color: #fff; padding: 10px 14px; border-radius: 10px; font-size: 11px; z-index: 999; box-shadow: 0 5px 15px rgba(0,0,0,0.2); border-left: 4px solid var(--accent); transition: transform 0.3s ease, opacity 0.3s ease; transform: translateX(120%); opacity: 0; max-width: 280px; }
        #fakeNotification.show { transform: translateX(0); opacity: 1; }

        /* Welcome Section */
        .welcome-banner { background: linear-gradient(135deg, var(--primary), #1e293b); color: #fff; border-radius: 16px; padding: 20px; margin-bottom: 14px; text-align: center; box-shadow: 0 4px 15px rgba(0,0,0,0.1); border: 1px solid var(--border); }
        .welcome-banner h2 { font-size: 20px; color: var(--accent); margin-bottom: 6px; }
        .welcome-banner p { font-size: 12px; color: #cbd5e1; line-height: 1.5; margin-bottom: 12px; }
        .services-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 8px; margin-top: 10px; text-align: left; }
        .service-box { background: rgba(255,255,255,0.05); padding: 10px; border-radius: 10px; font-size: 11px; border: 1px solid rgba(255,255,255,0.1); }
        .service-box i { color: var(--accent); margin-bottom: 4px; display: block; font-size: 14px; }

        /* Search & Filters */
        .search-box { position: relative; margin-bottom: 8px; }
        .search-box input { padding-left: 36px; margin-bottom: 0; }
        .search-box i { position: absolute; left: 12px; top: 12px; color: #94a3b8; font-size: 14px; }

        .app-filters { display: flex; gap: 6px; overflow-x: auto; padding: 4px 0 12px 0; scrollbar-width: none; }
        .app-filters::-webkit-scrollbar { display: none; }
        .pill-btn { background: var(--card); border: 1px solid var(--border); padding: 6px 12px; border-radius: 20px; font-size: 11px; cursor: pointer; white-space: nowrap; font-weight: 500; color: var(--text); box-shadow: 0 2px 4px rgba(0,0,0,0.02); }
        .pill-btn.active { background: var(--primary); color: white; border-color: var(--primary); }

        /* Post Layout */
        .post-top { display: flex; justify-content: space-between; align-items: flex-start; margin-bottom: 6px; }
        .post-heading { font-size: 15px; font-weight: 700; color: var(--text); line-height: 1.3; }
        .app-badge { background: #e0f2fe; color: #0284c7; font-size: 9px; padding: 3px 8px; border-radius: 6px; font-weight: 600; }
        body.dark-mode .app-badge { background: #0369a1; color: #e0f2fe; }
        .post-meta-row { display: flex; justify-content: space-between; align-items: center; font-size: 10px; color: #94a3b8; margin-bottom: 8px; }
        .post-body { font-size: 13px; color: var(--text); opacity: 0.85; margin-bottom: 10px; line-height: 1.5; white-space: pre-line; }
        .post-img { width: 100%; border-radius: 10px; max-height: 250px; object-fit: cover; margin-bottom: 12px; border: 1px solid var(--border); }
        
        /* Star Rating Styles */
        .star-rating-box { display: flex; align-items: center; gap: 4px; font-size: 13px; color: #cbd5e1; margin-bottom: 10px; cursor: pointer; }
        .star-rating-box .fa-star.rated { color: #f59e0b; }

        .post-action-bar { display: flex; justify-content: space-between; align-items: center; border-top: 1px solid var(--border); padding-top: 10px; margin-top: 8px; }
        .app-action-btn { background: var(--input-bg); border: 1px solid var(--border); padding: 6px 12px; border-radius: 8px; cursor: pointer; font-size: 12px; font-weight: 600; display: inline-flex; align-items: center; gap: 5px; color: var(--text); }
        .join-btn { background: #eff6ff; color: #2563eb; border-color: #dbeafe; }
        body.dark-mode .join-btn { background: #1e3a8a; color: #93c5fd; border-color: #1d4ed8; }

        /* Ad Overlay Popup */
        .ad-overlay { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.7); z-index: 9999; display: flex; justify-content: center; align-items: center; padding: 20px; }
        .ad-modal { background: var(--card); width: 100%; max-width: 400px; border-radius: 16px; padding: 20px; text-align: center; position: relative; box-shadow: 0 10px 25px rgba(0,0,0,0.3); border: 1px solid var(--border); }
        .ad-timer { position: absolute; top: 12px; right: 15px; background: #fee2e2; color: #dc2626; font-size: 11px; font-weight: 700; padding: 3px 8px; border-radius: 20px; }
        .ad-content-img { width: 100%; max-height: 200px; object-fit: cover; border-radius: 10px; margin: 10px 0; }

        /* Admin Analytics Cards */
        .analytics-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 8px; margin-bottom: 15px; }
        .stat-box { background: var(--input-bg); border: 1px solid var(--border); border-radius: 10px; padding: 10px; text-align: center; }
        .stat-box h5 { font-size: 10px; color: #94a3b8; margin-bottom: 4px; }
        .stat-box span { font-size: 16px; font-weight: 700; color: var(--accent); }

        /* Bottom App Navigation Bar */
        .app-bottom-nav { position: fixed; bottom: 0; left: 0; width: 100%; background: var(--card); border-top: 1px solid var(--border); display: flex; justify-content: space-around; padding: 8px 0; z-index: 1000; box-shadow: -4px 12px rgba(0,0,0,0.05); }
        .nav-item { text-align: center; color: #64748b; font-size: 10px; cursor: pointer; background: none; border: none; flex: 1; font-weight: 500; }
        .nav-item i { font-size: 16px; display: block; margin-bottom: 2px; }
        .nav-item.active { color: var(--accent); }

        /* Tables for Admin */
        .admin-table { width: 100%; border-collapse: collapse; font-size: 11px; margin-top: 8px; }
        .admin-table th, .admin-table td { padding: 8px; border-bottom: 1px solid var(--border); text-align: left; }
        .admin-table th { background: var(--input-bg); color: var(--text); font-weight: 600; }
    </style>
</head>
<body>

    <!-- Loading Spinner -->
    <div id="loadingOverlay" class="hidden">
        <div class="spinner"></div>
        <div id="loadingText" style="font-size: 13px; font-weight: 500;">Processing...</div>
    </div>

    <!-- Fake Notification Toast -->
    <div id="fakeNotification">
        <i class="fa-solid fa-bell" style="color: var(--accent);"></i> <span id="fakeNotifText"></span>
    </div>

    <!-- Ad Popup -->
    <div id="adPopup" class="ad-overlay hidden">
        <div class="ad-modal">
            <div id="adTimerBadge" class="ad-timer">Closing in 5s</div>
            <h3 style="font-size: 16px; color: var(--text); margin-bottom: 5px;" id="adTitleText">Sponsored Ad</h3>
            <p style="font-size: 12px; color: #94a3b8; margin-bottom: 10px;" id="adDescText">Please wait...</p>
            <div id="adMediaContainer"></div>
            <a id="adLinkBtn" href="#" target="_blank" class="btn" style="text-decoration:none; display:inline-block; margin-top:10px;">Learn More</a>
        </div>
    </div>

    <!-- Top App Bar -->
    <header class="app-header">
        <div class="app-logo" onclick="handleLogoTap()">
            <i class="fa-solid fa-bolt" style="color: var(--accent);"></i> Prime Solutions
        </div>
        <div class="header-actions">
            <button class="theme-toggle-btn" onclick="toggleDarkMode()" title="Toggle Theme"><i class="fa-solid fa-moon" id="themeIcon"></i></button>
            <div id="headerStatus" class="app-user-status">Guest Mode</div>
        </div>
    </header>

    <div class="container">
        
        <!-- Tab 1: Home Feed & Welcome View -->
        <div id="tabHome">
            <div class="welcome-banner">
                <h2>Welcome to Prime Solutions</h2>
                <p>Your ultimate portal for global earning jobs, application guides, and smart digital opportunities.</p>
                
                <!-- Direct WhatsApp Community Join Button -->
                <a href="https://chat.whatsapp.com/D6QqMvZFBqLE4Hu4MsYEL5?s=cl&p=a&ilr=1" target="_blank" class="btn btn-whatsapp">
                    <i class="fa-brands fa-whatsapp" style="font-size: 16px;"></i> Join WhatsApp Community Hub
                </a>

                <div style="font-size: 10px; color: var(--accent); font-weight: 600; margin-bottom: 8px;">DESIGN & POWERED BY PRIME SOLUTIONS</div>
                <div class="services-grid">
                    <div class="service-box"><i class="fa-solid fa-laptop-code"></i> Web Portals & Apps</div>
                    <div class="service-box"><i class="fa-solid fa-wallet"></i> Earning Job Feeds</div>
                    <div class="service-box"><i class="fa-solid fa-shield-halved"></i> Secure Firebase Data</div>
                    <div class="service-box"><i class="fa-solid fa-bullhorn"></i> Promotional Ads</div>
                </div>
            </div>

            <!-- Install App (PWA) Banner (Hidden by default unless installable) -->
            <div id="pwaInstallCard" class="app-card hidden" style="background: linear-gradient(135deg, #10b981, #059669); color: white; text-align: center; padding: 12px;">
                <h4 style="font-size: 13px; margin-bottom: 4px;"><i class="fa-solid fa-mobile-screen-button"></i> Install Prime Solutions App</h4>
                <p style="font-size: 11px; margin-bottom: 8px; opacity: 0.9;">Add to your home screen for quick access without opening browser!</p>
                <button id="pwaInstallBtn" class="btn" style="background: white; color: #065f46; font-weight: 700; width: auto; margin: 0 auto; padding: 6px 16px;">Install Now</button>
            </div>

            <!-- Live Search Bar -->
            <div class="search-box">
                <i class="fa-solid fa-magnifying-glass"></i>
                <input type="text" id="searchInput" placeholder="Search posts, platforms (e.g. Vestify Pro)..." oninput="handleSearch()">
            </div>

            <div class="app-filters">
                <button class="pill-btn active" onclick="filterPosts('All', this)">All Feeds</button>
                <button class="pill-btn" onclick="filterPosts('Free Earning', this)">Free Earning</button>
                <button class="pill-btn" onclick="filterPosts('Investment', this)">Investment</button>
                <button class="pill-btn" onclick="filterPosts('Apps & Games', this)">Apps & Games</button>
                <button class="pill-btn" onclick="filterPosts('Social Media Tasks', this)">Social Media Tasks</button>
                <button class="pill-btn" onclick="filterPosts('Saved', this)"><i class="fa-solid fa-bookmark"></i> Saved</button>
            </div>

            <div id="feedContainer">
                <div style="text-align: center; color: #94a3b8; padding: 40px; font-size: 13px;">Loading live updates...</div>
            </div>
        </div>

        <!-- Tab 2: Help & Support View -->
        <div id="tabHelp" class="hidden">
            <div class="app-card">
                <h3 style="font-size: 16px; margin-bottom: 8px; color: var(--text);">Realtime Help & Support</h3>
                <p style="font-size: 12px; color: #94a3b8; margin-bottom: 12px;">Send your queries or messages directly to the Prime Solutions admin team in realtime!</p>
                <input type="text" id="helpUserName" placeholder="Your Name">
                <input type="email" id="helpUserEmail" placeholder="Your Email">
                <textarea id="helpUserMsg" placeholder="Describe your issue or question..."></textarea>
                <button class="btn" onclick="sendHelpMessage()"><i class="fa-solid fa-paper-plane"></i> Send to Admin</button>
            </div>
        </div>

        <!-- Tab 3: Account / Login View -->
        <div id="tabAccount" class="hidden">
            <div class="app-card">
                <h3 id="authTitle" style="font-size: 16px; margin-bottom: 12px; color: var(--text);">Account Login</h3>
                <input type="email" id="authEmail" placeholder="Email Address">
                <input type="password" id="authPassword" placeholder="Password">
                <button class="btn" id="authSubmitBtn" onclick="submitAuth()">Login</button>
                <button class="btn btn-google" onclick="loginWithGoogle()"><i class="fa-brands fa-google"></i> Continue with Google</button>
                <div style="text-align: center; margin-top: 12px; font-size: 12px; color: #94a3b8; cursor: pointer;" onclick="toggleAuthMode()">
                    Don't have an account? <span style="color: var(--accent); font-weight: 600;">Sign Up</span>
                </div>
            </div>

            <div id="userProfileBox" class="app-card hidden" style="text-align: center;">
                <div style="font-size: 35px; color: var(--accent); margin-bottom: 8px;"><i class="fa-solid fa-circle-user"></i></div>
                <div id="profileEmail" style="font-size: 13px; font-weight: 600; margin-bottom: 15px;"></div>
                <button class="btn btn-danger" onclick="logoutUser()">Logout Session</button>
            </div>
        </div>

        <!-- Tab 4: Eagle Eye Admin Panel -->
        <div id="tabAdmin" class="hidden">
            <div class="app-card admin-card">
                <h3 style="font-size: 15px; margin-bottom: 12px; color: var(--text); display: flex; align-items: center; gap: 6px;">
                    <i class="fa-solid fa-shield-halved" style="color: var(--accent);"></i> Eagle Eye Admin Panel
                </h3>

                <!-- Admin Analytics Cards -->
                <div class="analytics-grid">
                    <div class="stat-box">
                        <h5>Total Users</h5>
                        <span id="statTotalUsers">0</span>
                    </div>
                    <div class="stat-box">
                        <h5>Total Posts</h5>
                        <span id="statTotalPosts">0</span>
                    </div>
                    <div class="stat-box">
                        <h5>Total Views</h5>
                        <span id="statTotalViews">0</span>
                    </div>
                </div>

                <!-- Registered Users Section -->
                <h4 style="font-size: 13px; margin-bottom: 6px; color: var(--text);"><i class="fa-solid fa-users"></i> Registered Users Data</h4>
                <div style="max-height: 160px; overflow-y: auto; margin-bottom: 15px; border: 1px solid var(--border); border-radius: 8px;">
                    <table class="admin-table">
                        <thead><tr><th>Email</th><th>Auth Method</th><th>Action</th></tr></thead>
                        <tbody id="adminUsersTableBody"></tbody>
                    </table>
                </div>

                <hr style="margin: 15px 0; border:0; border-top:1px solid var(--border);">

                <!-- Unlimited Posts Creator -->
                <h4 style="font-size: 13px; margin-bottom: 6px; color: var(--text);"><i class="fa-solid fa-newspaper"></i> Create Unlimited Post</h4>
                <input type="text" id="postTitleInput" placeholder="Post Title">
                <select id="postCategory">
                    <option value="Free Earning">Free Earning</option>
                    <option value="Investment">Investment</option>
                    <option value="Apps & Games">Apps & Games</option>
                    <option value="Social Media Tasks">Social Media Tasks</option>
                </select>
                <textarea id="postDescInput" placeholder="Write description & instructions..."></textarea>
                <input type="text" id="postUrlInput" placeholder="Target Joining Link (https://...)">
                
                <label style="font-size: 11px; font-weight: 600; color: #94a3b8; display: block; margin-bottom: 4px;">Attach Image (Base64)</label>
                <input type="file" id="postImageInput" accept="image/*" style="padding: 6px;">
                <button class="btn" onclick="uploadPost()"><i class="fa-solid fa-paper-plane"></i> Publish Live Post</button>
                
                <hr style="margin: 15px 0; border:0; border-top:1px solid var(--border);">
                
                <!-- Ad Manager Section -->
                <h4 style="font-size: 13px; margin-bottom: 6px; color: var(--text);"><i class="fa-solid fa-rectangle-ad"></i> Configure Popup Ad & Interval</h4>
                <input type="text" id="adTitleInput" placeholder="Ad Title" value="🚀 Vestify Pro - Cloud Mining & Affiliate Earnings!">
                <input type="text" id="adDescInput" placeholder="Ad Short Text" value="Start your cloud mining journey today. Earn daily profits and grow your income securely!">
                <input type="text" id="adUrlInput" placeholder="Ad Target Link" value="https://bit.ly/4zqAtFi">
                <select id="adIntervalSelect">
                    <option value="2">Show every 2 minutes</option>
                    <option value="4">Show every 4 minutes</option>
                    <option value="5" selected>Show every 5 minutes</option>
                    <option value="10">Show every 10 minutes</option>
                </select>
                <input type="file" id="adImageInput" accept="image/*" style="padding: 6px;">
                <button class="btn" style="background:#2563eb;" onclick="publishAd()">Update Live Ad Settings</button>
                <button class="btn btn-danger" style="margin-top: 8px;" onclick="deleteActiveAd()">
                    <i class="fa-solid fa-trash"></i> Remove / Turn Off Active Ad
                </button>

                <hr style="margin: 15px 0; border:0; border-top:1px solid var(--border);">

                <!-- Realtime Help Messages from Users -->
                <h4 style="font-size: 13px; margin-bottom: 6px; color: var(--text);"><i class="fa-solid fa-headset"></i> User Help Messages</h4>
                <div id="adminHelpMessagesList" style="max-height: 150px; overflow-y: auto; margin-bottom: 15px;"></div>

                <hr style="margin: 15px 0; border:0; border-top:1px solid var(--border);">
                <h4 style="font-size: 13px; margin-bottom: 8px; color: var(--text);">Active Posts Control & Deletion</h4>
                <div id="adminDeleteList" style="max-height: 150px; overflow-y: auto;"></div>
            </div>
        </div>

    </div>

    <!-- Bottom App Navigation Bar -->
    <nav class="app-bottom-nav">
        <button class="nav-item active" onclick="switchTab('Home', this)">
            <i class="fa-solid fa-house"></i>Home
        </button>
        <button class="nav-item" onclick="switchTab('Help', this)">
            <i class="fa-solid fa-headset"></i>Help
        </button>
        <button class="nav-item" onclick="switchTab('Account', this)">
            <i class="fa-solid fa-user"></i>Account
        </button>
    </nav>

    <!-- Firebase SDK Scripts -->
    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
        import { getAuth, createUserWithEmailAndPassword, signInWithEmailAndPassword, signInWithPopup, GoogleAuthProvider, onAuthStateChanged, signOut } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-auth.js";
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
        const googleProvider = new GoogleAuthProvider();

        let isSignUpMode = false;
        let allPostsData = [];
        let currentFilter = 'All';
        let searchQuery = '';

        // --- PWA Install Prompt Handler ---
        let deferredPrompt;
        window.addEventListener('beforeinstallprompt', (e) => {
            e.preventDefault();
            deferredPrompt = e;
            document.getElementById('pwaInstallCard').classList.remove('hidden');
        });

        document.getElementById('pwaInstallBtn').addEventListener('click', async () => {
            if (deferredPrompt) {
                deferredPrompt.prompt();
                const { outcome } = await deferredPrompt.userChoice;
                if (outcome === 'accepted') {
                    document.getElementById('pwaInstallCard').classList.add('hidden');
                }
                deferredPrompt = null;
            }
        });

        // --- Dark Mode Handler ---
        window.toggleDarkMode = () => {
            document.body.classList.toggle('dark-mode');
            const isDark = document.body.classList.contains('dark-mode');
            localStorage.setItem('prime_dark_mode', isDark);
            document.getElementById('themeIcon').className = isDark ? "fa-solid fa-sun" : "fa-solid fa-moon";
        };

        if (localStorage.getItem('prime_dark_mode') === 'true') {
            document.body.classList.add('dark-mode');
            document.getElementById('themeIcon').className = "fa-solid fa-sun";
        }

        function showLoader(text = "Processing...") {
            document.getElementById('loadingText').innerText = text;
            document.getElementById('loadingOverlay').classList.remove('hidden');
        }
        function hideLoader() {
            document.getElementById('loadingOverlay').classList.add('hidden');
        }

        // --- App Tab Switcher ---
        window.switchTab = (tabName, btnElement) => {
            document.getElementById('tabHome').classList.add('hidden');
            document.getElementById('tabHelp').classList.add('hidden');
            document.getElementById('tabAccount').classList.add('hidden');
            document.getElementById('tabAdmin').classList.add('hidden');

            document.querySelectorAll('.nav-item').forEach(el => el.classList.remove('active'));
            if(btnElement) btnElement.classList.add('active');

            if(tabName === 'Home') document.getElementById('tabHome').classList.remove('hidden');
            if(tabName === 'Help') document.getElementById('tabHelp').classList.remove('hidden');
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

        // --- Auth & User Recording System ---
        window.toggleAuthMode = () => {
            isSignUpMode = !isSignUpMode;
            document.getElementById('authTitle').innerText = isSignUpMode ? "Create New Account" : "Account Login";
            document.getElementById('authSubmitBtn').innerText = isSignUpMode ? "Sign Up" : "Login";
        };

        function saveUserDataToDB(user, authType) {
            set(ref(db, 'users/' + user.uid), {
                email: user.email || "No Email",
                authMethod: authType,
                lastLogin: Date.now()
            });
        }

        window.submitAuth = () => {
            const email = document.getElementById('authEmail').value;
            const pass = document.getElementById('authPassword').value;
            if(!email || !pass) { alert("Enter email and password sweetie!"); return; }
            showLoader("Authenticating...");

            if(isSignUpMode) {
                createUserWithEmailAndPassword(auth, email, pass)
                    .then((res) => { saveUserDataToDB(res.user, "Email/Password"); hideLoader(); alert("Account created successfully!"); })
                    .catch(e => { hideLoader(); alert(e.message); });
            } else {
                signInWithEmailAndPassword(auth, email, pass)
                    .then((res) => { saveUserDataToDB(res.user, "Email/Password"); hideLoader(); alert("Logged in successfully!"); })
                    .catch(e => { hideLoader(); alert(e.message); });
            }
        };

        window.loginWithGoogle = () => {
            showLoader("Connecting with Google...");
            signInWithPopup(auth, googleProvider)
                .then((res) => { saveUserDataToDB(res.user, "Google"); hideLoader(); alert("Google login successful!"); })
                .catch(e => { hideLoader(); alert(e.message); });
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

        // --- Base64 Image Converter Helper ---
        function getBase64(file, callback) {
            const reader = new FileReader();
            reader.readAsDataURL(file);
            reader.onload = () => callback(reader.result);
            reader.onerror = error => console.log('Error: ', error);
        }

        // --- Unlimited Post Creation (Base64) ---
        window.uploadPost = () => {
            const title = document.getElementById('postTitleInput').value.trim();
            const category = document.getElementById('postCategory').value;
            const description = document.getElementById('postDescInput').value.trim();
            const url = document.getElementById('postUrlInput').value.trim();
            const imageFile = document.getElementById('postImageInput').files[0];

            if(!title || !url) { alert("Title and Link are required sweetie!"); return; }
            showLoader("Publishing post...");

            const saveData = (imageBase64 = "") => {
                push(ref(db, 'posts'), { 
                    title, category, description, url, 
                    image: imageBase64, 
                    likes: 0, 
                    views: 0,
                    totalRating: 0,
                    ratingCount: 0,
                    timestamp: Date.now() 
                }).then(() => {
                    document.getElementById('postTitleInput').value = '';
                    document.getElementById('postDescInput').value = '';
                    document.getElementById('postUrlInput').value = '';
                    document.getElementById('postImageInput').value = '';
                    hideLoader();
                    alert("Posted live successfully!");
                    switchTab('Home', document.querySelector('.app-bottom-nav .nav-item'));
                });
            };

            if (imageFile) {
                getBase64(imageFile, (base64String) => saveData(base64String));
            } else {
                saveData("");
            }
        };

        // --- Ad Configuration & Interval System ---
        window.publishAd = () => {
            const title = document.getElementById('adTitleInput').value.trim();
            const description = document.getElementById('adDescInput').value.trim();
            const url = document.getElementById('adUrlInput').value.trim();
            const interval = parseInt(document.getElementById('adIntervalSelect').value) || 5;
            const imageFile = document.getElementById('adImageInput').files[0];

            showLoader("Updating Ad settings...");
            const saveAdData = (imgBase64 = "") => {
                set(ref(db, 'activeAd'), {
                    title, description, url, interval,
                    image: imgBase64,
                    active: true
                }).then(() => { hideLoader(); alert("Live Ad & interval settings updated!"); });
            };

            if (imageFile) {
                getBase64(imageFile, (base64) => saveAdData(base64));
            } else {
                saveAdData("");
            }
        };

        window.deleteActiveAd = () => {
            if(confirm("Kya aap active ad ko remove karna chahte hain sweetie?")) {
                showLoader("Removing ad...");
                remove(ref(db, 'activeAd'))
                    .then(() => {
                        hideLoader();
                        document.getElementById('adTitleInput').value = '';
                        document.getElementById('adDescInput').value = '';
                        document.getElementById('adUrlInput').value = '';
                        document.getElementById('adImageInput').value = '';
                        alert("Active ad successfully remove kar diya gaya hai!");
                    })
                    .catch(e => { hideLoader(); alert(e.message); });
            }
        };

        // --- Help Message System ---
        window.sendHelpMessage = () => {
            const name = document.getElementById('helpUserName').value.trim();
            const email = document.getElementById('helpUserEmail').value.trim();
            const message = document.getElementById('helpUserMsg').value.trim();

            if(!name || !message) { alert("Please provide your name and message sweetie!"); return; }
            showLoader("Sending message...");

            push(ref(db, 'helpMessages'), {
                name, email, message, timestamp: Date.now()
            }).then(() => {
                document.getElementById('helpUserMsg').value = '';
                hideLoader();
                alert("Your message has been sent to Prime Solutions Admin successfully!");
            });
        };

        window.deletePost = (id) => { if(confirm("Delete this post?")) remove(ref(db, 'posts/' + id)); };
        window.deleteUser = (uid) => { if(confirm("Remove user from records?")) remove(ref(db, 'users/' + uid)); };
        window.deleteHelpMsg = (id) => { remove(ref(db, 'helpMessages/' + id)); };
        window.likePost = (id, likes) => update(ref(db, 'posts/' + id), { likes: (likes || 0) + 1 });
        
        // --- Star Rating Handler ---
        window.ratePost = (id, currentTotal, currentCount, ratingVal) => {
            let ratedPosts = JSON.parse(localStorage.getItem('prime_rated_posts') || '{}');
            if(ratedPosts[id]) {
                alert("Aap is post ko pehle hi rate kar chuke hain sweetie!");
                return;
            }
            ratedPosts[id] = ratingVal;
            localStorage.setItem('prime_rated_posts', JSON.stringify(ratedPosts));

            update(ref(db, 'posts/' + id), {
                totalRating: (currentTotal || 0) + ratingVal,
                ratingCount: (currentCount || 0) + 1
            });
            alert(`Thank you for rating ${ratingVal} stars sweetie!`);
        };

        // --- Social Share Handler ---
        window.shareOnSocial = (platform, title, url) => {
            let shareText = encodeURIComponent(`Check out this amazing opportunity on Prime Solutions: ${title}\nLink: ${url}`);
            let shareUrl = "";
            if(platform === 'whatsapp') {
                shareUrl = `https://api.whatsapp.com/send?text=${shareText}`;
            } else if(platform === 'facebook') {
                shareUrl = `https://www.facebook.com/sharer/sharer.php?u=${encodeURIComponent(url)}`;
            } else if(platform === 'telegram') {
                shareUrl = `https://t.me/share/url?url=${encodeURIComponent(url)}&text=${encodeURIComponent(title)}`;
            }
            window.open(shareUrl, '_blank');
        };

        // --- Bookmark / Saved Posts System ---
        window.toggleBookmark = (id) => {
            let saved = JSON.parse(localStorage.getItem('prime_saved_posts') || '[]');
            if(saved.includes(id)) {
                saved = saved.filter(item => item !== id);
                alert("Post removed from saved bookmarks!");
            } else {
                saved.push(id);
                alert("Post saved to bookmarks successfully!");
            }
            localStorage.setItem('prime_saved_posts', JSON.stringify(saved));
            renderFeed();
        };

        window.viewPostLink = (id, url, currentViews) => {
            update(ref(db, 'posts/' + id), { views: (currentViews || 0) + 1 });
            window.open(url, '_blank');
        };

        window.copyPostLink = (url) => { navigator.clipboard.writeText(url); alert("Link copied!"); };

        window.filterPosts = (cat, btn) => {
            currentFilter = cat;
            document.querySelectorAll('.pill-btn').forEach(b => b.classList.remove('active'));
            btn.classList.add('active');
            renderFeed();
        };

        window.handleSearch = () => {
            searchQuery = document.getElementById('searchInput').value.toLowerCase().trim();
            renderFeed();
        };

        // --- Admin Data Sync & Analytics ---
        onValue(ref(db, 'users'), (snapshot) => {
            const data = snapshot.val();
            const userTable = document.getElementById('adminUsersTableBody');
            userTable.innerHTML = '';
            let userCount = 0;
            if(data) {
                userCount = Object.keys(data).length;
                Object.keys(data).forEach(uid => {
                    userTable.innerHTML += `
                        <tr>
                            <td>${escapeHtml(data[uid].email)}</td>
                            <td>${escapeHtml(data[uid].authMethod)}</td>
                            <td><button class="btn btn-danger" style="width:auto; padding:2px 6px; font-size:10px;" onclick="deleteUser('${uid}')">Remove</button></td>
                        </tr>
                    `;
                });
            }
            document.getElementById('statTotalUsers').innerText = userCount;
        });

        onValue(ref(db, 'helpMessages'), (snapshot) => {
            const data = snapshot.val();
            const helpList = document.getElementById('adminHelpMessagesList');
            helpList.innerHTML = '';
            if(data) {
                Object.keys(data).forEach(id => {
                    helpList.innerHTML += `
                        <div style="padding:8px; border-bottom:1px solid #f1f5f9; font-size:11px;">
                            <strong>${escapeHtml(data[id].name)}</strong> (${escapeHtml(data[id].email || 'N/A')}):<br>
                            ${escapeHtml(data[id].message)}
                            <div style="text-align: right; margin-top: 4px;">
                                <button class="btn btn-danger" style="width:auto; padding:2px 6px; font-size:10px;" onclick="deleteHelpMsg('${id}')">Delete</button>
                            </div>
                        </div>
                    `;
                });
            }
        });

        // --- Dynamic Ad Timer Loop ---
        let adIntervalMinutes = 5;
        onValue(ref(db, 'activeAd'), (snapshot) => {
            const adData = snapshot.val();
            if (adData && adData.active) {
                document.getElementById('adTitleText').innerText = adData.title || "Sponsored Ad";
                document.getElementById('adDescText').innerText = adData.description || "";
                document.getElementById('adLinkBtn').href = adData.url || "#";
                adIntervalMinutes = parseInt(adData.interval) || 5;
                
                const mediaDiv = document.getElementById('adMediaContainer');
                mediaDiv.innerHTML = adData.image ? `<img src="${adData.image}" class="ad-content-img">` : '';
            }
        });

        setInterval(() => {
            const adPopup = document.getElementById('adPopup');
            adPopup.classList.remove('hidden');

            let timeLeft = 5;
            const timerBadge = document.getElementById('adTimerBadge');
            timerBadge.innerText = `Closing in ${timeLeft}s`;

            const timerInterval = setInterval(() => {
                timeLeft--;
                timerBadge.innerText = `Closing in ${timeLeft}s`;
                if (timeLeft <= 0) {
                    clearInterval(timerInterval);
                    adPopup.classList.add('hidden');
                }
            }, 1000);
        }, adIntervalMinutes * 60 * 1000);

        // --- Fake Engagement Notifications Loop ---
        const fakeNames = ["Ali Khan", "Zainab", "Bilal Ahmed", "Sana", "Hamza", "Ayesha"];
        const fakeActions = ["just joined Free Earning!", "withdrew $20 successfully!", "completed a social media task!", "unlocked VIP portal access!"];
        
        setInterval(() => {
            const randomName = fakeNames[Math.floor(Math.random() * fakeNames.length)];
            const randomAction = fakeActions[Math.floor(Math.random() * fakeActions.length)];
            const notif = document.getElementById('fakeNotification');
            document.getElementById('fakeNotifText').innerText = `${randomName} ${randomAction}`;
            
            notif.classList.add('show');
            setTimeout(() => { notif.classList.remove('show'); }, 4000);
        }, 18000);

        // --- Posts Sync & Analytics Rendering ---
        onValue(ref(db, 'posts'), (snapshot) => {
            const data = snapshot.val();
            allPostsData = [];
            const deleteList = document.getElementById('adminDeleteList');
            deleteList.innerHTML = '';
            let totalPostsCount = 0;
            let totalViewsCount = 0;

            if(data) {
                totalPostsCount = Object.keys(data).length;
                Object.keys(data).forEach(key => {
                    const postItem = data[key];
                    totalViewsCount += (postItem.views || 0);
                    allPostsData.push({ id: key, ...postItem });
                    deleteList.innerHTML += `
                        <div style="display:flex; justify-content:space-between; align-items:center; padding:6px 0; border-bottom:1px solid #f1f5f9; font-size:11px;">
                            <span>${escapeHtml(postItem.title)}</span>
                            <button class="btn btn-danger" style="width:auto; padding:2px 8px; font-size:10px;" onclick="deletePost('${key}')">Delete</button>
                        </div>
                    `;
                });
            }
            document.getElementById('statTotalPosts').innerText = totalPostsCount;
            document.getElementById('statTotalViews').innerText = totalViewsCount;
            renderFeed();
        });

        function renderFeed() {
            const container = document.getElementById('feedContainer');
            container.innerHTML = '';
            
            let filtered = allPostsData;
            
            if(currentFilter === 'Saved') {
                const savedIds = JSON.parse(localStorage.getItem('prime_saved_posts') || '[]');
                filtered = filtered.filter(p => savedIds.includes(p.id));
            } else if(currentFilter !== 'All') {
                filtered = filtered.filter(p => p.category === currentFilter);
            }

            if(searchQuery !== '') {
                filtered = filtered.filter(p => p.title.toLowerCase().includes(searchQuery) || p.description.toLowerCase().includes(searchQuery));
            }

            filtered.sort((a, b) => b.timestamp - a.timestamp);

            if(filtered.length === 0) {
                container.innerHTML = '<div style="text-align: center; color: #94a3b8; padding: 40px; font-size: 13px;">No updates found!</div>';
                return;
            }

            const savedIds = JSON.parse(localStorage.getItem('prime_saved_posts') || '[]');
            const ratedPosts = JSON.parse(localStorage.getItem('prime_rated_posts') || '{}');

            filtered.forEach(post => {
                let timeStr = new Date(post.timestamp).toLocaleDateString() + ' ' + new Date(post.timestamp).toLocaleTimeString([], {hour: '2-digit', minute:'2-digit'});
                let imageHTML = post.image ? `<img src="${post.image}" class="post-img">` : '';
                let isBookmarked = savedIds.includes(post.id);
                let bookmarkIconClass = isBookmarked ? "fa-solid fa-bookmark" : "fa-regular fa-bookmark";

                // Average Rating Calculation
                let avgRating = 0;
                if(post.ratingCount && post.ratingCount > 0) {
                    avgRating = (post.totalRating / post.ratingCount).toFixed(1);
                }

                let starsHtml = '';
                for(let i=1; i<=5; i++) {
                    let starClass = (i <= Math.round(avgRating)) ? "fa-solid fa-star rated" : "fa-regular fa-star";
                    starsHtml += `<i class="${starClass}" onclick="ratePost('${post.id}', ${post.totalRating || 0}, ${post.ratingCount || 0}, ${i})" title="Rate ${i} Stars"></i>`;
                }

                container.innerHTML += `
                    <div class="app-card">
                        <div class="post-top">
                            <div class="post-heading">${escapeHtml(post.title)}</div>
                            <span class="app-badge">${escapeHtml(post.category || 'General')}</span>
                        </div>
                        <div class="post-meta-row">
                            <span>${timeStr}</span>
                            <span><i class="fa-solid fa-eye"></i> ${post.views || 0} views</span>
                        </div>
                        
                        <!-- Star Rating Display & Interactive Box -->
                        <div class="star-rating-box">
                            <div>${starsHtml}</div>
                            <span style="font-size:11px; font-weight:600; color:var(--text); margin-left:6px;">(${avgRating} / ${post.ratingCount || 0} ratings)</span>
                        </div>

                        <div class="post-body">${escapeHtml(post.description)}</div>
                        ${imageHTML}
                        
                        <div style="margin-bottom: 10px;">
                            <a href="javascript:void(0)" onclick="viewPostLink('${post.id}', '${escapeHtml(post.url)}', ${post.views || 0})" class="app-action-btn join-btn" style="text-decoration:none; display:inline-flex;">
                                <i class="fa-solid fa-arrow-up-right-from-square"></i> Visit Link / Join Now
                            </a>
                        </div>

                        <!-- Social Share Buttons Row -->
                        <div style="display: flex; gap: 6px; margin-bottom: 10px;">
                            <button class="app-action-btn" style="background:#25d366; color:white; border:none; flex:1; justify-content:center;" onclick="shareOnSocial('whatsapp', '${escapeHtml(post.title)}', '${escapeHtml(post.url)}')">
                                <i class="fa-brands fa-whatsapp"></i> Share
                            </button>
                            <button class="app-action-btn" style="background:#1877f2; color:white; border:none; flex:1; justify-content:center;" onclick="shareOnSocial('facebook', '${escapeHtml(post.title)}', '${escapeHtml(post.url)}')">
                                <i class="fa-brands fa-facebook"></i> Share
                            </button>
                            <button class="app-action-btn" style="background:#229ed9; color:white; border:none; flex:1; justify-content:center;" onclick="shareOnSocial('telegram', '${escapeHtml(post.title)}', '${escapeHtml(post.url)}')">
                                <i class="fa-brands fa-telegram"></i> Share
                            </button>
                        </div>

                        <div class="post-action-bar">
                            <button class="app-action-btn" onclick="likePost('${post.id}', ${post.likes || 0})">
                                <i class="fa-solid fa-heart" style="color: #ef4444;"></i> (${post.likes || 0})
                            </button>
                            <button class="app-action-btn" onclick="toggleBookmark('${post.id}')" style="color: ${isBookmarked ? 'var(--accent)' : 'inherit'};">
                                <i class="${bookmarkIconClass}"></i> ${isBookmarked ? 'Saved' : 'Save'}
                            </button>
                            <button class="app-action-btn" onclick="copyPostLink('${escapeHtml(post.url)}')">
                                <i class="fa-solid fa-copy"></i> Copy
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
