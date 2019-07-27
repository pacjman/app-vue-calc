
<template>
  <div id="app">
    <h1>Calculator Demo</h1>

    <!--  https://github.com/salazarr-js/v-calculator  -->

    <div id="calculator">

      <div>
        <img width="320" src="pacjman.jpg"/>
      </div>

      <div class="calculator-logs">
        <span v-for="log in logs">{{ log }}</span>
      </div>

      <input type="string" class="calculator-input" v-model="value" @keyup.enter="pop()">

      <div class="calculator-row">
        <div class="calculator-col">
          <button class="calculator-btn gray action" @click="reset()">AC</button>
        </div>
        <div class="calculator-col">
          <button class="calculator-btn gray action" @click="clear()">C</button>
        </div>
        <div class="calculator-col">
          <button class="calculator-btn gray action" @click="push('%')">%</button>
        </div>
        <div class="calculator-col">
          <button class="calculator-btn accent action" @click="push('/')">÷</button>
        </div>
      </div>

      <div class="calculator-row">
        <div class="calculator-col">
          <button class="calculator-btn" @click="push(7)">7</button>
        </div>
        <div class="calculator-col">
          <button class="calculator-btn" @click="push(8)">8</button>
        </div>
        <div class="calculator-col">
          <button class="calculator-btn" @click="push(9)">9</button>
        </div>
        <div class="calculator-col">
          <button class="calculator-btn accent action" @click="push('*')">x</button>
        </div>
      </div>

      <div class="calculator-row">
        <div class="calculator-col">
          <button class="calculator-btn" @click="push(4)">4</button>
        </div>
        <div class="calculator-col">
          <button class="calculator-btn" @click="push(5)">5</button>
        </div>
        <div class="calculator-col">
          <button class="calculator-btn" @click="push(6)">6</button>
        </div>
        <div class="calculator-col">
          <button class="calculator-btn accent action" @click="push('-')">-</button>
        </div>
      </div>

      <div class="calculator-row">
        <div class="calculator-col">
          <button class="calculator-btn" @click="push(1)">1</button>
        </div>
        <div class="calculator-col">
          <button class="calculator-btn" @click="push(2)">2</button>
        </div>
        <div class="calculator-col">
          <button class="calculator-btn" @click="push(3)">3</button>
        </div>
        <div class="calculator-col">
          <button class="calculator-btn accent action" @click="push('+')">+</button>
        </div>
      </div>

      <div class="calculator-row">
        <div class="calculator-col wide">
          <button class="calculator-btn" @click="push(0)">0</button>
        </div>
        <div class="calculator-col">
          <button class="calculator-btn action" @click="push('.')">.</button>
        </div>
        <div class="calculator-col">
          <button class="calculator-btn accent action" @click="pop()">=</button>
        </div>
      </div>
    </div>

  </div>
</template>

<script lang="ts">

  import Vue from 'vue';
  import Component from 'vue-class-component';

  @Component({
    components: { }
  })

  export default class App extends Vue {
    
    expr: string = '';
    logs: string[] = [];

    constructor() {
      super();

      this.expr = '';
      this.logs = LogRepo.Get();
    }

    reset(): void {

      this.expr = '';
      this.logs = [];

      LogRepo.Put(this.logs);
    }

    push(e: string): void {

      if ( Util.IsNumber(e) ) {

        if ( this.expr.length == 0 ) {
          this.expr = e.toString();
        } else {
          this.expr += e.toString();
        }

      } else {

        if ( this.expr.length == 0) {
          return;
        } else {

          let prev = this.expr[this.expr.length - 1];
          if ( Util.IsOperator(prev) ) {
            this.expr = this.expr.slice(0, -1);
          }
            
          this.expr += e.toString();
        }
      }
    }

    pop(): void {

      let log: string = this.expr;
      this.expr = eval(this.expr).toString();

      if (log != this.expr) {
        this.logs.push( log + `=${this.expr}` );
        LogRepo.Put(this.logs);
      }

    }

    clear(): void {
      this.expr = '';
    }
    
    get value(): string {

      return this.expr.length > 0
        ? this.expr
        : "0"
        ;

    }

  }

  class Util {

    static IsNumber(e: any): boolean {
      return ( Number.isInteger(e) );
    }

    static IsOperator(e: string): boolean {
      return ( e == "%" || e == "/" || e == "*" || e == "-" || e == "." );
    }

  }

  class LogRepo {

    static Get(): string[] {

      let logStr = window.localStorage.getItem('logs');
      if (logStr === null) {
        LogRepo.Put([]);
        return [];
      }

      let logObj = JSON.parse(logStr);
      return logObj;

    }

    static Put(value : string[]) {

      let logStr = JSON.stringify(value);
      window.localStorage.setItem('logs', logStr);

    }

  }


</script>

<style>

  *, ::after, ::before {
    box-sizing: border-box;
  }

  body {
    margin: 0;
    height: 100vh;
    display: flex;
    font-size: 10px;
    align-items: flex-end;
    justify-content: center;
    background-color: #333;
  }

  #calculator {
    width: 100%;
    margin: 0 auto;
    display: flex;
    padding: 0;
    max-width: 320px;
    min-width: 320px;
    flex-direction: column;
    background-color: #2f2f31;
  }

  #calculator .calculator-logs {
    height: 80px;
    display: flex;
    position: relative;
    overflow: hidden;
    align-items: flex-end;
    flex-direction: column;
    justify-content: flex-end;
    background-color: #ccc;
  }
  #calculator .calculator-logs:before {
    top: 0;
    left: 0;
    right: 0;
    height: 48px;
    content: '';
    z-index: 5;
    position: absolute;
    background: linear-gradient(to bottom, #2f2f31, rgba(47, 47, 49, 0));
  }
  #calculator .calculator-logs span {
    color: #333;
    opacity: .75;
    display: block;
    font-size: .8rem;
    text-align: right;
    margin-top: .4rem;
    line-height: 1;
    font-weight: lighter;
  }
  #calculator .calculator-input {
    color: #333;
    width: 100%;
    border: none;
    padding: .8rem;
    display: block;
    font-size: 2.4rem;
    background-color: #b3ffe0;
    text-align: right;
    font-weight: lighter;
  }
  #calculator .calculator-input:focus, #calculator .calculator-input:active {
    outline: none;
  }
  #calculator .calculator-row {
    display: flex;
    padding: 0;
    justify-content: space-around;
  }
  #calculator .calculator-row .calculator-col {
    flex: 1;
    box-shadow: 0 0 0 1px #2f2f31;
  }
  #calculator .calculator-row .calculator-col.wide {
    flex: 2;
  }
  #calculator .calculator-btn {
    width: 100%;
    color: #D4D4D2;
    border: none;
    cursor: pointer;
    padding: .8rem;
    outline: none;
    font-size: 1.6rem;
    transition: all .3s ease-in-out;
    font-weight: 200;
    justify-content: center;
    background-color: #616163;
  }
  #calculator .calculator-btn.accent {
    background-color: #f49e3f;
    color: #fff;
  }
  #calculator .calculator-btn.gray {
    background-color: #424345;
  }
  #calculator .calculator-btn:active {
    background-color: #2f2f31;
  }

</style>
