<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <title>The Speed Typer</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      text-align: center;
      background-color: #222;
      color: white;
      transition: background-color 0.2s;
    }

    h1 {
      margin-top: 50px;
    }

    #word {
      font-size: 40px;
      margin: 20px;
      font-weight: bold;
    }

    input {
      padding: 10px;
      font-size: 18px;
      border-radius: 5px;
      border: none;
      outline: none;
    }

    #score {
      margin-top: 20px;
      font-size: 20px;
    }

    /* efek benar */
    .correct {
      background-color: green !important;
    }

    /* efek shake */
    .shake {
      animation: shake 0.3s;
    }

    @keyframes shake {
      0% { transform: translateX(0); }
      25% { transform: translateX(-5px); }
      50% { transform: translateX(5px); }
      75% { transform: translateX(-5px); }
      100% { transform: translateX(0); }
    }
  </style>
</head>
<body>

  <h1>⚡ The Speed Typer</h1>
  <div id="word">loading...</div>
  <input type="text" id="input" placeholder="Ketik di sini..." autofocus />
  <div id="score">Skor: 0</div>

  <script>
    const words = [
      "apel", "jeruk", "komputer", "internet", "coding",
      "sekolah", "buku", "meja", "kursi", "keyboard",
      "monitor", "game", "cepat", "belajar", "program"
    ];

    let currentWord = "";
    let score = 0;

    const wordEl = document.getElementById("word");
    const inputEl = document.getElementById("input");
    const scoreEl = document.getElementById("score");

    function getRandomWord() {
      return words[Math.floor(Math.random() * words.length)];
    }

    function setNewWord() {
      currentWord = getRandomWord();
      wordEl.textContent = currentWord;
    }

    inputEl.addEventListener("input", () => {
      if (inputEl.value === currentWord) {
        // benar
        score++;
        scoreEl.textContent = "Skor: " + score;

        document.body.classList.add("correct");
        setTimeout(() => {
          document.body.classList.remove("correct");
        }, 200);

        inputEl.value = "";
        setNewWord();
      }
    });

    inputEl.addEventListener("keyup", (e) => {
      if (e.key === "Enter") {
        if (inputEl.value !== currentWord) {
          // salah
          document.body.classList.add("shake");
          setTimeout(() => {
            document.body.classList.remove("shake");
          }, 300);
        }
      }
    });

    // mulai game
    setNewWord();
  </script>

</body>
</html>
