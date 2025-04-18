<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>PPS Test - BEU Insight</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      padding: 20px;
      background-color: #f8f9fa;
    }
    .question {
      margin-top: 20px;
    }
    .btn {
      padding: 10px 20px;
      background-color: #007bff;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }
    .btn:hover {
      background-color: #0056b3;
    }
    #quiz, #result {
      display: none;
    }
  </style>
</head>
<body>
  <h1>PPS Test - BEU Insight</h1>

  <div id="start-screen">
    <h2>Enter Your Details</h2>
    <label>Name: <input type="text" id="name"></label><br><br>
    <label>Branch: <input type="text" id="branch"></label><br><br>
    <button class="btn" onclick="startQuiz()">Start Test</button>
  </div>

  <div id="quiz">
    <div class="question" id="question-box"></div>
    <div id="options"></div>
    <button class="btn" onclick="nextQuestion()">Next</button>
  </div>

  <div id="result">
    <h2>BEU Insight</h2>
    <p id="greeting"></p>
    <p id="score"></p>
    <p id="feedback"></p>
    <p>To attempt full test, follow us on WhatsApp channel: <strong>BEU Insight</strong></p>
  </div>

  <script>
    const questions = [
      {
        q: "Which header file is required for using `sqrt()` in C?",
        options: ["<stdio.h>", "<math.h>", "<stdlib.h>", "<conio.h>"],
        answer: 1
      },
      {
        q: "Which is a valid function returning a pointer to an integer?",
        options: ["int* func() { ... }", "int func*() { ... }", "*int func() { ... }", "int func()* { ... }"],
        answer: 0
      },
      {
        q: "How is a 2D array parameter declared in a function?",
        options: ["int arr[][]", "int arr[][size]", "int *arr[]", "int **arr"],
        answer: 1
      },
      {
        q: "What does `*p = 10;` accomplish?",
        options: ["Assigns 10 to the pointer `p`", "Assigns 10 to the variable pointed to by `p`", "Declares a pointer `p`", "None of the above"],
        answer: 1
      },
      {
        q: "How many recursive calls occur for `fibonacci(5)`?",
        options: ["5", "10", "15", "20"],
        answer: 2
      }
    ];

    let current = 0;
    let score = 0;
    let userName = "";
    let userBranch = "";

    function startQuiz() {
      userName = document.getElementById("name").value.trim();
      userBranch = document.getElementById("branch").value.trim();

      if (!userName || !userBranch) {
        alert("Please enter both name and branch.");
        return;
      }

      document.getElementById("start-screen").style.display = "none";
      document.getElementById("quiz").style.display = "block";
      loadQuestion();
    }

    function loadQuestion() {
      const q = questions[current];
      document.getElementById("question-box").innerHTML = `<h3>Question ${current + 1}: ${q.q}</h3>`;
      const optionsDiv = document.getElementById("options");
      optionsDiv.innerHTML = "";

      q.options.forEach((opt, index) => {
        optionsDiv.innerHTML += `
          <label>
            <input type="radio" name="answer" value="${index}"> ${opt}
          </label><br>`;
      });
    }

    function nextQuestion() {
      const selected = document.querySelector('input[name="answer"]:checked');
      if (!selected) {
        alert("Please select an answer.");
        return;
      }

      const answer = parseInt(selected.value);
      if (answer === questions[current].answer) {
        score += 2;
      }

      current++;
      if (current < questions.length) {
        loadQuestion();
      } else {
        showResult();
      }
    }

    function showResult() {
      document.getElementById("quiz").style.display = "none";
      document.getElementById("result").style.display = "block";

      document.getElementById("greeting").textContent = `Congratulations, ${userName} from ${userBranch}!`;
      document.getElementById("score").textContent = `Your total score is: ${score} / 10`;

      let feedback = "";
      if (score === 10) {
        feedback = "Extraordinary! Keep it up!";
      } else if (score > 5) {
        feedback = "Good! Need a bit more practice.";
      } else {
        feedback = "Better luck next time!";
      }

      document.getElementById("feedback").textContent = feedback;
    }
  </script>
</body>
</html>


