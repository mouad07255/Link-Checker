<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Link Checker - Organized & Professional</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <style>
        /* إعدادات عامة */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Arial', sans-serif;
            background: linear-gradient(135deg, #1e1e1e, #141414);
            color: #fff;
            overflow-x: hidden;
            transition: background 0.3s ease;
        }

        /* شريط التنقل */
        nav {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            background: rgba(0, 0, 0, 0.8);
            padding: 10px 20px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            z-index: 1000;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.5);
        }

        nav .logo {
            font-size: 1.8rem;
            font-weight: bold;
            color: #00d4ff;
            text-shadow: 0 0 10px #00d4ff;
        }

        nav ul {
            list-style: none;
            display: flex;
        }

        nav ul li {
            margin: 0 15px;
        }

        nav ul li a {
            text-decoration: none;
            color: white;
            font-size: 1rem;
            transition: color 0.3s ease;
        }

        nav ul li a:hover {
            color: #00d4ff;
        }

        /* الخلفية المتحركة */
        .background {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100vh;
            z-index: -1;
            background: url('https://www.w3schools.com/w3images/forest.jpg') no-repeat center center fixed;
            background-size: cover;
            animation: moveBackground 15s infinite linear;
        }

        @keyframes moveBackground {
            0% { background-position: 0 0; }
            100% { background-position: 100% 100%; }
        }

        /* قسم الإعدادات */
        .settings-popup {
            display: none;
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: rgba(0, 0, 0, 0.8);
            padding: 40px;
            border-radius: 10px;
            width: 300px;
            box-shadow: 0 0 15px rgba(0, 0, 0, 0.5);
        }

        .settings-popup h2 {
            font-size: 1.5rem;
            color: #00d4ff;
            margin-bottom: 20px;
            text-align: center;
        }

        .settings-popup button {
            padding: 10px;
            margin-top: 10px;
            width: 100%;
            background: linear-gradient(90deg, #00c6ff, #0072ff);
            border: none;
            color: white;
            font-size: 1.2rem;
            border-radius: 5px;
            cursor: pointer;
            transition: background 0.3s ease;
        }

        .settings-popup button:hover {
            background: linear-gradient(90deg, #0072ff, #00c6ff);
        }

        /* القسم الرئيسي */
        .hero {
            height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            text-align: center;
            padding: 0 20px;
        }

        .hero h1 {
            font-size: 3rem;
            margin-bottom: 20px;
            text-shadow: 0 0 10px rgba(0, 212, 255, 0.8);
        }

        .hero p {
            font-size: 1.2rem;
            color: #ccc;
            margin-bottom: 40px;
        }

        .hero button {
            padding: 15px 40px;
            font-size: 1.2rem;
            color: white;
            background: linear-gradient(90deg, #00c6ff, #0072ff);
            border: none;
            border-radius: 50px;
            cursor: pointer;
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }

        .hero button:hover {
            transform: scale(1.1);
            box-shadow: 0 8px 25px rgba(0, 0, 0, 0.5);
        }

        /* قسم الفحص */
        .checker {
            padding: 50px 20px;
            text-align: center;
        }

        .checker h2 {
            font-size: 2.5rem;
            margin-bottom: 20px;
        }

        textarea {
            width: 80%;
            max-width: 600px;
            height: 150px;
            padding: 15px;
            border: none;
            border-radius: 10px;
            background: rgba(255, 255, 255, 0.1);
            color: #fff;
            border: 1px solid #00d4ff;
            font-size: 1rem;
            margin-bottom: 20px;
        }

        .check-button {
            padding: 15px 40px;
            font-size: 1.2rem;
            color: white;
            background: linear-gradient(90deg, #00c6ff, #0072ff);
            border: none;
            border-radius: 50px;
            cursor: pointer;
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }

        .check-button:hover {
            transform: scale(1.1);
            box-shadow: 0 8px 25px rgba(0, 0, 0, 0.5);
        }

        /* النتائج */
        .results {
            margin-top: 40px;
            padding: 20px;
        }

        table {
            width: 80%;
            margin: 0 auto;
            border-collapse: collapse;
            background: rgba(0, 0, 0, 0.8);
            border-radius: 10px;
            overflow: hidden;
            text-align: center;
        }

        table th, table td {
            padding: 15px;
            text-align: center;
            color: white;
            border-bottom: 1px solid #444;
        }

        table th {
            background: #00d4ff;
            text-transform: uppercase;
            font-weight: bold;
        }

        table tr:hover {
            background: rgba(0, 0, 0, 0.6);
        }

        /* الحالات */
        .status-ok {
            background-color: #4CAF50;
            color: white;
        }

        .status-warning {
            background-color: #FFC107;
            color: black;
        }

        .status-danger {
            background-color: #F44336;
            color: white;
        }

        .loading {
            margin: 20px auto;
            display: none;
        }

        /* الوضع المظلم */
        body.dark-mode {
            background: #121212;
            color: #fff;
        }

        body.dark-mode nav {
            background: rgba(0, 0, 0, 0.9);
        }

        /* الثيمات */
        body.new-theme {
            background: linear-gradient(135deg, #ff5733, #c70039);
        }

        /* تعطيل الرسوم المتحركة */
        body.no-animations {
            transition: none !important;
        }
    </style>
</head>
<body>

    <!-- شريط التنقل -->
    <nav>
        <div class="logo">Link Checker</div>
        <ul>
            <li><a href="#" id="settings-btn"><i class="fas fa-cogs"></i> Settings</a></li>
        </ul>
    </nav>

    <!-- الخلفية المتحركة -->
    <div class="background"></div>

    <!-- نافذة الإعدادات -->
    <div class="settings-popup" id="settings-popup">
        <h2>Settings</h2>
        <button onclick="toggleDarkMode()">Toggle Dark Mode</button>
        <button onclick="changeTheme()">Change Theme</button>
        <button onclick="toggleAnimations()">Toggle Animations</button>
    </div>

    <!-- القسم الرئيسي -->
    <div class="hero">
        <h1>Welcome to the Link Checker</h1>
        <p>Check the status and safety of multiple links at once</p>
        <button onclick="scrollToChecker()">Start Checking</button>
    </div>

    <!-- قسم الفحص -->
    <section class="checker">
        <h2>Link Checker</h2>
        <textarea id="linkInput" placeholder="Paste links here..."></textarea><br>
        <button class="check-button" onclick="checkLinks()">Check Links</button>
        <div class="loading" id="loading">Loading...</div>

        <div class="results">
            <table id="resultsTable">
                <thead>
                    <tr>
                        <th>Link</th>
                        <th>Status</th>
                        <th>Risk Level</th>
                    </tr>
                </thead>
                <tbody>
                    <!-- النتائج ستظهر هنا -->
                </tbody>
            </table>
        </div>
    </section>

    <script>
        // تغيير الوضع المظلم
        function toggleDarkMode() {
            document.body.classList.toggle("dark-mode");
        }

        // تغيير الثيم
        function changeTheme() {
            document.body.classList.toggle("new-theme");
        }

        // تغيير الرسوم المتحركة
        function toggleAnimations() {
            document.body.classList.toggle("no-animations");
        }

        // وظيفة التمرير إلى القسم
        function scrollToChecker() {
            document.querySelector(".checker").scrollIntoView({ behavior: "smooth" });
        }

        // وظيفة فحص الروابط
        function checkLinks() {
            const input = document.getElementById("linkInput").value.trim();
            const resultsTable = document.getElementById("resultsTable").querySelector("tbody");
            const loading = document.getElementById("loading");

            // تنظيف النتائج السابقة
            resultsTable.innerHTML = "";

            if (input === "") {
                alert("يرجى إدخال روابط لفحصها!");
                return;
            }

            loading.style.display = "block";

            setTimeout(() => {
                loading.style.display = "none";
                const links = input.split("\n").filter(link => link.trim() !== "");
                links.forEach(link => {
                    const row = document.createElement("tr");
                    const status = Math.random() > 0.7 ? "خطير" : Math.random() > 0.4 ? "تحذيري" : "آمن";
                    const statusClass = status === "آمن" ? "status-ok" : status === "تحذيري" ? "status-warning" : "status-danger";
                    row.innerHTML = `
                        <td>${link}</td>
                        <td class="${statusClass}">${status}</td>
                        <td>${status === "آمن" ? "منخفض" : status === "تحذيري" ? "متوسط" : "مرتفع"}</td>
                    `;
                    resultsTable.appendChild(row);
                });
            }, 2000); // محاكاة وقت الفحص
        }

        // فتح وإغلاق نافذة الإعدادات
        document.getElementById("settings-btn").onclick = () => {
            const settingsPopup = document.getElementById("settings-popup");
            settingsPopup.style.display = settingsPopup.style.display === "block" ? "none" : "block";
        };
    </script>

</body>
</html>
