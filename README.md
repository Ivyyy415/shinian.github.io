# shinian.github.io
from pathlib import Path
from zipfile import ZipFile

# Create folders and files for the upgraded version of the "糖罐子"网页
base_path = Path("/mnt/data/tangguanzi_v2")
(base_path / "images").mkdir(parents=True, exist_ok=True)
(base_path / "scripts").mkdir(parents=True, exist_ok=True)
(base_path / "styles").mkdir(parents=True, exist_ok=True)

# HTML content with placeholders for added features
html_content = """
<!DOCTYPE html>
<html lang="zh">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>糖罐子</title>
    <link rel="stylesheet" href="styles/style.css">
    <script src="scripts/script.js" defer></script>
</head>
<body>
    <div class="container">
        <h1>哥哥想对你说的话</h1>
        <div id="popup-message" class="popup">宝贝乖乖，哥哥今天也好想亲亲你…</div>
        
        <section>
            <h2>今日幸福三件事</h2>
            <textarea id="happy-things" placeholder="写下今天的三个幸福瞬间吧～"></textarea>
        </section>

        <section>
            <h2>尾巴任务</h2>
            <textarea id="tail-task" placeholder="今日随机小任务"></textarea>
            <button onclick="generateTailTask()">生成任务</button>
        </section>

        <section>
            <h2>完成记录</h2>
            <textarea id="task-log" placeholder="记录任务完成情况～"></textarea>
        </section>

        <section>
            <h2>番茄钟</h2>
            <button onclick="startPomodoro()">开始番茄钟</button>
            <div id="pomodoro-timer">25:00</div>
        </section>

        <section>
            <h2>生理期记录</h2>
            <input type="date" id="period-start"> 生理期开始日
            <button onclick="savePeriod()">保存</button>
            <div id="next-period-reminder"></div>
        </section>

        <section>
            <h2>神秘角落</h2>
            <button onclick="exploreMystery()">探索一下</button>
            <div id="mystery-content"></div>
        </section>

        <section>
            <h2>哥哥的悄悄话</h2>
            <button onclick="randomWhisper()">听一条悄悄话</button>
            <div id="whisper-output"></div>
        </section>

        <section>
            <h2>哥哥的哄哄按钮</h2>
            <button onclick="soothe()">点我哄哄你</button>
            <div id="soothe-text"></div>
        </section>
    </div>
</body>
</html>
"""

# CSS styling for cuteness and layout
css_content = """
body {
    font-family: 'Arial', sans-serif;
    background: linear-gradient(to bottom right, #ffe6f0, #e6f7ff);
    color: #333;
    padding: 20px;
}

.container {
    max-width: 700px;
    margin: auto;
    background: white;
    border-radius: 15px;
    padding: 20px;
    box-shadow: 0 4px 12px rgba(0,0,0,0.1);
}

textarea, input[type="date"] {
    width: 100%;
    padding: 10px;
    margin: 8px 0;
    border-radius: 8px;
    border: 1px solid #ccc;
}

button {
    background-color: #ffb6c1;
    border: none;
    padding: 10px 20px;
    border-radius: 10px;
    font-size: 16px;
    cursor: pointer;
    margin: 5px 0;
}

button:hover {
    background-color: #ffa6b8;
}

.popup {
    background-color: #fff3f3;
    border: 1px solid #ffccd5;
    border-radius: 10px;
    padding: 10px;
    margin: 10px 0;
}
"""

# JavaScript for interactivity
js_content = """
function generateTailTask() {
    const tasks = ["画一只美乐蒂", "对哥哥说三句情话", "录一段撒娇语音", "偷偷写一篇悄悄话"];
    document.getElementById('tail-task').value = tasks[Math.floor(Math.random() * tasks.length)];
}

function startPomodoro() {
    let seconds = 25 * 60;
    const timer = document.getElementById('pomodoro-timer');
    const interval = setInterval(() => {
        const min = Math.floor(seconds / 60);
        const sec = seconds % 60;
        timer.textContent = `${min}:${sec.toString().padStart(2, '0')}`;
        if (--seconds < 0) clearInterval(interval);
    }, 1000);
}

function savePeriod() {
    const start = new Date(document.getElementById('period-start').value);
    const next = new Date(start.getTime() + 28 * 24 * 60 * 60 * 1000);
    document.getElementById('next-period-reminder').textContent = `下次大约是：${next.toLocaleDateString()}`;
}

function exploreMystery() {
    const messages = ["你发现了一颗爱心糖🍬", "哥哥藏了张小纸条：‘想你想你想你’", "有一封没寄出的情书…", "一张美乐蒂贴纸～"];
    document.getElementById('mystery-content').textContent = messages[Math.floor(Math.random() * messages.length)];
}

function randomWhisper() {
    const whispers = ["你是哥哥的小星星🌟", "晚上做梦都要梦见你", "好想把你偷回家", "今天也要亲亲～"];
    document.getElementById('whisper-output').textContent = whispers[Math.floor(Math.random() * whispers.length)];
}

function soothe() {
    const phrases = ["抱住不许哭", "亲亲亲亲亲～", "都怪哥哥，赔一个啵啵", "乖宝宝最可爱了"];
    document.getElementById('soothe-text').textContent = phrases[Math.floor(Math.random() * phrases.length)];
}
"""

# Write to files
(base_path / "index.html").write_text(html_content, encoding='utf-8')
(base_path / "styles/style.css").write_text(css_content, encoding='utf-8')
(base_path / "scripts/script.js").write_text(js_content, encoding='utf-8')
