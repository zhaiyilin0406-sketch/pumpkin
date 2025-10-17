# thustudent
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <title>支付确认</title>
    <style>
        body {
            margin: 0;
            padding: 50px;
            font-family: "微软雅黑", sans-serif;
            background-color: #f5f5f5;
            text-align: center;
            display: flex;
            flex-direction: column;
            align-items: center;
        }
        .confirm-box {
            background: white;
            padding: 60px 30px;
            border-radius: 10px;
            max-width: 500px;
            margin: 20px auto;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }
        .confirm-text {
            font-size: 22px;
            color: #333;
            line-height: 1.8;
            margin-top: 30px;
        }
        .key-info {
            font-weight: bold;
            color: #2c3e50;
        }
        /* 红色提示文字样式：初始隐藏 */
        .question-text {
            color: #e74c3c; /* 标准红色 */
            font-size: 18px;
            margin-top: 20px;
            display: none; /* 初始不显示，后续通过JS控制 */
        }
        .loader {
            width: 40px;
            height: 40px;
            border: 4px solid #f3f3f3;
            border-top: 4px solid #2c3e50;
            border-radius: 50%;
            animation: spin 1s linear infinite;
            display: inline-block;
        }
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
        .success-icon {
            width: 60px;
            height: 60px;
            border: 4px solid #2ecc71;
            border-radius: 50%;
            display: none;
            align-items: center;
            justify-content: center;
            margin: 0 auto;
        }
        .success-icon::after {
            content: '';
            width: 20px;
            height: 35px;
            border: 3px solid #2ecc71;
            border-top: none;
            border-left: none;
            transform: rotate(45deg);
        }
    </style>
</head>
<body>
    <div class="loader" id="loader"></div>
    <div class="success-icon" id="successIcon"></div>
    <div class="confirm-box">
        <p class="confirm-text">
            <span class="key-info">申浩正先生</span>已支付
            <span class="key-info" id="amount">0</span>元，<br>
            确认为本人操作，稍后自动扣费
        </p>
        <!-- 红色提示文字：初始隐藏 -->
        <p class="question-text" id="questionText">如有疑问，请回复【TD】，我们将为您核实</p>
    </div>

    <script>
        const amountElem = document.getElementById('amount');
        const loader = document.getElementById('loader');
        const successIcon = document.getElementById('successIcon');
        const questionText = document.getElementById('questionText'); // 红色文字元素
        let currentAmount = 0;
        const targetAmount = 1000;
        const speed = 10; // 快速跳动的速度参数

        const updateAmount = () => {
            if (currentAmount < targetAmount) {
                currentAmount += Math.ceil(Math.random() * 5);
                if (currentAmount > targetAmount) currentAmount = targetAmount;
                amountElem.textContent = currentAmount;
                setTimeout(updateAmount, speed);
            } else {
                // 所有动态效果完成后，显示成功图标+红色提示文字
                loader.style.display = 'none';
                successIcon.style.display = 'flex';
                questionText.style.display = 'block'; // 显示红色文字
            }
        };

        window.onload = updateAmount;
    </script>
</body>
</html>
