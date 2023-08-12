<template>
    <div>
        <div class="container">
            <div class="calculator">
                <form>
                    <div class="display">
                        <input type="text" name="diaplay" v-model="display">
                    </div>
                    <div>
                        <input type="button" value="AC" @click="allClear" class="clear">
                        <input type="button" value="DE" @click="remove()" class="operator">
                        <input type="button" value="." @click="addtoDisplay('.')" class="operator">
                        <input type="button" value="/" @click="addtoDisplay('/')" class="operator">
                    </div>
                    <div>
                        <input type="button" value="7" @click="addtoDisplay(7)">
                        <input type="button" value="8" @click="addtoDisplay(8)">
                        <input type="button" value="9" @click="addtoDisplay(9)">
                        <input type="button" value="*" @click="addtoDisplay('*')" class="operator">
                    </div>
                    <div>
                        <input type="button" value="4" @click="addtoDisplay(4)">
                        <input type="button" value="5" @click="addtoDisplay(5)">
                        <input type="button" value="6" @click="addtoDisplay(6)">
                        <input type="button" value="-" @click="addtoDisplay('-')" class="operator">
                    </div>
                    <div>
                        <input type="button" value="1" @click="addtoDisplay(1)">
                        <input type="button" value="2" @click="addtoDisplay(2)">
                        <input type="button" value="3" @click="addtoDisplay(3)">
                        <input type="button" value="+" @click="addtoDisplay('+')" class="operator">
                    </div>
                    <div>
                        <input type="button" value="00" @click="addtoDisplay('00')">
                        <input type="button" value="0" @click="addtoDisplay(0)">
                        <input type="button" value="=" class="equal" @click="calculate()">
                    </div>
                </form>
            </div>

        </div>
    </div>
</template>

<script>
import * as math from 'mathjs'; 

export default {
    name: 'Cal-App',
    data() {
        return {
            display: 'Calculator',
            isNotclicked: true
        }
    },
    methods: {
        addtoDisplay(value) {
            if(this.isNotclicked){
                this.display = ''
                this.isNotclicked = false
            }
            this.display += value
            console.log('value',value)
        },
        allClear() {
            this.display = ''
        },
        calculate() {
            try {
                // this.display = eval(this.display)
                this.display = math.evaluate(this.display).toString();
            }
            catch {
                this.display = 'Error'
            }
        },
        remove() {
            this.display=this.display.toString().slice(0, -1)
        }
    }
}
</script>

<style>
.container {
    background: rgb(252, 255, 252);
    display: flex;
    align-items: center;
    justify-content: center;
}
.calculator {
    background: #3a4452;
    padding: 20px;
    border-radius: 10px;
}
.calculator form input {
    border: 0;
    outline: 0;
    width: 60px;
    height: 60px;
    border-radius: 10px;
    box-shadow: -8px -8px 15px rgba(255, 255, 255, 0.1), 5px 5px 15px rgba(0, 0, 0, 0.2);
    background: transparent;
    font-size: 25px;
    color: white;
    margin: 10px;
    transition: background-color 0.3s ease, color 0.3s ease; 
}
.calculator form input:active {
    background-color: rgba(255, 255, 255, 0.1); /* Change the background color when button is clicked */
  }
form .display {
    display: flex;
    justify-content: flex-end;
    margin: 20px 0;
}
form .display input {
    text-align: right;
    flex: 1;
    font-size: 45px;
    box-shadow: none;
}
form input.equal {
    width: 145px;
}
form input.operator {
    color: #33ffd8;
}
form input.clear {
    color: rgb(125, 237, 13);
}
form input.equal {
    color: rgb(125, 237, 13);
}
</style>