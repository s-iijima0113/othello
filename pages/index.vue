<template>
  <div class="othello-box">
    <template v-for="y in board.length">
      <!-- 配列の数を数えている（８） -->
      <div
        v-for="x in [
        [0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, -1, 1, 0, 0, 0],
        [0, 0, 0, 1, -1, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0]
      ][y - 1].length"
        :key="`${x}${y}`"
        class="othello-box-line"
        @click="checkPutable(x - 1, y - 1)"
      >
      <!-- ①配列の子要素の数を数えている(8) -->
      <!-- ②要素にラベルをはっている -->
      <!-- ③クリックしたらcheckPutableの関数を呼び出す。クリックした座標をx-1,y-1として渡す-->
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
        [0, 1, 1, -1, 1, 0, 0, 0],
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
        for (let i = 1; i < 9; i++) {
          if (board[y][x + i] !== turn) {
            break
          }
          putable = true
          candidateY = y // 色を変える候補（Y）
          candidateX = x + i // 色を変える候補（X）
        }
      }
      if (putable === true) {
        this.board[y][x] = turn
        this.board[candidateY][candidateX] = turn
        this.turn = -turn // ターンの変更
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
