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
    body { background-color: #0b0f19; color: #f3f4f6; font-family: 'Inter', sans-serif; padding-bottom: 60px; transition: background 0.3s, color 0.3s; }
    body.light-theme { background-color: #f3f4f6; color: #1f2937; }
    body.light-theme .glassmorphism { background: rgba(255, 255, 255, 0.85); border: 1px solid rgba(0, 0, 0, 0.08); color: #1f2937; }
    body.light-theme input, body.light-theme textarea, body.light-theme select { background-color: #ffffff !important; color: #1f2937 !important; border-color: #d1d5db !important; }
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

    <div class="flex items-center space-x-2">
      <!-- THEME TOGGLE BUTTON -->
      <button onclick="toggleTheme()" class="text-gray-300 hover:text-white p-1.5 text-sm" title="Toggle Theme"><i class="fa-solid fa-circle-half-stroke"></i></button>

      <div id="authNavButtons" class="flex items-center space-x-3">
        <button onclick="toggleModal('authModal')" class="bg-blue-600 hover:bg-blue-700 text-sm font-semibold px-4 py-2 rounded-lg transition text-white">Login / Register</button>
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

        <button onclick="openWalletModal()" class="bg-gradient-to-r from-amber-500 to-yellow-600 text-xs font-bold px-2.5 py-1.5 rounded-lg hover:opacity-90 flex items-center gap-1 text-black">
          <i class="fa-solid fa-coins"></i> <span id="navWalletBalance">PKR 0</span>
        </button>
        <button onclick="openDepositModal()" class="bg-gradient-to-r from-green-500 to-emerald-600 text-xs font-bold px-2.5 py-1.5 rounded-lg hover:opacity-90 flex items-center gap-1 text-white">
          <i class="fa-solid fa-wallet"></i> <span class="hidden sm:inline">Top-up</span>
        </button>
        <div class="flex items-center gap-2 cursor-pointer" onclick="openMyProfileModal()">
          <img id="navUserAvatarImg" class="w-7 h-7 rounded-full object-cover hidden border border-blue-500" />
          <div id="navUserAvatarFallback" class="w-7 h-7 rounded-full bg-blue-600 flex items-center justify-center font-bold text-xs text-white">U</div>
          <span id="navUserName" class="text-sm font-medium text-gray-300 hover:text-blue-400 transition"></span>
          <span id="navVerifiedBadge" class="hidden text-blue-400 text-xs" title="Verified Creator"><i class="fa-solid fa-circle-check"></i></span>
        </div>
        <button onclick="logout()" class="text-gray-400 hover:text-red-400 text-sm pl-1"><i class="fa-solid fa-right-from-bracket"></i></button>
      </div>
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
          <i class="fa-solid fa-clapperboard text-red-500 text-lg"></i> <span class="font-medium">PrimeX Reels</span>
        </button>
        <button onclick="switchTab('marketplace')" class="w-full flex items-center space-x-3 text-gray-300 hover:text-white p-2 rounded-lg hover:bg-gray-800/50 transition">
          <i class="fa-solid fa-store text-emerald-400 text-lg"></i> <span class="font-medium">Marketplace</span>
        </button>
        <button onclick="switchTab('live')" class="w-full flex items-center space-x-3 text-gray-300 hover:text-white p-2 rounded-lg hover:bg-gray-800/50 transition">
          <i class="fa-solid fa-video text-amber-400 text-lg"></i> <span class="font-medium">Live Streams</span>
        </button>
        <button onclick="switchTab('saved')" class="w-full flex items-center space-x-3 text-gray-300 hover:text-white p-2 rounded-lg hover:bg-gray-800/50 transition">
          <i class="fa-solid fa-bookmark text-yellow-500 text-lg"></i> <span class="font-medium">Saved Bookmarks</span>
        </button>
        <button onclick="switchTab('groups')" class="w-full flex items-center space-x-3 text-gray-300 hover:text-white p-2 rounded-lg hover:bg-gray-800/50 transition">
          <i class="fa-solid fa-users text-green-400 text-lg"></i> <span class="font-medium">Communities</span>
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
      </div>
    </aside>

    <!-- CENTER CONTENT AREA -->
    <main class="col-span-1 md:col-span-2 space-y-6">

      <!-- PRIME STORIES BAR -->
      <div class="glassmorphism p-3 rounded-xl">
        <h3 class="text-xs font-bold text-gray-400 mb-2 uppercase tracking-wider">PrimeX Stories</h3>
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
          <textarea id="postInput" rows="2" placeholder="What's happening on PrimeX? Use #hashtags" class="w-full bg-gray-900 border border-gray-700 rounded-lg p-3 text-sm focus:outline-none focus:border-blue-500 resize-none text-white"></textarea>
          
          <div id="mediaPreviewContainer" class="hidden relative">
            <img id="imagePreview" class="w-full h-40 object-cover rounded-lg hidden" />
            <video id="videoPreview" class="w-full h-40 object-cover rounded-lg hidden" controls></video>
            <button onclick="clearMedia()" class="absolute top-2 right-2 bg-red-600 text-white rounded-full w-6 h-6 text-xs flex items-center justify-center"><i class="fa-solid fa-xmark"></i></button>
          </div>

          <!-- POLL CREATION CONTAINER -->
          <div id="pollCreatorContainer" class="hidden space-y-2 p-3 bg-gray-900/60 rounded-lg border border-gray-800">
            <p class="text-xs font-bold text-blue-400">Create Interactive Poll</p>
            <input id="pollQuestion" type="text" placeholder="Ask a question..." class="w-full bg-gray-900 border border-gray-700 p-2 rounded text-xs text-white" />
            <div class="grid grid-cols-2 gap-2">
              <input id="pollOpt1" type="text" placeholder="Option 1" class="bg-gray-900 border border-gray-700 p-2 rounded text-xs text-white" />
              <input id="pollOpt2" type="text" placeholder="Option 2" class="bg-gray-900 border border-gray-700 p-2 rounded text-xs text-white" />
            </div>
          </div>

          <div class="flex justify-between items-center pt-2">
            <div class="flex space-x-3 text-gray-400">
              <label class="cursor-pointer hover:text-blue-400"><i class="fa-regular fa-image text-lg"></i><input type="file" id="imageInput" accept="image/*" class="hidden" onchange="previewMedia(this, 'image')"></label>
              <label class="cursor-pointer hover:text-purple-400"><i class="fa-solid fa-video text-lg"></i><input type="file" id="videoInput" accept="video/*" class="hidden" onchange="previewMedia(this, 'video')"></label>
              <button onclick="togglePollCreator()" class="hover:text-emerald-400 text-lg" title="Add Poll"><i class="fa-solid fa-square-poll-vertical"></i></button>
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
            <i class="fa-solid fa-fire"></i> PrimeX Reels & Duets
          </h2>
          <button onclick="openUploadReelModal()" class="bg-red-600 hover:bg-red-700 text-xs font-bold px-3 py-1.5 rounded-lg flex items-center gap-1 text-white">
            <i class="fa-solid fa-plus"></i> Upload Reel
          </button>
        </div>
        <div id="reelsContainer" class="h-[600px] overflow-y-scroll reel-snap rounded-2xl glassmorphism space-y-4 custom-scrollbar p-2"></div>
      </div>

      <!-- TAB 3: MARKETPLACE -->
      <div id="marketplaceTab" class="hidden space-y-4">
        <div class="flex justify-between items-center">
          <h2 class="text-lg font-bold text-emerald-400 flex items-center gap-2"><i class="fa-solid fa-store"></i> PrimeX Classifieds & Marketplace</h2>
          <button onclick="openAddProductModal()" class="bg-emerald-600 hover:bg-emerald-700 text-xs font-bold px-3 py-1.5 rounded-lg text-white"><i class="fa-solid fa-plus"></i> Sell Item</button>
        </div>
        <div id="marketplaceContainer" class="grid grid-cols-1 sm:grid-cols-2 gap-4"></div>
      </div>

      <!-- TAB 4: LIVE STREAMS -->
      <div id="liveTab" class="hidden space-y-4">
        <div class="flex justify-between items-center">
          <h2 class="text-lg font-bold text-amber-400 flex items-center gap-2"><i class="fa-solid fa-video"></i> Live Broadcasting Rooms</h2>
          <button onclick="startLiveStream()" class="bg-amber-600 hover:bg-amber-700 text-xs font-bold px-3 py-1.5 rounded-lg text-black"><i class="fa-solid fa-broadcast-tower"></i> Go Live</button>
        </div>
        <div id="liveStreamsContainer" class="grid grid-cols-1 sm:grid-cols-2 gap-4"></div>
      </div>

      <!-- TAB 5: SAVED BOOKMARKS -->
      <div id="savedTab" class="hidden space-y-4">
        <h2 class="text-lg font-bold text-yellow-400 flex items-center gap-2"><i class="fa-solid fa-bookmark"></i> Saved Posts</h2>
        <div id="savedPostsContainer" class="space-y-4"></div>
      </div>

      <!-- TAB 6: GROUPS -->
      <div id="groupsTab" class="hidden space-y-4">
        <h2 class="text-lg font-bold text-green-400 flex items-center gap-2"><i class="fa-solid fa-users"></i> Communities</h2>
        <div class="grid grid-cols-1 sm:grid-cols-2 gap-3">
          <div class="glassmorphism p-4 rounded-xl border border-green-500/20 text-center space-y-2">
            <i class="fa-solid fa-code text-2xl text-green-400"></i>
            <h3 class="font-bold text-sm">Tech & Web Developers</h3>
            <p class="text-[11px] text-gray-400">Discuss web apps, APIs & modern tech.</p>
            <button onclick="joinCommunity('Tech Community')" class="bg-green-600 text-xs font-bold px-3 py-1 rounded-lg text-white">Joined</button>
          </div>
          <div class="glassmorphism p-4 rounded-xl border border-blue-500/20 text-center space-y-2">
            <i class="fa-solid fa-mountain text-2xl text-blue-400"></i>
            <h3 class="font-bold text-sm">Global Explorers Club</h3>
            <p class="text-[11px] text-gray-400">Share news, photos & tourism updates.</p>
            <button onclick="joinCommunity('Explorers Club')" class="bg-blue-600 text-xs font-bold px-3 py-1 rounded-lg text-white">Joined</button>
          </div>
        </div>
      </div>

    </main>

    <!-- RIGHT SIDEBAR (TRENDING & ANALYTICS) -->
    <aside class="hidden md:block col-span-1 space-y-4">
      <div class="glassmorphism p-4 rounded-xl space-y-3 border border-indigo-500/30">
        <h3 class="font-bold text-sm text-indigo-400 flex items-center gap-1"><i class="fa-solid fa-fire"></i> Trending Topics</h3>
        <div id="trendingTagsContainer" class="space-y-2 text-xs">
          <p class="text-gray-500 text-center py-2">Analyzing trends...</p>
        </div>
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
      <div id="viewProfileAvatarContainer" class="w-16 h-16 rounded-full mx-auto shadow-lg overflow-hidden flex items-center justify-center bg-blue-600 font-bold text-xl text-white">
        <img id="viewProfileAvatarImg" class="w-full h-full object-cover hidden" />
        <span id="viewProfileAvatarFallback">U</span>
      </div>
      <div>
        <h2 id="viewProfileName" class="text-lg font-bold flex items-center justify-center gap-1 text-white">User Name</h2>
        <p id="viewProfileLocation" class="text-xs text-indigo-400 mt-0.5"></p>
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
    <div class="glassmorphism max-w-sm w-full p-6 rounded-2xl space-y-4 relative max-h-[90vh] overflow-y-auto custom-scrollbar">
      <button onclick="toggleModal('editProfileModal')" class="absolute top-4 right-4 text-gray-400 hover:text-white"><i class="fa-solid fa-xmark"></i></button>
      <h2 class="text-lg font-bold text-center text-indigo-400 flex items-center justify-center gap-2"><i class="fa-solid fa-user-pen"></i> Update Profile</h2>
      <div class="text-center space-y-2">
        <div class="w-20 h-20 rounded-full mx-auto overflow-hidden bg-gray-800 border border-gray-700 flex items-center justify-center">
          <img id="editAvatarPreview" class="w-full h-full object-cover hidden" />
          <span id="editAvatarFallbackTxt" class="text-lg font-bold">U</span>
        </div>
        <label class="inline-block cursor-pointer bg-gray-800 hover:bg-gray-700 text-xs font-semibold px-3 py-1.5 rounded-lg text-white">
          Upload Avatar <input type="file" id="editAvatarInput" accept="image/*" class="hidden" onchange="previewEditAvatar(this)">
        </label>
      </div>
      <div>
        <label class="text-xs text-gray-400">Display Name</label>
        <input id="editDisplayName" type="text" placeholder="Your Full Name..." class="w-full bg-gray-900 border border-gray-700 p-2.5 rounded-lg text-xs mt-1 text-white" />
      </div>
      <div>
        <label class="text-xs text-gray-400">Date of Birth (DOB)</label>
        <input id="editDob" type="date" class="w-full bg-gray-900 border border-gray-700 p-2.5 rounded-lg text-xs mt-1 text-white" />
      </div>
      <div class="grid grid-cols-2 gap-2">
        <div>
          <label class="text-xs text-gray-400">Country</label>
          <input id="editCountry" type="text" placeholder="Country" class="w-full bg-gray-900 border border-gray-700 p-2.5 rounded-lg text-xs mt-1 text-white" />
        </div>
        <div>
          <label class="text-xs text-gray-400">City</label>
          <input id="editCity" type="text" placeholder="City" class="w-full bg-gray-900 border border-gray-700 p-2.5 rounded-lg text-xs mt-1 text-white" />
        </div>
      </div>
      <div>
        <label class="text-xs text-gray-400">Bio</label>
        <textarea id="editUserBio" rows="3" placeholder="Tell something about yourself..." class="w-full bg-gray-900 border border-gray-700 p-2.5 rounded-lg text-xs mt-1 text-white resize-none"></textarea>
      </div>
      <button onclick="saveUserProfile()" class="w-full bg-indigo-600 hover:bg-indigo-700 py-2.5 rounded-lg text-xs font-bold text-white">Save Changes</button>
    </div>
  </div>

  <!-- ADD MARKETPLACE ITEM MODAL -->
  <div id="addProductModal" class="fixed inset-0 bg-black/80 hidden items-center justify-center p-4 z-50">
    <div class="glassmorphism max-w-sm w-full p-6 rounded-2xl space-y-3 relative">
      <button onclick="toggleModal('addProductModal')" class="absolute top-4 right-4 text-gray-400 hover:text-white"><i class="fa-solid fa-xmark"></i></button>
      <h2 class="text-lg font-bold text-emerald-400 text-center">List Product for Sale</h2>
      <input id="prodTitle" type="text" placeholder="Product Name" class="w-full bg-gray-900 border border-gray-700 p-2.5 rounded text-xs text-white" />
      <input id="prodPrice" type="number" placeholder="Price in PKR" class="w-full bg-gray-900 border border-gray-700 p-2.5 rounded text-xs text-white" />
      <textarea id="prodDesc" rows="2" placeholder="Product details..." class="w-full bg-gray-900 border border-gray-700 p-2.5 rounded text-xs text-white resize-none"></textarea>
      <input id="prodImg" type="file" accept="image/*" class="w-full bg-gray-900 border border-gray-700 p-2 rounded text-xs text-white" />
      <button onclick="submitMarketplaceItem()" class="w-full bg-emerald-600 py-2.5 rounded text-xs font-bold text-white">Publish Listing</button>
    </div>
  </div>

  <!-- LIVE STREAM ROOM VIEW MODAL -->
  <div id="liveRoomModal" class="fixed inset-0 bg-black/90 hidden items-center justify-center p-4 z-50">
    <div class="glassmorphism max-w-lg w-full h-[550px] p-4 rounded-2xl flex flex-col relative">
      <button onclick="toggleModal('liveRoomModal')" class="absolute top-4 right-4 text-gray-400 hover:text-white"><i class="fa-solid fa-xmark"></i></button>
      <input id="activeLiveRoomId" type="hidden" />
      <h2 id="liveRoomTitle" class="text-md font-bold text-amber-400 border-b border-gray-800 pb-2"><i class="fa-solid fa-broadcast-tower"></i> Live Broadcast</h2>
      <div class="flex-1 grid grid-cols-3 gap-2 py-2 overflow-hidden">
        <div class="col-span-2 bg-black rounded-xl flex items-center justify-center relative overflow-hidden">
          <video id="liveVideoPlayer" autoplay muted class="w-full h-full object-cover"></video>
          <span class="absolute top-2 left-2 bg-red-600 text-white text-[10px] font-bold px-2 py-0.5 rounded animate-pulse">LIVE</span>
        </div>
        <div class="col-span-1 flex flex-col justify-between bg-gray-900/60 p-2 rounded-xl">
          <div id="liveChatComments" class="flex-1 overflow-y-auto space-y-1.5 custom-scrollbar text-[11px]"></div>
          <div class="flex gap-1 pt-2 border-t border-gray-800">
            <input id="liveCommentInput" type="text" placeholder="Comment..." class="flex-1 bg-gray-900 border border-gray-700 p-1.5 rounded text-[10px] text-white" />
            <button onclick="sendLiveComment()" class="bg-amber-600 text-black font-bold px-2.5 py-1.5 rounded text-[10px]">Send</button>
          </div>
        </div>
      </div>
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
    <button onclick="switchTab('marketplace')" class="flex flex-col items-center text-gray-400 hover:text-emerald-400">
      <i class="fa-solid fa-store text-lg"></i><span class="text-[10px]">Shop</span>
    </button>
    <button onclick="switchTab('live')" class="flex flex-col items-center text-gray-400 hover:text-amber-400">
      <i class="fa-solid fa-video text-lg"></i><span class="text-[10px]">Live</span>
    </button>
    <button onclick="openChatModal()" class="flex flex-col items-center text-gray-400 hover:text-cyan-400">
      <i class="fa-solid fa-paper-plane text-lg"></i><span class="text-[10px]">Chat</span>
    </button>
  </div>

  <!-- MODAL: ADD STORY -->
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
        <div class="bg-gray-900/80 p-3 rounded-xl border border-indigo-500/20"><p class="text-[10px] text-gray-400 uppercase">Platform Status</p><p class="text-sm font-bold text-purple-400">PrimeX Active</p></div>
      </div>
    </div>
  </div>

  <!-- MODAL: DUET REACTION -->
  <div id="duetModal" class="fixed inset-0 bg-black/80 hidden items-center justify-center p-4 z-50">
    <div class="glassmorphism max-w-md w-full p-6 rounded-2xl space-y-4 relative">
      <button onclick="toggleModal('duetModal')" class="absolute top-4 right-4 text-gray-400 hover:text-white"><i class="fa-solid fa-xmark"></i></button>
      <h2 class="text-lg font-bold text-center text-red-400">Create Duet Video</h2>
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
    let selectedEditAvatarBase64 = null;
    let isPollActive = false;

    onAuthStateChanged(auth, async (user) => {
      currentUser = user;
      if (user) {
        document.getElementById('authNavButtons').classList.add('hidden');
        document.getElementById('userNavProfile').classList.remove('hidden');
        
        const profileSnap = await get(ref(db, `users/${user.uid}`));
        const profileData = profileSnap.exists() ? profileSnap.val() : {};
        const displayName = profileData.displayName ? profileData.displayName : (user.displayName || user.email.split('@')[0]);

        document.getElementById('navUserName').innerText = displayName;
        if (profileData.avatar) {
          document.getElementById('navUserAvatarImg').src = profileData.avatar;
          document.getElementById('navUserAvatarImg').classList.remove('hidden');
          document.getElementById('navUserAvatarFallback').classList.add('hidden');
        } else {
          document.getElementById('navUserAvatarImg').classList.add('hidden');
          document.getElementById('navUserAvatarFallback').classList.remove('hidden');
          document.getElementById('navUserAvatarFallback').innerText = displayName.charAt(0).toUpperCase();
        }

        loadUserWallet(user.uid);
        checkVerificationStatus(user.uid);
        listenNotifications(user.uid);
        loadSavedBookmarks();
        loadMarketplace();
        loadLiveStreams();
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

    // DIRECT MESSAGES CHAT SYSTEM
    window.openChatModal = async () => {
      if (!currentUser) return alert("Please login first!");
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
          div.innerHTML = `<div class="w-6 h-6 rounded-full bg-blue-600 flex items-center justify-center font-bold text-[10px] text-white overflow-hidden">${uData.avatar ? `<img src="${uData.avatar}" class="w-full h-full object-cover">` : (uData.displayName || 'U').charAt(0).toUpperCase()}</div><span class="truncate">${uData.displayName || 'User'}</span>`;
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

    // BOOKMARKS
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

    window.filterFeedPosts = () => {
      const query = document.getElementById('searchInput').value.toLowerCase();
      const posts = document.querySelectorAll('#postsFeed > div');
      posts.forEach(post => {
        const text = post.innerText.toLowerCase();
        if (text.includes(query)) post.style.display = "block";
        else post.style.display = "none";
      });
    };

    // PROFILE EDIT SYSTEM
    window.openMyProfileModal = async () => {
      if (!currentUser) return alert("Please login first!");
      const profileSnap = await get(ref(db, `users/${currentUser.uid}`));
      if (profileSnap.exists()) {
        const data = profileSnap.val();
        document.getElementById('editDisplayName').value = data.displayName || currentUser.displayName || '';
        document.getElementById('editDob').value = data.dob || '';
        document.getElementById('editCountry').value = data.country || '';
        document.getElementById('editCity').value = data.city || '';
        document.getElementById('editUserBio').value = data.bio || '';
        if (data.avatar) {
          selectedEditAvatarBase64 = data.avatar;
          document.getElementById('editAvatarPreview').src = data.avatar;
          document.getElementById('editAvatarPreview').classList.remove('hidden');
          document.getElementById('editAvatarFallbackTxt').classList.add('hidden');
        }
      }
      toggleModal('editProfileModal');
    };

    window.previewEditAvatar = (input) => {
      const file = input.files[0];
      if (!file) return;
      const reader = new FileReader();
      reader.onloadend = () => {
        selectedEditAvatarBase64 = reader.result;
        document.getElementById('editAvatarPreview').src = selectedEditAvatarBase64;
        document.getElementById('editAvatarPreview').classList.remove('hidden');
        document.getElementById('editAvatarFallbackTxt').classList.add('hidden');
      };
      reader.readAsDataURL(file);
    };

    window.saveUserProfile = async () => {
      if (!currentUser) return;
      const displayName = document.getElementById('editDisplayName').value.trim();
      const dob = document.getElementById('editDob').value;
      const country = document.getElementById('editCountry').value.trim();
      const city = document.getElementById('editCity').value.trim();
      const bio = document.getElementById('editUserBio').value.trim();
      if (!displayName) return alert("Name is required!");

      const payload = { displayName, dob, country, city, bio };
      if (selectedEditAvatarBase64) payload.avatar = selectedEditAvatarBase64;

      await update(ref(db, `users/${currentUser.uid}`), payload);
      document.getElementById('navUserName').innerText = displayName;
      if (selectedEditAvatarBase64) {
        document.getElementById('navUserAvatarImg').src = selectedEditAvatarBase64;
        document.getElementById('navUserAvatarImg').classList.remove('hidden');
        document.getElementById('navUserAvatarFallback').classList.add('hidden');
      }
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
      let locationStr = "";
      let avatarUrl = null;

      if (userSnap.exists()) {
        const uVal = userSnap.val();
        name = uVal.displayName || name;
        bio = uVal.bio || bio;
        avatarUrl = uVal.avatar || null;
        if (uVal.city || uVal.country) {
          locationStr = [uVal.city, uVal.country].filter(Boolean).join(', ');
        }
      }

      if (avatarUrl) {
        document.getElementById('viewProfileAvatarImg').src = avatarUrl;
        document.getElementById('viewProfileAvatarImg').classList.remove('hidden');
        document.getElementById('viewProfileAvatarFallback').classList.add('hidden');
      } else {
        document.getElementById('viewProfileAvatarImg').classList.add('hidden');
        document.getElementById('viewProfileAvatarFallback').classList.remove('hidden');
        document.getElementById('viewProfileAvatarFallback').innerText = name.charAt(0).toUpperCase();
      }

      document.getElementById('viewProfileName').innerHTML = `${name} ${isVerified ? '<span class="text-blue-400 text-xs"><i class="fa-solid fa-circle-check"></i></span>' : ''}`;
      document.getElementById('viewProfileLocation').innerText = locationStr;
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

    // STORIES
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
                ${story.avatar ? `<img src="${story.avatar}" class="w-full h-full object-cover">` : story.author.charAt(0)}
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
      const avatarUrl = profileSnap.exists() ? profileSnap.val().avatar : null;

      const reader = new FileReader();
      reader.onloadend = async () => {
        const type = file.type.startsWith('image') ? 'image' : 'video';
        const storyRef = push(ref(db, 'stories'));
        await set(storyRef, { author: authorName, avatar: avatarUrl, uid: currentUser.uid, media: reader.result, mediaType: type, timestamp: Date.now() });
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

    // DUETS & REELS
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
        await set(reelRef, { author: authorName, uid: currentUser.uid, title: "Duet Video", videoBase64: originalUrl, duetVideoBase64: reader.result, isDuet: true, reactions: {}, timestamp: Date.now() });
        toggleModal('duetModal'); alert("Duet Reel published!");
      };
      reader.readAsDataURL(file);
    };

    window.toggleReelReaction = async (reelKey, reactionType) => {
      if (!currentUser) return alert("Please login first!");
      const reelRef = ref(db, `reels/${reelKey}/reactions`);
      const snap = await get(reelRef);
      let reactions = snap.exists() ? snap.val() : {};

      if (reactions[currentUser.uid] === reactionType) {
        delete reactions[currentUser.uid];
      } else {
        reactions[currentUser.uid] = reactionType;
      }
      await set(reelRef, reactions);
    };

    onValue(ref(db, 'reels'), (snapshot) => {
      const container = document.getElementById('reelsContainer'); container.innerHTML = '';
      const data = snapshot.val(); if (!data) return;
      Object.entries(data).reverse().forEach(([key, reel]) => {
        const reactions = reel.reactions || {};
        const reactionCounts = { like: 0, love: 0, haha: 0, wow: 0, sad: 0, angry: 0 };
        Object.values(reactions).forEach(r => { if (reactionCounts[r] !== undefined) reactionCounts[r]++; });
        const myReaction = currentUser ? reactions[currentUser.uid] : null;

        const div = document.createElement('div');
        div.className = "reel-card relative h-full bg-black rounded-xl overflow-hidden flex items-center justify-center border border-gray-800";
        
        let mediaHtml = reel.isDuet 
          ? `<div class="grid grid-cols-2 w-full h-full"><video src="${reel.videoBase64}" controls loop class="w-full h-full object-cover"></video><video src="${reel.duetVideoBase64}" controls loop class="w-full h-full object-cover"></video></div>`
          : `<video src="${reel.videoBase64}" controls loop class="w-full h-full object-cover"></video>`;

        div.innerHTML = `
          ${mediaHtml}
          <div class="absolute bottom-4 left-4 right-4 space-y-2 z-10 bg-black/60 p-3 rounded-xl backdrop-blur-md">
            <div class="flex justify-between items-center">
              <div>
                <p class="font-bold text-sm text-white cursor-pointer hover:underline" onclick="inspectUserProfile('${reel.uid}')">${reel.author}</p>
                <p class="text-xs text-gray-300">${reel.title}</p>
              </div>
              ${!reel.isDuet ? `<button onclick="openDuetModal('${reel.videoBase64}')" class="text-[10px] bg-red-600 text-white font-bold px-2 py-1 rounded">Duet</button>` : ''}
            </div>
            <div class="flex items-center space-x-2 pt-1 border-t border-gray-700/50 text-xs">
              <button onclick="toggleReelReaction('${key}', 'like')" class="flex items-center gap-1 px-2 py-1 rounded ${myReaction === 'like' ? 'bg-blue-600 text-white' : 'bg-gray-800 text-gray-300'}">👍 ${reactionCounts.like}</button>
              <button onclick="toggleReelReaction('${key}', 'love')" class="flex items-center gap-1 px-2 py-1 rounded ${myReaction === 'love' ? 'bg-red-600 text-white' : 'bg-gray-800 text-gray-300'}">❤️ ${reactionCounts.love}</button>
              <button onclick="toggleReelReaction('${key}', 'haha')" class="flex items-center gap-1 px-2 py-1 rounded ${myReaction === 'haha' ? 'bg-amber-600 text-white' : 'bg-gray-800 text-gray-300'}">😂 ${reactionCounts.haha}</button>
              <button onclick="toggleReelReaction('${key}', 'wow')" class="flex items-center gap-1 px-2 py-1 rounded ${myReaction === 'wow' ? 'bg-purple-600 text-white' : 'bg-gray-800 text-gray-300'}">😮 ${reactionCounts.wow}</button>
            </div>
          </div>
        `;
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

    window.togglePollCreator = () => {
      isPollActive = !isPollActive;
      document.getElementById('pollCreatorContainer').classList.toggle('hidden', !isPollActive);
    };

    window.submitPost = async () => {
      if (!currentUser) return alert("Please login first!");
      const content = document.getElementById('postInput').value;
      if (!content && !selectedMediaBase64 && !isPollActive) return alert("Add content first!");

      let pollData = null;
      if (isPollActive) {
        const question = document.getElementById('pollQuestion').value;
        const opt1 = document.getElementById('pollOpt1').value;
        const opt2 = document.getElementById('pollOpt2').value;
        if (!question || !opt1 || !opt2) return alert("Fill all poll fields!");
        pollData = { question, options: [opt1, opt2], votes: { 0: [], 1: [] } };
      }

      const isVerifiedSnap = await get(ref(db, `verifiedUsers/${currentUser.uid}`));
      const isVerified = isVerifiedSnap.exists() && isVerifiedSnap.val() === true;
      const profileSnap = await get(ref(db, `users/${currentUser.uid}`));
      const authorName = profileSnap.exists() && profileSnap.val().displayName ? profileSnap.val().displayName : (currentUser.displayName || currentUser.email.split('@')[0]);

      const postRef = push(ref(db, 'posts'));
      await set(postRef, {
        author: authorName, uid: currentUser.uid, isVerified, content,
        media: selectedMediaBase64 || null, mediaType: selectedMediaType || null,
        poll: pollData, reactions: {}, views: 1, isBoosted: false, timestamp: Date.now()
      });

      document.getElementById('postInput').value = ''; clearMedia();
      isPollActive = false; document.getElementById('pollCreatorContainer').classList.add('hidden');
      alert("Post published live!");
    };

    window.votePoll = async (postKey, optionIndex) => {
      if (!currentUser) return alert("Please login first!");
      const pollRef = ref(db, `posts/${postKey}/poll`);
      const snap = await get(pollRef);
      if (!snap.exists()) return;
      const poll = snap.val();
      
      // Remove prior votes by user
      [0, 1].forEach(idx => {
        if (poll.votes[idx]) {
          poll.votes[idx] = poll.votes[idx].filter(uid => uid !== currentUser.uid);
        }
      });

      if (!poll.votes[optionIndex]) poll.votes[optionIndex] = [];
      poll.votes[optionIndex].push(currentUser.uid);

      await set(pollRef, poll);
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
        await set(reelRef, { author: authorName, uid: currentUser.uid, title, videoBase64: reader.result, reactions: {}, timestamp: Date.now() });
        toggleModal('uploadReelModal'); alert("Reel published!");
      };
      reader.readAsDataURL(file);
    };

    // MARKETPLACE
    window.openAddProductModal = () => { if (!currentUser) return alert("Please login first!"); toggleModal('addProductModal'); };
    window.submitMarketplaceItem = async () => {
      const title = document.getElementById('prodTitle').value;
      const price = document.getElementById('prodPrice').value;
      const desc = document.getElementById('prodDesc').value;
      const file = document.getElementById('prodImg').files[0];
      if (!title || !price || !file) return alert("Fill all product fields!");

      const reader = new FileReader();
      reader.onloadend = async () => {
        const prodRef = push(ref(db, 'marketplace'));
        await set(prodRef, { title, price, desc, image: reader.result, sellerUid: currentUser.uid, sellerName: currentUser.displayName || 'Seller', timestamp: Date.now() });
        toggleModal('addProductModal'); alert("Product listed successfully!");
      };
      reader.readAsDataURL(file);
    };

    function loadMarketplace() {
      onValue(ref(db, 'marketplace'), (snapshot) => {
        const container = document.getElementById('marketplaceContainer'); container.innerHTML = '';
        const data = snapshot.val(); if (!data) return;
        Object.entries(data).reverse().forEach(([key, prod]) => {
          const div = document.createElement('div');
          div.className = "glassmorphism p-3 rounded-xl space-y-2 border border-emerald-500/20";
          div.innerHTML = `
            <img src="${prod.image}" class="w-full h-36 object-cover rounded-lg" />
            <div class="flex justify-between items-center"><h3 class="font-bold text-sm">${prod.title}</h3><span class="text-emerald-400 font-extrabold text-xs">PKR ${prod.price}</span></div>
            <p class="text-[11px] text-gray-400 truncate">${prod.desc}</p>
            <button onclick="inspectUserProfile('${prod.sellerUid}')" class="w-full bg-emerald-600 hover:bg-emerald-700 text-xs py-1.5 rounded font-bold text-white">Contact Seller</button>
          `;
          container.appendChild(div);
        });
      });
    }

    // LIVE STREAMING MODULE
    window.startLiveStream = async () => {
      if (!currentUser) return alert("Please login first!");
      const title = prompt("Enter Live Stream Title:");
      if (!title) return;

      const liveRef = push(ref(db, 'livestreams'));
      await set(liveRef, { id: liveRef.key, title, hostUid: currentUser.uid, hostName: currentUser.displayName || 'Host', active: true, timestamp: Date.now() });
      openLiveRoom(liveRef.key, title);
    };

    function loadLiveStreams() {
      onValue(ref(db, 'livestreams'), (snapshot) => {
        const container = document.getElementById('liveStreamsContainer'); container.innerHTML = '';
        const data = snapshot.val(); if (!data) return;
        Object.values(data).forEach(stream => {
          if (stream.active) {
            const div = document.createElement('div');
            div.className = "glassmorphism p-4 rounded-xl space-y-2 border border-amber-500/30 text-center";
            div.innerHTML = `
              <div class="w-12 h-12 rounded-full bg-amber-500/20 text-amber-400 mx-auto flex items-center justify-center font-bold"><i class="fa-solid fa-video text-lg"></i></div>
              <h3 class="font-bold text-sm">${stream.title}</h3>
              <p class="text-[11px] text-gray-400">Hosted by ${stream.hostName}</p>
              <button onclick="openLiveRoom('${stream.id}', '${stream.title}')" class="w-full bg-amber-600 text-black text-xs font-bold py-1.5 rounded">Join Room</button>
            `;
            container.appendChild(div);
          }
        });
      });
    }

    window.openLiveRoom = (roomId, title) => {
      document.getElementById('activeLiveRoomId').value = roomId;
      document.getElementById('liveRoomTitle').innerHTML = `<i class="fa-solid fa-broadcast-tower"></i> ${title}`;
      toggleModal('liveRoomModal');

      // Request webcam for streaming simulation
      navigator.mediaDevices.getUserMedia({ video: true, audio: true }).then(stream => {
        document.getElementById('liveVideoPlayer').srcObject = stream;
      }).catch(err => console.log("Webcam permission denied or unavailable"));

      onValue(ref(db, `livestreams/${roomId}/comments`), (snap) => {
        const box = document.getElementById('liveChatComments'); box.innerHTML = '';
        const data = snap.val(); if (!data) return;
        Object.values(data).forEach(c => {
          const el = document.createElement('div');
          el.innerHTML = `<span class="font-bold text-amber-400">${c.name}:</span> <span class="text-gray-300">${c.text}</span>`;
          box.appendChild(el);
        });
        box.scrollTop = box.scrollHeight;
      });
    };

    window.sendLiveComment = async () => {
      const roomId = document.getElementById('activeLiveRoomId').value;
      const text = document.getElementById('liveCommentInput').value.trim();
      if (!text || !currentUser) return;
      const refComm = push(ref(db, `livestreams/${roomId}/comments`));
      await set(refComm, { name: currentUser.displayName || 'User', text, timestamp: Date.now() });
      document.getElementById('liveCommentInput').value = '';
    };

    // MULTI-REACTIONS ENGINE
    window.togglePostReaction = async (postKey, reactionType) => {
      if (!currentUser) return alert("Please login first!");
      const postRef = ref(db, `posts/${postKey}`);
      const snap = await get(postRef);
      if (snap.exists()) {
        const postData = snap.val();
        let reactions = postData.reactions || {};

        if (reactions[currentUser.uid] === reactionType) {
          delete reactions[currentUser.uid];
        } else {
          reactions[currentUser.uid] = reactionType;
          pushNotification(postData.uid, `${currentUser.displayName || 'Someone'} reacted to your post!`);
        }
        await update(postRef, { reactions });
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

    // BOOST & VERIFICATION
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

    // FEED RENDER ENGINE & TRENDING HASHTAGS
    onValue(ref(db, 'posts'), (snapshot) => {
      const feed = document.getElementById('postsFeed'); feed.innerHTML = '';
      const trendingContainer = document.getElementById('trendingTagsContainer');
      const data = snapshot.val(); if (!data) return;
      
      let calcViews = 0;
      let hashtagCounts = {};
      const postsArray = Object.entries(data);
      postsArray.sort((a, b) => (b[1].isBoosted ? 1 : 0) - (a[1].isBoosted ? 1 : 0));

      postsArray.forEach(([key, post]) => {
        calcViews += (post.views || 1);
        
        // Extract hashtags
        const tags = post.content ? post.content.match(/#[\w]+/g) : null;
        if (tags) {
          tags.forEach(t => { hashtagCounts[t] = (hashtagCounts[t] || 0) + 1; });
        }

        const commentCount = post.comments ? Object.keys(post.comments).length : 0;
        const reactions = post.reactions || {};
        const reactionCounts = { like: 0, love: 0, haha: 0, wow: 0, sad: 0, angry: 0 };
        Object.values(reactions).forEach(r => { if (reactionCounts[r] !== undefined) reactionCounts[r]++; });
        const myReaction = currentUser ? reactions[currentUser.uid] : null;

        // Poll HTML generation
        let pollHtml = '';
        if (post.poll) {
          const totalVotes = Object.values(post.poll.votes || {}).reduce((a, b) => a + (b ? b.length : 0), 0);
          pollHtml = `<div class="p-3 bg-gray-900/60 rounded-xl space-y-2 border border-gray-800">
            <p class="font-bold text-xs text-blue-400">${post.poll.question}</p>`;
          post.poll.options.forEach((opt, idx) => {
            const votesArr = post.poll.votes[idx] || [];
            const count = votesArr.length;
            const pct = totalVotes > 0 ? Math.round((count / totalVotes) * 100) : 0;
            const hasVoted = currentUser && votesArr.includes(currentUser.uid);
            pollHtml += `<button onclick="votePoll('${key}', ${idx})" class="w-full text-left p-2 rounded text-xs bg-gray-800 hover:bg-gray-700 flex justify-between items-center ${hasVoted ? 'border border-blue-500' : ''}">
              <span>${opt} ${hasVoted ? '✓' : ''}</span><span class="text-gray-400">${pct}% (${count})</span>
            </button>`;
          });
          pollHtml += `</div>`;
        }

        const el = document.createElement('div');
        el.className = `glassmorphism p-4 rounded-xl space-y-3 ${post.isBoosted ? 'border border-amber-500/50 bg-amber-950/10' : ''}`;
        el.innerHTML = `
          ${post.isBoosted ? '<span class="text-[10px] bg-amber-500 text-black font-bold px-2 py-0.5 rounded uppercase"><i class="fa-solid fa-bullhorn"></i> Sponsored Ad</span>' : ''}
          <div class="flex justify-between items-center">
            <div class="flex items-center space-x-2">
              <div class="w-8 h-8 rounded-full bg-gradient-to-tr from-blue-500 to-purple-500 flex items-center justify-center font-bold text-xs cursor-pointer overflow-hidden" onclick="inspectUserProfile('${post.uid}')">${post.author.charAt(0).toUpperCase()}</div>
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
          ${pollHtml}
          
          <div class="flex flex-wrap gap-2 items-center justify-between text-xs text-gray-300 pt-2 border-t border-gray-800">
            <div class="flex items-center space-x-1.5">
              <button onclick="togglePostReaction('${key}', 'like')" class="px-2 py-1 rounded flex items-center gap-1 ${myReaction === 'like' ? 'bg-blue-600 text-white' : 'bg-gray-800/80 hover:bg-gray-700'}">👍 <span>${reactionCounts.like}</span></button>
              <button onclick="togglePostReaction('${key}', 'love')" class="px-2 py-1 rounded flex items-center gap-1 ${myReaction === 'love' ? 'bg-red-600 text-white' : 'bg-gray-800/80 hover:bg-gray-700'}">❤️ <span>${reactionCounts.love}</span></button>
              <button onclick="togglePostReaction('${key}', 'haha')" class="px-2 py-1 rounded flex items-center gap-1 ${myReaction === 'haha' ? 'bg-amber-600 text-white' : 'bg-gray-800/80 hover:bg-gray-700'}">😂 <span>${reactionCounts.haha}</span></button>
              <button onclick="togglePostReaction('${key}', 'wow')" class="px-2 py-1 rounded flex items-center gap-1 ${myReaction === 'wow' ? 'bg-purple-600 text-white' : 'bg-gray-800/80 hover:bg-gray-700'}">😮 <span>${reactionCounts.wow}</span></button>
            </div>
            <div class="flex items-center space-x-3 text-gray-400">
              <button onclick="openCommentsModal('${key}')" class="hover:text-blue-400"><i class="fa-regular fa-comment"></i> ${commentCount}</button>
              <button onclick="sharePost('${key}')" class="hover:text-green-400"><i class="fa-solid fa-share"></i></button>
              <span><i class="fa-regular fa-eye"></i> ${post.views || 1}</span>
            </div>
          </div>
        `;
        feed.appendChild(el);
      });
      document.getElementById('statTotalViews').innerText = calcViews;

      // Render Trending Tags
      trendingContainer.innerHTML = '';
      const sortedTags = Object.entries(hashtagCounts).sort((a,b) => b[1] - a[1]);
      if (sortedTags.length > 0) {
        sortedTags.slice(0, 5).forEach(([tag, count]) => {
          const tEl = document.createElement('div');
          tEl.className = "flex justify-between items-center text-gray-300 hover:text-indigo-400 cursor-pointer";
          tEl.innerHTML = `<span class="font-bold">${tag}</span><span class="text-[10px] bg-gray-800 px-1.5 py-0.5 rounded">${count} posts</span>`;
          tEl.onclick = () => { document.getElementById('searchInput').value = tag; filterFeedPosts(); };
          trendingContainer.appendChild(tEl);
        });
      } else {
        trendingContainer.innerHTML = '<p class="text-gray-500 text-center py-2">No trending topics yet.</p>';
      }
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
    function toggleTheme() { document.body.classList.toggle('light-theme'); }
    
    function switchTab(tab) {
      document.getElementById('feedTab').classList.add('hidden');
      document.getElementById('reelsTab').classList.add('hidden');
      document.getElementById('marketplaceTab').classList.add('hidden');
      document.getElementById('liveTab').classList.add('hidden');
      document.getElementById('savedTab').classList.add('hidden');
      document.getElementById('groupsTab').classList.add('hidden');
      if (tab === 'feed') document.getElementById('feedTab').classList.remove('hidden');
      if (tab === 'reels') document.getElementById('reelsTab').classList.remove('hidden');
      if (tab === 'marketplace') document.getElementById('marketplaceTab').classList.remove('hidden');
      if (tab === 'live') document.getElementById('liveTab').classList.remove('hidden');
      if (tab === 'saved') document.getElementById('savedTab').classList.remove('hidden');
      if (tab === 'groups') document.getElementById('groupsTab').classList.remove('hidden');
    }
  </script>
</body>
</html>
