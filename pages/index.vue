<template>
  <div class="othello-box">
    <template v-for="y in board.length">
      <div
        v-for="x in board.length"
        :key="`${x}-${y}`"
        class="othello-box-line"
        @click="checkPutable(x - 1, y - 1)"
      >
        <div
          v-if="board[y - 1][x - 1] !== 0"
          :class="['stone', board[y - 1][x - 1] === 1 ? 'white' : 'black']"
        />
      </div>
    </template>
  </div>
</template>

<script>
export default {
  data () {
    return {
      board: [
        [0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, -1, 1, 0, 0, 0],
        [0, 0, 0, 1, -1, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0]
      ],
      turn: -1
    }
  },
  methods: {
    checkPutable (x, y) {
      this.board = JSON.parse(JSON.stringify(this.board))
      let putable = false
      const turn = this.turn
      const board = this.board
      let candidateX
      let candidateY

      if (board[y][x] === 0) { // クリックした場所
       const candidates = [x = 1, y = 3]
       if (candidates>0) {
         for (candidates) {
           board = turn
         }
       }
      }

      if (putable === true) {
        this.board[y][x] = turn
        this.board[candidateY][candidateX] = turn
        this.turn = -turn
      } else {
        console.log('ここにはおけません！')
      }
      console.log(x, y, putable, turn)
    }
  }
}
</script>

<style>
.othello-box{
  height: 640px;
  width: 640px;
  background-color: green;
  margin: 50px auto;
}

.othello-box-line{
  height:12.5%;
  width: 12.5%;
  border: solid 1px black;
  box-sizing: border-box;
  float:left;
}

.stone{
  width: 80%;
  height: 80%;
  margin: 10%;
  border-radius: 50%;
}

.black{
  background: black;
}

.white{
  background: white;
}
</style>
