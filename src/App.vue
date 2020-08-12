<template>
  <div id="app">
    <textarea type="text" class="result" :value="calculatorExpression" readonly ></textarea>
    <div class="button-wrapper">
      <ActionButton :color="button.color" :value="button.value" :size="button.size" v-for="(button, index) in buttons" :key="index" @GetVal="AddValueToCalculation($event)"></ActionButton>
      <ActionButton color="#ff397b" value="√" size="40px" @GetVal="SquareRoot()"></ActionButton>
      <ActionButton color="#ff397b" value="sin" size="40px" @GetVal="Sinus()"></ActionButton>
      <ActionButton color="#ff397b" value="cos" size="40px" @GetVal="Cosinus()"></ActionButton>
      <ActionButton color="#ff397b" value="16" size="40px" @GetVal="Covert(16)"></ActionButton>
      <ActionButton color="#ff397b" value="8" size="40px" @GetVal="Covert(8)"></ActionButton>
      <ActionButton color="#ff397b" value="6" size="40px" @GetVal="Covert(6)"></ActionButton>
      <ActionButton color="#ff397b" value="2" size="40px" @GetVal="Covert(2)"></ActionButton>
      <ActionButton color="#ff397b" value="=" size="130px" @GetVal="Calculate()"></ActionButton>
      <ActionButton color="#ff397b" value="C" size="40px" @GetVal="Clear()"></ActionButton>
    </div>
  </div>
</template>

<script>

import ActionButton from "./components/ActionButton.vue";

export default {
  name: 'App',
  components: {
    ActionButton
  },
  data( ) {
    return {
      calculatorExpression: "0",
      buttons:[
        {
          color:"#40434d",
          value:"7",
          size:"40px"
        },
        {
          color:"#40434d",
          value:"8",
          size:"40px"
        },
        {
          color:"#40434d",
          value:"9",
          size:"40px"
        },
        {
          color:"#ff397b",
          value:"/",
          size:"40px"
        },
        {
          color:"#40434d",
          value:"4",
          size:"40px"
        },
        {
          color:"#40434d",
          value:"5",
          size:"40px"
        },
        {
          color:"#40434d",
          value:"6",
          size:"40px"
        },
        {
          color:"#ff397b",
          value:"*",
          size:"40px"
        },
        {
          color:"#40434d",
          value:"1",
          size:"40px"
        },
        {
          color:"#40434d",
          value:"2",
          size:"40px"
        },
        {
          color:"#40434d",
          value:"3",
          size:"40px"
        },
        {
          color:"#ff397b",
          value:"-",
          size:"40px"
        },
        {
          color:"#40434d",
          value:"0",
          size:"85px"
        },
        {
          color:"#ff397b",
          value:".",
          size:"40px"
        },
        {
          color:"#ff397b",
          value:"+",
          size:"40px"
        },
        {
          color:"#ff397b",
          value:"**",
          size:"40px"
        }
      ]
    }
  },
  methods: {
    AddValueToCalculation: function(val){
      
      if(this.calculatorExpression == "0"){
        this.calculatorExpression = val;
      }else{
        let checkForNan = parseInt(val); // getting value as a number
        let lastOfExpression = parseInt(this.calculatorExpression[this.calculatorExpression.length-1]); // getting last of expression string as a number

        /* Cheking for entering 2 not a number symbols in a row */

        if(isNaN(checkForNan)){  // if entered value is not a number
          if(!isNaN(lastOfExpression)){ // and last of expression string symbol is number
            this.calculatorExpression += val;
          }
        }else{
          this.calculatorExpression += val;
        }
      }
    },
    Clear: function(){
      this.calculatorExpression = "0";
    },
    Calculate: function(){
      this.calculatorExpression = eval(this.calculatorExpression);
    },
    SquareRoot: function(){
      this.calculatorExpression = Math.sqrt(parseInt(this.calculatorExpression));
    },
    Cosinus: function(){
      this.calculatorExpression = Math.cos(parseInt(this.calculatorExpression));
    },
    Sinus: function(){
      this.calculatorExpression = Math.sin(parseInt(this.calculatorExpression));
    },
    Covert: function(system){
      this.calculatorExpression = parseInt(this.calculatorExpression).toString(system);
    }
  }
}
</script>

<style>
  #app{
    margin:0 auto;
    margin-top:100px;
    width:205px;
    height:auto;
    background:#000;
    box-shadow: -4px 3px 25px 0px rgba(50, 50, 50, 0.45);
  }
  .result{
    width:100%;
    height:50px;
    border:0;
    outline:0;
    background: #282730;
    color:#fff;
    font-size:20px;
    padding:15px;
    box-sizing: border-box;
    font-family:'Courier New', Courier, monospace;
    text-align: right;
    resize: none;
  }
  .result::-webkit-scrollbar{
    width:5px;
    background:#000;
    cursor: pointer;
  }
  .result::-webkit-scrollbar-thumb{
    background:rgb(255, 57, 123);
  }
  .button-wrapper{
    display:flex;
    flex-wrap: wrap;
    width:100%;
    padding:10px;
    box-sizing: border-box;
    margin:0 auto;
  }
</style>