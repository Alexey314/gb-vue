<template>
  <div>
    <h1>{{ msg }}</h1>
    <input v-model.number="operands[0]"/>&nbsp;
    <input v-model.number="operands[1]"/> = {{result}}
    <div :class="$style.btn_container">
      <button :class="$style.button" @click="calculate('+')">+</button>
      <button :class="$style.button" @click="calculate('-')">-</button>
      <button :class="$style.button" @click="calculate('/')">/</button>
      <button :class="$style.button" @click="calculate('*')">*</button>
      <button :class="$style.button" @click="calculate('**')">x<sup>y</sup></button>
      <button :class="$style.button" @click="calculate('//')">int /</button>
    </div>
    <input id="vkcheckbox" type="checkbox" v-model="showVirtKeyb"/>
    <label for="vkcheckbox">Отобразить экранную клавиатуру</label>
    <div v-show="showVirtKeyb">
      <div :class="$style.btn_container">
        <button :class="$style.button" v-for="(n,i) in 10" :key="i" @click="onVirtKeyClick(`${i}`)">{{i}}</button>
        <button :class="$style.button" @click="onVirtKeyClick('Backspace')">&lt;-</button>
      </div>
      <div :class="$style.btn_container">
        <input type="radio" id="radio1" value="0" v-model="inputOperandNum">
        <label for="radio1">Операнд 1</label>
        <input type="radio" id="radio2" value="1" v-model="inputOperandNum">
        <label for="radio2">Операнд 2</label>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Calculator',
  data: () => ({
    operands: [0, 0],
    result: 0,
    showVirtKeyb: true,
    inputOperandNum: '0'
  }),
  props: {
    msg: String
  },
  methods: {
    calculate (operation) {
      const opMap = {
        '+': () => this.operands[0] + this.operands[1],
        '-': () => this.operands[0] - this.operands[1],
        '/': () => this.operands[0] / this.operands[1],
        '*': () => this.operands[0] * this.operands[1],
        '**': () => this.operands[0] ** this.operands[1],
        '//': () => (((this.operands[0] | 0) / (this.operands[1] | 0)) | 0)
      }
      this.result = opMap[operation]()
    },
    onVirtKeyClick (key) {
      const idx = +this.inputOperandNum
      this.$set(this.operands, idx, (key === 'Backspace')
        ? `${this.operands[idx]}`.slice(0, -1)
        : Number(`${this.operands[idx]}` + key))
    }
  }
}
</script>

<style module lang="scss">
.btn_container {
  display: flex;
  justify-content: center;
  align-items: center;
}
.button {
  display: block;
  box-sizing: border-box;
  margin: 8px;
  min-width: 32px;
  height: 32px;
}
</style>
