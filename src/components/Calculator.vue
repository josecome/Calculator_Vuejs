<template>
    <div>
        <table>
            <tr>
                <td colspan="3">
                    <div id="lbl">
                        <label>{{ nmbr }}</label>
                    </div>                    
                </td>
                <td>
                    <button class="btn_clean" @click="clean_screen()">C</button>
                </td>
            </tr>
            <tr>
                <td>
                    <button @click="addNmber($event)">7</button>
                </td>
                <td>
                    <button @click="addNmber($event)">8</button>
                </td>
                <td>
                    <button @click="addNmber($event)">9</button>
                </td>
                <td>
                    <button class="oper" @click="addNmber($event)">/</button>
                </td>
            </tr>
            <tr>
                <td>
                    <button @click="addNmber($event)">4</button>
                </td>
                <td>
                    <button @click="addNmber($event)">5</button>
                </td>
                <td>
                    <button @click="addNmber($event)">6</button>
                </td>
                <td>
                    <button class="oper" @click="addNmber($event)">x</button>
                </td>
            </tr>
            <tr>
                <td>
                    <button @click="addNmber($event)">1</button>
                </td>
                <td>
                    <button @click="addNmber($event)">2</button>
                </td>
                <td>
                    <button @click="addNmber($event)">3</button>
                </td>
                <td>
                    <button class="oper" @click="addNmber($event)">-</button>
                </td>
            </tr>
            <tr>
                <td>
                    <button @click="addNmber($event)">0</button>
                </td>
                <td>
                    <button @click="addNmber($event)">.</button>
                </td>
                <td>
                    <button class="oper2" @click="addNmber($event)">=</button>
                </td>
                <td>
                    <button class="oper" @click="addNmber($event)">+</button>
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
            lastop: "NA"
        }
    },
    methods: {
        addNmber(v){
           if("=" === v.target.textContent){
            if(this.lastop === "NA"){
                return;
            } else{
                if(this.lastop === "-"){
                   this.nmbr = Number(this.prevnmbr) - Number(this.nmbr);
                } else if(this.lastop === "+"){
                    this.nmbr = this.prevnmbr + this.nmbr;
                } else if(this.lastop === "/"){
                    this.nmbr = this.prevnmbr / this.nmbr;
                } else if(this.lastop === "x"){
                    this.nmbr = this.prevnmbr * this.nmbr;
                }
                console.log("nmbr: " + this.nmbr);
            }
            this.prevnmbr = 0;
            return;
           } 
           if (!("=/+-x").includes(v.target.textContent)){ 
            this.nmbr = Number("" + this.nmbr + v.target.textContent);
            console.log("N: " + this.nmbr)
           } else {
            this.prevnmbr = this.nmbr; 
            this.nmbr = 0;
            this.lastop = v.target.textContent;
            console.log("O: " + this.prevnmbr + v.target.textContent)
           }
        },
        clean_screen(){
            this.prevnmbr = 0;
            this.nmbr = 0;
            this.lastop = "NA";
        }
    },
    watch: {
        nmbr(val, prevval) {
            //console.log("val: " + String(val) + "," + String(prevval))
            if((String(val) === "NaN" || String(val) === "Infinity") && String(prevval) === "0") {
               alert("Any number can't divide zero!");
            }
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