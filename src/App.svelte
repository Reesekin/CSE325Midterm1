
<script lang="ts">
	import Katex from 'svelte-katex';
	export let name: string;
	import Mod from "./Mod.svelte";
	import Pwm from "./Pwm.svelte";
	import PS from "./PS.svelte";
</script>

<main>
	<h1>CSE 325: Midterm 1</h1>
	<h4>Written by: {name}</h4>
	<!-- Calulcators -->
		<Mod/>
		<Pwm/>
		<PS/>
	<!------------------->
	<!-- Resources -->
	<div class="section">
		<h2>Resources: </h2>
		<div class="content column">
			<a href="../ref.pdf" type="application/pdf" target="_blank">Reference Manual</a>
			<a href="../schematic.pdf" type="application/pdf" target="_blank">Schematic</a>
			<a href="https://www.calculator.net/ohms-law-calculator.html" target="_blank">Ohm's Law Calculator</a>
		</div>
		<h2>Important Pages:</h2>
		<h3 class="content">Resource Manual:</h3>
		<div class="content1">	
			<p>Hookup ALT# to PIN (Useful for finding mux value PORT->PCR[bit]): <a href="../ref.pdf#page=172" type="application/pdf" target="_blank">pg.172</a></p>
			<p>System Clock Gating Control Register 4: <a href="../ref.pdf#page=214" type="application/pdf" target="_blank">pg.214</a></p>
			<p>System Clock Gating Control Register 5: <a href="../ref.pdf#page=216" type="application/pdf" target="_blank">pg.216</a></p>
			<p>System Clock Gating Control Register 6: <a href="../ref.pdf#page=218" type="application/pdf" target="_blank">pg.218</a></p>
			<p>System Clock Gating Control Register 7: <a href="../ref.pdf#page=220" type="application/pdf" target="_blank">pg.220</a></p>
			<p>TPM0_C2SC: <a href="../ref.pdf#page=569" type="application/pdf" target="_blank">pg.569</a></p>
		</div>
	</div>
	<!-- Module 1 -->
	<div class="section">
		<h2>Timers: </h2>
		<div class="content1">
			<div class="katex">
				<Katex displayMode> Period = \frac{'1'}{'{Frequency}'}</Katex>
				<Katex displayMode> Period = T_{'{on}'} + T_{'{off}'} </Katex>
				<Katex displayMode> Duty Cycle = {'(T_{{on}}'}/{'T_{{on}} + T_{{off}})'}*100 </Katex>
			</div>
			<p class="bold"> Prescale Factor Selection (pg. 567 ref)</p>
			<ul>
				<li>000 -> divide by 1</li>
				<li>001 -> divide by 2</li>
				<li>010 -> divide by 4</li>
				<li>011 -> divide by 8</li>
				<li>100 -> divide by 16</li>
				<li>101 -> divide by 32</li>
				<li>110 -> divide by 64</li>
				<li>111 -> divide by 128</li>
			</ul>
		<h2>Digital Pins: </h2>
		<ul>
			<li>SIM->SCGC5 – Port Clock Gating</li>
			<li>PORTA->PCR[n] - Port Control Register</li>
			<li>GPIOA->PDDR – Data Direction Register</li>
			<ul>
				<li>0 – Input</li>
				<li>1 – Output</li>
			</ul>
			<li>GPIOA->PDOR – Output Register</li>
			<li>GPIOA->PSOR – Set Output Register</li>
			<li>GPIOA->PTOR - Toggle Output Register</li>
			<li>GPIOA->PDIR - Data Input Register</li>
		</ul>
	</div>
</main>

<style>
	.katex{
		width:fit-content;
		margin: 0 auto;
		background-color: rgb(255, 157, 0);
		box-shadow: 0 2px 5px 0 rgba(0, 0, 0, 0.5);
		border: #313131 solid 1px;
		padding: 0 40px 0 40px;
		border-radius: 10px;
	}
	main {
		margin: 0 auto;
		text-align: center;
		position: absolute;
		top: 0;
		left: 0;
		background-color: rgb(237, 237, 237);
		height: fit-content;
		width: 100%;
	}
	.section {
		text-align: left;
	}
	.content {
		margin-left: 20px;
	}
	.bold {
		font-weight: bold;
	}
	.content1 {
		margin-left: 40px;
	}
	a {
		color: #ff3e00;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}
	.column {
		display: flex;
		flex-direction: column;
	}
</style>