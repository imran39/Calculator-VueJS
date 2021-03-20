<template>
  <div class="calculator">
    
    <div class="previous display">{{previous}}</div>
    <div class="display" >{{ result|| 0}}</div>
    <button @click="allclear" class="btn span clr"><i>AC</i></button>
    <button @click="pow()" class="btn operator"> xⁿ </button>
    <button @click="root()" class="btn operator">√</button>
    <button @click="dlt" class="btn"><b>⌫</b></button>
    <button @click="sign" class="btn">+/-</button>
    <button @click="percent" class="btn operator">%</button>
    <button @click="mult()" class="btn operator">*</button>
    <button @click="append('7')" class="btn">7</button>
    <button @click="append('8')" class="btn">8</button>
    <button @click="append('9')" class="btn">9</button> 
    <button @click="divide()" class="btn operator">÷</button>
    <button @click="append('4')" class="btn">4</button>
    <button @click="append('5')" class="btn">5</button>
    <button @click="append('6')" class="btn">6</button>
    <button @click="minus()" class="btn operator">-</button>
    <button @click="append('1')" class="btn">1</button>
    <button @click="append('2')" class="btn">2</button>
    <button @click="append('3')" class="btn">3</button>
    <button @click="add()" class="btn operator">+</button>
    <button @click="append('0')" class="btn ">0</button>
    <button @click="dot()" class="btn">.</button>
    <button @click="equal()" class="operator span eql"><b >=</b></button>
   
  </div>
</template>

<script>
export default {
  name: 'App',

  data(){
      return{
        result:'',
        previous:'',
        current:'',
        operator:null,
        operatorClicked: false,
      }
    },
    methods:{
      allclear(){
        this.current='';
        this.previous='';
        this.result='';
      },
      dlt(){
      this.current = `${this.current.slice(0, -1)}`;

      this.result = `${this.result.slice(0, -1)}`;
      },
      sign(){
      this.current = this.current.charAt(0) ==='-'?this.current.slice(1) : `-${this.current}`;
      },
      mult(){
      //this.setPrevious();
      if(this.current!==''){
        this.previous=this.current + "*";
        this.operatorClicked=true;}
      },
      divide(){
      this.operator=(a,b)=>a/b;
      //this.setPrevious();
      if(this.current!==''){  
        this.previous=this.current +"÷";
        this.operatorClicked=true;}
      },
      minus(){

      this.operator=(a,b)=>b - a;
      //this.setPrevious();
      if(this.current!==''){
        this.previous=this.current + " -";
        this.operatorClicked=true;}
      },
      add(){
      this.operator=(a,b)=>a+b;
      //this.setPrevious();
      if(this.current!==''){
        this.previous=this.current + "+";
        this.operatorClicked=true;}
      },
      equal(){
      if(this.current!==''){
        this.current=`${this.operator(parseFloat(this.current),parseFloat(this.previous))}`;}
      this.result="= " +this.current;
        
      },
      percent(){
      if(this.current!=='' && this.operatorClicked==false){
        this.current=`${parseFloat(this.current)/100}`;}
        this.result=this.current;
      },
      dot(){
      if(this.current.indexOf('.')===-1){this.append('.');}
      },
      pow(){
      this.operator=(a,b)=> Math.pow(a, b);
      //this.setPrevious();
      if(this.current!==''){
        this.previous=this.current + "^";
        this.current=0;
        this.operatorClicked=true;}
      },
      root(){
      this.operator=(a)=> Math.sqrt(a);
      if(this.current!==''){
        this.previous="√"+this.current;
        this.current='';
        this.operatorClicked=true;}


      },
      append(number){
      if(this.operatorClicked){
        this.current='';
        this.operatorClicked=false;
        }
      this.current=`${this.current}${number}`;
      this.result=this.current;
      },

      setPrevious(){
      this.previous=this.current;
      this.operatorClicked=true;
      },
    }
}
</script>

<style scoped>
.calculator {
  justify:center;
  align-content:center;
  margin: 0 auto;
  padding:100px;
  width:300px;
  font-size:30px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows:minmax(50px, auto);
  border-radius: 16px 16px 16px 16px;
}
.btn {
  font-size:30px;
  border:1px solid white;
  background-color:#F2F2F2;
  }
.display {
  column-grid:1/-1;
  justify-content: space-around;
  display:flex;
  align-items: flex-end;
  flex-direction: column;
  word-wrap: break-word;
  word-break: break-all;
  font-size:30px;
  grid-column:1/5;
  background-color:#333;
  color:white;
  padding:8px;
}
.operator{
  //background-color: rgba(125 175 226 / 75%);
  color:#606d9c;
}
.previous{
  color: rgba(125 175 226  .75);
  font-size:20px;
  grid-column:1/5;
  background-color:#333;
  color:white;
}
.extra{
  color:white;
  background-color:rgba(125 175 226 / 75%);
}
.span{
  grid-column: span 2;
}
.eql{
  color: orange;
  font-size:50px;
  border:1px solid white;
  background-color:#F2F2F2;
}
.clr{
  color: red;
}
</style>