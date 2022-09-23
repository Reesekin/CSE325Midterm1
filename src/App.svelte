
<script lang="ts">
	export let name: string;

	import Katex from 'svelte-katex'

	//MOD calculation
	let modeq = "MOD = \\frac{Frequency}{Prescalar} * time -1"

	let f = 0;
	let frequency = 0;
	let fUnit = "Hz";
	let prescalar = 1;
	let time = 0;
	let t = 0;
	let tUnit = "ms";
	let ans = 0;

	function calcMod(){
		console.log(fUnit);
		switch (fUnit){
			case "GHz":
				frequency = f * 10**9;
				break;
			case "MHz":
				frequency = f * 10**6;
				break;
			case "kHz":
				frequency = f * 10**3;
				break;
			case "Hz":
				frequency = f;
				break;
		}
		switch (tUnit){
			case "s":
				time = t;
				break;
			case "ms":
				time = t / 1000;
				break;
			case "us":
				time = t / 1000000;
				break;
			case "ns":
				time = t / 1000000000;
				break;
		}
		let mod = (frequency/prescalar)*time-1;
		modeq = `MOD = \\frac{${frequency}Hz}{${prescalar}} * ${time}s -1 = {\\color{Red} ${parseFloat(mod.toFixed(2))}}`
		ans = mod;
		return mod;
	}
	function reset(){
		modeq = "MOD = \\frac{Frequency}{Prescalar} * time -1"
		frequency = 0;
		prescalar = 0;
		time = 0;
		ans = 0;
	}
</script>

<main>
	<h1>CSE 325: Midterm 1</h1>
	<h4>Written by: Tommy Thai</h4>
	<h2> MOD calculator: </h2>
	<!-- Mod calulcator -->
	<Katex displayMode>{modeq}</Katex>
	<div id="in">
		<!-- Update MOD on input change-->
		<label for="freq">Frequency: </label>
		<input type="number" id="freq" min="0" bind:value={f} on:input={() => calcMod()} placeholder="Frequency" />
		<select bind:value={fUnit} on:change={() => calcMod()}>
			<option value="GHz">GHz</option>
			<option value="MHz">MHz</option>
			<option value="kHz">kHz</option>
			<option value="Hz">Hz</option>
		</select>
		<label for="prescalar">Prescalar: </label>
		<input type="number" id="ps" min="1" bind:value={prescalar} on:input={() => calcMod()} placeholder="Prescalar" />
		<label for="time">Time: </label>
		<input type="number" min="0" bind:value={t} on:input={() => calcMod()} placeholder="Time" />
		<select bind:value={tUnit} on:change={e => calcMod()}>
			<option value="s">s</option>
			<option value="ms">ms</option>
			<option value="us">us</option>
			<option value="ns">ns</option>
			<option value="ps">ps</option>
		</select>
	</div>
	<!-- Reset -->
	<button on:click={() => reset()}>Reset</button>
	<!------------------->
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
	#in {
		display: flex;
		flex-direction: row;
		justify-content: center;
		vertical-align: middle;
		border:#ff3e00;
		border-width: 1px;
	}
	#in input {
		width: 100px;
	}
	div#in, label {
		margin: 5px;
	}

</style>