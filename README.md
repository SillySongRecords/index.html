<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Browncow Distribution</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/3.7.0/chart.min.js"></script>
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #f8fafc;
        }
        .theme-purple { background-color: #5a4ae3; }
        .theme-text { color: #5a4ae3; }
        .theme-border { border-color: #5a4ae3; }
        .btn-primary {
            background-color: #5a4ae3;
            color: white;
            transition: background-color 0.3s;
        }
        .btn-primary:hover {
            background-color: #4b3bc5;
        }
        .btn-secondary {
            background-color: #e2e8f0;
            color: #475569;
            transition: background-color 0.3s;
        }
        .btn-secondary:hover {
            background-color: #cbd5e1;
        }
        /* Hide scrollbar for Chrome, Safari and Opera */
        .no-scrollbar::-webkit-scrollbar {
            display: none;
        }
        /* Hide scrollbar for IE, Edge and Firefox */
        .no-scrollbar {
            -ms-overflow-style: none;  /* IE and Edge */
            scrollbar-width: none;  /* Firefox */
        }
        .view {
            display: none;
        }
        .active-view {
            display: block;
        }
        .animate-spin {
            animation: spin 1s linear infinite;
        }
        @keyframes spin {
            from { transform: rotate(0deg); }
            to { transform: rotate(360deg); }
        }
    </style>
</head>
<body class="bg-gray-50">

    <!-- Loading Spinner Overlay -->
    <div id="loading-overlay" class="fixed inset-0 bg-black bg-opacity-50 z-50 flex items-center justify-center hidden">
        <div class="animate-spin rounded-full h-16 w-16 border-t-4 border-b-4 border-white"></div>
    </div>
    
    <!-- Toast Notification -->
    <div id="toast" class="fixed top-5 right-5 bg-green-500 text-white py-2 px-4 rounded-lg shadow-lg hidden transition-opacity duration-300">
        <p id="toast-message"></p>
    </div>

    <!-- ===== AUTHENTICATION VIEW ===== -->
    <div id="auth-view" class="view active-view min-h-screen flex items-center justify-center bg-gray-100">
        <div class="w-full max-w-md p-8 space-y-8 bg-white rounded-2xl shadow-lg">
            <!-- Login Form -->
            <div id="login-form">
                <div class="text-center">
                    <h2 class="text-3xl font-bold text-gray-900">
                        <span class="theme-text">Browncow</span> Distribution
                    </h2>
                    <p class="mt-2 text-sm text-gray-600">Welcome back! Please sign in.</p>
                </div>
                <form class="mt-8 space-y-6" onsubmit="handleLogin(event)">
                    <div class="rounded-md shadow-sm -space-y-px">
                        <div>
                            <input id="login-email" name="email" type="email" autocomplete="email" required class="appearance-none rounded-none relative block w-full px-3 py-2 border border-gray-300 placeholder-gray-500 text-gray-900 rounded-t-md focus:outline-none focus:ring-purple-500 focus:border-purple-500 focus:z-10 sm:text-sm" placeholder="Email address">
                        </div>
                        <div>
                            <input id="login-password" name="password" type="password" autocomplete="current-password" required class="appearance-none rounded-none relative block w-full px-3 py-2 border border-gray-300 placeholder-gray-500 text-gray-900 rounded-b-md focus:outline-none focus:ring-purple-500 focus:border-purple-500 focus:z-10 sm:text-sm" placeholder="Password">
                        </div>
                    </div>
                    <div>
                        <button type="submit" class="group relative w-full flex justify-center py-2 px-4 border border-transparent text-sm font-medium rounded-md text-white bg-purple-600 hover:bg-purple-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-purple-500 btn-primary">
                            Sign in
                        </button>
                    </div>
                </form>
                <div class="text-sm text-center mt-4">
                    <a href="#" id="show-signup" class="font-medium theme-text hover:text-purple-500">
                        Don't have an account? Sign up
                    </a>
                </div>
            </div>

            <!-- Signup Form -->
            <div id="signup-form" class="hidden">
                 <div class="text-center">
                    <h2 class="text-3xl font-bold text-gray-900">
                        <span class="theme-text">Browncow</span> Distribution
                    </h2>
                    <p class="mt-2 text-sm text-gray-600">Create your account to get started.</p>
                </div>
                <form class="mt-8 space-y-6" onsubmit="handleSignup(event)">
                     <div class="rounded-md shadow-sm">
                        <input id="signup-name" type="text" required class="appearance-none rounded-md relative block w-full px-3 py-2 border border-gray-300 placeholder-gray-500 text-gray-900 focus:outline-none focus:ring-purple-500 focus:border-purple-500 sm:text-sm mb-2" placeholder="Full Name or Artist Name">
                        <input id="signup-email" type="email" required class="appearance-none rounded-md relative block w-full px-3 py-2 border border-gray-300 placeholder-gray-500 text-gray-900 focus:outline-none focus:ring-purple-500 focus:border-purple-500 sm:text-sm mb-2" placeholder="Email address">
                        <input id="signup-password" type="password" required class="appearance-none rounded-md relative block w-full px-3 py-2 border border-gray-300 placeholder-gray-500 text-gray-900 focus:outline-none focus:ring-purple-500 focus:border-purple-500 sm:text-sm" placeholder="Password (min. 6 characters)">
                    </div>
                    <div>
                        <button type="submit" class="group relative w-full flex justify-center py-2 px-4 border border-transparent text-sm font-medium rounded-md text-white bg-purple-600 hover:bg-purple-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-purple-500 btn-primary">
                            Sign up
                        </button>
                    </div>
                </form>
                <div class="text-sm text-center mt-4">
                    <a href="#" id="show-login" class="font-medium theme-text hover:text-purple-500">
                        Already have an account? Sign in
                    </a>
                </div>
            </div>
        </div>
    </div>


    <!-- ===== MAIN APPLICATION VIEW (USER & ADMIN) ===== -->
    <div id="app-view" class="view">
        <div class="flex h-screen bg-gray-100">
            <!-- Sidebar -->
            <div class="hidden md:flex flex-col w-64 bg-white shadow-lg">
                <div class="flex items-center justify-center h-16 bg-white border-b">
                    <h1 class="text-2xl font-bold theme-text">Browncow</h1>
                </div>
                <div class="flex flex-col flex-grow p-4">
                    <nav id="user-nav" class="flex-grow space-y-2">
                        <!-- User navigation links will be inserted here -->
                    </nav>
                    <nav id="admin-nav" class="flex-grow space-y-2 hidden">
                        <!-- Admin navigation links will be inserted here -->
                    </nav>
                    <div class="mt-auto">
                        <a href="#" onclick="handleLogout()" class="flex items-center px-4 py-2 mt-2 text-sm font-medium text-gray-600 rounded-md hover:bg-gray-200">
                            <svg class="w-5 h-5 mr-3" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 16l4-4m0 0l-4-4m4 4H7m6 4v1a3 3 0 01-3 3H6a3 3 0 01-3-3V7a3 3 0 013-3h4a3 3 0 013 3v1"></path></svg>
                            Logout
                        </a>
                    </div>
                </div>
            </div>

            <!-- Main Content -->
            <div class="flex flex-col flex-1 overflow-y-auto">
                <header class="flex items-center justify-between h-16 bg-white border-b px-6">
                    <div class="flex items-center">
                         <button id="mobile-menu-button" class="md:hidden mr-4 text-gray-600">
                            <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16m-7 6h7"></path></svg>
                        </button>
                        <h1 id="page-title" class="text-xl font-semibold text-gray-800">Dashboard</h1>
                    </div>
                    <div class="flex items-center">
                        <span id="user-greeting" class="text-sm text-gray-600"></span>
                    </div>
                </header>

                <main class="p-6 md:p-10 space-y-8">
                    <!-- Dynamic Content Area -->
                    <div id="content-area">
                        <!-- Views will be rendered here -->
                    </div>
                </main>
            </div>
        </div>
        
        <!-- Mobile Sidebar -->
        <div id="mobile-menu" class="fixed inset-0 flex z-40 md:hidden hidden">
            <div class="fixed inset-0 bg-black opacity-25" id="mobile-menu-overlay"></div>
            <div class="relative flex-1 flex flex-col max-w-xs w-full bg-white">
                <div class="absolute top-0 right-0 -mr-12 pt-2">
                    <button id="mobile-menu-close" class="ml-1 flex items-center justify-center h-10 w-10 rounded-full focus:outline-none focus:ring-2 focus:ring-inset focus:ring-white">
                        <svg class="h-6 w-6 text-white" stroke="currentColor" fill="none" viewBox="0 0 24 24">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
                        </svg>
                    </button>
                </div>
                <div class="flex-1 h-0 pt-5 pb-4 overflow-y-auto">
                    <div class="flex-shrink-0 flex items-center px-4">
                        <h1 class="text-2xl font-bold theme-text">Browncow</h1>
                    </div>
                    <nav id="mobile-user-nav" class="mt-5 px-2 space-y-1">
                        <!-- Mobile user nav links -->
                    </nav>
                     <nav id="mobile-admin-nav" class="mt-5 px-2 space-y-1 hidden">
                        <!-- Mobile admin nav links -->
                    </nav>
                </div>
                 <div class="flex-shrink-0 flex border-t p-4">
                    <a href="#" onclick="handleLogout()" class="flex-shrink-0 group block">
                        <div class="flex items-center">
                            <div>
                                <svg class="w-6 h-6 text-gray-600" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 16l4-4m0 0l-4-4m4 4H7m6 4v1a3 3 0 01-3 3H6a3 3 0 01-3-3V7a3 3 0 013-3h4a3 3 0 013 3v1"></path></svg>
                            </div>
                            <div class="ml-3">
                                <p class="text-sm font-medium text-gray-700 group-hover:text-gray-900">Logout</p>
                            </div>
                        </div>
                    </a>
                </div>
            </div>
        </div>
    </div>


    <script type="module">
        // Firebase and App imports
        import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";
        import { getAuth, createUserWithEmailAndPassword, signInWithEmailAndPassword, onAuthStateChanged, signOut, updateProfile } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js";
        import { getFirestore, doc, setDoc, getDoc, addDoc, collection, query, where, getDocs, onSnapshot, updateDoc, orderBy } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";
        
        // IMPORTANT: Replace with your Firebase project configuration
        const firebaseConfig = {
            apiKey: "AIzaSyBimPDyP_2XWcuwvOpVUcfCAJE-G5pDrqs",
            authDomain: "bccr-899f8.firebaseapp.com",
            projectId: "bccr-899f8",
            storageBucket: "bccr-899f8.firebasestorage.app",
            messagingSenderId: "630028306842",
            appId: "1:630028306842:web:67bcefc01a26024d4ed223"
        };
        
        // IMPORTANT: Replace with your Cloudinary configuration
        const CLOUDINARY_CLOUD_NAME = "dp9on02kr"; 
        const CLOUDINARY_UPLOAD_PRESET = "bccccc";

        // Initialize Firebase
        const app = initializeApp(firebaseConfig);
        const auth = getAuth(app);
        const db = getFirestore(app);
        
        let currentUser = null;
        let isAdmin = false;

        // --- UI Elements ---
        const authView = document.getElementById('auth-view');
        const appView = document.getElementById('app-view');
        const contentArea = document.getElementById('content-area');
        const pageTitle = document.getElementById('page-title');
        const userGreeting = document.getElementById('user-greeting');
        const loadingOverlay = document.getElementById('loading-overlay');
        const toast = document.getElementById('toast');
        const toastMessage = document.getElementById('toast-message');

        // --- Navigation Setup ---
        const userNavLinks = [
            { name: 'Dashboard', icon: '<svg class="w-5 h-5 mr-3" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 12l2-2m0 0l7-7 7 7M5 10v10a1 1 0 001 1h3m10-11l2 2m-2-2v10a1 1 0 01-1 1h-3m-6 0a1 1 0 001-1v-4a1 1 0 011-1h2a1 1 0 011 1v4a1 1 0 001 1m-6 0h6"></path></svg>', view: 'user-dashboard' },
            { name: 'Create Release', icon: '<svg class="w-5 h-5 mr-3" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 6v6m0 0v6m0-6h6m-6 0H6"></path></svg>', view: 'create-release' },
            { name: 'My Releases', icon: '<svg class="w-5 h-5 mr-3" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 19V6l12-3v13M9 19c0 1.105-1.343 2-3 2s-3-.895-3-2 1.343-2 3-2 3 .895 3 2zm12-3c0 1.105-1.343 2-3 2s-3-.895-3-2 1.343-2 3-2 3 .895 3 2zM9 6l12-3"></path></svg>', view: 'my-releases' },
            { name: 'Analytics', icon: '<svg class="w-5 h-5 mr-3" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11 3.055A9.001 9.001 0 1020.945 13H11V3.055z"></path><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M20.488 9H15V3.512A9.025 9.025 0 0120.488 9z"></path></svg>', view: 'analytics' },
            { name: 'Payouts', icon: '<svg class="w-5 h-5 mr-3" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 9V7a2 2 0 00-2-2H5a2 2 0 00-2 2v6a2 2 0 002 2h2m2 4h10a2 2 0 002-2v-6a2 2 0 00-2-2H9a2 2 0 00-2 2v6a2 2 0 002 2zm7-5a2 2 0 11-4 0 2 2 0 014 0z"></path></svg>', view: 'payouts' },
        ];
        const adminNavLinks = [
            { name: 'Review Queue', icon: '<svg class="w-5 h-5 mr-3" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5H7a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2V7a2 2 0 00-2-2h-2M9 5a2 2 0 002 2h2a2 2 0 002-2M9 5a2 2 0 012-2h2a2 2 0 012 2m-6 9l2 2 4-4"></path></svg>', view: 'admin-review' },
            { name: 'Manage Users', icon: '<svg class="w-5 h-5 mr-3" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4.354a4 4 0 110 5.292M15 21H3v-1a6 6 0 0112 0v1zm0 0h6v-1a6 6 0 00-9-5.197M15 21a6 6 0 00-9-5.197M15 11a3 3 0 11-6 0 3 3 0 016 0z"></path></svg>', view: 'admin-users' },
        ];

        function createNavLink(link, index) {
            const isActive = index === 0;
            return `
                <a href="#" data-view="${link.view}" class="nav-link ${isActive ? 'bg-purple-100 theme-text' : 'text-gray-600'} flex items-center px-4 py-2 text-sm font-medium rounded-md hover:bg-gray-200">
                    ${link.icon}
                    ${link.name}
                </a>`;
        }
        
        // --- Authentication Logic ---
        window.handleLogin = async (e) => {
            e.preventDefault();
            showLoading(true);
            const email = document.getElementById('login-email').value;
            const password = document.getElementById('login-password').value;
            try {
                await signInWithEmailAndPassword(auth, email, password);
                showToast('Login successful!');
            } catch (error) {
                console.error("Login Error:", error);
                 if (error.code === 'auth/configuration-not-found') {
                    showToast('Auth not configured. Please enable Email/Password sign-in in Firebase.', 'error');
                } else {
                    showToast(`Error: ${error.message}`, 'error');
                }
            } finally {
                showLoading(false);
            }
        };

        window.handleSignup = async (e) => {
            e.preventDefault();
            showLoading(true);
            const name = document.getElementById('signup-name').value;
            const email = document.getElementById('signup-email').value;
            const password = document.getElementById('signup-password').value;
            try {
                const userCredential = await createUserWithEmailAndPassword(auth, email, password);
                const user = userCredential.user;
                await updateProfile(user, { displayName: name });
                // Create user document in Firestore
                await setDoc(doc(db, "users", user.uid), {
                    name: name,
                    email: email,
                    createdAt: new Date(),
                    isAdmin: false, // Default role
                    balance: 0
                });
                showToast('Signup successful! Welcome.');
            } catch (error) {
                console.error("Signup Error:", error);
                 if (error.code === 'auth/configuration-not-found') {
                    showToast('Auth not configured. Please enable Email/Password sign-in in Firebase.', 'error');
                } else {
                    showToast(`Error: ${error.message}`, 'error');
                }
            } finally {
                showLoading(false);
            }
        };
        
        window.handleLogout = async () => {
            showLoading(true);
            await signOut(auth);
            currentUser = null;
            isAdmin = false;
            showToast('Logged out successfully.');
            showLoading(false);
        };
        
        onAuthStateChanged(auth, async (user) => {
            if (user) {
                currentUser = user;
                const userDoc = await getDoc(doc(db, "users", user.uid));
                if (userDoc.exists() && userDoc.data().isAdmin) {
                    isAdmin = true;
                } else {
                    isAdmin = false;
                }
                
                if(!user.displayName && userDoc.exists()){
                    user.displayName = userDoc.data().name;
                }

                userGreeting.textContent = `Hello, ${user.displayName || user.email}`;
                setupAppUI();
                authView.classList.remove('active-view');
                appView.classList.add('active-view');
            } else {
                currentUser = null;
                isAdmin = false;
                authView.classList.add('active-view');
                appView.classList.remove('active-view');
            }
        });

        // --- UI & View Management ---
        function setupAppUI() {
            const userNavContainer = document.getElementById('user-nav');
            const adminNavContainer = document.getElementById('admin-nav');
            const mobileUserNavContainer = document.getElementById('mobile-user-nav');
            const mobileAdminNavContainer = document.getElementById('mobile-admin-nav');

            if (isAdmin) {
                userNavContainer.classList.add('hidden');
                mobileUserNavContainer.classList.add('hidden');
                adminNavContainer.classList.remove('hidden');
                mobileAdminNavContainer.classList.remove('hidden');
                adminNavContainer.innerHTML = adminNavLinks.map((link, i) => createNavLink(link, i)).join('');
                mobileAdminNavContainer.innerHTML = adminNavLinks.map((link, i) => createNavLink(link, i)).join('');
                navigateTo('admin-review');
            } else {
                adminNavContainer.classList.add('hidden');
                mobileAdminNavContainer.classList.add('hidden');
                userNavContainer.classList.remove('hidden');
                mobileUserNavContainer.classList.remove('hidden');
                userNavContainer.innerHTML = userNavLinks.map((link, i) => createNavLink(link, i)).join('');
                mobileUserNavContainer.innerHTML = userNavLinks.map((link, i) => createNavLink(link, i)).join('');
                navigateTo('user-dashboard');
            }
            
            document.querySelectorAll('.nav-link').forEach(link => {
                link.addEventListener('click', (e) => {
                    e.preventDefault();
                    const viewName = link.getAttribute('data-view');
                    navigateTo(viewName);
                    document.querySelectorAll('.nav-link').forEach(l => l.classList.remove('bg-purple-100', 'theme-text'));
                    document.querySelectorAll(`.nav-link[data-view="${viewName}"]`).forEach(l => l.classList.add('bg-purple-100', 'theme-text'));
                    document.getElementById('mobile-menu').classList.add('hidden');
                });
            });
        }
        
        function navigateTo(viewName) {
            const link = [...userNavLinks, ...adminNavLinks].find(l => l.view === viewName);
            if(link) pageTitle.textContent = link.name;
            
            switch(viewName) {
                case 'user-dashboard': renderUserDashboard(); break;
                case 'create-release': renderCreateReleaseForm(); break;
                case 'my-releases': renderMyReleases(); break;
                case 'analytics': renderAnalytics(); break;
                case 'payouts': renderPayouts(); break;
                case 'admin-review': renderAdminReviewQueue(); break;
                case 'admin-users': renderAdminUsers(); break;
            }
        }

        function showLoading(show) {
            loadingOverlay.classList.toggle('hidden', !show);
        }

        function showToast(message, type = 'success') {
            toastMessage.textContent = message;
            toast.classList.remove('hidden', 'bg-green-500', 'bg-red-500');
            toast.classList.add(type === 'success' ? 'bg-green-500' : 'bg-red-500');
            setTimeout(() => {
                toast.classList.add('hidden');
            }, 4000);
        }
        
        // --- View Renderers ---
        
        async function renderUserDashboard() {
            const userDoc = await getDoc(doc(db, "users", currentUser.uid));
            const userData = userDoc.data();
            const balance = userData.balance ? userData.balance.toFixed(2) : '0.00';

            contentArea.innerHTML = `
                <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                    <div class="bg-white p-6 rounded-xl shadow-md"><h3 class="text-lg font-semibold text-gray-700">Current Balance</h3><p class="text-3xl font-bold theme-text mt-2">$${balance}</p></div>
                    <div class="bg-white p-6 rounded-xl shadow-md"><h3 class="text-lg font-semibold text-gray-700">Total Releases</h3><p id="total-releases" class="text-3xl font-bold text-gray-800 mt-2">Loading...</p></div>
                    <div class="bg-white p-6 rounded-xl shadow-md"><h3 class="text-lg font-semibold text-gray-700">Live on Stores</h3><p id="live-releases" class="text-3xl font-bold text-gray-800 mt-2">Loading...</p></div>
                </div>
                <div class="mt-8 bg-white p-6 rounded-xl shadow-md">
                    <h3 class="text-xl font-semibold text-gray-800 mb-4">Recent Releases</h3>
                    <div id="recent-releases-list" class="space-y-4"><p>Loading recent releases...</p></div>
                </div>
            `;
            
            const q = query(collection(db, "releases"), where("userId", "==", currentUser.uid));
            onSnapshot(q, (querySnapshot) => {
                const releases = [];
                querySnapshot.forEach((doc) => releases.push({id: doc.id, ...doc.data()}));
                releases.sort((a, b) => (b.createdAt?.toDate() || 0) - (a.createdAt?.toDate() || 0));

                document.getElementById('total-releases').textContent = releases.length;
                document.getElementById('live-releases').textContent = releases.filter(r => r.status === 'live').length;

                let recentHtml = releases.length === 0 ? `<p class="text-gray-500">You haven't created any releases yet. Click 'Create Release' to get started!</p>` : releases.slice(0, 5).map(createReleaseListItem).join('');
                document.getElementById('recent-releases-list').innerHTML = recentHtml;
            });
        }
        
        function renderCreateReleaseForm() {
            contentArea.innerHTML = `
                <div class="bg-white p-8 rounded-xl shadow-md max-w-4xl mx-auto">
                    <h2 class="text-2xl font-bold text-gray-800 mb-6">Create New Release</h2>
                    <form id="create-release-form">
                        <div class="mb-6">
                            <h3 class="text-lg font-semibold mb-2 text-gray-700">1. Upload Files</h3>
                            <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                                <div>
                                    <label class="block text-sm font-medium text-gray-700 mb-1">Audio File (WAV, FLAC, MP3)</label>
                                    <input type="file" id="audio-file" required class="block w-full text-sm text-gray-500 file:mr-4 file:py-2 file:px-4 file:rounded-full file:border-0 file:text-sm file:font-semibold file:bg-purple-50 file:text-purple-700 hover:file:bg-purple-100"/>
                                    <div id="audio-upload-progress" class="mt-2"></div>
                                </div>
                                <div>
                                    <label class="block text-sm font-medium text-gray-700 mb-1">Cover Art (3000x3000px, JPG)</label>
                                    <input type="file" id="artwork-file" required class="block w-full text-sm text-gray-500 file:mr-4 file:py-2 file:px-4 file:rounded-full file:border-0 file:text-sm file:font-semibold file:bg-purple-50 file:text-purple-700 hover:file:bg-purple-100"/>
                                    <div id="artwork-upload-progress" class="mt-2"></div>
                                </div>
                            </div>
                        </div>
                        <div class="mb-6 border-t pt-6">
                            <h3 class="text-lg font-semibold mb-4 text-gray-700">2. Release Information</h3>
                             <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                                <div><label class="block text-sm font-medium text-gray-700">Song Title</label><input type="text" id="song-title" required class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-purple-500 focus:ring-purple-500 sm:text-sm"></div>
                                <div><label class="block text-sm font-medium text-gray-700">Primary Artist</label><input type="text" id="primary-artist" required placeholder="Your artist name" value="${currentUser.displayName || ''}" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-purple-500 focus:ring-purple-500 sm:text-sm"></div>
                                <div><label class="block text-sm font-medium text-gray-700">Featured Artists (optional)</label><input type="text" id="featured-artists" placeholder="e.g., Artist A, Artist B" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-purple-500 focus:ring-purple-500 sm:text-sm"></div>
                                <div><label class="block text-sm font-medium text-gray-700">Release Date</label><input type="date" id="release-date" required class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-purple-500 focus:ring-purple-500 sm:text-sm"></div>
                                <div><label class="block text-sm font-medium text-gray-700">Genre</label><select id="genre" required class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-purple-500 focus:ring-purple-500 sm:text-sm"><option>Pop</option><option>Rock</option><option>Hip-Hop/Rap</option><option>Electronic</option><option>R&B</option><option>Country</option><option>Jazz</option></select></div>
                                <div><label class="block text-sm font-medium text-gray-700">Record Label</label><input type="text" id="record-label" placeholder="Your label name" value="${currentUser.displayName || ''}" required class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-purple-500 focus:ring-purple-500 sm:text-sm"></div>
                            </div>
                        </div>
                        <div class="mb-6 border-t pt-6">
                             <h3 class="text-lg font-semibold mb-4 text-gray-700">3. Select Stores</h3>
                             <div class="grid grid-cols-2 md:grid-cols-4 gap-4">
                                ${['Spotify', 'Apple Music', 'Amazon Music', 'Tidal', 'Deezer', 'YouTube Music', 'Pandora', 'TikTok'].map(dsp => `<label class="flex items-center space-x-2 border p-3 rounded-lg hover:bg-gray-50"><input type="checkbox" name="stores" value="${dsp}" class="h-4 w-4 rounded border-gray-300 text-purple-600 focus:ring-purple-500" checked><span class="text-sm font-medium text-gray-700">${dsp}</span></label>`).join('')}
                            </div>
                        </div>
                        <div class="flex justify-end mt-8"><button type="submit" class="btn-primary font-bold py-2 px-6 rounded-lg">Submit for Review</button></div>
                    </form>
                </div>
            `;
            document.getElementById('create-release-form').addEventListener('submit', handleCreateRelease);
        }

        async function handleCreateRelease(e) {
            e.preventDefault();
            showLoading(true);

            if (CLOUDINARY_CLOUD_NAME === "YOUR_CLOUD_NAME" || CLOUDINARY_UPLOAD_PRESET === "YOUR_UPLOAD_PRESET") {
                 showToast('Cloudinary is not configured. Please follow the README.', 'error');
                 showLoading(false);
                 return;
            }

            const audioFile = document.getElementById('audio-file').files[0];
            const artworkFile = document.getElementById('artwork-file').files[0];
            if (!audioFile || !artworkFile) {
                showToast('Please upload both audio and artwork files.', 'error');
                showLoading(false);
                return;
            }

            try {
                const audioUrl = await uploadFile(audioFile, 'audio-upload-progress');
                const artworkUrl = await uploadFile(artworkFile, 'artwork-upload-progress');
                const selectedStores = Array.from(document.querySelectorAll('input[name="stores"]:checked')).map(el => el.value);
                
                const releaseData = {
                    userId: currentUser.uid, artist: document.getElementById('primary-artist').value, title: document.getElementById('song-title').value,
                    featuredArtists: document.getElementById('featured-artists').value, releaseDate: document.getElementById('release-date').value,
                    genre: document.getElementById('genre').value, recordLabel: document.getElementById('record-label').value,
                    stores: selectedStores, audioUrl, artworkUrl, status: 'in-review', createdAt: new Date(),
                };

                await addDoc(collection(db, 'releases'), releaseData);
                showToast('Release submitted for review successfully!');
                navigateTo('my-releases');
            } catch (error) {
                console.error("Error creating release:", error);
                showToast(`Error: ${error}`, 'error');
            } finally {
                showLoading(false);
            }
        }
        
        function uploadFile(file, progressElementId) {
            return new Promise((resolve, reject) => {
                const url = `https://api.cloudinary.com/v1_1/${CLOUDINARY_CLOUD_NAME}/auto/upload`;
                const formData = new FormData();
                formData.append('file', file);
                formData.append('upload_preset', CLOUDINARY_UPLOAD_PRESET);

                const xhr = new XMLHttpRequest();
                xhr.open('POST', url, true);
                const progressDiv = document.getElementById(progressElementId);

                xhr.upload.onprogress = function(e) {
                    if (e.lengthComputable) {
                        const progress = (e.loaded / e.total) * 100;
                        if(progressDiv) progressDiv.innerHTML = `<div class="w-full bg-gray-200 rounded-full h-2.5"><div class="bg-purple-600 h-2.5 rounded-full" style="width: ${progress}%"></div></div><p class="text-xs text-center">${Math.round(progress)}%</p>`;
                    }
                };
                xhr.onload = function() {
                    if (xhr.status === 200) {
                        const response = JSON.parse(xhr.responseText);
                        if(progressDiv) progressDiv.innerHTML = `<p class="text-sm text-green-600">Upload complete!</p>`;
                        resolve(response.secure_url);
                    } else {
                        const error = JSON.parse(xhr.responseText);
                        console.error("Upload Error:", error);
                        reject(error.error.message);
                    }
                };
                xhr.onerror = function() {
                    reject('An error occurred during the upload.');
                };
                xhr.send(formData);
            });
        }
        
        function renderMyReleases() {
             contentArea.innerHTML = `
                <div class="bg-white p-6 rounded-xl shadow-md">
                    <h2 class="text-xl font-semibold text-gray-800 mb-4">My Releases</h2>
                    <div id="my-releases-list" class="space-y-4"><p>Loading your releases...</p></div>
                </div>
            `;
            
            const q = query(collection(db, "releases"), where("userId", "==", currentUser.uid));
            onSnapshot(q, (querySnapshot) => {
                const listEl = document.getElementById('my-releases-list');
                if (querySnapshot.empty) {
                    listEl.innerHTML = `<p class="text-gray-500">You haven't submitted any releases yet.</p>`;
                    return;
                }
                const releases = [];
                querySnapshot.forEach(doc => releases.push({id: doc.id, ...doc.data()}));
                releases.sort((a, b) => (b.createdAt?.toDate() || 0) - (a.createdAt?.toDate() || 0));
                listEl.innerHTML = releases.map(createReleaseListItem).join('');
            });
        }
        
        function getStatusBadge(status) {
            const badges = {
                'in-review': 'bg-yellow-100 text-yellow-800', 'approved': 'bg-blue-100 text-blue-800',
                'live': 'bg-green-100 text-green-800', 'rejected': 'bg-red-100 text-red-800',
            };
            const badgeClass = badges[status] || 'bg-gray-100 text-gray-800';
            return `<span class="${badgeClass} text-xs font-medium mr-2 px-2.5 py-0.5 rounded-full">${status.replace('-', ' ')}</span>`;
        }
        
        function createReleaseListItem(release) {
            return `
                <div class="border rounded-lg p-4 flex items-center justify-between hover:bg-gray-50">
                    <div class="flex items-center min-w-0">
                        <img src="${release.artworkUrl}" alt="Artwork" class="w-12 h-12 rounded-md mr-4 object-cover flex-shrink-0">
                        <div class="min-w-0">
                            <p class="font-semibold text-gray-800 truncate">${release.title}</p>
                            <p class="text-sm text-gray-500 truncate">${release.artist}</p>
                        </div>
                    </div>
                    <div class="text-right flex-shrink-0 ml-4">
                        ${getStatusBadge(release.status)}
                        <p class="text-xs text-gray-400 mt-1">Release: ${release.releaseDate}</p>
                        ${release.status === 'rejected' ? `<p class="text-xs text-red-500 mt-1 truncate" title="Reason: ${release.rejectionReason}">Reason: ${release.rejectionReason || 'N/A'}</p>` : ''}
                    </div>
                </div>
            `;
        }
        
        function renderAnalytics() {
            contentArea.innerHTML = `
                <div class="bg-white p-6 rounded-xl shadow-md">
                    <h2 class="text-xl font-semibold text-gray-800 mb-4">Analytics</h2>
                    <p class="text-gray-600">This is a demo. Analytics data is randomly generated.</p>
                    <div class="mt-4">
                        <label for="release-select" class="block text-sm font-medium text-gray-700">Select a release to view stats</label>
                        <select id="release-select" class="mt-1 block w-full pl-3 pr-10 py-2 text-base border-gray-300 focus:outline-none focus:ring-purple-500 focus:border-purple-500 sm:text-sm rounded-md"></select>
                    </div>
                    <div class="mt-6"><canvas id="streamsChart"></canvas></div>
                </div>
            `;
            
            const q = query(collection(db, "releases"), where("userId", "==", currentUser.uid), where("status", "==", "live"));
            getDocs(q).then(snapshot => {
                const selectEl = document.getElementById('release-select');
                if(snapshot.empty) {
                    selectEl.innerHTML = `<option>No live releases to show analytics for.</option>`;
                    return;
                }
                snapshot.forEach(doc => {
                    const release = doc.data();
                    selectEl.innerHTML += `<option value="${doc.id}">${release.title} - ${release.artist}</option>`;
                });
                renderChart(); 
                selectEl.onchange = renderChart;
            });
        }
        
        let streamsChartInstance = null;
        function renderChart() {
            const ctx = document.getElementById('streamsChart').getContext('2d');
            const labels = ['Spotify', 'Apple Music', 'Amazon Music', 'Tidal', 'Deezer', 'TikTok'];
            const data = labels.map(() => Math.floor(Math.random() * 50000));
            if (streamsChartInstance) streamsChartInstance.destroy();
            streamsChartInstance = new Chart(ctx, {
                type: 'bar',
                data: { labels, datasets: [{ label: '# of Streams', data, backgroundColor: 'rgba(90, 74, 227, 0.6)', borderColor: 'rgba(90, 74, 227, 1)', borderWidth: 1, borderRadius: 5 }] },
                options: { responsive: true, scales: { y: { beginAtZero: true } } }
            });
        }

        async function renderPayouts() {
            const userDoc = await getDoc(doc(db, "users", currentUser.uid));
            const userData = userDoc.data();
            const balance = userData?.balance ? userData.balance.toFixed(2) : '0.00';
            
            contentArea.innerHTML = `
                <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
                    <div class="md:col-span-1 bg-white p-6 rounded-xl shadow-md">
                        <h3 class="text-lg font-semibold text-gray-700">Available for Payout</h3>
                        <p class="text-4xl font-bold theme-text mt-2">$${balance}</p>
                        <button id="request-payout-btn" class="w-full mt-4 btn-primary font-bold py-2 px-4 rounded-lg ${balance <= 0 ? 'opacity-50 cursor-not-allowed' : ''}" ${balance <= 0 ? 'disabled' : ''}>Request Payout</button>
                    </div>
                    <div class="md:col-span-2 bg-white p-6 rounded-xl shadow-md">
                        <h3 class="text-xl font-semibold text-gray-800 mb-4">Payout History</h3>
                        <div id="payouts-history-list" class="space-y-3"></div>
                    </div>
                </div>
            `;

            document.getElementById('request-payout-btn').addEventListener('click', async () => {
                if(balance > 0) {
                    showLoading(true);
                    try {
                        await addDoc(collection(db, "payouts"), { userId: currentUser.uid, userName: currentUser.displayName, amount: userData.balance, status: 'pending', requestedAt: new Date() });
                        await updateDoc(doc(db, "users", currentUser.uid), { balance: 0 });
                        showToast('Payout requested successfully!');
                        renderPayouts();
                    } catch(e) {
                        showToast('Error requesting payout.', 'error');
                        console.error(e);
                    } finally {
                        showLoading(false);
                    }
                }
            });
            
            const q = query(collection(db, "payouts"), where("userId", "==", currentUser.uid));
            onSnapshot(q, (snapshot) => {
                const listEl = document.getElementById('payouts-history-list');
                if(snapshot.empty) {
                    listEl.innerHTML = `<p class="text-gray-500">No payout history.</p>`;
                    return;
                }
                let html = '';
                snapshot.forEach(doc => {
                    const p = doc.data();
                    html += `<div class="flex justify-between items-center p-3 border rounded-md"><div><p class="font-medium text-gray-800">$${p.amount.toFixed(2)}</p><p class="text-xs text-gray-500">Requested on ${p.requestedAt.toDate().toLocaleDateString()}</p></div><span class="text-sm font-medium capitalize ${p.status === 'processed' ? 'text-green-600' : 'text-yellow-600'}">${p.status}</span></div>`;
                });
                listEl.innerHTML = html;
            });
        }
        
        // ADMIN VIEWS
        function renderAdminReviewQueue() {
             contentArea.innerHTML = `
                <div class="bg-white p-6 rounded-xl shadow-md">
                    <h2 class="text-xl font-semibold text-gray-800 mb-4">Release Review Queue</h2>
                    <div class="overflow-x-auto">
                        <table class="min-w-full divide-y divide-gray-200">
                            <thead class="bg-gray-50"><tr><th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase">Artist & Title</th><th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase">Release Date</th><th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase">Submitted</th><th class="px-6 py-3 text-right text-xs font-medium text-gray-500 uppercase">Actions</th></tr></thead>
                            <tbody id="review-queue-body" class="bg-white divide-y divide-gray-200"></tbody>
                        </table>
                    </div>
                </div>
            `;
            
            const q = query(collection(db, "releases"), where("status", "==", "in-review"));
            onSnapshot(q, (snapshot) => {
                const tbody = document.getElementById('review-queue-body');
                if(snapshot.empty) {
                    tbody.innerHTML = `<tr><td colspan="4" class="px-6 py-4 text-center text-gray-500">The review queue is empty. Great job!</td></tr>`;
                    return;
                }
                tbody.innerHTML = snapshot.docs.map(doc => {
                    const r = doc.data();
                    return `<tr><td class="px-6 py-4 whitespace-nowrap"><div class="flex items-center"><div class="flex-shrink-0 h-10 w-10"><img class="h-10 w-10 rounded-md" src="${r.artworkUrl}" alt=""></div><div class="ml-4"><div class="text-sm font-medium text-gray-900">${r.title}</div><div class="text-sm text-gray-500">${r.artist}</div></div></div></td><td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">${r.releaseDate}</td><td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">${r.createdAt.toDate().toLocaleDateString()}</td><td class="px-6 py-4 whitespace-nowrap text-right text-sm font-medium"><button onclick="window.reviewRelease('${doc.id}')" class="theme-text hover:text-purple-900">Review</button></td></tr>`;
                }).join('');
            });
        }
        
        window.reviewRelease = async (releaseId) => {
            const docRef = doc(db, "releases", releaseId);
            const releaseDoc = await getDoc(docRef);
            const r = releaseDoc.data();

            const modalHtml = `
                <div id="review-modal" class="fixed inset-0 bg-gray-600 bg-opacity-50 overflow-y-auto h-full w-full z-40">
                    <div class="relative top-20 mx-auto p-5 border w-full max-w-3xl shadow-lg rounded-md bg-white">
                        <div class="mt-3"><h3 class="text-xl leading-6 font-medium text-gray-900 mb-4">Review: ${r.title} by ${r.artist}</h3>
                            <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
                                <div class="md:col-span-1"><img src="${r.artworkUrl}" class="rounded-lg shadow-md w-full"><a href="${r.audioUrl}" target="_blank" class="block w-full text-center mt-4 bg-gray-200 hover:bg-gray-300 text-gray-800 font-bold py-2 px-4 rounded">Listen to Audio</a></div>
                                <div class="md:col-span-2 text-sm space-y-2 text-gray-700"><p><strong>Artist:</strong> ${r.artist}</p><p><strong>Title:</strong> ${r.title}</p><p><strong>Release Date:</strong> ${r.releaseDate}</p><p><strong>Genre:</strong> ${r.genre}</p><p><strong>Label:</strong> ${r.recordLabel}</p><p><strong>Stores:</strong> ${r.stores.join(', ')}</p></div>
                            </div>
                            <div class="mt-6 border-t pt-4"><label class="block text-sm font-medium text-gray-700">Rejection Reason (if applicable)</label><input type="text" id="rejection-reason" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm" placeholder="e.g., Artwork does not meet guidelines"></div>
                            <div class="items-center px-4 py-3 mt-4 space-x-2 flex justify-end"><button id="close-modal-btn" class="btn-secondary px-4 py-2 rounded-md">Cancel</button><button id="reject-btn" class="bg-red-500 hover:bg-red-600 text-white px-4 py-2 rounded-md">Reject</button><button id="approve-btn" class="bg-green-500 hover:bg-green-600 text-white px-4 py-2 rounded-md">Approve & Deliver</button></div>
                        </div>
                    </div>
                </div>`;
            document.body.insertAdjacentHTML('beforeend', modalHtml);
            
            const closeModal = () => document.getElementById('review-modal').remove();
            
            document.getElementById('close-modal-btn').onclick = closeModal;
            document.getElementById('approve-btn').onclick = async () => {
                await updateDoc(docRef, { status: 'approved' }); // In a real app, this would trigger delivery
                showToast('Release approved.', 'success');
                closeModal();
            };
            document.getElementById('reject-btn').onclick = async () => {
                const reason = document.getElementById('rejection-reason').value;
                if (!reason) { alert('Please provide a reason for rejection.'); return; }
                await updateDoc(docRef, { status: 'rejected', rejectionReason: reason });
                showToast('Release rejected and user notified.', 'success');
                closeModal();
            };
        }

        function renderAdminUsers() {
            contentArea.innerHTML = `
                <div class="bg-white p-6 rounded-xl shadow-md">
                    <h2 class="text-xl font-semibold text-gray-800 mb-4">User Management</h2>
                     <div class="overflow-x-auto"><table class="min-w-full divide-y divide-gray-200"><thead class="bg-gray-50"><tr><th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase">Name</th><th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase">Email</th><th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase">Balance</th></tr></thead><tbody id="users-list-body" class="bg-white divide-y divide-gray-200"></tbody></table></div>
                </div>
            `;
            onSnapshot(collection(db, "users"), (snapshot) => {
                const tbody = document.getElementById('users-list-body');
                tbody.innerHTML = snapshot.docs.map(doc => {
                    const u = doc.data();
                    return `<tr><td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-gray-900">${u.name}</td><td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">${u.email}</td><td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">$${(u.balance || 0).toFixed(2)}</td></tr>`;
                }).join('');
            });
        }
        
        // --- Event Listeners for UI toggles ---
        document.getElementById('show-signup').addEventListener('click', (e) => { e.preventDefault(); document.getElementById('login-form').classList.add('hidden'); document.getElementById('signup-form').classList.remove('hidden'); });
        document.getElementById('show-login').addEventListener('click', (e) => { e.preventDefault(); document.getElementById('signup-form').classList.add('hidden'); document.getElementById('login-form').classList.remove('hidden'); });
        const mobileMenu = document.getElementById('mobile-menu');
        document.getElementById('mobile-menu-button').addEventListener('click', () => mobileMenu.classList.remove('hidden'));
        document.getElementById('mobile-menu-close').addEventListener('click', () => mobileMenu.classList.add('hidden'));
        document.getElementById('mobile-menu-overlay').addEventListener('click', () => mobileMenu.classList.add('hidden'));

    </script>
</body>
</html>

