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
* a
* a
* a
* a
* a
