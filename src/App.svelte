
<main>
	<h1>Stretch Timer</h1>

	<input type="number" placeholder="Interval">

	<input type="number" placeholder="Breaks">



	<button disabled={timerRunning || pause} on:click={startStopwatch}>Start</button>
	<button on:click={pauseStopwatch}>{pause ? "Continue" : "Pause"}</button>
	<button on:click={resetStopwatch}>Reset Timer</button>

	<div>{stopwatchValue}</div>


</main>

<script>

let stopwatchValue = 0
let time
let pause = false
let timerRunning = false

const startStopwatch = () => {
	timerRunning = true
	pause = false
	time = setInterval(function(){ stopwatchValue += 1 }, 1000);
}
const pauseStopwatch = () => {
	if (stopwatchValue === 0) {
		return
	}
	if (pause) {
		startStopwatch()
	} else {
		timerRunning = false
		clearInterval(time)
		pause = true
	}
}

const resetStopwatch = () => {
	timerRunning = false
	pause = false
	clearInterval(time)
	stopwatchValue = 0
}
</script>












<style>

</style>