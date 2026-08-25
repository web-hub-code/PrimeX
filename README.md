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
      <h1 class="text-2xl font-extrabold tracking-wider bg-gradient-to-r from-blue-500 via-indigo-500 to-purple-500 bg-clip-text text-transparent">
        PrimeX
      </h1>
    </div>
    <div id="authNavButtons" class="flex items-center space-x-3">
      <button onclick="toggleModal('authModal')" class="bg-blue-600 hover:bg-blue-700 text-sm font-semibold px-4 py-2 rounded-lg transition">Login / Register</button>
    </div>
    <div id="userNavProfile" class="hidden flex items-center space-x-4">
      <button onclick="openDepositModal()" class="bg-gradient-to-r from-green-500 to-emerald-600 text-xs font-bold px-3 py-2 rounded-lg hover:opacity-90 flex items-center gap-1">
        <i class="fa-solid font-bold fa-wallet"></i> Deposit
      </button>
      <button id="eagleEyeBtn" onclick="toggleAdminPanel()" class="hidden bg-purple-600 hover:bg-purple-700 text-xs font-bold px-3 py-2 rounded-lg flex items-center gap-1">
        <i class="fa-solid fa-eye"></i> EagleEye
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
          <i class="fa-solid fa-fire text-red-500 text-lg"></i> <span class="font-medium">Trending</span>
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
        <textarea id="postInput" rows="2" placeholder="What's happening on PrimeX?" class="w-full bg-gray-900 border border-gray-700 rounded-lg p-3 text-sm focus:outline-none focus:border-blue-500 resize-none"></textarea>
        <div class="flex justify-between items-center pt-2">
          <div class="flex space-x-3 text-gray-400">
            <button class="hover:text-blue-400"><i class="fa-regular fa-image"></i></button>
            <button class="hover:text-purple-400"><i class="fa-solid fa-video"></i></button>
          </div>
          <button onclick="submitPost()" class="bg-blue-600 hover:bg-blue-700 text-xs font-bold px-4 py-2 rounded-lg">Post</button>
        </div>
      </div>

      <!-- EAGLE EYE ADMIN PANEL (HIDDEN BY DEFAULT) -->
      <section id="eagleEyePanel" class="hidden glassmorphism p-5 rounded-xl border border-purple-500/30 space-y-4">
        <div class="flex justify-between items-center border-b border-gray-800 pb-3">
          <h2 class="text-lg font-bold text-purple-400 flex items-center gap-2">
            <i class="fa-solid fa-eye"></i> EagleEye Administration
          </h2>
          <span class="text-xs bg-purple-900/50 text-purple-300 px-2.5 py-1 rounded-full border border-purple-700">Live Oversight</span>
        </div>
        <div id="depositRequestsContainer" class="space-y-3 custom-scrollbar max-h-96 overflow-y-auto">
          <p class="text-gray-400 text-xs">Loading deposit requests...</p>
        </div>
      </section>

      <!-- FEED POSTS CONTAINER -->
      <section id="postsFeed" class="space-y-4">
        <!-- Posts dynamically rendered here -->
      </section>
    </main>

    <!-- RIGHT SIDEBAR -->
    <aside class="hidden md:block col-span-1 space-y-4">
      <div class="glassmorphism p-4 rounded-xl">
        <h3 class="font-bold text-sm text-gray-400 mb-3">Notice Board</h3>
        <p class="text-xs text-gray-300 leading-relaxed">
          Welcome to <strong class="text-blue-400">PrimeX</strong>. Deposit approval process takes 5–15 minutes after submission. Always re-check Payment TIDs!
        </p>
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

  <!-- DEPOSIT MODAL (MANUAL PAYMENT SYSTEM) -->
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

  <!-- FIREBASE MODULE & LOGIC -->
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

    // Set global admin emails (Add your email here)
    const ADMIN_EMAILS = ["admin@primex.com"];

    let currentUser = null;

    // Authentication Listeners
    onAuthStateChanged(auth, (user) => {
      currentUser = user;
      if (user) {
        document.getElementById('authNavButtons').classList.add('hidden');
        document.getElementById('userNavProfile').classList.remove('hidden');
        document.getElementById('navUserName').innerText = user.displayName || user.email.split('@')[0];
        
        // Admin privilege check
        if (ADMIN_EMAILS.includes(user.email)) {
          document.getElementById('eagleEyeBtn').classList.remove('hidden');
          listenToEagleEye();
        }
      } else {
        document.getElementById('authNavButtons').classList.remove('hidden');
        document.getElementById('userNavProfile').classList.add('hidden');
        document.getElementById('eagleEyeBtn').classList.add('hidden');
      }
    });

    // Auth Functions
    window.loginWithGoogle = async () => {
      try {
        await signInWithPopup(auth, googleProvider);
        toggleModal('authModal');
      } catch (err) { alert(err.message); }
    };

    window.loginWithEmail = async () => {
      const email = document.getElementById('authEmail').value;
      const pass = document.getElementById('authPassword').value;
      if (!email || !pass) return alert("Please fill credentials");
      try {
        await signInWithEmailAndPassword(auth, email, pass);
        toggleModal('authModal');
      } catch (err) {
        // Auto sign up if user doesn't exist
        try {
          await createUserWithEmailAndPassword(auth, email, pass);
          toggleModal('authModal');
        } catch (e) { alert(e.message); }
      }
    };

    window.logout = () => signOut(auth);

    // Deposit Submission System (Base64 Proof Processing)
    window.submitDeposit = async () => {
      if (!currentUser) return alert("Please login first, sweetie!");
      
      const method = document.getElementById('depositMethod').value;
      const amount = document.getElementById('depositAmount').value;
      const tid = document.getElementById('depositTID').value;
      const fileInput = document.getElementById('depositProof');

      if (!amount || !tid || !fileInput.files[0]) return alert("All deposit fields & proof image are required!");

      const file = fileInput.files[0];
      const reader = new FileReader();

      reader.onloadend = async () => {
        const base64Image = reader.result;
        const newDepositRef = push(ref(db, 'deposits'));
        await set(newDepositRef, {
          id: newDepositRef.key,
          uid: currentUser.uid,
          userEmail: currentUser.email,
          method: method,
          amount: amount,
          tid: tid,
          proofBase64: base64Image,
          status: 'pending',
          timestamp: Date.now()
        });

        alert("Deposit submitted! Admin will verify soon.");
        toggleModal('depositModal');
      };

      reader.readAsDataURL(file);
    };

    // EagleEye Admin Realtime Stream & Actions
    function listenToEagleEye() {
      onValue(ref(db, 'deposits'), (snapshot) => {
        const container = document.getElementById('depositRequestsContainer');
        container.innerHTML = '';
        const data = snapshot.val();
        
        if (!data) {
          container.innerHTML = `<p class="text-xs text-gray-500">No deposit logs found.</p>`;
          return;
        }

        Object.values(data).reverse().forEach((item) => {
          const card = document.createElement('div');
          card.className = "p-3 bg-gray-900/90 rounded-lg border border-gray-800 space-y-2 text-xs";
          card.innerHTML = `
            <div class="flex justify-between items-start">
              <div>
                <p class="font-bold text-gray-200">${item.userEmail}</p>
                <p class="text-gray-400">${item.method} • <span class="text-emerald-400 font-bold">PKR ${item.amount}</span></p>
                <p class="text-gray-400 font-mono">TID: ${item.tid}</p>
              </div>
              <span class="px-2 py-0.5 rounded text-[10px] uppercase font-bold ${
                item.status === 'approved' ? 'bg-green-900/40 text-green-400 border border-green-800' :
                item.status === 'rejected' ? 'bg-red-900/40 text-red-400 border border-red-800' :
                'bg-yellow-900/40 text-yellow-400 border border-yellow-800'
              }">${item.status}</span>
            </div>
            ${item.proofBase64 ? `<img src="${item.proofBase64}" class="w-full h-24 object-cover rounded border border-gray-800" />` : ''}
            ${item.status === 'pending' ? `
              <div class="flex space-x-2 pt-1">
                <button onclick="updateDepositStatus('${item.id}', 'approved')" class="flex-1 bg-green-600 hover:bg-green-700 py-1 rounded font-bold text-white">Approve</button>
                <button onclick="updateDepositStatus('${item.id}', 'rejected')" class="flex-1 bg-red-600 hover:bg-red-700 py-1 rounded font-bold text-white">Reject</button>
              </div>
            ` : ''}
          `;
          container.appendChild(card);
        });
      });
    }

    window.updateDepositStatus = async (id, status) => {
      await update(ref(db, `deposits/${id}`), { status: status });
    };

    // Feed Post Actions
    window.submitPost = async () => {
      if (!currentUser) return alert("Please login to post!");
      const text = document.getElementById('postInput').value;
      if (!text) return;

      const postRef = push(ref(db, 'posts'));
      await set(postRef, {
        author: currentUser.displayName || currentUser.email.split('@')[0],
        content: text,
        timestamp: Date.now()
      });

      document.getElementById('postInput').value = '';
    };

    // Realtime Posts Stream
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
            <div>
              <p class="text-sm font-bold">${post.author}</p>
              <p class="text-[10px] text-gray-500">${new Date(post.timestamp).toLocaleTimeString()}</p>
            </div>
          </div>
          <p class="text-sm text-gray-300 leading-normal">${post.content}</p>
        `;
        feed.appendChild(el);
      });
    });
  </script>

  <script>
    // Modal Helpers
    function toggleModal(id) {
      const el = document.getElementById(id);
      el.classList.toggle('hidden');
      el.classList.toggle('flex');
    }
    function openDepositModal() { toggleModal('depositModal'); }
    function toggleAdminPanel() {
      const panel = document.getElementById('eagleEyePanel');
      panel.classList.toggle('hidden');
    }
  </script>
</body>
</html>
