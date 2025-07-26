# abcd
<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>수업 타이머 + 활동 안내</title>
    <style>
      body {
        font-family: sans-serif;
        text-align: center;
        padding: 2rem;
        max-width: 600px;
        margin: auto;
      }
      #activity {
        font-size: 1.5rem;
        margin-bottom: 1rem;
      }
      #timer {
        font-size: 2rem;
        margin-bottom: 1rem;
      }
      img {
        max-width: 100%;
        border-radius: 10px;
        margin-top: 1rem;
      }
    </style>
  </head>
  <body>
    <h1>수업 타이머 + 활동 안내</h1>
    <div id="activity"></div>
    <div id="timer"></div>
    <img id="activityImage" src="" alt="" style="display: none" />

    <script>
      const activities = [
        {
          title: "마인드맵 그리기",
          duration: 60, // 초 단위
          image: "https://via.placeholder.com/400x200?text=마인드맵"
        },
        {
          title: "조별 토의",
          duration: 90,
          image: "https://via.placeholder.com/400x200?text=조별+토의"
        },
        {
          title: "소감 나누기",
          duration: 60,
          image: "https://via.placeholder.com/400x200?text=소감+나누기"
        }
      ];

      let current = 0;
      let timer;

      function startActivity(index) {
        if (index >= activities.length) {
          document.getElementById("activity").textContent = "수업이 종료되었습니다.";
          document.getElementById("timer").textContent = "";
          document.getElementById("activityImage").style.display = "none";
          return;
        }

        const act = activities[index];
        let remaining = act.duration;

        document.getElementById("activity").textContent = act.title;
        document.getElementById("activityImage").src = act.image;
        document.getElementById("activityImage").style.display = "block";

        document.getElementById("timer").textContent = formatTime(remaining);

        timer = setInterval(() => {
          remaining--;
          document.getElementById("timer").textContent = formatTime(remaining);
          if (remaining <= 0) {
            clearInterval(timer);
            startActivity(index + 1);
          }
        }, 1000);
      }

      function formatTime(seconds) {
        const min = Math.floor(seconds / 60);
        const sec = seconds % 60;
        return `${min}:${sec.toString().padStart(2, '0')}`;
      }

      // 시작
      startActivity(current);
    </script>
  </body>
</html>
