<!DOCTYPE html>
<html lang="zh-Hant">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>誰是可疑帳號？｜交友軟體模擬遊戲</title>
  <style>
    body {
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
      background-color: #f6f6f6;
      margin: 0;
      padding: 0;
    }
    header {
      background-color: #ff5b5b;
      color: #fff;
      padding: 15px 20px;
      text-align: center;
      font-size: 20px;
      font-weight: bold;
    }
    .container {
      max-width: 400px;
      margin: 30px auto;
      padding: 0 20px;
    }
    .profile-card {
      display: none;
      background: #fff;
      border-radius: 15px;
      box-shadow: 0 2px 10px rgba(0,0,0,0.08);
      overflow: hidden;
      margin-bottom: 30px;
    }
    .profile-photo {
      width: 100%;
      height: 300px;
      object-fit: cover;
    }
    .profile-content {
      padding: 15px;
    }
    .name-age {
      font-size: 20px;
      font-weight: bold;
    }
    .bio {
      font-size: 14px;
      color: #666;
      margin: 10px 0;
    }
    .chatbox {
      background: #f1f1f1;
      padding: 10px 15px;
      font-size: 14px;
      border-radius: 10px;
      margin-bottom: 15px;
    }
    .chatbox p {
      margin: 6px 0;
    }
    .btn {
      width: 48%;
      background-color: #ff5b5b;
      color: #fff;
      border: none;
      padding: 10px;
      font-size: 16px;
      cursor: pointer;
      border-radius: 10px;
      margin: 5px 1%;
    }
    .btn:hover {
      background-color: #e54848;
    }
    .result {
      text-align: center;
      font-size: 16px;
      font-weight: bold;
      margin-top: 20px;
    }
  </style>
</head>
<body>
  <header>誰是可疑帳號？</header>
  <div class="container" id="game">
    <!-- Profiles -->
    <!-- 用陣列 render，透過 JS 控制 -->
  </div>
  <div class="result" id="result"></div>

  <script>
    const profiles = [
      {
        id: 'A',
        name: '阿傑',
        age: 28,
        bio: '我喜歡聽你說故事，也願意陪你熬夜聊天',
        image: 'avatar_a.jpg',
        chat: [
          '妳今天過得好嗎？有沒有想我？',
          '如果我們住在一起就可以天天幫妳準備早餐了 ☕',
          '可以給我一張妳剛睡醒的照片嗎？我會放口袋收藏 ❤️'
        ]
      },
      {
        id: 'B',
        name: 'Mark',
        age: 32,
        bio: '海歸 🌍 | Harvard MBA ✈️ | 愛旅遊、愛賺錢、也想愛妳 😉',
        image: 'avatar_b.jpg',
        chat: [
          'You have such pretty lips... just saying 😏',
          'Can I be honest? You got me hard',
          'We should video chat sometime. I’ll show you mine if you show me yours 😉'
        ]
      },
      {
        id: 'C',
        name: 'Kenny',
        age: 30,
        bio: 'bartender 🍸 | 愛聽慢歌、愛看電影',
        image: 'avatar_c.jpg',
        chat: [
          '上次遇到妳我真的心跳漏了一拍',
          '我有拍妳跳舞的樣子，妳要不要看看？',
          '我們可以開視訊喝一杯，just us two'
        ]
      },
      {
        id: 'D',
        name: 'Leo',
        age: 29,
        bio: 'Fitness Coach 💪 | 練身體也練感情',
        image: 'avatar_d.jpg',
        chat: [
          '妳這樣的體態我可以幫妳調到最完美',
          '有沒有妳穿運動內衣的照片？我可以幫妳分析',
          '我拍一張我現在沒穿衣服的樣子給妳看'
        ]
      },
      {
        id: 'E',
        name: 'James',
        age: 27,
        bio: '寫程式的人也會寫情書 💻💌',
        image: 'avatar_e.jpg',
        chat: [
          '妳喜歡看動漫還是打遊戲？我兩個都可以陪妳',
          '如果妳也喜歡日文，我可以教妳',
          '有空可以一起來圖書館念書嗎？'
        ]
      }
    ];

    const risky = ['A', 'B', 'D'];
    let currentIndex = 0;

    function renderProfile(index) {
      const profile = profiles[index];
      const container = document.getElementById('game');
      container.innerHTML = `
        <div class="profile-card">
          <img src="${profile.image}" alt="${profile.name}" class="profile-photo">
          <div class="profile-content">
            <div class="name-age">${profile.name}, ${profile.age}</div>
            <div class="bio">${profile.bio}</div>
            <div class="chatbox">
              ${profile.chat.map(text => `<p><strong>${profile.name}：</strong> ${text}</p>`).join('')}
            </div>
            <button class="btn" onclick="handleAnswer(true)">可疑</button>
            <button class="btn" onclick="handleAnswer(false)">不可疑</button>
          </div>
        </div>
      `;
    }

    function handleAnswer(isSuspicious) {
      const profile = profiles[currentIndex];
      const isCorrect = isSuspicious === risky.includes(profile.id);
      const resultBox = document.getElementById('result');
      resultBox.innerText = isCorrect ? '✅ 判斷正確！' : '❌ 判斷錯誤';
      currentIndex++;
      if (currentIndex < profiles.length) {
        setTimeout(() => {
          resultBox.innerText = '';
          renderProfile(currentIndex);
        }, 1000);
      } else {
        setTimeout(() => {
          resultBox.innerText = '🎉 遊戲結束，感謝你的判斷！';
          document.getElementById('game').innerHTML = '';
        }, 1500);

      }
    }

    renderProfile(currentIndex);
  </script>
</body>
</html>
