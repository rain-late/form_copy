<template>
  <div ref="boardBox" class="sign-canvas-box boardBox">
    <canvas
      ref="board"
      @mousedown="pcStart"
      @mousemove="pcMove"
      @mouseup="pcEnd"
    />
  </div>
</template>

<script>
export default {
  name: 'CUSTOMCANVAS',
  data() {
    return {
      ctx: null,
      point: {
        x: 0,
        y: 0
      },
      moving: false // 是否正在绘制中且移动
    }
  },
  mounted() {
    const { board } = this.$refs // 获取DOM
    board.width = this.$refs.boardBox.offsetWidth // 设置画布宽
    board.height = this.$refs.boardBox.offsetHeight // 设置画布高
    this.ctx = board.getContext('2d') // 二维绘图
    this.ctx.strokeStyle = '#ff0000' // 颜色
    this.ctx.lineWidth = 5 // 线条宽度
  },
  methods: {
    // 鼠标按下(开始)
    pcStart(e) {
      debugger
      const x = e.offsetX; const
        y = e.offsetY // 获取鼠标在画板（canvas）的坐标
      this.point.x = x
      this.point.y = y
      this.ctx.beginPath()
      this.moving = true
    },
    // 鼠标移动（移动中...）
    pcMove(e) {
      if (this.moving) {
        const x = e.offsetX; const
          y = e.offsetY // 获取鼠标在画板（canvas）的坐标
        this.ctx.moveTo(this.point.x, this.point.y) // 把路径移动到画布中的指定点，不创建线条(起始点)
        this.ctx.lineTo(x, y) // 添加一个新点，然后创建从该点到画布中最后指定点的线条，不创建线条
        this.ctx.stroke() // 绘制
        this.point.x = x
        this.point.y = y // 重置点坐标为上一个坐标
      }
    },
    // 鼠标松开（结束）
    pcEnd() {
      if (this.moving) {
        this.ctx.closePath() // 停止绘制
        this.moving = false // 关闭绘制开关
      }
    }
  }
}
</script>
<style lang="scss" scoped>
.boardBox {
  // width: 600px;
  height: 200px;
  background: #eee;
}
</style>
