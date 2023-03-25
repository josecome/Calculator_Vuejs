<template>
    <div>
        <table>
            <tr>
                <td colspan="5">
                    <div id="lbl">
                        <label>{{ nmbr }}</label>
                    </div>                    
                </td>
                <td>
                    <button class="btn_clean" @click="clean_screen()">C</button>
                </td>
            </tr>
            <tr v-for="btns_rows in buttons_in_array">
                <td v-for="btns in btns_rows">
                    <button @click="addNmber($event)">{{ btns }}</button>
                </td>
            </tr>
        </table>        
    </div>
</template>
  
<script>
export default {
    name: 'Calculator',
    props: {
        
    },
    components: {
        
    },
    data(){
        return{
            prevnmbr: 0,
            nmbr: 0,
            lastop: "NA",
            buttons_in_array: [[7, 8, 9, "/", "sin", "pi"], [4, 5, 6, "x", "cos", "e"],[1, 2, 3, "-", "log", "exp"], [0, ".", "=", "+", "ln", "x!"]],
            sin_cos_tan_notable_values: [[30, 0.5, 0.866, 0.5773], [45, 0.707, 0.707, 1], [60, 0.866, 0.5, 1.732]]
        }
    },
    methods: {
        addNmber(v){
           var targetedVal = v.target.textContent; 
           if("=" === targetedVal){
            if(this.lastop === "NA"){
                return;
            } else {
                if(this.lastop === "-"){
                   this.nmbr = Number(this.prevnmbr) - Number(this.nmbr);
                } else if(this.lastop === "+"){
                    this.nmbr = this.prevnmbr + this.nmbr;
                } else if(this.lastop === "/"){
                    this.nmbr = this.prevnmbr / this.nmbr;
                } else if(this.lastop === "x"){
                    this.nmbr = this.prevnmbr * this.nmbr;
                } else if(this.lastop === "exp"){
                    this.nmbr = this.ExponetialOfNumber(this.prevnmbr, this.nmbr);
                } else if(this.lastop === "sin"){
                    this.nmbr = this.calculateSinCosTan('sin', this.prevnmbr);
                }  else if(this.lastop === "cos"){
                    this.nmbr = this.calculateSinCosTan('cos', this.prevnmbr);
                }  else if(this.lastop === "tan"){
                    this.nmbr = this.calculateSinCosTan('tan', this.prevnmbr);
                } 
            }
                this.prevnmbr = 0;
                return;
            } 
            if("x!" === targetedVal){
                console.log("Value: " + this.nmbr)
                this.nmbr = this.calc_factorial(this.nmbr);
                console.log("Value2: " + this.nmbr)
                return;
            } else if(targetedVal === "pi") {
                    this.nmbr = 3.141592653589793238;             
            } else if(targetedVal === "e") {
                    this.nmbr = 2.7182818;             
            } else if (!["=", "/", "+", "-", "x", "exp", "sin", "cos", "tan"].includes(targetedVal)){ 
                this.nmbr = Number("" + this.nmbr + targetedVal);
           } else {
                if(targetedVal === "pi" || targetedVal === "e") {
                    return;
                }
                this.prevnmbr = this.nmbr; 
                this.nmbr = 0;
                this.lastop = targetedVal;
           }
        },
        clean_screen(){
            this.prevnmbr = 0;
            this.nmbr = 0;
            this.lastop = "NA";
        },
        factorial(y){var f = 1; for(var i = y; i >= 1; i--){f = f * i;/* console.log(i); */} return f},
        calc_factorial(n) {
            return n > 1 ? this.factorial(n) : n;
        },
        ExponetialOfNumber(v1, v2){
           var v_result = 1; 
           for(var i = 0; i < Number(v2); i++){
               v_result = v_result * v1; 
           }
           return v_result;
        },
        calculateSinCosTan(oper, value) {
            if (value > 90) {
                value = value % 90; 
            }
            if(![30, 45, 60].includes(value)){
                alert("Choose number that is 30 or 45 or 60 or multiple that when devide 90 the result match one of the value given");
                return value;
            }
            var _30 = this.sin_cos_tan_notable_values[0];
            var _45 = this.sin_cos_tan_notable_values[1];
            var _60 = this.sin_cos_tan_notable_values[2];

            if(value === 30) {
                if(oper === "sin") { return _30[1]} 
                else if(oper === "cos") {return _45[2]} 
                else if(oper === "tan") {return _60[3]}
            } else if(value === 45) {
                if(oper === "sin") { return _30[1]} 
                else if(oper === "cos") {return _45[2]} 
                else if(oper === "tan") {return _60[3]}
            } else if(value === 60) {
                if(oper === "sin") { return _30[1]} 
                else if(oper === "cos") {return _45[2]} 
                else if(oper === "tan") {return _60[3]}
            }   
            return value;
        }
    },
    computed: {

    },
    emits: [],
}
</script>

<style scoped>
button {
  background-color: rgba(51, 51, 51, 0.05);
  border-radius: 8px;
  border-width: 0;
  color: #333333;
  cursor: pointer;
  display: inline-block;
  font-family: "Haas Grot Text R Web", "Helvetica Neue", Helvetica, Arial, sans-serif;
  font-size: 14px;
  font-weight: 500;
  line-height: 20px;
  list-style: none;
  margin: 0;
  padding: 10px 12px;
  text-align: center;
  transition: all 200ms;
  vertical-align: baseline;
  white-space: nowrap;
  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
  width: 60px;
}
#lbl {
  width: 100%;  
  border: 1px solid gray; 
  border-radius: 6px;
  text-align: right;  
}
.oper{
    background-color: #A9A9A9;
}
.oper2{
    background-color: #0000FF;
    color: white;
}
.btn_clean{
    background-color: #FF0000;
    color: white;
}
</style>