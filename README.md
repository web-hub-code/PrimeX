<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PrimeX - Next-Gen Social Platform</title>
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

        <!-- Header -->
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
                <h2 class="text-2xl font-black mb-1">Welcome to PrimeX</h2>
                <p class="text-gray-400 text-xs mb-6">High-Level Media & Creator Platform</p>

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

        <!-- App Container -->
        <main id="app-view" class="flex-1 overflow-y-auto no-scrollbar hidden relative">
            
            <!-- Home Feed View (TikTok Reel Snap) -->
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

            <!-- Explore View (Instagram Grid) -->
            <div id="view-explore" class="h-full w-full p-4 hidden overflow-y-auto no-scrollbar">
                <div class="relative mb-4">
                    <i class="fa-solid fa-magnifying-glass absolute left-3 top-3 text-gray-400"></i>
                    <input type="text" placeholder="Search creators, viral reels..." class="w-full bg-gray-900 border border-gray-800 rounded-xl pl-9 pr-4 py-2 text-sm focus:outline-none">
                </div>
                <h3 class="text-sm font-bold text-indigo-400 mb-3"><i class="fa-solid fa-fire mr-1"></i> Trending Media</h3>
                <div id="explore-grid" class="grid grid-cols-2 gap-2"></div>
            </div>

            <!-- Wallet View -->
            <div id="view-wallet" class="h-full w-full p-6 hidden overflow-y-auto no-scrollbar">
                <div class="bg-gradient-to-r from-indigo-900 to-purple-900 border border-indigo-500/30 rounded-2xl p-5 mb-6 text-center shadow-lg">
                    <span class="text-xs uppercase font-bold text-indigo-300">Creator Coins Wallet</span>
                    <h2 class="text-4xl font-extrabold my-2 text-amber-400 flex items-center justify-center gap-2">
                        <i class="fa-solid fa-coins"></i> <span id="wallet-coins">0</span>
                    </h2>
                    <p class="text-xs text-gray-300">Estimated Value: <span id="wallet-pkr" class="text-emerald-400 font-bold">0 PKR</span></p>
                </div>
                
                <h3 class="text-sm font-bold mb-3">Instant Withdrawal Gateway</h3>
                <div class="space-y-3">
                    <div class="bg-gray-900 border border-gray-800 p-3.5 rounded-xl space-y-2">
                        <div class="flex justify-between items-center">
                            <span class="text-xs font-semibold">EasyPaisa / JazzCash</span>
                            <span class="text-[10px] text-emerald-400 font-bold">1 Coin = 0.5 PKR</span>
                        </div>
                        <input type="text" id="withdraw-account" placeholder="Enter Account / Mobile Number" class="w-full bg-gray-950 border border-gray-800 rounded-lg p-2 text-xs text-white focus:outline-none focus:border-indigo-500">
                        <button onclick="requestWithdrawal('EasyPaisa/JazzCash')" class="w-full bg-emerald-600 hover:bg-emerald-700 text-xs font-bold py-2 rounded-lg transition">Request Payout</button>
                    </div>
                </div>
            </div>

            <!-- Profile View -->
            <div id="view-profile" class="h-full w-full p-6 hidden overflow-y-auto no-scrollbar">
                <div class="text-center">
                    <div id="profile-avatar" class="w-20 h-20 bg-indigo-600 rounded-full mx-auto flex items-center justify-center text-2xl font-black mb-2 border-2 border-indigo-400 shadow-lg">U</div>
                    <h2 class="text-lg font-bold flex items-center justify-center gap-1">
                        <span id="profile-name">User</span>
                        <i class="fa-solid fa-circle-check text-indigo-400 text-sm"></i>
                    </h2>
                    <p class="text-xs text-indigo-400 font-semibold mb-4">PrimeX Verified Creator</p>
                </div>

                <div class="flex justify-around bg-gray-900 border border-gray-800 p-3 rounded-xl mb-6 text-center">
                    <div><span class="block font-bold text-sm">12</span><span class="text-[10px] text-gray-400">Posts</span></div>
                    <div><span class="block font-bold text-sm">2.4K</span><span class="text-[10px] text-gray-400">Followers</span></div>
                    <div><span id="profile-coins" class="block font-bold text-sm text-amber-400">0</span><span class="text-[10px] text-gray-400">Coins</span></div>
                </div>
            </div>

            <!-- Upload Modal -->
            <div id="upload-modal" class="fixed inset-0 bg-black/80 backdrop-blur-sm z-50 flex items-center justify-center p-4 hidden">
                <div class="bg-gray-900 border border-gray-800 w-full max-w-sm rounded-2xl p-5 relative">
                    <button id="close-modal" class="absolute top-4 right-4 text-gray-400 hover:text-white"><i class="fa-solid fa-xmark text-lg"></i></button>
                    <h3 class="text-lg font-bold mb-4">Upload Media</h3>
                    
                    <textarea id="post-caption" rows="2" placeholder="Write caption..." class="w-full bg-gray-950 border border-gray-800 rounded-xl p-3 text-sm focus:outline-none focus:border-indigo-500 mb-3 resize-none"></textarea>
                    
                    <div class="mb-4">
                        <label class="block text-xs font-bold text-gray-400 mb-1">Select Video / Image File:</label>
                        <input type="file" id="post-file-input" accept="image/*,video/*" class="w-full text-xs text-gray-400 bg-gray-950 border border-gray-800 rounded-xl p-2 cursor-pointer">
                    </div>

                    <div id="upload-status" class="text-xs text-indigo-400 font-bold mb-3 hidden text-center">
                        <i class="fa-solid fa-spinner fa-spin mr-1"></i> Uploading...
                    </div>

                    <button id="btn-submit-post" class="w-full bg-indigo-600 hover:bg-indigo-700 font-bold py-2.5 rounded-xl text-sm transition">Publish Post</button>
                </div>
            </div>

            <!-- TikTok / Instagram Style Interactive Live Modal -->
            <div id="live-stream-modal" class="fixed inset-0 bg-black z-50 hidden flex flex-col justify-between p-4">
                <div class="flex justify-between items-center z-20">
                    <div class="flex items-center gap-2 bg-black/50 backdrop-blur px-3 py-1.5 rounded-full border border-gray-800">
                        <span class="w-2 h-2 rounded-full bg-rose-500 animate-ping"></span>
                        <span class="text-xs font-bold text-rose-500">LIVE</span>
                        <span class="text-xs text-gray-300 font-semibold"><i class="fa-solid fa-eye text-xs ml-1"></i> 1.5K</span>
                    </div>
                    <button id="btn-close-live" class="w-8 h-8 bg-gray-900 rounded-full flex items-center justify-center text-white"><i class="fa-solid fa-xmark"></i></button>
                </div>

                <div class="absolute inset-0 z-0 overflow-hidden flex items-center justify-center">
                    <video id="liveBroadcasterFeed" class="w-full h-full object-cover" autoplay playsinline muted></video>
                    <canvas id="giftCanvas" class="absolute inset-0 pointer-events-none z-10"></canvas>
                </div>

                <div class="bg-gray-900/80 backdrop-blur border border-gray-800 rounded-2xl p-3 flex justify-around items-center z-20">
                    <button onclick="sendVirtualGift('💖 Heart', 5)" class="flex flex-col items-center text-rose-400 hover:scale-110 transition">
                        <span class="text-xl">💖</span>
                        <span class="text-[9px] font-bold">5 Coins</span>
                    </button>
                    <button onclick="sendVirtualGift('👑 Crown', 50)" class="flex flex-col items-center text-amber-400 hover:scale-110 transition">
                        <span class="text-xl">👑</span>
                        <span class="text-[9px] font-bold">50 Coins</span>
                    </button>
                    <button onclick="sendVirtualGift('🚀 Rocket', 100)" class="flex flex-col items-center text-indigo-400 hover:scale-110 transition">
                        <span class="text-xl">🚀</span>
                        <span class="text-[9px] font-bold">100 Coins</span>
                    </button>
                </div>
            </div>

            <!-- Real-Time Chat & WebRTC Video Call Window -->
            <div id="view-chat" class="fixed inset-0 bg-gray-950 z-40 hidden flex flex-col">
                <div class="h-14 border-b border-gray-800 px-4 flex items-center justify-between">
                    <div class="flex items-center gap-3">
                        <button id="btn-close-chat" class="text-gray-400 text-lg"><i class="fa-solid fa-arrow-left"></i></button>
                        <h3 class="font-bold text-sm">Messenger & Video Call</h3>
                    </div>
                    <div class="flex items-center gap-4 text-indigo-400">
                        <button onclick="startRealWebRTCCall('audio')" title="Audio Call"><i class="fa-solid fa-phone text-base"></i></button>
                        <button onclick="startRealWebRTCCall('video')" title="Video Call"><i class="fa-solid fa-video text-base"></i></button>
                    </div>
                </div>

                <div id="activeCallOverlay" class="hidden absolute inset-0 bg-black z-50 flex flex-col justify-between p-4">
                    <div class="relative w-full h-full bg-gray-900 rounded-2xl overflow-hidden flex items-center justify-center">
                        <video id="remoteCallVideo" class="w-full h-full object-cover" autoplay playsinline></video>
                        <video id="localCallVideo" class="absolute top-4 right-4 w-28 h-40 bg-black rounded-xl border border-indigo-500 object-cover" autoplay playsinline muted></video>
                        <button onclick="endWebRTCCall()" class="absolute bottom-6 bg-rose-600 hover:bg-rose-700 text-white p-4 rounded-full text-xl shadow-lg">
                            <i class="fa-solid fa-phone-slash"></i>
                        </button>
                    </div>
                </div>

                <div id="chat-messages" class="flex-1 p-4 overflow-y-auto space-y-3"></div>
                <div class="p-3 border-t border-gray-800 flex gap-2">
                    <input type="text" id="chat-input" placeholder="Message..." class="flex-1 bg-gray-900 border border-gray-800 rounded-xl px-4 py-2 text-sm focus:outline-none">
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

    <!-- Firebase SDK Modules -->
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
            appId: "1:465444221491:web:9824b4f1f9f592f76ce946"
        };

        const app = initializeApp(firebaseConfig);
        const auth = getAuth(app);
        const db = getDatabase(app);
        const storage = getStorage(app);
        const googleProvider = new GoogleAuthProvider();

        let currentUser = null;
        let peerConnection = null;
        let localStream = null;

        const authView = document.getElementById('auth-view');
        const appView = document.getElementById('app-view');
        const bottomNav = document.getElementById('bottom-nav');
        const userHeaderActions = document.getElementById('user-header-actions');
        const reelsFeed = document.getElementById('reels-feed');
        const uploadModal = document.getElementById('upload-modal');
        const liveModal = document.getElementById('live-stream-modal');
        const uploadStatus = document.getElementById('upload-status');

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
                document.getElementById('profile-name').textContent = user.displayName || user.email.split('@')[0];
                document.getElementById('profile-avatar').textContent = (user.displayName || user.email).charAt(0).toUpperCase();
                loadPosts();
                syncUserWallet();
            } else {
                currentUser = null;
                authView.classList.remove('hidden');
                appView.classList.add('hidden');
                bottomNav.classList.add('hidden');
                userHeaderActions.classList.add('hidden');
            }
        });

        document.getElementById('btn-google').addEventListener('click', () => signInWithPopup(auth, googleProvider));
        document.getElementById('auth-form').addEventListener('submit', (e) => {
            e.preventDefault();
            signInWithEmailAndPassword(auth, document.getElementById('email').value, document.getElementById('password').value);
        });
        document.getElementById('btn-signup').addEventListener('click', () => {
            createUserWithEmailAndPassword(auth, document.getElementById('email').value, document.getElementById('password').value);
        });
        document.getElementById('btn-logout').addEventListener('click', () => signOut(auth));

        // Live Broadcasting & Gifting
        document.getElementById('btn-go-live').addEventListener('click', async () => {
            liveModal.classList.remove('hidden');
            try {
                localStream = await navigator.mediaDevices.getUserMedia({ video: true, audio: true });
                document.getElementById('liveBroadcasterFeed').srcObject = localStream;
            } catch(e) { console.error(e); }
        });

        document.getElementById('btn-close-live').addEventListener('click', () => {
            liveModal.classList.add('hidden');
            if(localStream) localStream.getTracks().forEach(track => track.stop());
        });

        const canvas = document.getElementById('giftCanvas');
        const ctx = canvas.getContext('2d');
        let giftParticles = [];

        window.sendVirtualGift = (giftName, coins) => {
            updateUserCoins(coins);
            canvas.width = canvas.offsetWidth;
            canvas.height = canvas.offsetHeight;
            for(let i=0; i<20; i++) {
                giftParticles.push({
                    x: canvas.width / 2,
                    y: canvas.height / 2,
                    vx: (Math.random() - 0.5) * 6,
                    vy: (Math.random() - 0.5) * 6,
                    size: Math.random() * 24 + 12,
                    text: giftName.split(' ')[0]
                });
            }
            requestAnimationFrame(renderGiftParticles);
        };

        function renderGiftParticles() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            giftParticles.forEach((p, index) => {
                p.x += p.vx;
                p.y += p.vy;
                p.size *= 0.95;
                ctx.font = `${p.size}px serif`;
                ctx.fillText(p.text, p.x, p.y);
                if(p.size < 2) giftParticles.splice(index, 1);
            });
            if(giftParticles.length > 0) requestAnimationFrame(renderGiftParticles);
        }

        // WebRTC Real Call Signaling
        window.startRealWebRTCCall = async (type) => {
            document.getElementById('activeCallOverlay').classList.remove('hidden');
            peerConnection = new RTCPeerConnection({ iceServers: [{ urls: 'stun:stun.l.google.com:19302' }] });
            const mediaStream = await navigator.mediaDevices.getUserMedia({ video: type === 'video', audio: true });
            document.getElementById('localCallVideo').srcObject = mediaStream;
            mediaStream.getTracks().forEach(track => peerConnection.addTrack(track, mediaStream));
            peerConnection.ontrack = (e) => {
                document.getElementById('remoteCallVideo').srcObject = e.streams[0];
            };
        };

        window.endWebRTCCall = () => {
            if(peerConnection) peerConnection.close();
            document.getElementById('activeCallOverlay').classList.add('hidden');
        };

        // Wallet Sync & Payout Request
        function syncUserWallet() {
            onValue(ref(db, `users/${currentUser.uid}/coins`), (snapshot) => {
                const coins = snapshot.val() || 0;
                document.getElementById('wallet-coins').textContent = coins;
                document.getElementById('profile-coins').textContent = coins;
                document.getElementById('wallet-pkr').textContent = `${(coins * 0.5).toFixed(1)} PKR`;
            });
        }

        function updateUserCoins(amount) {
            if(!currentUser) return;
            const currentCoins = parseInt(document.getElementById('wallet-coins').textContent || '0');
            set(ref(db, `users/${currentUser.uid}/coins`), currentCoins + amount);
        }

        window.requestWithdrawal = (method) => {
            const acc = document.getElementById('withdraw-account').value.trim();
            const coins = parseInt(document.getElementById('wallet-coins').textContent || '0');
            if(!acc) return alert("Enter valid account details!");
            if(coins < 50) return alert("Minimum withdrawal threshold is 50 Coins!");

            push(ref(db, 'payoutRequests'), {
                uid: currentUser.uid,
                account: acc,
                method: method,
                coins: coins,
                pkrAmount: coins * 0.5,
                timestamp: Date.now()
            }).then(() => {
                alert(`Payout request of ${coins * 0.5} PKR submitted successfully!`);
                set(ref(db, `users/${currentUser.uid}/coins`), 0);
            });
        };

        // Post Upload Mechanics
        const toggleModal = (show) => uploadModal.classList.toggle('hidden', !show);
        document.getElementById('btn-create-post').addEventListener('click', () => toggleModal(true));
        document.getElementById('nav-btn-create').addEventListener('click', () => toggleModal(true));
        document.getElementById('close-modal').addEventListener('click', () => toggleModal(false));

        document.getElementById('btn-open-chat').addEventListener('click', () => document.getElementById('view-chat').classList.remove('hidden'));
        document.getElementById('btn-close-chat').addEventListener('click', () => document.getElementById('view-chat').classList.add('hidden'));

        document.getElementById('btn-submit-post').addEventListener('click', async () => {
            const caption = document.getElementById('post-caption').value.trim();
            const fileInput = document.getElementById('post-file-input');
            const file = fileInput.files[0];
            if (!file) return alert("Select media file to upload!");

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
                alert(err.message);
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
                            <span class="text-[11px] text-indigo-400 font-semibold"><i class="fa-solid fa-music text-xs mr-1"></i> Original Audio</span>
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
            updateUserCoins(10);
        };
    </script>
</body>
</html>
