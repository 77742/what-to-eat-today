<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>今天吃什么</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: -apple-system, BlinkMacSystemFont, sans-serif;
    }

    body {
      min-height: 100vh;
      background-color: #f7f7f7;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      padding: 24px;
    }

    .container {
      width: 100%;
      max-width: 360px;
      text-align: center;
    }

    h2 {
      font-weight: 400;
      color: #222;
      margin-bottom: 32px;
      letter-spacing: 1px;
    }

    #foodName {
      font-size: 28px;
      font-weight: 500;
      color: #111;
      min-height: 60px;
      margin-bottom: 40px;
    }

    .btn-draw {
      padding: 12px 36px;
      border: 1px solid #222;
      background: transparent;
      border-radius: 999px;
      font-size: 15px;
      cursor: pointer;
      transition: 0.2s;
    }

    .btn-draw:active {
      background: #222;
      color: white;
    }

    .add-area {
      margin-top: 50px;
      width: 100%;
    }

    input {
      width: 75%;
      padding: 10px 14px;
      border: 1px solid #ddd;
      border-radius: 8px;
      outline: none;
      font-size: 14px;
    }

    .btn-add {
      margin-top: 12px;
      padding: 9px 22px;
      background: #222;
      color: white;
      border: none;
      border-radius: 8px;
      cursor: pointer;
    }

    .tip {
      margin-top: 16px;
      font-size: 12px;
      color: #777;
    }
  </style>
</head>

<body>
  <div class="container">
    <h2>今天吃什么</h2>
    <div id="foodName">点击抽取</div>
    <button class="btn-draw" onclick="randomFood()">抽签</button>

    <div class="add-area">
      <input id="inputFood" placeholder="输入菜品，自定义添加">
      <br>
      <button class="btn-add" onclick="addFood()">添加菜品</button>
      <div class="tip">菜品自动保存，刷新不会丢失</div>
    </div>
  </div>

  <script>
    // 读取本地存储，没有就使用默认菜单
    let foodList = JSON.parse(localStorage.getItem("foodMenu")) || [
      "黄焖鸡米饭",
      "麻辣烫",
      "螺蛳粉",
      "猪脚饭",
      "拉面",
      "汉堡",
      "火锅",
      "饺子"
    ];

    // 随机抽取
    function randomFood() {
      let item = foodList[Math.floor(Math.random() * foodList.length)];
      document.getElementById("foodName").innerText = item;
    }

    // 新增菜品并保存
    function addFood() {
      let val = document.getElementById("inputFood").value.trim();
      if (!val) return;
      foodList.push(val);
      localStorage.setItem("foodMenu", JSON.stringify(foodList));
      document.getElementById("inputFood").value = "";
      alert("添加成功！");
    }
  </script>
</body>
</html>
