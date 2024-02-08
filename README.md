# Quiz App

This is a simple quiz application built with HTML, CSS, and JavaScript. It presents users with a series of questions and multiple-choice answers. Users can select an answer, and the application will indicate whether it is correct or incorrect. At the end of the quiz, the user's score is displayed.

## Questions

1. Which is the largest Animal in the world

   - [ ] Shark
   - [x] Blue Whale
   - [ ] Elephant
   - [ ] Rhino

2. Which is the Smallest Country in the world

   - [x] Vatican City
   - [ ] Bhutan
   - [ ] Nepal
   - [ ] Shri Lanka

3. Which is the largest Desert in the world

   - [ ] Kalahari
   - [ ] Gobi
   - [ ] Sahara
   - [x] Antarctica

4. Which is the Smallest Continent in the world
   - [ ] Asia
   - [x] Australia
   - [ ] Arctic
   - [ ] Africa

## Logic

```javascript
const questions = [
  {
    question: "Which is the largest Animal in the world",
    answers: [
      { text: "Shark", correct: false },
      { text: "Blue Whale", correct: true },
      { text: "Elephant", correct: false },
      { text: "Rhino", correct: false },
    ],
  },
  {
    question: "Which is the Smallest Country in the world",
    answers: [
      { text: "Vatican City", correct: true },
      { text: "Bhutan", correct: false },
      { text: "Nepal", correct: false },
      { text: "Shri Lanka", correct: false },
    ],
  },
  {
    question: "Which is the largest Desert in the world",
    answers: [
      { text: "Kalahari", correct: false },
      { text: "Gobi", correct: true },
      { text: "Sahara", correct: false },
      { text: "Antarctica", correct: true },
    ],
  },
  {
    question: "Which is the Smallest Continent in the world",
    answers: [
      { text: "Asia", correct: false },
      { text: "Australia", correct: true },
      { text: "Arctic", correct: false },
      { text: "Africa", correct: false },
    ],
  },
];

const questionElement = document.getElementById("question");
const answerButtons = document.getElementById("answer-buttons");
const nextButton = document.getElementById("next-btn");

let currentQuestionIndex = 0;
let score = 0;

function startQuiz() {
  currentQuestionIndex = 0;
  score = 0;
  nextButton.innerHTML = "Next";
  showQuestion();
}

function showQuestion() {
  resetState();
  let currentQuestion = questions[currentQuestionIndex];
  let questionNo = currentQuestionIndex + 1;
  questionElement.innerHTML = questionNo + ". " + currentQuestion.question;

  currentQuestion.answers.forEach((answer) => {
    const button = document.createElement("button");
    button.innerHTML = answer.text;
    button.classList.add("btn");
    answerButtons.appendChild(button);
    if (answer.correct) {
      button.dataset.correct = answer.correct;
    }
    button.addEventListener("click", selectAnswer);
  });
}

function resetState() {
  nextButton.style.display = "none";
  while (answerButtons.firstChild) {
    answerButtons.removeChild(answerButtons.firstChild);
  }
}

function selectAnswer(e) {
  const selectedBtn = e.target;
  const isCorrect = selectedBtn.dataset.correct === "true";
  if (isCorrect) {
    selectedBtn.classList.add("correct");
    score++;
  } else {
    selectedBtn.classList.add("incorrect");
  }
  Array.from(answerButtons.children).forEach((button) => {
    if (button.dataset.correct === "true") {
      button.classList.add("correct");
    }
    button.disabled = true;
  });
  nextButton.style.display = "block";
}

function showScore() {
  resetState();
  questionElement.innerHTML = `You Scored ${score} out of ${questions.length}!`;
  nextButton.innerHTML = "Play Again";
  nextButton.style.display = "block";
}

function handleNextButton() {
  currentQuestionIndex++;
  if (currentQuestionIndex < questions.length) {
    showQuestion();
  } else {
    showScore();
  }
}

nextButton.addEventListener("click", () => {
  if (currentQuestionIndex < questions.length) {
    handleNextButton();
  } else {
    startQuiz();
  }
});

startQuiz();
```

## Usage

1. Open the `index.html` file in your web browser.
2. The quiz will start automatically.
3. Read each question carefully and select the answer you believe is correct.
4. After selecting an answer, click "Next" to proceed to the next question.
5. At the end of the quiz, your score will be displayed.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Contributing

Contributions are welcome! Fork the repository and submit a pull request with your changes.
