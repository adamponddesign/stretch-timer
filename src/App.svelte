
<main>
	<h1>Stretch Timer</h1>

	<div class="input-container">
		<label for="stretch-hold">Hold stretch for?</label>
		<input id="stretch-hold" bind:value={stretchHoldTime} type="number">
	</div>
	<div class="input-container">
		<label for="rest-time">How much rest?</label>
		<input id="rest-time"bind:value={restTimeInput} type="number">
	</div>



	<div class="button-container">
		<button disabled={timerRunning || pause} on:click={startStopwatch}>Start</button>
		<button on:click={pauseStopwatch}>{pause ? "Continue" : "Pause"}</button>
		<button on:click={resetStopwatch}>Reset Timer</button>
	</div>

	<div>Stretch Timer = {mins} : {secs < 10 ? 0 : ''}{secs}</div>
	<div>Rest Timer = {restTime ? restTime : 0}</div>

	<div class="message">{message}</div>
</main>

<script>

let stopwatchValue = 0
let interval
let intervalRest
let pause = false
let timerRunning = false
let stretchHoldTime
let message = ''
let secs = 0
let restTime = '0'
let restTimeInput

$: restTime = restTimeInput
$: mins = Math.floor((stopwatchValue % 3600) / 60)
$: secs = Math.floor(stopwatchValue % 60)

const startStopwatch = () => {
	message = 'Stretch'
	timerRunning = true
	pause = false
	interval = setInterval(function(){ stopwatchValue += 1 }, 1000);
}
const pauseStopwatch = (restTime) => {
	if (stopwatchValue === 0) {
		return
	}
	if (pause) {
		startStopwatch()
	} else {
		timerRunning = false
		message = 'Timer Paused'
		clearInterval(interval)
		pause = true
	}
}

const resetStopwatch = () => {
	message = ''
	timerRunning = false
	pause = false
	clearInterval(interval)
	stopwatchValue = 0
}


$: if (secs === stretchHoldTime) {
	restTimerStartCountdown()
}

$: if (restTime === 0) {
		clearInterval(intervalRest)
		startStopwatch()
		restTime = restTimeInput
	}

const restTimerStartCountdown = () => {
	message = 'rest'
	pauseStopwatch()
	intervalRest = setInterval(function(){ restTime -= 1 }, 1000);
	
}



</script>












<style>

	main {
		width: 600px;
		margin: 0 auto;
	}

	h1 {
		text-align: center;
	}

	input {
		width: 100px;
		margin: 10px 20px;
	}
	.input-container {
		display: flex;
		align-items: baseline;
    justify-content: center;
	}

	.message {
		font-size: 30px;
		color: red;
	}
</style>