<template>
  <div class="calculator">
    <div class="display">{{ current || 0 }}</div>
    <div class="btn" @click="clear">AC</div>
    <div class="btn" @click="sign">+/-</div>
    <div @click="percent" class="btn">%</div>
    <div class="btn operator" @click="divide">÷</div>
    <div @click="addNum(7)" class="btn">7</div>
    <div @click="addNum(8)" class="btn">8</div>
    <div @click="addNum(9)" class="btn">9</div>
    <div class="btn operator" @click="times">×</div>
    <div @click="addNum(4)" class="btn">4</div>
    <div @click="addNum(5)" class="btn">5</div>
    <div @click="addNum(6)" class="btn">6</div>
    <div class="btn operator" @click="minus">-</div>
    <div @click="addNum(1)" class="btn">1</div>
    <div @click="addNum(2)" class="btn">2</div>
    <div @click="addNum(3)" class="btn">3</div>
    <div class="btn operator" @click="add">+</div>
    <div @click="addNum(0)" class='btn zero'>0</div>
    <div @click="dot" class="btn">.</div>
    <div @click="equal" class="btn operator">=</div>
  </div>
</template>

<script>
export default {
  name: 'Calculator',
  data() {
    return {
      current: '',
      previous: null,
      operator: null,
      operatorClicked: false,
    };
  },
  methods: {
    clear() {
      this.current = '';
    },
    sign() {
      if (this.current.charAt(0) === '' || this.previous.charAt(0) === '') {
        this.current = '';
      } else if (this.current.charAt(0) === '-' || this.previous.charAt(0) === '-') {
        this.current = this.current.split('').splice(1).join('');
      } else {
        this.current = `-${this.current}`;
      }
    },
    percent() {
      this.current /= 100;
    },
    addNum(num) {
      if (this.operatorClicked) {
        this.current = '';
        this.operatorClicked = false;
      }
      this.current += num;
    },
    dot() {
      if (this.current.includes('.')) {
        this.current.split('').splice(-1).join('');
      } else {
        this.current += '.';
      }
    },
    add() {
      this.previous = parseFloat(this.current);
      this.operator = (a, b) => a + b;
      this.operatorClicked = true;
    },
    divide() {
      this.previous = parseFloat(this.current);
      this.operator = (a, b) => a / b;
      this.operatorClicked = true;
    },
    times() {
      this.previous = parseFloat(this.current);
      this.operator = (a, b) => a * b;
      this.operatorClicked = true;
    },
    minus() {
      this.previous = parseFloat(this.current);
      this.operator = (a, b) => a - b;
      this.operatorClicked = true;
    },
    equal() {
      this.current = this.operator(parseFloat(this.previous), parseFloat(this.current));
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">
body {
  margin: 0;
}
div.calculator {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  margin: 60px auto;
  width: 250px;
  text-align: center;
  border-radius: 10px;
  .display {
    grid-column: 1/5;
    background: rgb(43, 43, 43);
    font-size: 40px;
    color: #fff;
    width: 100%;
  }
  .btn {
    padding: 10px;
    background: #E0DFE1;
    border: 1px solid rgb(116, 116, 116);
    font-size: 19px;
    &:hover {
      cursor: pointer;
    }
  }
  .zero {
    grid-column: 1/3;
  }
  .operator {
    background: #F09238;
        color: #fff;
  }
}
</style>
