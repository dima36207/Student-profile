<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Digital Student Profile</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://unpkg.com/lucide@latest"></script>
    <style>
        /* Custom font and basic setup */
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap');
        
        /* Define U of M inspired colors for Tailwind utility classes */
        :root {
            --color-navy: #192a56; /* Deep Blue/Navy (Primary U of M) */
            --color-gold: #ffc300; /* Professional Gold/Yellow Accent (U of M Accent) */
        }
        
        body {
            font-family: 'Inter', sans-serif;
            /* Pale U of M-inspired background color for depth */
            background-color: #eef2f8; 
            /* Subtle texture/pattern for visual interest */
            background-image: radial-gradient(circle at 1px 1px, rgba(209, 213, 219, 0.2) 1px, transparent 0);
            background-size: 15px 15px;
            min-height: 100vh;
        }
        .profile-card {
            box-shadow: 0 15px 30px -5px rgba(0, 0, 0, 0.2), 0 8px 10px -6px rgba(0, 0, 0, 0.1);
            border: 1px solid rgba(0, 0, 0, 0.05);
            background-color: white; /* Keep card white to pop */
        }
        /* Style for the modal overlay */
        .modal-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.85);
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 100;
        }
        /* Ensure the logo container wraps content correctly */
        .logo-container {
            display: flex;
            justify-content: center;
            width: 100%;
            position: relative; /* Context for logo absolute positioning */
        }
        /* Custom style for the U of M logo placeholder */
        #uofm-logo {
            background-color: var(--color-navy);
            border: 2px solid var(--color-gold);
        }
        /* Custom button styling for primary actions (Navy/Gold) */
        .btn-primary {
            background-color: var(--color-navy);
            transition: background-color 0.3s, transform 0.1s;
        }
        .btn-primary:hover {
            background-color: #152240; /* Slightly darker navy */
            transform: translateY(-1px);
        }
        /* Custom button styling for secondary actions (Resume - Slate Gray) */
        .btn-secondary {
            background-color: #64748b; /* Slate Gray */
            transition: background-color 0.3s, transform 0.1s;
        }
        .btn-secondary:hover {
            background-color: #475569; /* Darker Slate Gray */
            transform: translateY(-1px);
        }
    </style>
</head>
<body class="flex flex-col items-center justify-center p-4">

    <div id="profile-container" class="profile-card bg-white w-full max-w-md mx-auto rounded-3xl p-8 text-center transition-all duration-300">
        
        <div class="logo-container">
            <a href="https://umanitoba.ca/" 
                target="_blank" 
                rel="noopener noreferrer" 
                aria-label="Visit University of Manitoba website"
                class="absolute top-0 right-0 w-12 h-12 rounded-full transition-transform duration-300 hover:scale-110 z-10">
                
                <img id="uofm-logo" src="https://placehold.co/50x50/192a56/ffc300?text=U+of+M" alt="University of Manitoba Logo" 
                    class="w-full h-full p-1 rounded-full border-2">
            </a>
        </div>
        
        <div class="flex flex-col items-center mt-4">
            <img id="profile-image" src="https://placehold.co/128x128/1e3a8a/ffffff?text=STUDENT" alt="Profile Picture" class="w-32 h-32 rounded-full object-cover ring-4 ring-yellow-500 mb-4 transition-transform duration-300 hover:scale-105">

            <h1 id="student-name" class="text-3xl font-bold text-gray-900 mb-1">Loading Profile...</h1>

            <p id="student-major" class="text-xl font-medium mb-4" style="color: var(--color-gold);">Finance, Asper School of Business</p>

            <div class="flex items-center justify-center text-sm text-gray-500 mb-8">
                <i data-lucide="shield" class="w-4 h-4 mr-1"></i>
                <span id="user-id-display" class="truncate max-w-xs">ID: Initializing...</span>
                <span id="connection-status" class="ml-3 px-2 py-0.5 rounded-full text-xs font-semibold bg-red-100 text-red-700">Offline</span>
            </div>

            <p id="student-bio" class="text-gray-600 mb-8 px-4">Driven Finance student at the Asper School of Business with proven customer service and team leadership skills. Seeking an internship to apply analytical rigor to real-world challenges.</p>

            <button id="view-resume-btn" class="btn-secondary flex items-center justify-center space-x-2 w-4/5 mx-auto text-white font-semibold py-3 px-4 rounded-xl transition duration-200 shadow-md mb-4">
                <i data-lucide="file-text" class="w-5 h-5"></i>
                <span>View My Resume</span>
            </button>
            
            <button id="cooperation-btn" class="btn-primary flex items-center justify-center space-x-2 w-4/5 mx-auto text-white font-semibold py-3 px-4 rounded-xl transition duration-200 shadow-lg mb-8">
                <i data-lucide="mail-check" class="w-5 h-5"></i>
                <span>Send Automated Follow-Up</span>
            </button>


            <div id="social-links-container" class="flex flex-wrap justify-center gap-4 mb-6">
                </div>
            
            <button id="edit-profile-btn" class="flex items-center space-x-2 bg-indigo-500 hover:bg-indigo-600 text-white font-semibold py-2 px-4 rounded-xl transition duration-200 hidden">
                <i data-lucide="settings" class="w-5 h-5"></i>
                <span>Edit Profile</span>
            </button>
        </div>
    </div>
    
    <div id="cooperation-modal" class="modal-overlay hidden">
        <div class="bg-white p-8 rounded-3xl w-full max-w-sm m-4 text-center transform transition-all duration-300 scale-100">
            <h2 class="text-2xl font-bold text-gray-900 mb-2">Automated Follow-Up</h2>
            <p class="text-gray-600 mb-6 text-sm">Fill in your information so Dmytro can send you a personalized follow-up email immediately.</p>

            <form id="cooperation-form" class="space-y-4 text-left">
                <input type="text" id="coop-name" name="RecipientName" placeholder="Your Full Name (e.g., Jane Doe)" required class="w-full p-3 border border-gray-300 rounded-xl focus:ring-blue-500 focus:border-blue-500">
                <input type="email" id="coop-email" name="RecipientEmail" placeholder="Your Email Address" required class="w-full p-3 border border-gray-300 rounded-xl focus:ring-blue-500 focus:border-blue-500">
                <input type="text" id="coop-company" name="CompanyName" placeholder="Your Company Name" required class="w-full p-3 border border-gray-300 rounded-xl focus:ring-blue-500 focus:border-blue-500">
                <input type="text" id="coop-place" name="PlaceMet" placeholder="Where We Met (e.g., Career Fair)" required class="w-full p-3 border border-gray-300 rounded-xl focus:ring-blue-500 focus:border-blue-500">
                
                <button type="submit" class="w-full btn-primary text-white font-bold py-3 rounded-xl shadow-md hover:shadow-lg mt-6">
                    Send My Contact Info
                </button>
            </form>
            <button type="button" onclick="closeCooperationModal()" class="mt-4 text-sm text-gray-500 hover:text-gray-700 transition duration-200">
                Cancel
            </button>
        </div>
    </div>


    <div id="resume-modal" class="modal-overlay hidden">
        <div class="bg-white p-6 rounded-3xl w-full max-w-xl m-4 h-[90vh] flex flex-col transform transition-all duration-300">
            <div class="flex justify-between items-center mb-4 pb-2 border-b">
                <h2 class="text-2xl font-bold text-gray-900">My Resume</h2>
                <button onclick="closeResumeModal()" class="text-gray-500 hover:text-gray-900 transition duration-200">
                    <i data-lucide="x" class="w-6 h-6"></i>
                </button>
            </div>
            <div id="resume-content-display" class="overflow-y-auto flex-grow pr-3">
                </div>
            
            <button onclick="closeResumeModal()" class="mt-4 w-full btn-primary text-white font-bold py-2 px-4 rounded-xl transition duration-200">
                Close
            </button>
        </div>
    </div>

    <div id="edit-modal" class="modal-overlay hidden">
        <div class="bg-white p-8 rounded-3xl w-full max-w-lg m-4 transform transition-all duration-300">
            <h2 class="text-2xl font-bold text-gray-900 mb-6">Edit Your Profile</h2>

            <form id="edit-form" class="space-y-4">
                <div>
                    <label for="edit-name" class="block text-sm font-medium text-gray-700 mb-1">Full Name</label>
                    <input type="text" id="edit-name" class="w-full p-2 border border-gray-300 rounded-xl">
                </div>
                <div>
                    <label for="edit-major" class="block text-sm font-medium text-gray-700 mb-1">Title/Major</label>
                    <input type="text" id="edit-major" class="w-full p-2 border border-gray-300 rounded-xl">
                </div>
                <div>
                    <label for="edit-bio" class="block text-sm font-medium text-gray-700 mb-1">Bio (Max 100 chars)</label>
                    <textarea id="edit-bio" maxlength="100" class="w-full p-2 border border-gray-300 rounded-xl resize-none h-20"></textarea>
                </div>
                <div>
                    <label for="edit-phone" class="block text-sm font-medium text-gray-700 mb-1">Phone Number (For Email Signature)</label>
                    <input type="tel" id="edit-phone" class="w-full p-2 border border-gray-300 rounded-xl">
                </div>


                <h3 class="text-lg font-semibold mt-6 pt-4 border-t">Social Links (Use Full URLs)</h3>

                <div class="space-y-2">
                    <label class="block text-sm font-medium text-gray-700">LinkedIn URL</label>
                    <input type="url" id="link-linkedin" placeholder="https://linkedin.com/in/..." class="w-full p-2 border border-gray-300 rounded-xl">

                    <label class="block text-sm font-medium text-gray-700">Instagram URL</label>
                    <input type="url" id="link-instagram" placeholder="https://instagram.com/..." class="w-full p-2 border border-gray-300 rounded-xl">
                    
                    <label class="block text-sm font-medium text-gray-700">Facebook URL</label>
                    <input type="url" id="link-facebook" placeholder="https://facebook.com/..." class="w-full p-2 border border-gray-300 rounded-xl">

                    <label class="block text-sm font-medium text-gray-700">Portfolio/Other URL</label>
                    <input type="url" id="link-other" placeholder="https://mywebsite.com" class="w-full p-2 border border-gray-300 rounded-xl">

                    <label for="edit-resume-content" class="block text-sm font-medium text-gray-700 pt-4">Resume Text Content (New)</label>
                    <textarea id="edit-resume-content" rows="10" placeholder="Paste your full resume text here..." class="w-full p-2 border border-gray-300 rounded-xl resize-none"></textarea>
                </div>

                <div class="flex justify-end space-x-3 pt-4">
                    <button type="button" onclick="closeEditModal()" class="bg-gray-500 hover:bg-gray-600 text-white font-bold py-2 px-4 rounded-xl transition duration-200">
                        Cancel
                    </button>
                    <button type="submit" class="bg-indigo-600 hover:bg-indigo-700 text-white font-bold py-2 px-4 rounded-xl transition duration-200">
                        Save Profile
                    </button>
                </div>
            </form>
        </div>
        
    </div>

    <div id="message-box" class="fixed top-4 right-4 p-3 rounded-xl shadow-lg text-white font-medium transition-opacity duration-300 opacity-0 z-50"></div>

    <script>
        const __app_id = 'test-app';
        const __initial_auth_token = null; 
        // This is a minimal, invalid config. It lets the script run but Firebase will fail to connect.
        const __firebase_config = JSON.stringify({
            apiKey: "AIzaSy_fake-api-key-for-local-demo-123",
            authDomain: "local-demo-app.firebaseapp.com",
            projectId: "local-demo-project"
        });
    </script>
    <script type="module">
        // --- FIREBASE IMPORTS ---
        import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";
        import { getAuth, signInAnonymously, signInWithCustomToken, onAuthStateChanged, setPersistence, browserLocalPersistence } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js";
        import { getFirestore, doc, setDoc, onSnapshot, getDoc, collection, setLogLevel } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";

        // Set log level for debugging
        setLogLevel('debug');

        // --- GLOBAL VARIABLES & CONFIGURATION ---
        const FORM_SUBMIT_URL = "https://formspree.io/f/xyznvoog"; // Generic Formspree endpoint 
        const MY_EMAIL_ADDRESS = "dimad36207@gmail.com"; // Your target email for the inquiry (Dmytro's email)

        // Canvas provided global variables (MANDATORY USE)
        const appId = typeof __app_id !== 'undefined' ? __app_id : 'default-app-id';
        const initialAuthToken = typeof __initial_auth_token !== 'undefined' ? __initial_auth_token : null;
        
        let firebaseConfig = null;
        if (typeof __firebase_config === 'string' && __firebase_config.trim() !== '') {
            try {
                firebaseConfig = JSON.parse(__firebase_config);
            } catch (e) {
                console.error("Error parsing __firebase_config (Is it valid JSON?):", e);
            }
        }

        let app;
        let db;
        let auth;
        let currentUserId = null;
        let isAuthReady = false;
        let profileData = null; // Holds the most recent data from Firestore

        // --- MOCK DATA (Includes user's resume content and a phone number) ---
        const initialMockData = {
            name: "Dmytro Denysenko",
            major: "Finance, Asper School of Business",
            bio: "Driven Finance student at the Asper School of Business with proven customer service and team leadership skills. Seeking an internship to apply analytical rigor to real-world challenges.",
            phone: "(431) 788-2320", // Added phone number for email signature
            links: {
                linkedin: "https://www.linkedin.com/in/dmytro-denysenko-61595a2a8/",
                instagram: "https://www.instagram.com/dima36207", 
                facebook: "https://www.facebook.com/dima.dima.17405",
                other: "",
            },
            // Full resume content for resume button action
            resumeContent: `DMYTRO DENYSENKO
dima36207@gmail.com | (431) 788-2320 | Winnipeg, MB

SUMMARY
Driven and analytical university student with experience in customer service and teamwork. Fluent in
English, Ukrainian, and Russian, which helps me communicate with diverse guests. Quick learner with a
positive attitude, ready to provide fast and friendly service.

SKILLS
Financial Analysis (Basic), Customer Service, Cash Handling, Teamwork (Worked well with others in fast-paced settings),
Cleanliness and Organization (Kept work areas tidy), Fluent in English, Ukrainian, and Russian,
Flexibility (Available for various shifts, including weekends and holidays).

PROFESSIONAL EXPERIENCE
STEINBACH FAMILY RESOURCE CENTER - June - August 2024
Community Resource Assistant
- Assisted guests (families, children) with a friendly and helpful attitude, demonstrating customer service skills.
- Handled food inventory and kept storage areas clean, showing attention to hygiene and organization.
- Worked as part of a team to set up events, demonstrating teamwork and reliability.

EDUCATION
UNIVERSITY OF MANITOBA - September 2024 - Present
Asper School of Business, Major: Finance
Current GPA: 3.5. Completed first year.

POWERRVIEW SCHOOL, MANITOBA
High School Diploma
Graduated with honors (90%+ average).`
        };

        // --- UTILITY FUNCTIONS ---
        function showMessage(message, type = 'success') {
            const box = document.getElementById('message-box');
            box.textContent = message;
            box.classList.remove('bg-green-500', 'bg-red-500', 'opacity-0', 'hidden');

            if (type === 'success') {
                box.classList.add('bg-green-500');
            } else if (type === 'error' || type === 'warning') {
                box.classList.add('bg-red-500');
            }

            box.classList.add('opacity-100');

            setTimeout(() => {
                box.classList.remove('opacity-100');
                box.classList.add('opacity-0');
            }, 3000);
        }

        /**
         * Converts raw resume text into formatted HTML for display in the modal.
         */
        function formatResumeContent(text) {
            if (!text) return '<p class="text-gray-500 p-4">No resume content available. Please edit your profile to add it.</p>';

            // 1. Replace all caps headings (SUMMARY, SKILLS, etc.) with styled headers
            let html = text.replace(/^(DMYTRO DENYSENKO|SUMMARY|SKILLS|PROFESSIONAL EXPERIENCE|EDUCATION|ADDITIONAL INFORMATION|UNIVERSITY OF MANITOBA|POWERRVIEW SCHOOL, MANITOBA)/gm, (match) => {
                if (match === 'DMYTRO DENYSENKO') {
                    // Special styling for the name/contact header
                    return `<div class="text-center mb-4"><h1 class="text-2xl font-extrabold text-gray-900">${match}</h1>`;
                }
                if (match.includes('SCHOOL') || match.includes('UNIVERSITY') || match.includes('CENTER')) {
                    // Education/Company titles
                    return `</div><h3 class="text-lg font-bold text-gray-800 mt-4">${match}</h3>`;
                }
                // Main Section Headers
                return `</div><h2 class="text-xl font-bold text-gray-800 mt-6 mb-2 border-b-2 border-gray-300 pb-1">${match}</h2>`;
            });
            
            // 2. Simple replacement of newline characters with <br> for basic formatting
            html = html.replace(/\n/g, '<br>');
            
            // 3. Clean up the multiple <br> tags and formatting 
            html = html.replace(/<br><br><br>/g, '<div class="h-4"></div>');
            html = html.replace(/<br><br>/g, '<br>'); 

            // 4. Handle list formatting (lines starting with -)
            html = html.replace(/- ([^<]+)/g, '<li class="list-disc ml-6">$1</li>');
            html = html.replace(/<\/li><br><ul>/g, '</li></ul>'); // Clean up broken list tags

            // 5. Wrap the text in a general class
            return `<div class="text-gray-800 text-sm leading-relaxed">${html}</div>`;
        }


        // --- UI UPDATERS ---
        function updateProfileUI(profile) {
            document.getElementById('student-name').textContent = profile.name || 'Student Name';
            document.getElementById('student-major').textContent = profile.major || 'Major/Title';
            // Use the first line of the bio for the main profile card
            const shortBio = profile.bio ? profile.bio.split('\n')[0] : 'No bio provided.';
            document.getElementById('student-bio').textContent = shortBio;
            
            // Render Social Links
            const container = document.getElementById('social-links-container');
            container.innerHTML = '';

            const iconMap = {
                linkedin: { icon: 'linkedin', color: 'bg-blue-600', label: 'LinkedIn' },
                instagram: { icon: 'instagram', color: 'bg-pink-500', label: 'Instagram' },
                facebook: { icon: 'facebook', color: 'bg-blue-700', label: 'Facebook' },
                other: { icon: 'globe', color: 'bg-gray-700', label: 'Portfolio' },
            };

            for (const key in profile.links) {
                const url = profile.links[key];
                if (url && url.trim() !== '') {
                    const map = iconMap[key];
                    const link = document.createElement('a');
                    link.href = url;
                    link.target = "_blank";
                    link.className = `flex items-center space-x-2 text-white font-semibold py-2 px-4 rounded-xl transition duration-300 hover:opacity-80 ${map.color} shadow-sm`;
                    link.innerHTML = `<i data-lucide="${map.icon}" class="w-5 h-5"></i><span>${map.label}</span>`;
                    container.appendChild(link);
                }
            }
            // Re-render lucide icons
            if (typeof lucide !== 'undefined') {
                lucide.createIcons();
            }
        }
        
        // --- MODAL HANDLERS ---
        window.closeEditModal = () => {
            document.getElementById('edit-modal').classList.add('hidden');
        };

        function openEditModal() {
            if (!profileData) return showMessage("Profile data not yet loaded.", 'warning');

            // Populate form fields with current profile data
            document.getElementById('edit-name').value = profileData.name || '';
            document.getElementById('edit-major').value = profileData.major || '';
            document.getElementById('edit-bio').value = profileData.bio || '';
            document.getElementById('edit-phone').value = profileData.phone || ''; // New field
            document.getElementById('edit-resume-content').value = profileData.resumeContent || '';

            // Populate links
            document.getElementById('link-linkedin').value = profileData.links?.linkedin || '';
            document.getElementById('link-instagram').value = profileData.links?.instagram || '';
            document.getElementById('link-facebook').value = profileData.links?.facebook || '';
            document.getElementById('link-other').value = profileData.links?.other || '';

            document.getElementById('edit-modal').classList.remove('hidden');
        }

        window.closeResumeModal = () => {
            document.getElementById('resume-modal').classList.add('hidden');
        };

        function openResumeModal(content) {
            const contentDisplay = document.getElementById('resume-content-display');
            contentDisplay.innerHTML = formatResumeContent(content);
            document.getElementById('resume-modal').classList.remove('hidden');
            // Re-render lucide icons in the modal if any were formatted in
            if (typeof lucide !== 'undefined') {
                lucide.createIcons();
            }
        }

        window.closeCooperationModal = () => {
            document.getElementById('cooperation-modal').classList.add('hidden');
        };

        function openCooperationModal() {
            document.getElementById('cooperation-modal').classList.remove('hidden');
            // Clear fields for a new inquiry
            document.getElementById('coop-name').value = '';
            document.getElementById('coop-email').value = '';
            document.getElementById('coop-company').value = '';
            document.getElementById('coop-place').value = '';
        }

        // --- FIREBASE LOGIC ---

        async function initFirebase() {
            if (!firebaseConfig) {
                console.error("Firebase config is missing. Running in Offline Demo Mode.");
                // Immediately set initial data if in Offline mode
                profileData = initialMockData;
                updateProfileUI(profileData);
                document.getElementById('user-id-display').textContent = `ID: OFFLINE`;
                document.getElementById('connection-status').textContent = 'Demo Mode';
                document.getElementById('edit-profile-btn').classList.remove('hidden'); // Allow editing mock data
                return false;
            }
            
            try {
                app = initializeApp(firebaseConfig);
                auth = getAuth(app);
                db = getFirestore(app);

                await setPersistence(auth, browserLocalPersistence);
                
                let userSignedIn = false;

                if (initialAuthToken) {
                    await signInWithCustomToken(auth, initialAuthToken);
                    userSignedIn = true;
                } else {
                    await signInAnonymously(auth);
                    userSignedIn = true;
                }
                
                if (userSignedIn) {
                    onAuthStateChanged(auth, (user) => {
                        if (user) {
                            currentUserId = user.uid;
                            isAuthReady = true;
                            document.getElementById('user-id-display').textContent = `ID: ${currentUserId.substring(0, 8)}...`;
                            document.getElementById('connection-status').textContent = 'Online';
                            document.getElementById('connection-status').classList.remove('bg-red-100', 'text-red-700');
                            document.getElementById('connection-status').classList.add('bg-green-100', 'text-green-700');
                            document.getElementById('edit-profile-btn').classList.remove('hidden');
                            
                            // Start listening for data once authenticated
                            listenForProfileData();
                        } else {
                            currentUserId = null;
                            isAuthReady = true;
                            console.log("User signed out.");
                        }
                    });
                }
                return true;

            } catch (error) {
                console.error("Firebase Initialization Error:", error);
                showMessage("Database connection failed. Check console for details.", 'error');
                
                // Fallback to offline mode on connection error
                profileData = initialMockData;
                updateProfileUI(profileData);
                document.getElementById('user-id-display').textContent = `ID: OFFLINE`;
                document.getElementById('connection-status').textContent = 'Demo Mode';
                document.getElementById('edit-profile-btn').classList.remove('hidden');
                return false;
            }
        }

        function getProfileDocRef() {
             // Firestore path: /artifacts/{appId}/users/{userId}/profiles/data
            return doc(db, 'artifacts', appId, 'users', currentUserId, 'profiles', 'data');
        }

        async function listenForProfileData() {
            if (!db || !currentUserId) return;

            const docRef = getProfileDocRef();

            // Set up real-time listener
            onSnapshot(docRef, async (docSnap) => {
                if (docSnap.exists()) {
                    // Data exists, update UI with live data
                    profileData = docSnap.data();
                    updateProfileUI(profileData);
                    showMessage("Profile loaded from cloud.", 'success');
                } else {
                    // Data does not exist, create initial data based on mock data 
                    console.log("No profile data found. Creating initial profile.");
                    await createInitialProfile(docRef);
                    // The onSnapshot listener will re-fire immediately after the write.
                }
            }, (error) => {
                console.error("Firestore listen error:", error);
                showMessage("Failed to load profile data in real-time.", 'error');
            });
        }
        
        async function createInitialProfile(docRef) {
             // Ensure all necessary fields from mock data are copied
            const initialData = {
                name: initialMockData.name,
                major: initialMockData.major,
                bio: initialMockData.bio,
                phone: initialMockData.phone, // Include phone
                links: initialMockData.links,
                resumeContent: initialMockData.resumeContent, // Include new field
            };
            try {
                // Write the full document
                await setDoc(docRef, initialData);
                
                // CRUCIAL: Immediately update profileData locally to ensure the resume content is available.
                profileData = initialData;
                updateProfileUI(profileData); 
                
                showMessage("Initial profile created successfully.", 'success');
            } catch (e) {
                console.error("Error creating initial profile:", e);
                showMessage("Failed to create initial profile.", 'error');
            }
        }

        async function saveProfile(e) {
            e.preventDefault();
            if (!isAuthReady || !currentUserId) return showMessage("Authentication is not ready.", 'warning');

            const docRef = getProfileDocRef();

            const updatedData = {
                name: document.getElementById('edit-name').value.trim(),
                major: document.getElementById('edit-major').value.trim(),
                bio: document.getElementById('edit-bio').value.trim(),
                phone: document.getElementById('edit-phone').value.trim(), // Save phone
                resumeContent: document.getElementById('edit-resume-content').value.trim(), // Save resume content
                links: {
                    linkedin: document.getElementById('link-linkedin').value.trim(),
                    instagram: document.getElementById('link-instagram').value.trim(),
                    facebook: document.getElementById('link-facebook').value.trim(),
                    other: document.getElementById('link-other').value.trim(),
                }
            };

            try {
                await setDoc(docRef, updatedData, { merge: true });
                closeEditModal();
                showMessage("Profile saved successfully!", 'success');
            } catch (error) {
                console.error("Error saving profile:", error);
                showMessage("Failed to save profile. See console.", 'error');
            }
        }
        
        // --- COOPERATION LOGIC (Automated Follow-Up) ---
        async function handleCooperationRequest(e) {
            e.preventDefault();
            
            // Recipient's details (the person who scanned the card)
            const recipientName = document.getElementById('coop-name').value.trim();
            const recipientEmail = document.getElementById('coop-email').value.trim();
            const companyName = document.getElementById('coop-company').value.trim();
            const placeMet = document.getElementById('coop-place').value.trim();
            
            // Dmytro's details (the sender of the email)
            const yourName = profileData?.name || initialMockData.name;
            const yourEmail = MY_EMAIL_ADDRESS;
            const yourPhone = profileData?.phone || initialMockData.phone;
            const yourField = profileData?.major.split(',')[0].trim() || 'Finance';
            const specificAspect = profileData?.major || 'Finance at the Asper School of Business';
            const linkedInUrl = profileData?.links?.linkedin || 'Not provided';
            
            // Constructing the email body
            const emailSubject = `Following up from ${placeMet} - ${yourName} (${yourField})`;
            const emailBody = `
Hi ${recipientName},

It was a pleasure meeting you at ${placeMet}. I really enjoyed our conversation about ${yourField} and your work at ${companyName}.

As a passionate student specializing in ${specificAspect}, I am always eager to connect with professionals in the field.

I look forward to the possibility of connecting again soon.

Best regards,

${yourName}
${yourEmail}
${yourPhone}
LinkedIn: ${linkedInUrl}
`;

            // 1. Construct the Formspree payload
            const formData = new FormData();
            formData.append('_replyto', yourEmail); // Dmytro's email will be the reply-to address
            formData.append('_subject', emailSubject); 
            formData.append('Recipient Email (TO)', recipientEmail); // Add the recruiter's email as a data point
            formData.append('Recipient Name', recipientName);
            formData.append('Company Name', companyName);
            formData.append('Where We Met', placeMet);
            formData.append('message', emailBody);

            // 2. Execute the fetch POST request to Formspree
            try {
                const response = await fetch(FORM_SUBMIT_URL, {
                    method: 'POST',
                    body: formData,
                    headers: {
                        'Accept': 'application/json'
                    }
                });

                // 3. Handle response
                if (response.ok) {
                    closeCooperationModal();
                    // The email will be sent to the address configured in Formspree for the given FORM_SUBMIT_URL.
                    showMessage(`Success! Dmytro will receive your contact information to send a follow-up email.`, 'success');
                } else {
                    const errorData = await response.json();
                    console.error("Formspree Error:", errorData);
                    showMessage('Follow-up request failed. Check your Formspree endpoint.', 'error');
                }

            } catch (error) {
                console.error('Network or Fetch Error:', error);
                showMessage('A network error occurred. Could not send request.', 'error');
            }
        }


        // --- EVENT LISTENERS ---
        document.addEventListener('DOMContentLoaded', () => {
            initFirebase();
            
            // Resume Button
            document.getElementById('view-resume-btn').addEventListener('click', () => {
                if (profileData) {
                    openResumeModal(profileData.resumeContent);
                } else {
                    showMessage("Profile data not loaded yet.", 'warning');
                }
            });

            // Cooperation Button
            document.getElementById('cooperation-btn').addEventListener('click', openCooperationModal);

            // Edit Button
            document.getElementById('edit-profile-btn').addEventListener('click', openEditModal);
            
            // Edit Form Submission
            document.getElementById('edit-form').addEventListener('submit', saveProfile);
            
            // *** FIX: Cooperation Form Submission Listener ***
            document.getElementById('cooperation-form').addEventListener('submit', handleCooperationRequest);
            
        });
    </script>
</body>
</html>
