<script>
	let total = 0;
	let numberInput = "0";
	let state = null;

	let operations = [
		{id:1,name:"add",symbol:"+"},
		{id:2,name:"subtract",symbol:"-"},
		{id:3,name:"multiply",symbol:"x"},
		{id:4,name:"divide",symbol:"÷"}
	];

	let numkeys = [
		{id:11,name:7},
		{id:12,name:8},
		{id:13,name:9},
		{id:14,name:4},
		{id:15,name:5},
		{id:16,name:6},
		{id:17,name:1},
		{id:18,name:2},
		{id:19,name:3},
		{id:20,name:0},
		{id:21,name:"."},
		{id:22,name:"C"},
	];
	//Operators
	function resolveState(){
		switch(state){
			case "add":
				total += parseFloat(numberInput);
				numberInput = "0";
				break;
			case "subtract":
				total -= parseFloat(numberInput);
				numberInput = "0";
				break;
			case "multiply":
				total *= parseFloat(numberInput);
				numberInput = "0";
				break;
			case "divide":
				total /= parseFloat(numberInput);
				numberInput = "0";
				break;
			default:
				total = parseFloat(numberInput);
				numberInput = "0";
				break;
		}
	}
	//Set Operators
	function setOperation(operation){
		resolveState();
		state = operation;
	}
	//Set Value
	function setValue(value){
		if(numberInput.toString() == "0" || state == "equal"){
			numberInput = "";
		}
		if(state == "equal"){
			state = null;
		} 
		if(value == "C"){
			total = 0;
			state = null;
			numberInput = "0";
			return;
		}
		numberInput += value;
	}
	//Calculate
	function equal(){
		resolveState();
		numberInput = total;
		state = "equal";
	}

</script>

<div id="calculator">
	<input type="text" value={numberInput}/>
	<div class="buttons">
		<div class="operations">
			{#each operations as operation (operation.id)}
				<button on:click={() => setOperation(`${operation.name}`)}>{operation.symbol}</button>
			{/each}
		</div>
		<div class="numbers">
			{#each numkeys as numkey (numkey.id)}
			<button on:click={() => setValue(`${numkey.name}`)}>{numkey.name}</button>
			{/each}
		</div>
		<div class="equals">
			<button on:click={equal}>=</button>
		</div>
	</div>
</div>

<style>
	#calculator {
		border:2px solid black;
		width: 600px;
		height:600px;
		margin: auto;
		padding: 20px;
	}
	input[type=text]{
		font-size: 20px;
		width: 93%;
		padding: 40px 20px;
		outline: none;
		text-align: right;		
	}
	.operations button {
		width: 130px;
		height: 80px;
		margin: 10px;
	}
	button{
		border: 1px solid lig;
	}
	.numbers{
		max-width: 500px;
	}
	.numbers button{
		width: 130px;
		height: 80px;
		margin: 10px;
	}
	.equals button{
		position: absolute;
		top: 25.5%;
		left: 58.3%;
		width: 130px;
		height: 375px;
	}
</style>

