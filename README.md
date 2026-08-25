<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>PrimeX Pro Ultimate - Full Social Ecosystem</title>
  <!-- Tailwind CSS -->
  <script src="https://cdn.tailwindcss.com"></script>
  <!-- FontAwesome -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css"/>
  <style>
    body { background-color: #0b0f19; color: #f3f4f6; font-family: 'Inter', sans-serif; padding-bottom: 60px; }
    @media (min-width: 768px) { body { padding-bottom: 0; } }
    .glassmorphism { background: rgba(17, 24, 39, 0.7); backdrop-filter: blur(12px); border: 1px solid rgba(255, 255, 255, 0.08); }
    .custom-scrollbar::-webkit-scrollbar { width: 5px; height: 5px; }
    .custom-scrollbar::-webkit-scrollbar-thumb { background: #374151; border-radius: 4px; }
    .reel-snap { scroll-snap-type: y mandatory; }
    .reel-card { scroll-snap-align: start; }
  </style>
</head>
<body class="custom-scrollbar">

  <!-- TOP NAVIGATION BAR -->
  <nav class="sticky top-0 z-50 glassmorphism border-b border-gray-800 px-4 py-3 flex justify-between items-center">
    <div class="flex items-center space-x-3">
      <h1 id="secretLogoBtn" onclick="handleLogoTap()" class="cursor-pointer text-xl sm:text-2xl font-extrabold tracking-wider bg-gradient-to-r from-blue-500 via-indigo-500 to-purple-500 bg-clip-text text-transparent select-none">
        PrimeX <span class="text-[10px] bg-amber-500 text-black px-1.5 py-0.5 rounded font-bold uppercase">Pro Mega</span>
      </h1>
      <!-- LIVE SEARCH BAR -->
      <div class="relative hidden sm:block">
        <input id="searchInput" onkeyup="filterFeedPosts()" type="text" placeholder="Search posts or creators..." class="bg-gray-900 border border-gray-700 rounded-lg text-xs px-3 py-1.5 text-white w-48 focus:w-64 transition-all focus:outline-none focus:border-blue-500" />
      </div>
    </div>

    <div id="authNavButtons" class="flex items-center space-x-3">
      <button onclick="toggleModal('authModal')" class="bg-blue-600 hover:bg-blue-700 text-sm font-semibold px-4 py-2 rounded-lg transition">Login / Register</button>
    </div>

    <div id="userNavProfile" class="hidden flex items-center space-x-2 md:space-x-3">
      <!-- NOTIFICATION BELL ICON -->
      <button onclick="openNotificationsModal()" class="relative text-gray-300 hover:text-white p-1.5">
        <i class="fa-solid fa-bell text-lg"></i>
        <span id="notifBadge" class="hidden absolute top-0 right-0 w-2.5 h-2.5 bg-red-500 rounded-full animate-pulse"></span>
      </button>
      <!-- DIRECT MESSAGES CHAT ICON -->
      <button onclick="openChatModal()" class="text-gray-300 hover:text-white p-1.5" title="Direct Messages">
        <i class="fa-solid fa-paper-plane text-lg"></i>
      </button>

      <button onclick="openAnalyticsModal()" class="bg-indigo-600/80 hover:bg-indigo-600 text-xs font-bold px-2.5 py-1.5 rounded-lg flex items-center gap-1">
        <i class="fa-solid fa-chart-line"></i> <span class="hidden sm:inline">Analytics</span>
      </button>
      <button onclick="openWalletModal()" class="bg-gradient-to-r from-amber-500 to-yellow-600 text-xs font-bold px-2.5 py-1.5 rounded-lg hover:opacity-90 flex items-center gap-1 text-black">
        <i class="fa-solid fa-coins"></i> <span id="navWalletBalance">PKR 0</span>
      </button>
      <button onclick="openDepositModal()" class="bg-gradient-to-r from-green-500 to-emerald-600 text-xs font-bold px-2.5 py-1.5 rounded-lg hover:opacity-90 flex items-center gap-1">
        <i class="fa-solid fa-wallet"></i> <span class="hidden sm:inline">Top-up</span>
      </button>
      <div class="flex items-center gap-1 cursor-pointer" onclick="openMyProfileModal()">
        <span id="navUserName" class="text-sm font-medium text-gray-300 hover:text-blue-400 transition"></span>
        <span id="navVerifiedBadge" class="hidden text-blue-400 text-xs" title="Verified Creator"><i class="fa-solid fa-circle-check"></i></span>
      </div>
      <button onclick="logout()" class="text-gray-400 hover:text-red-400 text-sm pl-1"><i class="fa-solid fa-right-from-bracket"></i></button>
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
          <i class="fa-solid fa-clapperboard text-red-500 text-lg"></i> <span class="font-medium">TikTok Reels</span>
        </button>
        <button onclick="switchTab('saved')" class="w-full flex items-center space-x-3 text-gray-300 hover:text-white p-2 rounded-lg hover:bg-gray-800/50 transition">
          <i class="fa-solid fa-bookmark text-yellow-500 text-lg"></i> <span class="font-medium">Saved Bookmarks</span>
        </button>
        <button onclick="switchTab('groups')" class="w-full flex items-center space-x-3 text-gray-300 hover:text-white p-2 rounded-lg hover:bg-gray-800/50 transition">
          <i class="fa-solid fa-users text-green-400 text-lg"></i> <span class="font-medium">Facebook Communities</span>
        </button>
        <button onclick="openChatModal()" class="w-full flex items-center space-x-3 text-gray-300 hover:text-white p-2 rounded-lg hover:bg-gray-800/50 transition">
          <i class="fa-solid fa-comments text-cyan-400 text-lg"></i> <span class="font-medium">Direct Messages</span>
        </button>
        <button onclick="openMyProfileModal()" class="w-full flex items-center space-x-3 text-gray-300 hover:text-white p-2 rounded-lg hover:bg-gray-800/50 transition">
          <i class="fa-solid fa-user-gear text-indigo-400 text-lg"></i> <span class="font-medium">Edit Profile</span>
        </button>
        <button onclick="openAnalyticsModal()" class="w-full flex items-center space-x-3 text-gray-300 hover:text-white p-2 rounded-lg hover:bg-gray-800/50 transition">
          <i class="fa-solid fa-chart-pie text-purple-400 text-lg"></i> <span class="font-medium">Creator Dashboard</span>
        </button>
        <button onclick="openVerifyModal()" class="w-full flex items-center space-x-3 text-gray-300 hover:text-white p-2 rounded-lg hover:bg-gray-800/50 transition">
          <i class="fa-solid fa-certificate text-blue-400 text-lg"></i> <span class="font-medium">Get Verified Badge</span>
        </button>
        <button onclick="openWalletModal()" class="w-full flex items-center space-x-3 text-gray-300 hover:text-white p-2 rounded-lg hover:bg-gray-800/50 transition">
          <i class="fa-solid fa-wallet text-amber-500 text-lg"></i> <span class="font-medium">Wallet & Earnings</span>
        </button>
      </div>
    </aside>

    <!-- CENTER CONTENT AREA -->
    <main class="col-span-1 md:col-span-2 space-y-6">

      <!-- INSTAGRAM STORIES BAR -->
      <div class="glassmorphism p-3 rounded-xl">
        <h3 class="text-xs font-bold text-gray-400 mb-2 uppercase tracking-wider">Instagram Stories</h3>
        <div id="storiesBar" class="flex items-center space-x-3 overflow-x-auto custom-scrollbar pb-1">
          <div onclick="openAddStoryModal()" class="flex-shrink-0 flex flex-col items-center cursor-pointer group">
            <div class="w-14 h-14 rounded-full border-2 border-dashed border-blue-500 flex items-center justify-center bg-gray-900 group-hover:bg-gray-800 transition">
              <i class="fa-solid fa-plus text-blue-400"></i>
            </div>
            <span class="text-[10px] mt-1 text-gray-400 group-hover:text-white">Add Story</span>
          </div>
          <div id="storiesContainer" class="flex space-x-3"></div>
        </div>
      </div>

      <!-- TAB 1: HOME FEED -->
      <div id="feedTab" class="space-y-6">
        <!-- CREATE POST BOX -->
        <div class="glassmorphism p-4 rounded-xl space-y-3">
          <textarea id="postInput" rows="2" placeholder="What's happening on PrimeX, sweetie?" class="w-full bg-gray-900 border border-gray-700 rounded-lg p-3 text-sm focus:outline-none focus:border-blue-500 resize-none text-white"></textarea>
          
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
            <button onclick="submitPost()" class="bg-blue-600 hover:bg-blue-700 text-xs font-bold px-4 py-2 rounded-lg text-white">Publish Post</button>
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
              <h3 class="text-xs font-bold text-gray-400 uppercase tracking-wider mb-2">Pending Fund Deposits</h3>
              <div id="depositRequestsContainer" class="space-y-3 custom-scrollbar max-h-48 overflow-y-auto"></div>
            </div>
            <div class="border-t border-gray-800 pt-4">
              <h3 class="text-xs font-bold text-gray-400 uppercase tracking-wider mb-2">Pending Withdrawals</h3>
              <div id="withdrawRequestsContainer" class="space-y-3 custom-scrollbar max-h-48 overflow-y-auto"></div>
            </div>
          </div>
        </section>

        <!-- FEED POSTS CONTAINER -->
        <section id="postsFeed" class="space-y-4"></section>
      </div>

      <!-- TAB 2: REELS -->
      <div id="reelsTab" class="hidden space-y-4">
        <div class="flex justify-between items-center">
          <h2 class="text-lg font-bold text-red-400 flex items-center gap-2">
            <i class="fa-solid fa-fire"></i> Prime Reels & TikTok Duets
          </h2>
          <button onclick="openUploadReelModal()" class="bg-red-600 hover:bg-red-700 text-xs font-bold px-3 py-1.5 rounded-lg flex items-center gap-1 text-white">
            <i class="fa-solid fa-plus"></i> Upload Reel
          </button>
        </div>
        <div id="reelsContainer" class="h-[600px] overflow-y-scroll reel-snap rounded-2xl glassmorphism space-y-4 custom-scrollbar p-2"></div>
      </div>

      <!-- TAB 3: SAVED BOOKMARKS -->
      <div id="savedTab" class="hidden space-y-4">
        <h2 class="text-lg font-bold text-yellow-400 flex items-center gap-2"><i class="fa-solid fa-bookmark"></i> Saved Posts</h2>
        <div id="savedPostsContainer" class="space-y-4"></div>
      </div>

      <!-- TAB 4: GROUPS -->
      <div id="groupsTab" class="hidden space-y-4">
        <h2 class="text-lg font-bold text-green-400 flex items-center gap-2"><i class="fa-solid fa-users"></i> Facebook Style Communities</h2>
        <div class="grid grid-cols-1 sm:grid-cols-2 gap-3">
          <div class="glassmorphism p-4 rounded-xl border border-green-500/20 text-center space-y-2">
            <i class="fa-solid fa-code text-2xl text-green-400"></i>
            <h3 class="font-bold text-sm">Tech & Web Developers GB</h3>
            <p class="text-[11px] text-gray-400">Discuss web apps, APIs & modern tech.</p>
            <button onclick="joinCommunity('Tech GB')" class="bg-green-600 text-xs font-bold px-3 py-1 rounded-lg text-white">Joined</button>
          </div>
          <div class="glassmorphism p-4 rounded-xl border border-blue-500/20 text-center space-y-2">
            <i class="fa-solid fa-mountain text-2xl text-blue-400"></i>
            <h3 class="font-bold text-sm">Discover Gilgit-Baltistan</h3>
            <p class="text-[11px] text-gray-400">Share news, photos & tourism updates.</p>
            <button onclick="joinCommunity('GB Tourism')" class="bg-blue-600 text-xs font-bold px-3 py-1 rounded-lg text-white">Joined</button>
          </div>
        </div>
      </div>

    </main>

    <!-- RIGHT SIDEBAR -->
    <aside class="hidden md:block col-span-1 space-y-4">
      <div class="glassmorphism p-4 rounded-xl space-y-3 border border-indigo-500/30">
        <h3 class="font-bold text-sm text-indigo-400 flex items-center gap-1"><i class="fa-solid fa-chart-line"></i> Creator Analytics</h3>
        <p class="text-xs text-gray-300 leading-relaxed">Monitor your real-time video performance, views growth, and wallet balance analytics.</p>
        <button onclick="openAnalyticsModal()" class="w-full bg-indigo-600 hover:bg-indigo-700 text-white font-bold py-2 rounded-lg text-xs">Open Dashboard</button>
      </div>
      <div class="glassmorphism p-4 rounded-xl space-y-3 border border-amber-500/30">
        <h3 class="font-bold text-sm text-amber-400 flex items-center gap-1"><i class="fa-solid fa-bullhorn"></i> Paid Ad Booster</h3>
        <p class="text-xs text-gray-300 leading-relaxed">Boost your posts or reels to appear on top of all feeds (Starting @ PKR 300).</p>
        <button onclick="openBoostInfo()" class="w-full bg-gradient-to-r from-amber-500 to-yellow-600 text-black font-bold py-2 rounded-lg text-xs">Learn More & Boost</button>
      </div>
    </aside>
  </div>

  <!-- DIRECT MESSAGES CHAT MODAL -->
  <div id="chatModal" class="fixed inset-0 bg-black/85 hidden items-center justify-center p-4 z-50">
    <div class="glassmorphism max-w-lg w-full h-[550px] p-4 rounded-2xl flex flex-col relative">
      <button onclick="toggleModal('chatModal')" class="absolute top-4 right-4 text-gray-400 hover:text-white"><i class="fa-solid fa-xmark"></i></button>
      <h2 class="text-md font-bold text-blue-400 flex items-center gap-2 border-b border-gray-800 pb-3">
        <i class="fa-solid fa-comments"></i> Prime Messenger
      </h2>
      <div class="flex-1 grid grid-cols-3 gap-2 py-2 overflow-hidden">
        <div id="chatUsersList" class="col-span-1 border-r border-gray-800 pr-2 space-y-2 overflow-y-auto custom-scrollbar"></div>
        <div class="col-span-2 flex flex-col justify-between pl-2">
          <div id="chatMessagesBox" class="flex-1 overflow-y-auto space-y-2 custom-scrollbar p-1">
            <p class="text-[11px] text-gray-500 text-center py-10">Select a user to start chatting.</p>
          </div>
          <div class="flex gap-2 pt-2 border-t border-gray-800">
            <input id="chatInput" type="text" placeholder="Type a message..." class="flex-1 bg-gray-900 border border-gray-700 rounded-lg text-xs px-2.5 py-2 text-white focus:outline-none" />
            <button onclick="sendChatMessage()" class="bg-blue-600 hover:bg-blue-700 text-xs font-bold px-3 py-2 rounded-lg text-white"><i class="fa-solid fa-paper-plane"></i></button>
          </div>
        </div>
      </div>
    </div>
  </div>

  <!-- NOTIFICATIONS MODAL -->
  <div id="notificationsModal" class="fixed inset-0 bg-black/85 hidden items-center justify-center p-4 z-50">
    <div class="glassmorphism max-w-sm w-full p-5 rounded-2xl space-y-4 relative">
      <button onclick="toggleModal('notificationsModal')" class="absolute top-4 right-4 text-gray-400 hover:text-white"><i class="fa-solid fa-xmark"></i></button>
      <h2 class="text-md font-bold text-purple-400 flex items-center gap-2"><i class="fa-solid fa-bell"></i> Notifications</h2>
      <div id="notificationsList" class="space-y-2 max-h-64 overflow-y-auto custom-scrollbar"></div>
    </div>
  </div>

  <!-- VIEW USER PROFILE & FOLLOW MODAL -->
  <div id="userProfileModal" class="fixed inset-0 bg-black/85 hidden items-center justify-center p-4 z-50">
    <div class="glassmorphism max-w-sm w-full p-6 rounded-2xl space-y-4 relative text-center">
      <button onclick="toggleModal('userProfileModal')" class="absolute top-4 right-4 text-gray-400 hover:text-white"><i class="fa-solid fa-xmark"></i></button>
      <div class="w-16 h-16 rounded-full bg-gradient-to-tr from-blue-500 to-indigo-500 flex items-center justify-center text-xl font-bold text-white mx-auto shadow-lg" id="viewProfileAvatar">U</div>
      <div>
        <h2 id="viewProfileName" class="text-lg font-bold flex items-center justify-center gap-1 text-white">User Name</h2>
        <p id="viewProfileBio" class="text-xs text-gray-400 mt-1">Bio details will appear here...</p>
      </div>
      <div class="flex justify-center gap-6 py-2 border-y border-gray-800 text-xs text-gray-300">
        <div><span id="viewProfileFollowersCount" class="font-bold text-white">0</span> <br><span class="text-gray-400 text-[10px] uppercase">Followers</span></div>
        <div><span id="viewProfileFollowingCount" class="font-bold text-white">0</span> <br><span class="text-gray-400 text-[10px] uppercase">Following</span></div>
      </div>
      <div class="flex gap-2">
        <button id="viewProfileFollowBtn" onclick="toggleFollowUser()" class="flex-1 bg-blue-600 hover:bg-blue-700 py-2 rounded-lg text-xs font-bold text-white">Follow</button>
        <button id="viewProfileMsgBtn" onclick="startDirectMessage()" class="flex-1 bg-gray-800 hover:bg-gray-700 py-2 rounded-lg text-xs font-bold text-white"><i class="fa-solid fa-paper-plane"></i> Message</button>
      </div>
    </div>
  </div>

  <!-- EDIT PROFILE MODAL -->
  <div id="editProfileModal" class="fixed inset-0 bg-black/80 hidden items-center justify-center p-4 z-50">
    <div class="glassmorphism max-w-sm w-full p-6 rounded-2xl space-y-4 relative">
      <button onclick="toggleModal('editProfileModal')" class="absolute top-4 right-4 text-gray-400 hover:text-white"><i class="fa-solid fa-xmark"></i></button>
      <h2 class="text-lg font-bold text-center text-indigo-400 flex items-center justify-center gap-2"><i class="fa-solid fa-user-pen"></i> Update Profile</h2>
      <div>
        <label class="text-xs text-gray-400">Display Name</label>
        <input id="editDisplayName" type="text" placeholder="Your Full Name..." class="w-full bg-gray-900 border border-gray-700 p-2.5 rounded-lg text-xs mt-1 text-white" />
      </div>
      <div>
        <label class="text-xs text-gray-400">Bio</label>
        <textarea id="editUserBio" rows="3" placeholder="Tell something about yourself..." class="w-full bg-gray-900 border border-gray-700 p-2.5 rounded-lg text-xs mt-1 text-white resize-none"></textarea>
      </div>
      <button onclick="saveUserProfile()" class="w-full bg-indigo-600 hover:bg-indigo-700 py-2.5 rounded-lg text-xs font-bold text-white">Save Changes</button>
    </div>
  </div>

  <!-- MOBILE BOTTOM NAVIGATION BAR -->
  <div class="md:hidden fixed bottom-0 left-0 right-0 z-40 glassmorphism border-t border-gray-800 flex justify-around py-2">
    <button onclick="switchTab('feed')" class="flex flex-col items-center text-gray-400 hover:text-blue-400">
      <i class="fa-solid fa-house text-lg"></i><span class="text-[10px]">Feed</span>
    </button>
    <button onclick="switchTab('reels')" class="flex flex-col items-center text-gray-400 hover:text-red-400">
      <i class="fa-solid fa-clapperboard text-lg"></i><span class="text-[10px]">Reels</span>
    </button>
    <button onclick="openChatModal()" class="flex flex-col items-center text-gray-400 hover:text-cyan-400">
      <i class="fa-solid fa-paper-plane text-lg"></i><span class="text-[10px]">Chat</span>
    </button>
    <button onclick="switchTab('saved')" class="flex flex-col items-center text-gray-400 hover:text-yellow-400">
      <i class="fa-solid fa-bookmark text-lg"></i><span class="text-[10px]">Saved</span>
    </button>
  </div>

  <!-- MODAL: ADD INSTAGRAM STORY -->
  <div id="addStoryModal" class="fixed inset-0 bg-black/80 hidden items-center justify-center p-4 z-50">
    <div class="glassmorphism max-w-sm w-full p-6 rounded-2xl space-y-4 relative">
      <button onclick="toggleModal('addStoryModal')" class="absolute top-4 right-4 text-gray-400 hover:text-white"><i class="fa-solid fa-xmark"></i></button>
      <h2 class="text-lg font-bold text-center text-blue-400">Post 24-Hour Story</h2>
      <input id="storyFileInput" type="file" accept="image/*,video/*" class="w-full bg-gray-900 border border-gray-700 p-2.5 rounded-lg text-xs text-white" />
      <button onclick="submitStory()" class="w-full bg-blue-600 hover:bg-blue-700 py-2.5 rounded-lg text-xs font-bold text-white">Upload Story</button>
    </div>
  </div>

  <!-- MODAL: VIEW STORY VIEWPORT -->
  <div id="viewStoryModal" class="fixed inset-0 bg-black/90 hidden items-center justify-center p-4 z-50">
    <div class="max-w-xs w-full glassmorphism rounded-2xl p-4 text-center relative">
      <button onclick="toggleModal('viewStoryModal')" class="absolute top-2 right-2 bg-red-600 text-white rounded-full w-6 h-6 text-xs flex items-center justify-center"><i class="fa-solid fa-xmark"></i></button>
      <p id="storyAuthor" class="font-bold text-xs text-blue-400 mb-2"></p>
      <img id="storyImageDisplay" class="w-full h-80 object-cover rounded-xl hidden" />
      <video id="storyVideoDisplay" class="w-full h-80 object-cover rounded-xl hidden" controls autoplay></video>
    </div>
  </div>

  <!-- MODAL: ANALYTICS DASHBOARD -->
  <div id="analyticsModal" class="fixed inset-0 bg-black/80 hidden items-center justify-center p-4 z-50">
    <div class="glassmorphism max-w-md w-full p-6 rounded-2xl space-y-4 relative">
      <button onclick="toggleModal('analyticsModal')" class="absolute top-4 right-4 text-gray-400 hover:text-white"><i class="fa-solid fa-xmark"></i></button>
      <h2 class="text-lg font-bold text-center text-indigo-400 flex items-center justify-center gap-2"><i class="fa-solid fa-chart-pie"></i> Creator Performance Analytics</h2>
      <div class="grid grid-cols-2 gap-3 text-center">
        <div class="bg-gray-900/80 p-3 rounded-xl border border-indigo-500/20"><p class="text-[10px] text-gray-400 uppercase">Total Post Views</p><p id="statTotalViews" class="text-xl font-extrabold text-blue-400">0</p></div>
        <div class="bg-gray-900/80 p-3 rounded-xl border border-indigo-500/20"><p class="text-[10px] text-gray-400 uppercase">Engagement Rate</p><p id="statEngagement" class="text-xl font-extrabold text-green-400">94.2%</p></div>
        <div class="bg-gray-900/80 p-3 rounded-xl border border-indigo-500/20"><p class="text-[10px] text-gray-400 uppercase">Est. Monetization</p><p id="statMonetization" class="text-xl font-extrabold text-amber-400">PKR 0</p></div>
        <div class="bg-gray-900/80 p-3 rounded-xl border border-indigo-500/20"><p class="text-[10px] text-gray-400 uppercase">Top Reach Region</p><p class="text-sm font-bold text-purple-400">Gilgit-Baltistan</p></div>
      </div>
    </div>
  </div>

  <!-- MODAL: TIKTOK DUET REACTION -->
  <div id="duetModal" class="fixed inset-0 bg-black/80 hidden items-center justify-center p-4 z-50">
    <div class="glassmorphism max-w-md w-full p-6 rounded-2xl space-y-4 relative">
      <button onclick="toggleModal('duetModal')" class="absolute top-4 right-4 text-gray-400 hover:text-white"><i class="fa-solid fa-xmark"></i></button>
      <h2 class="text-lg font-bold text-center text-red-400">Create TikTok Duet Video</h2>
      <input id="duetOriginalUrl" type="hidden" />
      <div class="grid grid-cols-2 gap-2 h-40 bg-black rounded-lg overflow-hidden border border-gray-700">
        <video id="duetOriginalPreview" class="w-full h-full object-cover" muted></video>
        <div class="flex items-center justify-center bg-gray-900 text-xs text-gray-500">Your Video Split Screen</div>
      </div>
      <input id="duetVideoInput" type="file" accept="video/*" class="w-full bg-gray-900 border border-gray-700 p-2 rounded-lg text-xs text-white" />
      <button onclick="submitDuetReel()" class="w-full bg-red-600 hover:bg-red-700 py-2.5 rounded-lg text-xs font-bold text-white">Publish Duet Reel</button>
    </div>
  </div>

  <!-- MODAL: POST COMMENTS -->
  <div id="commentsModal" class="fixed inset-0 bg-black/80 hidden items-center justify-center p-4 z-50">
    <div class="glassmorphism max-w-md w-full p-6 rounded-2xl space-y-4 relative flex flex-col max-h-[80vh]">
      <button onclick="toggleModal('commentsModal')" class="absolute top-4 right-4 text-gray-400 hover:text-white"><i class="fa-solid fa-xmark"></i></button>
      <h2 class="text-lg font-bold text-center text-blue-400 flex items-center justify-center gap-2"><i class="fa-solid fa-comments"></i> Comments</h2>
      <input id="activePostKey" type="hidden" />
      <div id="commentsList" class="flex-1 overflow-y-auto space-y-3 custom-scrollbar pr-1"></div>
      <div class="flex gap-2 pt-2 border-t border-gray-800">
        <input id="commentInput" type="text" placeholder="Write a comment..." class="flex-1 bg-gray-900 border border-gray-700 rounded-lg p-2 text-xs text-white focus:outline-none" />
        <button onclick="submitComment()" class="bg-blue-600 hover:bg-blue-700 text-xs font-bold px-4 py-2 rounded-lg text-white">Send</button>
      </div>
    </div>
  </div>

  <!-- BOOST POST MODAL -->
  <div id="boostModal" class="fixed inset-0 bg-black/80 hidden items-center justify-center p-4 z-50">
    <div class="glassmorphism max-w-sm w-full p-6 rounded-2xl space-y-4 relative">
      <button onclick="toggleModal('boostModal')" class="absolute top-4 right-4 text-gray-400 hover:text-white"><i class="fa-solid fa-xmark"></i></button>
      <h2 class="text-lg font-bold text-center text-amber-400">Boost Post (Paid Ad)</h2>
      <p class="text-xs text-gray-300 text-center">Pin this post on top of user feeds for 24 hours.</p>
      <input id="boostPostKey" type="hidden" />
      <select id="boostPackage" class="w-full bg-gray-900 border border-gray-700 p-2.5 rounded-lg text-xs text-white">
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
      <p class="text-xs text-gray-300">Unlock official credibility for a fee of <strong>PKR 999</strong>.</p>
      <button onclick="purchaseVerification()" class="w-full bg-blue-600 hover:bg-blue-700 py-2.5 rounded-lg text-xs font-bold text-white">Pay & Get Verified</button>
    </div>
  </div>

  <!-- UPLOAD REEL MODAL -->
  <div id="uploadReelModal" class="fixed inset-0 bg-black/80 hidden items-center justify-center p-4 z-50">
    <div class="glassmorphism max-w-md w-full p-6 rounded-2xl space-y-4 relative">
      <button onclick="toggleModal('uploadReelModal')" class="absolute top-4 right-4 text-gray-400 hover:text-white"><i class="fa-solid fa-xmark"></i></button>
      <h2 class="text-lg font-bold text-center text-red-400">Upload Short Reel</h2>
      <input id="reelTitleInput" type="text" placeholder="Reel Caption / Title" class="w-full bg-gray-900 border border-gray-700 p-2.5 rounded-lg text-sm text-white" />
      <div>
        <label class="text-xs text-gray-400">Select Video from Device</label>
        <input id="reelVideoFile" type="file" accept="video/*" class="w-full bg-gray-900 border border-gray-700 p-2 rounded-lg text-xs mt-1 text-white" />
      </div>
      <button onclick="submitReel()" class="w-full bg-red-600 hover:bg-red-700 py-2.5 rounded-lg text-sm font-bold text-white">Publish Reel</button>
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
          <select id="withdrawMethod" class="w-full bg-gray-900 border border-gray-700 p-2.5 rounded-lg mt-1 text-white">
            <option value="EasyPaisa">EasyPaisa</option>
            <option value="JazzCash">JazzCash</option>
          </select>
        </div>
        <div>
          <label class="text-gray-400">Account Number / Phone</label>
          <input id="withdrawAccount" type="text" placeholder="03XXXXXXXXX" class="w-full bg-gray-900 border border-gray-700 p-2.5 rounded-lg mt-1 text-white" />
        </div>
        <div>
          <label class="text-gray-400">Withdraw Amount (Min PKR 500)</label>
          <input id="withdrawAmount" type="number" placeholder="500" class="w-full bg-gray-900 border border-gray-700 p-2.5 rounded-lg mt-1 text-white" />
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
        <input id="authEmail" type="email" placeholder="Email Address" class="w-full bg-gray-900 border border-gray-700 p-2.5 rounded-lg text-sm text-white focus:outline-none" />
        <input id="authPassword" type="password" placeholder="Password" class="w-full bg-gray-900 border border-gray-700 p-2.5 rounded-lg text-sm text-white focus:outline-none" />
        <button onclick="loginWithEmail()" class="w-full bg-blue-600 hover:bg-blue-700 py-2.5 rounded-lg text-sm font-semibold text-white">Login / Sign Up</button>
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
      <input id="adminKeyInput" type="password" placeholder="Enter Key (5426)" class="w-full bg-gray-900 border border-gray-700 p-2.5 rounded-lg text-center tracking-widest text-sm text-white focus:outline-none" />
      <div class="flex space-x-2">
        <button onclick="verifyAdminKey()" class="flex-1 bg-purple-600 py-2 rounded-lg text-xs font-bold text-white">Unlock</button>
        <button onclick="toggleModal('adminKeyModal')" class="flex-1 bg-gray-800 py-2 rounded-lg text-xs text-white">Cancel</button>
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
        <select id="depositMethod" class="w-full bg-gray-900 border border-gray-700 p-2.5 rounded-lg text-white">
          <option value="EasyPaisa">EasyPaisa (03379827882)</option>
          <option value="JazzCash">JazzCash (03705519562)</option>
        </select>
        <input id="depositAmount" type="number" placeholder="Amount Sent (PKR)" class="w-full bg-gray-900 border border-gray-700 p-2.5 rounded-lg text-white" />
        <input id="depositTID" type="text" placeholder="Transaction ID (TID)" class="w-full bg-gray-900 border border-gray-700 p-2.5 rounded-lg text-white" />
        <button onclick="submitDeposit()" class="w-full bg-emerald-600 py-2.5 rounded-lg font-bold text-white">Submit Top-up Request</button>
      </div>
    </div>
  </div>

  <!-- FIREBASE ENGINE & EXTENDED CORE LOGIC -->
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
    let activeInspectedUid = null;
    let activeChatTargetUid = null;
    let globalPostsCache = {};

    onAuthStateChanged(auth, async (user) => {
      currentUser = user;
      if (user) {
        document.getElementById('authNavButtons').classList.add('hidden');
        document.getElementById('userNavProfile').classList.remove('hidden');
        
        const profileSnap = await get(ref(db, `users/${user.uid}`));
        const displayName = profileSnap.exists() && profileSnap.val().displayName 
          ? profileSnap.val().displayName 
          : (user.displayName || user.email.split('@')[0]);

        document.getElementById('navUserName').innerText = displayName;
        loadUserWallet(user.uid);
        checkVerificationStatus(user.uid);
        listenNotifications(user.uid);
        loadSavedBookmarks();
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
        document.getElementById('statMonetization').innerText = `PKR ${bal}`;
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

    // DIRECT MESSAGES (CHAT) SYSTEM
    window.openChatModal = async () => {
      if (!currentUser) return alert("Please login first, sweetie!");
      toggleModal('chatModal');
      loadChatUsers();
    };

    async function loadChatUsers() {
      const snap = await get(ref(db, 'users'));
      const list = document.getElementById('chatUsersList');
      list.innerHTML = '';
      if (!snap.exists()) return;

      Object.entries(snap.val()).forEach(([uid, uData]) => {
        if (uid !== currentUser.uid) {
          const div = document.createElement('div');
          div.className = "p-2 bg-gray-900 hover:bg-gray-800 rounded-lg cursor-pointer flex items-center gap-2 text-xs";
          div.onclick = () => selectChatUser(uid, uData.displayName || 'User');
          div.innerHTML = `<div class="w-6 h-6 rounded-full bg-blue-600 flex items-center justify-center font-bold text-[10px] text-white">${(uData.displayName || 'U').charAt(0).toUpperCase()}</div><span class="truncate">${uData.displayName || 'User'}</span>`;
          list.appendChild(div);
        }
      });
    }

    window.startDirectMessage = () => {
      if (!activeInspectedUid) return;
      toggleModal('userProfileModal');
      toggleModal('chatModal');
      selectChatUser(activeInspectedUid, document.getElementById('viewProfileName').innerText);
    };

    function selectChatUser(targetUid, name) {
      activeChatTargetUid = targetUid;
      const chatId = currentUser.uid < targetUid ? `${currentUser.uid}_${targetUid}` : `${targetUid}_${currentUser.uid}`;
      
      onValue(ref(db, `chats/${chatId}`), (snapshot) => {
        const box = document.getElementById('chatMessagesBox');
        box.innerHTML = '';
        const data = snapshot.val();
        if (!data) {
          box.innerHTML = `<p class="text-[11px] text-gray-500 text-center py-10">Chatting with ${name}. Say hi!</p>`;
          return;
        }
        Object.values(data).forEach(msg => {
          const isMe = msg.senderUid === currentUser.uid;
          const msgDiv = document.createElement('div');
          msgDiv.className = `flex ${isMe ? 'justify-end' : 'justify-start'}`;
          msgDiv.innerHTML = `<div class="${isMe ? 'bg-blue-600 text-white' : 'bg-gray-800 text-gray-200'} text-xs p-2 rounded-lg max-w-[80%]">${msg.text}</div>`;
          box.appendChild(msgDiv);
        });
        box.scrollTop = box.scrollHeight;
      });
    }

    window.sendChatMessage = async () => {
      if (!currentUser || !activeChatTargetUid) return;
      const text = document.getElementById('chatInput').value.trim();
      if (!text) return;

      const chatId = currentUser.uid < activeChatTargetUid ? `${currentUser.uid}_${activeChatTargetUid}` : `${activeChatTargetUid}_${currentUser.uid}`;
      const msgRef = push(ref(db, `chats/${chatId}`));
      await set(msgRef, {
        senderUid: currentUser.uid,
        text,
        timestamp: Date.now()
      });

      // Trigger Notification to Receiver
      pushNotification(activeChatTargetUid, `${currentUser.displayName || 'Someone'} sent you a message!`);

      document.getElementById('chatInput').value = '';
    };

    // NOTIFICATIONS SYSTEM
    function listenNotifications(uid) {
      onValue(ref(db, `notifications/${uid}`), (snapshot) => {
        const list = document.getElementById('notificationsList');
        const badge = document.getElementById('notifBadge');
        list.innerHTML = '';
        const data = snapshot.val();

        if (data) {
          badge.classList.remove('hidden');
          Object.values(data).reverse().forEach(n => {
            const div = document.createElement('div');
            div.className = "p-2 bg-gray-900 rounded-lg text-xs border border-gray-800 text-gray-300";
            div.innerText = n.message;
            list.appendChild(div);
          });
        } else {
          badge.classList.add('hidden');
          list.innerHTML = '<p class="text-xs text-gray-500 text-center py-4">No notifications yet.</p>';
        }
      });
    }

    async function pushNotification(targetUid, message) {
      if (targetUid === currentUser.uid) return;
      const notifRef = push(ref(db, `notifications/${targetUid}`));
      await set(notifRef, { message, timestamp: Date.now() });
    }

    window.openNotificationsModal = () => {
      if (!currentUser) return;
      toggleModal('notificationsModal');
    };

    // BOOKMARKS & SAVED POSTS
    window.toggleBookmarkPost = async (postKey) => {
      if (!currentUser) return alert("Please login first!");
      const bookmarkRef = ref(db, `bookmarks/${currentUser.uid}/${postKey}`);
      const snap = await get(bookmarkRef);
      if (snap.exists()) {
        await remove(bookmarkRef);
        alert("Removed from saved bookmarks!");
      } else {
        await set(bookmarkRef, true);
        alert("Saved to bookmarks!");
      }
      loadSavedBookmarks();
    };

    async function loadSavedBookmarks() {
      if (!currentUser) return;
      onValue(ref(db, `bookmarks/${currentUser.uid}`), async (snapshot) => {
        const container = document.getElementById('savedPostsContainer');
        container.innerHTML = '';
        const data = snapshot.val();
        if (!data) {
          container.innerHTML = '<p class="text-center text-xs text-gray-500 py-10">No saved posts yet.</p>';
          return;
        }
        for (const postKey of Object.keys(data)) {
          const pSnap = await get(ref(db, `posts/${postKey}`));
          if (pSnap.exists()) {
            const post = pSnap.val();
            const el = document.createElement('div');
            el.className = "glassmorphism p-4 rounded-xl space-y-3";
            el.innerHTML = `<p class="font-bold text-sm text-blue-400">${post.author}</p><p class="text-xs text-gray-300">${post.content}</p>`;
            container.appendChild(el);
          }
        }
      });
    }

    // SEARCH FILTER LOGIC
    window.filterFeedPosts = () => {
      const query = document.getElementById('searchInput').value.toLowerCase();
      const posts = document.querySelectorAll('#postsFeed > div');
      posts.forEach(post => {
        const text = post.innerText.toLowerCase();
        if (text.includes(query)) post.style.display = "block";
        else post.style.display = "none";
      });
    };

    // PROFILE SYSTEM
    window.openMyProfileModal = async () => {
      if (!currentUser) return alert("Please login first!");
      const profileSnap = await get(ref(db, `users/${currentUser.uid}`));
      if (profileSnap.exists()) {
        const data = profileSnap.val();
        document.getElementById('editDisplayName').value = data.displayName || currentUser.displayName || '';
        document.getElementById('editUserBio').value = data.bio || '';
      }
      toggleModal('editProfileModal');
    };

    window.saveUserProfile = async () => {
      if (!currentUser) return;
      const displayName = document.getElementById('editDisplayName').value.trim();
      const bio = document.getElementById('editUserBio').value.trim();
      if (!displayName) return alert("Name is required!");

      await update(ref(db, `users/${currentUser.uid}`), { displayName, bio });
      document.getElementById('navUserName').innerText = displayName;
      toggleModal('editProfileModal');
      alert("Profile updated successfully!");
    };

    window.inspectUserProfile = async (targetUid) => {
      activeInspectedUid = targetUid;
      const userSnap = await get(ref(db, `users/${targetUid}`));
      const isVerifiedSnap = await get(ref(db, `verifiedUsers/${targetUid}`));
      const isVerified = isVerifiedSnap.exists() && isVerifiedSnap.val() === true;

      let name = "User";
      let bio = "No bio available yet.";
      if (userSnap.exists()) {
        name = userSnap.val().displayName || name;
        bio = userSnap.val().bio || bio;
      }

      document.getElementById('viewProfileAvatar').innerText = name.charAt(0).toUpperCase();
      document.getElementById('viewProfileName').innerHTML = `${name} ${isVerified ? '<span class="text-blue-400 text-xs"><i class="fa-solid fa-circle-check"></i></span>' : ''}`;
      document.getElementById('viewProfileBio').innerText = bio;

      onValue(ref(db, `followers/${targetUid}`), (snap) => {
        document.getElementById('viewProfileFollowersCount').innerText = snap.exists() ? Object.keys(snap.val()).length : 0;
      });

      onValue(ref(db, `following/${targetUid}`), (snap) => {
        document.getElementById('viewProfileFollowingCount').innerText = snap.exists() ? Object.keys(snap.val()).length : 0;
      });

      const followBtn = document.getElementById('viewProfileFollowBtn');
      if (currentUser && currentUser.uid === targetUid) {
        followBtn.classList.add('hidden');
      } else {
        followBtn.classList.remove('hidden');
        if (currentUser) {
          const checkFollowSnap = await get(ref(db, `followers/${targetUid}/${currentUser.uid}`));
          followBtn.innerText = checkFollowSnap.exists() ? "Unfollow" : "Follow";
        }
      }
      toggleModal('userProfileModal');
    };

    window.toggleFollowUser = async () => {
      if (!currentUser || !activeInspectedUid) return alert("Please login first!");
      const followerRef = ref(db, `followers/${activeInspectedUid}/${currentUser.uid}`);
      const followingRef = ref(db, `following/${currentUser.uid}/${activeInspectedUid}`);
      
      const snap = await get(followerRef);
      if (snap.exists()) {
        await remove(followerRef);
        await remove(followingRef);
      } else {
        await set(followerRef, true);
        await set(followingRef, true);
        pushNotification(activeInspectedUid, `${currentUser.displayName || 'Someone'} started following you!`);
      }
      inspectUserProfile(activeInspectedUid);
    };

    // INSTAGRAM STORIES
    onValue(ref(db, 'stories'), (snapshot) => {
      const container = document.getElementById('storiesContainer'); container.innerHTML = '';
      const data = snapshot.val(); if (!data) return;
      const now = Date.now();
      Object.values(data).forEach(story => {
        if (now - story.timestamp < 24 * 60 * 60 * 1000) {
          const div = document.createElement('div');
          div.className = "flex-shrink-0 flex flex-col items-center cursor-pointer";
          div.onclick = () => viewStory(story);
          div.innerHTML = `
            <div class="w-14 h-14 rounded-full p-[2px] bg-gradient-to-tr from-yellow-400 via-red-500 to-purple-500">
              <div class="w-full h-full rounded-full bg-gray-900 border-2 border-black flex items-center justify-center font-bold text-xs text-white uppercase overflow-hidden">
                ${story.author.charAt(0)}
              </div>
            </div>
            <span class="text-[10px] mt-1 text-gray-300">${story.author.substring(0, 8)}</span>
          `;
          container.appendChild(div);
        }
      });
    });

    window.openAddStoryModal = () => { if (!currentUser) return alert("Please login first!"); toggleModal('addStoryModal'); };
    window.submitStory = async () => {
      const file = document.getElementById('storyFileInput').files[0];
      if (!file) return alert("Select media first!");
      const profileSnap = await get(ref(db, `users/${currentUser.uid}`));
      const authorName = profileSnap.exists() && profileSnap.val().displayName ? profileSnap.val().displayName : (currentUser.displayName || currentUser.email.split('@')[0]);

      const reader = new FileReader();
      reader.onloadend = async () => {
        const type = file.type.startsWith('image') ? 'image' : 'video';
        const storyRef = push(ref(db, 'stories'));
        await set(storyRef, { author: authorName, uid: currentUser.uid, media: reader.result, mediaType: type, timestamp: Date.now() });
        toggleModal('addStoryModal'); alert("Story published!");
      };
      reader.readAsDataURL(file);
    };

    function viewStory(story) {
      document.getElementById('storyAuthor').innerText = story.author + "'s Story";
      if (story.mediaType === 'image') {
        document.getElementById('storyImageDisplay').src = story.media;
        document.getElementById('storyImageDisplay').classList.remove('hidden');
        document.getElementById('storyVideoDisplay').classList.add('hidden');
      } else {
        document.getElementById('storyVideoDisplay').src = story.media;
        document.getElementById('storyVideoDisplay').classList.remove('hidden');
        document.getElementById('storyImageDisplay').classList.add('hidden');
      }
      toggleModal('viewStoryModal');
    }

    // TIKTOK DUETS & REELS
    window.openDuetModal = (videoUrl) => {
      if (!currentUser) return alert("Please login first!");
      document.getElementById('duetOriginalUrl').value = videoUrl;
      document.getElementById('duetOriginalPreview').src = videoUrl;
      toggleModal('duetModal');
    };

    window.submitDuetReel = async () => {
      const originalUrl = document.getElementById('duetOriginalUrl').value;
      const file = document.getElementById('duetVideoInput').files[0];
      if (!file) return alert("Select your video!");
      const profileSnap = await get(ref(db, `users/${currentUser.uid}`));
      const authorName = profileSnap.exists() && profileSnap.val().displayName ? profileSnap.val().displayName : (currentUser.displayName || currentUser.email.split('@')[0]);

      const reader = new FileReader();
      reader.onloadend = async () => {
        const reelRef = push(ref(db, 'reels'));
        await set(reelRef, { author: authorName, uid: currentUser.uid, title: "Duet with Creator", videoBase64: originalUrl, duetVideoBase64: reader.result, isDuet: true, timestamp: Date.now() });
        toggleModal('duetModal'); alert("Duet Reel published!");
      };
      reader.readAsDataURL(file);
    };

    onValue(ref(db, 'reels'), (snapshot) => {
      const container = document.getElementById('reelsContainer'); container.innerHTML = '';
      const data = snapshot.val(); if (!data) return;
      Object.values(data).reverse().forEach(reel => {
        const div = document.createElement('div');
        div.className = "reel-card relative h-full bg-black rounded-xl overflow-hidden flex items-center justify-center border border-gray-800";
        if (reel.isDuet) {
          div.innerHTML = `<div class="grid grid-cols-2 w-full h-full"><video src="${reel.videoBase64}" controls loop class="w-full h-full object-cover"></video><video src="${reel.duetVideoBase64}" controls loop class="w-full h-full object-cover"></video></div><div class="absolute bottom-4 left-4 space-y-1 z-10 bg-black/50 p-2 rounded-lg"><span class="text-[9px] bg-red-600 text-white font-bold px-1.5 py-0.5 rounded">TikTok Duet</span><p class="font-bold text-sm text-white cursor-pointer" onclick="inspectUserProfile('${reel.uid}')">${reel.author}</p><p class="text-xs text-gray-300">${reel.title}</p></div>`;
        } else {
          div.innerHTML = `<video src="${reel.videoBase64}" controls loop class="w-full h-full object-cover"></video><div class="absolute bottom-4 left-4 space-y-1 bg-black/50 p-2 rounded-lg z-10"><p class="font-bold text-sm text-white cursor-pointer" onclick="inspectUserProfile('${reel.uid}')">${reel.author}</p><p class="text-xs text-gray-300">${reel.title}</p><button onclick="openDuetModal('${reel.videoBase64}')" class="text-[10px] bg-red-600 text-white font-bold px-2 py-1 rounded flex items-center gap-1 mt-1"><i class="fa-solid fa-duet"></i> Duet React</button></div>`;
        }
        container.appendChild(div);
      });
    });

    // MEDIA PREVIEW & FEED
    window.previewMedia = (input, type) => {
      const file = input.files[0]; if (!file) return;
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
      selectedMediaBase64 = null; selectedMediaType = null;
      document.getElementById('mediaPreviewContainer').classList.add('hidden');
      document.getElementById('imageInput').value = ''; document.getElementById('videoInput').value = '';
    };

    window.submitPost = async () => {
      if (!currentUser) return alert("Please login first!");
      const content = document.getElementById('postInput').value;
      if (!content && !selectedMediaBase64) return alert("Add content first!");

      const isVerifiedSnap = await get(ref(db, `verifiedUsers/${currentUser.uid}`));
      const isVerified = isVerifiedSnap.exists() && isVerifiedSnap.val() === true;
      const profileSnap = await get(ref(db, `users/${currentUser.uid}`));
      const authorName = profileSnap.exists() && profileSnap.val().displayName ? profileSnap.val().displayName : (currentUser.displayName || currentUser.email.split('@')[0]);

      const postRef = push(ref(db, 'posts'));
      await set(postRef, {
        author: authorName, uid: currentUser.uid, isVerified, content,
        media: selectedMediaBase64 || null, mediaType: selectedMediaType || null,
        likes: 0, views: 1, isBoosted: false, timestamp: Date.now()
      });

      document.getElementById('postInput').value = ''; clearMedia(); alert("Post published live!");
    };

    window.submitReel = async () => {
      if (!currentUser) return alert("Please login first!");
      const title = document.getElementById('reelTitleInput').value;
      const file = document.getElementById('reelVideoFile').files[0];
      if (!title || !file) return alert("Fill all details!");

      const profileSnap = await get(ref(db, `users/${currentUser.uid}`));
      const authorName = profileSnap.exists() && profileSnap.val().displayName ? profileSnap.val().displayName : (currentUser.displayName || currentUser.email.split('@')[0]);

      const reader = new FileReader();
      reader.onloadend = async () => {
        const reelRef = push(ref(db, 'reels'));
        await set(reelRef, { author: authorName, uid: currentUser.uid, title, videoBase64: reader.result, timestamp: Date.now() });
        toggleModal('uploadReelModal'); alert("Reel published!");
      };
      reader.readAsDataURL(file);
    };

    // LIKES & COMMENTS ENGINE
    window.toggleLikePost = async (postKey) => {
      if (!currentUser) return alert("Please login first!");
      const postRef = ref(db, `posts/${postKey}`);
      const snap = await get(postRef);
      if (snap.exists()) {
        const postData = snap.val();
        const likedBy = postData.likedBy || {};
        const isLiked = likedBy[currentUser.uid];

        if (isLiked) delete likedBy[currentUser.uid];
        else {
          likedBy[currentUser.uid] = true;
          pushNotification(postData.uid, `${currentUser.displayName || 'Someone'} liked your post!`);
        }
        await update(postRef, { likes: Object.keys(likedBy).length, likedBy });
      }
    };

    window.openCommentsModal = (postKey) => {
      document.getElementById('activePostKey').value = postKey;
      toggleModal('commentsModal'); loadComments(postKey);
    };

    function loadComments(postKey) {
      onValue(ref(db, `posts/${postKey}/comments`), (snapshot) => {
        const list = document.getElementById('commentsList'); list.innerHTML = '';
        const data = snapshot.val(); if (!data) { list.innerHTML = '<p class="text-center text-xs text-gray-500 py-4">No comments yet.</p>'; return; }
        Object.values(data).forEach(c => {
          const item = document.createElement('div');
          item.className = "p-2 bg-gray-900 rounded-lg text-xs space-y-0.5";
          item.innerHTML = `<span class="font-bold text-blue-400 cursor-pointer" onclick="inspectUserProfile('${c.uid}')">${c.author}: </span><span class="text-gray-300">${c.text}</span>`;
          list.appendChild(item);
        });
      });
    }

    window.submitComment = async () => {
      if (!currentUser) return alert("Please login first!");
      const postKey = document.getElementById('activePostKey').value;
      const text = document.getElementById('commentInput').value.trim();
      if (!text) return;

      const profileSnap = await get(ref(db, `users/${currentUser.uid}`));
      const authorName = profileSnap.exists() && profileSnap.val().displayName ? profileSnap.val().displayName : (currentUser.displayName || currentUser.email.split('@')[0]);

      const commentRef = push(ref(db, `posts/${postKey}/comments`));
      await set(commentRef, { author: authorName, uid: currentUser.uid, text, timestamp: Date.now() });
      
      const pSnap = await get(ref(db, `posts/${postKey}`));
      if (pSnap.exists()) pushNotification(pSnap.val().uid, `${authorName} commented on your post!`);

      document.getElementById('commentInput').value = '';
    };

    window.sharePost = (postKey) => {
      if (navigator.share) navigator.share({ title: 'PrimeX Post', url: window.location.href });
      else { navigator.clipboard.writeText(window.location.href); alert("Link copied!"); }
    };

    // BOOST POST & VERIFICATION
    window.openBoostModal = (postKey) => { if (!currentUser) return alert("Please login first!"); document.getElementById('boostPostKey').value = postKey; toggleModal('boostModal'); };
    window.confirmBoostPost = async () => {
      const postKey = document.getElementById('boostPostKey').value;
      const cost = parseFloat(document.getElementById('boostPackage').value);
      const walletRef = ref(db, `wallets/${currentUser.uid}/balance`);
      const snap = await get(walletRef);
      const currentBal = snap.exists() ? snap.val() : 0;

      if (currentBal < cost) return alert("Insufficient balance!");

      await set(walletRef, currentBal - cost);
      await update(ref(db, `posts/${postKey}`), { isBoosted: true });
      toggleModal('boostModal'); alert("Post boosted successfully!");
    };

    window.purchaseVerification = async () => {
      if (!currentUser) return alert("Please login first!");
      const cost = 999;
      const walletRef = ref(db, `wallets/${currentUser.uid}/balance`);
      const snap = await get(walletRef);
      const currentBal = snap.exists() ? snap.val() : 0;

      if (currentBal < cost) return alert("Insufficient balance! PKR 999 required.");

      await set(walletRef, currentBal - cost);
      await set(ref(db, `verifiedUsers/${currentUser.uid}`), true);
      toggleModal('verifyModal'); alert("Verified Blue Tick active!");
    };

    // DEPOSIT MANUAL & WITHDRAW
    window.submitDeposit = async () => {
      if (!currentUser) return;
      const method = document.getElementById('depositMethod').value;
      const amount = parseFloat(document.getElementById('depositAmount').value);
      const tid = document.getElementById('depositTID').value;
      if (!amount || !tid) return alert("Fill all fields!");

      const refReq = push(ref(db, 'deposits'));
      await set(refReq, { id: refReq.key, uid: currentUser.uid, email: currentUser.email, method, amount, tid, status: 'pending', timestamp: Date.now() });
      toggleModal('depositModal'); alert("Top-up request sent!");
    };

    // FEED RENDER ENGINE
    onValue(ref(db, 'posts'), (snapshot) => {
      const feed = document.getElementById('postsFeed'); feed.innerHTML = '';
      const data = snapshot.val(); if (!data) return;
      
      let calcViews = 0;
      const postsArray = Object.entries(data);
      postsArray.sort((a, b) => (b[1].isBoosted ? 1 : 0) - (a[1].isBoosted ? 1 : 0));

      postsArray.forEach(([key, post]) => {
        calcViews += (post.views || 1);
        const commentCount = post.comments ? Object.keys(post.comments).length : 0;
        const likedBy = post.likedBy || {};
        const isLikedByMe = currentUser && likedBy[currentUser.uid];
        const likesCount = Object.keys(likedBy).length;

        const el = document.createElement('div');
        el.className = `glassmorphism p-4 rounded-xl space-y-3 ${post.isBoosted ? 'border border-amber-500/50 bg-amber-950/10' : ''}`;
        el.innerHTML = `
          ${post.isBoosted ? '<span class="text-[10px] bg-amber-500 text-black font-bold px-2 py-0.5 rounded uppercase"><i class="fa-solid fa-bullhorn"></i> Sponsored Ad</span>' : ''}
          <div class="flex justify-between items-center">
            <div class="flex items-center space-x-2">
              <div class="w-8 h-8 rounded-full bg-gradient-to-tr from-blue-500 to-purple-500 flex items-center justify-center font-bold text-xs cursor-pointer" onclick="inspectUserProfile('${post.uid}')">${post.author.charAt(0).toUpperCase()}</div>
              <div>
                <p class="text-sm font-bold flex items-center gap-1 cursor-pointer hover:underline" onclick="inspectUserProfile('${post.uid}')">
                  ${post.author} ${post.isVerified ? '<span class="text-blue-400 text-xs"><i class="fa-solid fa-circle-check"></i></span>' : ''}
                </p>
                <p class="text-[10px] text-gray-500">${new Date(post.timestamp).toLocaleTimeString()}</p>
              </div>
            </div>
            <div class="flex items-center gap-2">
              <button onclick="toggleBookmarkPost('${key}')" class="text-gray-400 hover:text-yellow-400 text-xs"><i class="fa-solid fa-bookmark"></i></button>
              ${currentUser && currentUser.uid === post.uid && !post.isBoosted ? `<button onclick="openBoostModal('${key}')" class="text-[10px] bg-amber-600 hover:bg-amber-700 text-black font-bold px-2.5 py-1 rounded-lg">Boost</button>` : ''}
            </div>
          </div>
          <p class="text-sm text-gray-300">${post.content}</p>
          ${post.media && post.mediaType === 'image' ? `<img src="${post.media}" class="w-full h-64 object-cover rounded-lg" />` : ''}
          ${post.media && post.mediaType === 'video' ? `<video src="${post.media}" controls class="w-full h-64 object-cover rounded-lg"></video>` : ''}
          <div class="flex justify-between items-center text-xs text-gray-400 pt-2 border-t border-gray-800">
            <button onclick="toggleLikePost('${key}')" class="flex items-center gap-1 ${isLikedByMe ? 'text-red-500 font-bold' : 'hover:text-red-400'}">
              <i class="${isLikedByMe ? 'fa-solid' : 'fa-regular'} fa-heart"></i> <span>${likesCount} Likes</span>
            </button>
            <button onclick="openCommentsModal('${key}')" class="flex items-center gap-1 hover:text-blue-400">
              <i class="fa-regular fa-comment"></i> <span>${commentCount} Comments</span>
            </button>
            <button onclick="sharePost('${key}')" class="flex items-center gap-1 hover:text-green-400">
              <i class="fa-solid fa-share"></i> <span>Share</span>
            </button>
            <span class="text-gray-500"><i class="fa-regular fa-eye"></i> ${post.views || 1} Views</span>
          </div>
        `;
        feed.appendChild(el);
      });
      document.getElementById('statTotalViews').innerText = calcViews;
    });

    // SECRET ADMIN PANEL
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
        const container = document.getElementById('depositRequestsContainer'); container.innerHTML = '';
        const data = snapshot.val(); if (!data) return;
        Object.entries(data).reverse().forEach(([key, item]) => {
          if (item.status === 'pending') {
            const div = document.createElement('div');
            div.className = "p-3 bg-gray-900 rounded-lg border border-gray-800 flex justify-between items-center text-xs";
            div.innerHTML = `<div><p class="font-bold">${item.email}</p><p class="text-green-400">${item.method}: PKR ${item.amount} (TID: ${item.tid})</p></div><button onclick="approveDeposit('${key}', '${item.uid}', ${item.amount})" class="bg-green-600 px-2 py-1 rounded text-white font-bold">Approve</button>`;
            container.appendChild(div);
          }
        });
      });

      onValue(ref(db, 'withdrawals'), (snapshot) => {
        const container = document.getElementById('withdrawRequestsContainer'); container.innerHTML = '';
        const data = snapshot.val(); if (!data) return;
        Object.entries(data).reverse().forEach(([key, item]) => {
          if (item.status === 'pending') {
            const div = document.createElement('div');
            div.className = "p-3 bg-gray-900 rounded-lg border border-gray-800 flex justify-between items-center text-xs";
            div.innerHTML = `<div><p class="font-bold">${item.email}</p><p class="text-amber-400">${item.method}: PKR ${item.amount} (Acc: ${item.account})</p></div><button onclick="approveWithdrawal('${key}')" class="bg-amber-600 px-2 py-1 rounded text-black font-bold">Mark Paid</button>`;
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
      alert("Top-up approved!");
    };

    window.approveWithdrawal = async (wKey) => {
      await update(ref(db, `withdrawals/${wKey}`), { status: 'approved' });
      alert("Withdrawal marked as Paid!");
    };

    window.requestWithdrawal = async () => {
      if (!currentUser) return;
      const method = document.getElementById('withdrawMethod').value;
      const account = document.getElementById('withdrawAccount').value;
      const amount = parseFloat(document.getElementById('withdrawAmount').value);
      if (!account || !amount || amount < 500) return alert("Min PKR 500 required!");

      const walletRef = ref(db, `wallets/${currentUser.uid}/balance`);
      const snap = await get(walletRef);
      const currentBal = snap.exists() ? snap.val() : 0;
      if (currentBal < amount) return alert("Insufficient balance!");

      await set(walletRef, currentBal - amount);
      const wRef = push(ref(db, 'withdrawals'));
      await set(wRef, { uid: currentUser.uid, email: currentUser.email, method, account, amount, status: 'pending', timestamp: Date.now() });
      alert("Withdrawal requested!"); toggleModal('walletModal');
    };
  </script>

  <script>
    function toggleModal(id) { const el = document.getElementById(id); el.classList.toggle('hidden'); el.classList.toggle('flex'); }
    function openDepositModal() { toggleModal('depositModal'); }
    function openWalletModal() { toggleModal('walletModal'); }
    function openUploadReelModal() { toggleModal('uploadReelModal'); }
    function openVerifyModal() { toggleModal('verifyModal'); }
    function openAnalyticsModal() { toggleModal('analyticsModal'); }
    function openBoostInfo() { alert("Boost Feature: Pay a small fee to pin your post on top of everyone's feed!"); }
    function joinCommunity(name) { alert("Welcome to " + name + " community group!"); }
    
    function switchTab(tab) {
      document.getElementById('feedTab').classList.add('hidden');
      document.getElementById('reelsTab').classList.add('hidden');
      document.getElementById('savedTab').classList.add('hidden');
      document.getElementById('groupsTab').classList.add('hidden');
      if (tab === 'feed') document.getElementById('feedTab').classList.remove('hidden');
      if (tab === 'reels') document.getElementById('reelsTab').classList.remove('hidden');
      if (tab === 'saved') document.getElementById('savedTab').classList.remove('hidden');
      if (tab === 'groups') document.getElementById('groupsTab').classList.remove('hidden');
    }
  </script>
</body>
</html>
