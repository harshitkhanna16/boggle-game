#  Boggle Game Solver

A web-based Boggle-style word game built using HTML, CSS, and JavaScript.

##  Gameplay Features
- 4x4 letter grid with smart word embedding
- Random letters fill the rest of the grid
- Predefined words always included
- Click-and-drag tile selection to form words
- Highlighted tile path during selection
- "Submit" button to check and submit words
- Valid words are verified using Dictionary API
- Words must be at least 3 letters
- Duplicate word submissions are blocked
- Found words are listed with definitions
- +10 points per valid word
- Score updates live
- Selection clears automatically after submission

## Timer and Game Flow
- 2-minute countdown timer (120 seconds)
- Timer shown live beside score
- Game ends when timer reaches 0
- Final score and number of words shown in an alert
- Grid and controls are disabled after timeout
- "Restart" button resets the game

## Hint System
- One-time use "Hint" button
- Highlights the path of one unfound embedded word
- Button gets disabled after use
- Hint path clears when new selection starts

## Leaderboard
- Top 5 scores stored in localStorage
- Player prompted for name before game starts
- Leaderboard updates only if new score is higher for the same name
- Sorted by score (descending)
- Gold, Silver and Bronze backgrounds for top 3
- Leaderboard is responsive for mobile and desktop

## User Experience
- Prompt for player name on game start and restart
- Word list auto-scrolls as new words are added
- Responsive UI for smaller screens
- Smooth hover and selection effects on tiles
- Tiles visually indicate selection and hints
- Disabled interactions after game ends
- Stylish and modern color theme with visual consistency

## How to Play
1. Open `index.html` in your browser.
2. Enter your name.
3. Drag over the letters to form words.
4. Submit valid English words to earn points.
5. Use the hint once if needed. Try to beat the top score!

## Tech Stack
- HTML
- CSS
- JavaScript
- [dictionaryapi.dev](https://dictionaryapi.dev) for word validation


Happy Playing!
