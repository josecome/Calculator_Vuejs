<template>
    <div>
        <table>
            <tr>
                <td colspan="3">
                    <Label
                        :text="nmbr" 
                    />                 
                </td>
                <td>
                    <Button
                        @btn-click="clean_screen()"
                        :text="'C'"
                        :color="'#FF0000'"
                        :class_name="'btn'"
                    />
                </td>
            </tr>
            <tr v-for="btns_rows in buttons_in_array">
                <td v-for="btns in btns_rows">
                    <Button
                        @btn-click="addNmber(btns)"
                        :text="btns"
                        :color="'rgba(51, 51, 51, 0.05)'"
                        :class_name="'btn2'"
                    />
                </td>
            </tr>
        </table>        
    </div>
</template>
  
<script>
import Label from './Label.vue'
import Button from './Button.vue'
export default {
    name: 'Calculator',
    props: {
        
    },
    components: {
        Label,
        Button
    },
    data(){
        return{
            prevnmbr: 0,
            nmbr: 0,
            lastop: "NA",
            buttons_in_array: [[7, 8, 9, "/"], [4, 5, 6, "x"],[1, 2, 3, "-"], [0, ".", "=", "+"]]
        }
    },
    methods: {
        addNmber(v){
           var targetedVal = v;  
           if("=" === targetedVal){
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
            }
            this.prevnmbr = 0;
            return;
           } 
           if (!["=", "/", "+", "-", "x"].includes(targetedVal)){ 
            this.nmbr = Number("" + this.nmbr + targetedVal);
           } else {
            this.prevnmbr = this.nmbr; 
            this.nmbr = 0;
            this.lastop = targetedVal;
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

.oper{
    background-color: #A9A9A9;
}
.oper2{
    background-color: #0000FF;
    color: white;
}
</style>