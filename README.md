# quiz-game
لعبة الغاز ومسابقات 
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Quiz Master</title>
    <style>
        body { font-family: Arial, sans-serif; background-color: #f4f4f4; padding: 20px; }
        h1 { text-align: center; }
        .quiz-container { max-width: 600px; margin: auto; border: 1px solid #ccc; background: #fff; padding: 20px; border-radius: 8px; }
        .question { font-size: 1.2em; margin-bottom: 15px; }
        .options { list-style-type: none; padding: 0; }
        .options li { margin: 10px 0; }
        button { padding: 10px 15px; background-color: #28a745; color: white; border: none; border-radius: 4px; cursor: pointer; }
        button:hover { background-color: #218838; }
        #result { margin-top: 20px; font-size: 1.5em; }
    </style>
</head>
<body>
    <div class="quiz-container">
        <h1>Quiz Master</h1>
        <div id="quiz"></div>
        <button id="next">Next Question</button>
        <div id="result"></div>
    </div>
    <script>
        const quizData = [
            { question: 'What is the capital of France?', a: 'Berlin', b: 'Madrid', c: 'Paris', d: 'Lisbon', correct: 'c' },
            { question: 'Which planet is known as the Red Planet?', a: 'Earth', b: 'Mars', c: 'Jupiter', d: 'Saturn', correct: 'b' },
            { question: 'What is the tallest mountain in the world?', a: 'K2', b: 'Mount Everest', c: 'Kangchenjunga', d: 'Lhotse', correct: 'b' },
            { question: 'Who wrote the play Hamlet?', a: 'Charles Dickens', b: 'William Shakespeare', c: 'J.K. Rowling', d: 'Mark Twain', correct: 'b' },
            { question: 'What is the largest ocean on Earth?', a: 'Indian Ocean', b: 'Atlantic Ocean', c: 'Arctic Ocean', d: 'Pacific Ocean', correct: 'd' }
        ];

        let currentQuestion = 0;
        let score = 0;

        function loadQuiz() {
            if (currentQuestion < quizData.length) {
                const currentQuizData = quizData[currentQuestion];
                const quizContainer = document.getElementById('quiz');
                quizContainer.innerHTML = `
                    <div class="question">${currentQuizData.question}</div>
                    <ul class="options">
                        <li><input type="radio" name="answer" value="a"> ${currentQuizData.a}</li>
                        <li><input type="radio" name="answer" value="b"> ${currentQuizData.b}</li>
                        <li><input type="radio" name="answer" value="c"> ${currentQuizData.c}</li>
                        <li><input type="radio" name="answer" value="d"> ${currentQuizData.d}</li>
                    </ul>
                `;
            } else {
                showResult();
            }
        }

        function showResult() {
            const resultContainer = document.getElementById('result');
            resultContainer.innerHTML = `You scored ${score} out of ${quizData.length}`;
            document.getElementById('quiz').style.display = 'none';
            document.getElementById('next').style.display = 'none';
        }

        document.getElementById('next').addEventListener('click', () => {
            const answerEls = document.querySelectorAll('input[name="answer"]');
            let answer;
            answerEls.forEach((answerEl) => {
                if (answerEl.checked) {
                    answer = answerEl.value;
                }
            });

            if (answer) {
                if (answer === quizData[currentQuestion].correct) {
                    score++;
                }
                currentQuestion++;
                loadQuiz();
            }
        });

        loadQuiz();
    </script>
</body>
</html>
