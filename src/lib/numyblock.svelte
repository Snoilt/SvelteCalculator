<script lang="ts">

let inputValueString: string = ""
let equationArray: string[] = []
let equationHistory = []
let x: number = 0
let y: number = 0
let lastFormula
let openForDelete: boolean = false
let testOperator: string

function calculate(operator: string){
        
    let result: number

    if (equationHistory.length != 0) {
        x = lastFormula.result
    } 

    console.log("Factor 1: " + x)
    console.log("Factor 2: " + y)
    
    switch (operator){
        case "+": result = x + y
        break
        case "-": result = x - y
        break
        case "/": result = x / y
        break
        case "*": result = x * y
        break
        default:
        break
    }

    inputValueString = `${result}`

    let obj = {
        x: x,
        y: y,
        operator: operator,
        result: result
    }

    lastFormula = obj
    equationHistory.push(obj)
    console.log(equationHistory)
    equationArray = []
    openForDelete = true
    return result
}

function getXAndY(operator: string) { 
    
    if (x == 0) {
        x = parseFloat(equationArray.join(""))
        inputValueString = ""
        equationArray = []
        testOperator = operator
        return 
    } else {
        y = parseFloat(equationArray.join(""))
        inputValueString = ""
        equationArray = []
        calculate(testOperator)
        return
    }
    
}

const equationCapture = (operandOrNumber: string) => {
    const clickedOperand: boolean = RegExp('[\+\-\/\*\=]').test(operandOrNumber)
    const fieldClicked: boolean = RegExp('[0-9\+\-\/\*]').test(operandOrNumber)
    const acClicked: boolean = operandOrNumber == "AC"
    const delClicked: boolean = operandOrNumber == "DEL"

    function pushToInput(){
        equationArray.push(operandOrNumber)
        inputValueString += operandOrNumber
    }

    if (clickedOperand && inputValueString != "" && operandOrNumber != "=") {
        inputValueString = ""
        getXAndY(operandOrNumber)
        return
    }

    if (operandOrNumber == "=" && x != 0) {
        inputValueString = ""
        getXAndY(testOperator)
        return
    }

    if (fieldClicked && inputValueString != "" && openForDelete ){
        openForDelete = false
        inputValueString = ""
    }

    if (fieldClicked && !clickedOperand) {
        pushToInput()
        return
    }

    if (acClicked) {
        inputValueString = ""
        equationArray = []
        equationHistory = []
    }1

}
  
</script>

<div class="container">

  <input disabled id="input" class="center" type="form" bind:value={inputValueString} />
    <div id="operators" class = "grids">
        <button class="controlElement"  on:click = {() => equationCapture("+")}>+</button>
        <button class="controlElement"  on:click = {() => equationCapture("-")}>-</button>
        <button class="controlElement"  on:click = {() => equationCapture("*")}>x</button>
        <button class="controlElement"  on:click = {() => equationCapture("/")}>/</button>
        <button class="controlElement"  on:click = {() => equationCapture("=")}>=</button>
    </div>
  <div id="numberblock" class="grids">
    <button class="controlElement" on:click = {() => equationCapture("7")}>7</button>
    <button class="controlElement" on:click = {() => equationCapture("8")}>8</button>
    <button class="controlElement" on:click = {() => equationCapture("9")}>9</button>
    <button class="controlElement" on:click = {() => equationCapture("4")}>4</button>
    <button class="controlElement" on:click = {() => equationCapture("5")}>5</button>
    <button class="controlElement" on:click = {() => equationCapture("6")}>6</button>
    <button class="controlElement" on:click = {() => equationCapture("1")}>1</button>
    <button class="controlElement" on:click = {() => equationCapture("2")}>2</button>
    <button class="controlElement" on:click = {() => equationCapture("3")}>3</button>
    <button class="controlElement" on:click = {() => equationCapture("AC")}>AC</button>
    <button class="controlElement" on:click = {() => equationCapture("0")}>0</button>
    <button class="controlElement" on:click = {() => equationCapture("DEL")}>DEL</button>
</div>
</div>


<style>
  #numberblock {
    width: 150px;
    grid-template-columns: 45px 45px 45px;

  }

  #operators {
    grid-template-columns: 45px 45px 45px 45px 45px;
  }
  

  .grids {
    margin: auto;
    text-align: center;
    display: grid;
    justify-content: center;
    grid-auto-rows: 30px;
    gap: 10px;
    margin-top: 15px;
  }

  .controlElement {
    background-color: #474E68;
    border-radius: 5px;
    border: none;
    color: rgb(172, 172, 172);
  }

  .controlElement:hover {
    background-color: #50577A;
  }

  .controlElement:active {
    background-color: #6B728E;
  }

  .center {
    display: block;
    margin-left: auto;
    margin-right: auto;
  }

  #input {
    width: 270px;
    height: 30px;
    border-radius: 2px;
    border-top-style: hidden;
    border-right-style: hidden;
    border-left-style: hidden;
    background-color: #404258 ;
    border-color: #6B728E;
    color: rgb(172, 172, 172);
    text-align: center;
  }

  @media (prefers-color-scheme: light) {


    .controlElement {
        background-color: #D6E4E5;
        color: #497174;
    }
    .controlElement:hover {
        background-color: #EDEDED;
    }

    .controlElement:active {
        background-color: #EB6440;
    }
    #input {
        background-color: #e5eef0;
        color: #497174;
        border:none;
    }
    }

</style>
