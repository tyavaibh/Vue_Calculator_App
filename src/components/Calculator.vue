<template>
    <div class="calculator">

        <div class="display">{{current || 0}}</div>

        <div @click="clear" class="btn">C</div>
        <div @click="sign" class="btn">+/-</div>
        <div @click="percent" class="btn">%</div>
        <div @click="divide" class="btn operator">/</div>

        <div @click="append(9)" class="btn">9</div>
        <div @click="append(8)" class="btn">8</div>
        <div @click="append(7)" class="btn">7</div>
        <div @click="times" class="btn operator">x</div>

        <div @click="append(6)" class="btn">6</div>
        <div @click="append(5)" class="btn">5</div>
        <div @click="append(4)" class="btn">4</div>
        <div @click="minus" class="btn operator">-</div>

        <div @click="append(3)" class="btn">3</div>
        <div @click="append(2)" class="btn">2</div>
        <div @click="append(1)" class="btn">1</div>
        <div @click="add" class="btn operator">+</div>

        <div @click="append(0)" class="zero btn">0</div>
        <div @click="dot" class="btn">.</div>
        <div @click="result" class="btn operator">=</div>
    </div>
</template>

<script>

export default {
    name:"Calculator",

    data(){
        return {
            current:"",
            operator:null,            
        }
    },

    methods:{
        clear(){
            this.current='';
        },

        sign(){
            this.current=this.current.charAt(0)==="-" ? this.current.slice(1) : `-${this.current}`
        },

        percent(){
            this.current=`${parseFloat(this.current)/100}`
        },

        append(number){
            this.current=`${this.current}${number}`
        },

        dot(){
            if(this.current.indexOf('.')===-1){
                this.append('.')
            }
        },

        divide(){
            (this.current.charAt(this.current.length-1)!=="/" ) && (this.current.charAt(this.current.length-1)!=="*" )
            && (this.current.charAt(this.current.length-1)!=="-" ) && (this.current.charAt(this.current.length-1)!=="+" )
             ? this.append('/') : null
        },

        times(){
            (this.current.charAt(this.current.length-1)!=="/" )&& (this.current.charAt(this.current.length-1)!=="*" )
            && (this.current.charAt(this.current.length-1)!=="-" ) && (this.current.charAt(this.current.length-1)!=="+" )
             ? this.append('*') : null
        },

        minus(){
            (this.current.charAt(this.current.length-1)!=="/" )&& (this.current.charAt(this.current.length-1)!=="*" )
            && (this.current.charAt(this.current.length-1)!=="-" ) && (this.current.charAt(this.current.length-1)!=="+" )
             ? this.append('-') : null
        },

        add(){
            (this.current.charAt(this.current.length-1)!=="/" )&& (this.current.charAt(this.current.length-1)!=="*" )
            && (this.current.charAt(this.current.length-1)!=="-" ) && (this.current.charAt(this.current.length-1)!=="+")
             ? this.append('+') : null
        },

        result(){
            this.current=eval(this.current).toString();
        }
    }
}
</script>

<style scoped>
.calculator{
    font-size: 35px;
    display:grid;
    grid-template-columns: repeat(4,1fr);
    grid-auto-rows: minmax(50px,auto);
    width:300px;
    margin: 0 auto;
}

.display{
    grid-column:1/5;
    background-color:rgb(56, 53, 53);
    color:white;
}

.zero{
    grid-column:1/3;
}

.btn{
    background-color: #F2F2F2;
    border: 1px solid #999;
}

.operator{
    background-color: rgb(58, 58, 211);
    color:white;
}
</style>