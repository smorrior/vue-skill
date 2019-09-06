<template>
  <div class="mob">
    <img src="../assets/samsung.png">
    <div class="displayMob">
      <div class="display">
          {{current || '0' }}
      </div>
      <div class="calculator">
        <div @click="clear" class="btn colored">C</div>
        <div @click="sign" class="btn colored">+/-</div>
        <div @click="percent" class="btn colored">%</div>
        <div @click="divide" class="btn colored">/</div>
        <div @click="append('7')" class="btn">7</div>
        <div @click="append('8')" class="btn">8</div>
        <div @click="append('9')" class="btn">9</div>
        <div @click="times" class="btn colored">x</div>
        <div @click="append('4')" class="btn">4</div>
        <div @click="append('5')" class="btn">5</div>
        <div @click="append('6')" class="btn">6</div>
        <div @click="minus" class="btn colored">-</div>
        <div @click="append('1')" class="btn">1</div>
        <div @click="append('2')" class="btn">2</div>
        <div @click="append('3')" class="btn">3</div>
        <div @click="plus" class="btn colored">+</div>
        <div @click="append('0')" class="btn">0</div>
        <div @click="dot" class="btn colored">.</div>
        <div @click="equal" class="btn double colored">=</div>
      </div>
    </div>
  </div>
</template>
<script>
  export default {
    data() {
      return {
        previous: null,
        current:'',
        operator: null,
        operatorClicked: false
      }
    },
    methods: {
      clear() {
        this.current = '';
      },
      sign() {
        this.current = this.current.charAt(0) === '-' ? this.current.slice(1) : `-${this.current}`;
      },
      percent() {
        this.current = `${parseFloat(this.current) / 1000}`;
      },
      append(number) {
        if (this.operatorClicked) {
          this.current = '';
          this.operatorClicked = false;
        }
        this.current = `${this.current}${number}`;
      },
      dot(){
        if (this.current.indexOf('.') === -1) {
          this.append('.');
        }
      },
      setPrevious() {
        this.previous = this.current;
        this.operatorClicked = true;
      },
      times(){
        this.operator = (a, b) => a * b;
        this.setPrevious();
      },
      divide(){
        this.operator = (a, b) => a / b;
        this.setPrevious();
      },
      plus(){
        this.operator = (a, b) => a + b;
        this.setPrevious();
      },
      minus(){
        this.operator = (a, b) => a - b;
        this.setPrevious();
      },
      equal() {
        this.current = `${this.operator(
          parseFloat(this.current), 
          parseFloat(this.previous)
        )}`;
        this.previous = null;
      }
    }
  }
</script>
<style lang="scss">
  body {
    background-color: #e2e2e2;
  }
  .mob{
    position: relative;
    width: 390px;
    height: 817px;
    margin: 0 auto;
    
  }
  .displayMob {
    position: absolute;
    top: 17px;
    left: 8px;
    right: 8px;
    bottom: 24px;
    background-color:#1f1f1f;
    border-radius: 30px;
    box-shadow: inset -57px -47px 56px -31px rgba(61,61,61,1);
  }
  .calculator {
    font-size: 30px;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-auto-rows: minmax(50px, auto);
    grid-gap: 2px;
    border-radius: 10px;
    padding: 25px;
  }
  .display {
    height: 380px;
    grid-column: 1 / 5;
    border-radius: 27px 27px 150px 0;
    background-color: #e0fffa;
    font-size: 30px;
  }
  .btn {
    color:#969696;
    line-height: 65px;
    cursor:pointer;
   
    &.double {
      grid-column: 3 / 5;
    }
    &.colored {
    color:#34ffde;
    }
  }
  .btn.double.colored {
    color: #f46c36;s
  }
</style>
