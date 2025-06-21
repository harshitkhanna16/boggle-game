<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>BOGGLE GAME</title>
  <style>
    :root {
      --primary-color: #1d3557;
      --secondary-color: #457b9d;
      --accent-color: #e63946;
      --success-color: #2a9d8f;
      --warning-color: #e76f51;
      --text-light: #f1faee;
      --text-secondary: #a8dadc;
      --background-dark: #264653;
    }

    body {
      font-family: Arial, sans-serif;
      background: var(--primary-color);
      color: var(--text-light);
      display: flex;
      justify-content: center;
      align-items: flex-start;
      min-height: 100vh;
      margin: 0;
      padding: 20px;
      box-sizing: border-box;
    }

    .game-wrapper {
      display: flex;
      justify-content: center;
      align-items: flex-start;
      gap: 40px;
      flex-wrap: wrap;
    }

    .game-container {
      text-align: center;
      width: 100%;
      max-width: 400px;
      background: var(--secondary-color);
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 8px 20px rgba(0, 0, 0, 0.4);
    }

    .small-label {
      font-size: 12px;
      color: var(--text-secondary);
      margin-bottom: 5px;
    }

    h1 { 
      margin-bottom: 10px; 
      color: var(--text-light);
    }

    .info {
      display: flex;
      justify-content: space-between;
      padding: 0 10px;
      font-size: 18px;
      font-weight: bold;
    }

    .grid {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 10px;
      margin: 20px 0;
    }

    .tile {
      background: var(--text-light);
      color: var(--primary-color);
      font-size: 24px;
      padding: 20px;
      border-radius: 6px;
      cursor: pointer;
      user-select: none;
      transition: background 0.2s, transform 0.1s;
      text-align: center;
    }

    .tile:hover {
      transform: scale(1.05);
      background: var(--text-secondary);
    }

    .tile.selected {
      background: var(--accent-color);
      color: white;
      transform: scale(1.1);
    }

    .tile.hint {
      background: #ffbe0b !important;
      color: #000;
      font-weight: bold;
    }

    .controls {
      display: flex;
      gap: 10px;
      margin-bottom: 10px;
      padding: 0 10px;
    }

    .controls input {
      flex: 1;
      padding: 12px;
      font-size: 16px;
      border: none;
      border-radius: 4px;
    }

    .controls button {
      padding: 12px 20px;
      font-size: 16px;
      background: var(--success-color);
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      transition: background 0.3s ease;
    }

    .controls button:hover {
      background: #21867a;
    }

    .hint-restart {
      display: flex;
      justify-content: space-between;
      gap: 10px;
      margin: 10px;
      padding: 0 10px;
    }

    .hint-restart button {
      flex: 1;
      padding: 12px;
      font-size: 16px;
      font-weight: bold;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      transition: background 0.3s ease;
    }

    #hintBtn {
      background-color: #2ecc71;
    }

    #hintBtn:hover:not(:disabled) {
      background-color: #27ae60;
    }

    #hintBtn:disabled {
      background-color: #a5d6a7;
      cursor: not-allowed;
    }

    #restartBtn {
      background-color: var(--warning-color);
    }

    #restartBtn:hover {
      background-color: #c0392b;
    }

    .word-list {
      text-align: left;
      margin-top: 15px;
      padding: 0 10px;
    }

    .word-list h3 { 
      margin-bottom: 5px; 
      color: var(--text-light);
    }

    .word-list ul {
      list-style: none;
      padding: 0;
      max-height: 120px;
      overflow-y: auto;
    }

    .word-list li {
      background: rgba(255, 255, 255, 0.1);
      padding: 8px 10px;
      margin-bottom: 4px;
      border-radius: 4px;
      font-size: 14px;
      line-height: 1.4;
    }

    .leaderboard-container {
      width: 250px;
      background: var(--background-dark);
      padding: 20px;
      border-radius: 10px;
      color: var(--text-light);
      font-family: Arial, sans-serif;
      max-height: 500px;
      overflow-y: auto;
      box-shadow: 0 8px 20px rgba(0, 0, 0, 0.4);
    }

    .leaderboard-container h3 {
      margin-top: 0;
      margin-bottom: 15px;
      color: var(--text-light);
      text-align: center;
    }

    .leaderboard-container ol {
      padding-left: 20px;
      margin: 0;
    }

    .leaderboard-container li {
      background: rgba(255, 255, 255, 0.1);
      padding: 10px 15px;
      margin-bottom: 8px;
      border-radius: 6px;
      font-weight: bold;
    }

    .leaderboard-container li:first-child {
      background: linear-gradient(45deg, #ffd700, #ffed4e);
      color: #333;
    }

    .leaderboard-container li:nth-child(2) {
      background: linear-gradient(45deg, #c0c0c0, #e8e8e8);
      color: #333;
    }

    .leaderboard-container li:nth-child(3) {
      background: linear-gradient(45deg, #cd7f32, #deb887);
      color: #333;
    }

    @media (max-width: 768px) {
      .game-wrapper {
        flex-direction: column;
        align-items: center;
      }
      
      .leaderboard-container {
        width: 100%;
        max-width: 400px;
      }
    }
  </style>
</head>
<body>
  <div class="game-wrapper">
    <div class="game-container">
      <div class="small-label">DAA-IV-T137</div>
      <h1>BOGGLE GAME</h1>
      <div class="info">
        <span>Score: <span id="score">0</span></span>
        <span>Time: <span id="timer">120</span>s</span>
      </div>
      <div class="grid" id="grid"></div>
      <div class="controls">
        <input type="text" id="currentWord" placeholder="Selected word" readonly />
        <button id="submitBtn">Submit</button>
      </div>
      <div class="hint-restart">
        <button id="hintBtn">Hint (1 left)</button>
        <button id="restartBtn">Restart</button>
      </div>
      <div class="word-list">
        <h3>Found Words:</h3>
        <ul id="wordList"></ul>
      </div>
    </div>
    
    <div class="leaderboard-container">
      <h3>🏆 Leaderboard - Top 5</h3>
      <ol id="leaderboardList"></ol>
    </div>
  </div>

  <script>
    class BoggleGame {
      constructor() {
        // Game constants
        this.GRID_SIZE = 4;
        this.GAME_DURATION = 120;
        this.WORD_SCORE = 10;
        this.EMBED_WORDS = ["CAT", "DOG", "SUN", "FUN"];
        
        // Game state
        this.foundWords = new Set();
        this.hintUsed = false;
        this.score = 0;
        this.timer = this.GAME_DURATION;
        this.interval = null;
        this.gameEnded = false;
        this.selectedTiles = [];
        this.isDragging = false;
        this.currentPlayerName = '';
        
        // DOM elements
        this.gridElement = document.getElementById("grid");
        this.scoreElement = document.getElementById("score");
        this.timerElement = document.getElementById("timer");
        this.currentWordInput = document.getElementById("currentWord");
        this.wordListElement = document.getElementById("wordList");
        this.submitBtn = document.getElementById("submitBtn");
        this.hintBtn = document.getElementById("hintBtn");
        this.restartBtn = document.getElementById("restartBtn");
        this.leaderboardList = document.getElementById("leaderboardList");
        
        // Leaderboard
        this.leaderboard = this.loadLeaderboard();
        
        this.init();
      }
      
      init() {
        this.setupEventListeners();
        this.updateLeaderboard();
        this.promptPlayerName();
        this.generateSmartGrid();
        this.startTimer();
      }
      
      setupEventListeners() {
        this.submitBtn.addEventListener("click", () => {
          if (!this.gameEnded) this.submitWord();
        });
        
        this.hintBtn.addEventListener("click", () => this.showHint());
        this.restartBtn.addEventListener("click", () => this.restart());
        
        document.addEventListener("mouseup", () => {
          if (!this.gameEnded && this.isDragging) {
            this.isDragging = false;
            this.submitWord();
          }
        });
      }
      
      promptPlayerName() {
        let playerName = prompt('Enter your name to start the game:', 'Player');
        this.currentPlayerName = playerName ? playerName.trim() : 'Player';
      }
      
      generateSmartGrid() {
        const grid = Array(this.GRID_SIZE * this.GRID_SIZE).fill("");

        const canPlace = (word, row, col, dir) => {
          const dx = { h: 0, v: 1, d: 1 }[dir];
          const dy = { h: 1, v: 0, d: 1 }[dir];
          for (let i = 0; i < word.length; i++) {
            let x = row + dx * i, y = col + dy * i;
            if (x >= this.GRID_SIZE || y >= this.GRID_SIZE || grid[x * this.GRID_SIZE + y] !== "") {
              return false;
            }
          }
          return true;
        };

        const placeWord = (word) => {
          let attempts = 0;
          const maxAttempts = 100;
          
          while (attempts < maxAttempts) {
            let row = Math.floor(Math.random() * this.GRID_SIZE);
            let col = Math.floor(Math.random() * this.GRID_SIZE);
            let dir = ["h", "v", "d"][Math.floor(Math.random() * 3)];
            
            if (canPlace(word, row, col, dir)) {
              for (let i = 0; i < word.length; i++) {
                let x = row + (dir === "v" || dir === "d" ? i : 0);
                let y = col + (dir === "h" || dir === "d" ? i : 0);
                grid[x * this.GRID_SIZE + y] = word[i];
              }
              return true;
            }
            attempts++;
          }
          return false;
        };

        // Place embedded words
        this.EMBED_WORDS.forEach(word => placeWord(word));

        // Fill empty spaces with random letters
        const letters = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
        grid.forEach((v, i) => {
          if (!v) grid[i] = letters[Math.floor(Math.random() * letters.length)];
        });

        // Create grid UI
        this.gridElement.innerHTML = "";
        grid.forEach((char, i) => {
          const tile = document.createElement("div");
          tile.className = "tile";
          tile.textContent = char;
          tile.dataset.index = i;
          
          tile.addEventListener("mousedown", () => {
            if (!this.gameEnded) this.startSelect(tile);
          });
          
          tile.addEventListener("mouseenter", () => {
            if (this.isDragging && !this.gameEnded) this.addTile(tile);
          });
          
          this.gridElement.appendChild(tile);
        });
      }

      startSelect(tile) {
        this.isDragging = true;
        this.clearHint();
        this.clearSelection();
        this.addTile(tile);
      }

      addTile(tile) {
        if (!tile.classList.contains("selected")) {
          tile.classList.add("selected");
          this.selectedTiles.push(tile.textContent);
          this.currentWordInput.value = this.selectedTiles.join("");
        }
      }

      clearSelection() {
        document.querySelectorAll(".tile.selected").forEach(t => t.classList.remove("selected"));
        this.selectedTiles = [];
        this.currentWordInput.value = "";
      }

      async submitWord() {
        const word = this.currentWordInput.value.toUpperCase();
        
        if (word.length < 3) {
          this.clearSelection();
          return;
        }
        
        if (this.foundWords.has(word)) {
          alert(`"${word}" has already been found!`);
          this.clearSelection();
          return;
        }

        try {
          const response = await fetch(`https://api.dictionaryapi.dev/api/v2/entries/en/${word.toLowerCase()}`);
          
          if (response.ok) {
            const data = await response.json();
            
            if (Array.isArray(data) && data[0]?.meanings?.length > 0) {
              this.foundWords.add(word);
              this.score += this.WORD_SCORE;
              this.scoreElement.textContent = this.score;

              let meaning = "No definition available";
              const definitions = data[0].meanings[0].definitions;
              if (definitions && definitions.length > 0) {
                meaning = definitions[0].definition;
                // Limit meaning length for display
                if (meaning.length > 100) {
                  meaning = meaning.substring(0, 97) + "...";
                }
              }

              const li = document.createElement("li");
              li.innerHTML = `<strong>${word}</strong>: ${meaning}`;
              this.wordListElement.appendChild(li);
              
              // Scroll to bottom of word list
              this.wordListElement.scrollTop = this.wordListElement.scrollHeight;

              // Check if all embedded words are found
              if (this.EMBED_WORDS.every(w => this.foundWords.has(w))) {
                this.hintBtn.disabled = true;
              }
            } else {
              alert(`"${word}" is not a valid English word.`);
            }
          } else {
            alert(`"${word}" is not a valid English word.`);
          }
        } catch (error) {
          console.error('Dictionary API error:', error);
          alert("Error checking word validity. Please try again.");
        }

        this.clearSelection();
      }

      startTimer() {
        clearInterval(this.interval);
        this.interval = setInterval(() => {
          this.timer--;
          this.timerElement.textContent = this.timer;
          if (this.timer <= 0) {
            this.endGame();
          }
        }, 1000);
      }

      endGame() {
        this.gameEnded = true;
        clearInterval(this.interval);
        
        // Disable controls
        this.submitBtn.disabled = true;
        this.hintBtn.disabled = true;
        
        // Disable grid interactions
        document.querySelectorAll(".tile").forEach(tile => {
          tile.style.pointerEvents = "none";
          tile.style.cursor = "default";
        });
        
        this.gridElement.style.opacity = 0.5;

        // Update leaderboard
        this.updateLeaderboardWithScore(this.currentPlayerName, this.score);
        
        alert(`Time's up! Final Score: ${this.score}\nWords found: ${this.foundWords.size}`);
      }

      showHint() {
        if (this.hintUsed || this.gameEnded) return;

        const tiles = document.querySelectorAll(".tile");
        const grid = Array.from({ length: this.GRID_SIZE }, (_, i) =>
          Array.from({ length: this.GRID_SIZE }, (_, j) => 
            tiles[i * this.GRID_SIZE + j].textContent
          )
        );

        for (let word of this.EMBED_WORDS) {
          if (!this.foundWords.has(word)) {
            const path = this.dfsHighlight(word, grid);
            if (path) {
              path.forEach(([i, j]) => {
                tiles[i * this.GRID_SIZE + j].classList.add("hint");
              });
              this.hintUsed = true;
              this.hintBtn.disabled = true;
              this.hintBtn.textContent = "Hint (0 left)";
              return;
            }
          }
        }

        this.hintBtn.disabled = true;
        alert("No hints available.");
      }

      dfsHighlight(word, grid) {
        const visited = Array(this.GRID_SIZE).fill().map(() => Array(this.GRID_SIZE).fill(false));
        const path = [];
        const directions = [[-1,-1],[0,-1],[1,-1],[-1,0],[1,0],[-1,1],[0,1],[1,1]];

        const dfs = (i, j, idx) => {
          if (idx === word.length) return true;
          if (i < 0 || i >= this.GRID_SIZE || j < 0 || j >= this.GRID_SIZE || 
              visited[i][j] || grid[i][j] !== word[idx]) {
            return false;
          }

          visited[i][j] = true;
          path.push([i, j]);

          for (let [dx, dy] of directions) {
            if (dfs(i + dx, j + dy, idx + 1)) return true;
          }

          visited[i][j] = false;
          path.pop();
          return false;
        };

        for (let i = 0; i < this.GRID_SIZE; i++) {
          for (let j = 0; j < this.GRID_SIZE; j++) {
            if (dfs(i, j, 0)) return [...path];
            path.length = 0;
          }
        }
        return null;
      }

      clearHint() {
        document.querySelectorAll(".tile.hint").forEach(t => t.classList.remove("hint"));
      }

      loadLeaderboard() {
        try {
          return JSON.parse(localStorage.getItem('boggleLeaderboard') || '[]');
        } catch (error) {
          console.error('Error loading leaderboard:', error);
          return [];
        }
      }

      saveLeaderboard() {
        try {
          localStorage.setItem('boggleLeaderboard', JSON.stringify(this.leaderboard));
        } catch (error) {
          console.error('Error saving leaderboard:', error);
        }
      }

      updateLeaderboardWithScore(playerName, score) {
        if (score === 0) return;
        
        const existingIndex = this.leaderboard.findIndex(entry => entry.name === playerName);
        
        if (existingIndex !== -1) {
          // Update existing player's best score
          if (score > this.leaderboard[existingIndex].score) {
            this.leaderboard[existingIndex].score = score;
          }
        } else {
          // Add new player
          this.leaderboard.push({ name: playerName, score });
        }
        
        // Sort by score (descending) and keep top 5
        this.leaderboard.sort((a, b) => b.score - a.score);
        this.leaderboard = this.leaderboard.slice(0, 5);
        
        this.saveLeaderboard();
        this.updateLeaderboard();
      }

      updateLeaderboard() {
        this.leaderboardList.innerHTML = '';
        
        if (this.leaderboard.length === 0) {
          const li = document.createElement('li');
          li.textContent = 'No scores yet!';
          li.style.fontStyle = 'italic';
          li.style.textAlign = 'center';
          this.leaderboardList.appendChild(li);
          return;
        }
        
        this.leaderboard.slice(0, 5).forEach(({name, score}, index) => {
          const li = document.createElement('li');
          const medal = index === 0 ? '🥇' : index === 1 ? '🥈' : index === 2 ? '🥉' : '';
          li.textContent = `${medal} ${name}: ${score}`;
          this.leaderboardList.appendChild(li);
        });
      }

      restart() {
        const confirmRestart = this.gameEnded || 
          confirm('Are you sure you want to restart? Your current game will be lost.');
        
        if (!confirmRestart) return;

        // Save current score if game ended
        if (this.gameEnded && this.score > 0) {
          this.updateLeaderboardWithScore(this.currentPlayerName, this.score);
        }

        // Prompt for new player name
        this.promptPlayerName();

        // Reset game state
        clearInterval(this.interval);
        this.foundWords.clear();
        this.score = 0;
        this.timer = this.GAME_DURATION;
        this.scoreElement.textContent = this.score;
        this.timerElement.textContent = this.timer;
        this.wordListElement.innerHTML = '';
        this.clearHint();
        this.clearSelection();
        this.gameEnded = false;
        this.submitBtn.disabled = false;
        this.hintBtn.disabled = false;
        this.hintUsed = false;
        this.hintBtn.textContent = 'Hint (1 left)';
        this.gridElement.style.opacity = 1;
        
        // Re-enable grid interactions
        document.querySelectorAll('.tile').forEach(tile => {
          tile.style.pointerEvents = '';
          tile.style.cursor = 'pointer';
        });

        // Start new game
        this.generateSmartGrid();
        this.startTimer();
        this.updateLeaderboard();
      }
    }

    // Initialize the game when page loads
    window.addEventListener('load', () => {
      new BoggleGame();
    });
  </script>
</body>
</html>
