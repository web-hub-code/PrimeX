<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PrimeX - All-in-One Social Ecosystem</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        .no-scrollbar::-webkit-scrollbar { display: none; }
        .no-scrollbar { -ms-overflow-style: none; scrollbar-width: none; }
        .reel-snap { scroll-snap-type: y mandatory; }
        .reel-item { scroll-snap-align: start; }
    </style>
</head>
<body class="bg-black text-white min-h-screen flex justify-center font-sans overflow-hidden">

    <!-- Mobile Wrapper -->
    <div class="w-full max-w-md h-screen flex flex-col justify-between bg-gray-950 relative border-x border-gray-800">

        <!-- Top Header -->
        <header class="h-14 border-b border-gray-800/80 px-4 flex justify-between items-center bg-gray-950/90 backdrop-blur z-20 sticky top-0">
            <h1 class="text-xl font-black tracking-wider text-indigo-500">PrimeX<span class="text-xs text-indigo-400 font-normal ml-1">v2.0</span></h1>
            <div id="user-header-actions" class="flex items-center gap-3 hidden">
                <button id="btn-create-post" class="bg-indigo-600 hover:bg-indigo-700 text-xs px-3 py-1.5 rounded-full font-bold transition flex items-center gap-1">
                    <i class="fa-solid fa-plus"></i> Post
                </button>
                <button id="btn-logout" class="text-gray-400 hover:text-red-400 text-xs transition">
                    <i class="fa-solid fa-right-from-bracket text-lg"></i>
                </button>
            </div>
        </header>

        <!-- Auth View -->
        <main id="auth-view" class="flex-1 p-6 flex flex-col justify-center items-center">
            <div class="w-full bg-gray-900 border border-gray-800 rounded-3xl p-6 shadow-2xl text-center">
                <h2 class="text-2xl font-black mb-1">Join PrimeX</h2>
                <p class="text-gray-400 text-xs mb-6">Experience the next generation of social media</p>

                <button id="btn-google" class="w-full bg-white text-gray-900 font-semibold py-2.5 px-4 rounded-xl flex items-center justify-center gap-3 transition mb-4 shadow">
                    <i class="fa-brands fa-google text-red-500 text-lg"></i>
                    <span>Continue with Google</span>
                </button>

                <div class="flex items-center my-4">
                    <hr class="flex-grow border-gray-800">
                    <span class="px-3 text-xs text-gray-500">OR</span>
                    <hr class="flex-grow border-gray-800">
                </div>

                <form id="auth-form" class="space-y-3">
                    <input type="email" id="email" placeholder="Email Address" required class="w-full bg-gray-950 border border-gray-800 rounded-xl px-4 py-2.5 text-sm focus:outline-none focus:border-indigo-500">
                    <input type="password" id="password" placeholder="Password" required class="w-full bg-gray-950 border border-gray-800 rounded-xl px-4 py-2.5 text-sm focus:outline-none focus:border-indigo-500">
                    
                    <div class="flex gap-2 pt-2">
                        <button type="submit" id="btn-login" class="w-1/2 bg-indigo-600 hover:bg-indigo-700 font-bold py-2.5 rounded-xl text-xs uppercase tracking-wider transition">Login</button>
                        <button type="button" id="btn-signup" class="w-1/2 bg-gray-800 hover:bg-gray-700 font-bold py-2.5 rounded-xl text-xs uppercase tracking-wider transition">Sign Up</button>
                    </div>
                </form>

                <p id="auth-error" class="text-red-400 text-xs mt-3 hidden"></p>
            </div>
        </main>

        <!-- Main App Views Container -->
        <main id="app-view" class="flex-1 overflow-y-auto no-scrollbar hidden relative">
            
            <!-- Feed / Reels Container (TikTok Style Vertical Scroll) -->
            <div id="reels-feed" class="h-full w-full overflow-y-scroll reel-snap no-scrollbar">
                <!-- Dynamic Posts Render Here -->
            </div>

            <!-- Create Post Modal -->
            <div id="upload-modal" class="fixed inset-0 bg-black/80 backdrop-blur-sm z-50 flex items-center justify-center p-4 hidden">
                <div class="bg-gray-900 border border-gray-800 w-full max-w-sm rounded-2xl p-5 relative">
                    <button id="close-modal" class="absolute top-4 right-4 text-gray-400 hover:text-white">
                        <i class="fa-solid fa-xmark text-lg"></i>
                    </button>
                    <h3 class="text-lg font-bold mb-4">Create PrimeX Post</h3>
                    
                    <textarea id="post-caption" rows="3" placeholder="Write a caption..." class="w-full bg-gray-950 border border-gray-800 rounded-xl p-3 text-sm focus:outline-none focus:border-indigo-500 mb-3 resize-none"></textarea>
                    
                    <input type="text" id="post-media-url" placeholder="Image / Video URL (https://...)" class="w-full bg-gray-950 border border-gray-800 rounded-xl px-4 py-2.5 text-sm focus:outline-none focus:border-indigo-500 mb-4">
                    
                    <button id="btn-submit-post" class="w-full bg-indigo-600 hover:bg-indigo-700 font-bold py-2.5 rounded-xl text-sm transition">Publish Post</button>
                </div>
            </div>

        </main>

        <!-- Bottom Navigation Bar (Instagram Style) -->
        <nav id="bottom-nav" class="h-16 border-t border-gray-800/80 bg-gray-950/95 backdrop-blur px-6 flex justify-between items-center z-20 hidden">
            <button class="flex flex-col items-center gap-1 text-indigo-500">
                <i class="fa-solid fa-house text-lg"></i>
                <span class="text-[10px] font-medium">Home</span>
            </button>
            <button class="flex flex-col items-center gap-1 text-gray-400 hover:text-white">
                <i class="fa-solid fa-compass text-lg"></i>
                <span class="text-[10px] font-medium">Explore</span>
            </button>
            <button id="nav-btn-create" class="flex flex-col items-center justify-center w-10 h-10 bg-indigo-600 rounded-full text-white shadow-lg shadow-indigo-500/30">
                <i class="fa-solid fa-plus text-lg"></i>
            </button>
            <button class="flex flex-col items-center gap-1 text-gray-400 hover:text-white">
                <i class="fa-solid fa-wallet text-lg"></i>
                <span class="text-[10px] font-medium">Wallet</span>
            </button>
            <button class="flex flex-col items-center gap-1 text-gray-400 hover:text-white">
                <i class="fa-solid fa-user text-lg"></i>
                <span class="text-[10px] font-medium">Profile</span>
            </button>
        </nav>

    </div>

    <!-- Firebase SDK v10 -->
    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
        import { 
            getAuth, 
            GoogleAuthProvider, 
            signInWithPopup, 
            createUserWithEmailAndPassword, 
            signInWithEmailAndPassword, 
            onAuthStateChanged,
            signOut 
        } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-auth.js";
        import { getDatabase, ref, set, push, onValue, update } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-database.js";

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

        // UI References
        const authView = document.getElementById('auth-view');
        const appView = document.getElementById('app-view');
        const bottomNav = document.getElementById('bottom-nav');
        const userHeaderActions = document.getElementById('user-header-actions');
        const reelsFeed = document.getElementById('reels-feed');
        const uploadModal = document.getElementById('upload-modal');
        const authError = document.getElementById('auth-error');

        const showError = (msg) => {
            authError.textContent = msg;
            authError.classList.remove('hidden');
        };

        // Auth Listener
        onAuthStateChanged(auth, (user) => {
            if (user) {
                currentUser = user;
                authView.classList.add('hidden');
                appView.classList.remove('hidden');
                bottomNav.classList.remove('hidden');
                userHeaderActions.classList.remove('hidden');
                loadPosts();
            } else {
                currentUser = null;
                authView.classList.remove('hidden');
                appView.classList.add('hidden');
                bottomNav.classList.add('hidden');
                userHeaderActions.classList.add('hidden');
            }
        });

        // Login & Signup Event Handlers
        document.getElementById('btn-google').addEventListener('click', () => {
            signInWithPopup(auth, googleProvider).catch((e) => showError(e.message));
        });

        document.getElementById('auth-form').addEventListener('submit', (e) => {
            e.preventDefault();
            const em = document.getElementById('email').value;
            const pass = document.getElementById('password').value;
            signInWithEmailAndPassword(auth, em, pass).catch((e) => showError(e.message));
        });

        document.getElementById('btn-signup').addEventListener('click', () => {
            const em = document.getElementById('email').value;
            const pass = document.getElementById('password').value;
            createUserWithEmailAndPassword(auth, em, pass).catch((e) => showError(e.message));
        });

        document.getElementById('btn-logout').addEventListener('click', () => signOut(auth));

        // Create Post Modal Controls
        const toggleModal = (show) => uploadModal.classList.toggle('hidden', !show);
        document.getElementById('btn-create-post').addEventListener('click', () => toggleModal(true));
        document.getElementById('nav-btn-create').addEventListener('click', () => toggleModal(true));
        document.getElementById('close-modal').addEventListener('click', () => toggleModal(false));

        // Publish Post to Firebase Database
        document.getElementById('btn-submit-post').addEventListener('click', () => {
            const caption = document.getElementById('post-caption').value.trim();
            const mediaUrl = document.getElementById('post-media-url').value.trim();

            if (!mediaUrl) {
                alert("Please provide an image or video URL!");
                return;
            }

            const postsRef = ref(db, 'posts');
            const newPostRef = push(postsRef);
            
            set(newPostRef, {
                id: newPostRef.key,
                uid: currentUser.uid,
                author: currentUser.displayName || currentUser.email.split('@')[0],
                caption: caption,
                mediaUrl: mediaUrl,
                likesCount: 0,
                timestamp: Date.now()
            }).then(() => {
                document.getElementById('post-caption').value = '';
                document.getElementById('post-media-url').value = '';
                toggleModal(false);
            });
        });

        // Realtime Feed Rendering (Full Screen Reel Scroll)
        function loadPosts() {
            const postsRef = ref(db, 'posts');
            onValue(postsRef, (snapshot) => {
                reelsFeed.innerHTML = '';
                const data = snapshot.val();
                if (!data) {
                    reelsFeed.innerHTML = `<div class="h-full flex flex-col justify-center items-center text-gray-500 text-xs"><i class="fa-regular fa-folder-open text-3xl mb-2"></i>No posts yet. Be the first to publish!</div>`;
                    return;
                }

                const postsArray = Object.values(data).reverse();
                postsArray.forEach((post) => {
                    const postCard = document.createElement('div');
                    postCard.className = 'reel-item h-full w-full relative flex flex-col justify-between bg-gray-900 border-b border-gray-800';
                    
                    const isVideo = post.mediaUrl.match(/\.(mp4|webm|ogg)$/i);
                    
                    postCard.innerHTML = `
                        <!-- Media Background -->
                        <div class="absolute inset-0 z-0 flex items-center justify-center bg-black">
                            ${isVideo ? 
                                `<video src="${post.mediaUrl}" class="w-full h-full object-cover" autoplay loop muted playsinline></video>` : 
                                `<img src="${post.mediaUrl}" class="w-full h-full object-cover" alt="PrimeX Content">`
                            }
                        </div>

                        <!-- Shadow Overlay -->
                        <div class="absolute inset-0 bg-gradient-to-b from-black/40 via-transparent to-black/90 z-10 pointer-events-none"></div>

                        <!-- Top Info -->
                        <div class="relative z-20 p-4 flex items-center gap-3">
                            <div class="w-9 h-9 bg-indigo-600 rounded-full flex items-center justify-center font-bold text-xs uppercase shadow">
                                ${post.author.charAt(0)}
                            </div>
                            <div>
                                <h4 class="text-sm font-bold">${post.author}</h4>
                                <span class="text-[10px] text-gray-300">PrimeX Creator</span>
                            </div>
                        </div>

                        <!-- Right Actions Sidebar -->
                        <div class="absolute right-4 bottom-20 z-20 flex flex-col gap-5 items-center">
                            <button onclick="likePost('${post.id}', ${post.likesCount || 0})" class="flex flex-col items-center gap-1 text-white">
                                <div class="w-11 h-11 bg-gray-900/60 backdrop-blur rounded-full flex items-center justify-center text-rose-500 text-lg shadow">
                                    <i class="fa-solid fa-heart"></i>
                                </div>
                                <span class="text-xs font-semibold">${post.likesCount || 0}</span>
                            </button>
                            <button class="flex flex-col items-center gap-1 text-white">
                                <div class="w-11 h-11 bg-gray-900/60 backdrop-blur rounded-full flex items-center justify-center text-gray-200 text-lg shadow">
                                    <i class="fa-solid fa-comment-dots"></i>
                                </div>
                                <span class="text-xs font-semibold">0</span>
                            </button>
                            <button class="flex flex-col items-center gap-1 text-white">
                                <div class="w-11 h-11 bg-gray-900/60 backdrop-blur rounded-full flex items-center justify-center text-gray-200 text-lg shadow">
                                    <i class="fa-solid fa-share"></i>
                                </div>
                                <span class="text-xs font-semibold">Share</span>
                            </button>
                        </div>

                        <!-- Bottom Caption Info -->
                        <div class="relative z-20 p-4 mb-2">
                            <p class="text-sm font-medium mb-1 drop-shadow">${post.caption || ''}</p>
                            <span class="text-[11px] text-indigo-400 font-semibold"><i class="fa-solid fa-music text-xs mr-1"></i> PrimeX Original Audio</span>
                        </div>
                    `;
                    reelsFeed.appendChild(postCard);
                });
            });
        }

        // Global Like Function
        window.likePost = (postId, currentLikes) => {
            const postRef = ref(db, `posts/${postId}`);
            update(postRef, {
                likesCount: currentLikes + 1
            });
        };
    </script>
</body>
</html>
