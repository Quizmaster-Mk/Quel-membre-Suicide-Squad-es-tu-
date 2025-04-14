<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Quel membre de la Suicide Squad es-tu ?</title>
  <style>
    body {
      font-family: 'Courier New', monospace;
      background-color: #0b0b0b; /* Noir profond */
      color: #fff;
      margin: 0;
      padding: 20px;
      text-align: center;
    }

    h1 {
      color: #ff0080; /* Rose néon */
      text-shadow: 2px 2px 5px #00ffcc; /* Vert acide fluo */
      font-size: 40px;
      margin-bottom: 20px;
    }

    img.logo {
      max-width: 200px;
      margin-bottom: 20px;
      border-radius: 20px;
      box-shadow: 0 0 15px #ff0080;
    }

    .question {
      margin: 20px 0;
      background-color: #1a1a1a;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 0 10px rgba(0, 255, 204, 0.7);
    }

    .options button {
      background-color: #ff0080;
      color: #fff;
      padding: 10px 20px;
      border: none;
      margin: 5px;
      font-size: 18px;
      cursor: pointer;
      border-radius: 5px;
      transition: all 0.3s ease;
    }

    .options button:hover {
      background-color: #00ffcc;
      transform: rotate(-2deg) scale(1.1);
    }

    .result {
      background-color: #1a1a1a;
      padding: 20px;
      border-radius: 10px;
      margin-top: 20px;
      display: none;
      box-shadow: 0 0 10px rgba(255, 0, 128, 0.7);
    }

    .score {
      font-size: 18px;
      margin-top: 10px;
      color: #00ffcc;
    }
  </style>
</head>
<body>
  <img class="logo" src="https://zupimages.net/up/25/16/kj9u.jpg" alt="Logo Suicide Squad">
  <h1>Quel membre de la Suicide Squad es-tu ?</h1>

  <div id="quiz-container">
    <div class="question" id="question-container">
      <h2 id="question-text"></h2>
      <div class="options" id="options-container"></div>
    </div>
  </div>

  <div class="result" id="result-container">
    <h2>Tu es...</h2>
    <p id="result-text"></p>
    <p class="score">Ouais, c'est toi ! Et ce n'est pas rien !</p>
    <button onclick="startQuiz()">Rejouer et exploser les scores !</button>
  </div>

  <script>
    const questions = [
      { question: "Quelle est ta manière de résoudre les conflits ?", options: ["Un gros marteau dans la tronche", "Une balle bien placée", "Avec style et sarcasme", "Je négocie... et trahis ensuite"], result: [0, 1, 2, 3] },
      { question: "Ton arme préférée ?", options: ["Une batte cloutée rose bonbon", "Des flingues custom", "Un crocodile affamé", "Mon cerveau tordu"], result: [0, 1, 2, 3] },
      { question: "Ton hobby quand t'es pas en mission suicide ?", options: ["Faire exploser des trucs", "Tirer dans des trucs", "Manger des trucs", "Rire dans le vide"], result: [0, 1, 2, 3] },
      { question: "Comment tu gères une équipe ?", options: ["Je la mène à la ruine avec panache", "Je m'en fous, je bosse solo", "Je la mange ?", "Je les manipule pour qu’ils fassent tout"] , result: [0, 1, 2, 3] },
      { question: "Ta devise dans la vie ?", options: ["YOLO avec des explosions", "Tirer d’abord, réfléchir après", "Plus c’est crade, plus c’est bon", "Pourquoi faire simple quand on peut tout détruire ?"], result: [0, 1, 2, 3] }
    ];

    const characters = [
      { name: "Harley Quinn", description: "Folle furieuse et irrésistible, tu mets le chaos partout où tu passes. Tes ennemis ? Trop occupés à se marrer... ou à saigner." },
      { name: "Deadshot", description: "Sniper de l’extrême, tu rates jamais ta cible. Sérieux mais stylé, tu restes pro même dans un cirque d’explosifs." },
      { name: "Killer Croc", description: "Mi-homme mi-saurien, 100% effrayant. Tu préfères les égouts et les bastons à mains nues. Rawrrr." },
      { name: "The Joker (caméo surprise)", description: "Personne t’attendait là, mais bim ! Te voilà. Imprévisible, manipulateur, et foutrement théâtral." }
    ];

    let currentQuestion = 0;
    let userAnswers = [];

    function startQuiz() {
      currentQuestion = 0;
      userAnswers = [];
      document.getElementById('result-container').style.display = 'none';
      document.getElementById('quiz-container').style.display = 'block';
      showQuestion();
    }

    function showQuestion() {
      const question = questions[currentQuestion];
      document.getElementById('question-text').innerText = question.question;

      const optionsContainer = document.getElementById('options-container');
      optionsContainer.innerHTML = '';

      question.options.forEach((option, index) => {
        const button = document.createElement('button');
        button.innerText = option;
        button.onclick = () => {
          userAnswers.push(question.result[index]);
          currentQuestion++;
          if (currentQuestion < questions.length) {
            showQuestion();
          } else {
            showResult();
          }
        };
        optionsContainer.appendChild(button);
      });
    }

    function showResult() {
      const resultIndex = userAnswers.reduce((a, b) => a + b, 0) % characters.length;
      const result = characters[resultIndex];

      document.getElementById('result-text').innerText = `${result.name} - ${result.description}`;
      document.getElementById('quiz-container').style.display = 'none';
      document.getElementById('result-container').style.display = 'block';
    }

    startQuiz();
  </script>
</body>
</html>
