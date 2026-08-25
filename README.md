<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>PrimeX - NextGen Social Network</title>
  <!-- Tailwind CSS -->
  <script src="https://cdn.tailwindcss.com"></script>
  <!-- FontAwesome -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css"/>
  <style>
    body { background-color: #0b0f19; color: #f3f4f6; font-family: 'Inter', sans-serif; }
    .glassmorphism { background: rgba(17, 24, 39, 0.7); backdrop-filter: blur(12px); border: 1px solid rgba(255, 255, 255, 0.08); }
    .custom-scrollbar::-webkit-scrollbar { width: 6px; }
    .custom-scrollbar::-webkit-scrollbar-thumb { background: #374151; border-radius: 4px; }
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
    <div id="userNavProfile" class="hidden flex items-center space-x-4">
      <button onclick="openDepositModal()" class="bg-gradient-to-r from-green-500 to-emerald-600 text-xs font-bold px-3 py-2 rounded-lg hover:opacity-90 flex items-center gap-1">
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
        <a href="#" class="flex items-center space-x-3 text-gray-300 hover:text-white p-2 rounded-lg hover:bg-gray-800/50 transition">
          <i class="fa-solid fa-house text-blue-500 text-lg"></i> <span class="font-medium">Feed</span>
        </a>
        <a href="#" class="flex items-center space-x-3 text-gray-300 hover:text-white p-2 rounded-lg hover:bg-gray-800/50 transition">
          <i class="fa-solid fa-video text-red-500 text-lg"></i> <span class="font-medium">Reels / TikTok</span>
        </a>
        <a href="#" class="flex items-center space-x-3 text-gray-300 hover:text-white p-2 rounded-lg hover:bg-gray-800/50 transition">
          <i class="fa-solid fa-wallet text-emerald-500 text-lg"></i> <span class="font-medium">Wallet & Funds</span>
        </a>
      </div>
    </aside>

    <!-- CENTER FEED & POST CREATOR -->
    <main class="col-span-1 md:col-span-2 space-y-6">
      
      <!-- CREATE POST BOX -->
      <div class="glassmorphism p-4 rounded-xl space-y-3">
        <textarea id="postInput" rows="2" placeholder="What's happening on PrimeX, sweetie?" class="w-full bg-gray-900 border border-gray-700 rounded-lg p-3 text-sm focus:outline-none focus:border-blue-500 resize-none"></textarea>
        <div class="flex justify-between items-center pt-2">
          <div class="flex space-x-3 text-gray-400">
            <button class="hover:text-blue-400"><i class="fa-regular fa-image"></i></button>
            <button class="hover:text-purple-400"><i class="fa-solid fa-video"></i></button>
          </div>
          <button onclick="submitPost()" class="bg-blue-600 hover:bg-blue-700 text-xs font-bold px-4 py-2 rounded-lg">Post</button>
        </div>
      </div>

      <!-- EAGLE EYE ADMIN PANEL (HIDDEN UNLESS UNLOCKED VIA 5 TAPS + KEY 5426) -->
      <section id="eagleEyePanel" class="hidden glassmorphism p-5 rounded-xl border border-purple-500/30 space-y-6">
        <div class="flex justify-between items-center border-b border-gray-800 pb-3">
          <h2 class="text-lg font-bold text-purple-400 flex items-center gap-2">
            <i class="fa-solid fa-shield-halved"></i> EagleEye Admin Master Control
          </h2>
          <button onclick="lockAdminPanel()" class="text-xs bg-red-900/40 text-red-400 border border-red-700 px-2.5 py-1 rounded-lg">Lock Panel</button>
        </div>

        <!-- Sub Tabs inside Admin Panel -->
        <div class="space-y-4">
          <div>
            <h3 class="text-xs font-bold text-gray-400 uppercase tracking-wider mb-2">Pending Deposit Requests</h3>
            <div id="depositRequestsContainer" class="space-y-3 custom-scrollbar max-h-60 overflow-y-auto">
              <p class="text-gray-400 text-xs">Loading deposits...</p>
            </div>
          </div>

          <div class="border-t border-gray-800 pt-4">
            <h3 class="text-xs font-bold text-gray-400 uppercase tracking-wider mb-2">Registered Users Database</h3>
            <div id="adminUsersContainer" class="space-y-2 custom-scrollbar max-h-60 overflow-y-auto">
              <!-- Users list rendered dynamically -->
            </div>
          </div>
        </div>
      </section>

      <!-- FEED POSTS CONTAINER -->
      <section id="postsFeed" class="space-y-4">
        <!-- Posts dynamically rendered here -->
      </section>
    </main>

    <!-- RIGHT SIDEBAR -->
    <aside class="hidden md:block col-span-1 space-y-4">
      <div class="glassmorphism p-4 rounded-xl space-y-3">
        <h3 class="font-bold text-sm text-gray-400">Trending Topics</h3>
        <div class="space-y-2 text-xs">
          <p class="text-blue-400 font-semibold">#PrimeXLaunch</p>
          <p class="text-gray-300">#EasyPaisaJazzCash</p>
          <p class="text-gray-300">#NextGenSocial</p>
        </div>
      </div>
    </aside>
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
        <div class="relative flex py-2 items-center">
          <div class="flex-grow border-t border-gray-700"></div>
          <span class="flex-shrink mx-4 text-xs text-gray-400">OR</span>
          <div class="flex-grow border-t border-gray-700"></div>
        </div>
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
      <p class="text-xs text-gray-400">Enter master access key to open admin control panel.</p>
      <input id="adminKeyInput" type="password" placeholder="Enter Key (e.g. 5426)" class="w-full bg-gray-900 border border-gray-700 p-2.5 rounded-lg text-center tracking-widest text-sm focus:outline-none focus:border-purple-500" />
      <div class="flex space-x-2">
        <button onclick="verifyAdminKey()" class="flex-1 bg-purple-600 hover:bg-purple-700 py-2 rounded-lg text-xs font-bold">Unlock</button>
        <button onclick="toggleModal('adminKeyModal')" class="flex-1 bg-gray-800 hover:bg-gray-700 py-2 rounded-lg text-xs">Cancel</button>
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
        <div>
          <label class="text-xs text-gray-400">Select Gateway</label>
          <select id="depositMethod" class="w-full bg-gray-900 border border-gray-700 p-2.5 rounded-lg mt-1 focus:outline-none">
            <option value="EasyPaisa">EasyPaisa (03379827882)</option>
            <option value="JazzCash">JazzCash (03705519562)</option>
          </select>
        </div>
        <div>
          <label class="text-xs text-gray-400">Amount (PKR)</label>
          <input id="depositAmount" type="number" placeholder="e.g. 1000" class="w-full bg-gray-900 border border-gray-700 p-2.5 rounded-lg mt-1 focus:outline-none" />
        </div>
        <div>
          <label class="text-xs text-gray-400">Transaction ID (TID)</label>
          <input id="depositTID" type="text" placeholder="Enter 11-12 digit TID" class="w-full bg-gray-900 border border-gray-700 p-2.5 rounded-lg mt-1 focus:outline-none" />
        </div>
        <div>
          <label class="text-xs text-gray-400">Payment Screenshot Proof</label>
          <input id="depositProof" type="file" accept="image/*" class="w-full bg-gray-900 border border-gray-700 p-2 rounded-lg mt-1 text-xs text-gray-400" />
        </div>
        <button onclick="submitDeposit()" class="w-full bg-gradient-to-r from-emerald-600 to-green-600 hover:opacity-90 py-2.5 rounded-lg text-sm font-bold">Submit Payment Verification</button>
      </div>
    </div>
  </div>

  <!-- FIREBASE LOGIC -->
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

        // Track user registration in DB
        set(ref(db, `users/${user.uid}`), {
          email: user.email,
          name: user.displayName || user.email.split('@')[0],
          lastLogin: Date.now(),
          status: 'active'
        });
      } else {
        document.getElementById('authNavButtons').classList.remove('hidden');
        document.getElementById('userNavProfile').classList.add('hidden');
      }
    });

    window.loginWithGoogle = async () => {
      try { await signInWithPopup(auth, googleProvider); toggleModal('authModal'); } catch (err) { alert(err.message); }
    };

    window.loginWithEmail = async () => {
      const email = document.getElementById('authEmail').value;
      const pass = document.getElementById('authPassword').value;
      if (!email || !pass) return alert("Please fill credentials");
      try {
        await signInWithEmailAndPassword(auth, email, pass);
        toggleModal('authModal');
      } catch (err) {
        try { await createUserWithEmailAndPassword(auth, email, pass); toggleModal('authModal'); } catch (e) { alert(e.message); }
      }
    };

    window.logout = () => signOut(auth);

    // Manual Deposit System
    window.submitDeposit = async () => {
      if (!currentUser) return alert("Please login first, sweetie!");
      const method = document.getElementById('depositMethod').value;
      const amount = document.getElementById('depositAmount').value;
      const tid = document.getElementById('depositTID').value;
      const fileInput = document.getElementById('depositProof');

      if (!amount || !tid || !fileInput.files[0]) return alert("All fields & proof are required!");

      const reader = new FileReader();
      reader.onloadend = async () => {
        const newRef = push(ref(db, 'deposits'));
        await set(newRef, {
          id: newRef.key,
          uid: currentUser.uid,
          userEmail: currentUser.email,
          method, amount, tid,
          proofBase64: reader.result,
          status: 'pending',
          timestamp: Date.now()
        });
        alert("Deposit submitted successfully!");
        toggleModal('depositModal');
      };
      reader.readAsDataURL(fileInput.files[0]);
    };

    // Secret Tap Counter logic for Logo
    let tapCount = 0;
    let tapTimer = null;
    window.handleLogoTap = () => {
      tapCount++;
      clearTimeout(tapTimer);
      tapTimer = setTimeout(() => { tapCount = 0; }, 1000); // Reset within 1 sec

      if (tapCount >= 5) {
        tapCount = 0;
        toggleModal('adminKeyModal');
      }
    };

    window.verifyAdminKey = () => {
      const key = document.getElementById('adminKeyInput').value;
      if (key === "5426") {
        toggleModal('adminKeyModal');
        document.getElementById('eagleEyePanel').classList.remove('hidden');
        loadEagleEyeData();
        alert("EagleEye Admin Panel Unlocked Successfully!");
      } else {
        alert("Invalid Security Key!");
      }
    };

    window.lockAdminPanel = () => {
      document.getElementById('eagleEyePanel').classList.add('hidden');
    };

    function loadEagleEyeData() {
      // Load Deposits
      onValue(ref(db, 'deposits'), (snapshot) => {
        const container = document.getElementById('depositRequestsContainer');
        container.innerHTML = '';
        const data = snapshot.val();
        if (!data) { container.innerHTML = `<p class="text-xs text-gray-500">No deposits found.</p>`; return; }

        Object.values(data).reverse().forEach((item) => {
          const div = document.createElement('div');
          div.className = "p-3 bg-gray-900 rounded-lg border border-gray-800 space-y-2 text-xs";
          div.innerHTML = `
            <div class="flex justify-between">
              <div><p class="font-bold">${item.userEmail}</p><p class="text-emerald-400">${item.method}: PKR ${item.amount}</p><p class="font-mono text-gray-400">TID: ${item.tid}</p></div>
              <span class="px-2 py-0.5 rounded text-[10px] font-bold uppercase ${item.status === 'approved' ? 'bg-green-900/40 text-green-400' : item.status === 'rejected' ? 'bg-red-900/40 text-red-400' : 'bg-yellow-900/40 text-yellow-400'}">${item.status}</span>
            </div>
            ${item.proofBase64 ? `<img src="${item.proofBase64}" class="w-full h-20 object-cover rounded" />` : ''}
            ${item.status === 'pending' ? `<div class="flex space-x-2"><button onclick="updateStatus('${item.id}', 'approved')" class="flex-1 bg-green-600 py-1 rounded text-white font-bold">Approve</button><button onclick="updateStatus('${item.id}', 'rejected')" class="flex-1 bg-red-600 py-1 rounded text-white font-bold">Reject</button></div>` : ''}
          `;
          container.appendChild(div);
        });
      });

      // Load Users Database
      onValue(ref(db, 'users'), (snapshot) => {
        const container = document.getElementById('adminUsersContainer');
        container.innerHTML = '';
        const data = snapshot.val();
        if (!data) return;

        Object.entries(data).forEach(([uid, user]) => {
          const div = document.createElement('div');
          div.className = "p-2.5 bg-gray-900 rounded-lg border border-gray-800 flex justify-between items-center text-xs";
          div.innerHTML = `
            <div><p class="font-bold text-gray-200">${user.name}</p><p class="text-gray-400">${user.email}</p></div>
            <span class="text-emerald-400 font-semibold uppercase text-[10px] bg-emerald-950 px-2 py-0.5 rounded">${user.status || 'Active'}</span>
          `;
          container.appendChild(div);
        });
      });
    }

    window.updateStatus = async (id, status) => {
      await update(ref(db, `deposits/${id}`), { status });
    };

    // Posts Feed System
    window.submitPost = async () => {
      if (!currentUser) return alert("Please login first!");
      const content = document.getElementById('postInput').value;
      if (!content) return;

      const postRef = push(ref(db, 'posts'));
      await set(postRef, { author: currentUser.displayName || currentUser.email.split('@')[0], content, timestamp: Date.now() });
      document.getElementById('postInput').value = '';
    };

    onValue(ref(db, 'posts'), (snapshot) => {
      const feed = document.getElementById('postsFeed');
      feed.innerHTML = '';
      const data = snapshot.val();
      if (!data) return;

      Object.values(data).reverse().forEach((post) => {
        const el = document.createElement('div');
        el.className = 'glassmorphism p-4 rounded-xl space-y-2';
        el.innerHTML = `
          <div class="flex items-center space-x-2">
            <div class="w-8 h-8 rounded-full bg-gradient-to-tr from-blue-500 to-purple-500 flex items-center justify-center font-bold text-xs">
              ${post.author.charAt(0).toUpperCase()}
            </div>
            <div><p class="text-sm font-bold">${post.author}</p><p class="text-[10px] text-gray-500">${new Date(post.timestamp).toLocaleTimeString()}</p></div>
          </div>
          <p class="text-sm text-gray-300">${post.content}</p>
        `;
        feed.appendChild(el);
      });
    });
  </script>

  <script>
    function toggleModal(id) {
      const el = document.getElementById(id);
      el.classList.toggle('hidden');
      el.classList.toggle('flex');
    }
    function openDepositModal() { toggleModal('depositModal'); }
  </script>
</body>
</html>
