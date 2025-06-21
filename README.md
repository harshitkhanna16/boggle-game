# Boggle Game Solver

A browser-based interactive word game inspired by the classic Boggle board game. Built using HTML, CSS, and JavaScript, it allows users to form words by dragging across letter tiles, validate them via a dictionary API, and compete for the top score on a live leaderboard.

## Introduction

This project is a smart word puzzle game that combines logic, vocabulary, and time-based gameplay. It dynamically generates a 4x4 grid with hidden words embedded in random directions. Players find valid words by dragging across adjacent letters, score points, and try to beat the 2-minute timer. It's perfect for sharpening your language skills and having fun!

## Workflow

1. **Game Initialization**:  
   - Player is prompted to enter their name.
   - A 4x4 letter grid is generated with 4 embedded English words.

2. **Word Formation**:  
   - Player drags across letter tiles to form words.
   - Selected word is validated using the [dictionaryapi.dev](https://dictionaryapi.dev) API.

3. **Scoring and Tracking**:  
   - Each valid word scores 10 points.
   - Words are listed with definitions.
   - A 2-minute timer counts down.

4. **Game Over**:  
   - When time is up, game ends and final score is shown.
   - Score is saved to a persistent leaderboard.

5. **Leaderboard**:  
   - Top 5 scores are stored in `localStorage`.
   - Scores are updated only if the new one is higher for the same player.

6. **Extras**:  
   - A one-time hint reveals the path of an embedded word.
   - Restart button allows for a fresh game with a new grid and name.

## Features

- Smart 4x4 grid with predefined word embedding
- Word selection via mouse drag
- Dictionary-based word validation
- Score tracking with +10 per valid word
- 2-minute countdown timer
- One-time visual hint feature
- Duplicate word prevention
- Found words list with short definitions
- Local top 5 leaderboard with medals
- Responsive UI for desktop and mobile
- Restart with new name and grid

## Tech Stack

- **Frontend**: HTML5, CSS3, JavaScript (ES6)
- **API**: [Free Dictionary API](https://dictionaryapi.dev/)
- **Storage**: Web Browser `localStorage` for leaderboard

## Project Structure
boggle-game/
│
├── index.html # Main HTML file
├── README.md # Project documentation
└── (Optional)
├── style.css # If CSS separated
└── script.js # If JS separated


## Future Scope
- Mobile Touch Support
- Multiplayer Mode (local or online)
- Dark Mode Toggle
- Difficulty levels (Easy/Medium/Hard)

## Author
**Harshit Khanna**  
