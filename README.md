<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8">
  <title>抽選＆交換サイト（乱数表示付き）</title>
  <style>
    body { display: flex; justify-content: center; align-items: center; height: 100vh; background: #f0f8ff; margin: 0; font-family: Arial, sans-serif; }
    .container { text-align: center; background: #fff; padding: 2rem; border-radius: 8px; box-shadow: 0 4px 8px rgba(0,0,0,0.1); }
    .title { font-size: 2rem; margin-bottom: 1rem; }
    .result { font-size: 2rem; color: #0077cc; margin: 1rem 0; }
    .rand { font-size: 1rem; color: #555; }
    .btn { font-size: 1rem; padding: 0.5rem 1rem; margin-top: 1rem; cursor: pointer; }
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

    // 初期抽選
    window.addEventListener('DOMContentLoaded', () => {
      const storedResult = getCookie('lottery_result');
      const storedRand = getCookie('lottery_rand');

      if (storedResult && storedRand) {
        // すでに抽選済みの場合、cookieの内容を表示
        resultDiv.textContent = storedResult;
        randDiv.textContent = `乱数: ${parseFloat(storedRand).toFixed(2)}`;
      } else {
        const rand = Math.random() * 1000;
        randDiv.textContent = `乱数: ${rand.toFixed(2)}`;

        let prize;
        if (rand < 10) {
          prize = "🎉 1等！おめでとう！";
        } else if (rand < 40) {
          prize = "✨ 2等！すばらしい！";
        } else {
          prize = "🎁 3等！感謝の気持ちを込めて！";
        }

        resultDiv.textContent = prize;
        // cookieに保存
        setCookie('lottery_result', prize);
        setCookie('lottery_rand', rand);
      }
    });

    // 交換処理と閉じるボタン表示
    exchangeBtn.addEventListener('click', () => {
      resultDiv.textContent = "✅ 景品を交換しました！";
      exchangeBtn.disabled = true;

      const closeBtn = document.createElement('button');
      closeBtn.textContent = 'サイトを閉じる';
      closeBtn.className = 'btn';
      closeBtn.onclick = () => {
        window.open('', '_self');
        window.close();
        setTimeout(() => {
          window.location.href = 'http://abehiroshi.la.coocan.jp'; // 任意のリダイレクト先
        }, 3000);
      };
      closeContainer.appendChild(closeBtn);
    });
  </script>
</body>
</html>
