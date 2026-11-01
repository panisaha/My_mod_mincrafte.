<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My Mod Minecraft</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        body {
            background-color: #121212;
            color: #ffffff;
            line-height: 1.6;
        }
        header {
            background: linear-gradient(135deg, #1f1c2c, #928dab);
            padding: 60px 20px;
            text-align: center;
            border-bottom: 4px solid #00ff88;
        }
        header h1 {
            font-size: 2.5rem;
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.5);
        }
        header p {
            font-size: 1.2rem;
            color: #e0e0e0;
        }
        .container {
            max-width: 800px;
            margin: 40px auto;
            padding: 0 20px;
        }
        .about-box {
            background-color: #1e1e1e;
            padding: 30px;
            border-radius: 10px;
            box-shadow: 0 4px 6px rgba(0,0,0,0.3);
            margin-bottom: 30px;
            border-left: 4px solid #00ff88;
        }
        .download-btn {
            display: block;
            width: 100%;
            max-width: 300px;
            margin: 0 auto;
            background-color: #00ff88;
            color: #121212;
            text-align: center;
            padding: 15px;
            font-size: 1.2rem;
            font-weight: bold;
            text-decoration: none;
            border-radius: 8px;
            transition: background-color 0.3s, transform 0.2s;
        }
        .download-btn:hover {
            background-color: #00cc6a;
            transform: scale(1.05);
        }
        .info {
            text-align: center;
            margin-top: 15px;
            font-size: 0.9rem;
            color: #aaaaaa;
        }
        footer {
            text-align: center;
            padding: 20px;
            margin-top: 50px;
            border-top: 1px solid #333;
            color: #777;
        }
    </style>
</head>
<body>

    <header>
        <h1>My Mod Minecraft</h1>
        <p>Custom mods for your Minecraft experience</p>
    </header>

    <div class="container">
        <div class="about-box">
            <h2>About This Mod</h2>
            <br>
            <p>Hello! We are a team creating custom Minecraft mods for you to download and enjoy. If you have any ideas or items you'd like to see added to the game, feel free to leave a comment, and we will make the mod for you. Thank you for your support!</p>
        </div>

        <!-- لینک دانلود (بعدا آدرس فایل .jar رو اینجا میذاریم) -->
        <a href="#" class="download-btn">Download Mod</a>
        <div class="info">
            Requires: <strong>Minecraft 1.20.1</strong> | <strong>Forge</strong> | <strong>Java 17</strong>
        </div>

        <!-- دکمه پشتیبانی (ایمیل خودت رو جایگزین کن) -->
        <div style="text-align: center; margin-top: 40px;">
            <a href="mailto:ایمیل_خودت_اینجا@example.com?subject=Support%20Request" style="background-color: #007bff; color: white; padding: 12px 24px; text-decoration: none; border-radius: 8px; font-weight: bold; display: inline-block;">📧 Contact Support</a>
        </div>
        
        <!-- کدهای giscus (کامنت‌ها) -->
        <script src="https://giscus.app/client.js"
            data-repo="panisaha/My_mod_mincrafte"
            data-repo-id="R_kgDOVe-RMQ"
            data-category="Announcements"
            data-category-id="DIC_kwDOVe-RMc4DKJMM"
            data-mapping="pathname"
            data-strict="0"
            data-reactions-enabled="1"
            data-emit-metadata="0"
            data-input-position="bottom"
            data-theme="preferred_color_scheme"
            data-lang="en"
            crossorigin="anonymous"
            async>
        </script>
    </div>

    <footer>
        &copy; 2026 My Mod Minecraft. All rights reserved.
    </footer>

</body>
</html>
