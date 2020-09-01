<template>
  <div class="calculator">
    <div class="display"> {{ current || 0 }} </div>
    <div v-on:click="clear" class="btn">C</div>
    <div v-on:click="sign" class="btn">+/-</div>
    <div v-on:click="percent" class="btn">%</div>
    <div v-on:click="divide" class="btn operator">/</div>
    <div v-on:click="append('7')" class="btn">7</div>
    <div v-on:click="append('8')" class="btn">8</div>
    <div v-on:click="append('9')" class="btn">9</div>
    <div v-on:click="times" class="btn operator">x</div>
    <div v-on:click="append('4')" class="btn">4</div>
    <div v-on:click="append('5')" class="btn">5</div>
    <div v-on:click="append('6')" class="btn">6</div>
    <div v-on:click="minus" class="btn operator">-</div>
    <div v-on:click="append('1')" class="btn">1</div>
    <div v-on:click="append('2')" class="btn">2</div>
    <div v-on:click="append('3')" class="btn">3</div>
    <div v-on:click="add" class="btn operator">+</div>
    <div v-on:click="append('0')" class="btn zero">0</div>
    <div v-on:click="sqrt" class="btn sqrt">√</div>
    <div v-on:click="dot" class="btn">.</div>
    <div v-on:click="equal" class="btn operator">=</div>
    <div v-on:click="pi" class="btn">𝛑</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      current: '',
      previous: null,
      operator: null,
      operatorClicked: false
    }
  },
  methods: {
    clear: function () {
      this.current = '';
    },
    sign: function () {
      this.current = this.current.charAt(0) === '-' ? this.current.slice(1) : `-${this.current}`;
    },
    percent: function () {
      this.current = `${parseFloat(this.current) / 100}`
    },
    sqrt: function () {
      this.current = `${parseFloat(Math.sqrt(this.current).toFixed(2))}`
    },
    pi: function () {
      this.current = `${parseFloat(Math.PI).toFixed(2)}`
    },
    append: function (n) {
      if (this.operatorClicked) {
        this.current = '';
        this.operatorClicked = false;
      }
      this.current = `${this.current}${n}`;
    },
    dot: function () {
      if (this.current.indexOf('.') === -1) this.append('.');
    },
    setPrevious: function () {
      this.previous = this.current;
      this.operatorClicked = true;
    },
    divide: function () {
      this.operator = (a, b) => a / b;
      this.setPrevious();
    },
    times: function () {
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },
    minus: function () {
      this.operator = (a, b) => a - b;
      this.setPrevious();
    },
    add: function () {
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },
    equal() {
      this.current = `${this.operator(parseFloat(this.previous), parseFloat(this.current))}`
      this.previous = null
    }
  }
}
</script>

<style scoped>
.calculator {
  width: 400px;
  margin: 0 auto;
  font-size: 30px;
  line-height: 40px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
}
.display {
  grid-column: 1 / 5;
  background-color: #333;
  color: white;
  text-align: right;
  padding: 25px 10px 0 0;
  font-size: 50px;
  height: 60px;
}
.btn {
  cursor: pointer;
  padding-top: 5px;
  background-color: #eee;
  border: 1px solid #999;
}
.btn:hover {
  background-color: #fff;
  border: 1px solid #999;
}
.operator {
  background-color: orange;
  color: white;
}
.operator:hover {
  background-color: orangered;
  color: #222222;
}
</style>