<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PrimeX - Ultimate Social Ecosystem</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        .no-scrollbar::-webkit-scrollbar { display: none; }
        .no-scrollbar { -ms-overflow-style: none; scrollbar-width: none; }
        .reel-snap { scroll-snap-type: y mandatory; }
        .reel-item { scroll-snap-align: start; }
    </style>
</head>
<body class="bg-black text-white min-h-screen flex justify-center font-sans overflow-hidden">

    <div class="w-full max-w-md h-screen flex flex-col justify-between bg-gray-950 relative border-x border-gray-800">

        <!-- Top Header -->
        <header class="h-14 border-b border-gray-800 px-4 flex justify-between items-center bg-gray-950/90 backdrop-blur z-20 sticky top-0">
            <h1 class="text-xl font-black tracking-wider text-indigo-500">PrimeX<span class="text-xs text-amber-400 font-bold ml-1">v5.0 PRO</span></h1>
            <div id="user-header-actions" class="flex items-center gap-2 hidden">
                <button id="btn-go-live" class="bg-rose-600 hover:bg-rose-700 text-xs px-2.5 py-1 rounded-full font-bold transition flex items-center gap-1 shadow-lg shadow-rose-600/30 animate-pulse">
                    <i class="fa-solid fa-video"></i> LIVE
                </button>
                <button id="btn-open-chat" class="text-gray-300 hover:text-indigo-400 text-lg p-1 transition">
                    <i class="fa-solid fa-paper-plane"></i>
                </button>
                <button id="btn-create-post" class="bg-indigo-600 hover:bg-indigo-700 text-xs px-2.5 py-1 rounded-full font-bold transition flex items-center gap-1 shadow-lg shadow-indigo-600/30">
                    <i class="fa-solid fa-cloud-arrow-up"></i>
                </button>
                <button id="btn-logout" class="text-gray-400 hover:text-red-400 text-xs p-1 transition">
                    <i class="fa-solid fa-right-from-bracket text-lg"></i>
                </button>
            </div>
        </header>

        <!-- Auth View -->
        <main id="auth-view" class="flex-1 p-6 flex flex-col justify-center items-center">
            <div class="w-full bg-gray-900 border border-gray-800 rounded-3xl p-6 shadow-2xl text-center">
                <h2 class="text-2xl font-black mb-1">Join PrimeX</h2>
                <p class="text-gray-400 text-xs mb-6">Next-Gen Media, Live & Financial Platform</p>

                <button id="btn-google" class="w-full bg-white text-gray-900 font-semibold py-2.5 px-4 rounded-xl flex items-center justify-center gap-3 transition mb-4 shadow">
                    <i class="fa-brands fa-google text-red-500 text-lg"></i>
                    <span>Continue with Google</span>
                </button>

                <div class="flex items-center my-4">
                    <hr class="flex-grow border-gray-800">
                    <span class="px-3 text-xs text-gray-500">OR</span>
                    <hr class="flex-grow border-gray-800">
                </div>

                <form id="auth-form" class="space-y-3">
                    <input type="email" id="email" placeholder="Email Address" required class="w-full bg-gray-950 border border-gray-800 rounded-xl px-4 py-2.5 text-sm focus:outline-none focus:border-indigo-500">
                    <input type="password" id="password" placeholder="Password" required class="w-full bg-gray-950 border border-gray-800 rounded-xl px-4 py-2.5 text-sm focus:outline-none focus:border-indigo-500">
                    
                    <div class="flex gap-2 pt-2">
                        <button type="submit" id="btn-login" class="w-1/2 bg-indigo-600 hover:bg-indigo-700 font-bold py-2.5 rounded-xl text-xs uppercase tracking-wider transition">Login</button>
                        <button type="button" id="btn-signup" class="w-1/2 bg-gray-800 hover:bg-gray-700 font-bold py-2.5 rounded-xl text-xs uppercase tracking-wider transition">Sign Up</button>
                    </div>
                </form>

                <p id="auth-error" class="text-red-400 text-xs mt-3 hidden"></p>
            </div>
        </main>

        <!-- Main Content Views -->
        <main id="app-view" class="flex-1 overflow-y-auto no-scrollbar hidden relative">
            
            <!-- Home Feed View -->
            <div id="view-home" class="h-full w-full flex flex-col">
                <div class="h-20 border-b border-gray-800 flex items-center gap-3 px-4 overflow-x-auto no-scrollbar bg-gray-950/50">
                    <div class="flex flex-col items-center gap-1 cursor-pointer">
                        <div class="w-12 h-12 rounded-full border-2 border-indigo-500 flex items-center justify-center bg-gray-800 text-indigo-400 shadow">
                            <i class="fa-solid fa-plus"></i>
                        </div>
                        <span class="text-[10px] text-gray-400">Your Story</span>
                    </div>
                    <div id="stories-container" class="flex items-center gap-3"></div>
                </div>

                <div id="reels-feed" class="flex-1 overflow-y-scroll reel-snap no-scrollbar"></div>
            </div>

            <!-- Explore View -->
            <div id="view-explore" class="h-full w-full p-4 hidden overflow-y-auto no-scrollbar">
                <div class="relative mb-4">
                    <i class="fa-solid fa-magnifying-glass absolute left-3 top-3 text-gray-400"></i>
                    <input type="text" placeholder="Search creators, live streams..." class="w-full bg-gray-900 border border-gray-800 rounded-xl pl-9 pr-4 py-2 text-sm focus:outline-none">
                </div>
                <h3 class="text-sm font-bold text-indigo-400 mb-3"><i class="fa-solid fa-fire mr-1"></i> AI Trending Shorts</h3>
                <div id="explore-grid" class="grid grid-cols-2 gap-2"></div>
            </div>

            <!-- Wallet View -->
            <div id="view-wallet" class="h-full w-full p-6 hidden overflow-y-auto no-scrollbar">
                <div class="bg-gradient-to-r from-indigo-900 to-purple-900 border border-indigo-500/30 rounded-2xl p-5 mb-6 text-center shadow-lg">
                    <span class="text-xs uppercase font-bold text-indigo-300">Creator Coins Wallet</span>
                    <h2 class="text-4xl font-extrabold my-2 text-amber-400 flex items-center justify-center gap-2">
                        <i class="fa-solid fa-coins"></i> <span id="wallet-coins">0</span>
                    </h2>
                    <p class="text-xs text-gray-300">Estimated value: <span id="wallet-pkr" class="text-emerald-400 font-bold">0 PKR</span></p>
                </div>
                
                <h3 class="text-sm font-bold mb-3">Withdraw Gateway</h3>
                <div class="space-y-2">
                    <div class="bg-gray-900 border border-gray-800 p-3 rounded-xl flex justify-between items-center">
                        <span class="text-xs font-semibold">EasyPaisa / JazzCash</span>
                        <button class="bg-emerald-600 hover:bg-emerald-700 text-[10px] font-bold px-3 py-1.5 rounded-lg">Withdraw</button>
                    </div>
                    <div class="bg-gray-900 border border-gray-800 p-3 rounded-xl flex justify-between items-center">
                        <span class="text-xs font-semibold">Binance Crypto (USDT)</span>
                        <button class="bg-emerald-600 hover:bg-emerald-700 text-[10px] font-bold px-3 py-1.5 rounded-lg">Withdraw</button>
                    </div>
                </div>
            </div>

            <!-- Profile & Creator Analytics View -->
            <div id="view-profile" class="h-full w-full p-6 hidden overflow-y-auto no-scrollbar">
                <div class="text-center">
                    <div id="profile-avatar" class="w-20 h-20 bg-indigo-600 rounded-full mx-auto flex items-center justify-center text-2xl font-black mb-2 border-2 border-indigo-400 shadow-lg">U</div>
                    <h2 class="text-lg font-bold flex items-center justify-center gap-1">
                        <span id="profile-name">User Name</span>
                        <i class="fa-solid fa-circle-check text-indigo-400 text-sm" title="Verified Creator"></i>
                    </h2>
                    <p class="text-xs text-indigo-400 font-semibold mb-4">PrimeX Verified Creator</p>
                </div>

                <div class="flex justify-around bg-gray-900 border border-gray-800 p-3 rounded-xl mb-6 text-center">
                    <div><span class="block font-bold text-sm">12</span><span class="text-[10px] text-gray-400">Posts</span></div>
                    <div><span class="block font-bold text-sm">1.4K</span><span class="text-[10px] text-gray-400">Followers</span></div>
                    <div><span class="block font-bold text-sm">350</span><span class="text-[10px] text-gray-400">Coins</span></div>
                </div>

                <!-- Creator Analytics Dashboard -->
                <h3 class="text-xs font-bold text-gray-400 uppercase tracking-wider mb-2">Creator Engagement Analytics</h3>
                <div class="bg-gray-900 border border-gray-800 rounded-xl p-4 space-y-3 mb-6">
                    <div class="flex justify-between items-center text-xs">
                        <span class="text-gray-400">Profile Impressions</span>
                        <span class="font-bold text-emerald-400">+24.5% (8.2K)</span>
                    </div>
                    <div class="w-full bg-gray-950 h-2 rounded-full overflow-hidden">
                        <div class="bg-indigo-500 h-full w-[75%]"></div>
                    </div>
                    <div class="flex justify-between items-center text-xs">
                        <span class="text-gray-400">Video Watch Time</span>
                        <span class="font-bold text-indigo-400">142 Hours</span>
                    </div>
                </div>
            </div>

            <!-- Upload Modal (With Music Selector) -->
            <div id="upload-modal" class="fixed inset-0 bg-black/80 backdrop-blur-sm z-50 flex items-center justify-center p-4 hidden">
                <div class="bg-gray-900 border border-gray-800 w-full max-w-sm rounded-2xl p-5 relative">
                    <button id="close-modal" class="absolute top-4 right-4 text-gray-400 hover:text-white"><i class="fa-solid fa-xmark text-lg"></i></button>
                    <h3 class="text-lg font-bold mb-4">Upload Media Post</h3>
                    
                    <textarea id="post-caption" rows="2" placeholder="Write caption..." class="w-full bg-gray-950 border border-gray-800 rounded-xl p-3 text-sm focus:outline-none focus:border-indigo-500 mb-3 resize-none"></textarea>
                    
                    <div class="mb-3">
                        <label class="block text-xs font-bold text-gray-400 mb-1">Select Audio / Music Track:</label>
                        <select id="post-music-select" class="w-full bg-gray-950 border border-gray-800 text-xs rounded-xl p-2.5 text-indigo-300 focus:outline-none">
                            <option value="PrimeX Original Sound">🎵 PrimeX Original Sound</option>
                            <option value="Trending Beat 2026">🔥 Trending Beat 2026</option>
                            <option value="Aesthetic Lofi Chill">🎧 Aesthetic Lofi Chill</option>
                        </select>
                    </div>

                    <div class="mb-4">
                        <label class="block text-xs font-bold text-gray-400 mb-1">Select Image/Video File:</label>
                        <input type="file" id="post-file-input" accept="image/*,video/*" class="w-full text-xs text-gray-400 bg-gray-950 border border-gray-800 rounded-xl p-2 cursor-pointer">
                    </div>

                    <div id="upload-status" class="text-xs text-indigo-400 font-bold mb-3 hidden text-center">
                        <i class="fa-solid fa-spinner fa-spin mr-1"></i> Uploading to Cloud...
                    </div>

                    <button id="btn-submit-post" class="w-full bg-indigo-600 hover:bg-indigo-700 font-bold py-2.5 rounded-xl text-sm transition">Publish Post</button>
                </div>
            </div>

            <!-- Live Streaming Modal (TikTok-Style Gifting) -->
            <div id="live-stream-modal" class="fixed inset-0 bg-black z-50 hidden flex flex-col justify-between p-4">
                <div class="flex justify-between items-center z-10">
                    <div class="flex items-center gap-2 bg-black/50 backdrop-blur px-3 py-1.5 rounded-full border border-gray-800">
                        <span class="w-2 h-2 rounded-full bg-rose-500 animate-ping"></span>
                        <span class="text-xs font-bold text-rose-500">LIVE</span>
                        <span class="text-xs text-gray-300 font-semibold"><i class="fa-solid fa-eye text-xs ml-1"></i> 1.2K</span>
                    </div>
                    <button id="btn-close-live" class="w-8 h-8 bg-gray-900 rounded-full flex items-center justify-center text-white"><i class="fa-solid fa-xmark"></i></button>
                </div>

                <div class="flex-1 flex items-center justify-center text-center">
                    <div>
                        <i class="fa-solid fa-broadcast-tower text-6xl text-rose-500 mb-3 animate-pulse"></i>
                        <h3 class="text-xl font-bold">You are Live on PrimeX!</h3>
                        <p class="text-xs text-gray-400">Broadcasting to global followers...</p>
                    </div>
                </div>

                <!-- Virtual Gifting Bar -->
                <div class="bg-gray-900/80 backdrop-blur border border-gray-800 rounded-2xl p-3 flex justify-around items-center">
                    <button onclick="sendVirtualGift('Heart 💖', 5)" class="flex flex-col items-center text-rose-400 hover:scale-110 transition">
                        <span class="text-xl">💖</span>
                        <span class="text-[9px] font-bold">5 Coins</span>
                    </button>
                    <button onclick="sendVirtualGift('Crown 👑', 50)" class="flex flex-col items-center text-amber-400 hover:scale-110 transition">
                        <span class="text-xl">👑</span>
                        <span class="text-[9px] font-bold">50 Coins</span>
                    </button>
                    <button onclick="sendVirtualGift('Rocket 🚀', 100)" class="flex flex-col items-center text-indigo-400 hover:scale-110 transition">
                        <span class="text-xl">🚀</span>
                        <span class="text-[9px] font-bold">100 Coins</span>
                    </button>
                </div>
            </div>

            <!-- Direct Messenger Modal (With Audio/Video Call Buttons) -->
            <div id="view-chat" class="fixed inset-0 bg-gray-950 z-40 hidden flex flex-col">
                <div class="h-14 border-b border-gray-800 px-4 flex items-center justify-between">
                    <div class="flex items-center gap-3">
                        <button id="btn-close-chat" class="text-gray-400 text-lg"><i class="fa-solid fa-arrow-left"></i></button>
                        <h3 class="font-bold text-sm">PrimeX Messenger</h3>
                    </div>
                    <div class="flex items-center gap-4 text-indigo-400">
                        <button onclick="triggerCall('Audio')" title="Audio Call"><i class="fa-solid fa-phone text-base"></i></button>
                        <button onclick="triggerCall('Video')" title="Video Call"><i class="fa-solid fa-video text-base"></i></button>
                    </div>
                </div>
                <div id="chat-messages" class="flex-1 p-4 overflow-y-auto space-y-3"></div>
                <div class="p-3 border-t border-gray-800 flex gap-2">
                    <input type="text" id="chat-input" placeholder="Type a message..." class="flex-1 bg-gray-900 border border-gray-800 rounded-xl px-4 py-2 text-sm focus:outline-none">
                    <button id="btn-send-msg" class="bg-indigo-600 px-4 py-2 rounded-xl text-sm font-bold"><i class="fa-solid fa-paper-plane"></i></button>
                </div>
            </div>

        </main>

        <!-- Bottom Navigation Bar -->
        <nav id="bottom-nav" class="h-16 border-t border-gray-800/80 bg-gray-950/95 backdrop-blur px-6 flex justify-between items-center z-20 hidden">
            <button onclick="switchTab('home')" id="nav-home" class="flex flex-col items-center gap-1 text-indigo-500">
                <i class="fa-solid fa-house text-lg"></i>
                <span class="text-[10px] font-medium">Home</span>
            </button>
            <button onclick="switchTab('explore')" id="nav-explore" class="flex flex-col items-center gap-1 text-gray-400 hover:text-white">
                <i class="fa-solid fa-compass text-lg"></i>
                <span class="text-[10px] font-medium">Explore</span>
            </button>
            <button id="nav-btn-create" class="flex flex-col items-center justify-center w-10 h-10 bg-indigo-600 rounded-full text-white shadow-lg shadow-indigo-500/30">
                <i class="fa-solid fa-plus text-lg"></i>
            </button>
            <button onclick="switchTab('wallet')" id="nav-wallet" class="flex flex-col items-center gap-1 text-gray-400 hover:text-white">
                <i class="fa-solid fa-wallet text-lg"></i>
                <span class="text-[10px] font-medium">Wallet</span>
            </button>
            <button onclick="switchTab('profile')" id="nav-profile" class="flex flex-col items-center gap-1 text-gray-400 hover:text-white">
                <i class="fa-solid fa-user text-lg"></i>
                <span class="text-[10px] font-medium">Profile</span>
            </button>
        </nav>

    </div>

    <!-- Firebase SDK v10 -->
    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
        import { 
            getAuth, GoogleAuthProvider, signInWithPopup, 
            createUserWithEmailAndPassword, signInWithEmailAndPassword, 
            onAuthStateChanged, signOut 
        } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-auth.js";
        import { getDatabase, ref, set, push, onValue, update } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-database.js";
        import { getStorage, ref as storageRef, uploadBytes, getDownloadURL } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-storage.js";

        const firebaseConfig = {
            apiKey: "AIzaSyCLFzI1dWn36_b3E9pzb_GU1Q3EyoRdnn0",
            authDomain: "primex-e8090.firebaseapp.com",
            databaseURL: "https://primex-e8090-default-rtdb.firebaseio.com",
            projectId: "primex-e8090",
            storageBucket: "primex-e8090.firebasestorage.app",
            messagingSenderId: "465444221491",
            appId: "1:465444221491:web:9824b4f1f9f592f76ce946",
            measurementId: "G-9LRYXH2D6E"
        };

        const app = initializeApp(firebaseConfig);
        const auth = getAuth(app);
        const db = getDatabase(app);
        const storage = getStorage(app);
        const googleProvider = new GoogleAuthProvider();

        let currentUser = null;

        const authView = document.getElementById('auth-view');
        const appView = document.getElementById('app-view');
        const bottomNav = document.getElementById('bottom-nav');
        const userHeaderActions = document.getElementById('user-header-actions');
        const reelsFeed = document.getElementById('reels-feed');
        const uploadModal = document.getElementById('upload-modal');
        const liveModal = document.getElementById('live-stream-modal');
        const uploadStatus = document.getElementById('upload-status');
        const authError = document.getElementById('auth-error');

        const showError = (msg) => {
            authError.textContent = msg;
            authError.classList.remove('hidden');
        };

        window.switchTab = (tab) => {
            ['home', 'explore', 'wallet', 'profile'].forEach(t => {
                const el = document.getElementById(`view-${t}`);
                const navEl = document.getElementById(`nav-${t}`);
                if (el) el.classList.toggle('hidden', t !== tab);
                if (navEl) navEl.className = t === tab ? 
                    'flex flex-col items-center gap-1 text-indigo-500' : 
                    'flex flex-col items-center gap-1 text-gray-400 hover:text-white';
            });
        };

        onAuthStateChanged(auth, (user) => {
            if (user) {
                currentUser = user;
                authView.classList.add('hidden');
                appView.classList.remove('hidden');
                bottomNav.classList.remove('hidden');
                userHeaderActions.classList.remove('hidden');
                document.getElementById('profile-name').textContent = user.displayName || user.email;
                document.getElementById('profile-avatar').textContent = (user.displayName || user.email).charAt(0).toUpperCase();
                loadPosts();
            } else {
                currentUser = null;
                authView.classList.remove('hidden');
                appView.classList.add('hidden');
                bottomNav.classList.add('hidden');
                userHeaderActions.classList.add('hidden');
            }
        });

        document.getElementById('btn-google').addEventListener('click', () => signInWithPopup(auth, googleProvider).catch(e => showError(e.message)));
        document.getElementById('auth-form').addEventListener('submit', (e) => {
            e.preventDefault();
            signInWithEmailAndPassword(auth, document.getElementById('email').value, document.getElementById('password').value).catch(e => showError(e.message));
        });
        document.getElementById('btn-signup').addEventListener('click', () => {
            createUserWithEmailAndPassword(auth, document.getElementById('email').value, document.getElementById('password').value).catch(e => showError(e.message));
        });
        document.getElementById('btn-logout').addEventListener('click', () => signOut(auth));

        // Live Stream Modal
        document.getElementById('btn-go-live').addEventListener('click', () => liveModal.classList.remove('hidden'));
        document.getElementById('btn-close-live').addEventListener('click', () => liveModal.classList.add('hidden'));

        // Upload Modal
        const toggleModal = (show) => uploadModal.classList.toggle('hidden', !show);
        document.getElementById('btn-create-post').addEventListener('click', () => toggleModal(true));
        document.getElementById('nav-btn-create').addEventListener('click', () => toggleModal(true));
        document.getElementById('close-modal').addEventListener('click', () => toggleModal(false));

        // Direct Messaging
        document.getElementById('btn-open-chat').addEventListener('click', () => document.getElementById('view-chat').classList.remove('hidden'));
        document.getElementById('btn-close-chat').addEventListener('click', () => document.getElementById('view-chat').classList.add('hidden'));

        // Virtual Gift Helper
        window.sendVirtualGift = (giftName, coins) => {
            const walletEl = document.getElementById('wallet-coins');
            const newCoins = parseInt(walletEl.textContent) + coins;
            walletEl.textContent = newCoins;
            document.getElementById('wallet-pkr').textContent = `${(newCoins * 0.5).toFixed(1)} PKR`;
            alert(`Sent ${giftName}! Added ${coins} coins to Creator Balance.`);
        };

        // Call Trigger Helper
        window.triggerCall = (type) => {
            alert(`Initiating High-Definition PrimeX ${type} Call...`);
        };

        // Submit Post with Music Selection
        document.getElementById('btn-submit-post').addEventListener('click', async () => {
            const caption = document.getElementById('post-caption').value.trim();
            const musicTrack = document.getElementById('post-music-select').value;
            const fileInput = document.getElementById('post-file-input');
            const file = fileInput.files[0];

            if (!file) return alert("Please select a file to upload!");

            uploadStatus.classList.remove('hidden');

            try {
                const sRef = storageRef(storage, `uploads/${Date.now()}_${file.name}`);
                const uploadResult = await uploadBytes(sRef, file);
                const mediaUrl = await getDownloadURL(uploadResult.ref);

                const newPostRef = push(ref(db, 'posts'));
                await set(newPostRef, {
                    id: newPostRef.key,
                    uid: currentUser.uid,
                    author: currentUser.displayName || currentUser.email.split('@')[0],
                    caption: caption,
                    musicTrack: musicTrack,
                    mediaUrl: mediaUrl,
                    mediaType: file.type.startsWith('video') ? 'video' : 'image',
                    likesCount: 0,
                    tipsCount: 0,
                    timestamp: Date.now()
                });

                document.getElementById('post-caption').value = '';
                fileInput.value = '';
                uploadStatus.classList.add('hidden');
                toggleModal(false);
            } catch (err) {
                uploadStatus.classList.add('hidden');
                alert("Upload failed: " + err.message);
            }
        });

        function loadPosts() {
            onValue(ref(db, 'posts'), (snapshot) => {
                reelsFeed.innerHTML = '';
                const exploreGrid = document.getElementById('explore-grid');
                exploreGrid.innerHTML = '';
                const data = snapshot.val();
                if (!data) return;

                const postsArray = Object.values(data).reverse();
                postsArray.forEach((post) => {
                    exploreGrid.innerHTML += `
                        <div class="h-36 bg-gray-900 rounded-xl overflow-hidden relative border border-gray-800">
                            ${post.mediaType === 'video' ? 
                                `<video src="${post.mediaUrl}" class="w-full h-full object-cover"></video>` : 
                                `<img src="${post.mediaUrl}" class="w-full h-full object-cover">`
                            }
                            <div class="absolute bottom-1 left-1 bg-black/60 px-2 py-0.5 rounded text-[10px] font-bold">
                                <i class="fa-solid fa-heart text-red-500"></i> ${post.likesCount || 0}
                            </div>
                        </div>
                    `;

                    const postCard = document.createElement('div');
                    postCard.className = 'reel-item h-full w-full relative flex flex-col justify-between bg-gray-900 border-b border-gray-800';
                    
                    postCard.innerHTML = `
                        <div class="absolute inset-0 z-0 flex items-center justify-center bg-black">
                            ${post.mediaType === 'video' ? 
                                `<video src="${post.mediaUrl}" class="w-full h-full object-cover" autoplay loop muted playsinline></video>` : 
                                `<img src="${post.mediaUrl}" class="w-full h-full object-cover">`
                            }
                        </div>
                        <div class="absolute inset-0 bg-gradient-to-b from-black/40 via-transparent to-black/90 z-10 pointer-events-none"></div>

                        <div class="relative z-20 p-4 flex items-center gap-3">
                            <div class="w-9 h-9 bg-indigo-600 rounded-full flex items-center justify-center font-bold text-xs uppercase shadow">
                                ${post.author.charAt(0)}
                            </div>
                            <div>
                                <h4 class="text-sm font-bold flex items-center gap-1">${post.author} <i class="fa-solid fa-circle-check text-indigo-400 text-xs"></i></h4>
                                <span class="text-[10px] text-indigo-400 font-semibold">PrimeX Creator</span>
                            </div>
                        </div>

                        <div class="absolute right-4 bottom-20 z-20 flex flex-col gap-5 items-center">
                            <button onclick="likePost('${post.id}', ${post.likesCount || 0})" class="flex flex-col items-center gap-1 text-white">
                                <div class="w-11 h-11 bg-gray-900/60 backdrop-blur rounded-full flex items-center justify-center text-rose-500 text-lg shadow">
                                    <i class="fa-solid fa-heart"></i>
                                </div>
                                <span class="text-xs font-semibold">${post.likesCount || 0}</span>
                            </button>
                            <button onclick="tipCreator('${post.id}', ${post.tipsCount || 0})" class="flex flex-col items-center gap-1 text-white">
                                <div class="w-11 h-11 bg-amber-500/80 backdrop-blur rounded-full flex items-center justify-center text-white text-lg shadow">
                                    <i class="fa-solid fa-coins"></i>
                                </div>
                                <span class="text-xs font-semibold text-amber-400">${post.tipsCount || 0}</span>
                            </button>
                        </div>

                        <div class="relative z-20 p-4 mb-2">
                            <p class="text-sm font-medium mb-1">${post.caption || ''}</p>
                            <span class="text-[11px] text-indigo-400 font-semibold"><i class="fa-solid fa-music text-xs mr-1"></i> ${post.musicTrack || 'PrimeX Original Sound'}</span>
                        </div>
                    `;
                    reelsFeed.appendChild(postCard);
                });
            });
        }

        window.likePost = (postId, currentLikes) => {
            update(ref(db, `posts/${postId}`), { likesCount: currentLikes + 1 });
        };

        window.tipCreator = (postId, currentTips) => {
            update(ref(db, `posts/${postId}`), { tipsCount: currentTips + 1 });
            const walletEl = document.getElementById('wallet-coins');
            const currentCoins = parseInt(walletEl.textContent) + 10;
            walletEl.textContent = currentCoins;
            document.getElementById('wallet-pkr').textContent = `${(currentCoins * 0.5).toFixed(1)} PKR`;
        };
    </script>
</body>
</html>
