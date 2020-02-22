 <template>
 
  <div class="calculator">
    <div class ="display">{{current || '0'}}</div>
    <div @click="clear" class= "btn">C</div>
    <div @click="sign" class= "btn">+/-</div>
    <div @click="percent" class= "btn">%</div>
    <div @click="divide" class= "btn operator">/</div>
    <div @click="append('7')" class= "v-btn btn">7</div>
    <div @click="append('8')" class= "v-btn btn">8</div>
    <div @click="append('9')" class= "v-btn btn">9</div>
    <div @click="times" class= "v-btn btn operator">*</div>
    <div @click="append('4')" class= "v-btn btn">4</div>
    <div @click="append('5')" class= "v-btn btn">5</div>
    <div @click="append('6')" class= "v-btn btn">6</div>
    <div @click="minus" class= "v-btn btn operator">-</div>
    <div @click="append('1')" class= "v-btn btn">1</div>
    <div @click="append('2')" class= "v-btn btn">2</div>
    <div @click="append('3')" class= "v-btn btn">3</div>
    <div @click="add" class= "v-btn btn operator">+</div>
    <div @click="append('0')" class= "v-btn btn zero">0</div>
    <div @click="dot" class= "v-btn btn">.</div>
    <div @click="equal" class= "v-btn btn operator">=</div>
    <div @click="convert" class= "v-btn btn zero">Farenheit a Celsius</div>
  </div>
  
</template>

<script>
export default {
  name: 'HelloWorld',
    data(){
        return{
            previous: null,
            current: '',
            operator: null,
            operatorClicked: false,
        }
    },
    methods: {
        clear(){
            this.current= '';
        },
        sign() {
            this.current = this.current.charAt(0) === '-' ?
               this.current.slice(1) : `-${this.current}`;
        },
        percent() {
          this.current = `${parseFloat(this.current) / 100}`   
        },
        append(number) {
            if(this.operatorClicked){
                this.current = '';
                this.operatorClicked = false;
            }
            this.current = `${this.current}${number}`;
        },
        dot(){
            if(this.current.indexOf('.') === -1){
                this.append('.');
            }
        },
        divide(){
            this.operator = (a,b)=>b/a;
            this.previous = this.current;
            this.operatorClicked = true;
        },
        times(){
            this.operator = (a,b)=>a*b;
            this.previous = this.current;
            this.operatorClicked = true;
        },
        minus(){
            this.operator = (a,b)=>b-a;
            this.previous = this.current;
            this.operatorClicked =true;
        },
        add(){
            this.operator = (a,b)=>a+b;
            this.previous = this.current;
            this.operatorClicked = true;
        },
        equal(){
            this.current = `${this.operator(parseFloat(this.current),parseFloat(this.previous))}`;
            this.previous = null;
        },
        convert(){
            this.operator = (a,b) =>((b - 32)*5)/9;
            this.previous = this.current;
            this.operatorClicked = true;
        },
    }
}
</script>


<style scoped>
.calculator {
    margin: 0 auto;
    width: 400px;
    font-size: 40px;
    display: grid;
    grid-template-columns: repeat(4,1fr);
    grid-auto-rows: minmax(50px,auto);  

}

.display {
    grid-column: 1/5;
    background-color: #333;
    color: white
}

.zero{
    grid-column: 1/3
}
.btn {
   background-color: #eee;
   border: 1px solid #333;

}

.operator {
    background-color: orange;
    color: white;

}
</style>

