import java.util.Scanner;

class Cell {
    private String value;
    private boolean isOccupied;

    public Cell() {
        this.value = "";
        this.isOccupied = false;
    }

    public String getValue() {
        return value;
    }

    public void setValue(String value) {
        this.value = value;
        this.isOccupied = true;
    }

    public boolean isOccupied() {
        return isOccupied;
    }

    public void reset() {
        this.value = "";
        this.isOccupied = false;
    }
}

class SmallBoard {
    private Cell[][] cells;
    private boolean isWon;
    private String winner;

    public SmallBoard() {
        cells = new Cell[3][3];
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                cells[i][j] = new Cell();
            }
        }
        isWon = false;
        winner = "";
    }

    public boolean makeMove(int row, int col, String symbol) {
        if (!cells[row][col].isOccupied() && !isWon) {
            cells[row][col].setValue(symbol);
            checkWin(symbol);
            return true;
        }
        return false;
    }

    public boolean isWon() {
        return isWon;
    }

    public String getWinner() {
        return winner;
    }

    public Cell getCell(int row, int col) {
        return cells[row][col];
    }

    private void checkWin(String symbol) {
        // Checkrows
        for (int i = 0; i < 3; i++) {
            if (cells[i][0].getValue().equals(symbol) &&
                    cells[i][1].getValue().equals(symbol) &&
                    cells[i][2].getValue().equals(symbol)) {
                isWon = true;
                winner = symbol;
                return;
            }
        }

        // Check columnS
        for (int i = 0; i < 3; i++) {
            if (cells[0][i].getValue().equals(symbol) &&
                    cells[1][i].getValue().equals(symbol) &&
                    cells[2][i].getValue().equals(symbol)) {
                isWon = true;
                winner = symbol;
                return;
            }
        }

        // Check diaonals
        if (cells[0][0].getValue().equals(symbol) &&
                cells[1][1].getValue().equals(symbol) &&
                cells[2][2].getValue().equals(symbol)) {
            isWon = true;
            winner = symbol;
            return;
        }

        if (cells[0][2].getValue().equals(symbol) &&
                cells[1][1].getValue().equals(symbol) &&
                cells[2][0].getValue().equals(symbol)) {
            isWon = true;
            winner = symbol;
        }
    }

    public void reset() {
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                cells[i][j].reset();
            }
        }
        isWon = false;
        winner = "";
    }
}

class Player {
    private String name;
    private String symbol;
    private int score;

    public Player(String name, String symbol) {
        this.name = name;
        this.symbol = symbol;
        this.score = 0;
    }

    public String getName() {
        return name;
    }

    public String getSymbol() {
        return symbol;
    }

    public int getScore() {
        return score;
    }

    public void incrementScore() {
        score++;
    }

    public void resetScore() {
        score = 0;
    }
}

class GameBoard {
    private SmallBoard[][] boards;
    private Player player1;
    private Player player2;
    private Player currentPlayer;
    private int nextBoardRow;
    private int nextBoardCol;
    private boolean gameWon;
    private boolean firstMove;

    public GameBoard(String player1Name, String player2Name) {
        boards = new SmallBoard[3][3];
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                boards[i][j] = new SmallBoard();
            }
        }

        player1 = new Player(player1Name, "X");
        player2 = new Player(player2Name, "O");
                currentPlayer = player1;
        nextBoardRow = -1;
        nextBoardCol = -1;
        gameWon = false;
        firstMove = true;
    }

    public boolean makeMove(int boardRow, int boardCol, int cellRow, int cellCol) {
        if (gameWon) return false;

        // Check if the bolrd is valid
        if (!firstMove && (boardRow != nextBoardRow || boardCol != nextBoardCol)) {
            if (nextBoardRow != -1 && nextBoardCol != -1) {
                return false;
            }
        }

        // Make the move
        if (boards[boardRow][boardCol].makeMove(cellRow, cellCol, currentPlayer.getSymbol())) {
            firstMove = false;

            // Set next board based on the cell played
            if (boards[cellRow][cellCol].isWon()) {
                nextBoardRow = -1;
                nextBoardCol = -1;
            } else {
                nextBoardRow = cellRow;
                nextBoardCol = cellCol;
            }

            // Check for win in the MAin Board
            checkMainBoardWin();

            // switch players
            currentPlayer = (currentPlayer == player1) ? player2 : player1;
            return true;
        }
        return false;
    }

    private void checkMainBoardWin() {
        // Check rows
        for (int i = 0; i < 3; i++) {
            if (boards[i][0].isWon() && boards[i][1].isWon() && boards[i][2].isWon() &&
                    boards[i][0].getWinner().equals(currentPlayer.getSymbol()) &&
                    boards[i][1].getWinner().equals(currentPlayer.getSymbol()) &&
                    boards[i][2].getWinner().equals(currentPlayer.getSymbol())) {
                gameWon = true;
                currentPlayer.incrementScore();
                return;
            }
        }

        // Check columns
        for (int i = 0; i < 3; i++) {
            if (boards[0][i].isWon() && boards[1][i].isWon() && boards[2][i].isWon() &&
                    boards[0][i].getWinner().equals(currentPlayer.getSymbol()) &&
                    boards[1][i].getWinner().equals(currentPlayer.getSymbol()) &&
                    boards[2][i].getWinner().equals(currentPlayer.getSymbol())) {
                gameWon = true;
                currentPlayer.incrementScore();
                return;
            }
        }

        // Check diagonals
        if (boards[0][0].isWon() && boards[1][1].isWon() && boards[2][2].isWon() &&
                boards[0][0].getWinner().equals(currentPlayer.getSymbol()) &&
                boards[1][1].getWinner().equals(currentPlayer.getSymbol()) &&
                boards[2][2].getWinner().equals(currentPlayer.getSymbol())) {
            gameWon = true;
            currentPlayer.incrementScore();
            return;
        }

        if (boards[0][2].isWon() && boards[1][1].isWon() && boards[2][0].isWon() &&
                boards[0][2].getWinner().equals(currentPlayer.getSymbol()) &&
                boards[1][1].getWinner().equals(currentPlayer.getSymbol()) &&
                boards[2][0].getWinner().equals(currentPlayer.getSymbol())) {
            gameWon = true;
            currentPlayer.incrementScore();
        }
    }

    public void resetGame() {
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                boards[i][j].reset();
            }
        }
        currentPlayer = player1;
        nextBoardRow = -1;
        nextBoardCol = -1;
        gameWon = false;
        firstMove = true;
    }

    public SmallBoard getBoard(int row, int col) {
        return boards[row][col];
    }

    public Player getCurrentPlayer() {
        return currentPlayer;
    }

    public boolean isGameWon() {
        return gameWon;
    }

    public int getNextBoardRow() {
        return nextBoardRow;
    }

    public int getNextBoardCol() {
        return nextBoardCol;
    }
}

public class TicTacToeInTicTacToe {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter Player 1 name: ");
        String player1Name = scanner.nextLine();
        System.out.print("Enter Player 2 name: ");
        String player2Name = scanner.nextLine();

        GameBoard gameBoard = new GameBoard(player1Name, player2Name);
        boolean playAgain;

        do {
            playAgain = false;
            while (!gameBoard.isGameWon()) {
                printGameBoard(gameBoard);
                System.out.println(gameBoard.getCurrentPlayer().getName() + "'s turn (" + gameBoard.getCurrentPlayer().getSymbol() + ")");
                System.out.print("Enter the large board row (0-2): ");
                int boardRow = scanner.nextInt();
                System.out.print("Enter the large board column (0-2): ");
                int boardCol = scanner.nextInt();
                System.out.print("Enter the small board row (0-2): ");
                int cellRow = scanner.nextInt();
                System.out.print("Enter the small board column (0-2): ");
                int cellCol = scanner.nextInt();

                if (!gameBoard.makeMove(boardRow, boardCol, cellRow, cellCol)) {
                    System.out.println("Invalid move. Try again.");
                }
            }

            printGameBoard(gameBoard);
            System.out.println(gameBoard.getCurrentPlayer().getName() + " wins the game!");
            System.out.println("Score: " + gameBoard.getCurrentPlayer().getName() + ": " + gameBoard.getCurrentPlayer().getScore());

            System.out.print("Do you want to play again? (yes/no): ");
            String response = scanner.next();
            if (response.equalsIgnoreCase("yes")) {
                gameBoard.resetGame();
                playAgain = true;
            }
        } while (playAgain);

        System.out.println("Thank you for playing!");
        scanner.close();
    }

    private static void printGameBoard(GameBoard gameBoard) {
        System.out.println("Current Game Board:");
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                SmallBoard smallBoard = gameBoard.getBoard(i, j);
                System.out.print("[" + (smallBoard.isWon() ? smallBoard.getWinner() : " ") + "]");
                for (int k = 0; k < 3; k++) {
                    for (int l = 0; l < 3; l++) {
                        System.out.print(smallBoard.getCell(k, l).getValue() + " ");
                    }
                    System.out.print(" | ");
                }
                System.out.println();
            }
            System.out.println("---------");
        }
    }
}
