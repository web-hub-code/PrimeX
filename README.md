<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>PrimeX - Paid Monetization & Social Network</title>
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
        PrimeX <span class="text-[10px] bg-amber-500 text-black px-1.5 py-0.5 rounded font-bold uppercase">Pro Ads</span>
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
        <i class="fa-solid fa-wallet"></i> Top-up / Add Funds
      </button>
      <div class="flex items-center gap-1">
        <span id="navUserName" class="text-sm font-medium text-gray-300"></span>
        <span id="navVerifiedBadge" class="hidden text-blue-400 text-xs" title="Verified Creator"><i class="fa-solid fa-circle-check"></i></span>
      </div>
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
          <i class="fa-solid fa-clapperboard text-red-500 text-lg"></i> <span class="font-medium">Prime Reels</span>
        </button>
        <button onclick="openVerifyModal()" class="w-full flex items-center space-x-3 text-gray-300 hover:text-white p-2 rounded-lg hover:bg-gray-800/50 transition">
          <i class="fa-solid fa-certificate text-blue-400 text-lg"></i> <span class="font-medium">Get Verified Badge</span>
        </button>
        <button onclick="openWalletModal()" class="w-full flex items-center space-x-3 text-gray-300 hover:text-white p-2 rounded-lg hover:bg-gray-800/50 transition">
          <i class="fa-solid fa-wallet text-amber-500 text-lg"></i> <span class="font-medium">Wallet & Monetization</span>
        </button>
      </div>
    </aside>

    <!-- CENTER CONTENT AREA -->
    <main class="col-span-1 md:col-span-2 space-y-6">
      
      <!-- TAB 1: HOME FEED -->
      <div id="feedTab" class="space-y-6">
        
        <!-- CREATE POST BOX -->
        <div class="glassmorphism p-4 rounded-xl space-y-3">
          <textarea id="postInput" rows="2" placeholder="What's happening on PrimeX, sweetie?" class="w-full bg-gray-900 border border-gray-700 rounded-lg p-3 text-sm focus:outline-none focus:border-blue-500 resize-none"></textarea>
          
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

        <!-- EAGLE EYE ADMIN PANEL -->
        <section id="eagleEyePanel" class="hidden glassmorphism p-5 rounded-xl border border-purple-500/30 space-y-6">
          <div class="flex justify-between items-center border-b border-gray-800 pb-3">
            <h2 class="text-lg font-bold text-purple-400 flex items-center gap-2">
              <i class="fa-solid fa-shield-halved"></i> EagleEye Admin Master Control
            </h2>
            <button onclick="lockAdminPanel()" class="text-xs bg-red-900/40 text-red-400 border border-red-700 px-2.5 py-1 rounded-lg">Lock Panel</button>
          </div>
          <div class="space-y-4">
            <div>
              <h3 class="text-xs font-bold text-gray-400 uppercase tracking-wider mb-2">Pending Fund Deposits (Top-ups)</h3>
              <div id="depositRequestsContainer" class="space-y-3 custom-scrollbar max-h-48 overflow-y-auto"></div>
            </div>
            <div class="border-t border-gray-800 pt-4">
              <h3 class="text-xs font-bold text-gray-400 uppercase tracking-wider mb-2">Pending Creator Withdrawals</h3>
              <div id="withdrawRequestsContainer" class="space-y-3 custom-scrollbar max-h-48 overflow-y-auto"></div>
            </div>
          </div>
        </section>

        <!-- FEED POSTS CONTAINER -->
        <section id="postsFeed" class="space-y-4"></section>
      </div>

      <!-- TAB 2: REELS FEED -->
      <div id="reelsTab" class="hidden space-y-4">
        <div class="flex justify-between items-center">
          <h2 class="text-lg font-bold text-red-400 flex items-center gap-2">
            <i class="fa-solid fa-fire"></i> Prime Reels Feed
          </h2>
          <button onclick="openUploadReelModal()" class="bg-red-600 hover:bg-red-700 text-xs font-bold px-3 py-1.5 rounded-lg flex items-center gap-1">
            <i class="fa-solid fa-plus"></i> Upload Reel
          </button>
        </div>
        <div id="reelsContainer" class="h-[600px] overflow-y-scroll reel-snap rounded-2xl glassmorphism space-y-4 custom-scrollbar p-2"></div>
      </div>
    </main>

    <!-- RIGHT SIDEBAR: PAID MONETIZATION PROMOTIONS -->
    <aside class="hidden md:block col-span-1 space-y-4">
      <div class="glassmorphism p-4 rounded-xl space-y-3 border border-amber-500/30">
        <h3 class="font-bold text-sm text-amber-400 flex items-center gap-1"><i class="fa-solid fa-bullhorn"></i> Paid Ad Booster</h3>
        <p class="text-xs text-gray-300 leading-relaxed">
          Want maximum reach? Boost your posts or reels to appear on top of all users' feeds with paid monetization plans (Starting @ PKR 300).
        </p>
        <button onclick="openBoostInfo()" class="w-full bg-gradient-to-r from-amber-500 to-yellow-600 text-black font-bold py-2 rounded-lg text-xs">Learn More & Boost</button>
      </div>
      <div class="glassmorphism p-4 rounded-xl space-y-2">
        <h3 class="font-bold text-xs text-blue-400 flex items-center gap-1"><i class="fa-solid fa-shield-check"></i> Verified Creator Program</h3>
        <p class="text-[11px] text-gray-400">Get the official blue checkmark badge on your profile and increase user trust.</p>
        <button onclick="openVerifyModal()" class="w-full bg-blue-600 hover:bg-blue-700 text-white font-bold py-1.5 rounded-lg text-xs">Apply Now (Paid)</button>
      </div>
    </aside>
  </div>

  <!-- BOOST POST MODAL -->
  <div id="boostModal" class="fixed inset-0 bg-black/80 hidden items-center justify-center p-4 z-50">
    <div class="glassmorphism max-w-sm w-full p-6 rounded-2xl space-y-4 relative">
      <button onclick="toggleModal('boostModal')" class="absolute top-4 right-4 text-gray-400 hover:text-white"><i class="fa-solid fa-xmark"></i></button>
      <h2 class="text-lg font-bold text-center text-amber-400">Boost Post (Paid Ad)</h2>
      <p class="text-xs text-gray-300 text-center">Select your budget to pin this post on top of user feeds for 24 hours.</p>
      <input id="boostPostKey" type="hidden" />
      <select id="boostPackage" class="w-full bg-gray-900 border border-gray-700 p-2.5 rounded-lg text-xs">
        <option value="300">Basic Boost - PKR 300 (1,000 Impressions)</option>
        <option value="750">Super Boost - PKR 750 (5,000 Impressions)</option>
        <option value="1500">Mega VIP Boost - PKR 1500 (15,000 Impressions)</option>
      </select>
      <button onclick="confirmBoostPost()" class="w-full bg-amber-600 hover:bg-amber-700 py-2.5 rounded-lg text-xs font-bold text-black">Pay & Launch Boost</button>
    </div>
  </div>

  <!-- VERIFIED BADGE MODAL -->
  <div id="verifyModal" class="fixed inset-0 bg-black/80 hidden items-center justify-center p-4 z-50">
    <div class="glassmorphism max-w-sm w-full p-6 rounded-2xl space-y-4 text-center relative">
      <button onclick="toggleModal('verifyModal')" class="absolute top-4 right-4 text-gray-400 hover:text-white"><i class="fa-solid fa-xmark"></i></button>
      <i class="fa-solid fa-certificate text-4xl text-blue-400"></i>
      <h2 class="text-lg font-bold">Get Verified Blue Tick</h2>
      <p class="text-xs text-gray-300">Unlock official credibility on PrimeX for a one-time verification fee of <strong>PKR 999</strong>.</p>
      <button onclick="purchaseVerification()" class="w-full bg-blue-600 hover:bg-blue-700 py-2.5 rounded-lg text-xs font-bold">Pay & Get Verified</button>
    </div>
  </div>

  <!-- SEND GIFT / SUPER THANKS MODAL -->
  <div id="giftModal" class="fixed inset-0 bg-black/80 hidden items-center justify-center p-4 z-50">
    <div class="glassmorphism max-w-sm w-full p-6 rounded-2xl space-y-4 text-center relative">
      <button onclick="toggleModal('giftModal')" class="absolute top-4 right-4 text-gray-400 hover:text-white"><i class="fa-solid fa-xmark"></i></button>
      <i class="fa-solid fa-gift text-4xl text-pink-400"></i>
      <h2 class="text-lg font-bold">Send Creator Gift</h2>
      <p class="text-xs text-gray-300">Support this creator directly from your wallet balance.</p>
      <input id="giftTargetUid" type="hidden" />
      <select id="giftAmount" class="w-full bg-gray-900 border border-gray-700 p-2.5 rounded-lg text-xs">
        <option value="50">Rose (PKR 50)</option>
        <option value="200">Coffee (PKR 200)</option>
        <option value="500">Super Car (PKR 500)</option>
      </select>
      <button onclick="confirmSendGift()" class="w-full bg-pink-600 hover:bg-pink-700 py-2.5 rounded-lg text-xs font-bold">Send Gift Now</button>
    </div>
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
      <h2 class="text-lg font-bold text-center text-amber-400 flex items-center justify-center gap-2"><i class="fa-solid fa-wallet"></i> Wallet & Monetization</h2>
      
      <div class="bg-gray-900 p-4 rounded-xl text-center space-y-1 border border-amber-500/30">
        <p class="text-xs text-gray-400">Available Balance</p>
        <p id="modalUserBalance" class="text-2xl font-extrabold text-amber-400">PKR 0</p>
      </div>

      <div class="space-y-3 text-xs">
        <div>
          <label class="text-gray-400">Select Withdrawal Method</label>
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
          <label class="text-gray-400">Withdraw Amount (Min PKR 500)</label>
          <input id="withdrawAmount" type="number" placeholder="500" class="w-full bg-gray-900 border border-gray-700 p-2.5 rounded-lg mt-1" />
        </div>
        <button onclick="requestWithdrawal()" class="w-full bg-amber-600 hover:bg-amber-700 py-2.5 rounded-lg text-sm font-bold text-black">Request Withdrawal</button>
      </div>
    </div>
  </div>

  <!-- AUTH MODAL -->
  <div id="authModal" class="fixed inset-0 bg-black/80 hidden items-center justify-center p-4 z-50">
    <div class="glassmorphism max-w-md w-full p-6 rounded-2xl space-y-4 relative">
      <button onclick="toggleModal('authModal')" class="absolute top-4 right-4 text-gray-400 hover:text-white"><i class="fa-solid fa-xmark"></i></button>
      <h2 class="text-xl font-bold text-center">Join PrimeX Pro</h2>
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
      <h2 class="text-xl font-bold text-center text-emerald-400">Top-up Wallet (Manual Payment)</h2>
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
        <input id="depositAmount" type="number" placeholder="Amount Sent (PKR)" class="w-full bg-gray-900 border border-gray-700 p-2.5 rounded-lg" />
        <input id="depositTID" type="text" placeholder="Transaction ID (TID)" class="w-full bg-gray-900 border border-gray-700 p-2.5 rounded-lg" />
        <button onclick="submitDeposit()" class="w-full bg-emerald-600 py-2.5 rounded-lg font-bold">Submit Top-up Request</button>
      </div>
    </div>
  </div>

  <!-- FIREBASE LOGIC & PAID FEATURES SCRIPT -->
  <script type="module">
    import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
    import { getAuth, signInWithPopup, GoogleAuthProvider, signInWithEmailAndPassword, createUserWithEmailAndPassword, onAuthStateChanged, signOut } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-auth.js";
    import { getDatabase, ref, push, set, onValue, update, get, remove } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-database.js";

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
        checkVerificationStatus(user.uid);
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

    function loadUserWallet(uid) {
      onValue(ref(db, `wallets/${uid}`), (snapshot) => {
        const bal = snapshot.val()?.balance || 0;
        document.getElementById('navWalletBalance').innerText = `PKR ${bal}`;
        document.getElementById('modalUserBalance').innerText = `PKR ${bal}`;
      });
    }

    function checkVerificationStatus(uid) {
      onValue(ref(db, `verifiedUsers/${uid}`), (snapshot) => {
        if (snapshot.exists() && snapshot.val() === true) {
          document.getElementById('navVerifiedBadge').classList.remove('hidden');
        } else {
          document.getElementById('navVerifiedBadge').classList.add('hidden');
        }
      });
    }

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

    window.submitPost = async () => {
      if (!currentUser) return alert("Please login first, sweetie!");
      const content = document.getElementById('postInput').value;
      if (!content && !selectedMediaBase64) return alert("Add text or media!");

      const isVerifiedSnap = await get(ref(db, `verifiedUsers/${currentUser.uid}`));
      const isVerified = isVerifiedSnap.exists() && isVerifiedSnap.val() === true;

      const postRef = push(ref(db, 'posts'));
      await set(postRef, {
        author: currentUser.displayName || currentUser.email.split('@')[0],
        uid: currentUser.uid,
        isVerified,
        content,
        media: selectedMediaBase64 || null,
        mediaType: selectedMediaType || null,
        likes: 0,
        isBoosted: false,
        timestamp: Date.now()
      });

      document.getElementById('postInput').value = '';
      clearMedia();
      alert("Post published live!");
    };

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
          timestamp: Date.now()
        });
        alert("Reel uploaded successfully!");
        toggleModal('uploadReelModal');
        document.getElementById('reelTitleInput').value = '';
        document.getElementById('reelVideoFile').value = '';
      };
      reader.readAsDataURL(file);
    };

    // PAID FEATURE: Boost Post
    window.openBoostModal = (postKey) => {
      if (!currentUser) return alert("Please login first!");
      document.getElementById('boostPostKey').value = postKey;
      toggleModal('boostModal');
    };

    window.confirmBoostPost = async () => {
      const postKey = document.getElementById('boostPostKey').value;
      const cost = parseFloat(document.getElementById('boostPackage').value);
      
      const walletRef = ref(db, `wallets/${currentUser.uid}/balance`);
      const snap = await get(walletRef);
      const currentBal = snap.exists() ? snap.val() : 0;

      if (currentBal < cost) return alert("Insufficient balance! Please top up your wallet first.");

      await set(walletRef, currentBal - cost);
      await update(ref(db, `posts/${postKey}`), { isBoosted: true });
      toggleModal('boostModal');
      alert("Success! Your post has been boosted and pinned on top.");
    };

    // PAID FEATURE: Verified Badge Purchase
    window.purchaseVerification = async () => {
      if (!currentUser) return alert("Please login first!");
      const cost = 999;
      const walletRef = ref(db, `wallets/${currentUser.uid}/balance`);
      const snap = await get(walletRef);
      const currentBal = snap.exists() ? snap.val() : 0;

      if (currentBal < cost) return alert("Insufficient balance! Verification costs PKR 999.");

      await set(walletRef, currentBal - cost);
      await set(ref(db, `verifiedUsers/${currentUser.uid}`), true);
      toggleModal('verifyModal');
      alert("Congratulations! You are now a Verified Creator with a Blue Tick.");
    };

    // PAID FEATURE: Send Gift to Creator
    window.openGiftModal = (authorUid) => {
      if (!currentUser) return alert("Please login first!");
      if (currentUser.uid === authorUid) return alert("You cannot send gifts to yourself!");
      document.getElementById('giftTargetUid').value = authorUid;
      toggleModal('giftModal');
    };

    window.confirmSendGift = async () => {
      const targetUid = document.getElementById('giftTargetUid').value;
      const giftCost = parseFloat(document.getElementById('giftAmount').value);

      const senderWalletRef = ref(db, `wallets/${currentUser.uid}/balance`);
      const senderSnap = await get(senderWalletRef);
      const senderBal = senderSnap.exists() ? senderSnap.val() : 0;

      if (senderBal < giftCost) return alert("Insufficient balance in your wallet!");

      // Deduct from sender, add to receiver
      await set(senderWalletRef, senderBal - giftCost);
      const receiverWalletRef = ref(db, `wallets/${targetUid}/balance`);
      const receiverSnap = await get(receiverWalletRef);
      const receiverBal = receiverSnap.exists() ? receiverSnap.val() : 0;
      await set(receiverWalletRef, receiverBal + giftCost);

      toggleModal('giftModal');
      alert("Gift sent successfully to the creator!");
    };

    // Manual Deposit
    window.submitDeposit = async () => {
      if (!currentUser) return;
      const method = document.getElementById('depositMethod').value;
      const amount = parseFloat(document.getElementById('depositAmount').value);
      const tid = document.getElementById('depositTID').value;
      if (!amount || !tid) return alert("Please fill all details!");

      const refReq = push(ref(db, 'deposits'));
      await set(refReq, {
        id: refReq.key,
        uid: currentUser.uid,
        email: currentUser.email,
        method,
        amount,
        tid,
        status: 'pending',
        timestamp: Date.now()
      });
      toggleModal('depositModal');
      alert("Top-up request submitted! Admin will verify and credit your wallet within 15 minutes.");
    };

    // Feed Render with Boost & Verified Badges
    onValue(ref(db, 'posts'), (snapshot) => {
      const feed = document.getElementById('postsFeed'); feed.innerHTML = '';
      const data = snapshot.val(); if (!data) return;
      
      const postsArray = Object.entries(data);
      postsArray.sort((a, b) => (b[1].isBoosted ? 1 : 0) - (a[1].isBoosted ? 1 : 0));

      postsArray.forEach(([key, post]) => {
        const el = document.createElement('div');
        el.className = `glassmorphism p-4 rounded-xl space-y-3 ${post.isBoosted ? 'border border-amber-500/50 bg-amber-950/10' : ''}`;
        el.innerHTML = `
          ${post.isBoosted ? '<span class="text-[10px] bg-amber-500 text-black font-bold px-2 py-0.5 rounded uppercase"><i class="fa-solid fa-bullhorn"></i> Sponsored Ad / Boosted</span>' : ''}
          <div class="flex justify-between items-center">
            <div class="flex items-center space-x-2">
              <div class="w-8 h-8 rounded-full bg-gradient-to-tr from-blue-500 to-purple-500 flex items-center justify-center font-bold text-xs">${post.author.charAt(0).toUpperCase()}</div>
              <div>
                <p class="text-sm font-bold flex items-center gap-1">
                  ${post.author} 
                  ${post.isVerified ? '<span class="text-blue-400 text-xs"><i class="fa-solid fa-circle-check"></i></span>' : ''}
                </p>
                <p class="text-[10px] text-gray-500">${new Date(post.timestamp).toLocaleTimeString()}</p>
              </div>
            </div>
            ${currentUser && currentUser.uid === post.uid && !post.isBoosted ? `<button onclick="openBoostModal('${key}')" class="text-[10px] bg-amber-600 hover:bg-amber-700 text-black font-bold px-2.5 py-1 rounded-lg">Boost Post</button>` : ''}
          </div>
          <p class="text-sm text-gray-300">${post.content}</p>
          ${post.media && post.mediaType === 'image' ? `<img src="${post.media}" class="w-full h-64 object-cover rounded-lg" />` : ''}
          ${post.media && post.mediaType === 'video' ? `<video src="${post.media}" controls class="w-full h-64 object-cover rounded-lg"></video>` : ''}
          <div class="flex justify-between items-center text-xs text-gray-400 pt-2 border-t border-gray-800">
            <span>${post.likes || 0} Likes</span>
            ${currentUser && currentUser.uid !== post.uid ? `<button onclick="openGiftModal('${post.uid}')" class="text-pink-400 font-bold hover:underline flex items-center gap-1"><i class="fa-solid fa-gift"></i> Send Gift</button>` : ''}
          </div>
        `;
        feed.appendChild(el);
      });
    });

    // Reels Render
    onValue(ref(db, 'reels'), (snapshot) => {
      const container = document.getElementById('reelsContainer'); container.innerHTML = '';
      const data = snapshot.val(); if (!data) { container.innerHTML = `<p class="text-xs text-center text-gray-500 py-20">No reels uploaded yet.</p>`; return; }
      Object.values(data).reverse().forEach(reel => {
        const div = document.createElement('div');
        div.className = "reel-card relative h-full bg-black rounded-xl overflow-hidden flex items-center justify-center border border-gray-800";
        div.innerHTML = `
          <video src="${reel.videoBase64}" autoplay loop muted class="w-full h-full object-cover"></video>
          <div class="absolute bottom-4 left-4 space-y-1">
            <p class="font-bold text-sm text-white">${reel.author}</p>
            <p class="text-xs text-gray-300">${reel.title}</p>
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
      // Load Deposits
      onValue(ref(db, 'deposits'), (snapshot) => {
        const container = document.getElementById('depositRequestsContainer'); container.innerHTML = '';
        const data = snapshot.val(); if (!data) return;
        Object.entries(data).reverse().forEach(([key, item]) => {
          if (item.status === 'pending') {
            const div = document.createElement('div');
            div.className = "p-3 bg-gray-900 rounded-lg border border-gray-800 flex justify-between items-center text-xs";
            div.innerHTML = `
              <div>
                <p class="font-bold">${item.email}</p>
                <p class="text-green-400">${item.method}: PKR ${item.amount} (TID: ${item.tid})</p>
              </div>
              <div class="flex gap-2">
                <button onclick="approveDeposit('${key}', '${item.uid}', ${item.amount})" class="bg-green-600 px-2 py-1 rounded text-white font-bold">Approve</button>
                <button onclick="rejectDeposit('${key}')" class="bg-red-600 px-2 py-1 rounded text-white">Reject</button>
              </div>
            `;
            container.appendChild(div);
          }
        });
      });
      // Load Withdrawals
      onValue(ref(db, 'withdrawals'), (snapshot) => {
        const container = document.getElementById('withdrawRequestsContainer'); container.innerHTML = '';
        const data = snapshot.val(); if (!data) return;
        Object.entries(data).reverse().forEach(([key, item]) => {
          if (item.status === 'pending') {
            const div = document.createElement('div');
            div.className = "p-3 bg-gray-900 rounded-lg border border-gray-800 flex justify-between items-center text-xs";
            div.innerHTML = `
              <div>
                <p class="font-bold">${item.userEmail}</p>
                <p class="text-amber-400">${item.method}: PKR ${item.amount} (${item.account})</p>
              </div>
              <div class="flex gap-2">
                <button onclick="approveWithdrawal('${key}')" class="bg-green-600 px-2 py-1 rounded text-white font-bold">Mark Paid</button>
                <button onclick="rejectWithdrawal('${key}', '${item.uid}', ${item.amount})" class="bg-red-600 px-2 py-1 rounded text-white">Refund & Reject</button>
              </div>
            `;
            container.appendChild(div);
          }
        });
      });
    }

    window.approveDeposit = async (depKey, targetUid, amount) => {
      const walletRef = ref(db, `wallets/${targetUid}/balance`);
      const snap = await get(walletRef);
      const currentBal = snap.exists() ? snap.val() : 0;
      await set(walletRef, currentBal + amount);
      await update(ref(db, `deposits/${depKey}`), { status: 'approved' });
      alert("Top-up approved and credited!");
    };

    window.rejectDeposit = async (depKey) => {
      await update(ref(db, `deposits/${depKey}`), { status: 'rejected' });
      alert("Deposit request rejected.");
    };

    window.approveWithdrawal = async (witKey) => {
      await update(ref(db, `withdrawals/${witKey}`), { status: 'paid' });
      alert("Withdrawal marked as paid!");
    };

    window.rejectWithdrawal = async (witKey, targetUid, amount) => {
      const walletRef = ref(db, `wallets/${targetUid}/balance`);
      const snap = await get(walletRef);
      const currentBal = snap.exists() ? snap.val() : 0;
      await set(walletRef, currentBal + amount);
      await update(ref(db, `withdrawals/${witKey}`), { status: 'rejected' });
      alert("Withdrawal rejected and funds refunded to user wallet.");
    };

    window.requestWithdrawal = async () => {
      if (!currentUser) return;
      const method = document.getElementById('withdrawMethod').value;
      const account = document.getElementById('withdrawAccount').value;
      const amount = parseFloat(document.getElementById('withdrawAmount').value);
      if (!account || !amount || amount < 500) return alert("Minimum withdrawal is PKR 500!");

      const walletRef = ref(db, `wallets/${currentUser.uid}/balance`);
      const snap = await get(walletRef);
      const currentBal = snap.exists() ? snap.val() : 0;
      if (currentBal < amount) return alert("Insufficient balance!");

      await set(walletRef, currentBal - amount);
      const reqRef = push(ref(db, 'withdrawals'));
      await set(reqRef, { uid: currentUser.uid, userEmail: currentUser.email, method, account, amount, status: 'pending', timestamp: Date.now() });
      alert("Withdrawal requested successfully!");
      toggleModal('walletModal');
    };
  </script>

  <script>
    function toggleModal(id) { const el = document.getElementById(id); el.classList.toggle('hidden'); el.classList.toggle('flex'); }
    function openDepositModal() { toggleModal('depositModal'); }
    function openWalletModal() { toggleModal('walletModal'); }
    function openUploadReelModal() { toggleModal('uploadReelModal'); }
    function openVerifyModal() { toggleModal('verifyModal'); }
    function openBoostInfo() { alert("Boost Feature: Pay a small fee to pin your post on top of everyone's feed for maximum views!"); }
    function switchTab(tab) {
      if (tab === 'feed') { document.getElementById('feedTab').classList.remove('hidden'); document.getElementById('reelsTab').classList.add('hidden'); }
      else { document.getElementById('feedTab').classList.add('hidden'); document.getElementById('reelsTab').classList.remove('hidden'); }
    }
  </script>
</body>
</html>
