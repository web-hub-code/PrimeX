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
      <h1 id="secretLogoBtn" onclick="handleLogoTap()" class="cursor-pointer text-2xl font-extrabold tracking-wider bg-gradient-to-r from-blue-500 via-indigo-500 to-purple-500 bg-clip-text text-transparent select-none">
        PrimeX <span class="text-[10px] bg-amber-500 text-black px-1.5 py-0.5 rounded font-bold uppercase">Pro Ultimate</span>
      </h1>
    </div>
    <div id="authNavButtons" class="flex items-center space-x-3">
      <button onclick="toggleModal('authModal')" class="bg-blue-600 hover:bg-blue-700 text-sm font-semibold px-4 py-2 rounded-lg transition">Login / Register</button>
    </div>
    <div id="userNavProfile" class="hidden flex items-center space-x-2 md:space-x-3">
      <button onclick="openAnalyticsModal()" class="bg-indigo-600/80 hover:bg-indigo-600 text-xs font-bold px-2.5 py-1.5 rounded-lg flex items-center gap-1">
        <i class="fa-solid fa-chart-line"></i> <span class="hidden sm:inline">Analytics</span>
      </button>
      <button onclick="openWalletModal()" class="bg-gradient-to-r from-amber-500 to-yellow-600 text-xs font-bold px-2.5 py-1.5 rounded-lg hover:opacity-90 flex items-center gap-1 text-black">
        <i class="fa-solid fa-coins"></i> <span id="navWalletBalance">PKR 0</span>
      </button>
      <button onclick="openDepositModal()" class="bg-gradient-to-r from-green-500 to-emerald-600 text-xs font-bold px-2.5 py-1.5 rounded-lg hover:opacity-90 flex items-center gap-1">
        <i class="fa-solid fa-wallet"></i> <span class="hidden sm:inline">Top-up</span>
      </button>
      <div class="flex items-center gap-1">
        <span id="navUserName" class="text-sm font-medium text-gray-300"></span>
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
        <button onclick="switchTab('groups')" class="w-full flex items-center space-x-3 text-gray-300 hover:text-white p-2 rounded-lg hover:bg-gray-800/50 transition">
          <i class="fa-solid fa-users text-green-400 text-lg"></i> <span class="font-medium">Facebook Communities</span>
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
          <!-- Add Story Trigger -->
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

      <!-- TAB 2: TIKTOK REELS FEED & DUET SYSTEM -->
      <div id="reelsTab" class="hidden space-y-4">
        <div class="flex justify-between items-center">
          <h2 class="text-lg font-bold text-red-400 flex items-center gap-2">
            <i class="fa-solid fa-fire"></i> Prime Reels & TikTok Duets
          </h2>
          <button onclick="openUploadReelModal()" class="bg-red-600 hover:bg-red-700 text-xs font-bold px-3 py-1.5 rounded-lg flex items-center gap-1">
            <i class="fa-solid fa-plus"></i> Upload Reel
          </button>
        </div>
        <div id="reelsContainer" class="h-[600px] overflow-y-scroll reel-snap rounded-2xl glassmorphism space-y-4 custom-scrollbar p-2"></div>
      </div>

      <!-- TAB 3: FACEBOOK COMMUNITIES / GROUPS -->
      <div id="groupsTab" class="hidden space-y-4">
        <h2 class="text-lg font-bold text-green-400 flex items-center gap-2">
          <i class="fa-solid fa-users"></i> Facebook Style Communities
        </h2>
        <div class="grid grid-cols-1 sm:grid-cols-2 gap-3">
          <div class="glassmorphism p-4 rounded-xl border border-green-500/20 text-center space-y-2">
            <i class="fa-solid fa-code text-2xl text-green-400"></i>
            <h3 class="font-bold text-sm">Tech & Web Developers GB</h3>
            <p class="text-[11px] text-gray-400">Discuss web apps, APIs & modern tech.</p>
            <button onclick="joinCommunity('Tech GB')" class="bg-green-600 text-xs font-bold px-3 py-1 rounded-lg">Joined</button>
          </div>
          <div class="glassmorphism p-4 rounded-xl border border-blue-500/20 text-center space-y-2">
            <i class="fa-solid fa-mountain text-2xl text-blue-400"></i>
            <h3 class="font-bold text-sm">Discover Gilgit-Baltistan</h3>
            <p class="text-[11px] text-gray-400">Share news, photos & tourism updates.</p>
            <button onclick="joinCommunity('GB Tourism')" class="bg-blue-600 text-xs font-bold px-3 py-1 rounded-lg">Joined</button>
          </div>
        </div>
      </div>

    </main>

    <!-- RIGHT SIDEBAR: PROMOTIONS & DASHBOARD LINK -->
    <aside class="hidden md:block col-span-1 space-y-4">
      <div class="glassmorphism p-4 rounded-xl space-y-3 border border-indigo-500/30">
        <h3 class="font-bold text-sm text-indigo-400 flex items-center gap-1"><i class="fa-solid fa-chart-line"></i> Creator Analytics</h3>
        <p class="text-xs text-gray-300 leading-relaxed">
          Monitor your real-time video performance, views growth, and wallet balance analytics.
        </p>
        <button onclick="openAnalyticsModal()" class="w-full bg-indigo-600 hover:bg-indigo-700 text-white font-bold py-2 rounded-lg text-xs">Open Dashboard</button>
      </div>

      <div class="glassmorphism p-4 rounded-xl space-y-3 border border-amber-500/30">
        <h3 class="font-bold text-sm text-amber-400 flex items-center gap-1"><i class="fa-solid fa-bullhorn"></i> Paid Ad Booster</h3>
        <p class="text-xs text-gray-300 leading-relaxed">
          Boost your posts or reels to appear on top of all feeds (Starting @ PKR 300).
        </p>
        <button onclick="openBoostInfo()" class="w-full bg-gradient-to-r from-amber-500 to-yellow-600 text-black font-bold py-2 rounded-lg text-xs">Learn More & Boost</button>
      </div>
    </aside>
  </div>

  <!-- MOBILE BOTTOM NAVIGATION BAR -->
  <div class="md:hidden fixed bottom-0 left-0 right-0 z-40 glassmorphism border-t border-gray-800 flex justify-around py-2">
    <button onclick="switchTab('feed')" class="flex flex-col items-center text-gray-400 hover:text-blue-400 focus:text-blue-400">
      <i class="fa-solid fa-house text-lg"></i>
      <span class="text-[10px] mt-0.5">Feed</span>
    </button>
    <button onclick="switchTab('reels')" class="flex flex-col items-center text-gray-400 hover:text-red-400 focus:text-red-400">
      <i class="fa-solid fa-clapperboard text-lg"></i>
      <span class="text-[10px] mt-0.5">Reels</span>
    </button>
    <button onclick="switchTab('groups')" class="flex flex-col items-center text-gray-400 hover:text-green-400 focus:text-green-400">
      <i class="fa-solid fa-users text-lg"></i>
      <span class="text-[10px] mt-0.5">Groups</span>
    </button>
    <button onclick="openAnalyticsModal()" class="flex flex-col items-center text-gray-400 hover:text-purple-400">
      <i class="fa-solid fa-chart-pie text-lg"></i>
      <span class="text-[10px] mt-0.5">Analytics</span>
    </button>
  </div>

  <!-- MODAL: ADD INSTAGRAM STORY -->
  <div id="addStoryModal" class="fixed inset-0 bg-black/80 hidden items-center justify-center p-4 z-50">
    <div class="glassmorphism max-w-sm w-full p-6 rounded-2xl space-y-4 relative">
      <button onclick="toggleModal('addStoryModal')" class="absolute top-4 right-4 text-gray-400 hover:text-white"><i class="fa-solid fa-xmark"></i></button>
      <h2 class="text-lg font-bold text-center text-blue-400">Post 24-Hour Story</h2>
      <input id="storyFileInput" type="file" accept="image/*,video/*" class="w-full bg-gray-900 border border-gray-700 p-2.5 rounded-lg text-xs" />
      <button onclick="submitStory()" class="w-full bg-blue-600 hover:bg-blue-700 py-2.5 rounded-lg text-xs font-bold">Upload Story</button>
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
      <h2 class="text-lg font-bold text-center text-indigo-400 flex items-center justify-center gap-2">
        <i class="fa-solid fa-chart-pie"></i> Creator Performance Analytics
      </h2>
      <div class="grid grid-cols-2 gap-3 text-center">
        <div class="bg-gray-900/80 p-3 rounded-xl border border-indigo-500/20">
          <p class="text-[10px] text-gray-400 uppercase">Total Post Views</p>
          <p id="statTotalViews" class="text-xl font-extrabold text-blue-400">0</p>
        </div>
        <div class="bg-gray-900/80 p-3 rounded-xl border border-indigo-500/20">
          <p class="text-[10px] text-gray-400 uppercase">Engagement Rate</p>
          <p id="statEngagement" class="text-xl font-extrabold text-green-400">94.2%</p>
        </div>
        <div class="bg-gray-900/80 p-3 rounded-xl border border-indigo-500/20">
          <p class="text-[10px] text-gray-400 uppercase">Est. Monetization</p>
          <p id="statMonetization" class="text-xl font-extrabold text-amber-400">PKR 0</p>
        </div>
        <div class="bg-gray-900/80 p-3 rounded-xl border border-indigo-500/20">
          <p class="text-[10px] text-gray-400 uppercase">Top Reach Region</p>
          <p class="text-sm font-bold text-purple-400">Gilgit-Baltistan</p>
        </div>
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
      <input id="duetVideoInput" type="file" accept="video/*" class="w-full bg-gray-900 border border-gray-700 p-2 rounded-lg text-xs" />
      <button onclick="submitDuetReel()" class="w-full bg-red-600 hover:bg-red-700 py-2.5 rounded-lg text-xs font-bold">Publish Duet Reel</button>
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
        <input id="commentInput" type="text" placeholder="Write a comment..." class="flex-1 bg-gray-900 border border-gray-700 rounded-lg p-2 text-xs focus:outline-none" />
        <button onclick="submitComment()" class="bg-blue-600 hover:bg-blue-700 text-xs font-bold px-4 py-2 rounded-lg">Send</button>
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
      <p class="text-xs text-gray-300">Unlock official credibility for a fee of <strong>PKR 999</strong>.</p>
      <button onclick="purchaseVerification()" class="w-full bg-blue-600 hover:bg-blue-700 py-2.5 rounded-lg text-xs font-bold">Pay & Get Verified</button>
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

  <!-- FIREBASE & EXTENDED Dynamic LOGIC SCRIPT -->
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

    // INSTAGRAM STORIES REALTIME LOGIC
    onValue(ref(db, 'stories'), (snapshot) => {
      const container = document.getElementById('storiesContainer');
      container.innerHTML = '';
      const data = snapshot.val();
      if (!data) return;

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

    window.openAddStoryModal = () => {
      if (!currentUser) return alert("Please login first, sweetie!");
      toggleModal('addStoryModal');
    };

    window.submitStory = async () => {
      const file = document.getElementById('storyFileInput').files[0];
      if (!file) return alert("Select media first!");
      const reader = new FileReader();
      reader.onloadend = async () => {
        const type = file.type.startsWith('image') ? 'image' : 'video';
        const storyRef = push(ref(db, 'stories'));
        await set(storyRef, {
          author: currentUser.displayName || currentUser.email.split('@')[0],
          uid: currentUser.uid,
          media: reader.result,
          mediaType: type,
          timestamp: Date.now()
        });
        toggleModal('addStoryModal');
        alert("24-Hour Story published!");
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

    // TIKTOK DUET SYSTEM ENGINE WITH CONTROLS
    window.openDuetModal = (videoUrl) => {
      if (!currentUser) return alert("Please login first!");
      document.getElementById('duetOriginalUrl').value = videoUrl;
      document.getElementById('duetOriginalPreview').src = videoUrl;
      toggleModal('duetModal');
    };

    window.submitDuetReel = async () => {
      const originalUrl = document.getElementById('duetOriginalUrl').value;
      const file = document.getElementById('duetVideoInput').files[0];
      if (!file) return alert("Select your reaction video!");

      const reader = new FileReader();
      reader.onloadend = async () => {
        const reelRef = push(ref(db, 'reels'));
        await set(reelRef, {
          author: currentUser.displayName || currentUser.email.split('@')[0],
          uid: currentUser.uid,
          title: "Duet with Creator",
          videoBase64: originalUrl,
          duetVideoBase64: reader.result,
          isDuet: true,
          likes: 0,
          timestamp: Date.now()
        });
        toggleModal('duetModal');
        alert("Duet Reel published!");
      };
      reader.readAsDataURL(file);
    };

    // REELS RENDER WITH CONTROLS AND MUTE SYNC
    onValue(ref(db, 'reels'), (snapshot) => {
      const container = document.getElementById('reelsContainer'); container.innerHTML = '';
      const data = snapshot.val(); if (!data) { container.innerHTML = `<p class="text-xs text-center text-gray-500 py-20">No reels uploaded yet.</p>`; return; }
      Object.values(data).reverse().forEach(reel => {
        const div = document.createElement('div');
        div.className = "reel-card relative h-full bg-black rounded-xl overflow-hidden flex items-center justify-center border border-gray-800";
        if (reel.isDuet) {
          div.innerHTML = `
            <div class="grid grid-cols-2 w-full h-full">
              <video src="${reel.videoBase64}" controls loop class="w-full h-full object-cover"></video>
              <video src="${reel.duetVideoBase64}" controls loop class="w-full h-full object-cover"></video>
            </div>
            <div class="absolute bottom-4 left-4 space-y-1 z-10 bg-black/50 p-2 rounded-lg backdrop-blur-sm">
              <span class="text-[9px] bg-red-600 text-white font-bold px-1.5 py-0.5 rounded">TikTok Duet</span>
              <p class="font-bold text-sm text-white">${reel.author}</p>
              <p class="text-xs text-gray-300">${reel.title}</p>
            </div>
          `;
        } else {
          div.innerHTML = `
            <video src="${reel.videoBase64}" controls loop class="w-full h-full object-cover"></video>
            <div class="absolute bottom-4 left-4 space-y-1 bg-black/50 p-2 rounded-lg backdrop-blur-sm z-10">
              <p class="font-bold text-sm text-white">${reel.author}</p>
              <p class="text-xs text-gray-300">${reel.title}</p>
              <button onclick="openDuetModal('${reel.videoBase64}')" class="text-[10px] bg-red-600 text-white font-bold px-2 py-1 rounded flex items-center gap-1 mt-1"><i class="fa-solid fa-[#fa-duet]"></i> Duet React</button>
            </div>
          `;
        }
        container.appendChild(div);
      });
    });

    // MEDIA PREVIEW & FEED HELPERS
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
        views: 1,
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

    // LIKE & COMMENT SYSTEM
    window.toggleLikePost = async (postKey) => {
      if (!currentUser) return alert("Please login first!");
      const postRef = ref(db, `posts/${postKey}`);
      const snap = await get(postRef);
      if (snap.exists()) {
        const postData = snap.val();
        const likedBy = postData.likedBy || {};
        const isLiked = likedBy[currentUser.uid];
        let currentLikes = postData.likes || 0;

        if (isLiked) {
          currentLikes = Math.max(0, currentLikes - 1);
          delete likedBy[currentUser.uid];
        } else {
          currentLikes += 1;
          likedBy[currentUser.uid] = true;
        }

        await update(postRef, { likes: currentLikes, likedBy });
      }
    };

    window.openCommentsModal = (postKey) => {
      document.getElementById('activePostKey').value = postKey;
      toggleModal('commentsModal');
      loadComments(postKey);
    };

    function loadComments(postKey) {
      onValue(ref(db, `posts/${postKey}/comments`), (snapshot) => {
        const list = document.getElementById('commentsList');
        list.innerHTML = '';
        const data = snapshot.val();
        if (!data) {
          list.innerHTML = '<p class="text-center text-xs text-gray-500 py-4">No comments yet. Be the first to comment!</p>';
          return;
        }
        Object.values(data).forEach(c => {
          const item = document.createElement('div');
          item.className = "p-2 bg-gray-900 rounded-lg text-xs space-y-0.5";
          item.innerHTML = `<span class="font-bold text-blue-400">${c.author}: </span><span class="text-gray-300">${c.text}</span>`;
          list.appendChild(item);
        });
      });
    }

    window.submitComment = async () => {
      if (!currentUser) return alert("Please login first!");
      const postKey = document.getElementById('activePostKey').value;
      const text = document.getElementById('commentInput').value.trim();
      if (!text) return;

      const commentRef = push(ref(db, `posts/${postKey}/comments`));
      await set(commentRef, {
        author: currentUser.displayName || currentUser.email.split('@')[0],
        uid: currentUser.uid,
        text,
        timestamp: Date.now()
      });
      document.getElementById('commentInput').value = '';
    };

    window.sharePost = (postKey) => {
      if (navigator.share) {
        navigator.share({ title: 'PrimeX Post', url: window.location.href });
      } else {
        navigator.clipboard.writeText(window.location.href);
        alert("Link copied to clipboard!");
      }
    };

    // BOOST POST
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

    // VERIFICATION
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

    // DEPOSIT MANUAL
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
      alert("Top-up request submitted!");
    };

    // FEED & ANALYTICS DATA CALCULATOR WITH LIKES AND COMMENTS
    onValue(ref(db, 'posts'), (snapshot) => {
      const feed = document.getElementById('postsFeed'); feed.innerHTML = '';
      const data = snapshot.val(); if (!data) return;
      
      let calcViews = 0;
      const postsArray = Object.entries(data);
      postsArray.sort((a, b) => (b[1].isBoosted ? 1 : 0) - (a[1].isBoosted ? 1 : 0));

      postsArray.forEach(([key, post]) => {
        calcViews += (post.views || 1);
        const commentCount = post.comments ? Object.keys(post.comments).length : 0;
        const isLikedByMe = currentUser && post.likedBy && post.likedBy[currentUser.uid];

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
            <button onclick="toggleLikePost('${key}')" class="flex items-center gap-1 ${isLikedByMe ? 'text-red-500 font-bold' : 'hover:text-red-400'}">
              <i class="${isLikedByMe ? 'fa-solid' : 'fa-regular'} fa-heart"></i> <span>${post.likes || 0} Likes</span>
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

    // SECRET ADMIN TRIGGER & CONTROL
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
      // Load Pending Deposits
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
              </div>
            `;
            container.appendChild(div);
          }
        });
      });

      // Load Pending Withdrawals
      onValue(ref(db, 'withdrawals'), (snapshot) => {
        const container = document.getElementById('withdrawRequestsContainer'); container.innerHTML = '';
        const data = snapshot.val(); if (!data) return;
        Object.entries(data).reverse().forEach(([key, item]) => {
          if (item.status === 'pending') {
            const div = document.createElement('div');
            div.className = "p-3 bg-gray-900 rounded-lg border border-gray-800 flex justify-between items-center text-xs";
            div.innerHTML = `
              <div>
                <p class="font-bold">${item.email}</p>
                <p class="text-amber-400">${item.method}: PKR ${item.amount} (Acc: ${item.account})</p>
              </div>
              <div class="flex gap-2">
                <button onclick="approveWithdrawal('${key}')" class="bg-amber-600 px-2 py-1 rounded text-black font-bold">Mark Paid</button>
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
      if (!account || !amount || amount < 500) return alert("Minimum withdrawal is PKR 500!");

      const walletRef = ref(db, `wallets/${currentUser.uid}/balance`);
      const snap = await get(walletRef);
      const currentBal = snap.exists() ? snap.val() : 0;
      if (currentBal < amount) return alert("Insufficient balance!");

      await set(walletRef, currentBal - amount);
      const wRef = push(ref(db, 'withdrawals'));
      await set(wRef, {
        uid: currentUser.uid,
        email: currentUser.email,
        method,
        account,
        amount,
        status: 'pending',
        timestamp: Date.now()
      });

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
    function openAnalyticsModal() { toggleModal('analyticsModal'); }
    function openBoostInfo() { alert("Boost Feature: Pay a small fee to pin your post on top of everyone's feed!"); }
    function joinCommunity(name) { alert("Welcome to " + name + " community group!"); }
    
    function switchTab(tab) {
      document.getElementById('feedTab').classList.add('hidden');
      document.getElementById('reelsTab').classList.add('hidden');
      document.getElementById('groupsTab').classList.add('hidden');
      if (tab === 'feed') document.getElementById('feedTab').classList.remove('hidden');
      if (tab === 'reels') document.getElementById('reelsTab').classList.remove('hidden');
      if (tab === 'groups') document.getElementById('groupsTab').classList.remove('hidden');
    }
  </script>
</body>
</html>
