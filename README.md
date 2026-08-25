<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PrimeX Supreme - App Experience</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700;800;900&display=swap" rel="stylesheet">
    <style>
        body { font-family: 'Poppins', sans-serif; }
        .no-scrollbar::-webkit-scrollbar { display: none; }
        .no-scrollbar { -ms-overflow-style: none; scrollbar-width: none; }
        .reel-snap { scroll-snap-type: y mandatory; }
        .reel-item { scroll-snap-align: start; }
        .app-shadow { box-shadow: 0 0 50px rgba(99, 102, 241, 0.15); }
        .glass-card { background: rgba(17, 24, 39, 0.7); backdrop-filter: blur(12px); border: 1px solid rgba(255, 255, 255, 0.08); }
        .glass-nav { background: rgba(10, 15, 30, 0.85); backdrop-filter: blur(20px); border-top: 1px solid rgba(255, 255, 255, 0.08); }
        .neon-glow { filter: drop-shadow(0 0 8px rgba(99, 102, 241, 0.6)); }
    </style>
</head>
<body class="bg-gray-950 text-slate-100 min-h-screen flex items-center justify-center p-0 md:p-4 overflow-hidden select-none">

    <!-- Mobile Frame Wrapper for Desktop/Tablet View -->
    <div class="w-full max-w-md h-screen md:h-[92vh] md:rounded-[40px] flex flex-col justify-between bg-black relative overflow-hidden border-0 md:border-[6px] border-gray-800 app-shadow">

        <!-- App Header Bar -->
        <header class="h-16 border-b border-gray-800/60 px-5 flex justify-between items-center bg-black/80 backdrop-blur-md z-30 sticky top-0">
            <div class="flex items-center gap-2">
                <div class="w-2.5 h-2.5 rounded-full bg-indigo-500 animate-pulse neon-glow"></div>
                <h1 class="text-xl font-extrabold tracking-tight bg-clip-text text-transparent bg-gradient-to-r from-indigo-400 via-purple-400 to-pink-500">PrimeX<span class="text-[10px] uppercase font-black text-amber-400 bg-amber-400/10 px-1.5 py-0.5 rounded-md ml-1 border border-amber-400/20">Pro</span></h1>
            </div>
            <div id="user-header-actions" class="flex items-center gap-2.5 hidden">
                <button id="btn-pk-battle" class="bg-gradient-to-r from-rose-500 to-indigo-600 text-[10px] px-3 py-1.5 rounded-full font-extrabold tracking-wider flex items-center gap-1.5 shadow-lg shadow-rose-600/30 hover:scale-105 active:scale-95 transition">
                    <i class="fa-solid fa-swords text-xs"></i> PK BATTLE
                </button>
                <button id="btn-go-live" class="bg-rose-600/90 hover:bg-rose-600 text-xs px-2.5 py-1.5 rounded-full font-bold transition flex items-center gap-1 shadow-md shadow-rose-600/20">
                    <i class="fa-solid fa-video text-[11px]"></i> LIVE
                </button>
                <button id="btn-open-chat" class="w-9 h-9 rounded-full bg-gray-900 flex items-center justify-center text-gray-300 hover:text-indigo-400 transition border border-gray-800">
                    <i class="fa-solid fa-paper-plane text-xs"></i>
                </button>
                <button id="btn-logout" class="w-9 h-9 rounded-full bg-gray-900 flex items-center justify-center text-gray-400 hover:text-rose-400 transition border border-gray-800">
                    <i class="fa-solid fa-right-from-bracket text-xs"></i>
                </button>
            </div>
        </header>

        <!-- Auth View -->
        <main id="auth-view" class="flex-1 p-6 flex flex-col justify-center items-center relative z-20">
            <div class="w-full glass-card rounded-3xl p-6 text-center border border-gray-800 shadow-2xl">
                <div class="w-16 h-16 bg-gradient-to-tr from-indigo-600 to-pink-500 rounded-2xl mx-auto flex items-center justify-center shadow-lg shadow-indigo-500/30 mb-4">
                    <i class="fa-solid fa-[#fa-shield-halved] fa-bolt text-2xl text-white"></i>
                </div>
                <h2 class="text-2xl font-black tracking-tight mb-1 text-white">Welcome to PrimeX</h2>
                <p class="text-xs text-gray-400 font-medium mb-6">Next-Gen Supreme Creator Engine</p>
                
                <button id="btn-google" class="w-full bg-white text-gray-900 font-semibold py-3 px-4 rounded-2xl flex items-center justify-center gap-3 hover:bg-gray-100 active:scale-98 transition mb-4 shadow-lg text-xs tracking-wide">
                    <i class="fa-brands fa-google text-red-500 text-base"></i>
                    <span>Continue with Google</span>
                </button>
                
                <div class="flex items-center my-4">
                    <hr class="flex-grow border-gray-800"><span class="px-3 text-[10px] font-bold text-gray-500 uppercase tracking-widest">OR</span><hr class="flex-grow border-gray-800">
                </div>
                
                <form id="auth-form" class="space-y-3">
                    <input type="email" id="email" placeholder="Email Address" required class="w-full bg-gray-950/80 border border-gray-800 rounded-2xl px-4 py-3 text-xs focus:outline-none focus:border-indigo-500 transition">
                    <input type="password" id="password" placeholder="Password" required class="w-full bg-gray-950/80 border border-gray-800 rounded-2xl px-4 py-3 text-xs focus:outline-none focus:border-indigo-500 transition">
                    <div class="flex gap-2.5 pt-2">
                        <button type="submit" id="btn-login" class="w-1/2 bg-gradient-to-r from-indigo-600 to-indigo-700 hover:from-indigo-500 hover:to-indigo-600 text-white font-bold py-3 rounded-2xl text-xs uppercase tracking-wider transition shadow-lg shadow-indigo-600/30">Login</button>
                        <button type="button" id="btn-signup" class="w-1/2 bg-gray-800/80 hover:bg-gray-800 font-bold py-3 rounded-2xl text-xs uppercase tracking-wider transition border border-gray-700">Sign Up</button>
                    </div>
                </form>

                <div class="mt-8 pt-4 border-t border-gray-800/60 text-[10px] text-gray-500 font-medium tracking-wide">
                    Powered by <span class="text-indigo-400 font-semibold">Prime Solutions LTD LLC</span>
                </div>
            </div>
        </main>

        <!-- Main App Container -->
        <main id="app-view" class="flex-1 overflow-y-auto no-scrollbar hidden relative z-10">
            
            <!-- Home Feed View -->
            <div id="view-home" class="h-full w-full flex flex-col">
                <div id="reels-feed" class="flex-1 overflow-y-scroll reel-snap no-scrollbar"></div>
            </div>

            <!-- Explore View -->
            <div id="view-explore" class="h-full w-full p-4 hidden overflow-y-auto no-scrollbar">
                <div class="relative mb-5">
                    <i class="fa-solid fa-magnifying-glass absolute left-3.5 top-3.5 text-gray-500 text-xs"></i>
                    <input type="text" placeholder="Search creators, viral reels..." class="w-full bg-gray-900/90 border border-gray-800 rounded-2xl pl-10 pr-4 py-2.5 text-xs text-slate-200 focus:outline-none focus:border-indigo-500 transition">
                </div>
                <h3 class="text-xs font-bold text-indigo-400 uppercase tracking-widest mb-3 flex items-center gap-1.5"><i class="fa-solid fa-fire text-amber-500"></i> Trending Reels</h3>
                <div id="explore-grid" class="grid grid-cols-2 gap-2.5"></div>
            </div>

            <!-- Wallet View -->
            <div id="view-wallet" class="h-full w-full p-5 hidden overflow-y-auto no-scrollbar">
                <div class="bg-gradient-to-br from-indigo-900/60 via-purple-900/40 to-black border border-indigo-500/30 rounded-3xl p-6 mb-6 text-center shadow-xl backdrop-blur relative overflow-hidden">
                    <div class="absolute -right-8 -bottom-8 w-28 h-28 bg-indigo-500/10 rounded-full blur-2xl"></div>
                    <span class="text-[10px] uppercase font-bold text-indigo-300 tracking-widest bg-indigo-500/20 px-3 py-1 rounded-full border border-indigo-500/30">Creator Coins Wallet</span>
                    <h2 class="text-4xl font-black my-3 text-amber-400 flex items-center justify-center gap-2">
                        <i class="fa-solid fa-coins text-3xl"></i> <span id="wallet-coins">0</span>
                    </h2>
                    <p class="text-xs text-gray-300 font-medium">Estimated Balance: <span id="wallet-pkr" class="text-emerald-400 font-bold">0 PKR</span></p>
                </div>
                
                <h3 class="text-xs font-bold text-gray-300 uppercase tracking-wider mb-3">Instant Payout Gateway</h3>
                <div class="glass-card p-4 rounded-2xl space-y-3">
                    <div class="flex justify-between items-center">
                        <span class="text-xs font-semibold text-slate-200">EasyPaisa / JazzCash</span>
                        <span class="text-[10px] text-emerald-400 font-bold bg-emerald-500/10 px-2 py-0.5 rounded border border-emerald-500/20">1 Coin = 0.5 PKR</span>
                    </div>
                    <input type="text" id="withdraw-account" placeholder="Enter Account / Mobile Number" class="w-full bg-gray-950 border border-gray-800 rounded-xl p-3 text-xs text-white focus:outline-none focus:border-indigo-500 transition">
                    <button onclick="requestWithdrawal('EasyPaisa/JazzCash')" class="w-full bg-emerald-600 hover:bg-emerald-500 text-xs font-bold py-3 rounded-xl transition shadow-lg shadow-emerald-600/20 tracking-wide uppercase">Request Payout</button>
                </div>

                <div class="mt-10 text-center text-[10px] text-gray-500 font-medium tracking-wide">
                    Powered by <span class="text-indigo-400 font-semibold">Prime Solutions LTD LLC</span>
                </div>
            </div>

            <!-- Profile View -->
            <div id="view-profile" class="h-full w-full p-6 hidden overflow-y-auto no-scrollbar">
                <div class="text-center">
                    <div id="profile-avatar" class="w-24 h-24 bg-gradient-to-tr from-indigo-600 to-pink-500 rounded-full mx-auto flex items-center justify-center text-3xl font-black mb-3 border-4 border-gray-900 shadow-xl shadow-indigo-500/20">U</div>
                    <h2 class="text-lg font-bold flex items-center justify-center gap-1.5 text-white">
                        <span id="profile-name">User</span>
                        <i class="fa-solid fa-circle-check text-indigo-400 text-sm"></i>
                    </h2>
                    <p class="text-[11px] text-indigo-400 font-semibold tracking-wide mb-5">Verified Creator</p>
                </div>

                <div class="flex justify-around glass-card p-4 rounded-2xl mb-6 text-center">
                    <div><span class="block font-black text-base text-white">12</span><span class="text-[10px] text-gray-400 font-medium">Posts</span></div>
                    <div><span class="block font-black text-base text-white">2.4K</span><span class="text-[10px] text-gray-400 font-medium">Followers</span></div>
                    <div><span id="profile-coins" class="block font-black text-base text-amber-400">0</span><span class="text-[10px] text-gray-400 font-medium">Coins</span></div>
                </div>

                <div class="text-center text-[10px] text-gray-500 font-medium tracking-wide pt-8">
                    Powered by <span class="text-indigo-400 font-semibold">Prime Solutions LTD LLC</span>
                </div>
            </div>

            <!-- TikTok Interactive Live Stream Modal -->
            <div id="live-stream-modal" class="fixed inset-0 bg-black z-50 hidden flex flex-col justify-between p-4">
                <div class="flex justify-between items-center z-20">
                    <div class="flex items-center gap-2 bg-black/60 backdrop-blur px-3 py-1.5 rounded-full border border-gray-800">
                        <span class="w-2 h-2 rounded-full bg-rose-500 animate-ping"></span>
                        <span class="text-xs font-bold text-rose-500">LIVE</span>
                    </div>
                    <button id="btn-close-live" class="w-9 h-9 bg-gray-900 rounded-full flex items-center justify-center text-white border border-gray-800"><i class="fa-solid fa-xmark"></i></button>
                </div>

                <div class="absolute inset-0 z-0 overflow-hidden flex items-center justify-center">
                    <video id="liveBroadcasterFeed" class="w-full h-full object-cover" autoplay playsinline muted></video>
                    <canvas id="giftCanvas" class="absolute inset-0 pointer-events-none z-10"></canvas>
                </div>

                <div class="glass-card rounded-2xl p-3 flex justify-around items-center z-20">
                    <button onclick="sendVirtualGift('💖 Heart', 5)" class="flex flex-col items-center text-rose-400 hover:scale-110 active:scale-95 transition">
                        <span class="text-2xl">💖</span>
                        <span class="text-[9px] font-bold">5 Coins</span>
                    </button>
                    <button onclick="sendVirtualGift('👑 Crown', 50)" class="flex flex-col items-center text-amber-400 hover:scale-110 active:scale-95 transition">
                        <span class="text-2xl">👑</span>
                        <span class="text-[9px] font-bold">50 Coins</span>
                    </button>
                    <button onclick="sendVirtualGift('🚀 Rocket', 100)" class="flex flex-col items-center text-indigo-400 hover:scale-110 active:scale-95 transition">
                        <span class="text-2xl">🚀</span>
                        <span class="text-[9px] font-bold">100 Coins</span>
                    </button>
                </div>
            </div>

            <!-- TikTok Style PK Battle Modal -->
            <div id="pk-battle-modal" class="fixed inset-0 bg-black z-50 hidden flex flex-col justify-between p-4">
                <div class="flex justify-between items-center z-20">
                    <div class="flex items-center gap-2 bg-rose-600/80 px-3 py-1 rounded-full text-[10px] font-black tracking-widest animate-pulse border border-rose-400/30">
                        <i class="fa-solid fa-swords"></i> LIVE PK BATTLE
                    </div>
                    <button id="btn-close-pk" class="w-9 h-9 bg-gray-900 rounded-full text-white flex items-center justify-center border border-gray-800"><i class="fa-solid fa-xmark"></i></button>
                </div>

                <div class="w-full bg-gray-800 rounded-full h-3.5 relative overflow-hidden my-3 flex border border-gray-700 shadow-inner">
                    <div id="blue-score-bar" class="bg-indigo-600 h-full w-1/2 transition-all duration-300"></div>
                    <div id="red-score-bar" class="bg-rose-600 h-full w-1/2 transition-all duration-300"></div>
                </div>

                <div class="grid grid-cols-2 gap-1.5 flex-1 my-2 relative rounded-3xl overflow-hidden border border-gray-800">
                    <div class="bg-gray-900/90 flex items-center justify-center relative">
                        <span class="absolute top-3 left-3 bg-indigo-600/90 text-[10px] px-2.5 py-1 rounded-full font-bold shadow">Creator A</span>
                        <i class="fa-solid fa-user text-5xl text-gray-700"></i>
                    </div>
                    <div class="bg-gray-900/90 flex items-center justify-center relative">
                        <span class="absolute top-3 right-3 bg-rose-600/90 text-[10px] px-2.5 py-1 rounded-full font-bold shadow">Creator B</span>
                        <i class="fa-solid fa-user text-5xl text-gray-700"></i>
                    </div>
                </div>

                <div class="glass-card rounded-2xl p-3 flex justify-between items-center z-20 gap-2">
                    <button onclick="votePK('blue')" class="flex-1 bg-indigo-600 hover:bg-indigo-500 text-xs py-2.5 rounded-xl font-bold transition shadow-lg shadow-indigo-600/30">Support Blue (+50)</button>
                    <button onclick="votePK('red')" class="flex-1 bg-rose-600 hover:bg-rose-500 text-xs py-2.5 rounded-xl font-bold transition shadow-lg shadow-rose-600/30">Support Red (+50)</button>
                </div>
            </div>

            <!-- WebRTC Audio/Video Call & Chat Modal -->
            <div id="view-chat" class="fixed inset-0 bg-gray-950 z-40 hidden flex flex-col">
                <div class="h-16 border-b border-gray-800/80 px-4 flex items-center justify-between bg-black/60 backdrop-blur">
                    <div class="flex items-center gap-3">
                        <button id="btn-close-chat" class="text-gray-400 hover:text-white text-lg"><i class="fa-solid fa-arrow-left"></i></button>
                        <div>
                            <h3 class="font-bold text-xs text-slate-100">Messenger & Calls</h3>
                            <span class="text-[9px] text-emerald-400 font-medium">Online</span>
                        </div>
                    </div>
                    <div class="flex items-center gap-3 text-indigo-400">
                        <button onclick="startRealWebRTCCall('audio')" class="w-8 h-8 rounded-full bg-gray-900 flex items-center justify-center border border-gray-800" title="Audio Call"><i class="fa-solid fa-phone text-xs"></i></button>
                        <button onclick="startRealWebRTCCall('video')" class="w-8 h-8 rounded-full bg-gray-900 flex items-center justify-center border border-gray-800" title="Video Call"><i class="fa-solid fa-video text-xs"></i></button>
                    </div>
                </div>

                <div id="activeCallOverlay" class="hidden absolute inset-0 bg-black z-50 flex flex-col justify-between p-4">
                    <div class="relative w-full h-full bg-gray-900 rounded-3xl overflow-hidden flex items-center justify-center border border-gray-800">
                        <video id="remoteCallVideo" class="w-full h-full object-cover" autoplay playsinline></video>
                        <video id="localCallVideo" class="absolute top-4 right-4 w-28 h-40 bg-black rounded-2xl border-2 border-indigo-500 object-cover shadow-2xl" autoplay playsinline muted></video>
                        <button onclick="endWebRTCCall()" class="absolute bottom-6 bg-rose-600 hover:bg-rose-500 text-white p-4 rounded-full text-xl shadow-xl shadow-rose-600/40">
                            <i class="fa-solid fa-phone-slash"></i>
                        </button>
                    </div>
                </div>

                <div id="chat-messages" class="flex-1 p-4 overflow-y-auto space-y-3"></div>
                <div class="p-3 border-t border-gray-800/80 flex gap-2 bg-black/60 backdrop-blur">
                    <input type="text" id="chat-input" placeholder="Message..." class="flex-1 bg-gray-900 border border-gray-800 rounded-2xl px-4 py-2.5 text-xs text-white focus:outline-none focus:border-indigo-500">
                    <button id="btn-send-msg" class="bg-indigo-600 hover:bg-indigo-500 px-4 py-2.5 rounded-2xl text-xs font-bold transition shadow-lg shadow-indigo-600/30"><i class="fa-solid fa-paper-plane"></i></button>
                </div>
            </div>

            <!-- Upload Modal with AI Auto Captions -->
            <div id="upload-modal" class="fixed inset-0 bg-black/80 backdrop-blur-md z-50 flex items-center justify-center p-4 hidden">
                <div class="glass-card w-full max-w-sm rounded-3xl p-6 relative shadow-2xl">
                    <button id="close-modal" class="absolute top-4 right-4 text-gray-400 hover:text-white"><i class="fa-solid fa-xmark text-lg"></i></button>
                    <h3 class="text-base font-bold text-white mb-4 flex items-center gap-2"><i class="fa-solid fa-cloud-arrow-up text-indigo-400"></i> Upload Media</h3>
                    
                    <textarea id="post-caption" rows="2" placeholder="Write caption..." class="w-full bg-gray-950/80 border border-gray-800 rounded-2xl p-3 text-xs focus:outline-none focus:border-indigo-500 mb-3 resize-none text-slate-200"></textarea>
                    
                    <div class="flex items-center justify-between bg-gray-950/80 p-3 rounded-2xl border border-gray-800 mb-3">
                        <span class="text-xs font-semibold text-gray-300 flex items-center gap-1.5"><i class="fa-solid fa-closed-captioning text-indigo-400"></i> Auto AI Subtitles</span>
                        <input type="checkbox" id="toggle-ai-subtitles" class="accent-indigo-600 w-4 h-4" checked>
                    </div>

                    <div class="mb-5">
                        <input type="file" id="post-file-input" accept="image/*,video/*" class="w-full text-xs text-gray-400 bg-gray-950/80 border border-gray-800 rounded-2xl p-2.5 cursor-pointer file:mr-3 file:py-1 file:px-3 file:rounded-xl file:border-0 file:text-xs file:font-semibold file:bg-indigo-600 file:text-white">
                    </div>

                    <div id="upload-status" class="text-xs text-indigo-400 font-bold mb-3 hidden text-center">
                        <i class="fa-solid fa-circle-notch fa-spin mr-1"></i> Uploading media...
                    </div>

                    <button id="btn-submit-post" class="w-full bg-gradient-to-r from-indigo-600 to-pink-600 hover:from-indigo-500 hover:to-pink-500 text-white font-bold py-3 rounded-2xl text-xs uppercase tracking-wider transition shadow-lg shadow-indigo-600/30">Publish Post</button>
                </div>
            </div>

        </main>

        <!-- Bottom Navigation Dock Bar -->
        <nav id="bottom-nav" class="h-16 glass-nav px-6 flex justify-between items-center z-30 hidden border-t border-gray-800/80">
            <button onclick="switchTab('home')" id="nav-home" class="flex flex-col items-center gap-1 text-indigo-400"><i class="fa-solid fa-house text-lg"></i><span class="text-[9px] font-semibold">Home</span></button>
            <button onclick="switchTab('explore')" id="nav-explore" class="flex flex-col items-center gap-1 text-gray-500 hover:text-gray-300"><i class="fa-solid fa-compass text-lg"></i><span class="text-[9px] font-semibold">Explore</span></button>
            <button id="nav-btn-create" class="flex flex-col items-center justify-center w-11 h-11 bg-gradient-to-tr from-indigo-600 to-pink-500 rounded-full text-white shadow-lg shadow-indigo-600/40 -mt-5 border-4 border-black active:scale-90 transition"><i class="fa-solid fa-plus text-base"></i></button>
            <button onclick="switchTab('wallet')" id="nav-wallet" class="flex flex-col items-center gap-1 text-gray-500 hover:text-gray-300"><i class="fa-solid fa-wallet text-lg"></i><span class="text-[9px] font-semibold">Wallet</span></button>
            <button onclick="switchTab('profile')" id="nav-profile" class="flex flex-col items-center gap-1 text-gray-500 hover:text-gray-300"><i class="fa-solid fa-user text-lg"></i><span class="text-[9px] font-semibold">Profile</span></button>
        </nav>

        <!-- Persistent App Footer -->
        <footer class="bg-black/95 border-t border-gray-900 py-1.5 text-center text-[9px] text-gray-500 font-semibold z-20">
            Powered by <span class="text-indigo-400">Prime Solutions LTD LLC</span>
        </footer>

    </div>

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

        window.switchTab = (tab) => {
            ['home', 'explore', 'wallet', 'profile'].forEach(t => {
                const el = document.getElementById(`view-${t}`);
                const navEl = document.getElementById(`nav-${t}`);
                if (el) el.classList.toggle('hidden', t !== tab);
                if (navEl) navEl.className = t === tab ? 'flex flex-col items-center gap-1 text-indigo-400 font-semibold' : 'flex flex-col items-center gap-1 text-gray-500 hover:text-gray-300';
            });
        };

        onAuthStateChanged(auth, (user) => {
            if (user) {
                currentUser = user;
                document.getElementById('auth-view').classList.add('hidden');
                document.getElementById('app-view').classList.remove('hidden');
                document.getElementById('bottom-nav').classList.remove('hidden');
                document.getElementById('user-header-actions').classList.remove('hidden');
                document.getElementById('profile-name').textContent = user.displayName || user.email.split('@')[0];
                document.getElementById('profile-avatar').textContent = (user.displayName || user.email).charAt(0).toUpperCase();
                loadPosts();
                syncUserWallet();
            } else {
                currentUser = null;
                document.getElementById('auth-view').classList.remove('hidden');
                document.getElementById('app-view').classList.add('hidden');
                document.getElementById('bottom-nav').classList.add('hidden');
                document.getElementById('user-header-actions').classList.add('hidden');
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

        // Interactive Live Stream & Gifting Canvas
        const liveModal = document.getElementById('live-stream-modal');
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
                    x: canvas.width / 2, y: canvas.height / 2,
                    vx: (Math.random() - 0.5) * 6, vy: (Math.random() - 0.5) * 6,
                    size: Math.random() * 24 + 12, text: giftName.split(' ')[0]
                });
            }
            requestAnimationFrame(renderGiftParticles);
        };

        function renderGiftParticles() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            giftParticles.forEach((p, index) => {
                p.x += p.vx; p.y += p.vy; p.size *= 0.95;
                ctx.font = `${p.size}px serif`;
                ctx.fillText(p.text, p.x, p.y);
                if(p.size < 2) giftParticles.splice(index, 1);
            });
            if(giftParticles.length > 0) requestAnimationFrame(renderGiftParticles);
        }

        // PK Battle Score Controls
        let blueScore = 500, redScore = 500;
        document.getElementById('btn-pk-battle').addEventListener('click', () => document.getElementById('pk-battle-modal').classList.remove('hidden'));
        document.getElementById('btn-close-pk').addEventListener('click', () => document.getElementById('pk-battle-modal').classList.add('hidden'));

        window.votePK = (team) => {
            if (team === 'blue') blueScore += 50;
            if (team === 'red') redScore += 50;
            const total = blueScore + redScore;
            document.getElementById('blue-score-bar').style.width = `${(blueScore / total) * 100}%`;
            document.getElementById('red-score-bar').style.width = `${(redScore / total) * 100}%`;
        };

        // WebRTC Real Audio/Video Calling
        window.startRealWebRTCCall = async (type) => {
            document.getElementById('activeCallOverlay').classList.remove('hidden');
            peerConnection = new RTCPeerConnection({ iceServers: [{ urls: 'stun:stun.l.google.com:19302' }] });
            const mediaStream = await navigator.mediaDevices.getUserMedia({ video: type === 'video', audio: true });
            document.getElementById('localCallVideo').srcObject = mediaStream;
            mediaStream.getTracks().forEach(track => peerConnection.addTrack(track, mediaStream));
            peerConnection.ontrack = (e) => document.getElementById('remoteCallVideo').srcObject = e.streams[0];
        };

        window.endWebRTCCall = () => {
            if(peerConnection) peerConnection.close();
            document.getElementById('activeCallOverlay').classList.add('hidden');
        };

        // Wallet Sync & Local PKR Payouts
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
                uid: currentUser.uid, account: acc, method: method, coins: coins, pkrAmount: coins * 0.5, timestamp: Date.now()
            }).then(() => {
                alert(`Payout request of ${coins * 0.5} PKR submitted!`);
                set(ref(db, `users/${currentUser.uid}/coins`), 0);
            });
        };

        // Post Upload & Feed Mechanics
        const uploadModal = document.getElementById('upload-modal');
        document.getElementById('btn-close-chat').addEventListener('click', () => document.getElementById('view-chat').classList.add('hidden'));
        document.getElementById('btn-open-chat').addEventListener('click', () => document.getElementById('view-chat').classList.remove('hidden'));
        document.getElementById('nav-btn-create').addEventListener('click', () => uploadModal.classList.remove('hidden'));
        document.getElementById('close-modal').addEventListener('click', () => uploadModal.classList.add('hidden'));

        document.getElementById('btn-submit-post').addEventListener('click', async () => {
            const caption = document.getElementById('post-caption').value.trim();
            const fileInput = document.getElementById('post-file-input');
            const file = fileInput.files[0];
            if (!file) return alert("Select media file to upload!");

            document.getElementById('upload-status').classList.remove('hidden');

            try {
                const sRef = storageRef(storage, `uploads/${Date.now()}_${file.name}`);
                const uploadResult = await uploadBytes(sRef, file);
                const mediaUrl = await getDownloadURL(uploadResult.ref);

                const newPostRef = push(ref(db, 'posts'));
                await set(newPostRef, {
                    id: newPostRef.key, uid: currentUser.uid,
                    author: currentUser.displayName || currentUser.email.split('@')[0],
                    caption: caption, mediaUrl: mediaUrl,
                    mediaType: file.type.startsWith('video') ? 'video' : 'image',
                    likesCount: 0, tipsCount: 0, timestamp: Date.now()
                });

                document.getElementById('post-caption').value = '';
                fileInput.value = '';
                document.getElementById('upload-status').classList.add('hidden');
                uploadModal.classList.add('hidden');
            } catch (err) {
                document.getElementById('upload-status').classList.add('hidden');
                alert(err.message);
            }
        });
Upload Modal with AI Auto Captions -->
            <div id="upload-modal" class="fixed inset-0 bg-black/80 backdrop-blur-md z-50 flex items-center justify-center p-4 hidden">
                <div class="glass-card w-full max-w-sm rounded-3xl p-6 relative shadow-2xl">
                    <button id="close-modal" class="absolute top-4 right-4 text-gray-400 hover:text-white"><i class="fa-solid fa-xmark text-lg"></i></button>
                    <h3 class="text-base font-bold text-white mb-4 flex items-center gap-2"><i class="fa-solid fa-cloud-arrow-up text-indigo-400"></i> Upload Media</h3>
                    
                    <textarea id="post-caption" rows="2" placeholder="Write caption..." class="w-full bg-gray-950/80 border border-gray-800 rounded-2xl p-3 text-xs focus:outline-none focus:border-indigo-500 mb-3 resize-none text-slate-200"></textarea>
                    
                    <div class="flex items-center justify-between bg-gray-950/80 p-3 rounded-2xl border border-gray-800 mb-3">
                        <span class="text-xs font-semibold text-gray-300 flex items-center gap-1.5"><i class="fa-solid fa-closed-captioning text-indigo-400"></i> Auto AI Subtitles</span>
                        <input type="checkbox" id="toggle-ai-subtitles" class="accent-indigo-600 w-4 h-4" checked>
                    </div>

                    <div class="mb-5">
                        <input type="file" id="post-file-input" accept="image/*,video/*" class="w-full text-xs text-gray-400 bg-gray-950/80 border border-gray-800 rounded-2xl p-2.5 cursor-pointer file:mr-3 file:py-1 file:px-3 file:rounded-xl file:border-0 file:text-xs file:font-semibold file:bg-indigo-600 file:text-white">
                    </div>

                    <div id="upload-status" class="text-xs text-indigo-400 font-bold mb-3 hidden text-center">
                        <i class="fa-solid fa-circle-notch fa-spin mr-1"></i> Uploading media...
                    </div>

                    <button id="btn-submit-post" class="w-full bg-gradient-to-r from-indigo-600 to-pink-600 hover:from-indigo-500 hover:to-pink-500 text-white font-bold py-3 rounded-2xl text-xs uppercase tracking-wider transition shadow-lg shadow-indigo-600/30">Publish Post</button>
                </div>
            </div>

        </main>

        <!-- Bottom Navigation Dock Bar -->
        <nav id="bottom-nav" class="h-16 glass-nav px-6 flex justify-between items-center z-30 hidden border-t border-gray-800/80">
            <button onclick="switchTab('home')" id="nav-home" class="flex flex-col items-center gap-1 text-indigo-400"><i class="fa-solid fa-house text-lg"></i><span class="text-[9px] font-semibold">Home</span></button>
            <button onclick="switchTab('explore')" id="nav-explore" class="flex flex-col items-center gap-1 text-gray-500 hover:text-gray-300"><i class="fa-solid fa-compass text-lg"></i><span class="text-[9px] font-semibold">Explore</span></button>
            <button id="nav-btn-create" class="flex flex-col items-center justify-center w-11 h-11 bg-gradient-to-tr from-indigo-600 to-pink-500 rounded-full text-white shadow-lg shadow-indigo-600/40 -mt-5 border-4 border-black active:scale-90 transition"><i class="fa-solid fa-plus text-base"></i></button>
            <button onclick="switchTab('wallet')" id="nav-wallet" class="flex flex-col items-center gap-1 text-gray-500 hover:text-gray-300"><i class="fa-solid fa-wallet text-lg"></i><span class="text-[9px] font-semibold">Wallet</span></button>
            <button onclick="switchTab('profile')" id="nav-profile" class="flex flex-col items-center gap-1 text-gray-500 hover:text-gray-300"><i class="fa-solid fa-user text-lg"></i><span class="text-[9px] font-semibold">Profile</span></button>
        </nav>

        <!-- Persistent App Footer -->
        <footer class="bg-black/95 border-t border-gray-900 py-1.5 text-center text-[9px] text-gray-500 font-semibold z-20">
            Powered by <span class="text-indigo-400">Prime Solutions LTD LLC</span>
        </footer>

    </div>

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

        window.switchTab = (tab) => {
            ['home', 'explore', 'wallet', 'profile'].forEach(t => {
                const el = document.getElementById(`view-${t}`);
                const navEl = document.getElementById(`nav-${t}`);
                if (el) el.classList.toggle('hidden', t !== tab);
                if (navEl) navEl.className = t === tab ? 'flex flex-col items-center gap-1 text-indigo-400 font-semibold' : 'flex flex-col items-center gap-1 text-gray-500 hover:text-gray-300';
            });
        };

        onAuthStateChanged(auth, (user) => {
            if (user) {
                currentUser = user;
                document.getElementById('auth-view').classList.add('hidden');
                document.getElementById('app-view').classList.remove('hidden');
                document.getElementById('bottom-nav').classList.remove('hidden');
                document.getElementById('user-header-actions').classList.remove('hidden');
                document.getElementById('profile-name').textContent = user.displayName || user.email.split('@')[0];
                document.getElementById('profile-avatar').textContent = (user.displayName || user.email).charAt(0).toUpperCase();
                loadPosts();
                syncUserWallet();
            } else {
                currentUser = null;
                document.getElementById('auth-view').classList.remove('hidden');
                document.getElementById('app-view').classList.add('hidden');
                document.getElementById('bottom-nav').classList.add('hidden');
                document.getElementById('user-header-actions').classList.add('hidden');
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

        // Interactive Live Stream & Gifting Canvas
        const liveModal = document.getElementById('live-stream-modal');
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
                    x: canvas.width / 2, y: canvas.height / 2,
                    vx: (Math.random() - 0.5) * 6, vy: (Math.random() - 0.5) * 6,
                    size: Math.random() * 24 + 12, text: giftName.split(' ')[0]
                });
            }
            requestAnimationFrame(renderGiftParticles);
        };

        function renderGiftParticles() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            giftParticles.forEach((p, index) => {
                p.x += p.vx; p.y += p.vy; p.size *= 0.95;
                ctx.font = `${p.size}px serif`;
                ctx.fillText(p.text, p.x, p.y);
                if(p.size < 2) giftParticles.splice(index, 1);
            });
            if(giftParticles.length > 0) requestAnimationFrame(renderGiftParticles);
        }

        // PK Battle Score Controls
        let blueScore = 500, redScore = 500;
        document.getElementById('btn-pk-battle').addEventListener('click', () => document.getElementById('pk-battle-modal').classList.remove('hidden'));
        document.getElementById('btn-close-pk').addEventListener('click', () => document.getElementById('pk-battle-modal').classList.add('hidden'));

        window.votePK = (team) => {
            if (team === 'blue') blueScore += 50;
            if (team === 'red') redScore += 50;
            const total = blueScore + redScore;
            document.getElementById('blue-score-bar').style.width = `${(blueScore / total) * 100}%`;
            document.getElementById('red-score-bar').style.width = `${(redScore / total) * 100}%`;
        };

        // WebRTC Real Audio/Video Calling
        window.startRealWebRTCCall = async (type) => {
            document.getElementById('activeCallOverlay').classList.remove('hidden');
            peerConnection = new RTCPeerConnection({ iceServers: [{ urls: 'stun:stun.l.google.com:19302' }] });
            const mediaStream = await navigator.mediaDevices.getUserMedia({ video: type === 'video', audio: true });
            document.getElementById('localCallVideo').srcObject = mediaStream;
            mediaStream.getTracks().forEach(track => peerConnection.addTrack(track, mediaStream));
            peerConnection.ontrack = (e) => document.getElementById('remoteCallVideo').srcObject = e.streams[0];
        };

        window.endWebRTCCall = () => {
            if(peerConnection) peerConnection.close();
            document.getElementById('activeCallOverlay').classList.add('hidden');
        };

        // Wallet Sync & Local PKR Payouts
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
                uid: currentUser.uid, account: acc, method: method, coins: coins, pkrAmount: coins * 0.5, timestamp: Date.now()
            }).then(() => {
                alert(`Payout request of ${coins * 0.5} PKR submitted!`);
                set(ref(db, `users/${currentUser.uid}/coins`), 0);
            });
        };

        // Post Upload & Feed Mechanics
        const uploadModal = document.getElementById('upload-modal');
        document.getElementById('btn-close-chat').addEventListener('click', () => document.getElementById('view-chat').classList.add('hidden'));
        document.getElementById('btn-open-chat').addEventListener('click', () => document.getElementById('view-chat').classList.remove('hidden'));
        document.getElementById('nav-btn-create').addEventListener('click', () => uploadModal.classList.remove('hidden'));
        document.getElementById('close-modal').addEventListener('click', () => uploadModal.classList.add('hidden'));

        document.getElementById('btn-submit-post').addEventListener('click', async () => {
            const caption = document.getElementById('post-caption').value.trim();
            const fileInput = document.getElementById('post-file-input');
            const file = fileInput.files[0];
            if (!file) return alert("Select media file to upload!");

            document.getElementById('upload-status').classList.remove('hidden');

            try {
                const sRef = storageRef(storage, `uploads/${Date.now()}_${file.name}`);
                const uploadResult = await uploadBytes(sRef, file);
                const mediaUrl = await getDownloadURL(uploadResult.ref);

                const newPostRef = push(ref(db, 'posts'));
                await set(newPostRef, {
                    id: newPostRef.key, uid: currentUser.uid,
                    author: currentUser.displayName || currentUser.email.split('@')[0],
                    caption: caption, mediaUrl: mediaUrl,
                    mediaType: file.type.startsWith('video') ? 'video' : 'image',
                    likesCount: 0, tipsCount: 0, timestamp: Date.now()
                });

                document.getElementById('post-caption').value = '';
                fileInput.value = '';
                document.getElementById('upload-status').classList.add('hidden');
                uploadModal.classList.add('hidden');
            } catch (err) {
                document.getElementById('upload-status').classList.add('hidden');
                alert(err.message);
            }
        });

        function loadPosts() {
            onValue(ref(db, 'posts'), (snapshot) => {
                const reelsFeed = document.getElementById('reels-feed');
                const exploreGrid = document.getElementById('explore-grid');
                reelsFeed.innerHTML = ''; exploreGrid.innerHTML = '';
                const data = snapshot.val();
                if (!data) return;

                Object.values(data).reverse().forEach((post) => {
                    exploreGrid.innerHTML += `
                        <div class="h-40 bg-gray-900 rounded-2xl overflow-hidden relative border border-gray-800/80 shadow">
                            ${post.mediaType === 'video' ? `<video src="${post.mediaUrl}" class="w-full h-full object-cover"></video>` : `<img src="${post.mediaUrl}" class="w-full h-full object-cover">`}
                            <div class="absolute bottom-2 left-2 bg-black/70 backdrop-blur px-2 py-0.5 rounded-lg text-[10px] font-bold text-white flex items-center gap-1">
                                <i class="fa-solid fa-heart text-rose-500"></i> ${post.likesCount || 0}
                            </div>
                        </div>`;

                    const postCard = document.createElement('div');
                    postCard.className = 'reel-item h-full w-full relative flex flex-col justify-between bg-black border-b border-gray-900 overflow-hidden';
                    postCard.innerHTML = `
                        <div class="absolute inset-0 z-0 flex items-center justify-center bg-black">
                            ${post.mediaType === 'video' ? `<video src="${post.mediaUrl}" class="w-full h-full object-cover" autoplay loop muted playsinline></video>` : `<img src="${post.mediaUrl}" class="w-full h-full object-cover">`}
                        </div>
                        <div class="absolute inset-0 bg-gradient-to-b from-black/60 via-transparent to-black/90 z-10 pointer-events-none"></div>
                        <div class="relative z-20 p-4 flex items-center gap-3">
                            <div class="w-10 h-10 bg-gradient-to-tr from-indigo-600 to-pink-500 rounded-full flex items-center justify-center font-black text-xs uppercase shadow-lg border-2 border-white/20">${post.author.charAt(0)}</div>
                            <div>
                                <h4 class="text-xs font-bold flex items-center gap-1.5 text-white">${post.author} <i class="fa-solid fa-circle-check text-indigo-400 text-xs"></i></h4>
                                <span class="text-[9px] text-indigo-400 font-semibold tracking-wide">Verified Creator</span>
                            </div>
                        </div>
                        <div class="absolute right-3.5 bottom-20 z-20 flex flex-col gap-4 items-center">
                            <button onclick="likePost('${post.id}', ${post.likesCount || 0})" class="flex flex-col items-center gap-1 text-white">
                                <div class="w-12 h-12 bg-gray-900/60 backdrop-blur-md rounded-full flex items-center justify-center text-rose-500 text-xl shadow-lg border border-white/10 active:scale-90 transition"><i class="fa-solid fa-heart"></i></div>
                                <span class="text-[11px] font-bold">${post.likesCount || 0}</span>
                            </button>
                            <button onclick="tipCreator('${post.id}', ${post.tipsCount || 0})" class="flex flex-col items-center gap-1 text-white">
                                <div class="w-12 h-12 bg-amber-500/90 backdrop-blur-md rounded-full flex items-center justify-center text-white text-xl shadow-lg border border-amber-300/30 active:scale-90 transition"><i class="fa-solid fa-coins"></i></div>
                                <span class="text-[11px] font-bold text-amber-400">${post.tipsCount || 0}</span>
                            </button>
                        </div>
                        <div class="relative z-20 p-4 mb-2">
                            <p class="text-xs font-medium text-slate-100 mb-1.5 leading-relaxed">${post.caption || ''}</p>
                            <span class="text-[10px] text-indigo-400 font-semibold flex items-center gap-1"><i class="fa-solid fa-music text-[10px]"></i> PrimeX Audio Original Track</span>
                        </div>`;
                    reelsFeed.appendChild(postCard);
                });
            });
        }

        window.likePost = (postId, currentLikes) => update(ref(db, `posts/${postId}`), { likesCount: currentLikes + 1 });
        window.tipCreator = (postId, currentTips) => {
            update(ref(db, `posts/${postId}`), { tipsCount: currentTips + 1 });
            updateUserCoins(10);
        };
    </script>
</body>
</html>
