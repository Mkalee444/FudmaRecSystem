
<?php
session_start();
if (!isset($_SESSION['username'])) {
    header("Location: login.php"); 
    exit();
}
?>

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Admin Dashboard</title>
    <style>
        /* Reset and General Styles */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: Arial, sans-serif;
            display: flex;
            flex-direction: column;
            min-height: 100vh;
            background: #f4f4f9;
        }

        header {
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: 10px 20px;
            background: #003366;
            color: white;
        }

        header img {
            height: 50px;
        }

        header h1 {
            font-size: 20px;
            margin-left: 10px;
        }

        footer {
            background: #003366;
            color: white;
            text-align: center;
            padding: 10px 20px;
            margin-top: auto;
        }

        /* Dashboard Layout */
        .dashboard-container {
            display: flex;
            flex: 1;
            position: relative;
        }

        /* Sidebar Menu */
        nav {
            width: 240px;
            background: #003366;
            color: white;
            display: flex;
            flex-direction: column;
            padding: 10px 0;
            position: fixed;
            left: 0;
            top: 60px;
            height: calc(100vh - 60px);
            transition: transform 0.3s ease;
            z-index: 10;
        }

        nav ul {
            list-style: none;
            padding: 0;
        }

        nav ul li {
            margin: 10px 0;
        }

        nav ul li button {
            display: flex;
            align-items: center;
            width: 100%;
            background: #0055cc;
            color: white;
            border: none;
            padding: 10px 15px;
            border-radius: 5px;
            font-size: 14px;
            text-align: left;
            cursor: pointer;
            transition: background 0.3s ease;
        }

        nav ul li button:hover {
            background: #0077ff;
        }

        nav ul li button i {
            margin-right: 10px;
        }

        nav.hidden {
            transform: translateX(-100%);
        }

        /* Content Area */
        .content {
            margin-left: 240px;
            flex: 1;
            padding: 20px;
            background: white;
            transition: margin-left 0.3s ease;
        }

        .content iframe {
            width: 100%;
            height: calc(100vh - 100px); /* Subtract header and footer height */
            border: none;
        }

        /* Responsive Design */
        @media (max-width: 768px) {
            nav {
                width: 240px;
            }

            .content {
                margin-left: 0;
            }

            nav ul li button {
                font-size: 12px;
            }

            header h1 {
                font-size: 18px;
            }
        }

        @media (max-width: 480px) {
            nav {
                width: 240px; /* Maintain the same width as desktop */
                transform: translateX(-100%);
                position: fixed;
                z-index: 10;
            }

            .content {
                margin-left: 0;
            }

            .menu-toggle {
                display: flex;
                align-items: center;
                padding: 10px;
                background: #003366;
                color: white;
                cursor: pointer;
            }

            .menu-toggle i {
                font-size: 20px;
            }

            nav.active {
                transform: translateX(0);
            }

            .content iframe {
                height: calc(100vh - 100px);
            }
        }
    </style>
</head>
<body>
    <!-- Header -->
    <header>
        <img src="logo.png" alt="Logo">
        <h1>Admin Dashboard</h1>
        <div class="menu-toggle" onclick="toggleMenu()">
            <i>☰</i>
        </div>
    </header>

    <div class="dashboard-container">
        <!-- Sidebar Menu -->
        <nav id="sidebar" class="hidden">
            <ul>
                <li><button onclick="loadContent('file_case.php')"><i>📄</i> File Case</button></li>
                <li><button onclick="loadContent('search_case.php')"><i>🔍</i> Search Case</button></li>
                <li><button onclick="loadContent('reports.php')"><i>📊</i> Reports</button></li>
                <li><button onclick="loadContent('queries.php')"><i>❓</i> Queries</button></li>
                <li><button onclick="loadContent('change_password.php')"><i>🔒</i> Change Password</button></li>
                <li><button onclick="location.href='logout.php'"><i>🚪</i> Logout</button></li>
            </ul>
        </nav>

        <!-- Content Area -->
        <div class="content">
            <iframe name="contentFrame" src="file_case.php"></iframe>
        </div>
    </div>

    <!-- Footer -->
    <footer>
        <p>&copy; 2024 Admin Dashboard. All rights reserved.</p>
    </footer>

    <script>
        const sidebar = document.getElementById('sidebar');

        function toggleMenu() {
            sidebar.classList.toggle('hidden');
            sidebar.classList.toggle('active');
        }

        function loadContent(url) {
            document.querySelector('iframe').src = url;
            if (window.innerWidth <= 480) {
                sidebar.classList.add('hidden');
            }
        }
    </script>
</body>
</html>

