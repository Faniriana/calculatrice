<template>
  <div class="calculator"><center>
    <center><div class="soratra"><span style="color: aqua;">C</span><span style="color: red;">A</span><span style="color: rgb(202, 191, 191);">L</span><span style="color: purple;">C</span><span style="color: yellow;">U</span><span style="rgb(53, 48, 48);">L</span><span style="color: burlywood;">A</span><span style="color: navy;">T</span><span style="color: aquamarine;">R</span><span style="color: red;">I</span><span style="color: pink;">C</span>E</div></center>
    <div class="display">{{ displayValue }}</div>
    <div class="buttons">
      <button id="operateurs" @click="clear">C</button>
      <button id="operateurs"  @click="operation('/')">/</button>
      <button id="operateurs"  @click="operation('*')">*</button>
      <button  id="operateurs" @click="operation('-')">-</button>
      <button id="operateurs" @click="operation('+')">+</button><br>
      <button @click="addDigit('7')">7</button>
      <button @click="addDigit('8')">8</button>
      <button @click="addDigit('9')">9</button>
      <button @click="addDigit('4')">4</button>
      <button @click="addDigit('5')">5</button><br>
      <button @click="addDigit('6')">6</button>
      <button @click="addDigit('1')">1</button>
      <button @click="addDigit('2')">2</button>
      <button @click="addDigit('3')">3</button>
      <button @click="addDigit('0')">0</button><br>
      <button id="operateurs"  @click="deleteLastDigit">DEL</button>
      <button id="operateurs"  @click="equals">=</button>
    </div></center>
  </div>
</template>


<script>
import { evaluate } from 'mathjs'

export default {
  data() {
    return {
      displayValue: '0',
      currentValue: '0',
      currentOperation: null
    }
  },
  methods: {
    addDigit(digit) {
      if (this.currentOperation) {
        this.displayValue += digit
        this.currentValue = this.displayValue
      } else {
        this.currentValue = this.currentValue === '0' ? digit : this.currentValue + digit
        this.displayValue = this.currentValue
      }
    },
    deleteLastDigit() {
      if (this.currentValue.length > 1) {
        this.currentValue = this.currentValue.slice(0, -1)
        this.displayValue = this.currentValue
      } else {
        this.currentValue = '0'
        this.displayValue = '0'
      }
    },
    operation(op) {
      if (this.currentOperation) {
        this.equals()
      }
      this.currentOperation = op
      this.displayValue += op
    },
    equals() {
      try {
        this.currentValue = String(evaluate(this.displayValue))
        this.displayValue = this.currentValue
        this.currentOperation = null
      } catch (error) {
        this.displayValue = 'syntaxe error'
      }
    },
    clear() {
      this.currentValue = '0'
      this.displayValue = '0'
      this.currentOperation = null
    }
    
  }
}
</script>

