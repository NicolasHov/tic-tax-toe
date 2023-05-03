<script>
import Board from './components/Board.vue'

export default {
  components: {
    Board
  },
  data() {
    return {
      board: new Array(3),
      player: "x",
      playCount: localStorage.getItem('playCount') ? parseInt(localStorage.getItem('playCount')) : 1,
    }
  },
  methods: {
    update_board(coords) {
      // if (this.isEnded() == true) {
      let updatedBoard = [...this.board]
      console.log(updatedBoard, coords, this.player); // debug
      updatedBoard[coords.row][coords.column] != " " ? null : updatedBoard[coords.row][coords.column] = this.player
      this.player == "x" ? this.player = "o" : this.player = "x"
      // return updatedBoard
      // }
      // return
    },
    fill_board() {
      // this.board = new Array(3)
      for (let i = 0; i < this.board.length; i++) {
        this.board[i] = new Array(3);
      }
      // Fill board with empty spaces
      for (let i = 0; i < this.board.length; i++) {
        for (let j = 0; j < this.board[i].length; j++) {
          this.board[i][j] = " "
        }
      }
    },
    getWinner(player) {
      // Horizontal rows
      for (let i = 0; i < 3; i++) {
        if (this.board[0][i] === player && this.board[1][i] === player && this.board[2][i] === player) {
          console.log("row", player);
          return true;
        }
      }

      // Vertical rows
      for (let i = 0; i < 3; i++) {
        if (this.board[i][0] === player && this.board[i][1] === player && this.board[i][2] === player) {
          console.log("column: ", player);
          return true;
        }
      }
      // Diagonals
      if (this.board[0][0] === player && this.board[1][1] === player && this.board[2][2] === player) {
        console.log("diagonal", player);
        return true;
      }
      if (this.board[1][0] === player && this.board[1][1] === player && this.board[0][2] === player) {
        console.log("diagonal", player);
        return true;
      }
      return false;
    },
    // isEnded() {
    //   return this.getWinner('x') || this.getWinner('o') // this.getPossibleMoves().length === 0 ||
    // }
  },
  mounted() {
    this.fill_board()
    // this.getWinner(player)
  },
  watch: {
    board: { // deep watcher to listen to array 'board' with 'deep'= true
        handler() { // TO FIX: add value to listen to ?
          // console.log("get Winner", this.getWinner('x'));
      },
      // immediate: true,
        deep: true, 
  }
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
  <!-- <div v-if="getWinner() === true">
    <div>Game over</div>
  </div> -->
</template>

<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
}

.container {
  display: flex;
  flex-wrap: wrap;
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
