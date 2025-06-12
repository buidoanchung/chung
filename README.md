<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>HRD.edu.vn- Hệ thống LMS học Nghề Nhân sự chuyên nghiệp</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    <script src="https://kit.fontawesome.com/a076d05399.js" crossorigin="anonymous"></script>
    <style>
        body { font-family: 'Inter', sans-serif; }
        /* Custom scrollbar for better UX */
        ::-webkit-scrollbar { width: 8px; }
        ::-webkit-scrollbar-track { background: #f1f1f1; }
        ::-webkit-scrollbar-thumb { background: #888; border-radius: 4px;}
        ::-webkit-scrollbar-thumb:hover { background: #555; }
        .tab-content { display: none; }
        .tab-content.active { display: block; }
    </style>
</head>
<body class="bg-gray-50 text-gray-800">

    <!-- Container chính -->
    <div id="app-container" class="min-h-screen">

        <!-- Màn hình đăng nhập & Đăng ký -->
        <section id="auth-section" class="flex items-center justify-center min-h-screen bg-gray-100">
            <div class="w-full max-w-md p-8 space-y-6 bg-white rounded-xl shadow-lg">
                <div class="text-center">
                    <h1 class="text-3xl font-bold text-blue-600">HR Ascent</h1>
                    <p class="text-gray-500">Lộ trình phát triển Nhân sự theo chuẩn SHRM</p>
                </div>

                <!-- Form Đăng nhập -->
                <form id="login-form" class="space-y-6">
                    <h2 class="text-xl font-semibold text-center text-gray-700">Đăng nhập</h2>
                    <div>
                        <label for="login-email" class="text-sm font-medium text-gray-700">Email</label>
                        <input id="login-email" type="email" required class="w-full px-4 py-2 mt-1 border border-gray-300 rounded-md focus:ring-blue-500 focus:border-blue-500" placeholder="your@email.com">
                    </div>
                    <div>
                        <label for="login-password" class="text-sm font-medium text-gray-700">Mật khẩu</label>
                        <input id="login-password" type="password" required class="w-full px-4 py-2 mt-1 border border-gray-300 rounded-md focus:ring-blue-500 focus:border-blue-500" placeholder="********">
                    </div>
                    <p id="login-error" class="text-sm text-red-500"></p>
                    <button type="submit" class="w-full py-2 font-semibold text-white bg-blue-600 rounded-md hover:bg-blue-700 transition duration-300">Đăng nhập</button>
                    <p class="text-sm text-center">Chưa có tài khoản? <a href="#" id="show-register" class="font-medium text-blue-600 hover:underline">Đăng ký ngay</a></p>
                </form>

                <!-- Form Đăng ký -->
                <form id="register-form" class="hidden space-y-4">
                     <h2 class="text-xl font-semibold text-center text-gray-700">Tạo tài khoản</h2>
                    <div>
                        <label for="register-name" class="text-sm font-medium text-gray-700">Họ và Tên</label>
                        <input id="register-name" type="text" required class="w-full px-4 py-2 mt-1 border border-gray-300 rounded-md focus:ring-blue-500 focus:border-blue-500" placeholder="Nguyễn Văn A">
                    </div>
                    <div>
                        <label for="register-email" class="text-sm font-medium text-gray-700">Email</label>
                        <input id="register-email" type="email" required class="w-full px-4 py-2 mt-1 border border-gray-300 rounded-md focus:ring-blue-500 focus:border-blue-500" placeholder="your@email.com">
                    </div>
                    <div>
                        <label for="register-phone" class="text-sm font-medium text-gray-700">Số điện thoại</label>
                        <input id="register-phone" type="tel" pattern="[0-9]*" required class="w-full px-4 py-2 mt-1 border border-gray-300 rounded-md focus:ring-blue-500 focus:border-blue-500" placeholder="09xxxxxxxx">
                    </div>
                    <div>
                        <label for="register-password" class="text-sm font-medium text-gray-700">Mật khẩu</p>
                        <input id="register-password" type="password" required class="w-full px-4 py-2 mt-1 border border-gray-300 rounded-md focus:ring-blue-500 focus:border-blue-500" placeholder="Tối thiểu 6 ký tự">
                    </div>
                    <p id="register-error" class="text-sm text-red-500"></p>
                    <button type="submit" class="w-full py-2 font-semibold text-white bg-green-600 rounded-md hover:bg-green-700 transition duration-300">Đăng ký</button>
                    <p class="text-sm text-center">Đã có tài khoản? <a href="#" id="show-login" class="font-medium text-blue-600 hover:underline">Đăng nhập</a></p>
                </form>
            </div>
        </section>

        <!-- Bảng điều khiển chính (Dashboard) -->
        <main id="dashboard-section" class="hidden">
            <header class="bg-white shadow-sm sticky top-0 z-40">
                <div class="container mx-auto px-4 sm:px-6 lg:px-8">
                    <div class="flex items-center justify-between h-16">
                        <div class="flex items-center">
                            <span class="text-2xl font-bold text-blue-600">HR Ascent</span>
                        </div>
                        <div class="flex items-center space-x-4">
                            <span id="user-name" class="font-semibold"></span>
                            <button id="logout-btn" class="px-4 py-2 text-sm font-medium text-white bg-red-500 rounded-md hover:bg-red-600">Đăng xuất</button>
                        </div>
                    </div>
                </div>
            </header>

            <div class="container mx-auto p-4 sm:p-6 lg:p-8">
                <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
                    <!-- Cột trái: Lộ trình và Biểu đồ -->
                    <div class="lg:col-span-1 space-y-6">
                        <div class="bg-white p-6 rounded-xl shadow-md">
                            <h2 class="text-xl font-bold mb-4">Lộ trình của bạn</h2>
                            <p class="text-gray-600">Cấp độ hiện tại:</p>
                            <p id="current-level" class="text-2xl font-bold text-blue-600"></p>
                            <p id="user-id-display" class="text-xs text-gray-400 mt-2 break-all"></p>
                        </div>
                        <div class="bg-white p-6 rounded-xl shadow-md">
                            <h2 class="text-xl font-bold mb-4">Biểu đồ Năng lực</h2>
                            <canvas id="competencyChart"></canvas>
                        </div>
                    </div>

                    <!-- Cột phải: Khóa học -->
                    <div class="lg:col-span-2 bg-white p-6 rounded-xl shadow-md">
                         <h2 class="text-xl font-bold mb-4">Các Miền Kiến thức (Knowledge Domains)</h2>
                         <div id="courses-container" class="space-y-6">
                            <!-- Nội dung khóa học sẽ được chèn vào đây bởi JS -->
                         </div>
                    </div>
                </div>
            </div>
        </main>

        <!-- Màn hình chi tiết khóa học -->
        <section id="course-section" class="hidden bg-gray-100 min-h-screen">
             <header class="bg-white shadow-sm sticky top-0 z-40">
                <div class="container mx-auto px-4 sm:px-6 lg:px-8">
                    <div class="flex items-center justify-between h-16">
                         <button id="back-to-dashboard" class="flex items-center text-blue-600 hover:text-blue-800">
                             <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-2" viewBox="0 0 20 20" fill="currentColor"><path fill-rule="evenodd" d="M12.707 5.293a1 1 0 010 1.414L9.414 10l3.293 3.293a1 1 0 01-1.414 1.414l-4-4a1 1 0 010-1.414l4-4a1 1 0 011.414 0z" clip-rule="evenodd" /></svg>
                             Quay lại Dashboard
                         </button>
                         <h1 id="course-title-header" class="text-xl font-bold text-center"></h1>
                         <div></div> <!-- Spacer -->
                    </div>
                </div>
            </header>
            <div class="container mx-auto p-4 sm:p-6 lg:p-8">
                <div class="bg-white p-8 rounded-xl shadow-lg">
                    <!-- Tabs -->
                    <div class="border-b border-gray-200 mb-6">
                        <nav class="-mb-px flex space-x-8" aria-label="Tabs">
                           <button class="tab-link whitespace-nowrap py-4 px-1 border-b-2 font-medium text-sm border-blue-500 text-blue-600" data-tab="why">Why</button>
                           <button class="tab-link whitespace-nowrap py-4 px-1 border-b-2 font-medium text-sm border-transparent text-gray-500 hover:text-gray-700 hover:border-gray-300" data-tab="what">What</button>
                           <button class="tab-link whitespace-nowrap py-4 px-1 border-b-2 font-medium text-sm border-transparent text-gray-500 hover:text-gray-700 hover:border-gray-300" data-tab="how">How to Apply</button>
                           <button class="tab-link whitespace-nowrap py-4 px-1 border-b-2 font-medium text-sm border-transparent text-gray-500 hover:text-gray-700 hover:border-gray-300" data-tab="case-study">Case Study</button>
                           <button class="tab-link whitespace-nowrap py-4 px-1 border-b-2 font-medium text-sm border-transparent text-gray-500 hover:text-gray-700 hover:border-gray-300" data-tab="knowledge-check">Knowledge Check</button>
                           <button class="tab-link whitespace-nowrap py-4 px-1 border-b-2 font-medium text-sm border-transparent text-gray-500 hover:text-gray-700 hover:border-gray-300" data-tab="next-step">Next Step</button>
                        </nav>
                    </div>

                    <!-- Tab Content -->
                    <div id="course-content-container" class="prose max-w-none">
                         <!-- Content sẽ được chèn vào đây -->
                    </div>

                </div>
            </div>
        </section>

    </div>

    <!-- Modal cho kết quả Quiz -->
    <div id="quiz-result-modal" class="hidden fixed inset-0 bg-gray-600 bg-opacity-50 overflow-y-auto h-full w-full z-50">
        <div class="relative top-20 mx-auto p-5 border w-96 shadow-lg rounded-md bg-white">
            <div class="mt-3 text-center">
                <h3 id="quiz-result-title" class="text-lg leading-6 font-medium text-gray-900"></h3>
                <div class="mt-2 px-7 py-3">
                    <p id="quiz-result-message" class="text-sm text-gray-500"></p>
                </div>
                <div class="items-center px-4 py-3">
                    <button id="close-quiz-modal-btn" class="px-4 py-2 bg-blue-500 text-white text-base font-medium rounded-md w-full shadow-sm hover:bg-blue-600 focus:outline-none focus:ring-2 focus:ring-blue-300">
                        Tuyệt vời!
                    </button>
                </div>
            </div>
        </div>
    </div>


    <script type="module">
        // Import các hàm cần thiết từ Firebase SDK
        import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";
        import { 
            getAuth, 
            createUserWithEmailAndPassword, 
            signInWithEmailAndPassword, 
            onAuthStateChanged, 
            signOut 
        } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js";
        import { 
            getFirestore, 
            doc, 
            setDoc, 
            getDoc,
            updateDoc
        } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";

        // FIX: Moved courseData object here and removed the separate import.
        const courseData = {
          Junior: {
            people: [
              {
                id: 'p-j-1',
                title: 'Viết Mô tả Công việc (JD) Hiệu quả',
                competencies: ['Communication', 'BusinessAcumen'],
                content: {
                  why: "Một JD tốt không chỉ là danh sách nhiệm vụ. Nó là công cụ marketing đầu tiên để thu hút đúng người, là cơ sở để đánh giá hiệu suất và là tài liệu pháp lý quan trọng. Một JD tệ sẽ khiến bạn lãng phí thời gian, tiền bạc và tuyển sai người.",
                  what: {
                    definition: "Mô tả công việc (Job Description) là một tài liệu văn bản mô tả các nhiệm vụ, trách nhiệm, kỹ năng yêu cầu, và điều kiện làm việc của một vị trí cụ thể trong tổ chức.",
                    framework: "Sử dụng mô hình KSAOs (Knowledge, Skills, Abilities, and Other characteristics) để xác định các yêu cầu cốt lõi. Cấu trúc JD chuẩn bao gồm: Chức danh, Tóm tắt công việc, Trách nhiệm chính, Yêu cầu (KSAOs), Điều kiện làm việc.",
                    image: "https://placehold.co/600x300/E0E7FF/4F46E5?text=Mô+hình+JD+hiệu+quả"
                  },
                  how: {
                    steps: [
                      "Bước 1: Phân tích công việc (Job Analysis) - Phỏng vấn Hiring Manager để hiểu rõ nhu cầu.",
                      "Bước 2: Sử dụng ngôn ngữ rõ ràng, bao hàm (inclusive language), tránh biệt ngữ.",
                      "Bước 3: Tập trung vào kết quả có thể đo lường, không chỉ là nhiệm vụ.",
                      "Bước 4: Kiểm tra lại các yêu cầu để đảm bảo không vi phạm luật lao động."
                    ],
                    downloadLink: "#"
                  },
                  caseStudy: {
                    scenario: "Công ty ABC đăng tuyển 'Marketing Executive' nhưng chỉ nhận được hồ sơ không phù hợp. JD của họ chỉ ghi chung chung 'làm các công việc marketing'. Bạn hãy phân tích và viết lại JD.",
                    questions: ["JD này thiếu những thông tin gì?", "Làm thế nào để JD hấp dẫn hơn với ứng viên tiềm năng?"]
                  },
                  knowledgeCheck: [
                    { question: "KSAOs là viết tắt của gì?", options: ["Kiến thức, Kỹ năng, Khả năng, Yếu tố khác", "Kiến thức, Lương, Khả năng, Tổ chức", "Kỹ năng, Kinh nghiệm, Khả năng, Mục tiêu"], answer: 0 },
                    { question: "Yếu tố nào quan trọng nhất khi viết JD?", options: ["Liệt kê càng nhiều nhiệm vụ càng tốt", "Tập trung vào kết quả mong muốn", "Sử dụng nhiều thuật ngữ chuyên ngành"], answer: 1 }
                  ],
                  nextStep: {
                    relatedLesson: "Sàng lọc hồ sơ và Lên lịch phỏng vấn",
                    externalLink: "https://www.shrm.org/resourcesandtools/tools-and-samples/how-to-guides/pages/how-to-develop-a-job-description.aspx",
                    externalLinkText: "SHRM: How to Develop a Job Description"
                  }
                }
              }
              // Thêm các khóa học khác cho Junior - People
            ],
            organization: [
              {
                id: 'o-j-1',
                title: 'Hiểu về Sơ đồ Tổ chức',
                competencies: ['BusinessAcumen', 'AnalyticalAptitude'],
                content: {
                    why: "Hiểu sơ đồ tổ chức giúp bạn biết ai báo cáo cho ai, luồng thông tin và quyền ra quyết định đi như thế nào. Điều này rất quan trọng để điều hướng công việc và giải quyết vấn đề hiệu quả.",
                    what: {
                        definition: "Sơ đồ tổ chức là một biểu đồ trực quan thể hiện cấu trúc nội bộ của một công ty bằng cách chi tiết hóa các vai trò, trách nhiệm và mối quan hệ giữa các cá nhân trong một thực thể.",
                        framework: "Các loại cấu trúc phổ biến: Cấu trúc theo chức năng (Functional), Cấu trúc theo bộ phận (Divisional), Cấu trúc ma trận (Matrix), và Cấu trúc phẳng (Flat).",
                        image: "https://placehold.co/600x300/D1FAE5/065F46?text=Các+loại+sơ+đồ+tổ+chức"
                    },
                    how: {
                        steps: [
                            "Bước 1: Xác định loại hình cấu trúc của công ty bạn.",
                            "Bước 2: Tìm hiểu các phòng ban chính và chức năng của chúng.",
                            "Bước 3: Nhận biết chuỗi mệnh lệnh (chain of command) cho vị trí của bạn.",
                            "Bước 4: Sử dụng sơ đồ để tìm đúng người cần liên hệ cho các công việc cụ thể."
                        ],
                        downloadLink: "#"
                    },
                    caseStudy: {
                        scenario: "Một nhân viên mới ở phòng Marketing muốn đề xuất một ý tưởng hợp tác với phòng Sales. Nhìn vào sơ đồ tổ chức, nhân viên đó nên liên hệ với ai đầu tiên để đảm bảo đúng quy trình?",
                        questions: ["Nhân viên có nên đi thẳng đến Giám đốc Sales không? Tại sao?", "Quy trình giao tiếp liên phòng ban hiệu quả nên như thế nào?"]
                    },
                    knowledgeCheck: [
                        { question: "Cấu trúc nào mà một nhân viên có thể có hai người quản lý?", options: ["Chức năng", "Ma trận", "Phẳng"], answer: 1 },
                        { question: "Mục đích chính của sơ đồ tổ chức là gì?", options: ["Hiển thị ảnh của nhân viên", "Làm rõ mối quan hệ báo cáo và trách nhiệm", "Quyết định mức lương"], answer: 1 }
                    ],
                    nextStep: {
                        relatedLesson: "Quy trình Onboarding cho nhân viên mới",
                        externalLink: "https://www.shrm.org/resourcesandtools/tools-and-samples/toolkits/pages/understandingorganizationalstructure.aspx",
                        externalLinkText: "SHRM: Understanding Organizational Structure"
                    }
                }
              }
            ],
            workplace: [],
            competencies: []
          },
          Middle: { /* Dữ liệu cho cấp Middle */ people:[], organization:[], workplace: [], competencies: [] },
          Senior: { /* Dữ liệu cho cấp Senior */ people:[], organization:[], workplace: [], competencies: [] },
          Executive: { /* Dữ liệu cho cấp Executive */ people:[], organization:[], workplace: [], competencies: [] }
        };
        
        // --- CẤU HÌNH FIREBASE ---
        // Sử dụng biến global __firebase_config nếu có, nếu không thì dùng config mặc định
        // Canvas sẽ tự động cung cấp biến này
        const firebaseConfig = typeof __firebase_config !== 'undefined' 
            ? JSON.parse(__firebase_config)
            : {
                apiKey: "YOUR_API_KEY", // Thay thế bằng key của bạn nếu chạy độc lập
                authDomain: "YOUR_AUTH_DOMAIN",
                projectId: "YOUR_PROJECT_ID",
                storageBucket: "YOUR_STORAGE_BUCKET",
                messagingSenderId: "YOUR_SENDER_ID",
                appId: "YOUR_APP_ID"
            };

        // Khởi tạo Firebase
        const app = initializeApp(firebaseConfig);
        const auth = getAuth(app);
        const db = getFirestore(app);

        // --- DOM Elements ---
        const authSection = document.getElementById('auth-section');
        const dashboardSection = document.getElementById('dashboard-section');
        const courseSection = document.getElementById('course-section');

        const loginForm = document.getElementById('login-form');
        const registerForm = document.getElementById('register-form');
        const showRegisterBtn = document.getElementById('show-register');
        const showLoginBtn = document.getElementById('show-login');

        const userNameDisplay = document.getElementById('user-name');
        const userIdDisplay = document.getElementById('user-id-display');
        const currentLevelDisplay = document.getElementById('current-level');
        const logoutBtn = document.getElementById('logout-btn');

        const coursesContainer = document.getElementById('courses-container');
        const backToDashboardBtn = document.getElementById('back-to-dashboard');
        const courseTitleHeader = document.getElementById('course-title-header');
        const courseContentContainer = document.getElementById('course-content-container');
        
        let competencyChart = null;
        let currentUserData = null;

        // --- CHUYỂN ĐỔI GIỮA FORM ĐĂNG NHẬP VÀ ĐĂNG KÝ ---
        showRegisterBtn.addEventListener('click', (e) => {
            e.preventDefault();
            loginForm.classList.add('hidden');
            registerForm.classList.remove('hidden');
        });

        showLoginBtn.addEventListener('click', (e) => {
            e.preventDefault();
            registerForm.classList.add('hidden');
            loginForm.classList.remove('hidden');
        });

        // --- XỬ LÝ XÁC THỰC (AUTHENTICATION) ---

        // Đăng ký
        registerForm.addEventListener('submit', async (e) => {
            e.preventDefault();
            const name = document.getElementById('register-name').value;
            const email = document.getElementById('register-email').value;
            const phone = document.getElementById('register-phone').value;
            const password = document.getElementById('register-password').value;
            const errorEl = document.getElementById('register-error');

            if (password.length < 6) {
                errorEl.textContent = "Mật khẩu phải có ít nhất 6 ký tự.";
                return;
            }
            if (!/^\d+$/.test(phone)) {
                 errorEl.textContent = "Số điện thoại chỉ được chứa chữ số.";
                 return;
            }
            errorEl.textContent = "";

            try {
                const userCredential = await createUserWithEmailAndPassword(auth, email, password);
                const user = userCredential.user;

                // Tạo document cho user mới trong Firestore
                const initialUserData = {
                    name: name,
                    email: email,
                    phone: phone,
                    currentLevel: 'Junior',
                    progress: {
                        people: { completed: [], total: courseData.Junior.people.length },
                        organization: { completed: [], total: courseData.Junior.organization.length },
                        workplace: { completed: [], total: courseData.Junior.workplace.length },
                        competencies: { completed: [], total: courseData.Junior.competencies.length },
                    },
                    competencyScores: {
                        Leadership: 5,
                        Communication: 5,
                        BusinessAcumen: 5,
                        EthicalPractice: 5,
                        RelationshipManagement: 5,
                        AnalyticalAptitude: 5
                    }
                };
                await setDoc(doc(db, "users", user.uid), initialUserData);
                // `onAuthStateChanged` sẽ xử lý việc chuyển trang
            } catch (error) {
                errorEl.textContent = mapAuthCodeToMessage(error.code);
            }
        });
        
        // Đăng nhập
        loginForm.addEventListener('submit', async (e) => {
            e.preventDefault();
            const email = document.getElementById('login-email').value;
            const password = document.getElementById('login-password').value;
            const errorEl = document.getElementById('login-error');
            errorEl.textContent = "";

            try {
                await signInWithEmailAndPassword(auth, email, password);
                // `onAuthStateChanged` sẽ xử lý việc chuyển trang
            } catch (error) {
                errorEl.textContent = mapAuthCodeToMessage(error.code);
            }
        });

        // Đăng xuất
        logoutBtn.addEventListener('click', async () => {
            await signOut(auth);
        });

        // --- TRẠNG THÁI XÁC THỰC ---
        onAuthStateChanged(auth, async (user) => {
            if (user) {
                // Người dùng đã đăng nhập
                await loadUserData(user.uid);
                showView('dashboard');
            } else {
                // Người dùng đã đăng xuất
                currentUserData = null;
                showView('auth');
            }
        });

        // --- TẢI VÀ HIỂN THỊ DỮ LIỆU ---
        async function loadUserData(uid) {
            const docRef = doc(db, "users", uid);
            const docSnap = await getDoc(docRef);

            if (docSnap.exists()) {
                currentUserData = { id: uid, ...docSnap.data() };
                renderDashboard();
            } else {
                console.log("Không tìm thấy dữ liệu người dùng!");
                // Có thể đăng xuất người dùng ở đây nếu dữ liệu không tồn tại
                signOut(auth);
            }
        }
        
        function renderDashboard() {
            if (!currentUserData) return;

            userNameDisplay.textContent = `Xin chào, ${currentUserData.name}`;
            userIdDisplay.textContent = `User ID: ${currentUserData.id}`;
            currentLevelDisplay.textContent = currentUserData.currentLevel;
            
            renderCourses();
            renderCompetencyChart();
        }

        function renderCourses() {
            coursesContainer.innerHTML = ''; // Xóa nội dung cũ
            const userLevel = currentUserData.currentLevel;
            const levelData = courseData[userLevel];
            
            for (const domainKey in levelData) {
                const domain = levelData[domainKey];
                const domainProgress = currentUserData.progress[domainKey];
                const progressPercentage = domainProgress.total > 0 ? (domainProgress.completed.length / domainProgress.total) * 100 : 0;
                
                const domainHTML = `
                    <div class="domain-card border border-gray-200 rounded-lg p-4">
                        <h3 class="text-lg font-semibold">${getDomainTitle(domainKey)}</h3>
                        <div class="w-full bg-gray-200 rounded-full h-2.5 mt-2 mb-4">
                            <div class="bg-blue-600 h-2.5 rounded-full" style="width: ${progressPercentage}%"></div>
                        </div>
                        <ul class="space-y-2">
                            ${domain.map((course, index) => {
                                const isCompleted = domainProgress.completed.includes(course.id);
                                return `
                                <li>
                                    <button data-course-id="${course.id}" data-domain-key="${domainKey}" class="w-full text-left p-3 rounded-md transition duration-200 ${isCompleted ? 'bg-green-100 text-gray-500 line-through' : 'bg-gray-100 hover:bg-blue-100'} flex justify-between items-center">
                                        <span>${course.title}</span>
                                        ${isCompleted ? '<svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-green-500" viewBox="0 0 20 20" fill="currentColor"><path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd" /></svg>' : '<svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-gray-400" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" /></svg>'}
                                    </button>
                                </li>
                                `;
                            }).join('')}
                        </ul>
                    </div>
                `;
                coursesContainer.innerHTML += domainHTML;
            }

            // Gắn event listener cho các nút khóa học
            document.querySelectorAll('[data-course-id]').forEach(button => {
                button.addEventListener('click', (e) => {
                    const courseId = e.currentTarget.dataset.courseId;
                    const domainKey = e.currentTarget.dataset.domainKey;
                    openCourse(courseId, domainKey);
                });
            });
        }
        
        function renderCompetencyChart() {
            const ctx = document.getElementById('competencyChart').getContext('2d');
            const scores = currentUserData.competencyScores;
            const labels = Object.keys(scores);
            const data = Object.values(scores);
            
            const benchmarkData = {
                Junior: 25, Middle: 50, Senior: 75, Executive: 90
            };
            const benchmarkValue = benchmarkData[currentUserData.currentLevel];

            if (competencyChart) {
                competencyChart.destroy();
            }

            competencyChart = new Chart(ctx, {
                type: 'radar',
                data: {
                    labels: labels.map(l => l.replace(/([A-Z])/g, ' $1').trim()), // Add space before uppercase letters
                    datasets: [{
                        label: 'Năng lực của bạn',
                        data: data,
                        backgroundColor: 'rgba(54, 162, 235, 0.2)',
                        borderColor: 'rgba(54, 162, 235, 1)',
                        borderWidth: 2
                    }, {
                        label: `Chuẩn ${currentUserData.currentLevel}`,
                        data: Array(labels.length).fill(benchmarkValue),
                        backgroundColor: 'rgba(255, 99, 132, 0.2)',
                        borderColor: 'rgba(255, 99, 132, 1)',
                        borderWidth: 1,
                        pointRadius: 0
                    }]
                },
                options: {
                    scales: {
                        r: {
                            angleLines: { display: true },
                            suggestedMin: 0,
                            suggestedMax: 100,
                            pointLabels: {
                                font: { size: 10 }
                            }
                        }
                    },
                    plugins: {
                        legend: { position: 'top' }
                    }
                }
            });
        }
        
        function openCourse(courseId, domainKey) {
            const course = courseData[currentUserData.currentLevel][domainKey].find(c => c.id === courseId);
            if (!course) return;

            courseTitleHeader.textContent = course.title;
            // Lưu id khóa học hiện tại để dùng khi hoàn thành
            courseContentContainer.dataset.currentCourseId = course.id;
            courseContentContainer.dataset.currentDomainKey = domainKey;

            // Kích hoạt tab đầu tiên và hiển thị nội dung
            showTabContent(course, 'why');

            // Xử lý chuyển tab
            document.querySelectorAll('.tab-link').forEach(tabLink => {
                tabLink.addEventListener('click', () => {
                    document.querySelectorAll('.tab-link').forEach(link => {
                        link.classList.remove('border-blue-500', 'text-blue-600');
                        link.classList.add('border-transparent', 'text-gray-500', 'hover:text-gray-700', 'hover:border-gray-300');
                    });
                    tabLink.classList.add('border-blue-500', 'text-blue-600');
                    tabLink.classList.remove('border-transparent', 'text-gray-500', 'hover:text-gray-700', 'hover:border-gray-300');
                    
                    showTabContent(course, tabLink.dataset.tab);
                });
            });

            showView('course');
        }

        function showTabContent(course, tabName) {
            let contentHTML = '';
            switch(tabName) {
                case 'why':
                    contentHTML = `<h2>Tại sao điều này lại quan trọng?</h2><p>${course.content.why}</p>`;
                    break;
                case 'what':
                    contentHTML = `<h2>What (Định nghĩa & Mô hình)</h2>
                        <p><strong>Định nghĩa:</strong> ${course.content.what.definition}</p>
                        <p><strong>Framework/Mô hình:</strong> ${course.content.what.framework}</p>
                        <img src="${course.content.what.image}" alt="Mô hình minh họa" class="mx-auto my-4 rounded-lg shadow-md max-w-full h-auto"/>
                    `;
                    break;
                case 'how':
                    contentHTML = `<h2>How to Apply (Cách áp dụng)</h2>
                        <ul>${course.content.how.steps.map(step => `<li>${step}</li>`).join('')}</ul>
                        <a href="${course.content.how.downloadLink}" target="_blank" class="inline-block mt-4 px-4 py-2 bg-blue-500 text-white rounded-md no-underline hover:bg-blue-600">Tải về Template</a>
                    `;
                    break;
                case 'case-study':
                    contentHTML = `<h2>Case Study (Tình huống Phân tích)</h2>
                        <div class="bg-yellow-50 border-l-4 border-yellow-400 p-4 my-4">
                            <p><strong>Tình huống:</strong> ${course.content.caseStudy.scenario}</p>
                        </div>
                        <p><strong>Câu hỏi phân tích:</p>
                        <ol>${course.content.caseStudy.questions.map(q => `<li>${q}</li>`).join('')}</ol>
                    `;
                    break;
                case 'knowledge-check':
                    contentHTML = `<h2>Kiểm tra kiến thức</h2>
                        <p>Chọn câu trả lời đúng nhất để củng cố kiến thức đã học.</p>
                        <form id="quiz-form">
                            ${course.content.knowledgeCheck.map((q, index) => `
                                <div class="my-4">
                                    <p class="font-semibold">${index + 1}. ${q.question}</p>
                                    ${q.options.map((opt, i) => `
                                        <div class="flex items-center my-2">
                                            <input type="radio" id="q${index}_opt${i}" name="q${index}" value="${i}" class="mr-2">
                                            <label for="q${index}_opt${i}">${opt}</label>
                                        </div>
                                    `).join('')}
                                </div>
                            `).join('')}
                            <button type="submit" class="mt-4 px-6 py-2 bg-green-600 text-white rounded-md hover:bg-green-700">Nộp bài</button>
                        </form>
                    `;
                    // Gắn listener cho quiz form sau khi render
                    setTimeout(() => {
                        const quizForm = document.getElementById('quiz-form');
                        if (quizForm) {
                            quizForm.addEventListener('submit', (e) => handleQuizSubmit(e, course));
                        }
                    }, 0);
                    break;
                case 'next-step':
                    contentHTML = `<h2>Next Step (Bước tiếp theo)</h2>
                        <p><strong>Bài học liên quan:</strong> ${course.content.nextStep.relatedLesson}</p>
                        <p><strong>Đọc thêm:</strong> <a href="${course.content.nextStep.externalLink}" target="_blank" class="text-blue-600 hover:underline">${course.content.nextStep.externalLinkText}</a></p>
                    `;
                    break;
            }
            courseContentContainer.innerHTML = contentHTML;
        }

        async function handleQuizSubmit(e, course) {
            e.preventDefault();
            const formData = new FormData(e.target);
            let score = 0;
            course.content.knowledgeCheck.forEach((q, index) => {
                const userAnswer = formData.get(`q${index}`);
                if (userAnswer && parseInt(userAnswer) === q.answer) {
                    score++;
                }
            });

            const totalQuestions = course.content.knowledgeCheck.length;
            const resultTitle = `Kết quả: ${score}/${totalQuestions}`;
            const resultMessage = score > totalQuestions / 2 
                ? "Chúc mừng! Bạn đã nắm vững kiến thức bài học."
                : "Hãy ôn lại bài một chút nhé!";

            // Hiển thị modal kết quả
            document.getElementById('quiz-result-title').textContent = resultTitle;
            document.getElementById('quiz-result-message').textContent = resultMessage;
            document.getElementById('quiz-result-modal').classList.remove('hidden');

            // Cập nhật tiến độ nếu trả lời đúng > 50%
            if (score > totalQuestions / 2) {
                await completeCourse(course.id, course.competencies);
            }
        }
        
        document.getElementById('close-quiz-modal-btn').addEventListener('click', () => {
             document.getElementById('quiz-result-modal').classList.add('hidden');
        });
        
        async function completeCourse(courseId, competenciesToUpdate) {
            const domainKey = courseContentContainer.dataset.currentDomainKey;
            
            // Tránh cập nhật trùng lặp
            if (currentUserData.progress[domainKey].completed.includes(courseId)) {
                console.log("Khóa học đã hoàn thành trước đó.");
                return;
            }

            // Cập nhật progress
            const newCompleted = [...currentUserData.progress[domainKey].completed, courseId];
            const progressUpdate = {
                [`progress.${domainKey}.completed`]: newCompleted
            };

            // Cập nhật competency scores
            const newScores = { ...currentUserData.competencyScores };
            competenciesToUpdate.forEach(comp => {
                if (newScores[comp] !== undefined) {
                    newScores[comp] = Math.min(100, newScores[comp] + 5); // Cộng 5 điểm, tối đa 100
                }
            });
            const scoresUpdate = {
                competencyScores: newScores
            };

            // Ghi vào Firestore
            const userDocRef = doc(db, "users", currentUserData.id);
            await updateDoc(userDocRef, { ...progressUpdate, ...scoresUpdate });

            // Cập nhật dữ liệu local và render lại dashboard
            currentUserData.progress[domainKey].completed = newCompleted;
            currentUserData.competencyScores = newScores;
            renderDashboard();
        }

        // --- QUẢN LÝ GIAO DIỆN (VIEW) ---
        function showView(viewName) {
            authSection.classList.add('hidden');
            dashboardSection.classList.add('hidden');
            courseSection.classList.add('hidden');

            if (viewName === 'auth') {
                authSection.classList.remove('hidden');
            } else if (viewName === 'dashboard') {
                dashboardSection.classList.remove('hidden');
            } else if (viewName === 'course') {
                courseSection.classList.remove('hidden');
            }
        }
        
        backToDashboardBtn.addEventListener('click', () => showView('dashboard'));

        // --- HÀM HỖ TRỢ ---
        function getDomainTitle(key) {
            const titles = {
                people: 'PEOPLE (Con người)',
                organization: 'ORGANIZATION (Tổ chức)',
                workplace: 'WORKPLACE (Môi trường làm việc)',
                competencies: 'COMPETENCIES (Năng lực Hành vi)'
            };
            return titles[key] || key;
        }

        function mapAuthCodeToMessage(code) {
            switch (code) {
                case 'auth/wrong-password':
                    return 'Mật khẩu không đúng. Vui lòng thử lại.';
                case 'auth/user-not-found':
                    return 'Không tìm thấy tài khoản với email này.';
                case 'auth/email-already-in-use':
                    return 'Email này đã được sử dụng. Vui lòng chọn email khác.';
                case 'auth/weak-password':
                    return 'Mật khẩu quá yếu. Vui lòng chọn mật khẩu khác an toàn hơn.';
                default:
                    return 'Đã có lỗi xảy ra. Vui lòng thử lại.';
            }
        }

    </script>
    
</body>
</html>
