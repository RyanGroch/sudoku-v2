# Sudoku Solver

A browser app which allows the user to play Sudoku puzzles. The app generates random puzzles using recursive backtracking, and can also visualize the solving algorithm.

You can visit the app [here](https://ryan-groch.github.io/sudoku-v2/).

## What is Sudoku?

Sudoku is a puzzle game played on a 9x9 grid. The goal is to make sure that each row, column, and 3x3 square (usually delineated by thicker black lines) have exactly one of each digit from 1 through 9. Some squares on the 9x9 grid are already filled in, while most of them are blank. The player must use the squares that are already determined to figure out the digits that fill the remaining squares.

A vast number of possible Sudoku puzzles can be created. Each puzzle is guaranteed to have exactly one solution provided that the puzzle has been created correctly.

## About the App

This app generates random puzzles and allows the user to play through them. While the app can generate puzzles of varying difficulty, the puzzles only differ in the number of starting digits provided. This may not be reflective of the true difficulty of the puzzle.

Additionally, users can take notes on the grid, receive hints, check for mistakes, erase tiles, and undo previous moves. These are common operations that Sudoku players often use, and exist to make the experience more pleasant.

The app also has a “Solve For Me” button, and clicking it will cause the app to visualize the solving algorithm on the currently displayed puzzle.

## About the Algorithm

The app uses two main algorithms. The first is a solver, used to solve puzzles that are not currently completed, and also to generate new solutions from scratch. The second is what I’ve called the “unsolver”, which takes in a completed solution and removes digits from it to create an unsolved puzzle.

### The Solver

The solver is a recursive backtracking algorithm which parses each tile on the 9x9 grid starting from the top left to the bottom right. When it encounters a blank tile, it inserts one of the digits from 1 through 9. If inserting that digit is shown to violate one of Sudoku’s rules, it will try a different digit. It may eventually attempt each of the nine digits, and if all of them fail then the algorithm will backtrack.

Provided that the insertion of a digit does not immediately violate one of Sudoku’s rules, the algorithm will continue parsing the tiles until it encounters another blank tile. It will then repeat the same process specified above, and continue doing so until the puzzle is solved.

If the solver is generating a solution from scratch, then it will return the first solution that it finds. In other instances, the solver may continue even after finding a solution, as it is used in the “unsolver” to ensure that a puzzle has exactly one solution.

### The Unsolver

The unsolver is an iterative algorithm. It randomly removes a digit from the puzzle, then runs the solver to ensure that there is still exactly one solution. The algorithm stops when it has either removed a specified number of digits, or when the algorithm has found through trial-and-error that it cannot remove another digit without creating at least one new solution for the puzzle.

This algorithm only runs when the program generates a new puzzle from scratch.

## Technologies Used

This app was built with vanilla Javascript, using Vite as the build tool.

## Possible Improvements

There are several changes I might eventually like to make to this app.

- Using a framework such as React would help clean up the codebase.
- I originally attempted to structure this project with an object-oriented design, but I think that made my code unnecessarily complicated. In future projects, I would like to move away from this approach.
- The unsolver does not currently backtrack. Writing in a way that allows backtracking would ensure that the algorithm can always reach its targeted number of digits.
