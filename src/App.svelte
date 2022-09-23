
<script lang="ts">
	import Katex from 'svelte-katex';
	export let name: string;
	import Mod from "./Mod.svelte";
	import Pwm from "./Pwm.svelte";
</script>

<main>
	<h1>CSE 325: Midterm 1</h1>
	<h4>Written by: {name}</h4>
	<!-- Mod calulcator -->
		<Mod/>
		<Pwm/>
	<!------------------->
	<!-- Resources -->
	<div class="section">
		<h2>Resources: </h2>
		<div class="content">
			<a href="../ref.pdf" type="application/pdf" target="_blank">Reference Manual</a><br>
			<a href="../schematic.pdf" type="application/pdf" target="_blank">Schematic</a>
		</div>
	</div>
	<!-- Module 1 -->
	<div class="section">
		<h2>Timers: </h2>
		<div class="content1">
			<div class="katex">
				<Katex displayMode> Period = \frac{'1'}{'{Frequency}'}</Katex>
				<Katex displayMode> Period = T_{'{on}'} + T_{'{off}'} </Katex>
				<Katex displayMode> Duty Cycle = {'T_{{on}}'}/{'T_{{on}} + T_{{off}}'}*100 </Katex>
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
</style>