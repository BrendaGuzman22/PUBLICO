# Guzman Arevalo
<template>
 <div id="app">
 <h1 class = "title">Brenda Rocio Guzman Arevalo</h1>
 <h2 > aplication de calculadora</h2>
 <div class ="calculador">
 <input type="text" class ="result" readonly />
 <div class="bottons">
 <button class="Number" @click="handleClick ('7')">7</ button>
 <button class="Number" @click="handleClick ('8')">8</ button>
 <button class="Number" @click="handleClick ('9')">9</ button>
 <button class="operator" @click="handleOperatorClick"('/')">/</button>

 <button class="Number"@click="handleClick ('4')">4/</button>
 <button class="Number" @click="handleClick('5')">5/</button>
 <button class="Number" @click="handleClick('6')">6/</button>
 <button  class="operator" @click="handleOperatorClick('*')">*</button><>

<button class="number" @click="handleClick ('1')">1/</button>
<button class="number" @click="handleClick ('2')">2/</button>
<button class="number" @click="handleClick ('3')">3/</button>
<button class="operator" @click="handleClick ('-')">-</button>

<button class="number" @click="handleclink ('0')" >0</button>
<button class="number" @click="handleclink ('.')" >.</button>
<button class="number" @click="handleclink ('00')">00</button>

<button class="operator" @clink="handleOperatorClick ('+')">+</button>

<button class="clear"@click="handleClear">c</button>
<button class="clear"@click="handleClearEntry">CE</button>
<button class="equal" @click="calculate()">=</button>
 </div>
 </div>
 </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      result: '',
      calculated: false
      // Flag to track if calculation has been done
    };
  },
  methods: {
    handleClick(value) {
      if (this.calculated) {
        // If calculation has been done, 
        // start a new expression
        this.result = value;
        this.calculated = false; // Reset flag
      } else {
        this.result += value;
      }
    },
    handleClear() {
      this.result = '';
      this.calculated = false; // Reset flag
    },
    handleClearEntry() {
      if (this.result && this.result.length > 0) {
        this.result = this.result.slice(0, -1);
        if (this.result.length === 0) {
          this.handleClear();
        }
      } else {
        this.handleClear();
      }
    },
    handleOperatorClick(operator) {
      // If the last character is an operator, 
      // replace it with the new operator
      if (/[+*/-]$/.test(this.result)) {
        this.result = this.result.slice(0, -1) + operator;
      } else {
        // Otherwise, add the new operator
        this.result += operator;
      }
      this.calculated = false; // Reset flag
    },
    calculate() {
      try {
        let evaluatedResult = eval(this.result.replace(/(^|[^0-9])0+(\d+)/g, '$1$2'));
        if (evaluatedResult === Infinity || evaluatedResult === -Infinity) {
          throw new Error('Division por cero');
        }
        this.result = Number.isFinite(evaluatedResult) ? evaluatedResult : 'Error';
        this.calculated = true;
        // Set flag to true after calculation
      } catch (error) {
        if (error.message === 'Division por cero') {
          this.result = 'Error: División por cero';
        } else {
          this.result = 'Error';
        }
      }
    }
  }
};

</script>
<style src="./calculadora.css"
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style> 
