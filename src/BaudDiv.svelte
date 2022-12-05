
<script lang="ts">
	import Katex from 'svelte-katex';
  let baudDivEq = "Baud_{Div} = \\frac{F_{UARTSRC}}{16*BaudRate}";
  let sc = 0; //UARTSRC
  let scf = sc;
  let scUnit = "MHz";
  let bps = 0; //BaudRate
  let bpsf = bps;
  let bpUnit = "seconds";

  function calcDiv(){

    switch(scUnit){
      case "GHz":
        scf = sc * 10**9;
        break;
      case "MHz":
        scf = sc * 10**6;
        break;
      case "kHz":
        scf = sc * 10**3;
        break;
      case "Hz":
        scf = sc;
        break;
    }
    switch(bpUnit){
      case "seconds":
        bpsf = bps;
        break;
      case "milliseconds":
        bpsf = bps * 10**-3;
        break;
      case "microseconds":
        bpsf = bps * 10**-6;
        break;
      case "nanoseconds":
        bpsf = bps * 10**-9;
        break;
    }
    let bd = (scf)/(16*bpsf);
    baudDivEq = `Baud_{Div} = \\frac{${scf}Hz}{16*${bpsf}bps} = {\\color{Red} ${Math.floor(parseFloat(bd.toFixed(4)))}}`;
  }

</script>

<main>
	<h2> Baud<sub>div</sub> calculator: </h2>
  <div class="katex">
		<Katex displayMode>{baudDivEq}</Katex>
	</div>
	<!-- Baud Div calulcator -->
	<div id="in">
		<!-- Update MOD on input change-->
		<div class="option">
      <div class="option">
        <label for="freq">F<sub>UARTSRC</sub>: </label>
        <input type="number" id="freq" min="0" bind:value={sc} on:input={() => calcDiv()} placeholder="" />
        <select bind:value={scUnit} on:change={() => calcDiv()}>
          <option value="GHz">GHz</option>
          <option value="MHz">MHz</option>
          <option value="kHz">kHz</option>
          <option value="Hz">Hz</option>
        </select>

      </div>
      <div class="option">
        <label for="freq">bps: </label>
        <input type="number" id="freq" min="0" bind:value={bps} on:input={() => calcDiv()} placeholder="bps" />
        <select bind:value={bpUnit} on:change={() => calcDiv()}>
          <option value="seconds">seconds</option>
          <option value="milliseconds">milliseconds</option>
          <option value="microseconds">microseconds</option>
          <option value="nanoseconds">nanoseconds</option>
        </select>
      </div>
	  <div>
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