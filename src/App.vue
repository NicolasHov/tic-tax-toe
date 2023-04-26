<script>
import Board from './components/Board.vue'

export default {
  components: {
    Board
  },
  data() {
    return {
      size: 10,
      player: ""
    }
  },
  methods: {
    create_board() {
      const board = new Array(this.size);
      for (let i = 0; i < board.length; i++) {
        board[i] = new Array(this.size);
      }
      // Fill board with empty spaces
      for (let i = 0; i < board.length; i++) {
        for (let j = 0; j < board[i].length; j++) {
          board[i][j] = " "
          // { value:Math.floor(Math.random()*5)+1 }
        }
      }
      return board
    },
    update_board(board, coords) {
      console.log(board, coords);
      board[coords.row][coords.column] != " " ? null : board[coords.row][coords.column] = this.player
      this.player == "x" ? this.player = "o" : this.player = "x"
      return board
    }
  },
  onMounted: {
    // lets see after
  }
}

</script>

<template>
  <header>
    <div class="wrapper">
    </div>
  </header>
  <Board :items="create_board()" :update_board="update_board" :player="player" />
</template>

<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
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
