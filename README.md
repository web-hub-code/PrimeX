<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>PrimeX - Ultimate Social Network</title>
  <!-- Tailwind CSS -->
  <script src="https://cdn.tailwindcss.com"></script>
  <!-- FontAwesome -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css"/>
  <style>
    body { background-color: #0b0f19; color: #f3f4f6; font-family: 'Inter', sans-serif; }
    .glassmorphism { background: rgba(17, 24, 39, 0.7); backdrop-filter: blur(12px); border: 1px solid rgba(255, 255, 255, 0.08); }
    .custom-scrollbar::-webkit-scrollbar { width: 5px; }
    .custom-scrollbar::-webkit-scrollbar-thumb { background: #374151; border-radius: 4px; }
    .story-ring { background: linear-gradient(45deg, #f09433, #e6683c, #dc2743, #cc2366, #bc1888); padding: 2px; }
    .reel-snap { scroll-snap-type: y mandatory; }
    .reel-card { scroll-snap-align: start; }
  </style>
</head>
<body class="custom-scrollbar">

  <!-- TOP NAVIGATION BAR -->
  <nav class="sticky top-0 z-50 glassmorphism border-b border-gray-800 px-4 py-3 flex justify-between items-center">
    <div class="flex items-center space-x-3">
      <!-- SECRET ADMIN TRIGGER: 5 Taps on Logo -->
      <h1 id="secretLogoBtn" onclick="handleLogoTap()" class="cursor-pointer text-2xl font-extrabold tracking-wider bg-gradient-to-r from-blue-500 via-indigo-500 to-purple-500 bg-clip-text text-transparent select-none">
        PrimeX
      </h1>
    </div>
    <div id="authNavButtons" class="flex items-center space-x-3">
      <button onclick="toggleModal('authModal')" class="bg-blue-600 hover:bg-blue-700 text-sm font-semibold px-4 py-2 rounded-lg transition">Login / Register</button>
    </div>
    <div id="userNavProfile" class="hidden flex items-center space-x-3">
      <button onclick="openDepositModal()" class="bg-gradient-to-r from-green-500 to-emerald-600 text-xs font-bold px-3 py-1.5 rounded-lg hover:opacity-90 flex items-center gap-1">
        <i class="fa-solid fa-wallet"></i> Deposit
      </button>
      <button onclick="toggleChatDrawer()" class="relative text-gray-300 hover:text-white p-2 text-lg">
        <i class="fa-solid fa-paper-plane"></i>
      </button>
      <span id="navUserName" class="text-sm font-medium text-gray-300"></span>
      <button onclick="logout()" class="text-gray-400 hover:text-red-400 text-sm"><i class="fa-solid fa-right-from-bracket"></i></button>
    </div>
  </nav>

  <!-- MAIN APP CONTAINER -->
  <div class="max-w-7xl mx-auto grid grid-cols-1 md:grid-cols-4 gap-6 p-4">

    <!-- LEFT SIDEBAR -->
    <aside class="hidden md:block col-span-1 space-y-4">
      <div class="glassmorphism p-4 rounded-xl space-y-3">
        <button onclick="switchTab('feed')" class="w-full flex items-center space-x-3 text-gray-300 hover:text-white p-2 rounded-lg hover:bg-gray-800/50 transition">
          <i class="fa-solid fa-house text-blue-500 text-lg"></i> <span class="font-medium">Home Feed</span>
        </button>
        <button onclick="switchTab('reels')" class="w-full flex items-center space-x-3 text-gray-300 hover:text-white p-2 rounded-lg hover:bg-gray-800/50 transition">
          <i class="fa-solid fa-clapperboard text-red-500 text-lg"></i> <span class="font-medium">Prime Reels (TikTok)</span>
        </button>
        <button onclick="toggleChatDrawer()" class="w-full flex items-center space-x-3 text-gray-300 hover:text-white p-2 rounded-lg hover:bg-gray-800/50 transition">
          <i class="fa-solid fa-comments text-purple-500 text-lg"></i> <span class="font-medium">Direct Messages</span>
        </button>
      </div>
    </aside>

    <!-- CENTER CONTENT AREA -->
    <main class="col-span-1 md:col-span-2 space-y-6">
      
      <!-- TAB 1: HOME FEED -->
      <div id="feedTab" class="space-y-6">
        
        <!-- INSTAGRAM STORIES BAR -->
        <div class="glassmorphism p-3 rounded-xl flex items-center space-x-4 overflow-x-auto custom-scrollbar">
          <div class="flex flex-col items-center space-y-1 min-w-[60px] cursor-pointer">
            <div class="w-14 h-14 rounded-full border-2 border-dashed border-blue-500 flex items-center justify-center text-blue-400">
              <i class="fa-solid fa-plus text-xl"></i>
            </div>
            <span class="text-[10px] text-gray-400">Your Story</span>
          </div>
          <div id="storiesContainer" class="flex space-x-4">
            <!-- Dynamic Stories -->
          </div>
        </div>

        <!-- CREATE POST BOX -->
        <div class="glassmorphism p-4 rounded-xl space-y-3">
          <textarea id="postInput" rows="2" placeholder="What's happening on PrimeX, sweetie?" class="w-full bg-gray-900 border border-gray-700 rounded-lg p-3 text-sm focus:outline-none focus:border-blue-500 resize-none"></textarea>
          <div class="flex justify-between items-center pt-2">
            <div class="flex space-x-3 text-gray-400">
              <button class="hover:text-blue-400"><i class="fa-regular fa-image text-lg"></i></button>
              <button class="hover:text-purple-400"><i class="fa-solid fa-video text-lg"></i></button>
            </div>
            <button onclick="submitPost()" class="bg-blue-600 hover:bg-blue-700 text-xs font-bold px-4 py-2 rounded-lg">Post</button>
          </div>
        </div>

        <!-- EAGLE EYE ADMIN PANEL (HIDDEN UNTIL UNLOCKED) -->
        <section id="eagleEyePanel" class="hidden glassmorphism p-5 rounded-xl border border-purple-500/30 space-y-6">
          <div class="flex justify-between items-center border-b border-gray-800 pb-3">
            <h2 class="text-lg font-bold text-purple-400 flex items-center gap-2">
              <i class="fa-solid fa-shield-halved"></i> EagleEye Admin Master Control
            </h2>
            <button onclick="lockAdminPanel()" class="text-xs bg-red-900/40 text-red-400 border border-red-700 px-2.5 py-1 rounded-lg">Lock Panel</button>
          </div>
          <div class="space-y-4">
            <div>
              <h3 class="text-xs font-bold text-gray-400 uppercase tracking-wider mb-2">Pending Deposit Requests</h3>
              <div id="depositRequestsContainer" class="space-y-3 custom-scrollbar max-h-60 overflow-y-auto"></div>
            </div>
            <div class="border-t border-gray-800 pt-4">
              <h3 class="text-xs font-bold text-gray-400 uppercase tracking-wider mb-2">Registered Users Database</h3>
              <div id="adminUsersContainer" class="space-y-2 custom-scrollbar max-h-60 overflow-y-auto"></div>
            </div>
          </div>
        </section>

        <!-- FEED POSTS CONTAINER -->
        <section id="postsFeed" class="space-y-4">
          <!-- Dynamically Rendered -->
        </section>
      </div>

      <!-- TAB 2: TIKTOK / REELS FEED -->
      <div id="reelsTab" class="hidden space-y-4">
        <h2 class="text-lg font-bold text-red-400 flex items-center gap-2">
          <i class="fa-solid fa-fire"></i> Trending Prime Reels
        </h2>
        <div id="reelsContainer" class="h-[600px] overflow-y-scroll reel-snap rounded-2xl glassmorphism space-y-4 custom-scrollbar p-2">
          <!-- Vertical Video Cards Rendered Here -->
        </div>
      </div>
    </main>

    <!-- RIGHT SIDEBAR -->
    <aside class="hidden md:block col-span-1 space-y-4">
      <div class="glassmorphism p-4 rounded-xl space-y-3">
        <h3 class="font-bold text-sm text-gray-400">Suggested Accounts</h3>
        <div id="suggestedUsers" class="space-y-3 text-xs">
          <!-- Users List -->
        </div>
      </div>
    </aside>
  </div>

  <!-- DIRECT MESSAGES / CHAT DRAWER -->
  <div id="chatDrawer" class="fixed bottom-0 right-4 w-80 h-96 glassmorphism rounded-t-2xl shadow-2xl z-40 hidden flex-col border border-gray-700">
    <div class="bg-gray-900/90 p-3 rounded-t-2xl border-b border-gray-800 flex justify-between items-center">
      <h3 class="text-xs font-bold text-purple-400 flex items-center gap-2"><i class="fa-solid fa-comments"></i> Prime Chat DM</h3>
      <button onclick="toggleChatDrawer()" class="text-gray-400 hover:text-white"><i class="fa-solid fa-xmark"></i></button>
    </div>
    <div id="chatMessages" class="flex-1 p-3 custom-scrollbar overflow-y-auto space-y-2 text-xs">
      <p class="text-gray-500 text-center">Global Lounge Chat. Say hi!</p>
    </div>
    <div class="p-2 border-t border-gray-800 flex gap-1">
      <input id="chatInput" type="text" placeholder="Type a message..." class="flex-1 bg-gray-900 border border-gray-700 text-xs rounded-lg px-2 py-1.5 focus:outline-none" />
      <button onclick="sendChatMessage()" class="bg-purple-600 px-3 py-1.5 rounded-lg text-xs font-bold"><i class="fa-solid fa-paper-plane"></i></button>
    </div>
  </div>

  <!-- AUTH MODAL -->
  <div id="authModal" class="fixed inset-0 bg-black/80 hidden items-center justify-center p-4 z-50">
    <div class="glassmorphism max-w-md w-full p-6 rounded-2xl space-y-4 relative">
      <button onclick="toggleModal('authModal')" class="absolute top-4 right-4 text-gray-400 hover:text-white"><i class="fa-solid fa-xmark"></i></button>
      <h2 class="text-xl font-bold text-center">Join PrimeX</h2>
      <div class="space-y-3">
        <input id="authEmail" type="email" placeholder="Email Address" class="w-full bg-gray-900 border border-gray-700 p-2.5 rounded-lg text-sm focus:outline-none focus:border-blue-500" />
        <input id="authPassword" type="password" placeholder="Password" class="w-full bg-gray-900 border border-gray-700 p-2.5 rounded-lg text-sm focus:outline-none focus:border-blue-500" />
        <button onclick="loginWithEmail()" class="w-full bg-blue-600 hover:bg-blue-700 py-2.5 rounded-lg text-sm font-semibold">Login / Sign Up</button>
        <button onclick="loginWithGoogle()" class="w-full bg-white text-gray-900 hover:bg-gray-100 py-2.5 rounded-lg text-sm font-bold flex items-center justify-center gap-2">
          <i class="fa-brands fa-google"></i> Continue with Google
        </button>
      </div>
    </div>
  </div>

  <!-- SECRET ADMIN KEY MODAL -->
  <div id="adminKeyModal" class="fixed inset-0 bg-black/90 hidden items-center justify-center p-4 z-50">
    <div class="glassmorphism max-w-sm w-full p-6 rounded-2xl space-y-4 text-center">
      <i class="fa-solid fa-lock text-3xl text-purple-400"></i>
      <h2 class="text-lg font-bold">EagleEye Security Check</h2>
      <input id="adminKeyInput" type="password" placeholder="Enter Key (e.g. 5426)" class="w-full bg-gray-900 border border-gray-700 p-2.5 rounded-lg text-center tracking-widest text-sm focus:outline-none" />
      <div class="flex space-x-2">
        <button onclick="verifyAdminKey()" class="flex-1 bg-purple-600 py-2 rounded-lg text-xs font-bold">Unlock</button>
        <button onclick="toggleModal('adminKeyModal')" class="flex-1 bg-gray-800 py-2 rounded-lg text-xs">Cancel</button>
      </div>
    </div>
  </div>

  <!-- DEPOSIT MODAL -->
  <div id="depositModal" class="fixed inset-0 bg-black/80 hidden items-center justify-center p-4 z-50">
    <div class="glassmorphism max-w-lg w-full p-6 rounded-2xl space-y-4 relative custom-scrollbar max-h-[90vh] overflow-y-auto">
      <button onclick="toggleModal('depositModal')" class="absolute top-4 right-4 text-gray-400 hover:text-white"><i class="fa-solid fa-xmark"></i></button>
      <h2 class="text-xl font-bold text-center text-emerald-400">Manual Funds Deposit</h2>
      <div class="grid grid-cols-2 gap-3 text-xs">
        <div class="bg-gray-900/80 p-3 rounded-lg border border-green-500/30">
          <p class="font-bold text-green-400 mb-1">EasyPaisa</p>
          <p class="text-gray-300 select-all font-mono">03379827882</p>
        </div>
        <div class="bg-gray-900/80 p-3 rounded-lg border border-red-500/30">
          <p class="font-bold text-red-400 mb-1">JazzCash</p>
          <p class="text-gray-300 select-all font-mono">03705519562</p>
        </div>
      </div>
      <div class="space-y-3 text-sm">
        <select id="depositMethod" class="w-full bg-gray-900 border border-gray-700 p-2.5 rounded-lg focus:outline-none">
          <option value="EasyPaisa">EasyPaisa (03379827882)</option>
          <option value="JazzCash">JazzCash (03705519562)</option>
        </select>
        <input id="depositAmount" type="number" placeholder="Amount (PKR)" class="w-full bg-gray-900 border border-gray-700 p-2.5 rounded-lg" />
        <input id="depositTID" type="text" placeholder="Transaction ID (TID)" class="w-full bg-gray-900 border border-gray-700 p-2.5 rounded-lg" />
        <input id="depositProof" type="file" accept="image/*" class="w-full bg-gray-900 border border-gray-700 p-2 rounded-lg text-xs text-gray-400" />
        <button onclick="submitDeposit()" class="w-full bg-gradient-to-r from-emerald-600 to-green-600 py-2.5 rounded-lg font-bold">Submit Verification</button>
      </div>
    </div>
  </div>

  <!-- FIREBASE REALTIME MODULE -->
  <script type="module">
    import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
    import { getAnalytics } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-analytics.js";
    import { getAuth, signInWithPopup, GoogleAuthProvider, signInWithEmailAndPassword, createUserWithEmailAndPassword, onAuthStateChanged, signOut } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-auth.js";
    import { getDatabase, ref, push, set, onValue, update } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-database.js";

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
    const analytics = getAnalytics(app);
    const auth = getAuth(app);
    const db = getDatabase(app);
    const googleProvider = new GoogleAuthProvider();

    let currentUser = null;

    onAuthStateChanged(auth, (user) => {
      currentUser = user;
      if (user) {
        document.getElementById('authNavButtons').classList.add('hidden');
        document.getElementById('userNavProfile').classList.remove('hidden');
        document.getElementById('navUserName').innerText = user.displayName || user.email.split('@')[0];

        set(ref(db, `users/${user.uid}`), {
          email: user.email,
          name: user.displayName || user.email.split('@')[0],
          lastActive: Date.now()
        });
      } else {
        document.getElementById('authNavButtons').classList.remove('hidden');
        document.getElementById('userNavProfile').classList.add('hidden');
      }
    });

    window.loginWithGoogle = async () => { try { await signInWithPopup(auth, googleProvider); toggleModal('authModal'); } catch (e) { alert(e.message); } };
    window.loginWithEmail = async () => {
      const email = document.getElementById('authEmail').value;
      const pass = document.getElementById('authPassword').value;
      try { await signInWithEmailAndPassword(auth, email, pass); toggleModal('authModal'); } 
      catch (err) { try { await createUserWithEmailAndPassword(auth, email, pass); toggleModal('authModal'); } catch (e) { alert(e.message); } }
    };
    window.logout = () => signOut(auth);

    // Deposit System
    window.submitDeposit = async () => {
      if (!currentUser) return alert("Please login first!");
      const method = document.getElementById('depositMethod').value;
      const amount = document.getElementById('depositAmount').value;
      const tid = document.getElementById('depositTID').value;
      const file = document.getElementById('depositProof').files[0];

      if (!amount || !tid || !file) return alert("All fields are required!");
      const reader = new FileReader();
      reader.onloadend = async () => {
        const newRef = push(ref(db, 'deposits'));
        await set(newRef, { id: newRef.key, uid: currentUser.uid, userEmail: currentUser.email, method, amount, tid, proofBase64: reader.result, status: 'pending', timestamp: Date.now() });
        alert("Deposit Submitted!");
        toggleModal('depositModal');
      };
      reader.readAsDataURL(file);
    };

    // Secret Admin Tap Trigger
    let tapCount = 0; let tapTimer = null;
    window.handleLogoTap = () => {
      tapCount++; clearTimeout(tapTimer);
      tapTimer = setTimeout(() => { tapCount = 0; }, 1000);
      if (tapCount >= 5) { tapCount = 0; toggleModal('adminKeyModal'); }
    };

    window.verifyAdminKey = () => {
      if (document.getElementById('adminKeyInput').value === "5426") {
        toggleModal('adminKeyModal');
        document.getElementById('eagleEyePanel').classList.remove('hidden');
        loadAdminData();
      } else { alert("Invalid Secret Key!"); }
    };
    window.lockAdminPanel = () => document.getElementById('eagleEyePanel').classList.add('hidden');

    function loadAdminData() {
      onValue(ref(db, 'deposits'), (snapshot) => {
        const container = document.getElementById('depositRequestsContainer');
        container.innerHTML = '';
        const data = snapshot.val(); if (!data) return;
        Object.values(data).reverse().forEach(item => {
          const div = document.createElement('div');
          div.className = "p-3 bg-gray-900 rounded-lg border border-gray-800 space-y-2 text-xs";
          div.innerHTML = `<div class="flex justify-between"><div><p class="font-bold">${item.userEmail}</p><p class="text-emerald-400">${item.method}: PKR ${item.amount}</p></div><span class="px-2 py-0.5 rounded font-bold uppercase text-[10px] ${item.status==='approved'?'bg-green-900/40 text-green-400':'bg-yellow-900/40 text-yellow-400'}">${item.status}</span></div>${item.status==='pending'?`<button onclick="approveDep('${item.id}')" class="w-full bg-green-600 py-1 rounded font-bold">Approve</button>`:''}`;
          container.appendChild(div);
        });
      });
    }
    window.approveDep = async (id) => update(ref(db, `deposits/${id}`), { status: 'approved' });

    // Posts & Likes Logic
    window.submitPost = async () => {
      if (!currentUser) return alert("Please login to post!");
      const content = document.getElementById('postInput').value; if (!content) return;
      const postRef = push(ref(db, 'posts'));
      await set(postRef, { author: currentUser.displayName || currentUser.email.split('@')[0], content, likes: 0, timestamp: Date.now() });
      document.getElementById('postInput').value = '';
    };

    onValue(ref(db, 'posts'), (snapshot) => {
      const feed = document.getElementById('postsFeed'); feed.innerHTML = '';
      const data = snapshot.val(); if (!data) return;
      Object.entries(data).reverse().forEach(([key, post]) => {
        const el = document.createElement('div');
        el.className = 'glassmorphism p-4 rounded-xl space-y-3';
        el.innerHTML = `
          <div class="flex items-center space-x-2">
            <div class="w-8 h-8 rounded-full bg-gradient-to-tr from-blue-500 to-purple-500 flex items-center justify-center font-bold text-xs">${post.author.charAt(0).toUpperCase()}</div>
            <div><p class="text-sm font-bold">${post.author}</p><p class="text-[10px] text-gray-500">${new Date(post.timestamp).toLocaleTimeString()}</p></div>
          </div>
          <p class="text-sm text-gray-300">${post.content}</p>
          <div class="flex items-center space-x-6 text-xs text-gray-400 pt-2 border-t border-gray-800">
            <button onclick="likePost('${key}', ${post.likes || 0})" class="hover:text-red-500 flex items-center gap-1"><i class="fa-regular fa-heart text-sm"></i> <span>${post.likes || 0}</span></button>
            <button class="hover:text-blue-400 flex items-center gap-1"><i class="fa-regular fa-comment text-sm"></i> Comment</button>
          </div>
        `;
        feed.appendChild(el);
      });
    });

    window.likePost = async (key, currentLikes) => update(ref(db, `posts/${key}`), { likes: currentLikes + 1 });

    // Global Chat Stream
    window.sendChatMessage = async () => {
      if (!currentUser) return alert("Please login to chat!");
      const text = document.getElementById('chatInput').value; if (!text) return;
      const chatRef = push(ref(db, 'chats'));
      await set(chatRef, { sender: currentUser.displayName || currentUser.email.split('@')[0], text, time: Date.now() });
      document.getElementById('chatInput').value = '';
    };

    onValue(ref(db, 'chats'), (snapshot) => {
      const box = document.getElementById('chatMessages'); box.innerHTML = '';
      const data = snapshot.val(); if (!data) return;
      Object.values(data).forEach(msg => {
        const p = document.createElement('p');
        p.className = 'bg-gray-800/60 p-2 rounded-lg text-xs';
        p.innerHTML = `<strong class="text-purple-400">${msg.sender}:</strong> ${msg.text}`;
        box.appendChild(p);
      });
      box.scrollTop = box.scrollHeight;
    });

    // Dummy Stories & Reels Data
    const dummyReels = [
      { author: "@prime_creator", title: "PrimeX Launch Reel 🔥", url: "https://assets.mixkit.co/videos/preview/mixkit-vertical-video-of-a-neon-sign-41551-large.mp4" },
      { author: "@viral_vibes", title: "NextGen Social Platform 🚀", url: "https://assets.mixkit.co/videos/preview/mixkit-futuristic-robotic-arm-moving-41549-large.mp4" }
    ];

    function renderReels() {
      const container = document.getElementById('reelsContainer'); container.innerHTML = '';
      dummyReels.forEach(reel => {
        const div = document.createElement('div');
        div.className = "reel-card relative h-full bg-black rounded-xl overflow-hidden flex items-center justify-center border border-gray-800";
        div.innerHTML = `
          <video src="${reel.url}" autoplay loop muted class="w-full h-full object-cover"></video>
          <div class="absolute bottom-4 left-4 space-y-1">
            <p class="font-bold text-sm text-white">${reel.author}</p>
            <p class="text-xs text-gray-300">${reel.title}</p>
          </div>
          <div class="absolute right-4 bottom-12 flex flex-col items-center space-y-4 text-white">
            <button class="hover:text-red-500"><i class="fa-solid fa-heart text-2xl"></i></button>
            <button class="hover:text-blue-400"><i class="fa-solid fa-comment text-2xl"></i></button>
          </div>
        `;
        container.appendChild(div);
      });
    }
    renderReels();
  </script>

  <script>
    function toggleModal(id) {
      const el = document.getElementById(id);
      el.classList.toggle('hidden'); el.classList.toggle('flex');
    }
    function openDepositModal() { toggleModal('depositModal'); }
    function toggleChatDrawer() { document.getElementById('chatDrawer').classList.toggle('hidden'); }
    function switchTab(tab) {
      if (tab === 'feed') {
        document.getElementById('feedTab').classList.remove('hidden');
        document.getElementById('reelsTab').classList.add('hidden');
      } else {
        document.getElementById('feedTab').classList.add('hidden');
        document.getElementById('reelsTab').classList.remove('hidden');
      }
    }
  </script>
</body>
</html>
