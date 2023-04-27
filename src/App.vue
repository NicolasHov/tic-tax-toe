<script>
import Board from './components/Board.vue'

export default {
  components: {
    Board
  },
  data() {
    return {
      size: 10,
      board: Array,
      player: "x",
      isEnded: false
    }
  },
  methods: {
    update_board(coords) {
      let updatedBoard = [...this.board]
      console.log(updatedBoard, coords, this.player);
      // let oneDindex = (coords.row * updatedBoard.length) + coords.column; // Indexes
      // console.log("oneDindex", oneDindex);
      updatedBoard[coords.row][coords.column] != " " ? null : updatedBoard[coords.row][coords.column] = this.player
      this.player == "x" ? this.player = "o" : this.player = "x"
      return updatedBoard
    }
    // calculateBooksMessage() {
    //   return this.author.books.length > 0 ? 'Yes' : 'No'
    // }
    ,
    fill_board() {
      this.board = new Array(this.size)
      for (let i = 0; i < this.board.length; i++) {
        this.board[i] = new Array(this.size);
      }
      // Fill board with empty spaces
      for (let i = 0; i < this.board.length; i++) {
        for (let j = 0; j < this.board[i].length; j++) {
          this.board[i][j] = " "
          // { value:Math.floor(Math.random()*5)+1 }
        }
      }
    },
  },
  mounted() {
    this.fill_board()
  },
  watch() {
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
}</style>
