<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <title>일본어 단어 퀴즈</title>
  <style>
    body { font-family: Arial, sans-serif; text-align: center; padding: 50px; }
    #question { font-size: 30px; margin: 20px; }
    #result { font-size: 24px; margin: 20px; }
    input, button { font-size: 20px; margin: 10px; padding: 10px; }
    #question-number { font-size: 18px; margin: 10px; }
  </style>
</head>
<body>

<h1>일본어 단어 퀴즈</h1>
<div id="question"></div>
<div id="question-number"></div>
<input type="text" id="answer" placeholder="발음을 입력하세요" autocomplete="off">
<br>
<button onclick="checkAnswer()">정답 확인</button>
<button onclick="resetQuiz()">다시하기</button>
<div id="result"></div>

<script>
const wordList = {
  "대학교": "다이가쿠", "바다": "우미", "산": "야마", "길": "미치",
  "얼굴": "카오", "몸, 신체": "카라다", "학교": "갓코-", "출발": "슈팟츠",
  "인사": "아이사츠", "교실": "쿄-시츠", "우산": "카사", "입구": "이리구치",
  "노래": "우타", "봄": "하루", "여름": "나츠", "가을": "아키", "겨울": "후유",
  "가족": "카조쿠", "은행": "깅코-", "식당": "쇼쿠도-", "공원": "코-엔",
  "날씨": "텐키", "시계": "토케이", "사진": "샤신", "학생": "가쿠세-",
  "아이": "코도모", "어른": "오토나", "하늘": "소라", "도서관": "토쇼칸",
  "색, 빛깔": "이로", "가방": "카방/밧구", "요리": "료-리", "문제": "몬다이",
  "시간": "지칸", "밤": "요루", "낮": "히루", "아침": "아사", "저녁": "유-가타",
  "교통": "코-츠-", "여행": "료코-", "강": "카와", "자기, 자신": "지분",
  "이유": "리유-", "세계": "세카이", "흥미": "쿄-미", "취미": "슈미",
  "안전": "안젠", "결혼": "켓콘", "약": "쿠스리", "전부": "젠부"
};

const koreanWords = Object.keys(wordList);
let currentIndex = 0;
let correctCount = 0;
let answerChecked = false;

function showQuestion() {
  if (currentIndex < koreanWords.length) {
    document.getElementById('question').innerText = koreanWords[currentIndex];
    document.getElementById('question-number').innerText = `${currentIndex + 1} / ${koreanWords.length}`;
    document.getElementById('answer').value = '';
    document.getElementById('result').innerText = '';
    answerChecked = false;
  } else {
    showResult();
  }
}

function checkAnswer() {
  if (currentIndex < koreanWords.length && !answerChecked) {
    const userAnswer = document.getElementById('answer').value.trim();
    const correctPronunciation = wordList[koreanWords[currentIndex]];
    if (userAnswer === correctPronunciation) {
      document.getElementById('result').innerText = '정답입니다!';
      document.getElementById('result').style.color = 'blue';
      correctCount++;
    } else {
      document.getElementById('result').innerText = `틀렸습니다. 정답은 '${correctPronunciation}'입니다.`;
      document.getElementById('result').style.color = 'red';
    }
    answerChecked = true;
    setTimeout(nextQuestion, 2000); // 2초 후 다음 문제
  }
}

function nextQuestion() {
  if (answerChecked) {
    currentIndex++;
    showQuestion();
  }
}

function resetQuiz() {
  currentIndex = 0;
  correctCount = 0;
  answerChecked = false;
  showQuestion();
  document.getElementById('result').innerText = '';
}

function showResult() {
  alert(`퀴즈 종료!\n맞춘 개수: ${correctCount} / ${koreanWords.length}\n점수: ${correctCount}점`);
  resetQuiz();
}

// 시작할 때 첫 문제 보여주기
showQuestion();
</script>

</body>
</html>
