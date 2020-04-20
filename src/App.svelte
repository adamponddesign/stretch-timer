
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

	{#if stretchHoldTime && restTimeInput}
	<div class="timer-display">
		<div>Stretch for <span>{timeDisplay}</span>seconds</div>
		<div>Rest for <span>{restTime}</span>seconds</div>
	</div>

	<div class="button-container">
		<button on:click={startStretchCountdown}>Start</button>
		<!-- <button disabled={!timerRunning || pause} on:click={pauseStopwatch}>{pause ? "Continue" : "Pause"}</button> -->
		<!-- <button on:click={resetStopwatch}>Reset</button> -->
	</div>
	{/if}


</main>

<script>


let interval
let intervalRest
let timerRunning = false
let stretchHoldTime
let secs = 0
let restTimeInput

$: timeDisplay = stretchHoldTime || ''
$: restTime = restTimeInput || ''

$: restInterval = restTime * 1000

$: console.log(restInterval)

const startStretchCountdown = () => {
	interval = setInterval(function(){ timeDisplay -= 1 }, 1000);
}

const stopStretchCountdown = () => {
	clearInterval(interval)
}

const startRestCountdown = () => {
	intervalRest = setInterval(function(){ restTime -= 1 }, 1000);
}

const stopRestCountdown = () => {
	clearInterval(intervalRest)
}


const resetStretchCountdown = () => {
	timeDisplay = stretchHoldTime
}
const resetRestCountdown = () => {
	timeDisplay = stretchHoldTime
	restInterval = restTime * 1000
}

$: if (timeDisplay === 0) {
	stopStretchCountdown()
	startRestCountdown()
	setTimeout(resetStretchCountdown, restInterval)
}

$: if (restTime === 0) {
		stopRestCountdown()
		startStretchCountdown()
		setTimeout(resetRestCountdown, restInterval)
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

	span {
		color: red;
		font-size: 60px;
	}

	.timer-display {
		text-align: center;
	}

	.timer-display div {
		width: 100%;
	}
</style>