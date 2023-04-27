<script>
export default {
  props: ['board', 'update_board']
}
</script>

<template>
   <div v-for="(row, x) in board">
      <div v-for="(cell, y) in row" 
      @click="update_board({ row: x, column: y })"
      :key="x + y"
      class="cell">
      {{ cell == 'x' ? 'X' : cell == 'o' ? 'O' : '' }}
    </div>
  </div>
</template>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Press+Start+2P&display=swap');

h1 {
  font-weight: 500;
  font-size: 2.6rem;
  top: -10px;
}

h3 {
  font-size: 1.2rem;
}

.cell {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 2rem;
  width: 2rem;
  border: 1px solid grey;
  background-color: rgb(192, 191, 191);
  color: red;
  font-size: large;
  font-family: 'Press Start 2P', cursive;
}

#blue {
  color: blue
}

#green {
  color: green
}

#red {
  color: red
}

@media (min-width: 1024px) {

  .greetings h1,
  .greetings h3 {
    text-align: left;
  }
}
</style>
