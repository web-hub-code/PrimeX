<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>PrimeX Pro - Complete Social Network</title>
  <!-- Tailwind CSS -->
  <script src="https://cdn.tailwindcss.com"></script>
  <!-- FontAwesome -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css"/>
  <style>
    body { background-color: #0b0f19; color: #f3f4f6; font-family: 'Inter', sans-serif; }
    .glassmorphism { background: rgba(17, 24, 39, 0.7); backdrop-filter: blur(12px); border: 1px solid rgba(255, 255, 255, 0.08); }
    .custom-scrollbar::-webkit-scrollbar { width: 5px; height: 5px; }
    .custom-scrollbar::-webkit-scrollbar-thumb { background: #374151; border-radius: 4px; }
    .reel-snap { scroll-snap-type: y mandatory; }
    .reel-card { scroll-snap-align: start; }
  </style>
</head>
<body class="custom-scrollbar">

  <!-- TOP NAVIGATION BAR -->
  <nav class="sticky top-0 z-40 glassmorphism border-b border-gray-800 px-4 py-3 flex justify-between items-center">
    <div class="flex items-center space-x-3">
      <h1 id="secretLogoBtn" onclick="handleLogoTap()" class="cursor-pointer text-2xl font-extrabold tracking-wider bg-gradient-to-r from-blue-500 via-indigo-500 to-purple-500 bg-clip-text text-transparent select-none">
        PrimeX <span class="text-[10px] bg-amber-500 text-black px-1.5 py-0.5 rounded font-bold uppercase">Pro Ultimate</span>
      </h1>
    </div>

    <!-- NOTIFICATIONS & MESSAGES NAV ICONS -->
    <div id="userNavProfile" class="hidden flex items-center space-x-3">
      <!-- NOTIFICATIONS ICON -->
      <div class="relative">
        <button onclick="toggleNotificationsMenu()" class="p-2 text-gray-300 hover:text-white rounded-full hover:bg-gray-800 transition relative">
          <i class="fa-solid fa-bell text-lg"></i>
          <span id="notifBadge" class="hidden absolute top-0 right-0 bg-red-600 text-[10px] font-bold text-white rounded-full w-4 h-4 flex items-center justify-center">0</span>
        </button>
        <!-- NOTIFICATIONS DROPDOWN -->
        <div id="notifDropdown" class="hidden absolute right-0 mt-2 w-72 glassmorphism rounded-xl p-3 shadow-2xl border border-gray-700 z-50">
          <h4 class="text-xs font-bold text-gray-400 border-b border-gray-800 pb-2 mb-2 uppercase">Notifications</h4>
          <div id="notifList" class="space-y-2 max-h-60 overflow-y-auto custom-scrollbar text-xs">
            <p class="text-gray-500 text-center py-2">No new notifications, sweetie!</p>
          </div>
        </div>
      </div>

      <!-- MESSAGES ICON -->
      <button onclick="switchTab('messages')" class="p-2 text-gray-300 hover:text-white rounded-full hover:bg-gray-800 transition relative">
        <i class="fa-solid fa-paper-plane text-lg"></i>
      </button>

      <!-- USER PROFILE BTN -->
      <button onclick="openMyProfile()" class="flex items-center gap-1 bg-gray-800 border border-gray-700 hover:border-blue-500 px-3 py-1 rounded-full">
        <span id="navUserName" class="text-xs font-semibold text-gray-200"></span>
        <span id="navVerifiedBadge" class="hidden text-blue-400 text-xs"><i class="fa-solid fa-circle-check"></i></span>
      </button>

      <button onclick="openWalletModal()" class="bg-gradient-to-r from-amber-500 to-yellow-600 text-xs font-bold px-3 py-1.5 rounded-lg text-black">
        <i class="fa-solid fa-coins"></i> <span id="navWalletBalance">PKR 0</span>
      </button>

      <button onclick="logout()" class="text-gray-400 hover:text-red-400 text-sm pl-2"><i class="fa-solid fa-right-from-bracket"></i></button>
    </div>

    <div id="authNavButtons" class="flex items-center space-x-3">
      <button onclick="toggleModal('authModal')" class="bg-blue-600 hover:bg-blue-700 text-sm font-semibold px-4 py-2 rounded-lg transition">Login / Register</button>
    </div>
  </nav>

  <!-- UPLOAD PROGRESS OVERLAY -->
  <div id="uploadProgressOverlay" class="hidden fixed bottom-4 right-4 bg-gray-900/90 border border-blue-500 p-4 rounded-xl shadow-2xl z-50 w-72">
    <div class="flex justify-between items-center mb-2">
      <span id="uploadStatusLabel" class="text-xs font-bold text-blue-400">Uploading Media...</span>
      <span id="uploadPercentText" class="text-xs font-mono font-bold text-white">0%</span>
    </div>
    <div class="w-full bg-gray-800 h-2 rounded-full overflow-hidden">
      <div id="uploadProgressBar" class="bg-blue-600 h-full w-0 transition-all duration-200"></div>
    </div>
  </div>

  <!-- MAIN APP LAYOUT -->
  <div class="max-w-7xl mx-auto grid grid-cols-1 md:grid-cols-4 gap-6 p-4">

    <!-- LEFT SIDEBAR -->
    <aside class="hidden md:block col-span-1 space-y-4">
      <div class="glassmorphism p-4 rounded-xl space-y-3">
        <button onclick="switchTab('feed')" class="w-full flex items-center space-x-3 text-gray-300 hover:text-white p-2 rounded-lg hover:bg-gray-800/50 transition">
          <i class="fa-solid fa-house text-blue-500 text-lg"></i> <span class="font-medium">Home Feed</span>
        </button>
        <button onclick="switchTab('reels')" class="w-full flex items-center space-x-3 text-gray-300 hover:text-white p-2 rounded-lg hover:bg-gray-800/50 transition">
          <i class="fa-solid fa-clapperboard text-red-500 text-lg"></i> <span class="font-medium">TikTok Reels</span>
        </button>
        <button onclick="switchTab('messages')" class="w-full flex items-center space-x-3 text-gray-300 hover:text-white p-2 rounded-lg hover:bg-gray-800/50 transition">
          <i class="fa-solid fa-comments text-purple-400 text-lg"></i> <span class="font-medium">Direct Messages</span>
        </button>
        <button onclick="openMyProfile()" class="w-full flex items-center space-x-3 text-gray-300 hover:text-white p-2 rounded-lg hover:bg-gray-800/50 transition">
          <i class="fa-solid fa-user text-indigo-400 text-lg"></i> <span class="font-medium">My Profile</span>
        </button>
        <button onclick="switchTab('groups')" class="w-full flex items-center space-x-3 text-gray-300 hover:text-white p-2 rounded-lg hover:bg-gray-800/50 transition">
          <i class="fa-solid fa-users text-green-400 text-lg"></i> <span class="font-medium">Communities</span>
        </button>
        <button onclick="openWalletModal()" class="w-full flex items-center space-x-3 text-gray-300 hover:text-white p-2 rounded-lg hover:bg-gray-800/50 transition">
          <i class="fa-solid fa-wallet text-amber-500 text-lg"></i> <span class="font-medium">Wallet & Earnings</span>
        </button>
      </div>
    </aside>

    <!-- CENTER FEED & APP VIEWS -->
    <main class="col-span-1 md:col-span-2 space-y-6">

      <!-- STORIES BAR -->
      <div class="glassmorphism p-3 rounded-xl">
        <h3 class="text-xs font-bold text-gray-400 mb-2 uppercase tracking-wider">Instagram Stories</h3>
        <div id="storiesBar" class="flex items-center space-x-3 overflow-x-auto custom-scrollbar pb-1">
          <div onclick="openAddStoryModal()" class="flex-shrink-0 flex flex-col items-center cursor-pointer group">
            <div class="w-14 h-14 rounded-full border-2 border-dashed border-blue-500 flex items-center justify-center bg-gray-900 group-hover:bg-gray-800 transition">
              <i class="fa-solid fa-plus text-blue-400"></i>
            </div>
            <span class="text-[10px] mt-1 text-gray-400">Add Story</span>
          </div>
          <div id="storiesContainer" class="flex space-x-3"></div>
        </div>
      </div>

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
              <i class="fa-solid fa-shield-halved"></i> EagleEye Admin Control
            </h2>
            <button onclick="lockAdminPanel()" class="text-xs bg-red-900/40 text-red-400 border border-red-700 px-2.5 py-1 rounded-lg">Lock Panel</button>
          </div>
          <div id="depositRequestsContainer" class="space-y-3 custom-scrollbar max-h-48 overflow-y-auto"></div>
        </section>

        <!-- FEED POSTS CONTAINER -->
        <section id="postsFeed" class="space-y-4"></section>
      </div>

      <!-- TAB 2: REELS FEED -->
      <div id="reelsTab" class="hidden space-y-4">
        <div class="flex justify-between items-center">
          <h2 class="text-lg font-bold text-red-400 flex items-center gap-2"><i class="fa-solid fa-fire"></i> Prime TikTok Reels</h2>
          <button onclick="openUploadReelModal()" class="bg-red-600 hover:bg-red-700 text-xs font-bold px-3 py-1.5 rounded-lg flex items-center gap-1"><i class="fa-solid fa-plus"></i> Upload Reel</button>
        </div>
        <div id="reelsContainer" class="h-[600px] overflow-y-scroll reel-snap rounded-2xl glassmorphism space-y-4 custom-scrollbar p-2"></div>
      </div>

      <!-- TAB 3: DIRECT MESSAGES -->
      <div id="messagesTab" class="hidden glassmorphism rounded-xl p-4 space-y-4 h-[600px] flex flex-col">
        <h2 class="text-lg font-bold text-purple-400 border-b border-gray-800 pb-2"><i class="fa-solid fa-comments"></i> Private Messenger</h2>
        <div class="flex-1 grid grid-cols-3 gap-3 overflow-hidden">
          <div id="chatUsersList" class="col-span-1 border-r border-gray-800 space-y-2 overflow-y-auto pr-2 custom-scrollbar"></div>
          <div class="col-span-2 flex flex-col justify-between bg-gray-900/50 rounded-lg p-3 relative">
            <!-- CALL BAR -->
            <div id="chatHeader" class="flex justify-between items-center border-b border-gray-800 pb-2 hidden">
              <span id="chatActiveUser" class="font-bold text-xs text-blue-400">Select User</span>
              <div class="flex space-x-2">
                <button onclick="startCall('audio')" class="text-green-400 hover:text-green-300 text-xs p-1"><i class="fa-solid fa-phone"></i> Audio Call</button>
                <button onclick="startCall('video')" class="text-blue-400 hover:text-blue-300 text-xs p-1"><i class="fa-solid fa-video"></i> Video Call</button>
              </div>
            </div>
            <div id="chatMessages" class="flex-1 overflow-y-auto space-y-2 p-2 text-xs custom-scrollbar">
              <p class="text-gray-500 text-center py-20">Select a user to start chatting, sweetie!</p>
            </div>
            <div id="chatInputArea" class="hidden flex gap-2 pt-2 border-t border-gray-800">
              <input id="chatMessageInput" type="text" placeholder="Type a message..." class="flex-1 bg-gray-900 border border-gray-700 rounded-lg p-2 text-xs focus:outline-none" />
              <button onclick="sendChatMessage()" class="bg-blue-600 hover:bg-blue-700 px-3 py-2 rounded-lg text-xs font-bold"><i class="fa-solid fa-paper-plane"></i></button>
            </div>
          </div>
        </div>
      </div>

      <!-- TAB 4: COMMUNITIES -->
      <div id="groupsTab" class="hidden space-y-4">
        <h2 class="text-lg font-bold text-green-400"><i class="fa-solid fa-users"></i> Facebook Communities</h2>
        <div class="grid grid-cols-2 gap-3">
          <div class="glassmorphism p-4 rounded-xl border border-green-500/20 text-center space-y-2">
            <i class="fa-solid fa-code text-2xl text-green-400"></i>
            <h3 class="font-bold text-sm">Tech & Web Developers GB</h3>
            <button onclick="alert('Welcome to Tech GB!')" class="bg-green-600 text-xs font-bold px-3 py-1 rounded-lg">Joined</button>
          </div>
        </div>
      </div>
    </main>

    <!-- RIGHT SIDEBAR -->
    <aside class="hidden md:block col-span-1 space-y-4">
      <div class="glassmorphism p-4 rounded-xl space-y-3 border border-indigo-500/30">
        <h3 class="font-bold text-sm text-indigo-400 flex items-center gap-1"><i class="fa-solid fa-chart-line"></i> Creator Dashboard</h3>
        <p class="text-xs text-gray-300">Track views, followings & real-time analytics.</p>
        <button onclick="openAnalyticsModal()" class="w-full bg-indigo-600 hover:bg-indigo-700 text-white font-bold py-2 rounded-lg text-xs">Open Analytics</button>
      </div>
    </aside>
  </div>

  <!-- MODAL: PROFILE DRAWER -->
  <div id="profileModal" class="fixed inset-0 bg-black/80 hidden items-center justify-center p-4 z-50">
    <div class="glassmorphism max-w-md w-full p-6 rounded-2xl space-y-4 relative max-h-[90vh] overflow-y-auto custom-scrollbar">
      <button onclick="toggleModal('profileModal')" class="absolute top-4 right-4 text-gray-400 hover:text-white"><i class="fa-solid fa-xmark"></i></button>
      <div class="text-center space-y-2">
        <div class="w-20 h-20 rounded-full bg-gradient-to-tr from-blue-500 to-purple-500 mx-auto flex items-center justify-center font-extrabold text-2xl" id="profileAvatar">U</div>
        <h3 class="font-bold text-lg flex items-center justify-center gap-1" id="profileName">User Name</h3>
        <p class="text-xs text-gray-400" id="profileEmail">user@example.com</p>
        <div class="flex justify-center space-x-6 text-xs pt-2">
          <div><b id="profileFollowers" class="text-blue-400">0</b> <span class="text-gray-400">Followers</span></div>
          <div><b id="profileFollowing" class="text-purple-400">0</b> <span class="text-gray-400">Following</span></div>
        </div>
        <button id="profileFollowBtn" onclick="toggleFollowUser()" class="w-full bg-blue-600 hover:bg-blue-700 font-bold py-2 rounded-lg text-xs mt-3">Follow</button>
      </div>
    </div>
  </div>

  <!-- MODAL: COMMENTS DRAWER -->
  <div id="commentsModal" class="fixed inset-0 bg-black/80 hidden items-center justify-center p-4 z-50">
    <div class="glassmorphism max-w-md w-full p-6 rounded-2xl space-y-4 relative">
      <button onclick="toggleModal('commentsModal')" class="absolute top-4 right-4 text-gray-400 hover:text-white"><i class="fa-solid fa-xmark"></i></button>
      <h3 class="text-md font-bold text-blue-400"><i class="fa-regular fa-comments"></i> Post Comments</h3>
      <input type="hidden" id="activePostKeyForComments" />
      <div id="commentsList" class="space-y-2 max-h-60 overflow-y-auto custom-scrollbar text-xs"></div>
      <div class="flex gap-2">
        <input id="commentInput" type="text" placeholder="Write a comment..." class="flex-1 bg-gray-900 border border-gray-700 p-2 rounded-lg text-xs" />
        <button onclick="submitComment()" class="bg-blue-600 px-3 py-2 rounded-lg text-xs font-bold">Post</button>
      </div>
    </div>
  </div>

  <!-- MODAL: LIVE CALL OVERLAY -->
  <div id="callModal" class="fixed inset-0 bg-black/90 hidden items-center justify-center p-4 z-50">
    <div class="glassmorphism max-w-sm w-full p-6 rounded-2xl space-y-4 text-center relative border border-green-500/50">
      <i class="fa-solid fa-video text-4xl text-green-400 animate-pulse"></i>
      <h3 class="font-bold text-md text-white" id="callTypeTitle">Live WebRTC Call</h3>
      <p class="text-xs text-gray-400">Connecting video and voice channels...</p>
      <div class="w-full h-40 bg-gray-900 rounded-xl flex items-center justify-center text-xs text-gray-600">Video Feed Stream</div>
      <button onclick="toggleModal('callModal')" class="w-full bg-red-600 hover:bg-red-700 py-2 rounded-lg text-xs font-bold">End Call</button>
    </div>
  </div>

  <!-- FIREBASE ENGINE SCRIPT -->
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
      appId: "1:465444221491:web:9824b4f1f9f592f76ce946"
    };

    const app = initializeApp(firebaseConfig);
    const auth = getAuth(app);
    const db = getDatabase(app);

    let currentUser = null;
    let selectedMediaBase64 = null;
    let selectedMediaType = null;
    let targetProfileUid = null;
    let activeChatUid = null;

    onAuthStateChanged(auth, (user) => {
      currentUser = user;
      if (user) {
        document.getElementById('authNavButtons').classList.add('hidden');
        document.getElementById('userNavProfile').classList.remove('hidden');
        document.getElementById('userNavProfile').classList.add('flex');
        document.getElementById('navUserName').innerText = user.displayName || user.email.split('@')[0];
        loadNotifications(user.uid);
        listenUsersForChat();
      } else {
        document.getElementById('authNavButtons').classList.remove('hidden');
        document.getElementById('userNavProfile').classList.add('hidden');
      }
    });

    // UPLOAD PROGRESS SIMULATION ENGINE
    function simulateUploadProgress(callback) {
      const overlay = document.getElementById('uploadProgressOverlay');
      const bar = document.getElementById('uploadProgressBar');
      const text = document.getElementById('uploadPercentText');
      overlay.classList.remove('hidden');
      let percent = 0;
      const interval = setInterval(() => {
        percent += 10;
        bar.style.width = percent + '%';
        text.innerText = percent + '%';
        if (percent >= 100) {
          clearInterval(interval);
          setTimeout(() => {
            overlay.classList.add('hidden');
            bar.style.width = '0%';
            if(callback) callback();
          }, 400);
        }
      }, 100);
    }

    // POST CREATION WITH PROGRESS BAR
    window.submitPost = async () => {
      if (!currentUser) return alert("Please login first, sweetie!");
      const content = document.getElementById('postInput').value;
      if (!content && !selectedMediaBase64) return alert("Add text or media!");

      simulateUploadProgress(async () => {
        const postRef = push(ref(db, 'posts'));
        await set(postRef, {
          author: currentUser.displayName || currentUser.email.split('@')[0],
          uid: currentUser.uid,
          content,
          media: selectedMediaBase64 || null,
          mediaType: selectedMediaType || null,
          likes: 0,
          views: 1,
          timestamp: Date.now()
        });
        document.getElementById('postInput').value = '';
        clearMedia();
      });
    };

    // LIKE SYSTEM WITH NOTIFICATIONS
    window.toggleLikePost = async (postKey, postAuthorUid) => {
      if (!currentUser) return alert("Please login!");
      const postRef = ref(db, `posts/${postKey}`);
      const snap = await get(postRef);
      if (snap.exists()) {
        const post = snap.val();
        const currentLikes = post.likes || 0;
        await update(postRef, { likes: currentLikes + 1 });
        
        // Push notification to post owner
        if (postAuthorUid !== currentUser.uid) {
          const notifRef = push(ref(db, `notifications/${postAuthorUid}`));
          await set(notifRef, {
            message: `${currentUser.displayName || currentUser.email.split('@')[0]} liked your post!`,
            timestamp: Date.now()
          });
        }
      }
    };

    // NOTIFICATIONS ENGINE
    function loadNotifications(uid) {
      onValue(ref(db, `notifications/${uid}`), (snapshot) => {
        const list = document.getElementById('notifList');
        const badge = document.getElementById('notifBadge');
        list.innerHTML = '';
        const data = snapshot.val();
        if (!data) return;
        const arr = Object.values(data).reverse();
        badge.innerText = arr.length;
        badge.classList.remove('hidden');

        arr.forEach(n => {
          const div = document.createElement('div');
          div.className = "p-2 bg-gray-900 rounded border border-gray-800 text-gray-300";
          div.innerText = n.message;
          list.appendChild(div);
        });
      });
    }

    window.toggleNotificationsMenu = () => {
      const drop = document.getElementById('notifDropdown');
      drop.classList.toggle('hidden');
    };

    // COMMENTS SYSTEM ENGINE
    window.openCommentsModal = (postKey) => {
      document.getElementById('activePostKeyForComments').value = postKey;
      toggleModal('commentsModal');
      onValue(ref(db, `comments/${postKey}`), (snapshot) => {
        const list = document.getElementById('commentsList');
        list.innerHTML = '';
        const data = snapshot.val();
        if (!data) { list.innerHTML = `<p class="text-gray-500 text-center">No comments yet.</p>`; return; }
        Object.values(data).forEach(c => {
          const div = document.createElement('div');
          div.className = "p-2 bg-gray-900 rounded border border-gray-800";
          div.innerHTML = `<b class="text-blue-400">${c.author}:</b> ${c.text}`;
          list.appendChild(div);
        });
      });
    };

    window.submitComment = async () => {
      if (!currentUser) return alert("Login first!");
      const postKey = document.getElementById('activePostKeyForComments').value;
      const text = document.getElementById('commentInput').value;
      if (!text) return;
      const cRef = push(ref(db, `comments/${postKey}`));
      await set(cRef, {
        author: currentUser.displayName || currentUser.email.split('@')[0],
        text,
        timestamp: Date.now()
      });
      document.getElementById('commentInput').value = '';
    };

    // FOLLOW / UNFOLLOW PROFILE SYSTEM ENGINE
    window.openUserProfile = (uid, name, email) => {
      targetProfileUid = uid;
      document.getElementById('profileAvatar').innerText = name.charAt(0).toUpperCase();
      document.getElementById('profileName').innerText = name;
      document.getElementById('profileEmail').innerText = email;
      
      onValue(ref(db, `followers/${uid}`), (snap) => {
        document.getElementById('profileFollowers').innerText = snap.exists() ? Object.keys(snap.val()).length : 0;
      });
      onValue(ref(db, `following/${uid}`), (snap) => {
        document.getElementById('profileFollowing').innerText = snap.exists() ? Object.keys(snap.val()).length : 0;
      });

      toggleModal('profileModal');
    };

    window.openMyProfile = () => {
      if (!currentUser) return alert("Login first!");
      window.openUserProfile(currentUser.uid, currentUser.displayName || currentUser.email.split('@')[0], currentUser.email);
    };

    window.toggleFollowUser = async () => {
      if (!currentUser || !targetProfileUid) return;
      const followRef = ref(db, `followers/${targetProfileUid}/${currentUser.uid}`);
      const snap = await get(followRef);
      if (snap.exists()) {
        await remove(followRef);
        await remove(ref(db, `following/${currentUser.uid}/${targetProfileUid}`));
      } else {
        await set(followRef, true);
        await set(ref(db, `following/${currentUser.uid}/${targetProfileUid}`), true);
      }
    };

    // PRIVATE MESSENGER & CHAT SYSTEM
    function listenUsersForChat() {
      onValue(ref(db, 'posts'), (snapshot) => {
        const usersList = document.getElementById('chatUsersList');
        usersList.innerHTML = '';
        const data = snapshot.val();
        if (!data) return;
        const users = {};
        Object.values(data).forEach(p => { if (p.uid !== currentUser.uid) users[p.uid] = p.author; });
        Object.entries(users).forEach(([uid, name]) => {
          const div = document.createElement('div');
          div.className = "p-2 bg-gray-900 rounded-lg hover:bg-gray-800 cursor-pointer text-xs font-bold text-gray-300";
          div.innerText = name;
          div.onclick = () => selectChatUser(uid, name);
          usersList.appendChild(div);
        });
      });
    }

    function selectChatUser(uid, name) {
      activeChatUid = uid;
      document.getElementById('chatActiveUser').innerText = name;
      document.getElementById('chatHeader').classList.remove('hidden');
      document.getElementById('chatInputArea').classList.remove('hidden');
      
      const chatId = currentUser.uid < uid ? `${currentUser.uid}_${uid}` : `${uid}_${currentUser.uid}`;
      onValue(ref(db, `chats/${chatId}`), (snapshot) => {
        const box = document.getElementById('chatMessages');
        box.innerHTML = '';
        const data = snapshot.val();
        if (!data) return;
        Object.values(data).forEach(m => {
          const div = document.createElement('div');
          div.className = `p-2 rounded-lg max-w-[80%] ${m.sender === currentUser.uid ? 'bg-blue-600 ml-auto text-white' : 'bg-gray-800 text-gray-200'}`;
          div.innerText = m.text;
          box.appendChild(div);
        });
      });
    }

    window.sendChatMessage = async () => {
      const input = document.getElementById('chatMessageInput');
      if (!input.value || !activeChatUid) return;
      const chatId = currentUser.uid < activeChatUid ? `${currentUser.uid}_${activeChatUid}` : `${activeChatUid}_${currentUser.uid}`;
      const msgRef = push(ref(db, `chats/${chatId}`));
      await set(msgRef, {
        sender: currentUser.uid,
        text: input.value,
        timestamp: Date.now()
      });
      input.value = '';
    };

    window.startCall = (type) => {
      document.getElementById('callTypeTitle').innerText = `Live ${type.toUpperCase()} Call Connection`;
      toggleModal('callModal');
    };

    // FEED RENDER ENGINE
    onValue(ref(db, 'posts'), (snapshot) => {
      const feed = document.getElementById('postsFeed'); feed.innerHTML = '';
      const data = snapshot.val(); if (!data) return;
      Object.entries(data).reverse().forEach(([key, post]) => {
        const el = document.createElement('div');
        el.className = 'glassmorphism p-4 rounded-xl space-y-3';
        el.innerHTML = `
          <div class="flex justify-between items-center">
            <div class="flex items-center space-x-2 cursor-pointer" onclick="openUserProfile('${post.uid}', '${post.author}', 'User Profile')">
              <div class="w-8 h-8 rounded-full bg-blue-600 flex items-center justify-center font-bold text-xs">${post.author.charAt(0).toUpperCase()}</div>
              <div>
                <p class="text-sm font-bold text-white">${post.author}</p>
                <p class="text-[10px] text-gray-500">${new Date(post.timestamp).toLocaleTimeString()}</p>
              </div>
            </div>
          </div>
          <p class="text-sm text-gray-300">${post.content}</p>
          ${post.media && post.mediaType === 'image' ? `<img src="${post.media}" class="w-full h-64 object-cover rounded-lg" />` : ''}
          ${post.media && post.mediaType === 'video' ? `<video src="${post.media}" controls class="w-full h-64 object-cover rounded-lg"></video>` : ''}
          <div class="flex justify-between items-center text-xs text-gray-400 pt-2 border-t border-gray-800">
            <button onclick="toggleLikePost('${key}', '${post.uid}')" class="hover:text-red-400 flex items-center gap-1"><i class="fa-solid fa-heart"></i> ${post.likes || 0} Likes</button>
            <button onclick="openCommentsModal('${key}')" class="hover:text-blue-400 flex items-center gap-1"><i class="fa-regular fa-comment"></i> Comments</button>
          </div>
        `;
        feed.appendChild(el);
      });
    });
  </script>

  <script>
    function toggleModal(id) { const el = document.getElementById(id); el.classList.toggle('hidden'); el.classList.toggle('flex'); }
    function switchTab(tab) {
      document.getElementById('feedTab').classList.add('hidden');
      document.getElementById('reelsTab').classList.add('hidden');
      document.getElementById('messagesTab').classList.add('hidden');
      document.getElementById('groupsTab').classList.add('hidden');
      if (tab === 'feed') document.getElementById('feedTab').classList.remove('hidden');
      if (tab === 'reels') document.getElementById('reelsTab').classList.remove('hidden');
      if (tab === 'messages') document.getElementById('messagesTab').classList.remove('hidden');
      if (tab === 'groups') document.getElementById('groupsTab').classList.remove('hidden');
    }
  </script>
</body>
</html>
