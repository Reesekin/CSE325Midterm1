
<script lang="ts">
	import Katex from 'svelte-katex';

	//MOD calculation
	let PSeq = "PS = \\frac{F_{tpm}}{(MOD+1)*F_{pwm}}";
	let f = 0;
    let p = 0;
    let ftpmfrequency = 0;
	let pwmfrequency = 0;
    let tpmUnit = "MHz";
	let pwmUnit = "MHz";
	let prescalar = 0;
	let mod = 0;
	let ans = 0;

	function calcMod(){
		switch (tpmUnit){
			case "GHz":
				ftpmfrequency = f * 10**9;
				break;
			case "MHz":
				ftpmfrequency = f * 10**6;
				break;
			case "kHz":
				ftpmfrequency = f * 10**3;
				break;
			case "Hz":
				ftpmfrequency = f;
				break;
		}
		switch (pwmUnit){
			case "GHz":
				pwmfrequency = p * 10**9;
				break;
			case "MHz":
                pwmfrequency = p * 10**6;
				break;
			case "kHz":
                pwmfrequency = p * 10**3;
				break;
			case "Hz":
                pwmfrequency = p;
				break;
		}
		let ps = (ftpmfrequency)/((mod+1)*pwmfrequency);
        PSeq = `PS = \\frac{${ftpmfrequency}Hz}{(${mod}+1)*${pwmfrequency}Hz} = {\\color{Red} ${parseFloat(ps.toFixed(4))}}`;
		ans = ps;
		return ps;
	}
	function reset(){
		PSeq = "PS = \\frac{F_{tpm}}{(MOD+1)*F_{pwm}}";
        ftpmfrequency = 0;
		pwmfrequency = 0;
		prescalar = 0;
		mod = 0;
		ans = 0;
	}
</script>

<main>
	<h2> PS calculator: </h2>
	<!-- PS calulcator -->
	<div class="katex">
		<Katex displayMode>{PSeq}</Katex>
	</div>
	
	<div id="in">
		<!-- Update MOD on input change-->
        <div class="option">
            <label for="freq">F<sub>tpm</sub>: </label>
            <input type="number" id="freq" min="0" bind:value={f} on:input={() => calcMod()} placeholder="Frequency" />
            <select bind:value={tpmUnit} on:change={() => calcMod()}>
                <option value="GHz">GHz</option>
                <option value="MHz">MHz</option>
                <option value="kHz">kHz</option>
                <option value="Hz">Hz</option>
            </select>
        </div>
        <div class="option">
            <label for="freq">F<sub>pwm</sub>: </label>
            <input type="number" id="freq" min="0" bind:value={p} on:input={() => calcMod()} placeholder="Frequency" />
            <select bind:value={pwmUnit} on:change={() => calcMod()}>
                <option value="GHz">GHz</option>
                <option value="MHz">MHz</option>
                <option value="kHz">kHz</option>
                <option value="Hz">Hz</option>
            </select>
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