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
        <!-- ③クリックしたらcheckPutableの関数を呼び出す。クリックした座標をx-1,y-1として渡す。（x - 1, y - 1）なのは、配列が０から始まるから。※X➡1~8, Y➡1~8をlenghtで定義済-->
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
      checkPutable (x, y) { // 上記の@click="checkPutableのx-1(0~7)とy-1(0~7)をもってきている。スコープ（ラベル）が同じ変数は値を持ってくる"
        this.board = JSON.parse(JSON.stringify(this.board))
        let putable = false
        const turn = this.turn
        const board = this.board
        const comfirmedArray = [] // 確定したものの配列

        if (board[y][x] === 0) { // クリックした場所
          const candidates = [] // めくれるかもしれない（５０％の配列）
          for (let i = 1; i < 9; i++) {
            if (board[y][x + i] === 0) {
              break
            } else if (board[y][x + i] === 1) {
              candidates.push({ a: x + i, b: 4 })
            } else if (board[y][x + i] === -1) {
              putable = true
              comfirmedArray.push(...candidates)
            }
          }
        }
        // ☝色変ができるか確認
        // 👇色を変える処理
        // console.log(comfirmedArray)
        if (putable === true) {
          for (const key in comfirmedArray) {
            const value = comfirmedArray[key]
            console.log(value)
          }
          this.turn = -turn // ターンの変更
        } else {
          console.log('ここにはおけません！')
        }
      }
    }
  }
  // 色の変更のみを行う
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
