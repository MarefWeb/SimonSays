<template>
  <div class="wrapper">
		<h1>Simon Says</h1>
    <Simon @mouse-up="mouseUp" @mouse-down="mouseDown" :buttons="buttons" :interectiveMode="interectiveMode" />
    <Info @start="start" :round="round" :roundsPassed="roundsPassed" :lose="lose" />
    <Options @changed-mode="changedMode" :mode="mode" />
  </div>
</template>

<script>
import Simon from '@/components/Simon'
import Info from '@/components/Info'
import Options from '@/components/Options'

export default {
  name: 'app',

	data() {
		return {
			gameSequence: [],
			userSequence: [],
			mode: '',
			roundsPassed: 0,
			round: 0,
			started: false,
			lose: false,
			buttons: {
				1: { id: 1, color: 'red', isActive: false, sound: new Audio(require('@/assets/sounds/1.mp3')) },
				2: { id: 2, color: 'blue', isActive: false, sound: new Audio(require('@/assets/sounds/2.mp3')) },
				3: { id: 3, color: 'yellow', isActive: false, sound: new Audio(require('@/assets/sounds/3.mp3')) },
				4: { id: 4, color: 'green', isActive: false, sound: new Audio(require('@/assets/sounds/4.mp3')) },
			},
			allDelays: {'easy': 1500, 'normal': 1000, 'hard': 400},
			delay: 0,
			interectiveMode: false
		}
	},

	methods: {
		// **Main methods**
		start() {
			if(!this.started) {
				this.lose = false;
				this.started = true;
				console.log('The game started...');
				this.delay = this.allDelays[this.mode]
				this.newRound();
			}
		},


		newRound() {
			this.round++;
			this.gameSequence.push(this.buttons[this.randomNumber()]);
			this.show(this.gameSequence);
		},

		show(sequence) {
			let i = 0;

			let interval = setInterval(() => {
				let button = sequence[i];

				button.sound.play();

				button.isActive = true;
				setTimeout(() => {
					button.isActive = false
				}, this.delay/2);

				i++;

				if(i == sequence.length) {
					clearInterval(interval);
					this.interectiveMode = true;
				}
			
			}, this.delay)
		},

		mouseDown(button_number) {
			if(this.interectiveMode) {
				let button = this.buttons[button_number]

				button.sound.play();
				button.isActive = true;
				
				this.userSequence.push(button);
			}
		},

		mouseUp(button_number) {
			if(this.interectiveMode) {
				this.checkLose();
				this.buttons[button_number].isActive = false;
			}
		},

		checkLose() {
			if(this.gameSequence.length === this.userSequence.length) {
				if(this.gameSequence.every((v, i) => v === this.userSequence[i])) {
					this.interectiveMode = false;
					this.userSequence = [];
					this.newRound();
				}
	
				else {
					this.endGame();
				}
			}

			else {
				if(this.userSequence.every((v, i) => v !== this.gameSequence[i])) {
					this.endGame();
				}
			}
		},

		endGame() {
			console.log('Game over!');
			this.interectiveMode = false;
			this.started = false;
			this.roundsPassed = this.round;
			this.round = 0;
			this.lose = true;
			this.gameSequence = [];
			this.userSequence = [];
		},

		// **Support methods**
		changedMode(data) {
			this.mode = data
		},

		randomNumber() {
			return Math.floor(Math.random() * 4 + 1)
		}

	},

  components: {
    Simon,
    Info,
    Options
  }
}
</script>

<style lang="sass" scoped>
.wrapper
	width: 540px
	margin: 0 auto

</style>

<style lang="sass">
body
	font-family: Arial, serif
	color: #333
	-webkit-user-select: none      
	-moz-user-select: none
	-ms-user-select: none
	-o-user-select: none
	user-select: none

h1 
	margin: 1em 0 2em
	text-align: center

ul 
	list-style: none

ul, li
	padding: 0
	margin: 0

.hoverable
  &:hover
    cursor: pointer

</style>