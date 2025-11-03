<!DOCTYPE html>
<html lang="bn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>মন ভালো - বাংলাদেশের জন্য মানসিক স্বাস্থ্য সহায়তা</title>
    <link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" />
    <style>
        /* Base styles */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Kalpurush', 'SolaimanLipi', Arial, sans-serif;
        }
        
        body {
            background-color: #f5f9fc;
            color: #333;
            line-height: 1.6;
        }
        
        /* Header styles */
        header {
            background-color: #006a4e;
            color: white;
            padding: 15px 20px;
            position: sticky;
            top: 0;
            z-index: 100;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }
        
        .header-container {
            display: flex;
            justify-content: space-between;
            align-items: center;
            max-width: 1200px;
            margin: 0 auto;
        }
        
        .logo {
            font-size: 1.5rem;
            font-weight: bold;
        }
        
        .logo span {
            color: #ffcc00;
        }
        
        nav ul {
            display: flex;
            list-style: none;
        }
        
        nav li {
            margin-left: 20px;
        }
        
        nav a {
            color: white;
            text-decoration: none;
            font-size: 1rem;
            padding: 8px 12px;
            border-radius: 4px;
            transition: background-color 0.3s;
        }
        
        nav a:hover {
            background-color: rgba(255, 255, 255, 0.2);
        }
        
        .mobile-menu-btn {
            display: none;
            background: none;
            border: none;
            color: white;
            font-size: 1.5rem;
            cursor: pointer;
        }
        
        /* Main content styles */
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }
        
        .hero {
            background: linear-gradient(rgba(0, 106, 78, 0.8), rgba(0, 106, 78, 0.6)), url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" width="100" height="100" viewBox="0 0 100 100"><rect width="100" height="100" fill="%23006a4e"/></svg>');
            background-size: cover;
            color: white;
            text-align: center;
            padding: 60px 20px;
            border-radius: 8px;
            margin-bottom: 30px;
        }
        
        .hero h1 {
            font-size: 2rem;
            margin-bottom: 15px;
        }
        
        .hero p {
            font-size: 1.2rem;
            max-width: 800px;
            margin: 0 auto 25px;
        }
        
        .btn {
            display: inline-block;
            background-color: #ffcc00;
            color: #006a4e;
            padding: 12px 24px;
            border-radius: 30px;
            text-decoration: none;
            font-weight: bold;
            font-size: 1rem;
            transition: all 0.3s;
            border: none;
            cursor: pointer;
            min-height: 44px;
            min-width: 120px;
        }
        
        .btn:hover {
            background-color: #e6b800;
            transform: translateY(-2px);
        }
        
        .btn-secondary {
            background-color: #e0e0e0;
            color: #333;
        }
        
        .btn-secondary:hover {
            background-color: #d0d0d0;
        }
        
        .section {
            background-color: white;
            border-radius: 8px;
            padding: 25px;
            margin-bottom: 25px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.05);
        }
        
        .section h2 {
            color: #006a4e;
            margin-bottom: 15px;
            font-size: 1.5rem;
        }
        
        .features {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 20px;
            margin-top: 20px;
        }
        
        .feature-card {
            background-color: #f0f7f4;
            border-radius: 8px;
            padding: 20px;
            text-align: center;
            transition: transform 0.3s;
        }
        
        .feature-card:hover {
            transform: translateY(-5px);
        }
        
        .feature-icon {
            font-size: 2.5rem;
            color: #006a4e;
            margin-bottom: 15px;
        }
        
        .feature-card h3 {
            margin-bottom: 10px;
            color: #006a4e;
        }
        
        /* Filter section */
        .filter-section {
            background-color: #e8f4f0;
            padding: 15px;
            border-radius: 8px;
            margin-bottom: 20px;
        }
        
        .filter-row {
            display: flex;
            flex-wrap: wrap;
            gap: 15px;
            align-items: center;
        }
        
        .filter-group {
            flex: 1;
            min-width: 200px;
        }
        
        .filter-group label {
            display: block;
            margin-bottom: 5px;
            font-weight: bold;
            color: #006a4e;
        }
        
        select, input, textarea {
            width: 100%;
            padding: 12px;
            border: 1px solid #ccc;
            border-radius: 4px;
            font-size: 1rem;
            min-height: 44px;
        }
        
        textarea {
            min-height: 120px;
            resize: vertical;
        }
        
        /* Resources grid */
        .resources-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
            gap: 20px;
            margin-top: 20px;
        }
        
        .resource-card {
            border: 1px solid #e0e0e0;
            border-radius: 8px;
            overflow: hidden;
            transition: box-shadow 0.3s;
        }
        
        .resource-card:hover {
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }
        
        .resource-header {
            background-color: #006a4e;
            color: white;
            padding: 15px;
        }
        
        .resource-body {
            padding: 15px;
        }
        
        .resource-type {
            display: inline-block;
            background-color: #ffcc00;
            color: #006a4e;
            padding: 4px 8px;
            border-radius: 4px;
            font-size: 0.8rem;
            font-weight: bold;
            margin-bottom: 10px;
        }
        
        /* Crisis contacts */
        .crisis-contacts {
            background-color: #fff9e6;
            border-left: 4px solid #ffcc00;
            padding: 15px;
            margin-top: 20px;
        }
        
        .crisis-contacts h3 {
            color: #b8860b;
            margin-bottom: 10px;
        }
        
        .contact-list {
            list-style: none;
        }
        
        .contact-list li {
            margin-bottom: 8px;
            display: flex;
            align-items: center;
        }
        
        .contact-list li:before {
            content: "•";
            color: #006a4e;
            font-weight: bold;
            margin-right: 10px;
        }
        
        /* Footer */
        footer {
            background-color: #004d38;
            color: white;
            padding: 30px 20px;
            margin-top: 40px;
        }
        
        .footer-container {
            max-width: 1200px;
            margin: 0 auto;
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 30px;
        }
        
        .footer-section h3 {
            margin-bottom: 15px;
            color: #ffcc00;
        }
        
        .footer-links {
            list-style: none;
        }
        
        .footer-links li {
            margin-bottom: 8px;
        }
        
        .footer-links a {
            color: #ccc;
            text-decoration: none;
            transition: color 0.3s;
        }
        
        .footer-links a:hover {
            color: white;
        }
        
        .copyright {
            text-align: center;
            margin-top: 30px;
            padding-top: 20px;
            border-top: 1px solid rgba(255,255,255,0.1);
            color: #ccc;
            font-size: 0.9rem;
        }
        
        /* Responsive styles */
        @media (max-width: 768px) {
            .header-container {
                flex-direction: column;
                align-items: flex-start;
            }
            
            nav {
                width: 100%;
                margin-top: 15px;
                display: none;
            }
            
            nav.active {
                display: block;
            }
            
            nav ul {
                flex-direction: column;
            }
            
            nav li {
                margin: 5px 0;
            }
            
            .mobile-menu-btn {
                display: block;
                position: absolute;
                right: 20px;
                top: 15px;
            }
            
            .hero h1 {
                font-size: 1.7rem;
            }
            
            .hero p {
                font-size: 1rem;
            }
            
            .filter-row {
                flex-direction: column;
            }
            
            .filter-group {
                width: 100%;
            }
        }
        
        /* Offline indicator */
        .offline-indicator {
            position: fixed;
            bottom: 20px;
            right: 20px;
            background-color: #ff6b6b;
            color: white;
            padding: 10px 15px;
            border-radius: 4px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.2);
            display: none;
            z-index: 1000;
        }
        
        .offline-indicator.active {
            display: block;
        }
        
        /* Mood tracker */
        .mood-tracker {
            background-color: #f0f7f4;
            border-radius: 8px;
            padding: 20px;
            margin-top: 20px;
        }
        
        .mood-options {
            display: flex;
            justify-content: space-between;
            margin: 20px 0;
            flex-wrap: wrap;
            gap: 10px;
        }
        
        .mood-option {
            flex: 1;
            min-width: 60px;
            text-align: center;
            cursor: pointer;
            padding: 10px;
            border-radius: 8px;
            transition: all 0.3s;
        }
        
        .mood-option:hover {
            background-color: rgba(0, 106, 78, 0.1);
        }
        
        .mood-option.selected {
            background-color: #006a4e;
            color: white;
        }
        
        .mood-emoji {
            font-size: 2rem;
            margin-bottom: 5px;
        }
        
        /* Privacy notice */
        .privacy-notice {
            background-color: #e6f7ff;
            border-left: 4px solid #1890ff;
            padding: 15px;
            margin: 20px 0;
            border-radius: 4px;
            font-size: 0.9rem;
        }
        
        /* Check-in history */
        .checkin-history {
            margin-top: 20px;
        }
        
        .history-chart {
            height: 200px;
            background-color: #f9f9f9;
            border-radius: 8px;
            margin-top: 15px;
            padding: 15px;
            display: flex;
            align-items: flex-end;
            justify-content: space-around;
        }
        
        .chart-bar {
            width: 30px;
            background-color: #006a4e;
            border-radius: 4px 4px 0 0;
            position: relative;
        }
        
        .chart-bar-label {
            position: absolute;
            bottom: -25px;
            left: 0;
            right: 0;
            text-align: center;
            font-size: 0.8rem;
        }
        
        /* Map container */
        .map-container {
            height: 400px;
            border-radius: 8px;
            overflow: hidden;
            margin-top: 20px;
            border: 1px solid #e0e0e0;
        }
        
        /* Welcome back message */
        .welcome-back {
            background-color: #e6f7ff;
            border-left: 4px solid #1890ff;
            padding: 15px;
            margin: 20px 0;
            border-radius: 4px;
        }
        
        /* Satirical elements */
        .satire-box {
            background-color: #fff9e6;
            border: 1px dashed #ffcc00;
            border-radius: 8px;
            padding: 15px;
            margin: 20px 0;
            font-style: italic;
        }
        
        .hablu-quote {
            background-color: #f0f7f4;
            border-left: 4px solid #006a4e;
            padding: 15px;
            margin: 15px 0;
        }
        
        .hablu-quote:before {
            content: '"';
            font-size: 2rem;
            color: #006a4e;
            margin-right: 5px;
        }
        
        /* Anonymous help form */
        .help-form {
            background-color: #f9f9f9;
            border-radius: 8px;
            padding: 20px;
            margin-top: 20px;
        }
        
        .form-group {
            margin-bottom: 20px;
        }
        
        .form-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: bold;
            color: #006a4e;
        }
        
        .checkbox-group {
            display: flex;
            align-items: flex-start;
            margin-bottom: 15px;
        }
        
        .checkbox-group input {
            width: auto;
            margin-right: 10px;
            margin-top: 5px;
        }
        
        .checkbox-group label {
            font-weight: normal;
            margin-bottom: 0;
        }
        
        .security-notice {
            background-color: #e8f4f0;
            border-left: 4px solid #006a4e;
            padding: 15px;
            margin: 20px 0;
            border-radius: 4px;
        }
        
        /* Seasonal tips */
        .seasonal-tips {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
            gap: 20px;
            margin-top: 20px;
        }
        
        .season-card {
            border: 1px solid #e0e0e0;
            border-radius: 8px;
            overflow: hidden;
            transition: transform 0.3s;
        }
        
        .season-card:hover {
            transform: translateY(-5px);
        }
        
        .season-header {
            padding: 15px;
            color: white;
            text-align: center;
        }
        
        .monsoon { background-color: #2980b9; }
        .winter { background-color: #3498db; }
        .summer { background-color: #e67e22; }
        .year-round { background-color: #27ae60; }
        
        .season-body {
            padding: 15px;
        }
        
        .season-body ul {
            padding-left: 20px;
        }
        
        .season-body li {
            margin-bottom: 8px;
        }
        
        /* Modal */
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0,0,0,0.5);
            z-index: 2000;
            align-items: center;
            justify-content: center;
        }
        
        .modal-content {
            background-color: white;
            border-radius: 8px;
            padding: 30px;
            max-width: 500px;
            width: 90%;
            text-align: center;
        }
        
        .modal h3 {
            color: #006a4e;
            margin-bottom: 15px;
        }
        
        .close-modal {
            position: absolute;
            top: 15px;
            right: 15px;
            background: none;
            border: none;
            font-size: 1.5rem;
            cursor: pointer;
            color: #666;
        }
        
        /* Queued requests */
        .queued-requests {
            background-color: #fff9e6;
            border-radius: 8px;
            padding: 15px;
            margin-top: 20px;
        }
        
        .request-item {
            background-color: white;
            border-radius: 4px;
            padding: 10px;
            margin-bottom: 10px;
            border-left: 4px solid #ffcc00;
        }
        
        /* Login Form */
        .login-form {
            max-width: 400px;
            margin: 50px auto;
            background-color: white;
            border-radius: 8px;
            padding: 30px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }
        
        .login-form h2 {
            text-align: center;
            margin-bottom: 20px;
            color: #006a4e;
        }
        
        .form-footer {
            text-align: center;
            margin-top: 20px;
        }
        
        .form-footer a {
            color: #006a4e;
            text-decoration: none;
        }
        
        /* Dashboard */
        .dashboard {
            display: none;
        }
        
        .dashboard-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }
        
        .dashboard-stats {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
            margin-bottom: 30px;
        }
        
        .stat-card {
            background-color: #f0f7f4;
            border-radius: 8px;
            padding: 20px;
            text-align: center;
        }
        
        .stat-value {
            font-size: 2rem;
            font-weight: bold;
            color: #006a4e;
            margin-bottom: 5px;
        }
        
        .stat-label {
            color: #666;
        }
        
        .updates-section {
            margin-top: 30px;
        }
        
        .update-form {
            background-color: #f9f9f9;
            border-radius: 8px;
            padding: 20px;
            margin-bottom: 20px;
        }
        
        .updates-list {
            display: grid;
            gap: 15px;
        }
        
        .update-item {
            background-color: white;
            border-radius: 8px;
            padding: 15px;
            border-left: 4px solid #006a4e;
            box-shadow: 0 2px 5px rgba(0,0,0,0.05);
        }
        
        .update-header {
            display: flex;
            justify-content: space-between;
            margin-bottom: 10px;
        }
        
        .update-author {
            font-weight: bold;
            color: #006a4e;
        }
        
        .update-date {
            color: #666;
            font-size: 0.9rem;
        }
        
        .update-content {
            line-height: 1.5;
        }
        
        /* User menu */
        .user-menu {
            position: relative;
        }
        
        .user-btn {
            background: none;
            border: none;
            color: white;
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: 8px;
        }
        
        .user-dropdown {
            position: absolute;
            top: 100%;
            right: 0;
            background-color: white;
            border-radius: 4px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
            padding: 10px 0;
            min-width: 150px;
            display: none;
        }
        
        .user-dropdown.active {
            display: block;
        }
        
        .user-dropdown a {
            display: block;
            padding: 8px 15px;
            color: #333;
            text-decoration: none;
        }
        
        .user-dropdown a:hover {
            background-color: #f5f5f5;
        }
        
        /* Maternal & Child Health Tracker */
        .tracker-tabs {
            display: flex;
            margin-bottom: 20px;
            border-bottom: 1px solid #e0e0e0;
        }
        
        .tracker-tab {
            padding: 10px 20px;
            cursor: pointer;
            border-bottom: 3px solid transparent;
        }
        
        .tracker-tab.active {
            border-bottom-color: #006a4e;
            color: #006a4e;
            font-weight: bold;
        }
        
        .tracker-content {
            display: none;
        }
        
        .tracker-content.active {
            display: block;
        }
        
        .schedule-list {
            margin-top: 20px;
        }
        
        .schedule-item {
            background-color: #f9f9f9;
            border-radius: 8px;
            padding: 15px;
            margin-bottom: 10px;
            border-left: 4px solid #006a4e;
        }
        
        .schedule-item.completed {
            border-left-color: #27ae60;
            background-color: #e8f5e8;
        }
        
        .schedule-item.overdue {
            border-left-color: #e74c3c;
            background-color: #fde8e6;
        }
        
        .schedule-header {
            display: flex;
            justify-content: space-between;
            margin-bottom: 5px;
        }
        
        .schedule-title {
            font-weight: bold;
        }
        
        .schedule-date {
            color: #666;
        }
        
        .schedule-status {
            display: inline-block;
            padding: 3px 8px;
            border-radius: 4px;
            font-size: 0.8rem;
            font-weight: bold;
        }
        
        .status-upcoming {
            background-color: #fff9e6;
            color: #b8860b;
        }
        
        .status-completed {
            background-color: #e8f5e8;
            color: #27ae60;
        }
        
        .status-overdue {
            background-color: #fde8e6;
            color: #e74c3c;
        }
        
        /* Symptom Awareness Guide */
        .symptom-categories {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
            gap: 15px;
            margin-top: 20px;
        }
        
        .symptom-category {
            background-color: #f0f7f4;
            border-radius: 8px;
            padding: 15px;
            cursor: pointer;
            transition: all 0.3s;
        }
        
        .symptom-category:hover {
            background-color: #e0f0e8;
            transform: translateY(-2px);
        }
        
        .symptom-category h4 {
            color: #006a4e;
            margin-bottom: 8px;
        }
        
        .symptom-details {
            display: none;
            margin-top: 20px;
            padding: 20px;
            background-color: #f9f9f9;
            border-radius: 8px;
        }
        
        .symptom-details.active {
            display: block;
        }
        
        .danger-signs {
            background-color: #fff9e6;
            border-left: 4px solid #ffcc00;
            padding: 15px;
            margin: 15px 0;
        }
        
        .danger-signs h4 {
            color: #b8860b;
            margin-bottom: 10px;
        }
        
        .action-steps {
            background-color: #e6f7ff;
            border-left: 4px solid #1890ff;
            padding: 15px;
            margin: 15px 0;
        }
        
        .action-steps h4 {
            color: #1890ff;
            margin-bottom: 10px;
        }
        
        .home-care {
            background-color: #e8f5e8;
            border-left: 4px solid #27ae60;
            padding: 15px;
            margin: 15px 0;
        }
        
        .home-care h4 {
            color: #27ae60;
            margin-bottom: 10px;
        }
        
        .warning-box {
            background-color: #fde8e6;
            border-left: 4px solid #e74c3c;
            padding: 15px;
            margin: 15px 0;
        }
        
        .warning-box h4 {
            color: #e74c3c;
            margin-bottom: 10px;
        }
    </style>
</head>
<body>
    <!-- Offline indicator -->
    <div class="offline-indicator" id="offlineIndicator">
        আপনি অফলাইনে আছেন। কিছু বৈশিষ্ট্য সীমিত হতে পারে।
    </div>
    
    <!-- Header -->
    <header>
        <div class="header-container">
            <div class="logo">মন <span>ভালো</span></div>
            <button class="mobile-menu-btn" id="mobileMenuBtn">☰</button>
            <nav id="mainNav">
                <ul>
                    <li><a href="#home">হোম</a></li>
                    <li><a href="#checkin">মেজাজ চেক-ইন</a></li>
                    <li><a href="#help">গোপন সহায়তা</a></li>
                    <li><a href="#seasonal">মৌসুমী স্বাস্থ্য</a></li>
                    <li><a href="#maternal">মা ও শিশু</a></li>
                    <li><a href="#symptoms">লক্ষণ গাইড</a></li>
                    <li><a href="#map">স্বাস্থ্য মানচিত্র</a></li>
                    <li><a href="#support">জরুরি যোগাযোগ</a></li>
                    <li id="dashboardLink" style="display: none;"><a href="#dashboard">ড্যাশবোর্ড</a></li>
                    <li id="userMenu" class="user-menu" style="display: none;">
                        <button class="user-btn" id="userBtn">
                            <span id="userName">ব্যবহারকারী</span> ▼
                        </button>
                        <div class="user-dropdown" id="userDropdown">
                            <a href="#dashboard">ড্যাশবোর্ড</a>
                            <a href="#" id="logoutBtn">লগ আউট</a>
                        </div>
                    </li>
                    <li id="loginLink"><a href="#login">লগ ইন</a></li>
                </ul>
            </nav>
        </div>
    </header>
    
    <!-- Login Form -->
    <div class="container" id="loginSection">
        <div class="login-form">
            <h2>মন ভালো তে লগ ইন করুন</h2>
            <div class="form-group">
                <label for="loginEmail">ইমেইল বা ফোন নম্বর</label>
                <input type="text" id="loginEmail" placeholder="আপনার ইমেইল বা ফোন নম্বর">
            </div>
            <div class="form-group">
                <label for="loginPassword">পাসওয়ার্ড</label>
                <input type="password" id="loginPassword" placeholder="আপনার পাসওয়ার্ড">
            </div>
            <button class="btn" id="loginBtn">লগ ইন</button>
            <div class="form-footer">
                <p>অ্যাকাউন্ট নেই? <a href="#" id="showRegister">এখানে রেজিস্টার করুন</a></p>
            </div>
        </div>
        
        <!-- Register Form -->
        <div class="login-form" id="registerForm" style="display: none;">
            <h2>নতুন অ্যাকাউন্ট তৈরি করুন</h2>
            <div class="form-group">
                <label for="registerName">পুরো নাম</label>
                <input type="text" id="registerName" placeholder="আপনার পুরো নাম">
            </div>
            <div class="form-group">
                <label for="registerEmail">ইমেইল</label>
                <input type="email" id="registerEmail" placeholder="আপনার ইমেইল ঠিকানা">
            </div>
            <div class="form-group">
                <label for="registerPhone">ফোন নম্বর</label>
                <input type="tel" id="registerPhone" placeholder="আপনার ফোন নম্বর">
            </div>
            <div class="form-group">
                <label for="registerPassword">পাসওয়ার্ড</label>
                <input type="password" id="registerPassword" placeholder="পাসওয়ার্ড তৈরি করুন">
            </div>
            <div class="form-group">
                <label for="registerConfirmPassword">পাসওয়ার্ড নিশ্চিত করুন</label>
                <input type="password" id="registerConfirmPassword" placeholder="পাসওয়ার্ড আবার লিখুন">
            </div>
            <button class="btn" id="registerBtn">রেজিস্টার করুন</button>
            <div class="form-footer">
                <p>ইতিমধ্যে অ্যাকাউন্ট আছে? <a href="#" id="showLogin">লগ ইন করুন</a></p>
            </div>
        </div>
    </div>
    
    <!-- Main content (shown after login) -->
    <div class="container" id="mainContent" style="display: none;">
        <!-- Hero section -->
        <section class="hero" id="home">
            <h1>আপনার মানসিক সুস্থতা আমাদের অগ্রাধিকার</h1>
            <p>বাংলাদেশের প্রতিটি মানুষের জন্য সহজলভ্য ও সাশ্রয়ী মানসিক স্বাস্থ্য সহায়তা</p>
            <a href="#help" class="btn">গোপনে সাহায্য নিন</a>
        </section>
        
        <!-- Satirical box -->
        <div class="satire-box">
            <p><strong>বাস্তবতা:</strong> ২২০ জন মনোরোগ বিশেষজ্ঞ ১৭ কোটি মানুষের জন্য। আমরা ২৪ ঘন্টার হ্যাকাথনে এই সমস্যার সমাধান করতে পারব? সম্ভবত না, তবে অন্তত আমরা চেষ্টা করছি!</p>
        </div>
        
        <!-- Features section -->
        <section class="section">
            <h2>আমাদের বৈশিষ্ট্য</h2>
            <div class="features">
                <div class="feature-card">
                    <div class="feature-icon">📱</div>
                    <h3>মোবাইল-ফার্স্ট</h3>
                    <p>সব ধরনের মোবাইল ডিভাইসে ব্যবহারের জন্য উপযোগী ডিজাইন</p>
                </div>
                <div class="feature-card">
                    <div class="feature-icon">🌐</div>
                    <h3>অফলাইন সমর্থন</h3>
                    <p>ইন্টারনেট ছাড়াই মূল বৈশিষ্ট্যগুলো ব্যবহার করুন</p>
                </div>
                <div class="feature-card">
                    <div class="feature-icon">🔒</div>
                    <h3>গোপনীয়তা সুরক্ষিত</h3>
                    <p>আপনার তথ্য নিরাপদে সংরক্ষণ করা হয়</p>
                </div>
                <div class="feature-card">
                    <div class="feature-icon">🗣️</div>
                    <h3>বাংলা ভাষায়</h3>
                    <p>সহজ ও স্পষ্ট বাংলা ভাষায় সমস্ত কন্টেন্ট</p>
                </div>
            </div>
        </section>
        
        <!-- Mental Health Check-In -->
        <section class="section" id="checkin">
            <h2>আপনার আজকের মেজাজ কেমন?</h2>
            <p>আপনার অনুভূতি ট্র্যাক করুন এবং ব্যক্তিগতকৃত সহায়তা পান</p>
            
            <!-- Welcome back message (shown after 3 days offline) -->
            <div class="welcome-back" id="welcomeBack" style="display: none;">
                <h3>আবারও স্বাগতম!</h3>
                <p>আমরা দেখতে পাচ্ছি আপনি কয়েকদিন পর ফিরেছেন। আমরা জানি জীবন কখনো কখনো ব্যস্ত হয়ে যায়। আপনি যখন প্রস্তুত, আপনার মেজাজ শেয়ার করতে পারেন। কোন চাপ নেই!</p>
            </div>
            
            <div class="hablu-quote">
                "যখন আমি পরীক্ষার আগে ৩টায় প্যানিক অ্যাটাক নিয়ে জেগে থাকতাম, কেউ জিজ্ঞাসা করেনি 'ভাই, কেমন আছ?' এখন আমি অন্যদের জন্য সেই নিরাপদ জায়গাটা বানাতে চাই।"
            </div>
            
            <div class="mood-tracker">
                <h3>আপনি আজ কেমন বোধ করছেন?</h3>
                <p>সঠিক শব্দ খুঁজে পাচ্ছেন না? বাংলাদেশে মানুষ সাধারণত বলে:</p>
                <ul>
                    <li>"মন খারাপ" (মনের অবস্থা ভাল না)</li>
                    <li>"বেশি চিন্তা হচ্ছে" (অতিরিক্ত দুশ্চিন্তা)</li>
                    <li>"কোনো কিছু ভাল লাগছে না" (হতাশার অনুভূতি)</li>
                </ul>
                
                <div class="mood-options">
                    <div class="mood-option" data-mood="very-happy">
                        <div class="mood-emoji">😄</div>
                        <div>খুব ভালো</div>
                    </div>
                    <div class="mood-option" data-mood="happy">
                        <div class="mood-emoji">😊</div>
                        <div>ভালো</div>
                    </div>
                    <div class="mood-option" data-mood="neutral">
                        <div class="mood-emoji">😐</div>
                        <div>মোটামুটি</div>
                    </div>
                    <div class="mood-option" data-mood="sad">
                        <div class="mood-emoji">😔</div>
                        <div>মন খারাপ</div>
                    </div>
                    <div class="mood-option" data-mood="very-sad">
                        <div class="mood-emoji">😢</div>
                        <div>খুব খারাপ</div>
                    </div>
                </div>
                
                <button class="btn" id="saveMoodBtn">আমার মেজাজ সংরক্ষণ করুন</button>
                
                <div class="checkin-history" id="checkinHistory">
                    <h3>আপনার মেজাজের ইতিহাস</h3>
                    <p>আপনার গত ৭ দিনের মেজাজের পরিবর্তন:</p>
                    <div class="history-chart" id="moodChart">
                        <!-- Chart will be populated by JavaScript -->
                    </div>
                </div>
                
                <div class="privacy-notice">
                    <strong>গোপনীয়তা নোট:</strong> আপনার মেজাজের তথ্য শুধুমাত্র আপনার ডিভাইসে সংরক্ষণ করা হয় এবং অন্য কারো সাথে শেয়ার করা হয় না।
                </div>
            </div>
        </section>
        
        <!-- Anonymous Help Request -->
        <section class="section" id="help">
            <h2>গোপনে সাহায্য চান</h2>
            
            <div class="hablu-quote">
                "যদি আমি সাহায্য চাই, তাহলে কি সন্ধ্যার মধ্যে পুরো গ্রাম জেনে যাবে? বাংলাদেশে, বিশেষ করে গ্রামীণ এলাকায়, মানসিক স্বাস্থ্য নিয়ে কুসংস্কার রয়েছে। সাহায্য চাওয়ার অর্থ হতে পারে গল্প, বিচার, বা আরও খারাপ - 'পাগল' বলে লেবেল লাগানো।"
            </div>
            
            <div class="security-notice">
                <h3>💡 আপনার গোপনীয়তা সুরক্ষিত</h3>
                <p>আমরা আপনার কোন ব্যক্তিগত তথ্য (নাম, ফোন নম্বর, ঠিকানা) সংগ্রহ করি না। আপনার অনুরোধ শুধুমাত্র নির্বাচিত স্বাস্থ্যকর্মীদের কাছে পৌঁছাবে যারা গোপনীয়তা রক্ষার শপথ নিয়েছেন।</p>
            </div>
            
            <div class="help-form">
                <div class="form-group">
                    <label for="issueType">আপনি কোন ধরনের সমস্যা নিয়ে কথা বলতে চান?</label>
                    <select id="issueType">
                        <option value="">একটি নির্বাচন করুন</option>
                        <option value="stress">অতিরিক্ত চাপ/টেনশন</option>
                        <option value="sadness">দীর্ঘদিন ধরে মন খারাপ</option>
                        <option value="family">পারিবারিক সমস্যা</option>
                        <option value="relationship">সম্পর্ক সংক্রান্ত সমস্যা</option>
                        <option value="work">কাজ/পড়াশোনার চাপ</option>
                        <option value="other">অন্যান্য</option>
                    </select>
                </div>
                
                <div class="form-group">
                    <label for="helpDescription">আপনার সমস্যা সম্পর্কে সংক্ষেপে লিখুন (ঐচ্ছিক):</label>
                    <textarea id="helpDescription" placeholder="আপনি যা বলতে চান, তা এখানে লিখুন..."></textarea>
                </div>
                
                <div class="form-group">
                    <label for="preferredContact">আপনি কিভাবে যোগাযোগ পছন্দ করবেন?</label>
                    <select id="preferredContact">
                        <option value="anonymous">গোপনে বার্তার মাধ্যমে (কোন ফোন নম্বর দরকার নেই)</option>
                        <option value="phone">ফোন কলের মাধ্যমে (আপনার নম্বর শেয়ার করতে হবে)</option>
                        <option value="in-person">ব্যক্তিগতভাবে দেখা করার মাধ্যমে</option>
                    </select>
                </div>
                
                <div class="checkbox-group">
                    <input type="checkbox" id="consentCheck" required>
                    <label for="consentCheck">আমি বুঝতে পেরেছি যে আমার অনুরোধ স্থানীয় এনজিও বা কমিউনিটি স্বাস্থ্যকর্মীর কাছে পাঠানো হবে এবং তারা ৪৮ ঘন্টার মধ্যে আমার সাথে যোগাযোগ করবেন। আমি আমার যোগাযোগের তথ্য পরে শেয়ার করতে পারি যদি আমি চাই।</label>
                </div>
                
                <div class="checkbox-group">
                    <input type="checkbox" id="privacyCheck" required>
                    <label for="privacyCheck">আমি বুঝতে পেরেছি যে আমার কোন ব্যক্তিগত তথ্য সংগ্রহ করা হবে না এবং আমার অনুরোধ সম্পূর্ণ গোপন রাখা হবে।</label>
                </div>
                
                <button class="btn" id="submitHelpRequest">সাহায্যের অনুরোধ পাঠান</button>
                
                <div class="queued-requests" id="queuedRequests" style="display: none;">
                    <h3>অফলাইন অনুরোধ</h3>
                    <p>আপনার অনুরোধগুলি সংরক্ষণ করা হয়েছে এবং ইন্টারনেট সংযোগ পাওয়া মাত্রই পাঠানো হবে:</p>
                    <div id="requestList">
                        <!-- Queued requests will appear here -->
                    </div>
                </div>
            </div>
        </section>
        
        <!-- Seasonal Health Tips -->
        <section class="section" id="seasonal">
            <h2>মৌসুমী স্বাস্থ্য পরামর্শ</h2>
            
            <div class="hablu-quote">
                "আমি ডেঙ্গু মৌসুমের কথা মনে করি: সবাই হঠাৎ করে এডিস মশা সম্পর্কে বিশেষজ্ঞ হয়ে যায়। আমার খালা ৪৭টি হোয়াটসঅ্যাপ বার্তা ফরওয়ার্ড করেছিলেন নিম পাতার বিষয়ে (কিছু সত্য, বেশিরভাগই ভুয়া তথ্য)।"
            </div>
            
            <div class="seasonal-tips">
                <div class="season-card">
                    <div class="season-header monsoon">
                        <h3>বর্ষা মৌসুম (জুন-সেপ্টেম্বর)</h3>
                    </div>
                    <div class="season-body">
                        <h4>ডেঙ্গু প্রতিরোধ</h4>
                        <ul>
                            <li>জমে থাকা পানি পরিষ্কার করুন (বালতি, ফুলের টব, টায়ার)</li>
                            <li>মশারি ব্যবহার করুন</li>
                            <li>ফুল হাতা জামা পরুন</li>
                            <li>জ্বর হলে প্রচুর পানি পান করুন এবং ডাক্তার দেখান</li>
                        </ul>
                    </div>
                </div>
                
                <div class="season-card">
                    <div class="season-header winter">
                        <h3>শীত মৌসুম (ডিসেম্বর-ফেব্রুয়ারি)</h3>
                    </div>
                    <div class="season-body">
                        <h4>সর্দি-কাশি ও নিউমোনিয়া</h4>
                        <ul>
                            <li>গরম পানি পান করুন</li>
                            <li>গরম কাপড় পরুন</li>
                            <li>শিশুদের নিউমোনিয়ার লক্ষণ দেখুন: দ্রুত শ্বাস, জ্বর</li>
                            <li>ভিটামিন সি সমৃদ্ধ খাবার খান</li>
                        </ul>
                    </div>
                </div>
                
                <div class="season-card">
                    <div class="season-header summer">
                        <h3>গ্রীষ্ম মৌসুম (মার্চ-মে)</h3>
                    </div>
                    <div class="season-body">
                        <h4>ডায়রিয়া ও হিট স্ট্রোক</h4>
                        <ul>
                            <li>নিরাপদ পানি পান করুন (১০ মিনিট ফুটিয়ে নিন)</li>
                            <li>ওরাল স্যালাইন তৈরি করুন</li>
                            <li>সূর্যের তাপ এড়িয়ে চলুন</li>
                            <li>হালকা রঙের ঢিলেঢালা পোশাক পরুন</li>
                        </ul>
                    </div>
                </div>
                
                <div class="season-card">
                    <div class="season-header year-round">
                        <h3>সারা বছর</h3>
                    </div>
                    <div class="season-body">
                        <h4>সাধারণ স্বাস্থ্যবিধি</h4>
                        <ul>
                            <li>নিয়মিত হাত ধোয়া (সাবান দিয়ে ২০ সেকেন্ড)</li>
                            <li>খাবার আগে ফলমূল ধুয়ে নিন</li>
                            <li>বাসি খাবার এড়িয়ে চলুন</li>
                            <li>নিয়মিত স্বাস্থ্য পরীক্ষা করুন</li>
                        </ul>
                    </div>
                </div>
            </div>
        </section>
        
        <!-- Maternal & Child Health Tracker -->
        <section class="section" id="maternal">
            <h2>মা ও শিশু স্বাস্থ্য ট্র্যাকার</h2>
            
            <div class="hablu-quote">
                "আমার বোনের প্রথম সন্তান হয়েছে গত বছর। তিনি দুটি প্রসবপূর্ব চেকআপ মিস করেছিলেন কারণ তারিখগুলো ভুলে গিয়েছিলেন, এবং কমিউনিটি ক্লিনিক রিমাইন্ডার পাঠায় না। বাচ্চা হওয়ার পর, টিকা ট্র্যাক করা হারিয়ে যাওয়া কাগজের কার্ডের জটিলতায় পরিণত হয়েছিল।"
            </div>
            
            <div class="privacy-notice">
                <strong>গোপনীয়তা নোট:</strong> এই তথ্য শুধুমাত্র আপনার ডিভাইসে সংরক্ষণ করা হয় এবং আপনি স্পষ্টভাবে শেয়ার করতে না চাইলে অন্য কারো সাথে শেয়ার করা হয় না।
            </div>
            
            <div class="tracker-tabs">
                <div class="tracker-tab active" data-tab="pregnancy">গর্ভাবস্থা ট্র্যাকার</div>
                <div class="tracker-tab" data-tab="child">শিশু টিকা ট্র্যাকার</div>
            </div>
            
            <!-- Pregnancy Tracker -->
            <div class="tracker-content active" id="pregnancy-tracker">
                <h3>গর্ভাবস্থা ট্র্যাকার</h3>
                <p>আপনার গর্ভাবস্থার তারিখ লিখুন এবং প্রসবপূর্ব চেকআপের রিমাইন্ডার পান</p>
                
                <div class="form-group">
                    <label for="lastPeriodDate">আপনার শেষ মাসিকের প্রথম দিন</label>
                    <input type="date" id="lastPeriodDate">
                </div>
                
                <div class="form-group">
                    <label for="expectedDelivery">প্রত্যাশিত প্রসব তারিখ (ঐচ্ছিক)</label>
                    <input type="date" id="expectedDelivery">
                </div>
                
                <button class="btn" id="calculatePregnancy">ট্র্যাকার শুরু করুন</button>
                
                <div class="schedule-list" id="pregnancySchedule" style="display: none;">
                    <h4>আপনার প্রসবপূর্ব চেকআপের সময়সূচী</h4>
                    <div id="ancScheduleList">
                        <!-- ANC schedule will be populated by JavaScript -->
                    </div>
                </div>
            </div>
            
            <!-- Child Vaccination Tracker -->
            <div class="tracker-content" id="child-tracker">
                <h3>শিশু টিকা ট্র্যাকার</h3>
                <p>আপনার শিশুর জন্ম তারিখ লিখুন এবং বাংলাদেশের ইপিআই টিকা সময়সূচী অনুযায়ী রিমাইন্ডার পান</p>
                
                <div class="form-group">
                    <label for="childName">শিশুর নাম (ঐচ্ছিক)</label>
                    <input type="text" id="childName" placeholder="শিশুর নাম">
                </div>
                
                <div class="form-group">
                    <label for="childBirthDate">শিশুর জন্ম তারিখ</label>
                    <input type="date" id="childBirthDate">
                </div>
                
                <button class="btn" id="calculateVaccination">ট্র্যাকার শুরু করুন</button>
                
                <div class="schedule-list" id="vaccinationSchedule" style="display: none;">
                    <h4>আপনার শিশুর টিকা সময়সূচী</h4>
                    <div id="vaccineScheduleList">
                        <!-- Vaccine schedule will be populated by JavaScript -->
                    </div>
                </div>
            </div>
        </section>
        
        <!-- Symptom Awareness Guide -->
        <section class="section" id="symptoms">
            <h2>লক্ষণ সচেতনতা গাইড</h2>
            
            <div class="hablu-quote">
                "হাবলুর দুঃস্বপ্ন: ওয়েবএমডি বাংলাদেশ সংস্করণ হয়ে ওঠা। তার সবচেয়ে কম প্রয়োজন হলো মানুষ যেন অ্যাপ থেকে স্ব-নির্ণয় না করে। এটি 'লক্ষণ লিখুন → রোগ নির্ণয় পান' নয়। এটি 'বিপদ সংকেত সম্পর্কে শিক্ষা দিন'।"
            </div>
            
            <div class="warning-box">
                <h4>⚠️ গুরুত্বপূর্ণ নোট</h4>
                <p>এই গাইড শুধুমাত্র শিক্ষামূলক উদ্দেশ্যে। এটি চিকিৎসা পরামর্শ বা রোগ নির্ণয়ের বিকল্প নয়। গুরুতর লক্ষণ দেখা দিলে অবশ্যই ডাক্তারের পরামর্শ নিন।</p>
            </div>
            
            <div class="symptom-categories">
                <div class="symptom-category" data-symptom="fever">
                    <h4>🔥 জ্বর</h4>
                    <p>জ্বর এবং সংশ্লিষ্ট লক্ষণ</p>
                </div>
                <div class="symptom-category" data-symptom="diarrhea">
                    <h4>💩 ডায়রিয়া</h4>
                    <p>ডায়রিয়া এবং পানিশূন্যতা</p>
                </div>
                <div class="symptom-category" data-symptom="respiratory">
                    <h4>😮‍💨 শ্বাসকষ্ট</h4>
                    <p>কাশি, সর্দি এবং শ্বাসকষ্ট</p>
                </div>
                <div class="symptom-category" data-symptom="chest">
                    <h4>❤️ বুকে ব্যথা</h4>
                    <p>বুক, পেট বা পেশীতে ব্যথা</p>
                </div>
                <div class="symptom-category" data-symptom="mental">
                    <h4>🧠 মানসিক স্বাস্থ্য</h4>
                    <p>মানসিক চাপ এবং উদ্বেগ</p>
                </div>
                <div class="symptom-category" data-symptom="child">
                    <h4>👶 শিশুদের লক্ষণ</h4>
                    <p>শিশুদের বিশেষ লক্ষণ</p>
                </div>
            </div>
            
            <!-- Symptom details will be populated by JavaScript -->
            <div id="symptomDetails">
                <!-- Symptom details will appear here -->
            </div>
        </section>
        
        <!-- Community Health Map -->
        <section class="section" id="map">
            <h2>আপনার এলাকায় স্বাস্থ্য সুবিধা খুঁজুন</h2>
            
            <div class="hablu-quote">
                "আমার গ্রামে কমিউনিটি ক্লিনিক ছিল 'মঙ্গল ও বৃহস্পতিবার সকালে, কখনো কখনো' খোলা। যখন আমার মায়ের বুকে ব্যথা হচ্ছিল, আমরা শুধু কোথায় যাব সেটা বের করতেই এক ঘন্টা হারিয়েছি।"
            </div>
            
            <div class="satire-box">
                <p><strong>এসডিজি ৩.৮:</strong> সার্বজনীন স্বাস্থ্য কভারেজ অর্জন করুন...<br>
                <strong>বাস্তবতা:</strong> ক্লিনিকের মানচিত্র দেখান এবং আশা করুন ব্যবহারকারীরা সেখানে যাওয়ার বাস ভাড়া দিতে পারবে।</p>
            </div>
            
            <div class="filter-section">
                <div class="filter-row">
                    <div class="filter-group">
                        <label for="division">বিভাগ</label>
                        <select id="division">
                            <option value="">বিভাগ নির্বাচন করুন</option>
                            <option value="dhaka">ঢাকা</option>
                            <option value="chittagong">চট্টগ্রাম</option>
                            <option value="rajshahi">রাজশাহী</option>
                            <option value="khulna">খুলনা</option>
                        </select>
                    </div>
                    <div class="filter-group">
                        <label for="district">জেলা</label>
                        <select id="district">
                            <option value="">জেলা নির্বাচন করুন</option>
                        </select>
                    </div>
                    <div class="filter-group">
                        <label for="upazila">উপজেলা</label>
                        <select id="upazila">
                            <option value="">উপজেলা নির্বাচন করুন</option>
                        </select>
                    </div>
                    <div class="filter-group">
                        <label for="facilityType">সুবিধার ধরন</label>
                        <select id="facilityType">
                            <option value="all">সব ধরনের সুবিধা</option>
                            <option value="clinic">কমিউনিটি ক্লিনিক</option>
                            <option value="health-center">ইউনিয়ন স্বাস্থ্য কেন্দ্র</option>
                            <option value="hospital">উপজেলা স্বাস্থ্য কমপ্লেক্স</option>
                            <option value="chw">কমিউনিটি স্বাস্থ্যকর্মী</option>
                            <option value="pharmacy">ফার্মেসি</option>
                        </select>
                    </div>
                </div>
            </div>
            
            <div class="map-container" id="healthMap">
                <!-- Map will be rendered here -->
            </div>
            
            <div class="resources-grid" id="healthResources">
                <!-- Resources will be populated by JavaScript -->
            </div>
        </section>
        
        <!-- Crisis contacts -->
        <section class="section" id="support">
            <h2>জরুরি সহায়তা</h2>
            <p>যদি আপনি বা আপনার পরিচিত কেউ মানসিক সংকটে থাকেন, নিচের হেল্পলাইনে যোগাযোগ করুন:</p>
            
            <div class="crisis-contacts">
                <h3>জরুরি যোগাযোগ</h3>
                <ul class="contact-list">
                    <li>জাতীয় মানসিক স্বাস্থ্য ইনস্টিটিউট হাসপাতাল: <strong>০১৭১৩-৩০৪৯৯৫</strong></li>
                    <li>মানসিক স্বাস্থ্য কাউন্সেলিং: <strong>১০৬৬৭</strong></li>
                    <li>সাইকিয়াট্রিক কেয়ার: <strong>০১৭১৬-৬২৩৪৮৬</strong></li>
                    <li>বাংলাদেশ প্রিভেন্টিভ সোসাইটি: <strong>০১৭১৫-৫৫৪৩৯১</strong></li>
                </ul>
            </div>
            
            <div class="privacy-notice">
                <strong>গুরুত্বপূর্ণ নোট:</strong> এই অ্যাপ্লিকেশনটি চিকিৎসা পরামর্শ প্রদান করে না। জরুরি অবস্থায় উপরের হেল্পলাইনে যোগাযোগ করুন বা নিকটস্থ স্বাস্থ্যকেন্দ্রে যান।
            </div>
        </section>
        
        <!-- Dashboard -->
        <section class="section dashboard" id="dashboard">
            <div class="dashboard-header">
                <h2>আপনার ড্যাশবোর্ড</h2>
                <button class="btn" id="addUpdateBtn">নতুন আপডেট যোগ করুন</button>
            </div>
            
            <div class="dashboard-stats">
                <div class="stat-card">
                    <div class="stat-value" id="moodStreak">০</div>
                    <div class="stat-label">চেক-ইন স্ট্রীক</div>
                </div>
                <div class="stat-card">
                    <div class="stat-value" id="helpRequests">০</div>
                    <div class="stat-label">সাহায্যের অনুরোধ</div>
                </div>
                <div class="stat-card">
                    <div class="stat-value" id="resourcesViewed">০</div>
                    <div class="stat-label">দেখা সম্পদ</div>
                </div>
                <div class="stat-card">
                    <div class="stat-value" id="communityPosts">০</div>
                    <div class="stat-label">কমিউনিটি পোস্ট</div>
                </div>
            </div>
            
            <div class="updates-section">
                <div class="update-form" id="updateForm" style="display: none;">
                    <h3>নতুন আপডেট যোগ করুন</h3>
                    <div class="form-group">
                        <label for="updateContent">আপনার আপডেট লিখুন</label>
                        <textarea id="updateContent" placeholder="আপনি আজ কেমন আছেন? আপনার অনুভূতি বা চিন্তা শেয়ার করুন..."></textarea>
                    </div>
                    <div class="form-group">
                        <label for="updatePrivacy">গোপনীয়তা সেটিং</label>
                        <select id="updatePrivacy">
                            <option value="public">সবার জন্য দৃশ্যমান</option>
                            <option value="anonymous">বেনামী (শুধুমাত্র কমিউনিটি সাপোর্টাররা দেখতে পারবেন)</option>
                            <option value="private">ব্যক্তিগত (শুধুমাত্র আপনি দেখতে পারবেন)</option>
                        </select>
                    </div>
                    <button class="btn" id="postUpdateBtn">পোস্ট করুন</button>
                    <button class="btn btn-secondary" id="cancelUpdateBtn">বাতিল করুন</button>
                </div>
                
                <h3>আপনার সাম্প্রতিক আপডেট</h3>
                <div class="updates-list" id="updatesList">
                    <!-- Updates will be populated by JavaScript -->
                </div>
            </div>
        </section>
    </div>
    
    <!-- Footer -->
    <footer>
        <div class="footer-container">
            <div class="footer-section">
                <h3>মন ভালো</h3>
                <p>বাংলাদেশের প্রতিটি মানুষের জন্য সহজলভ্য মানসিক স্বাস্থ্য সহায়তা</p>
            </div>
            
            <div class="footer-section">
                <h3>দ্রুত লিংক</h3>
                <ul class="footer-links">
                    <li><a href="#home">হোম</a></li>
                    <li><a href="#checkin">মেজাজ চেক-ইন</a></li>
                    <li><a href="#help">গোপন সহায়তা</a></li>
                    <li><a href="#seasonal">মৌসুমী স্বাস্থ্য</a></li>
                </ul>
            </div>
            
            <div class="footer-section">
                <h3>যোগাযোগ</h3>
                <ul class="footer-links">
                    <li>ইমেইল: info@monvalo.org</li>
                    <li>ফোন: ০১৬২৭-১২৯৭১৫</li>
                    <li>ঠিকানা: বাইউস্ট, কুমিল্লা</li>
                </ul>
            </div>
        </div>
        
        <div class="copyright">
            &copy; ২০২৫ মন ভালো - বাংলাদেশের জন্য মানসিক স্বাস্থ্য সহায়তা | BAIUST CSE Fall Fest Hackathon
        </div>
    </footer>
    
    <!-- Success Modal -->
    <div class="modal" id="successModal">
        <div class="modal-content">
            <button class="close-modal" id="closeSuccessModal">&times;</button>
            <h3>সফল!</h3>
            <p id="successMessage">আপনার অনুরোধ সফলভাবে সংরক্ষণ করা হয়েছে।</p>
            <button class="btn" id="okSuccessBtn">ঠিক আছে</button>
        </div>
    </div>
    
    <script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>
    <script>
        // User authentication state
        let currentUser = null;
        let isLoggedIn = false;
        
        // Check if user is logged in
        function checkLoginStatus() {
            const userData = localStorage.getItem('currentUser');
            if (userData) {
                currentUser = JSON.parse(userData);
                isLoggedIn = true;
                showMainContent();
            } else {
                showLoginForm();
            }
        }
        
        // Show login form
        function showLoginForm() {
            document.getElementById('loginSection').style.display = 'block';
            document.getElementById('mainContent').style.display = 'none';
            document.getElementById('dashboardLink').style.display = 'none';
            document.getElementById('userMenu').style.display = 'none';
            document.getElementById('loginLink').style.display = 'block';
        }
        
        // Show main content after login
        function showMainContent() {
            document.getElementById('loginSection').style.display = 'none';
            document.getElementById('mainContent').style.display = 'block';
            document.getElementById('dashboardLink').style.display = 'block';
            document.getElementById('userMenu').style.display = 'block';
            document.getElementById('loginLink').style.display = 'none';
            document.getElementById('userName').textContent = currentUser.name;
            
            // Update dashboard stats
            updateDashboardStats();
            loadUserUpdates();
        }
        
        // Update dashboard statistics
        function updateDashboardStats() {
            const moodData = JSON.parse(localStorage.getItem('moodData') || '{}');
            const moodStreak = calculateMoodStreak(moodData);
            document.getElementById('moodStreak').textContent = moodStreak;
            
            const helpRequests = JSON.parse(localStorage.getItem('helpRequests') || '[]');
            document.getElementById('helpRequests').textContent = helpRequests.length;
            
            const resourcesViewed = JSON.parse(localStorage.getItem('resourcesViewed') || '0');
            document.getElementById('resourcesViewed').textContent = resourcesViewed;
            
            const userUpdates = JSON.parse(localStorage.getItem('userUpdates') || '[]');
            const userUpdateCount = userUpdates.filter(update => update.userId === currentUser.id).length;
            document.getElementById('communityPosts').textContent = userUpdateCount;
        }
        
        // Calculate mood streak
        function calculateMoodStreak(moodData) {
            let streak = 0;
            const today = new Date();
            
            for (let i = 0; i < 30; i++) {
                const date = new Date();
                date.setDate(today.getDate() - i);
                const dateString = date.toISOString().split('T')[0];
                
                if (moodData[dateString]) {
                    streak++;
                } else {
                    break;
                }
            }
            
            return streak;
        }
        
        // Load user updates
        function loadUserUpdates() {
            const updatesList = document.getElementById('updatesList');
            updatesList.innerHTML = '';
            
            const userUpdates = JSON.parse(localStorage.getItem('userUpdates') || '[]');
            const userSpecificUpdates = userUpdates.filter(update => 
                update.userId === currentUser.id || update.privacy === 'public'
            );
            
            if (userSpecificUpdates.length === 0) {
                updatesList.innerHTML = '<p>আপনার এখনও কোন আপডেট নেই। আপনার প্রথম আপডেট যোগ করুন!</p>';
                return;
            }
            
            // Sort by date (newest first)
            userSpecificUpdates.sort((a, b) => new Date(b.date) - new Date(a.date));
            
            userSpecificUpdates.forEach(update => {
                const updateItem = document.createElement('div');
                updateItem.className = 'update-item';
                
                const authorName = update.userId === currentUser.id ? 'আপনি' : update.author;
                const displayDate = new Date(update.date).toLocaleDateString('bn-BD');
                
                updateItem.innerHTML = `
                    <div class="update-header">
                        <div class="update-author">${authorName}</div>
                        <div class="update-date">${displayDate}</div>
                    </div>
                    <div class="update-content">${update.content}</div>
                    ${update.userId === currentUser.id ? `<div style="margin-top: 10px; font-size: 0.8rem; color: #666;">গোপনীয়তা: ${getPrivacyLabel(update.privacy)}</div>` : ''}
                `;
                
                updatesList.appendChild(updateItem);
            });
        }
        
        // Get privacy label in Bangla
        function getPrivacyLabel(privacy) {
            switch(privacy) {
                case 'public': return 'সবার জন্য';
                case 'anonymous': return 'বেনামী';
                case 'private': return 'ব্যক্তিগত';
                default: return 'সবার জন্য';
            }
        }
        
        // Mobile menu toggle
        document.getElementById('mobileMenuBtn').addEventListener('click', function() {
            document.getElementById('mainNav').classList.toggle('active');
        });
        
        // User dropdown toggle
        document.getElementById('userBtn').addEventListener('click', function() {
            document.getElementById('userDropdown').classList.toggle('active');
        });
        
        // Close dropdown when clicking outside
        document.addEventListener('click', function(event) {
            if (!event.target.closest('.user-menu')) {
                document.getElementById('userDropdown').classList.remove('active');
            }
        });
        
        // Login functionality
        document.getElementById('loginBtn').addEventListener('click', function() {
            const email = document.getElementById('loginEmail').value;
            const password = document.getElementById('loginPassword').value;
            
            if (!email || !password) {
                alert('দয়া করে ইমেইল/ফোন এবং পাসওয়ার্ড প্রদান করুন।');
                return;
            }
            
            // In a real app, this would verify credentials with a server
            // For demo purposes, we'll use localStorage
            const users = JSON.parse(localStorage.getItem('users') || '[]');
            const user = users.find(u => (u.email === email || u.phone === email) && u.password === password);
            
            if (user) {
                currentUser = user;
                localStorage.setItem('currentUser', JSON.stringify(user));
                showMainContent();
                showSuccessModal('সফলভাবে লগ ইন করা হয়েছে!');
            } else {
                alert('ভুল ইমেইল/ফোন বা পাসওয়ার্ড।');
            }
        });
        
        // Register functionality
        document.getElementById('registerBtn').addEventListener('click', function() {
            const name = document.getElementById('registerName').value;
            const email = document.getElementById('registerEmail').value;
            const phone = document.getElementById('registerPhone').value;
            const password = document.getElementById('registerPassword').value;
            const confirmPassword = document.getElementById('registerConfirmPassword').value;
            
            if (!name || !email || !phone || !password || !confirmPassword) {
                alert('দয়া করে সব ফিল্ড পূরণ করুন।');
                return;
            }
            
            if (password !== confirmPassword) {
                alert('পাসওয়ার্ড মিলেনি।');
                return;
            }
            
            // In a real app, this would create a user account on a server
            // For demo purposes, we'll use localStorage
            const users = JSON.parse(localStorage.getItem('users') || '[]');
            
            // Check if user already exists
            if (users.find(u => u.email === email)) {
                alert('এই ইমেইল দিয়ে ইতিমধ্যে একটি অ্যাকাউন্ট আছে।');
                return;
            }
            
            const newUser = {
                id: Date.now().toString(),
                name: name,
                email: email,
                phone: phone,
                password: password,
                joinDate: new Date().toISOString()
            };
            
            users.push(newUser);
            localStorage.setItem('users', JSON.stringify(users));
            
            // Auto login after registration
            currentUser = newUser;
            localStorage.setItem('currentUser', JSON.stringify(newUser));
            showMainContent();
            showSuccessModal('অ্যাকাউন্ট সফলভাবে তৈরি হয়েছে!');
        });
        
        // Show register form
        document.getElementById('showRegister').addEventListener('click', function(e) {
            e.preventDefault();
            document.querySelector('.login-form').style.display = 'none';
            document.getElementById('registerForm').style.display = 'block';
        });
        
        // Show login form
        document.getElementById('showLogin').addEventListener('click', function(e) {
            e.preventDefault();
            document.querySelector('.login-form').style.display = 'block';
            document.getElementById('registerForm').style.display = 'none';
        });
        
        // Logout functionality
        document.getElementById('logoutBtn').addEventListener('click', function(e) {
            e.preventDefault();
            localStorage.removeItem('currentUser');
            currentUser = null;
            isLoggedIn = false;
            showLoginForm();
        });
        
        // Add update button
        document.getElementById('addUpdateBtn').addEventListener('click', function() {
            document.getElementById('updateForm').style.display = 'block';
        });
        
        // Cancel update
        document.getElementById('cancelUpdateBtn').addEventListener('click', function() {
            document.getElementById('updateForm').style.display = 'none';
            document.getElementById('updateContent').value = '';
        });
        
        // Post update
        document.getElementById('postUpdateBtn').addEventListener('click', function() {
            const content = document.getElementById('updateContent').value;
            const privacy = document.getElementById('updatePrivacy').value;
            
            if (!content) {
                alert('দয়া করে কিছু লিখুন।');
                return;
            }
            
            const userUpdates = JSON.parse(localStorage.getItem('userUpdates') || '[]');
            
            const newUpdate = {
                id: Date.now().toString(),
                userId: currentUser.id,
                author: privacy === 'anonymous' ? 'বেনামী ব্যবহারকারী' : currentUser.name,
                content: content,
                privacy: privacy,
                date: new Date().toISOString()
            };
            
            userUpdates.push(newUpdate);
            localStorage.setItem('userUpdates', JSON.stringify(userUpdates));
            
            document.getElementById('updateForm').style.display = 'none';
            document.getElementById('updateContent').value = '';
            
            loadUserUpdates();
            updateDashboardStats();
            showSuccessModal('আপডেট সফলভাবে পোস্ট করা হয়েছে!');
        });
        
        // Show success modal
        function showSuccessModal(message) {
            document.getElementById('successMessage').textContent = message;
            document.getElementById('successModal').style.display = 'flex';
        }
        
        // Close success modal
        document.getElementById('closeSuccessModal').addEventListener('click', function() {
            document.getElementById('successModal').style.display = 'none';
        });
        
        document.getElementById('okSuccessBtn').addEventListener('click', function() {
            document.getElementById('successModal').style.display = 'none';
        });
        
        // Maternal & Child Health Tracker functionality
        const trackerTabs = document.querySelectorAll('.tracker-tab');
        trackerTabs.forEach(tab => {
            tab.addEventListener('click', function() {
                const tabId = this.getAttribute('data-tab');
                
                // Update active tab
                trackerTabs.forEach(t => t.classList.remove('active'));
                this.classList.add('active');
                
                // Show corresponding content
                document.querySelectorAll('.tracker-content').forEach(content => {
                    content.classList.remove('active');
                });
                document.getElementById(`${tabId}-tracker`).classList.add('active');
            });
        });
        
        // Pregnancy tracker
        document.getElementById('calculatePregnancy').addEventListener('click', function() {
            const lastPeriodDate = document.getElementById('lastPeriodDate').value;
            const expectedDelivery = document.getElementById('expectedDelivery').value;
            
            if (!lastPeriodDate && !expectedDelivery) {
                alert('দয়া করে অন্তত একটি তারিখ প্রদান করুন।');
                return;
            }
            
            let deliveryDate;
            if (expectedDelivery) {
                deliveryDate = new Date(expectedDelivery);
            } else {
                // Calculate expected delivery date (40 weeks from last period)
                deliveryDate = new Date(lastPeriodDate);
                deliveryDate.setDate(deliveryDate.getDate() + 280); // 40 weeks
            }
            
            // Generate ANC schedule
            generateANCSchedule(deliveryDate);
            document.getElementById('pregnancySchedule').style.display = 'block';
        });
        
        // Generate ANC schedule
        function generateANCSchedule(deliveryDate) {
            const ancScheduleList = document.getElementById('ancScheduleList');
            ancScheduleList.innerHTML = '';
            
            const ancVisits = [
                { week: 8, title: 'প্রথম প্রসবপূর্ব চেকআপ' },
                { week: 12, title: 'দ্বিতীয় প্রসবপূর্ব চেকআপ' },
                { week: 16, title: 'তৃতীয় প্রসবপূর্ব চেকআপ' },
                { week: 20, title: 'চতুর্থ প্রসবপূর্ব চেকআপ' },
                { week: 24, title: 'পঞ্চম প্রসবপূর্ব চেকআপ' },
                { week: 28, title: 'ষষ্ঠ প্রসবপূর্ব চেকআপ' },
                { week: 32, title: 'সপ্তম প্রসবপূর্ব চেকআপ' },
                { week: 36, title: 'অষ্টম প্রসবপূর্ব চেকআপ' },
                { week: 38, title: 'নবম প্রসবপূর্ব চেকআপ' },
                { week: 40, title: 'দশম প্রসবপূর্ব চেকআপ' }
            ];
            
            const today = new Date();
            
            ancVisits.forEach(visit => {
                const visitDate = new Date(deliveryDate);
                visitDate.setDate(visitDate.getDate() - (280 - (visit.week * 7)));
                
                let status = 'upcoming';
                if (visitDate < today) {
                    status = 'overdue';
                }
                
                const scheduleItem = document.createElement('div');
                scheduleItem.className = `schedule-item ${status}`;
                
                const formattedDate = visitDate.toLocaleDateString('bn-BD');
                const statusText = status === 'upcoming' ? 'আসন্ন' : 'মিস হয়েছে';
                const statusClass = status === 'upcoming' ? 'status-upcoming' : 'status-overdue';
                
                scheduleItem.innerHTML = `
                    <div class="schedule-header">
                        <div class="schedule-title">${visit.title}</div>
                        <div class="schedule-date">${formattedDate}</div>
                    </div>
                    <div class="schedule-status ${statusClass}">${statusText}</div>
                `;
                
                ancScheduleList.appendChild(scheduleItem);
            });
        }
        
        // Vaccination tracker
        document.getElementById('calculateVaccination').addEventListener('click', function() {
            const childBirthDate = document.getElementById('childBirthDate').value;
            
            if (!childBirthDate) {
                alert('দয়া করে শিশুর জন্ম তারিখ প্রদান করুন।');
                return;
            }
            
            const birthDate = new Date(childBirthDate);
            
            // Generate vaccination schedule
            generateVaccinationSchedule(birthDate);
            document.getElementById('vaccinationSchedule').style.display = 'block';
        });
        
        // Generate vaccination schedule
        function generateVaccinationSchedule(birthDate) {
            const vaccineScheduleList = document.getElementById('vaccineScheduleList');
            vaccineScheduleList.innerHTML = '';
            
            const vaccines = [
                { days: 0, title: 'বিসিজি (BCG)', description: 'যক্ষ্মা রোগের টিকা' },
                { days: 42, title: 'পেন্টাভ্যালেন্ট ১ম ডোজ', description: 'ডিপথেরিয়া, টিটেনাস, পারটুসিস, হেপাটাইটিস বি এবং হিমোফিলাস ইনফ্লুয়েঞ্জা' },
                { days: 70, title: 'পেন্টাভ্যালেন্ট ২য় ডোজ', description: 'ডিপথেরিয়া, টিটেনাস, পারটুসিস, হেপাটাইটিস বি এবং হিমোফিলাস ইনফ্লুয়েঞ্জা' },
                { days: 98, title: 'পেন্টাভ্যালেন্ট ৩য় ডোজ', description: 'ডিপথেরিয়া, টিটেনাস, পারটুসিস, হেপাটাইটিস বি এবং হিমোফিলাস ইনফ্লুয়েঞ্জা' },
                { days: 270, title: 'এমআর ১ম ডোজ', description: 'হাম এবং রুবেলা' },
                { days: 540, title: 'এমআর ২য় ডোজ', description: 'হাম এবং রুবেলা' }
            ];
            
            const today = new Date();
            
            vaccines.forEach(vaccine => {
                const vaccineDate = new Date(birthDate);
                vaccineDate.setDate(vaccineDate.getDate() + vaccine.days);
                
                let status = 'upcoming';
                if (vaccineDate < today) {
                    status = 'overdue';
                }
                
                const scheduleItem = document.createElement('div');
                scheduleItem.className = `schedule-item ${status}`;
                
                const formattedDate = vaccineDate.toLocaleDateString('bn-BD');
                const statusText = status === 'upcoming' ? 'আসন্ন' : 'মিস হয়েছে';
                const statusClass = status === 'upcoming' ? 'status-upcoming' : 'status-overdue';
                
                scheduleItem.innerHTML = `
                    <div class="schedule-header">
                        <div class="schedule-title">${vaccine.title}</div>
                        <div class="schedule-date">${formattedDate}</div>
                    </div>
                    <div class="schedule-description">${vaccine.description}</div>
                    <div class="schedule-status ${statusClass}">${statusText}</div>
                `;
                
                vaccineScheduleList.appendChild(scheduleItem);
            });
        }
        
        // Symptom Awareness Guide
        const symptomCategories = document.querySelectorAll('.symptom-category');
        symptomCategories.forEach(category => {
            category.addEventListener('click', function() {
                const symptom = this.getAttribute('data-symptom');
                showSymptomDetails(symptom);
            });
        });
        
        // Show symptom details
        function showSymptomDetails(symptom) {
            const symptomDetails = document.getElementById('symptomDetails');
            symptomDetails.innerHTML = '';
            
            let detailsContent = '';
            
            switch(symptom) {
                case 'fever':
                    detailsContent = `
                        <div class="symptom-details active">
                            <h3>জ্বর সম্পর্কে তথ্য</h3>
                            <div class="danger-signs">
                                <h4>🚨 বিপদ সংকেত (ডাক্তার দেখান)</h4>
                                <ul>
                                    <li>জ্বর ৩ দিনের বেশি স্থায়ী হলে</li>
                                    <li>১০৩°F (৩৯.৪°C) এর বেশি জ্বর</li>
                                    <li>খিঁচুনি বা অজ্ঞান হয়ে যাওয়া</li>
                                    <li>গলা শক্ত হওয়া বা আলোতে চোখ ব্যথা</li>
                                    <li>শিশুদের ক্ষেত্রে: কান্না বন্ধ না করা, না খাওয়া</li>
                                </ul>
                            </div>
                            <div class="home-care">
                                <h4>🏠 ঘরোয়া যত্ন</h4>
                                <ul>
                                    <li>প্রচুর পানি ও তরল পান করুন</li>
                                    <li>পর্যাপ্ত বিশ্রাম নিন</li>
                                    <li>হালকা গরম পানিতে গা মুছুন</li>
                                    <li>হালকা ও সহজে হজম হয় এমন খাবার খান</li>
                                </ul>
                            </div>
                        </div>
                    `;
                    break;
                    
                case 'diarrhea':
                    detailsContent = `
                        <div class="symptom-details active">
                            <h3>ডায়রিয়া সম্পর্কে তথ্য</h3>
                            <div class="danger-signs">
                                <h4>🚨 বিপদ সংকেত (ডাক্তার দেখান)</h4>
                                <ul>
                                    <li>৩ দিনের বেশি ডায়রিয়া চলতে থাকলে</li>
                                    <li>মলের সাথে রক্ত গেলে</li>
                                    <li>পানিশূন্যতার লক্ষণ: শুষ্ক মুখ, চোখ গর্তে ঢুকে যাওয়া, প্রস্রাব কম হওয়া</li>
                                    <li>তীব্র পেট ব্যথা বা জ্বর</li>
                                </ul>
                            </div>
                            <div class="action-steps">
                                <h4>✅ করণীয়</h4>
                                <ul>
                                    <li>ওরাল স্যালাইন পান করুন</li>
                                    <li>পরিষ্কার পানি পান করুন</li>
                                    <li>হাত ভালোভাবে ধুয়ে নিন</li>
                                    <li>বাসি খাবার এড়িয়ে চলুন</li>
                                </ul>
                            </div>
                            <div class="warning-box">
                                <h4>⚠️ সতর্কতা</h4>
                                <p>ডায়রিয়া বন্ধ করার ওষুধ নিজে থেকে না খাওয়াই ভালো, বিশেষ করে শিশুদের ক্ষেত্রে।</p>
                            </div>
                        </div>
                    `;
                    break;
                    
                case 'respiratory':
                    detailsContent = `
                        <div class="symptom-details active">
                            <h3>শ্বাসকষ্ট সম্পর্কে তথ্য</h3>
                            <div class="danger-signs">
                                <h4>🚨 বিপদ সংকেত (ডাক্তার দেখান)</h4>
                                <ul>
                                    <li>নিশ্বাস নিতে কষ্ট হওয়া</li>
                                    <li>নীলচে ঠোঁট বা নখ</li>
                                    <li>বুকে তীব্র ব্যথা</li>
                                    <li>জ্বরের সাথে কাশি</li>
                                    <li>শিশুদের ক্ষেত্রে: দ্রুত শ্বাস, নাক ফুলে যাওয়া</li>
                                </ul>
                            </div>
                            <div class="home-care">
                                <h4>🏠 ঘরোয়া যত্ন</h4>
                                <ul>
                                    <li>গরম পানির ভাপ নিন</li>
                                    <li>গরম পানিতে লেবু ও মধু মিশিয়ে পান করুন</li>
                                    <li>ধুলাবালি ও ধোঁয়া এড়িয়ে চলুন</li>
                                    <li>পর্যাপ্ত বিশ্রাম নিন</li>
                                </ul>
                            </div>
                        </div>
                    `;
                    break;
                    
                case 'chest':
                    detailsContent = `
                        <div class="symptom-details active">
                            <h3>বুকে ব্যথা সম্পর্কে তথ্য</h3>
                            <div class="warning-box">
                                <h4>⚠️ গুরুত্বপূর্ণ সতর্কতা</h4>
                                <p>বুকে ব্যথা উপেক্ষা করবেন না। এটি হার্ট অ্যাটাকের লক্ষণ হতে পারে। অবিলম্বে হাসপাতালে যান।</p>
                            </div>
                            <div class="danger-signs">
                                <h4>🚨 বিপদ সংকেত (অবিলম্বে হাসপাতালে যান)</h4>
                                <ul>
                                    <li>বুকে চাপ, ভর বা ব্যথা</li>
                                    <li>ব্যথা বাহু, ঘাড়, চোয়াল বা পিঠে ছড়িয়ে পড়া</li>
                                    <li>শ্বাসকষ্ট</li>
                                    <li>ঠান্ডা ঘাম</li>
                                    <li>বমি বমি ভাব বা বমি</li>
                                </ul>
                            </div>
                        </div>
                    `;
                    break;
                    
                case 'mental':
                    detailsContent = `
                        <div class="symptom-details active">
                            <h3>মানসিক স্বাস্থ্য সম্পর্কে তথ্য</h3>
                            <div class="danger-signs">
                                <h4>🚨 বিপদ সংকেত (সাহায্য নিন)</h4>
                                <ul>
                                    <li>২ সপ্তাহের বেশি মন খারাপ থাকলে</li>
                                    <li>কোনো কিছু উপভোগ করতে না পারা</li>
                                    <li>ঘুম বা খাবারের অভ্যাসে বড় পরিবর্তন</li>
                                    <li>নিজেকে বা অন্যকে ক্ষতি করার想法</li>
                                    <li>দৈনন্দিন কাজ করতে অসুবিধা</li>
                                </ul>
                            </div>
                            <div class="action-steps">
                                <h4>✅ করণীয়</h4>
                                <ul>
                                    <li>কাউনের কথা বলুন - বন্ধু, পরিবার বা হেল্পলাইন</li>
                                    <li>নিয়মিত হালকা ব্যায়াম করুন</li>
                                    <li>পর্যাপ্ত ঘুমান</li>
                                    <li>সুষম খাবার খান</li>
                                    <li>মন ভালো রাখার কাজ করুন</li>
                                </ul>
                            </div>
                            <div class="home-care">
                                <h4>💚 মনে রাখবেন</h4>
                                <p>মানসিক সমস্যা দুর্বলতা নয়। সাহায্য চাওয়া সাহসের কাজ।</p>
                            </div>
                        </div>
                    `;
                    break;
                    
                case 'child':
                    detailsContent = `
                        <div class="symptom-details active">
                            <h3>শিশুদের বিশেষ লক্ষণ</h3>
                            <div class="danger-signs">
                                <h4>🚨 বিপদ সংকেত (ডাক্তার দেখান)</h4>
                                <ul>
                                    <li>জ্বর ১০০.৪°F (৩৮°C) এর বেশি (৩ মাসের কম বয়সী)</li>
                                    <li>জ্বর ৩ দিনের বেশি স্থায়ী হলে</li>
                                    <li>খিঁচুনি</li>
                                    <li>কান্না বন্ধ না করা</li>
                                    <li>খাওয়া-দাওয়া বন্ধ করে দেওয়া</li>
                                    <li>শ্বাসকষ্ট বা দ্রুত শ্বাস</li>
                                    <li>নীলচে ঠোঁট বা মুখ</li>
                                    <li>ঘাড় শক্ত হওয়া</li>
                                </ul>
                            </div>
                            <div class="action-steps">
                                <h4>✅ করণীয়</h4>
                                <ul>
                                    <li>নিয়মিত টিকা দিন</li>
                                    <li>পরিষ্কার-পরিচ্ছন্নতা বজায় রাখুন</li>
                                    <li>সুষম খাবার দিন</li>
                                    <li>পর্যাপ্ত তরল পান করান</li>
                                </ul>
                            </div>
                        </div>
                    `;
                    break;
            }
            
            symptomDetails.innerHTML = detailsContent;
        }
        
        // Initialize the app
        checkLoginStatus();
        
        // The rest of the existing JavaScript code for other features would go here
        // (mood tracking, map functionality, etc.)
        
        // For demonstration, I'm including a simplified version of the existing functionality
        // Mood tracker functionality
        const moodOptions = document.querySelectorAll('.mood-option');
        let selectedMood = null;
        
        moodOptions.forEach(option => {
            option.addEventListener('click', function() {
                moodOptions.forEach(opt => opt.classList.remove('selected'));
                this.classList.add('selected');
                selectedMood = this.getAttribute('data-mood');
            });
        });
        
        document.getElementById('saveMoodBtn').addEventListener('click', function() {
            if (selectedMood) {
                const today = new Date().toISOString().split('T')[0];
                const moodData = JSON.parse(localStorage.getItem('moodData') || '{}');
                moodData[today] = selectedMood;
                localStorage.setItem('moodData', JSON.stringify(moodData));
                
                alert('আপনার মেজাজ সংরক্ষণ করা হয়েছে! ধন্যবাদ আপনার অনুভূতি শেয়ার করার জন্য।');
                updateDashboardStats();
                
                moodOptions.forEach(opt => opt.classList.remove('selected'));
                selectedMood = null;
            } else {
                alert('দয়া করে আপনার আজকের মেজাজ নির্বাচন করুন।');
            }
        });
        
        // Initialize with some sample data for demonstration
        if (!localStorage.getItem('users')) {
            const sampleUsers = [
                {
                    id: '1',
                    name: 'হাবলু',
                    email: 'hablu@example.com',
                    phone: '01712345678',
                    password: 'password',
                    joinDate: new Date().toISOString()
                }
            ];
            localStorage.setItem('users', JSON.stringify(sampleUsers));
        }
    </script>
</body>
</html>
