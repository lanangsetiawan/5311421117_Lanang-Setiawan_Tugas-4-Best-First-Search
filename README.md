# 5311421117_Lanang-Setiawan_Tugas-4-Best-First-Search

package TicTacToe;  
/** * Enumeration for the various states of the game */ public enum 
GameState { // to save as "GameState.java" 
PLAYING, DRAW, CROSS_WON, NOUGHT_WON 
} 

  * GameState (dalam GameState.java) adalah enumerasi yang digunakan untuk mewakili status permainan Tic-Tac-Toe. Ada empat nilai yang mungkin:
    1. PLAYING: Ini menunjukkan bahwa permainan masih berlangsung.
    2. DRAW: Ini menunjukkan bahwa permainan berakhir dengan hasil imbang (tidak ada pemain yang menang).
    3. CROSS_WON: Ini menunjukkan bahwa pemain yang menggunakan tanda "X" telah menang.
    4. NOUGHT_WON: Ini menunjukkan bahwa pemain yang menggunakan tanda "O" telah menang.
     
package TicTacToe;
/** * Enumeration for the seeds and cell contents */ public enum Seed {
// to save as "Seed.java"
EMPTY, CROSS, NOUGHT
  
  * Seed (dalam Seed.java) adalah enumerasi yang digunakan untuk merepresentasikan isi sel pada papan permainan. Ada tiga nilai yang mungkin:
    1. EMPTY: Ini menunjukkan bahwa sel di papan permainan masih kosong
    2. CROSS: Ini menunjukkan bahwa sel diisi dengan tanda "X".
    3. NOUGHT: Ini menunjukkan bahwa sel diisi dengan tanda "O".
       
package TicTacToe;
/** * Enumeration for the various states of the game */ public enum
State { // to save as "GameState.java"
PLAYING, DRAW, CROSS_WON, NOUGHT_WON
}

  * State (dalam GameState.java) adalah enumerasi yang terlihat serupa dengan GameState, tetapi mungkin merupakan duplikasi. Pada dasarnya, enumerasi ini juga digunakan untuk mewakili status permainan Tic-Tac-Toe dan memiliki nilai yang sama seperti PLAYING, DRAW, CROSS_WON, dan NOUGHT_WON. Namun, menciptakan duplikasi enumerasi mungkin merupakan kesalahan penulisan yang harus dihindari.

package TicTacToe;
import java.awt.Graphics;
import java.awt.*;
import java.awt.Graphics2D;

public class Cell {
  //content of this cell (Seed.EMPTY, Seed.CROSS, or Seed.NOUGHT)
  Seed content;
  int row, col; // row and column of this cell
  /**Constructor to initialize this cell with the specified row and col */
  public Cell(int row, int col) {
    this.row = row;
    this.col = col;
    clear(); // clear content
  }
  /** Clear this cell's content to EMPTY */
  public void clear() {
    content = Seed.EMPTY;
  }
  /**Paint itself on the graphics canvas, given the Graphics context */
  public void paint(Graphics g) {
    // Use Graphics2D which allows us to set the pen's stroke
    Graphics2D g2d = (Graphics2D)g;
    g2d.setStroke(new BasicStroke(GameMain.SYMBOL_STROKE_WIDTH,
    BasicStroke.CAP_ROUND, BasicStroke.JOIN_ROUND)); // Graphics2Donly
    // Draw the Seed if it is not empty
    int x1 = col * GameMain.CELL_SIZE + GameMain.CELL_PADDING;
    int y1 = row * GameMain.CELL_SIZE + GameMain.CELL_PADDING;
    if (content == Seed.CROSS) {
      g2d.setColor(Color.RED);
      int x2 = (col + 1) * GameMain.CELL_SIZE - GameMain.CELL_PADDING;
      int y2 = (row + 1) * GameMain.CELL_SIZE - GameMain.CELL_PADDING;
      g2d.drawLine(x1, y1, x2, y2);
      g2d.drawLine(x2, y1, x1, y2);
    }
    else if (content == Seed.NOUGHT) {
      g2d.setColor(Color.BLUE);
      g2d.drawOval(x1, y1, GameMain.SYMBOL_SIZE, GameMain.SYMBOL_SIZE);
    }
  }
}

Kode ini merupakan bagian dari permainan Tic-Tac-Toe yang lebih besar yang mungkin mencakup kelas-kelas dan logika lain untuk mengatur permainan. Kelas Cell ini bertanggung jawab untuk menggambar dan mengatur isi setiap sel pada papan permainan.

  * Seed content: Ini adalah atribut yang merepresentasikan isi dari sel tersebut. Nilai dari Seed bisa berupa EMPTY, CROSS, atau NOUGHT sesuai dengan apakah sel tersebut kosong atau diisi dengan tanda "X" atau "O".
  * int row, col: Ini adalah atribut yang menyimpan posisi baris dan kolom dari sel tersebut di papan permainan.
  * Konstruktor Cell(int row, int col): Konstruktor ini digunakan untuk membuat objek Cell dengan baris dan kolom tertentu. Saat objek Cell dibuat, isi selnya diatur ke EMPTY menggunakan metode clear().
  * Metode clear(): Metode ini digunakan untuk menghapus isi sel dan mengaturnya kembali ke EMPTY.
  * Metode paint(Graphics g): Metode ini digunakan untuk menggambar sel pada papan permainan. Ini memanfaatkan objek Graphics untuk menggambar tanda "X" (dengan warna merah) atau "O" (dengan warna biru) di sel tersebut. Penggambaran tanda "X" dilakukan dengan menggambar dua garis silang, sementara penggambaran tanda "O" dilakukan dengan menggambar oval.

package TicTacToe;
import java.awt.*;

/**
* The Board class models the ROWS-by-COLS game-board.
*/

public class Board {
  // package access
  // composes of 2D array of ROWS-by-COLS Cell instances
  Cell[][] cells;
  
  /** Constructor to initialize the game board */
  public Board() {
    // allocate the array
    cells = new Cell[GameMain.ROWS][GameMain.COLS];
    for (int row = 0; row < GameMain.ROWS; ++row) {
      for (int col = 0; col < GameMain.COLS; ++col) {
      // allocate element of array
      cells[row][col] = new Cell(row, col);
      }
    }
  }
  
  /** Initialize (or re-initialize) the game board */
  public void init() {
    for (int row = 0; row < GameMain.ROWS; ++row) {
      for (int col = 0; col < GameMain.COLS; ++col) {
        // clear the cell content
        cells[row][col].clear();
      }
    }
  }
  
  /** Return true if it is a draw (i.e., no more EMPTY cell) */
  public boolean isDraw() {
    for (int row = 0; row < GameMain.ROWS; ++row) {
      for (int col = 0; col < GameMain.COLS; ++col) {
        if (cells[row][col].content == Seed.EMPTY) {
          // an empty seed found, not a draw, exit
          return false;
        }
      }
    }
    return true; // no empty cell, it's a draw
  }
 
 /** Return true if the player with "seed" has won after placing at
 (seedRow, seedCol) */
 public boolean hasWon(Seed seed, int seedRow, int seedCol) {
   return (cells[seedRow][0].content == seed // 3-in-the-row
   && cells[seedRow][1].content == seed
   && cells[seedRow][2].content == seed
   || cells[0][seedCol].content == seed // 3-in-the-column
   && cells[1][seedCol].content == seed
   && cells[2][seedCol].content == seed
   || seedRow == seedCol // 3-in-the-diagonal
   && cells[0][0].content == seed
   && cells[1][1].content == seed
   && cells[2][2].content == seed
   || seedRow + seedCol == 2 // 3-in-the-opposite-diagonal
   && cells[0][2].content == seed
   && cells[1][1].content == seed
   && cells[2][0].content == seed);
 }
 
 /** Paint itself on the graphics canvas, given the Graphics context */
 public void paint(Graphics g) {
   // Draw the grid-lines
   g.setColor(Color.GRAY);
   for (int row = 1; row < GameMain.ROWS; ++row) {
     g.fillRoundRect(0, GameMain.CELL_SIZE * row -
     GameMain.GRID_WIDHT_HALF,
     GameMain.CANVAS_WIDTH-1, GameMain.GRID_WIDTH,
     GameMain.GRID_WIDTH, GameMain.GRID_WIDTH);
   }
   for (int col = 1; col < GameMain.COLS; ++col) {
     g.fillRoundRect(GameMain.CELL_SIZE * col -
     GameMain.GRID_WIDHT_HALF, 0,
     GameMain.GRID_WIDTH, GameMain.CANVAS_HEIGHT - 1,
     GameMain.GRID_WIDTH, GameMain.GRID_WIDTH);
   }
   // Draw all the cells
   for (int row = 0; row < GameMain.ROWS; ++row) {
     for (int col = 0; col < GameMain.COLS; ++col) {
     cells[row][col].paint(g); // ask the cell to paint itself
     }
   }
 }
}
