# Raffle
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

    // 初期抽選
    window.addEventListener('DOMContentLoaded', () => {
      const rand = Math.random() * 1000;  // 0以上100未満の乱数を生成
      randDiv.textContent = `乱数: ${rand.toFixed(2)}`;  // 小数点2位まで表示

      let prize;
      if (rand < 10) {
        prize = "🎉 1等！おめでとう！";
      } else if (rand < 40) {
        prize = "✨ 2等！すばらしい！";
      } else {
        prize = "🎁 3等！感謝の気持ちを込めて！";
      }
      resultDiv.textContent = prize;
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
