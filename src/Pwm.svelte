
<script lang="ts">
	import Katex from 'svelte-katex';

	//MOD calculation
	let pwmeq = "F_{pwm} = \\frac{F_{tpm}/{PS}}{MOD+1}";
	let f = 0;
	let tpmfrequency = 0;
	let ftpmUnit = "MHz";
	let prescalar = 1;
	let mod = 0;
	let ans = 0;

	function calcMod(){
		console.log(ftpmUnit);
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
		let pwm = (tpmfrequency/prescalar)/(mod+1);
        pwmeq = `F_{pwm} = \\frac{${tpmfrequency}Hz/${prescalar}}{${mod}+1} = {\\color{Red} ${parseFloat(pwm.toFixed(4))}Hz}`;
		ans = pwm;
		return pwm;
	}
	function reset(){
		pwmeq = "F_{pwm} = \\frac{F_{tpm}/{PS}}{MOD+1}";
		tpmfrequency = 0;
		prescalar = 1;
		mod = 0;
		ans = 0;
	}
</script>

<main>
	<h2> F<sub>pwm</sub> calculator: </h2>
	<!-- Mod calulcator -->
	<div class="katex">
		<Katex displayMode>{pwmeq}</Katex>
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

        <div class="option">
            <label for="MOD">MOD: </label>
            <input type="number" min="0" bind:value={mod} on:input={() => calcMod()} placeholder="MOD" />
        </div>
	</div>
	<!-- Reset -->
	<button on:click={() => reset()}>Reset</button>
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