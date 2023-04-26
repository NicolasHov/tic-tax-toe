<script>
export default {
  props: ['items', 'player', 'update_board']
}
</script>

<template>
  <div v-for="(item, index1) in items">
    <button class="cell" v-for="(childItem, index2) in item"
      @click="update_board(items, { row: index1, column: index2 })" :key="index1 + index2">
      <!-- <span v-if="childItem.value == 'o'" id="green">{{ player }}</span> -->
      {{ player }}
    </button>
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
  /* text-align: center; */
  height: 2rem;
  width: 2rem;
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
