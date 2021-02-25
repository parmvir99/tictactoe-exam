<template lang="html">
  <div class="container p-5">
    <div class="">
      <div class="d-flex justify-content-between">
        <div class="player">
            <h1>
            <h3 class="fw-bold text-success" v-if="winner && winner === 'X'">WINNER!</h3>
              X
            <span v-if="player === 'X' && !winner">^</span>
            </h1>
        </div>
        <div class="player">
          <h2 class="fw-bold text-warning" v-if="winner === 'draw'">DRAW!</h2>
        </div>
        <div class="player">
          <h1>
            <h3 class="fw-bold text-success" v-if="winner && winner === 'O'">WINNER!</h3>
            O
            <span v-if="player === 'O' && !winner">^</span>
          </h1>
        </div>
      </div>
    </div>
    <div class="d-grid place-items-center pt-5">
      <div>
        <div v-for="(_, x) in 3" :key="x" class="row">
          <div :class="{ 'pointer-none': squares[x][y] !== '', 'text-success': checkWinningCells[x][y], 'cell': true }" v-for="(_, y) in 3" :key="y" @click="move(x, y)">
            {{ squares[x][y] }}
          </div>
        </div>
      </div>
    </div>
    <div class="text-center mt-5 pt-5">
      <button class="btn btn-light fw-bold btn-sm" type="button" name="button" @click="reset">Reset Board</button>
    </div>
  </div>
</template>

<script>
export default {
  name:'tictactoe',
  data () {
    return {
      test: null,
      winningCells: null,
      addClass: null,
      player: 'X',
      squares: [
        ['', '', ''],
        ['', '', ''],
        ['', '', '']
      ],
      checkWinningCells: [
        ['', '', ''],
        ['', '', ''],
        ['', '', '']
      ]
    }
  },
  computed: {
    winner () {
      return this.calculateWinner(this.squares.flat())
    }
  },
  methods: {
    move (x, y) {
      if (this.winner) return
      this.squares[x][y] = this.player
      this.player = this.player === 'O' ? 'X' : 'O'
    },
    reset () {
      this.player = 'X'
      this.squares = [
        ['', '', ''],
        ['', '', ''],
        ['', '', '']
      ]
      this.checkWinningCells = [
        ['', '', ''],
        ['', '', ''],
        ['', '', '']
      ]
    },

    calculateWinner (squares) {
      const lines = [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],
        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8],
        [0, 4, 8],
        [2, 4, 6]
      ]
      for (let i = 0; i < lines.length; i++) {
        const [a, b, c] = lines[i]
        if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c]) {
          const cells = [a, b, c]
          this.highlight(cells)
          return squares[a]
        }
      }

      if (!squares.includes('')) {
        return 'draw'
      }
      return null
    },

    highlight (cells) {

      this.checkWinningCells = [
        ['', '', ''],
        ['', '', ''],
        ['', '', '']
      ]
      for (let i = 0; i < cells.length; i++) {
        switch (cells[i]) {
          case 0:
            this.checkWinningCells[0][0] = true
            break
          case 1:
            this.checkWinningCells[0][1] = true
            break
          case 2:
            this.checkWinningCells[0][2] = true
            break
          case 3:
            this.checkWinningCells[1][0] = true
            break
          case 4:
            this.checkWinningCells[1][1] = true
            break
          case 5:
            this.checkWinningCells[1][2] = true
            break
          case 6:
            this.checkWinningCells[2][0] = true
            break
          case 7:
            this.checkWinningCells[2][1] = true
            break
          case 8:
            this.checkWinningCells[2][2] = true
            break
        }
      }
    },
  }
}
</script>

<style lang="css">
.cell {
  padding:0 !important;
  display:grid;
  place-items:center;
  color:#e0dbd1;
  font-size:100px;
  height:130px;
  width:150px !important;
  line-height:0;
  cursor: pointer;
}
.cell + .cell {
  border-left: 4px solid #8b8b8b;
}
.row + .row {
  border-top: 4px solid #8b8b8b;
}
.place-items-center {
  place-items:center;
}
.text-chalk {
  color:#e0dbd1;
}
.pointer-none {
  pointer-events: none;
}
.player h2 {
  letter-spacing: 4px;
}
.player h3 {
  position: absolute;
  top: -22px;
  letter-spacing: 3px;
  transform: rotate(-20deg);
  left: 30px;
  font-size:20px;
}
.player h1 {
  font-size:70px !important;
  line-height:1;
  position:relative;
}
.player h1 span {
  position:absolute;
  right: 5px;
  bottom: -15px;
}

.player h1 span {
  animation: shake infinite 1500ms cubic-bezier(.36,.07,.19,.97) both;
  transform: translate3d(0, 0, 0);
  backface-visibility: hidden;
  perspective: 1000px;
}

button {
  letter-spacing: 3px;
}

@keyframes shake {
  10%, 90% {
    transform: translate3d(-1px, 0, 0);
  }

  20%, 80% {
    transform: translate3d(2px, 0, 0);
  }

  30%, 50%, 70% {
    transform: translate3d(-4px, 0, 0);
  }

  40%, 60% {
    transform: translate3d(4px, 0, 0);
  }
}
</style>
