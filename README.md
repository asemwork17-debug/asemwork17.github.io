<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>موقعي المدمج</title>
    
    <!-- Favicon -->
    <link rel="icon" href="data:image/svg+xml,<svg xmlns=%22http://www.w3.org/2000/svg%22 viewBox=%220 0 100 100%22><text y=%22.9em%22 font-size=%2290%22>🚀</text></svg>">
    
    <!-- Font Awesome -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <style>
        /* Reset */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body, html {
            width: 100%;
            height: 100%;
            overflow: hidden;
            font-family: 'Segoe UI', 'Tahoma', 'Geneva', 'Verdana', sans-serif;
            background: #f5f5f5;
        }
        
        /* Header */
        .header {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 15px 20px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
            position: relative;
            z-index: 100;
        }
        
        .logo {
            display: flex;
            align-items: center;
            gap: 10px;
            font-size: 20px;
            font-weight: bold;
        }
        
        .logo i {
            font-size: 24px;
        }
        
        /* Controls */
        .controls {
            display: flex;
            gap: 10px;
        }
        
        .btn {
            background: rgba(255, 255, 255, 0.2);
            color: white;
            border: none;
            padding: 8px 15px;
            border-radius: 20px;
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: 8px;
            font-size: 14px;
            transition: all 0.3s;
        }
        
        .btn:hover {
            background: rgba(255, 255, 255, 0.3);
            transform: translateY(-2px);
        }
        
        /* Main Container */
        .container {
            width: 100vw;
            height: calc(100vh - 60px);
            position: relative;
            display: flex;
        }
        
        /* Sidebar */
        .sidebar {
            width: 250px;
            background: white;
            padding: 20px;
            box-shadow: 2px 0 10px rgba(0,0,0,0.1);
            display: flex;
            flex-direction: column;
            gap: 20px;
            transition: transform 0.3s;
        }
        
        .sidebar.hidden {
            transform: translateX(-100%);
        }
        
        .sidebar-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 10px;
        }
        
        .sidebar h3 {
            color: #333;
            font-size: 16px;
            margin-bottom: 10px;
        }
        
        .sidebar-info {
            background: #f8f9fa;
            padding: 15px;
            border-radius: 8px;
            border-right: 4px solid #667eea;
        }
        
        .sidebar-info p {
            color: #555;
            font-size: 14px;
            margin-bottom: 8px;
        }
        
        .info-label {
            font-weight: bold;
            color: #333;
        }
        
        /* Iframe Container */
        .iframe-container {
            flex: 1;
            position: relative;
            background: white;
        }
        
        #app-frame {
            width: 100%;
            height: 100%;
            border: none;
            display: block;
        }
        
        /* Loading Screen */
        .loader {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            display: flex;
            justify-content: center;
            align-items: center;
            flex-direction: column;
            z-index: 1000;
            transition: opacity 0.5s ease, visibility 0.5s;
        }
        
        .loader.hidden {
            opacity: 0;
            visibility: hidden;
        }
        
        .spinner {
            width: 60px;
            height: 60px;
            border: 5px solid rgba(255, 255, 255, 0.3);
            border-radius: 50%;
            border-top-color: white;
            animation: spin 1s ease-in-out infinite;
            margin-bottom: 20px;
        }
        
        @keyframes spin {
            to { transform: rotate(360deg); }
        }
        
        .loader-text {
            color: white;
            font-size: 18px;
            text-align: center;
            margin-bottom: 10px;
        }
        
        .loader-subtext {
            color: rgba(255, 255, 255, 0.8);
            font-size: 14px;
            text-align: center;
        }
        
        /* Error Message */
        .error-message {
            display: none;
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: white;
            padding: 40px;
            border-radius: 15px;
            box-shadow: 0 15px 40px rgba(0,0,0,0.15);
            text-align: center;
            z-index: 1001;
            max-width: 500px;
            width: 90%;
        }
        
        .error-message.show {
            display: block;
            animation: fadeIn 0.3s ease;
        }
        
        @keyframes fadeIn {
            from { opacity: 0; transform: translate(-50%, -40%); }
            to { opacity: 1; transform: translate(-50%, -50%); }
        }
        
        .error-icon {
            font-size: 50px;
            color: #ff4757;
            margin-bottom: 20px;
        }
        
        .error-message h3 {
            color: #333;
            margin-bottom: 15px;
            font-size: 20px;
        }
        
        .error-message p {
            color: #666;
            margin-bottom: 25px;
            line-height: 1.6;
        }
        
        .btn-group {
            display: flex;
            gap: 10px;
            justify-content: center;
            flex-wrap: wrap;
        }
        
        .btn-primary {
            background: #667eea;
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
            display: flex;
            align-items: center;
            gap: 8px;
            transition: background 0.3s;
        }
        
        .btn-primary:hover {
            background: #5a67d8;
        }
        
        .btn-secondary {
            background: #f1f2f6;
            color: #333;
            border: none;
            padding: 10px 20px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
            display: flex;
            align-items: center;
            gap: 8px;
            transition: background 0.3s;
        }
        
        .btn-secondary:hover {
            background: #e2e3e9;
        }
        
        /* Stats Bar */
        .stats-bar {
            position: absolute;
            bottom: 20px;
            right: 20px;
            background: rgba(0, 0, 0, 0.8);
            color: white;
            padding: 10px 15px;
            border-radius: 8px;
            font-size: 12px;
            display: flex;
            gap: 15px;
            z-index: 100;
        }
        
        .stat {
            display: flex;
            align-items: center;
            gap: 5px;
        }
        
        .stat i {
            color: #667eea;
        }
        
        /* Mobile Responsive */
        @media (max-width: 768px) {
            .sidebar {
                position: absolute;
                height: calc(100vh - 60px);
                z-index: 101;
            }
            
            .header {
                padding: 12px 15px;
            }
            
            .logo span {
                display: none;
            }
            
            .btn span {
                display: none;
            }
            
            .btn {
                padding: 10px;
                border-radius: 50%;
                width: 40px;
                height: 40px;
                justify-content: center;
            }
            
            .error-message {
                padding: 25px;
            }
            
            .btn-group {
                flex-direction: column;
            }
            
            .stats-bar {
                bottom: 10px;
                right: 10px;
                font-size: 10px;
                padding: 8px 10px;
                gap: 10px;
            }
        }
        
        /* Fullscreen Mode */
        body.fullscreen .header,
        body.fullscreen .sidebar,
        body.fullscreen .stats-bar {
            display: none;
        }
        
        body.fullscreen .container {
            height: 100vh;
        }
        
        /* Dark Mode */
        @media (prefers-color-scheme: dark) {
            body:not(.fullscreen) {
                background: #1a1a1a;
            }
            
            .sidebar {
                background: #2d2d2d;
                color: #fff;
            }
            
            .sidebar h3 {
                color: #fff;
            }
            
            .sidebar-info {
                background: #3d3d3d;
                color: #ccc;
            }
            
            .info-label {
                color: #fff;
            }
            
            .iframe-container {
                background: #1a1a1a;
            }
            
            .btn-secondary {
                background: #3d3d3d;
                color: #fff;
            }
            
            .btn-secondary:hover {
                background: #4d4d4d;
            }
        }
    </style>
</head>
<body>
    <!-- Header -->
    <header class="header">
        <div class="logo">
            <i class="fas fa-globe"></i>
            <span>موقعي المدمج</span>
        </div>
        
        <div class="controls">
            <button class="btn" id="toggleSidebar" title="إظهار/إخفاء القائمة">
                <i class="fas fa-bars"></i>
                <span>القائمة</span>
            </button>
            <button class="btn" id="reloadBtn" title="إعادة تحميل">
                <i class="fas fa-redo"></i>
                <span>إعادة تحميل</span>
            </button>
            <button class="btn" id="fullscreenBtn" title="ملء الشاشة">
                <i class="fas fa-expand"></i>
                <span>ملء الشاشة</span>
            </button>
        </div>
    </header>

    <!-- Main Container -->
    <div class="container">
        <!-- Sidebar -->
        <div class="sidebar" id="sidebar">
            <div class="sidebar-header">
                <h3><i class="fas fa-info-circle"></i> معلومات الموقع</h3>
                <button class="btn" id="closeSidebar" title="إغلاق">
                    <i class="fas fa-times"></i>
                </button>
            </div>
            
            <div class="sidebar-info">
                <p><span class="info-label">الحالة:</span> <span id="statusText">جاري التحميل...</span></p>
                <p><span class="info-label">آخر تحديث:</span> <span id="lastUpdate">--</span></p>
                <p><span class="info-label">وقت التحميل:</span> <span id="loadTime">--</span></p>
            </div>
            
            <div>
                <h3><i class="fas fa-cog"></i> الإعدادات</h3>
                <div style="display: flex; flex-direction: column; gap: 10px;">
                    <label style="display: flex; align-items: center; gap: 10px; cursor: pointer;">
                        <input type="checkbox" id="autoRefresh" checked>
                        <span>التحديث التلقائي</span>
                    </label>
                    
                    <div>
                        <label style="display: block; margin-bottom: 5px; font-size: 14px;">جودة العرض:</label>
                        <select id="qualitySelect" style="width: 100%; padding: 8px; border-radius: 5px; border: 1px solid #ddd;">
                            <option value="auto">تلقائي</option>
                            <option value="high">عالية</option>
                            <option value="medium">متوسطة</option>
                            <option value="low">منخفضة</option>
                        </select>
                    </div>
                </div>
            </div>
            
            <div>
                <h3><i class="fas fa-share-alt"></i> مشاركة</h3>
                <div style="display: flex; gap: 10px;">
                    <button class="btn-secondary" style="flex: 1;" onclick="copyLink()">
                        <i class="fas fa-link"></i> نسخ الرابط
                    </button>
                    <button class="btn-secondary" style="flex: 1;" onclick="sharePage()">
                        <i class="fas fa-share"></i> مشاركة
                    </button>
                </div>
            </div>
        </div>

        <!-- Iframe Container -->
        <div class="iframe-container">
            <!-- Loading Screen -->
            <div class="loader" id="loader">
                <div class="spinner"></div>
                <div class="loader-text">جاري تحميل المحتوى...</div>
                <div class="loader-subtext">قد تستغرق العملية بضع ثواني</div>
            </div>
            
            <!-- Error Message -->
            <div class="error-message" id="errorMessage">
                <div class="error-icon">
                    <i class="fas fa-exclamation-triangle"></i>
                </div>
                <h3>تعذر تحميل المحتوى</h3>
                <p>حدث خطأ أثناء محاولة تحميل المحتوى. يرجى التحقق من اتصالك بالإنترنت والمحاولة مرة أخرى.</p>
                <div class="btn-group">
                    <button class="btn-primary" onclick="retryLoading()">
                        <i class="fas fa-redo"></i> إعادة المحاولة
                    </button>
                    <button class="btn-secondary" onclick="showDetails()">
                        <i class="fas fa-info-circle"></i> تفاصيل التقنية
                    </button>
                </div>
            </div>
            
            <!-- Iframe -->
            <iframe 
                id="app-frame"
                src="https://script.google.com/macros/s/AKfycbxc_kFLk1LBUrU-KiFNZJ9Tx2IztzPnpc8YFO0BZ2VqDs45-04jvA4zIg4PdzkRdN2A/exec"
                title="التطبيق المدمج"
                allow="fullscreen"
                allowfullscreen
            ></iframe>
        </div>
    </div>

    <!-- Stats Bar -->
    <div class="stats-bar" id="statsBar">
        <div class="stat">
            <i class="fas fa-clock"></i>
            <span id="pageTime">--</span>
        </div>
        <div class="stat">
            <i class="fas fa-sync-alt"></i>
            <span id="refreshCount">0</span>
        </div>
        <div class="stat">
            <i class="fas fa-wifi"></i>
            <span id="connectionStatus">متصل</span>
        </div>
    </div>

    <script>
        // عناصر DOM
        const loader = document.getElementById('loader');
        const errorMessage = document.getElementById('errorMessage');
        const appFrame = document.getElementById('app-frame');
        const sidebar = document.getElementById('sidebar');
        const statsBar = document.getElementById('statsBar');
        
        // المتغيرات
        let isLoading = true;
        let loadStartTime = Date.now();
        let refreshCount = 0;
        let autoRefreshInterval;
        let connectionStatus = 'online';
        
        // تهيئة الصفحة
        function init() {
            updateStats();
            startLoadTimer();
            setupEventListeners();
            checkConnection();
            setupAutoRefresh();
            
            // تحديث الوقت كل ثانية
            setInterval(updateStats, 1000);
            
            // مراقبة اتصال الشبكة
            window.addEventListener('online', () => {
                connectionStatus = 'online';
                updateStats();
                if (isLoading) retryLoading();
            });
            
            window.addEventListener('offline', () => {
                connectionStatus = 'offline';
                updateStats();
                showError('انقطع اتصال الإنترنت');
            });
            
            // تهيئة الوقت
            updateLastUpdate();
        }
        
        // إعداد المستمعين للأحداث
        function setupEventListeners() {
            // أزرار التحكم
            document.getElementById('toggleSidebar').addEventListener('click', toggleSidebar);
            document.getElementById('closeSidebar').addEventListener('click', toggleSidebar);
            document.getElementById('reloadBtn').addEventListener('click', reloadFrame);
            document.getElementById('fullscreenBtn').addEventListener('click', toggleFullscreen);
            
            // إطار التحميل
            appFrame.addEventListener('load', handleLoadComplete);
            appFrame.addEventListener('error', handleLoadError);
            
            // لوحة المفاتيح
            document.addEventListener('keydown', handleKeyPress);
            
            // تحديث تلقائي
            document.getElementById('autoRefresh').addEventListener('change', setupAutoRefresh);
            document.getElementById('qualitySelect').addEventListener('change', handleQualityChange);
            
            // سحب لتحديث على الجوال
            let touchStartY = 0;
            document.addEventListener('touchstart', e => {
                touchStartY = e.touches[0].clientY;
            });
            
            document.addEventListener('touchmove', e => {
                if (touchStartY - e.touches[0].clientY > 100) {
                    reloadFrame();
                }
            });
        }
        
        // تبديل القائمة الجانبية
        function toggleSidebar() {
            sidebar.classList.toggle('hidden');
        }
        
        // إعادة تحميل الإطار
        function reloadFrame() {
            refreshCount++;
            updateStats();
            
            isLoading = true;
            loader.classList.remove('hidden');
            errorMessage.classList.remove('show');
            
            // إضافة timestamp لمنع التخزين المؤقت
            const timestamp = new Date().getTime();
            const currentSrc = appFrame.src.split('?')[0];
            appFrame.src = `${currentSrc}?t=${timestamp}`;
            
            startLoadTimer();
        }
        
        // تبديل وضع ملء الشاشة
        function toggleFullscreen() {
            if (!document.fullscreenElement) {
                document.documentElement.requestFullscreen().then(() => {
                    document.body.classList.add('fullscreen');
                });
            } else {
                document.exitFullscreen().then(() => {
                    document.body.classList.remove('fullscreen');
                });
            }
        }
        
        // التعامل مع اكتمال التحميل
        function handleLoadComplete() {
            isLoading = false;
            const loadTime = Date.now() - loadStartTime;
            
            setTimeout(() => {
                loader.classList.add('hidden');
                document.getElementById('statusText').textContent = 'محمّل';
                document.getElementById('loadTime').textContent = `${loadTime} مللي ثانية`;
                updateLastUpdate();
            }, 500);
        }
        
        // التعامل مع خطأ التحميل
        function handleLoadError() {
            isLoading = false;
            loader.classList.add('hidden');
            errorMessage.classList.add('show');
            document.getElementById('statusText').textContent = 'خطأ في التحميل';
        }
        
        // إعادة المحاولة
        function retryLoading() {
            errorMessage.classList.remove('show');
            loadStartTime = Date.now();
            reloadFrame();
        }
        
        // بدء مؤقت التحميل
        function startLoadTimer() {
            loadStartTime = Date.now();
            
            setTimeout(() => {
                if (isLoading) {
                    showError('استغرقت عملية التحميل وقتاً طويلاً');
                }
            }, 15000); // 15 ثانية
        }
        
        // عرض رسالة خطأ
        function showError(message) {
            isLoading = false;
            loader.classList.add('hidden');
            errorMessage.classList.add('show');
            document.getElementById('statusText').textContent = 'خطأ';
            
            if (message) {
                errorMessage.querySelector('p').textContent = message;
            }
        }
        
        // تحديث الإحصائيات
        function updateStats() {
            const pageTime = Math.floor((Date.now() - loadStartTime) / 1000);
            document.getElementById('pageTime').textContent = `${pageTime} ث`;
            document.getElementById('refreshCount').textContent = refreshCount;
            document.getElementById('connectionStatus').textContent = 
                connectionStatus === 'online' ? 'متصل' : 'غير متصل';
        }
        
        // تحديث وقت آخر تحديث
        function updateLastUpdate() {
            const now = new Date();
            const timeString = now.toLocaleTimeString('ar-SA');
            const dateString = now.toLocaleDateString('ar-SA');
            document.getElementById('lastUpdate').textContent = `${dateString} ${timeString}`;
        }
        
        // إعداد التحديث التلقائي
        function setupAutoRefresh() {
            const autoRefresh = document.getElementById('autoRefresh').checked;
            
            if (autoRefreshInterval) {
                clearInterval(autoRefreshInterval);
            }
            
            if (autoRefresh) {
                autoRefreshInterval = setInterval(() => {
                    if (!isLoading && connectionStatus === 'online') {
                        reloadFrame();
                    }
                }, 300000); // 5 دقائق
            }
        }
        
        // التعامل مع تغيير الجودة
        function handleQualityChange() {
            const quality = document.getElementById('qualitySelect').value;
            // يمكن إضافة منطق لتغيير جودة المحتوى هنا
            console.log('جودة العرض تغيرت إلى:', quality);
        }
        
        // التحقق من الاتصال
        function checkConnection() {
            connectionStatus = navigator.onLine ? 'online' : 'offline';
            updateStats();
        }
        
        // نسخ الرابط
        function copyLink() {
            navigator.clipboard.writeText(window.location.href).then(() => {
                alert('تم نسخ الرابط إلى الحافظة!');
            });
        }
        
        // مشاركة الصفحة
        function sharePage() {
            if (navigator.share) {
                navigator.share({
                    title: 'موقعي المدمج',
                    text: 'تفقد هذا الموقع المدمج',
                    url: window.location.href,
                });
            } else {
                copyLink();
            }
        }
        
        // عرض التفاصيل التقنية
        function showDetails() {
            const details = `
                <h3>معلومات تقنية:</h3>
                <p>نظام التشغيل: ${navigator.platform}</p>
                <p>المتصفح: ${navigator.userAgent.split(') ')[0].split('(')[1]}</p>
                <p>الدقة: ${window.screen.width} × ${window.screen.height}</p>
                <p>الذاكرة: ${navigator.deviceMemory || 'غير معروف'} GB</p>
                <p>الاتصال: ${connectionStatus}</p>
            `;
            alert(details);
        }
        
        // التعامل مع ضغطات المفاتيح
        function handleKeyPress(e) {
            switch(e.key) {
                case 'F5':
                case 'r':
                    if (e.ctrlKey) {
                        e.preventDefault();
                        reloadFrame();
                    }
                    break;
                case 'F11':
                    e.preventDefault();
                    toggleFullscreen();
                    break;
                case 'Escape':
                    if (document.fullscreenElement) {
                        document.exitFullscreen();
                        document.body.classList.remove('fullscreen');
                    }
                    break;
                case 'm':
                    if (e.ctrlKey) {
                        e.preventDefault();
                        toggleSidebar();
                    }
                    break;
            }
        }
        
        // بدء التشغيل عند تحميل الصفحة
        window.addEventListener('DOMContentLoaded', init);
        
        // إخفاء التحميل بعد وقت كحد أقصى
        setTimeout(() => {
            if (isLoading) {
                handleLoadError();
            }
        }, 20000);
    </script>
</body>
</html>
