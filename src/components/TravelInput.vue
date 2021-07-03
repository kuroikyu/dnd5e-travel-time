<template>
	<section>
		<h2>It's Travel Time!</h2>
		<form action="" class="inputs">
			<div class="input-group short">
				<label for="travel-distance" class="input-label">Travel distance (in miles)</label>
				<input
					type="text"
					id="travel-distance"
					placeholder="100"
					v-model.number="travel.distance"
				/>
			</div>
			<div class="input-group short">
				<label for="travel-pace" class="input-label">Travel pace (in feets)</label>
				<input type="text" id="travel-pace" placeholder="30" v-model.number="travel.pace" />
			</div>
			<div class="input-group long">
				<label class="input-label">Travel form</label>

				<div style="display: flex; align-content: center; justify-content: space-evenly">
					<div>
						<label for="normal-travel">Normal</label>
						<input type="radio" id="normal-travel" v-model="travel.type" value="normal" />
					</div>
					<div>
						<label for="special-travel">Special</label>
						<input type="radio" id="special-travel" v-model="travel.type" value="special" />
					</div>
				</div>
			</div>
		</form>
	</section>
	<section>
		<p class="travel-description">
			Travelling {{ travel.distance }} miles at a pace of {{ theSpeed }} feet.
		</p>
		<!-- <table style="width: 75%">
			<tr>
				<th>Pace</th>
				<th>Effective speed</th>
				<th>Time to travel</th>
			</tr>
			<tr>
				<td>Fast</td>
				<td>{{ fastSpeed }} miles/day</td>
				<td>
					{{ calculateFastTravelTime }}
				</td>
			</tr>
			<tr>
				<td>Normal</td>
				<td>{{ normalSpeed }} miles/day</td>
				<td>
					{{ calculateNormalTravelTime }}
				</td>
			</tr>
			<tr>
				<td>Slow</td>
				<td>{{ slowSpeed }} miles/day</td>
				<td>
					{{ calculateSlowTravelTime }}
				</td>
			</tr>
		</table> -->
	</section>
	<section>
		<div class="flex-display">
			<div class="speed-box slow">
				<span
					><svg
						xmlns="http://www.w3.org/2000/svg"
						width="24"
						height="24"
						viewBox="0 0 24 24"
						fill="none"
						stroke="currentColor"
						stroke-width="2"
						stroke-linecap="round"
						stroke-linejoin="round"
					>
						<polyline points="9 18 15 12 9 6"></polyline></svg
				></span>
				<strong
					><span>{{ calculateSlowTravelTime }}</span></strong
				>
				<span>@ {{ slowSpeed }} miles/day</span>
				<span></span>
				<span>Can Stealth</span>
			</div>
			<div class="speed-box normal">
				<span
					><svg
						xmlns="http://www.w3.org/2000/svg"
						width="24"
						height="24"
						viewBox="0 0 24 24"
						fill="none"
						stroke="currentColor"
						stroke-width="2"
						stroke-linecap="round"
						stroke-linejoin="round"
					>
						<polyline points="13 17 18 12 13 7"></polyline>
						<polyline points="6 17 11 12 6 7"></polyline></svg
				></span>
				<strong
					><span>{{ calculateNormalTravelTime }}</span></strong
				>
				<span>@ {{ normalSpeed }} miles/day</span>
				<span></span>
				<span>-</span>
			</div>
			<div class="speed-box fast">
				<span
					><svg
						xmlns="http://www.w3.org/2000/svg"
						width="24"
						height="24"
						viewBox="0 0 24 24"
						fill="none"
						stroke="currentColor"
						stroke-width="2"
						stroke-linecap="round"
						stroke-linejoin="round"
					>
						<polyline points="16 17 21   12 16 7"></polyline>
						<polyline points="9 17 14 12 9 7"></polyline>
						<polyline points="2 17 7 12 2 7"></polyline></svg
				></span>
				<strong
					><span>{{ calculateFastTravelTime }}</span></strong
				>
				<span>@ {{ fastSpeed }} miles/day</span>
				<span></span>
				<span>-5 Passive</span>
				<span>Perception</span>
			</div>
		</div>
	</section>
</template>

<script>
export default {
	name: 'TravelInput',
	props: {
		msg: String,
	},
	data() {
		return {
			travel: {
				distance: 90,
				pace: 30,
				type: 'normal',
			},
		}
	},
	computed: {
		theSpeed: function () {
			if (this.travel.type === 'normal') {
				return 30
			}
			return this.travel.pace
		},

		fastSpeed: function () {
			let speed = this.travel.pace
			let baseSpeed = (speed / 10) * 8

			if (this.travel.type === 'normal') {
				return 30
			}
			// else
			return (baseSpeed + baseSpeed * (1 / 3)).toFixed(1)
		},

		normalSpeed: function () {
			let speed = this.travel.pace
			let baseSpeed = (speed / 10) * 8

			if (this.travel.type === 'normal') {
				return 24
			}
			// else
			return baseSpeed.toFixed(1)
		},

		slowSpeed: function () {
			let speed = this.travel.pace
			let baseSpeed = (speed / 10) * 8

			if (this.travel.type === 'normal') {
				return 18
			}
			// else
			return (baseSpeed - baseSpeed * (1 / 3)).toFixed(1)
		},

		calculateFastTravelTime: function () {
			let days = (this.travel.distance / this.fastSpeed).toFixed(1)

			if (days < 1) {
				return `${days * 8} hours`
			}

			return `${days} days`
		},

		calculateNormalTravelTime: function () {
			let days = (this.travel.distance / this.normalSpeed).toFixed(1)

			if (days < 1) {
				return `${days * 8} hours`
			}

			return `${days} days`
		},

		calculateSlowTravelTime: function () {
			let days = (this.travel.distance / this.slowSpeed).toFixed(1)

			if (days < 1) {
				return `${days * 8} hours`
			}

			return `${days} days`
		},
	},
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
* {
	box-sizing: border-box;
}
#app {
	font-family: 'Avenir', Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	color: #2c3e50;
	margin-top: 60px;
}
@media screen and (min-width: 1000px) {
	#app {
		padding: 0 10%;
	}
}
@media screen and (min-width: 1400px) {
	#app {
		padding: 0 20%;
	}
}
#copy {
	width: 0;
	height: 0;
	opacity: 0;
}
h1 {
	text-align: center;
}
section {
	padding: 20px 10%;
}
ul {
	padding: 0;
}
li {
	list-style-type: none;
}
li.highlight-delete .input-group label {
	color: #a44;
}
li.highlight-delete .input-group input {
	background: #fee;
	color: #a44;
}
.input-label {
	display: block;
	text-align: left;
	margin-bottom: 6px;
	font-size: 12px;
	text-transform: uppercase;
}
input[type='text'] {
	padding: 0.7em;
	background: #fafafa;
	border: 1px solid #dddddd;
	border-radius: 3px;
	font-family: 'Dank Mono', 'Fira Code', 'Source Code Pro', monospace;
	margin-bottom: 20px;
	width: 100%;
}
input[type='checkbox'] {
	display: none;
}
section.tasks label {
	padding: 2em 2em 2em 0;
}
section.tasks input ~ label .checkbox {
	height: 0.8em;
	width: 0.8em;
	display: inline-block;
	background: #fafafa;
	margin-right: 0.5em;
	border: 1px solid #ddd;
	border-radius: 3px;
}
section.tasks input:checked ~ label .checkbox {
	background: #009844;
}
.input-group.long {
	grid-column: span 2;
}
.input-group-button {
	display: flex;
	flex-direction: row;
	border: 1px solid #dddddd;
	border-radius: 3px;
	background: #fafafa;
	padding: 2px;
	margin-bottom: 1em;
}
.input-group-button input {
	flex-grow: 2;
	border: none;
	background: unset;
	margin: 0;
	padding: calc(0.7em - 2px);
}
.input-group-button button {
	font-size: 0.6em;
	border-radius: 3px;
	text-transform: uppercase;
	border: none;
	background: #666666;
	color: white;
	padding: 1em;
}
button {
	font-size: 0.6em;
	border-radius: 3px;
	text-transform: uppercase;
	border: none;
	background: #666;
	color: white;
	padding: 1.6em 1em;
	transition: background ease-in-out 120ms;
}
button:hover {
	background: #444;
}
button.delete:hover {
	background: #a44;
}
hr {
	width: 100%;
	margin-bottom: 2em;
	opacity: 0.5;
}
section .inputs {
	display: grid;
	grid-template-columns: repeat(2, 1fr);
	grid-column-gap: 20px;
}
.inputs li {
	display: contents;
}
li button {
	margin-top: 19px;
	margin-bottom: 20px;
}
.center {
	text-align: center;
}
.center button:first-child {
	margin-right: 1em;
}
.flex-display {
	display: flex;
	justify-content: space-evenly;
}
.speed-box {
	background: rgb(195, 214, 223);
	padding: 10px;

	display: flex;
	flex-direction: column;
	row-gap: 10px;
	align-items: center;

	width: 25%;
	max-width: 200px;
}
.speed-box.slow {
	background: rgb(250, 231, 210);
}
.speed-box.fast {
	background: rgb(178, 226, 220);
}
table {
	display: none;
}
@media screen and (max-width: 600px) {
	section {
		padding: 15px 5%;
	}
	.flex-display {
		display: flex;
		justify-content: space-between;
	}
	.speed-box {
		width: 31%;
	}
	.travel-description {
		text-align: center;
	}
}
</style>
