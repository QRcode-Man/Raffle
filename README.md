https://github.com/user-attachments/assets/ee907ea9-5f50-44fd-beba-733ef3682942
https://github.com/user-attachments/assets/fb35cd47-d2dd-425f-a756-7dbd82bebce1
https://github.com/user-attachments/assets/7db83d51-117b-48bc-a8cb-5bfc451852f4
https://github.com/user-attachments/assets/3c46d8b3-2002-471b-b8c1-8ceaee0e830d
https://github.com/user-attachments/assets/e1056d0b-29c2-4441-9b54-8acc88a43e06

<html lang="ja">
<head>
  <meta charset="UTF-8">
  <title>抽選＆交換サイト（乱数表示付き）</title>
  <style>
    body {
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      background: #f0f8ff;
      margin: 0;
      font-family: Arial, sans-serif;
    }
    .container {
      text-align: center;
      background: #fff;
      padding: 2rem;
      border-radius: 8px;
      box-shadow: 0 4px 8px rgba(0,0,0,0.1);
    }
    .title {
      font-size: 2rem;
      margin-bottom: 1rem;
    }
    .result {
      font-size: 2rem;
      color: #0077cc;
      margin: 1rem 0;
    }
    .rand {
      font-size: 1rem;
      color: #555;
    }
    .btn {
      font-size: 1rem;
      padding: 0.5rem 1rem;
      margin-top: 1rem;
      cursor: pointer;
    }
  </style>
</head>
<body>
  <div class="container">
    <div class="title">抽選結果はこちら！</div>
    <div class="result" id="result">...</div>
    <div class="rand" id="rand">乱数: --</div>
    <button class="btn" id="exchangeBtn">交換する</button>
    <div id="closeContainer"></div>
  </div>

  <script>
    const resultDiv = document.getElementById('result');
    const randDiv = document.getElementById('rand');
    const exchangeBtn = document.getElementById('exchangeBtn');
    const closeContainer = document.getElementById('closeContainer');

    // Cookieを設定する関数（有効期限1日）
    function setCookie(name, value, days = 1) {
      const date = new Date();
      date.setTime(date.getTime() + (days*24*60*60*1000));
      document.cookie = `${name}=${encodeURIComponent(value)};expires=${date.toUTCString()};path=/`;
    }

    // Cookieを取得する関数
    function getCookie(name) {
      const match = document.cookie.match(new RegExp('(^| )' + name + '=([^;]+)'));
      return match ? decodeURIComponent(match[2]) : null;
    }

    // 「サイトを閉じる」ボタンを作成する関数
    function createCloseButton() {
      const closeBtn = document.createElement('button');
      closeBtn.textContent = '3秒後に自動で閉じます（またはクリック）';
      closeBtn.className = 'btn';
      closeBtn.onclick = () => {
        window.location.href = 'http://abehiroshi.la.coocan.jp'; // 任意のリダイレクト先
      };
      closeContainer.appendChild(closeBtn);

      setTimeout(() => {
        window.location.href = 'http://abehiroshi.la.coocan.jp';
      }, 3000);
    }

    // 初期処理
    window.addEventListener('DOMContentLoaded', () => {
      const storedResult = getCookie('lottery_result');
      const storedRand = getCookie('lottery_rand');
      const exchanged = getCookie('exchanged');

      // 抽選結果がすでに存在する場合
      if (storedResult && storedRand) {
        resultDiv.textContent = storedResult;
        randDiv.textContent = `乱数: ${parseFloat(storedRand).toFixed(2)}`;

        if (exchanged === 'true') {
          resultDiv.textContent = "✅ 景品を交換しました！";
          exchangeBtn.disabled = true;
          createCloseButton();
        }
      } else {
        // 新規抽選処理
        const rand = Math.random() * 1000;
        randDiv.textContent = `乱数: ${rand.toFixed(2)}`;

        let prize;
        if (rand < 10) {
          

    Uploading 1等.mp4…

prize = "🎉 1等！おめでとう！";
        } else if (rand < 40) {
          prize = "✨ 2等！すばらしい！";

https://github.com/user-attachments/assets/60a5991b-83f6-42cd-9317-a5007cbe0d4b


        } else if (rand < 80) {

https://github.com/user-attachments/assets/344af27a-7ff4-414b-8493-bbe035f5b947


          prize = "🎁 3等！感謝の気持ちを込めて！";
        } else if (rand < 150) {

https://github.com/user-attachments/assets/d85fc8c9-8472-4a67-b82e-626f7c1b2393


          prize = "4等！それなりに";
        } else {

https://github.com/user-attachments/assets/ec32af33-1ef9-4a4d-b1ca-33815fa4aa8c


          prize = "残念！はずれ～";
        }

        resultDiv.textContent = prize;
        setCookie('lottery_result', prize);
        setCookie('lottery_rand', rand);
      }
    });

    // 交換処理
    exchangeBtn.addEventListener('click', () => {
      resultDiv.textContent = "✅ 景品を交換しました！";
      exchangeBtn.disabled = true;
      setCookie('exchanged', 'true');
      createCloseButton();
    });
  </script>
