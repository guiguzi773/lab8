<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>随机选择学生</title>
    <style>
        body {
            font-family: 'Microsoft YaHei', sans-serif;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            margin: 0;
            background-color: #f5f5f5;
        }
        
        .container {
            text-align: center;
            background-color: white;
            padding: 30px;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            width: 80%;
            max-width: 500px;
        }
        
        h1 {
            color: #333;
            margin-bottom: 30px;
        }
        
        .display-area {
            height: 100px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 24px;
            font-weight: bold;
            color: #2c3e50;
            margin: 20px 0;
            border: 2px dashed #ccc;
            border-radius: 5px;
            background-color: #f9f9f9;
        }
        
        .selected-area {
            min-height: 60px;
            padding: 15px;
            margin-top: 20px;
            border: 2px solid #3498db;
            border-radius: 5px;
            background-color: #eaf2f8;
            font-size: 20px;
        }
        
        .buttons {
            margin-top: 30px;
        }
        
        button {
            padding: 10px 25px;
            margin: 0 10px;
            font-size: 16px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            transition: all 0.3s;
        }
        
        #startBtn {
            background-color: #2ecc71;
            color: white;
        }
        
        #startBtn:hover {
            background-color: #27ae60;
        }
        
        #stopBtn {
            background-color: #e74c3c;
            color: white;
        }
        
        #stopBtn:hover {
            background-color: #c0392b;
        }
        
        button:disabled {
            background-color: #95a5a6;
            cursor: not-allowed;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>随机选择学生</h1>
        
        <div class="display-area" id="displayArea">
            准备开始...
        </div>
        
        <div class="selected-area" id="selectedArea">
            选中学生将显示在这里
        </div>
        
        <div class="buttons">
            <button id="startBtn">开始</button>
            <button id="stopBtn" disabled>停止</button>
        </div>
    </div>

    <script>
        // 学生名单
        const students = [
            "张三", "李四", "王五", "赵六", "钱七", 
            "孙八", "周九", "吴十", "郑十一", "王十二",
            "刘十三", "陈十四", "杨十五", "黄十六", "赵十七"
        ];
        
        // 获取DOM元素
        const displayArea = document.getElementById("displayArea");
        const selectedArea = document.getElementById("selectedArea");
        const startBtn = document.getElementById("startBtn");
        const stopBtn = document.getElementById("stopBtn");
        
        let timer = null;
        let isRunning = false;
        
        // 随机选择学生函数
        function getRandomStudent() {
            const randomIndex = Math.floor(Math.random() * students.length);
            return students[randomIndex];
        }
        
        // 开始随机选择
        startBtn.addEventListener("click", function() {
            if (isRunning) return;
            
            isRunning = true;
            startBtn.disabled = true;
            stopBtn.disabled = false;
            
            // 快速切换显示不同的学生
            timer = setInterval(function() {
                displayArea.textContent = getRandomStudent();
            }, 100);
        });
        
        // 停止随机选择
        stopBtn.addEventListener("click", function() {
            if (!isRunning) return;
            
            clearInterval(timer);
            isRunning = false;
            startBtn.disabled = false;
            stopBtn.disabled = true;
            
            // 显示最终选中的学生
            const selectedStudent = displayArea.textContent;
            selectedArea.textContent = `选中学生: ${selectedStudent}`;
            
            // 高亮显示
            displayArea.style.backgroundColor = "#d4edda";
            displayArea.style.color = "#155724";
            displayArea.style.border = "2px solid #c3e6cb";
            
            // 2秒后恢复原样式
            setTimeout(function() {
                displayArea.style.backgroundColor = "#f9f9f9";
                displayArea.style.color = "#2c3e50";
                displayArea.style.border = "2px dashed #ccc";
            }, 2000);
        });
    </script>
</body>
</html>
