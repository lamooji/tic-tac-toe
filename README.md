# Tic-Tac-Toe

## Overview

A two-player tic-tac-toe game built with React. Players take turns placing X and O on a 3×3 board, and the game announces the winner when someone gets three in a row. A move history list lets you jump back to any earlier move ("time travel"). On top of the original tutorial, this version keeps a running scoreboard of wins for X and O and has buttons to restart the game and reset the scores.

## How to run it

You need [Node.js](https://nodejs.org/) installed.

```bash
npm install --legacy-peer-deps
npm start
```

The app opens at http://localhost:3000.

`--legacy-peer-deps` is needed because the tutorial starter uses a canary (pre-release) build of React, which npm treats as incompatible with `react-scripts` even though they work together.

## My contribution

Starting from the React tic-tac-toe tutorial, I added:

- **Restart button:** clears the board and the move history so a new game starts with X.
- **Scoreboard:** shows how many games X and O have won. Each game is counted only once, even if you use the move history to go back and replay the winning move.
- **Reset scores button:** sets both scores back to 0.

All changes are in `src/App.js`. New state (`scores` and `scored`) lives in the `Game` component, the score updates in `handlePlay` when a move produces a winner, and there are new `handleRestart` and `handleResetScores` functions.

## What I learned

The biggest challenge was getting the project to run at all. `npm install` failed with an `ERESOLVE` dependency error, because the starter's canary version of React didn't satisfy the version range `react-scripts` asks for. I read the error message closely, learned that npm never lets a pre-release version satisfy a normal range, and installed with `--legacy-peer-deps`. That led to a second error (`Cannot find module 'ajv/dist/compile/codegen'`), which I fixed by installing `ajv` version 8 as a dev dependency. This taught me how npm resolves peer dependencies and why reading the full error message matters more than retrying the same command.

I also learned how React state works when adding the scoreboard. I had to make sure going back in the move history didn't count the same win twice, so I added a `scored` flag that resets whenever a new game starts.

## References

- [React Tutorial: Tic-Tac-Toe](https://react.dev/learn/tutorial-tic-tac-toe): the starter code and base game come from the official React tutorial.
- [Create React App / react-scripts](https://create-react-app.dev/): the build tool used by the starter.
- Claude (Anthropic): used as an AI assistant to debug the npm install errors and to help implement and explain the restart button and scoreboard.
