<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>PrimeX - Earning & Social Network</title>
  <!-- Tailwind CSS -->
  <script src="https://cdn.tailwindcss.com"></script>
  <!-- FontAwesome -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css"/>
  <style>
    body { background-color: #0b0f19; color: #f3f4f6; font-family: 'Inter', sans-serif; }
    .glassmorphism { background: rgba(17, 24, 39, 0.7); backdrop-filter: blur(12px); border: 1px solid rgba(255, 255, 255, 0.08); }
    .custom-scrollbar::-webkit-scrollbar { width: 5px; }
    .custom-scrollbar::-webkit-scrollbar-thumb { background: #374151; border-radius: 4px; }
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
      <button onclick="openWalletModal()" class="bg-gradient-to-r from-amber-500 to-yellow-600 text-xs font-bold px-3 py-1.5 rounded-lg hover:opacity-90 flex items-center gap-1 text-black">
        <i class="fa-solid fa-coins"></i> <span id="navWalletBalance">PKR 0</span>
      </button>
      <button onclick="openDepositModal()" class="bg-gradient-to-r from-green-500 to-emerald-600 text-xs font-bold px-3 py-1.5 rounded-lg hover:opacity-90 flex items-center gap-1">
        <i class="fa-solid fa-wallet"></i> Deposit
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
        <button onclick="openWalletModal()" class="w-full flex items-center space-x-3 text-gray-300 hover:text-white p-2 rounded-lg hover:bg-gray-800/50 transition">
          <i class="fa-solid fa-wallet text-amber-500 text-lg"></i> <span class="font-medium">Creator Earnings</span>
        </button>
      </div>
    </aside>

    <!-- CENTER CONTENT AREA -->
    <main class="col-span-1 md:col-span-2 space-y-6">
      
      <!-- TAB 1: HOME FEED -->
      <div id="feedTab" class="space-y-6">
        
        <!-- CREATE POST BOX (PHONE STORAGE UPLOAD) -->
        <div class="glassmorphism p-4 rounded-xl space-y-3">
          <textarea id="postInput" rows="2" placeholder="What's happening on PrimeX, sweetie?" class="w-full bg-gray-900 border border-gray-700 rounded-lg p-3 text-sm focus:outline-none focus:border-blue-500 resize-none"></textarea>
          
          <!-- Image/Video Preview Container -->
          <div id="mediaPreviewContainer" class="hidden relative">
            <img id="imagePreview" class="w-full h-40 object-cover rounded-lg hidden" />
            <video id="videoPreview" class="w-full h-40 object-cover rounded-lg hidden" controls></video>
            <button onclick="clearMedia()" class="absolute top-2 right-2 bg-red-600 text-white rounded-full w-6 h-6 text-xs flex items-center justify-center"><i class="fa-solid fa-xmark"></i></button>
          </div>

          <div class="flex justify-between items-center pt-2">
            <div class="flex space-x-3 text-gray-400">
              <label class="cursor-pointer hover:text-blue-400"><i class="fa-regular fa-image text-lg"></i><input type="file" id="imageInput" accept="image/*" class="hidden" onchange="previewMedia(this, 'image')"></label>
              <label class="cursor-pointer hover:text-purple-400"><i class="fa-solid fa-video text-lg"></i><input type="file" id="videoInput" accept="video/*" class="hidden" onchange="previewMedia(this, 'video')"></label>
            </div>
            <button onclick="submitPost()" class="bg-blue-600 hover:bg-blue-700 text-xs font-bold px-4 py-2 rounded-lg">Publish Post</button>
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
              <h3 class="text-xs font-bold text-gray-400 uppercase tracking-wider mb-2">Pending Deposits</h3>
              <div id="depositRequestsContainer" class="space-y-3 custom-scrollbar max-h-48 overflow-y-auto"></div>
            </div>
            <div class="border-t border-gray-800 pt-4">
              <h3 class="text-xs font-bold text-gray-400 uppercase tracking-wider mb-2">Pending Earning Withdrawals</h3>
              <div id="withdrawRequestsContainer" class="space-y-3 custom-scrollbar max-h-48 overflow-y-auto"></div>
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
        <div class="flex justify-between items-center">
          <h2 class="text-lg font-bold text-red-400 flex items-center gap-2">
            <i class="fa-solid fa-fire"></i> Prime Reels Feed
          </h2>
          <button onclick="openUploadReelModal()" class="bg-red-600 hover:bg-red-700 text-xs font-bold px-3 py-1.5 rounded-lg flex items-center gap-1">
            <i class="fa-solid fa-plus"></i> Upload Reel
          </button>
        </div>
        <div id="reelsContainer" class="h-[600px] overflow-y-scroll reel-snap rounded-2xl glassmorphism space-y-4 custom-scrollbar p-2">
          <!-- Vertical Video Cards Rendered Here -->
        </div>
      </div>
    </main>

    <!-- RIGHT SIDEBAR -->
    <aside class="hidden md:block col-span-1 space-y-4">
      <div class="glassmorphism p-4 rounded-xl space-y-3">
        <h3 class="font-bold text-sm text-yellow-400 flex items-center gap-1"><i class="fa-solid fa-bolt"></i> Creator Monetization</h3>
        <p class="text-xs text-gray-300 leading-relaxed">
          Upload engaging videos and get rewarded! Every view and like increases your earning balance instantly. Withdraw via EasyPaisa/JazzCash.
        </p>
      </div>
    </aside>
  </div>

  <!-- UPLOAD REEL MODAL -->
  <div id="uploadReelModal" class="fixed inset-0 bg-black/80 hidden items-center justify-center p-4 z-50">
    <div class="glassmorphism max-w-md w-full p-6 rounded-2xl space-y-4 relative">
      <button onclick="toggleModal('uploadReelModal')" class="absolute top-4 right-4 text-gray-400 hover:text-white"><i class="fa-solid fa-xmark"></i></button>
      <h2 class="text-lg font-bold text-center text-red-400">Upload Short Reel</h2>
      <input id="reelTitleInput" type="text" placeholder="Reel Caption / Title" class="w-full bg-gray-900 border border-gray-700 p-2.5 rounded-lg text-sm" />
      <div>
        <label class="text-xs text-gray-400">Select Video from Device</label>
        <input id="reelVideoFile" type="file" accept="video/*" class="w-full bg-gray-900 border border-gray-700 p-2 rounded-lg text-xs mt-1" />
      </div>
      <button onclick="submitReel()" class="w-full bg-red-600 hover:bg-red-700 py-2.5 rounded-lg text-sm font-bold">Publish Reel</button>
    </div>
  </div>

  <!-- WALLET & WITHDRAW MODAL -->
  <div id="walletModal" class="fixed inset-0 bg-black/80 hidden items-center justify-center p-4 z-50">
    <div class="glassmorphism max-w-md w-full p-6 rounded-2xl space-y-4 relative">
      <button onclick="toggleModal('walletModal')" class="absolute top-4 right-4 text-gray-400 hover:text-white"><i class="fa-solid fa-xmark"></i></button>
      <h2 class="text-lg font-bold text-center text-amber-400 flex items-center justify-center gap-2"><i class="fa-solid fa-wallet"></i> Creator Earnings Wallet</h2>
      
      <div class="bg-gray-900 p-4 rounded-xl text-center space-y-1 border border-amber-500/30">
        <p class="text-xs text-gray-400">Available Balance</p>
        <p id="modalUserBalance" class="text-2xl font-extrabold text-amber-400">PKR 0</p>
        <p class="text-[10px] text-gray-500">Earned from video views & post interactions</p>
      </div>

      <div class="space-y-3 text-xs">
        <div>
          <label class="text-gray-400">Select Payment Method</label>
          <select id="withdrawMethod" class="w-full bg-gray-900 border border-gray-700 p-2.5 rounded-lg mt-1">
            <option value="EasyPaisa">EasyPaisa</option>
            <option value="JazzCash">JazzCash</option>
          </select>
        </div>
        <div>
          <label class="text-gray-400">Account Number / Phone</label>
          <input id="withdrawAccount" type="text" placeholder="03XXXXXXXXX" class="w-full bg-gray-900 border border-gray-700 p-2.5 rounded-lg mt-1" />
        </div>
        <div>
          <label class="text-gray-400">Withdraw Amount (PKR)</label>
          <input id="withdrawAmount" type="number" placeholder="Min PKR 500" class="w-full bg-gray-900 border border-gray-700 p-2.5 rounded-lg mt-1" />
        </div>
        <button onclick="requestWithdrawal()" class="w-full bg-amber-600 hover:bg-amber-700 py-2.5 rounded-lg text-sm font-bold text-black">Request Withdrawal</button>
      </div>
    </div>
  </div>

  <!-- AUTH MODAL -->
  <div id="authModal" class="fixed inset-0 bg-black/80 hidden items-center justify-center p-4 z-50">
    <div class="glassmorphism max-w-md w-full p-6 rounded-2xl space-y-4 relative">
      <button onclick="toggleModal('authModal')" class="absolute top-4 right-4 text-gray-400 hover:text-white"><i class="fa-solid fa-xmark"></i></button>
      <h2 class="text-xl font-bold text-center">Join PrimeX</h2>
      <div class="space-y-3">
        <input id="authEmail" type="email" placeholder="Email Address" class="w-full bg-gray-900 border border-gray-700 p-2.5 rounded-lg text-sm focus:outline-none" />
        <input id="authPassword" type="password" placeholder="Password" class="w-full bg-gray-900 border border-gray-700 p-2.5 rounded-lg text-sm focus:outline-none" />
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
      <input id="adminKeyInput" type="password" placeholder="Enter Key (5426)" class="w-full bg-gray-900 border border-gray-700 p-2.5 rounded-lg text-center tracking-widest text-sm focus:outline-none" />
      <div class="flex space-x-2">
        <button onclick="verifyAdminKey()" class="flex-1 bg-purple-600 py-2 rounded-lg text-xs font-bold">Unlock</button>
        <button onclick="toggleModal('adminKeyModal')" class="flex-1 bg-gray-800 py-2 rounded-lg text-xs">Cancel</button>
      </div>
    </div>
  </div>

  <!-- DEPOSIT MODAL -->
  <div id="depositModal" class="fixed inset-0 bg-black/80 hidden items-center justify-center p-4 z-50">
    <div class="glassmorphism max-w-lg w-full p-6 rounded-2xl space-y-4 relative">
      <button onclick="toggleModal('depositModal')" class="absolute top-4 right-4 text-gray-400 hover:text-white"><i class="fa-solid fa-xmark"></i></button>
      <h2 class="text-xl font-bold text-center text-emerald-400">Manual Funds Deposit</h2>
      <div class="grid grid-cols-2 gap-3 text-xs">
        <div class="bg-gray-900 p-3 rounded-lg border border-green-500/30">
          <p class="font-bold text-green-400 mb-1">EasyPaisa</p>
          <p class="text-gray-300 select-all font-mono">03379827882</p>
        </div>
        <div class="bg-gray-900 p-3 rounded-lg border border-red-500/30">
          <p class="font-bold text-red-400 mb-1">JazzCash</p>
          <p class="text-gray-300 select-all font-mono">03705519562</p>
        </div>
      </div>
      <div class="space-y-3 text-sm">
        <select id="depositMethod" class="w-full bg-gray-900 border border-gray-700 p-2.5 rounded-lg">
          <option value="EasyPaisa">EasyPaisa (03379827882)</option>
          <option value="JazzCash">JazzCash (03705519562)</option>
        </select>
        <input id="depositAmount" type="number" placeholder="Amount (PKR)" class="w-full bg-gray-900 border border-gray-700 p-2.5 rounded-lg" />
        <input id="depositTID" type="text" placeholder="Transaction ID (TID)" class="w-full bg-gray-900 border border-gray-700 p-2.5 rounded-lg" />
        <input id="depositProof" type="file" accept="image/*" class="w-full bg-gray-900 border border-gray-700 p-2 rounded-lg text-xs text-gray-400" />
        <button onclick="submitDeposit()" class="w-full bg-emerald-600 py-2.5 rounded-lg font-bold">Submit Deposit</button>
      </div>
    </div>
  </div>

  <!-- FIREBASE LOGIC & BASE64 STORAGE HANDLING -->
  <script type="module">
    import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
    import { getAnalytics } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-analytics.js";
    import { getAuth, signInWithPopup, GoogleAuthProvider, signInWithEmailAndPassword, createUserWithEmailAndPassword, onAuthStateChanged, signOut } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-auth.js";
    import { getDatabase, ref, push, set, onValue, update, get } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-database.js";

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
    let selectedMediaBase64 = null;
    let selectedMediaType = null;

    onAuthStateChanged(auth, (user) => {
      currentUser = user;
      if (user) {
        document.getElementById('authNavButtons').classList.add('hidden');
        document.getElementById('userNavProfile').classList.remove('hidden');
        document.getElementById('navUserName').innerText = user.displayName || user.email.split('@')[0];
        loadUserWallet(user.uid);
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

    // Load Wallet Balance
    function loadUserWallet(uid) {
      onValue(ref(db, `wallets/${uid}`), (snapshot) => {
        const bal = snapshot.val()?.balance || 0;
        document.getElementById('navWalletBalance').innerText = `PKR ${bal}`;
        document.getElementById('modalUserBalance').innerText = `PKR ${bal}`;
      });
    }

    // Direct Device Media Preview & Base64 Converter
    window.previewMedia = (input, type) => {
      const file = input.files[0];
      if (!file) return;
      selectedMediaType = type;
      const reader = new FileReader();
      reader.onloadend = () => {
        selectedMediaBase64 = reader.result;
        document.getElementById('mediaPreviewContainer').classList.remove('hidden');
        if (type === 'image') {
          document.getElementById('imagePreview').src = selectedMediaBase64;
          document.getElementById('imagePreview').classList.remove('hidden');
          document.getElementById('videoPreview').classList.add('hidden');
        } else {
          document.getElementById('videoPreview').src = selectedMediaBase64;
          document.getElementById('videoPreview').classList.remove('hidden');
          document.getElementById('imagePreview').classList.add('hidden');
        }
      };
      reader.readAsDataURL(file);
    };

    window.clearMedia = () => {
      selectedMediaBase64 = null;
      selectedMediaType = null;
      document.getElementById('mediaPreviewContainer').classList.add('hidden');
      document.getElementById('imageInput').value = '';
      document.getElementById('videoInput').value = '';
    };

    // Publish Post with Direct Media
    window.submitPost = async () => {
      if (!currentUser) return alert("Please login first, sweetie!");
      const content = document.getElementById('postInput').value;
      if (!content && !selectedMediaBase64) return alert("Add text or media!");

      const postRef = push(ref(db, 'posts'));
      await set(postRef, {
        author: currentUser.displayName || currentUser.email.split('@')[0],
        uid: currentUser.uid,
        content,
        media: selectedMediaBase64 || null,
        mediaType: selectedMediaType || null,
        likes: 0,
        timestamp: Date.now()
      });

      document.getElementById('postInput').value = '';
      clearMedia();
      alert("Post published live!");
    };

    // Publish Reel with Direct Device Video
    window.submitReel = async () => {
      if (!currentUser) return alert("Please login first!");
      const title = document.getElementById('reelTitleInput').value;
      const file = document.getElementById('reelVideoFile').files[0];
      if (!title || !file) return alert("Title and video file required!");

      const reader = new FileReader();
      reader.onloadend = async () => {
        const reelRef = push(ref(db, 'reels'));
        await set(reelRef, {
          author: currentUser.displayName || currentUser.email.split('@')[0],
          uid: currentUser.uid,
          title,
          videoBase64: reader.result,
          likes: 0,
          views: 0,
          timestamp: Date.now()
        });
        alert("Reel uploaded successfully!");
        toggleModal('uploadReelModal');
        document.getElementById('reelTitleInput').value = '';
        document.getElementById('reelVideoFile').value = '';
      };
      reader.readAsDataURL(file);
    };

    // Interaction & Earning Generator (Like gives earning to author)
    window.likePost = async (key, postUid, currentLikes) => {
      await update(ref(db, `posts/${key}`), { likes: currentLikes + 1 });
      // Give earning reward to author (e.g. PKR 5 per like)
      if (postUid) {
        const walletRef = ref(db, `wallets/${postUid}/balance`);
        const snap = await get(walletRef);
        const currentBal = snap.exists() ? snap.val() : 0;
        await set(walletRef, currentBal + 5);
      }
    };

    // Withdraw Request System
    window.requestWithdrawal = async () => {
      if (!currentUser) return;
      const method = document.getElementById('withdrawMethod').value;
      const account = document.getElementById('withdrawAccount').value;
      const amount = parseFloat(document.getElementById('withdrawAmount').value);

      if (!account || !amount || amount < 500) return alert("Minimum withdrawal amount is PKR 500!");

      const walletRef = ref(db, `wallets/${currentUser.uid}/balance`);
      const snap = await get(walletRef);
      const currentBal = snap.exists() ? snap.val() : 0;

      if (currentBal < amount) return alert("Insufficient balance in your wallet!");

      // Deduct temporarily & create request
      await set(walletRef, currentBal - amount);
      const reqRef = push(ref(db, 'withdrawals'));
      await set(reqRef, {
        id: reqRef.key,
        uid: currentUser.uid,
        userEmail: currentUser.email,
        method,
        account,
        amount,
        status: 'pending',
        timestamp: Date.now()
      });

      alert("Withdrawal request submitted successfully!");
      toggleModal('walletModal');
    };

    // Feed Realtime Render
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
          ${post.media && post.mediaType === 'image' ? `<img src="${post.media}" class="w-full h-64 object-cover rounded-lg" />` : ''}
          ${post.media && post.mediaType === 'video' ? `<video src="${post.media}" controls class="w-full h-64 object-cover rounded-lg"></video>` : ''}
          <div class="flex items-center space-x-6 text-xs text-gray-400 pt-2 border-t border-gray-800">
            <button onclick="likePost('${key}', '${post.uid}', ${post.likes || 0})" class="hover:text-red-500 flex items-center gap-1"><i class="fa-regular fa-heart text-sm"></i> <span>${post.likes || 0} Likes</span></button>
          </div>
        `;
        feed.appendChild(el);
      });
    });

    // Reels Realtime Render
    onValue(ref(db, 'reels'), (snapshot) => {
      const container = document.getElementById('reelsContainer'); container.innerHTML = '';
      const data = snapshot.val(); if (!data) { container.innerHTML = `<p class="text-xs text-center text-gray-500 py-20">No reels uploaded yet. Be the first!</p>`; return; }
      Object.values(data).reverse().forEach(reel => {
        const div = document.createElement('div');
        div.className = "reel-card relative h-full bg-black rounded-xl overflow-hidden flex items-center justify-center border border-gray-800";
        div.innerHTML = `
          <video src="${reel.videoBase64}" autoplay loop muted class="w-full h-full object-cover"></video>
          <div class="absolute bottom-4 left-4 space-y-1">
            <p class="font-bold text-sm text-white">${reel.author}</p>
            <p class="text-xs text-gray-300">${reel.title}</p>
          </div>
          <div class="absolute right-4 bottom-12 flex flex-col items-center space-y-4 text-white">
            <button class="hover:text-red-500"><i class="fa-solid fa-heart text-2xl"></i></button>
          </div>
        `;
        container.appendChild(div);
      });
    });

    // Secret Admin Trigger
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
      onValue(ref(db, 'withdrawals'), (snapshot) => {
        const container = document.getElementById('withdrawRequestsContainer');
        container.innerHTML = '';
        const data = snapshot.val(); if (!data) return;
        Object.values(data).reverse().forEach(item => {
          const div = document.createElement('div');
          div.className = "p-3 bg-gray-900 rounded-lg border border-gray-800 space-y-1 text-xs";
          div.innerHTML = `<p class="font-bold">${item.userEmail}</p><p class="text-amber-400">${item.method}: PKR ${item.amount} (${item.account})</p><span class="text-yellow-400 font-bold uppercase text-[10px]">${item.status}</span>`;
          container.appendChild(div);
        });
      });
    }
  </script>

  <script>
    function toggleModal(id) { const el = document.getElementById(id); el.classList.toggle('hidden'); el.classList.toggle('flex'); }
    function openDepositModal() { toggleModal('depositModal'); }
    function openWalletModal() { toggleModal('walletModal'); }
    function openUploadReelModal() { toggleModal('uploadReelModal'); }
    function switchTab(tab) {
      if (tab === 'feed') { document.getElementById('feedTab').classList.remove('hidden'); document.getElementById('reelsTab').classList.add('hidden'); }
      else { document.getElementById('feedTab').classList.add('hidden'); document.getElementById('reelsTab').classList.remove('hidden'); }
    }
  </script>
</body>
</html>
