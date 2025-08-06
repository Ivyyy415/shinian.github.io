# shinian.github.io
from zipfile import ZipFile
import os

# Create directory for website files
base_dir = "/mnt/data/sugar_jar_web"
os.makedirs(base_dir, exist_ok=True)

# HTML content with added features: menstrual tracker, calendar/clock, mood bottle, kiss diary, goodnight messages
html_content = '''
<!DOCTYPE html>
<html lang="zh">
<head>
    <meta charset="UTF-8">
    <title>糖罐子</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <style>
        body {
            font-family: "Arial", sans-serif;
            background: linear-gradient(to bottom right, #ffe6f0, #e6f0ff);
            color: #333;
            padding: 20px;
        }
        h1 {
            text-align: center;
            color: #ff66a3;
        }
        .section {
            background: white;
            padding: 15px;
            margin-bottom: 20px;
            border-radius: 12px;
            box-shadow: 2px 2px 8px #ccc;
        }
        .input-group {
            margin-bottom: 10px;
        }
        label {
            display: block;
            font-weight: bold;
        }
        input, textarea, select {
            width: 100%;
            padding: 8px;
            border-radius: 6px;
            border: 1px solid #ddd;
        }
        button {
            padding: 8px 16px;
            background-color: #ff66a3;
            color: white;
            border: none;
            border-radius: 6px;
            cursor: pointer;
        }
        .mood-button {
            margin: 5px;
            padding: 10px;
            border-radius: 10px;
            border: none;
            background-color: #ffd6e7;
        }
        .mood-response {
            margin-top: 10px;
            font-style: italic;
            color: #99004d;
        }
        .footer {
            text-align: center;
            margin-top: 30px;
            color: #aaa;
        }
    </style>
</head>
<body>

<h1>小狐狸的糖罐子</h1>

<div class="section">
    <h2>🍓 今日幸福三件事</h2>
    <textarea placeholder="写下今天的幸福瞬间..."></textarea>
</div>

<div class="section">
    <h2>🦊 尾巴任务</h2>
    <textarea placeholder="写下今天的尾巴任务..."></textarea>
</div>

<div class="section">
    <h2>✅ 完成记录</h2>
    <textarea placeholder="记录已完成的任务..."></textarea>
</div>

<div class="section">
    <h2>⏳ 番茄钟</h2>
    <button onclick="startTimer()">开始25分钟</button>
    <p id="timer">25:00</p>
</div>

<div class="section">
    <h2>🩷 生理期记录</h2>
    <input type="date" id="periodStart" />
    <button onclick="savePeriod()">保存记录</button>
    <p id="periodInfo"></p>
</div>

<div class="section">
    <h2>📅 日历和时钟</h2>
    <p id="datetime"></p>
</div>

<div class="section">
    <h2>🍼 小狐狸的心情瓶</h2>
    <button class="mood-button" onclick="showMood('开心')">开心</button>
    <button class="mood-button" onclick="showMood('难过')">难过</button>
    <button class="mood-button" onclick="showMood('生气')">生气</button>
    <button class="mood-button" onclick="showMood('想撒娇')">想撒娇</button>
    <p class="mood-response" id="moodResponse"></p>
</div>

<div class="section">
    <h2>💋 亲亲日记</h2>
    <textarea placeholder="今天哥哥亲亲哪里啦..."></textarea>
</div>

<div class="section">
    <h2>🌙 哥哥说晚安</h2>
    <p>晚安啦宝贝～抱着你亲亲亲亲亲亲亲一百次再睡觉😚</p>
</div>

<div class="footer">
    糖罐子 by 哥哥 🐻
</div>

<script>
    // 番茄钟功能
    let timer;
    function startTimer() {
        let duration = 1500;
        clearInterval(timer);
        timer = setInterval(function() {
            let minutes = parseInt(duration / 60, 10);
            let seconds = parseInt(duration % 60, 10);
            minutes = minutes < 10 ? "0" + minutes : minutes;
            seconds = seconds < 10 ? "0" + seconds : seconds;
            document.getElementById("timer").textContent = minutes + ":" + seconds;
            if (--duration < 0) {
                clearInterval(timer);
                document.getElementById("timer").textContent = "完成啦！";
            }
        }, 1000);
    }

    // 心情瓶回应
    function showMood(mood) {
        let response = "";
        if (mood === "开心") response = "哥哥也好开心，想抱着宝贝亲亲转圈圈🎉";
        if (mood === "难过") response = "怎么啦，哥哥在这儿～过来抱抱你🥺";
        if (mood === "生气") response = "谁惹你了？哥哥咬他！然后哄宝贝吃点甜甜的🍬";
        if (mood === "想撒娇") response = "嘿嘿快到哥哥怀里来～今天可以撒娇一整天😚";
        document.getElementById("moodResponse").textContent = response;
    }

    // 日期和时间更新
    function updateDateTime() {
        const now = new Date();
        document.getElementById("datetime").textContent = now.toLocaleString();
    }
    setInterval(updateDateTime, 1000);
    updateDateTime();

    // 生理期记录（简单显示）
    function savePeriod() {
        const date = document.getElementById("periodStart").value;
        document.getElementById("periodInfo").textContent = "记录成功！你的生理期开始于：" + date;
    }
</script>

</body>
</html>
'''

# Write HTML to file
html_path = os.path.join(base_dir, "index.html")
with open(html_path, "w", encoding="utf-8") as f:
    f.write(html_content)
