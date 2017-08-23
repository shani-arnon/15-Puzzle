# 15-Puzzle
Practice my JS

const BOARD_SIZE = 9;

function move(board, index) {
  board.cells[board.emptyIndex] = board.cells[index];
  board.cells[index] = 0;
  board.emptyIndex = index;
}

function movement(board, index) {
  var rowNumber = Math.floor(index / board.rowSize);
  var columnNumber = index % board.rowSize;

  if (rowNumber > 0) {
    var destinationIndex = index - board.rowSize;
    if (destinationIndex === board.emptyIndex) {
      move(board, index);
      return true;
    }
  }
  if (rowNumber < board.rowSize - 1) {
    var destinationIndex = index + board.rowSize;
    if (destinationIndex === board.emptyIndex) {
      move(board, index);
      return true;
    }
  }
  if (columnNumber < board.rowSize - 1) {
    var destinationIndex = index + 1;
    if (destinationIndex === board.emptyIndex) {
      move(board, index);
      return true;
    }
  }
  if (columnNumber > 0) {
    var destinationIndex = index - 1;
    if (destinationIndex === board.emptyIndex) {
      move(board, index);
      return true;
    }
  }

  return false;
}

// This is a function that shuffles an array of numbers.
function shuffle(array) {
  array.sort(function (a, b) {
    return 0.5 - Math.random();
  });
}

// This function creates a shuffled board.
function createBoard(boardSize) {
  var board = {
    cells: [],
    emptyIndex: null,
    size: boardSize,
    rowSize: Math.sqrt(boardSize)
  };
  
  // Fill the cells with ORDERED numbers.
  for (var i = 0; i < board.size; i++) {
    board.cells.push(i);
  }
  
  // Now we have an ORDERED board. Let's SHUFFLE it.
  shuffle(board.cells);

  // Find the location of the empty index.
  for (var i = 0; i < board.size; i++) {
    if (board.cells[i] === 0) {
      board.emptyIndex = i;
      break;
    }
  }
  
  return board;
}

// function main() {
//   var board = createBoard(BOARD_SIZE);

//   console.log(board.cells);

//   var clickedIndex = 2;

//   var moved = movement(board, clickedIndex);
//   console.log(`${clickedIndex} moved: ${moved}`);

//   console.log(board.cells);
// }

// main();
