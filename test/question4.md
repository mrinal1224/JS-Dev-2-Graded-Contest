### Problem Statement

You are tasked with designing the architecture for a game of Chess using constructor functions. This problem will test your understanding of prototypal inheritance and object-oriented design principles in JavaScript. Specifically, you will create a `ChessPiece` constructor function and extend it to create pieces like `Knight` and `Queen` that inherit from `ChessPiece`.

Each piece will have:
1. **Name**: Name of the piece, like "Knight" or "Queen."
2. **Color**: Color of the piece, either "White" or "Black."
3. **Position**: Current position of the piece on the chessboard, represented as coordinates (e.g., "B1", "D4", etc.).

You will then implement the following behavior:
1. Create a `ChessPiece` constructor function that takes three parameters:
   - `name`: Name of the chess piece.
   - `color`: Color of the chess piece.
   - `position`: The initial position of the piece on the board, represented as a string.
   
2. Implement a **moveTo(newPosition)** method in `ChessPiece`, which updates the current position of the piece.

3. Create **Knight** and **Queen** constructor functions that inherit from `ChessPiece`:
   - For the **Knight**, implement the `moveTo(newPosition)` method such that the piece can only move in an "L" shape (either two steps in one direction and one step in a perpendicular direction).
   - For the **Queen**, implement the `moveTo(newPosition)` method such that the piece can move any number of squares in a straight line (horizontally, vertically, or diagonally).

4. Validate the moves:
   - If the move is valid, update the position.
   - If the move is invalid, return an error message: `"Invalid move for {PieceName}!"`

### Solution Approach

1. **ChessPiece Constructor**: The base constructor function that initializes the name, color, and position of a piece. It will have a `moveTo` method that updates the position.
2. **Knight Constructor**: Inherit from `ChessPiece` and override the `moveTo` method to validate that moves are only in an "L" shape.
3. **Queen Constructor**: Inherit from `ChessPiece` and override the `moveTo` method to validate that the piece moves in straight lines (horizontally, vertically, or diagonally).
4. **Prototypal Inheritance**: The `Knight` and `Queen` constructor functions will inherit from `ChessPiece` using prototypal inheritance.

### Hints

1. Use prototypal inheritance to ensure that the `Knight` and `Queen` constructors inherit from `ChessPiece`.
2. For **Knight**:
   - A valid "L" shape move means two steps in one direction and one step in a perpendicular direction, or one step in one direction and two steps in a perpendicular direction.
3. For **Queen**:
   - A valid move is either in a straight line (horizontal or vertical) or a diagonal.

### Test Cases

```javascript
// Create a white Knight positioned at "B1" and move it to "C3" (valid), "E2" (valid), "C2" (invalid).
const whiteKnight = new Knight("White", "B1");

console.log(whiteKnight.moveTo("C3"));  // Valid move, should update position
console.log(whiteKnight.moveTo("E2"));  // Valid move, should update position
console.log(whiteKnight.moveTo("C2"));  // Invalid move, should return error message

// Create a black Queen positioned at "D4" and move it to "D7" (valid), "G7" (valid), "E6" (invalid).
const blackQueen = new Queen("Black", "D4");

console.log(blackQueen.moveTo("D7"));  // Valid move, should update position
console.log(blackQueen.moveTo("G7"));  // Valid move, should update position
console.log(blackQueen.moveTo("E6"));  // Invalid move, should return error message
```

### Code Stub

```javascript
// Base constructor function
function ChessPiece(name, color, position) {
    this.name = name;
    this.color = color;
    this.position = position;
}

ChessPiece.prototype.moveTo = function(newPosition) {
    this.position = newPosition;
};

// Knight constructor function
function Knight(color, position) {
    ChessPiece.call(this, 'Knight', color, position);
}

// Ensure Knight inherits from ChessPiece
Knight.prototype = Object.create(ChessPiece.prototype);
Knight.prototype.constructor = Knight;

// Implement moveTo for Knight with specific movement logic

// Queen constructor function
function Queen(color, position) {
    ChessPiece.call(this, 'Queen', color, position);
}

// Ensure Queen inherits from ChessPiece
Queen.prototype = Object.create(ChessPiece.prototype);
Queen.prototype.constructor = Queen;

// Implement moveTo for Queen with specific movement logic

// Write test cases below
```

### Complete Solution

```javascript
// Base constructor function
function ChessPiece(name, color, position) {
    this.name = name;
    this.color = color;
    this.position = position;
}

ChessPiece.prototype.moveTo = function(newPosition) {
    this.position = newPosition;
};

// Utility function to convert positions like 'B1' to numeric coordinates [x, y]
function positionToCoords(pos) {
    const x = pos.charCodeAt(0) - 'A'.charCodeAt(0);
    const y = parseInt(pos[1]) - 1;
    return [x, y];
}

// Utility function to convert coordinates back to positions like 'B1'
function coordsToPosition(coords) {
    const x = String.fromCharCode(coords[0] + 'A'.charCodeAt(0));
    const y = coords[1] + 1;
    return x + y;
}

// Knight constructor function
function Knight(color, position) {
    ChessPiece.call(this, 'Knight', color, position);
}

Knight.prototype = Object.create(ChessPiece.prototype);
Knight.prototype.constructor = Knight;

Knight.prototype.moveTo = function(newPosition) {
    const [currentX, currentY] = positionToCoords(this.position);
    const [newX, newY] = positionToCoords(newPosition);

    const dx = Math.abs(newX - currentX);
    const dy = Math.abs(newY - currentY);

    // Knight can move in "L" shape (2 + 1 or 1 + 2)
    if ((dx === 2 && dy === 1) || (dx === 1 && dy === 2)) {
        this.position = newPosition;
    } else {
        return `Invalid move for Knight!`;
    }
};

// Queen constructor function
function Queen(color, position) {
    ChessPiece.call(this, 'Queen', color, position);
}

Queen.prototype = Object.create(ChessPiece.prototype);
Queen.prototype.constructor = Queen;

Queen.prototype.moveTo = function(newPosition) {
    const [currentX, currentY] = positionToCoords(this.position);
    const [newX, newY] = positionToCoords(newPosition);

    const dx = Math.abs(newX - currentX);
    const dy = Math.abs(newY - currentY);

    // Queen can move in straight line or diagonally
    if (dx === dy || currentX === newX || currentY === newY) {
        this.position = newPosition;
    } else {
        return `Invalid move for Queen!`;
    }
};

// Test your solution
const whiteKnight = new Knight("White", "B1");

console.log(whiteKnight.moveTo("C3"));  // Valid move
console.log(whiteKnight.position);      // Should be "C3"

console.log(whiteKnight.moveTo("E2"));  // Valid move
console.log(whiteKnight.position);      // Should be "E2"

console.log(whiteKnight.moveTo("C2"));  // Invalid move

const blackQueen = new Queen("Black", "D4");

console.log(blackQueen.moveTo("D7"));   // Valid move
console.log(blackQueen.position);       // Should be "D7"

console.log(blackQueen.moveTo("G7"));   // Valid move
console.log(blackQueen.position);       // Should be "G7"

console.log(blackQueen.moveTo("E6"));   // Invalid move
```

This enhanced problem introduces more complex movement rules for the Knight and Queen, and tests students' ability to manage prototypal inheritance, coordinate conversions, and chess-specific movement logic.