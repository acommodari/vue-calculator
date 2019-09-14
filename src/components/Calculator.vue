<template>
  <div class="calculator">
    <div class="display">{{ current || "0" }}</div>
    <div class="btn operator" @click="clear">AC</div>
    <div class="btn operator" @click="sign">±</div>
    <div class="btn operator" @click="percent">%</div>
    <div class="btn operator" @click="divide">÷</div>
    <div class="btn" @click="append('7')">7</div>
    <div class="btn" @click="append('8')">8</div>
    <div class="btn" @click="append('9')">9</div>
    <div class="btn operator" @click="multiply">×</div>
    <div class="btn" @click="append('4')">4</div>
    <div class="btn" @click="append('5')">5</div>
    <div class="btn" @click="append('6')">6</div>
    <div class="btn operator" @click="substract">−</div>
    <div class="btn" @click="append('1')">1</div>
    <div class="btn" @click="append('2')">2</div>
    <div class="btn" @click="append('3')">3</div>
    <div class="btn operator" @click="add">+</div>
    <div class="btn zero" @click="append('0')">0</div>
    <div class="btn" @click="dot">.</div>
    <div class="btn operator" @click="equal">=</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      previous: null,
      current: "",
      operator: null,
      isOperatorClicked: false
    };
  },
  methods: {
    clear() {
      this.current = "";
    },
    sign() {
      this.current = `${parseFloat(this.current) * -1}`;
    },
    percent() {
      this.current = `${parseFloat(this.current) / 100}`;
    },
    append(number) {
      if (this.isOperatorClicked) {
        this.current = "";
        this.isOperatorClicked = false;
      }
      this.current = `${this.current}${number}`;
    },
    dot() {
      if (!this.current.includes(".")) {
        this.append(".");
      }
    },
    setPrevious() {
      this.previous = this.current;
      this.isOperatorClicked = true;
    },
    divide() {
      this.operator = (a, b) => a / b;
      this.setPrevious();
    },
    multiply() {
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },
    substract() {
      this.operator = (a, b) => a - b;
      this.setPrevious();
    },
    add() {
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },
    equal() {
      this.current = `${this.operator(
        parseFloat(this.previous),
        parseFloat(this.current)
      )}`;
      this.previous = null;
    }
  }
};
</script>

<style scoped>
.calculator {
  display: grid;
  align-items: stretch;
  width: 16rem;
  margin: 0 auto;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: 4rem;
  user-select: none;
  box-shadow: 0 1rem 2rem 0 rgba(0, 0, 0, 0.3);
}

.display {
  display: flex;
  align-items: center;
  justify-content: flex-end;
  padding: 0 0.5rem;
  color: white;
  background-color: black;
  grid-column: 1 / 5;
  font-size: 3rem;
  overflow: hidden;
}

.btn {
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 2rem;
  background-color: black;
  color: white;
  border: 1px solid #474747;
}

.zero {
  display: flex;
  grid-column: 1/3;
  align-items: center;
}

.operator {
  background-color: #272727;
  color: #dfdfdf;
}
</style>
