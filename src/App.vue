<script>
import Board from './components/Board.vue'

export default {
  components: {
    Board
  },
  data() {
    return {
      board: Array,
      player: "x",
      isEnded: false,
      playCount: localStorage.getItem('playCount') ? parseInt(localStorage.getItem('playCount')) : 1,
      lines: [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],
        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8],
        [0, 4, 8],
        [2, 4, 6],
      ]
    }
  },
  methods: {
    update_board(coords) {
      while (this.isEnded !== true) {
        let updatedBoard = [...this.board]
        // console.log(updatedBoard, coords, this.player);
        updatedBoard[coords.row][coords.column] != " " ? null : updatedBoard[coords.row][coords.column] = this.player
        this.player == "x" ? this.player = "o" : this.player = "x"
        return updatedBoard
      }
    },
    fill_board() {
      this.board = new Array(3)
      for (let i = 0; i < this.board.length; i++) {
        this.board[i] = new Array(3);
      }
      // Fill board with empty spaces
      for (let i = 0; i < this.board.length; i++) {
        for (let j = 0; j < this.board[i].length; j++) {
          this.board[i][j] = " "
          // { value:Math.floor(Math.random()*5)+1 }
        }
      }
    },
    calculateWinner() {
      let list = [...this.board].flat() // TOFIX: flat array
      console.log(list);
      // Win check for rows and columns
      for (let i = 0; i < 3; i++) {
        if (list[0 + i * 3] === this.player
          && list[1 + i * 3] === this.player
          && list[2 + i * 3] === this.player
          ||
          list[0 + i] === this.player
          && list[3 + i] === this.player
          && list[6 + i] === this.player) {
          console.log("row and colums");
          this.isEnded = true;
        }
      }
      // Win check for diagonals
      if (list[0] === this.player
        && list[4] === this.player
        && list[8] === this.player
        ||
        list[2] === this.player
        && list[4] === this.player
        && list[6] === this.player
      ) {
        console.log("diagonals");
        this.isEnded = true;
      }
    },
  },
  mounted() {
    this.fill_board()
  },
  watch() {
    this.calculateWinner()
    this.update_board()
  }
}

</script>

<template>
  <header>
    <div class="wrapper">
      <div>next player: {{ player }}</div>
    </div>
  </header>
  <div class="container">
    <Board :update_board="update_board" :board="board" />
  </div>
  <div>Game over: {{ isEnded }}</div>
</template>

<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
}

.container {
  display: flex;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
</style>
