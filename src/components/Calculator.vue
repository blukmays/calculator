<template>
 
  
<div class= "calculator">
  <div class="display">{{current || 0}}</div>
    <button @click= "clear" type="button">C</button>
    <button @click= "sign" type="button">+/-</button>
   <button @click = "percent" type="button">%</button>
   <button @click= "divide" type="button" class= "operator">&divide;</button>

   <button @click= "append(7)" type="button">7</button>
   <button @click= "append(8)" type="button">8</button>
   <button @click= "append(9)" type="button">9</button>
   <button type="button" class= "operator">&times;</button>

   <button @click= "append(4)" type="button">4</button>
   <button @click= "append(5)" type="button">5</button>
   <button @click= "append(6)" type="button">6</button>
   <button type="button" class= "operator">-</button>

   <button @click= "append(1)" type="button">1</button>
   <button @click= "append(2)" type="button">2</button>
   <button @click= "append(3)" type="button">3</button>
   <button @click= "add" type="button" class= "operator">+</button>

   <button @click= "append(0)" type="button" class= "zero">0</button>
   <button @click="dot" type="button">.</button>
   <button @click= "equal" type="button">=</button>
    </div>




</template>


<script>
export default {
    data() {
      return {
        previous: null,
        operator: null,
        operatorClicked: false,
        current: ''
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
        this.current = this.current / 100;
      },
      divide() {
        this.operator = (a,b) => a/b;
        this.previous = this.current;
        this.operatorClicked = true;
      },
      times() {
        this.operator = (a,b) => a * b;
        this.previous = this.current;
        this.operatorClicked = true;
      },
      add() {
        this.operator = (a,b) => a + b;
        this.previous = this.current;
        this.operatorClicked = true;
      },
      minus () {
        this.operator = (a,b) => a - b;
        this.previous = this.current;
        this.operatorClicked = true;
      },
      append(number) {
        if (this.operatorClicked === true) {
          this.current = '';
          this.operatorClicked = false;
        }
        this.current =
        this.current === 0
        ? (this.current = number) :
        '' + this.current + number;
      },
      dot() {
        if (this.current.indexOf('.') === -1){
          this.append('.');
        }
      },
      equal() {
      this.current = this.operator(Number(this.previous), Number(this.current));
      this.previous = null;
      this.operatorClicked = true;
      }
    }
  }
  





</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.calculator {
  margin: 0 auto;
  width: 400px;
  font-size: 40px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto)
}

.display {
  grid-column: 1/5;
  background-color: #333;
  color: white;
  border: 1px solid ;
}

.zero {
  grid-column: 1/3;
}

.button {
  background-color: #eee;
  border: 1px solid #333; 
}

.operator {
  background-color: orange; 
  color: white;
}


</style>
