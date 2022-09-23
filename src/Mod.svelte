
<script lang="ts">
	import Katex from 'svelte-katex';

	let sub : boolean = false;
	const tsub = `Substitute t for Fpwm`;
	const fsub = `Substitute Fpwm for t`;

	//MOD calculation
	const modeq1 = "MOD = \\frac{F_{tpm}}{PS} * time -1";
	const modeq2 = "MOD = \\frac{F_{tpm}/PS}{F_{pwm}} -1";
	let modeq = modeq1;
	let f = 0;
	let pwm = 0;
	let tpmfrequency = 0;
	let pwmfrequency = 0;
	let ftpmUnit = "MHz";
	let fpwmUnit = "MHz";
	let prescalar = 1;
	let time = 0;
	let t = 0;
	let tUnit = "ms";
	let ans = 0;

	function calcMod(){
		switch (ftpmUnit){
			case "GHz":
				tpmfrequency = f * 10**9;
				break;
			case "MHz":
				tpmfrequency = f * 10**6;
				break;
			case "kHz":
				tpmfrequency = f * 10**3;
				break;
			case "Hz":
				tpmfrequency = f;
				break;
		}
		switch (fpwmUnit){
			case "GHz":
				pwmfrequency = pwm * 10**9;
				break;
			case "MHz":
				pwmfrequency = pwm * 10**6;
				break;
			case "kHz":
				pwmfrequency = pwm * 10**3;
				break;
			case "Hz":
				pwmfrequency = pwm;
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
		let mod = sub? ((tpmfrequency/prescalar)/pwmfrequency)-1:(tpmfrequency/prescalar)*time-1;
		modeq = sub? `MOD = \\frac{${tpmfrequency}Hz/${prescalar}}{${pwmfrequency}Hz} - 1 = {\\color{Red} ${parseFloat(mod.toFixed(4))}}`
		:`MOD = \\frac{${tpmfrequency}Hz}{${prescalar}} * ${time}s - 1 = {\\color{Red} ${parseFloat(mod.toFixed(4))}}`
		ans = mod;
		return mod;
	}
	function reset(){
		modeq = sub? modeq = modeq2:modeq = modeq1;
		tpmfrequency = 0;
		pwmfrequency = 0;
		prescalar = 1;
		time = 0;
		ans = 0;
	}
	function toggle(){
		sub? modeq = modeq1:modeq = modeq2;
		sub = !sub;
	}
</script>

<main>
	<h2> MOD calculator: </h2>
	<!-- Mod calulcator -->
	<div class="katex">
		<Katex displayMode>{modeq}</Katex>
	</div>
	
	<div id="in">
		<!-- Update MOD on input change-->
		<div class="option">
			<label for="freq">F<sub>tpm</sub>: </label>
			<input type="number" id="freq" min="0" bind:value={f} on:input={() => calcMod()} placeholder="Frequency" />
			<select bind:value={ftpmUnit} on:change={() => calcMod()}>
				<option value="GHz">GHz</option>
				<option value="MHz">MHz</option>
				<option value="kHz">kHz</option>
				<option value="Hz">Hz</option>
			</select>
		</div>
		<div class="option">
			<label for="prescalar">Prescalar: </label>
			<input type="number" id="ps" min="1" bind:value={prescalar} on:input={() => calcMod()} placeholder="Prescalar" />
		</div>
		{#if !sub}
			<div class="option">
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
		{:else}
			<div class="option">
				<label for="pwm">F<sub>pwm</sub>: </label>
				<input type="number" min="0" bind:value={pwm} on:input={() => calcMod()} placeholder="Fpwm" />
				<select bind:value={fpwmUnit} on:change={() => calcMod()}>
					<option value="GHz">GHz</option>
					<option value="MHz">MHz</option>
					<option value="kHz">kHz</option>
					<option value="Hz">Hz</option>
				</select>
			</div>
		{/if} 
	</div>
	<div>
		<!-- Reset -->
		<button on:click={() => reset()}>Reset</button>
		<!-- Substitute t for Fpwm -->
		<button on:click={() => toggle()}>{sub? tsub : fsub}</button>
	</div>
</main>

<style>
	.katex{
		background-color: rgb(255, 157, 0);
		box-shadow: 0 2px 5px 0 rgba(0, 0, 0, 0.5);
		border: #313131 solid 1px;
		padding: 0 40px 0 40px;
		border-radius: 10px;
	}
	main {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
	}
    .option{
        display: flex;
        flex-direction: row;
        justify-content: center;
        align-items: center;
		vertical-align: middle;
    }
	#in {
		display: flex;
		flex-direction: row;
        border-radius: 5px;
        flex-wrap: wrap;
		width:fit-content;
		height: fit-content;
		background-color: rgb(255, 157, 0);
		box-shadow: 0 2px 5px 0 rgba(0, 0, 0, 0.5);
		border: #313131 solid 1px;
		padding: 20px 40px 0 40px;
		border-radius: 10px;
		justify-content: center;
	}
	button {
		color: #ff3e00;
		border-radius: 5px;
	}
	#in input {
		width: 100px;
        border-radius: 5px;
	}
    select {
        border-radius: 5px;
    }
	div#in, label {
		margin: 10px;
		padding-bottom: 10px;
	}
</style>