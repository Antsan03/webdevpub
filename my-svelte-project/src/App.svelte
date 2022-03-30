<script>
	import {Clock} from "./clock.js"
	import { fade } from 'svelte/transition';
	let visible = true;

	let clock = new Clock(15, 20)

	function tick(){
		clock.tick()
		clock = clock
	}

	setInterval(tick,1000)

</script>

<main>
	<link rel="preconnect" href="https://fonts.googleapis.com">
	<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
	<link href="https://fonts.googleapis.com/css2?family=VT323&display=swap" rel="stylesheet">

		<div class="grid-container">

			<div class="leftClock">
				<h2>En deprimerande klocka</h2>
				<h3>{clock.time}</h3>
			</div>

			<div class="middleClock">
				<h2>en rolig klocka</h2>
				<svg id="svgClock" viewBox="-50 -50 100 100">
					<circle class="clockOuterRing"  r=48px />
			
					{#each [0, 5, 10, 15, 20, 25, 30, 35, 40, 45, 50, 55] as minutes}
						<line
							class="hour"
							y1="44"
							y2="38"
							transform="rotate({30 * minutes})"
						/>
			
						{#each [1, 2, 3, 4] as offset}
							<line
								class="minute"
								y1="44"
								y2="40"
								transform="rotate({6 * (minutes + offset)})"
							/>
						{/each}
			
					{/each}
			
					<line 
						class="hourHand"
						y1="30"
						y2="-3"
						transform="rotate({180 + (6/12) * (clock.clockMinute + clock.clockHour * 60)})"
					/>
			
					<line 
						class="minuteHand"
						y1="35"
						y2="-6"
						transform="rotate({180 + 6 * clock.clockMinute})"
					/>
				</svg>

				<button on:click={tick}>
					Ticking away the moments that make up a dull day
				</button>
			</div>
			
			<div class="rightClock">
				<h2>EN epileptisk klocka</h2>
				<h4>{clock.time}</h4>
				<input bind:value={clock.alarm} placeholder="Alarm Time" />
			</div>
		</div>

	{#if clock.isTriggered}
		<p transition:fade class="alarm">Joe Biden Wake Up </p>
	{/if}

</main>

<style>

	main {
		font-family: 'VT323', monospace;
	}

	#svgClock{
        width: 200px;
        height: 200px;
		display: block;
		margin: auto;
    }

    .clockOuterRing{
        stroke: rgb(34, 35, 87);
        fill: rgb(34, 35, 87);
        stroke-width: 1px;
    }

    .hour{
        stroke: rgb(255, 255, 255);
    }

    .minute{
        stroke: rgb(230, 176, 176);
    }

    .minuteHand{
        stroke: rgb(255, 0, 106);
        stroke-width: 1.2px;
    }

    .hourHand{
        stroke: rgb(255, 118, 0);
        stroke-width: 2px;
    }

	.grid-container{
		display: grid;
		grid-template-columns: repeat(3,auto);
	}

	.leftClock{
		width: 475px;
		height: 412px;
	}

	.middleClock{
		width: 475px;
		height: 412px;
	}

	.rightClock{
		width: 475px;
		height: 412;
	}

	@keyframes example {
		0%   {color:rgb(0, 134, 40); left:0px; top:0px;}
  		25%  {color:rgb(1, 20, 194); left:200px; top:0px;}
  		50%  {color:rgb(255, 0, 0); left:200px; top:200px;}
  		75%  {color:rgb(157, 255, 0); left:0px; top:200px;}
  		100% {color:rgb(224, 0, 224); left:0px; top:0px;}
	}

	@keyframes shake {
  		0% { transform: translate(1px, 1px) rotate(0deg); color:rgb(0, 134, 40);}
  		10% { transform: translate(-1px, -2px) rotate(-1deg); }
  		20% { transform: translate(-3px, 0px) rotate(1deg); color:rgb(1, 20, 194);}
		30% { transform: translate(3px, 2px) rotate(0deg); }
		40% { transform: translate(1px, -1px) rotate(1deg); }
		50% { transform: translate(-1px, 2px) rotate(-1deg); color:rgb(255, 0, 0);}
		60% { transform: translate(-3px, 1px) rotate(0deg); }
		70% { transform: translate(3px, 1px) rotate(-1deg); color:rgb(157, 255, 0);}
		80% { transform: translate(-1px, -1px) rotate(1deg); }
		90% { transform: translate(1px, 2px) rotate(0deg); }
		100% { transform: translate(1px, -2px) rotate(-1deg); color:rgb(224, 0, 224);}
	}

	h2 {
		text-align: center;
		color: white;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	h3 {
		padding: 3mm;
		color: rgb(34, 35, 87);
		font-size: 5em;
		font-weight: 50;
		text-align: center;
		margin: 0px;
	}

	h4 {
		padding: 3mm;
		font-size: 5em;
		font-weight: 50;
		margin: 0px;
		text-align: center;
		animation-name: shake;
  		animation-duration: 1s;
		animation-iteration-count: infinite;
	}

	.alarm {
		text-align: center;
		color: black;
		font-size: 2em;
		font-weight: 15;
	}

	button{
		display: block;
		margin: auto;
		margin-top: 20px;
	}

	input{
		display: block;
		margin: auto;
	}

	@media (max-width: 600px) {
		.grid-container{
			display: flex;
			flex-direction: column;
		}
	}

	:global(body){
		background-color: mediumslateblue;
	}
</style>