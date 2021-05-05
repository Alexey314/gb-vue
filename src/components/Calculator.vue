<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <input v-model.number="operand1"/>&nbsp;
    <input v-model.number="operand2"/> = {{result}}
    <div >
      <button class="button" @click="calculate('+')">+</button>
      <button class="button" @click="calculate('-')">-</button>
      <button class="button" @click="calculate('/')">/</button>
      <button class="button" @click="calculate('*')">*</button>
      <button class="button" @click="calculate('**')">x<sup>y</sup></button>
      <button class="button" @click="calculate('//')">int /</button>
    </div>

  </div>
</template>

<script>
export default {
  name: 'Calculator',
  data: () => ({
    operand1: 0,
    operand2: 0,
    result: 0
  }),
  props: {
    msg: String
  },
  methods: {
    calculate (operation) {
      const opMap = {
        '+': () => this.operand1 + this.operand2,
        '-': () => this.operand1 - this.operand2,
        '/': () => this.operand1 / this.operand2,
        '*': () => this.operand1 * this.operand2,
        '**': () => this.operand1 ** this.operand2,
        '//': () => (((this.operand1 | 0) / (this.operand2 | 0)) | 0)
      }
      this.result = opMap[operation]()
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.button {
  box-sizing: border-box;
  margin: 8px;
  min-width: 32px;
  height: 32px;
}
</style>
