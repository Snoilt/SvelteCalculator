<script lang="ts">
  let inputValue: string = ""
  const typeThis = (dickNum) => {
    inputValue += `${dickNum}`;
};
 
  
</script>

<div class="container">

  <input id="input" class="center" type="form" bind:value={inputValue} />

    <div id="operators" class = "grids">
        <input type="button" class="controlElement" value="+" />
        <input type="button" class="controlElement" value="-" />
        <input type="button" class="controlElement" value="x" />
        <input type="button" class="controlElement" value="/" />
        <input type="button" class="controlElement" value="=" />
    </div>
  <div id="numberblock" class="grids">
    <input type="button" class="controlElement" value="7" on:click = {() => typeThis(7)}/>
    <input type="button" class="controlElement" value="8" on:click = {() => typeThis(8)}/>
    <input type="button" class="controlElement" value="9" on:click = {() => typeThis(9)}/>
    <input type="button" class="controlElement" value="4" on:click = {() => typeThis(4)}/>
    <input type="button" class="controlElement" value="5" on:click = {() => typeThis(5)}/>
    <input type="button" class="controlElement" value="6" on:click = {() => typeThis(6)}/>
    <input type="button" class="controlElement" value="1" on:click = {() => typeThis(1)}/>
    <input type="button" class="controlElement" value="3" on:click = {() => typeThis(3)}/>
    <input type="button" class="controlElement" value="2" on:click = {() => typeThis(2)}/>
  </div>
</div>

<style>
  #numberblock {
    width: 150px;
    grid-template-columns: 30px 30px 30px;

  }

  #operators {
    grid-template-columns: 30px 30px 30px 30px 30px;
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
    width: 180px;
    height: 30px;
    border-radius: 2px;
    border-top-style: hidden;
    border-right-style: hidden;
    border-left-style: hidden;
    background-color: #404258 ;
    border-color: #6B728E;
    color: rgb(172, 172, 172);
  }

  @media (prefers-color-scheme: light) {
    
    .controlElement {
        background-color: rgb(226, 226, 226);
    }
    .controlElement:hover {
    background-color: #a9a9a9;
  }

  .controlElement:active {
    background-color: #bfbfbf;
  }
  #input {
    background-color: aliceblue;
  }
  }

</style>
