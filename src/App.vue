<template>
	<div id="app">
		<div class="wrapper clearfix">
			<players 
				v-bind:activePlayer="activePlayer"
				v-bind:currentScore="currentScore"
				v-bind:scoresPlayer="scoresPlayer"
			></players>
			<controls
				v-on:handleRollDice="handleRollDice"
				v-on:handleNewGame="handleNewGame"
			/>
			<dices
				v-bind:dices="dices"
			/>
            <popup-rule
				v-bind:isOpenPopup="isOpenPopup"
				v-on:handleConfirmPlaying="handleConfirmPlaying"
			/>
        </div>
	</div>
</template>

<script>
import Players from './components/Players.vue'
import Controls from './components/Controls.vue'
import Dices from './components/Dices.vue'
import PopupRule from './components/PopupRule.vue'

export default {
	name: 'app',
	data () {
		return {
			isPlaying: false,
			isOpenPopup: false,
			activePlayer: 0,
			scoresPlayer: [13, 30],
			currentScore: 30,
			dices: [1, 6]
		}
	},
	components: {
		Players,
		Controls,
		Dices,
		PopupRule
	},
	methods: {
		handleNewGame() {
			console.log('hadle new game app.vue');
			// hien thi popup -> show lua choi
			this.isOpenPopup = true
		},
		handleConfirmPlaying() {
			this.isPlaying = true
			this.isOpenPopup = false
			this.activePlayer = 0
			this.currentScore = 0
			this.scoresPlayer = [0, 0]
			this.dices=[1, 1]
		},
		handleRollDice() {
			if(this.isPlaying) {
				var diceOne = Math.floor(Math.random() * 6) + 1
				var diceTwo = Math.floor(Math.random() * 6) + 1
				this.dices = [diceOne, diceTwo]
				if(diceOne === 1 || diceTwo === 1) {
					let activePlayer = this.activePlayer
					setTimeout(() => {
						alert(`Player ${activePlayer + 1} đã quay trúng 1. Rất tiếc!`)
					}, 10)
					// alert(`Player ${this.activePlayer + 1} đã quay trúng 1. Rất tiếc!`)
					this.nextPlayer()
				}else {
					// cộng dồn điểm tạm thời cho người đang chơi
					this.currentScore = this.currentScore + diceOne + diceTwo
				}
			}else {
				alert('Vui lòng nhấn newgame')
			}
		},
		nextPlayer() {
			this.activePlayer = this.activePlayer === 0 ? 1 : 0
			this.currentScore = 0
		}
	}
}
</script>

<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    
}

.clearfix::after {
    content: "";
    display: table;
    clear: both;
}

body {
    background-image: linear-gradient(rgba(62, 20, 20, 0.4), rgba(62, 20, 20, 0.4)), url('/public/assets/back.jpg');
    background-size: cover;
    background-position: center;
    font-family: Lato;
    font-weight: 300;
    position: relative;
    height: 100vh;
    color: #555;
}

.wrapper {
    width: 1000px;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background-color: #fff;
    box-shadow: 0px 10px 50px rgba(0, 0, 0, 0.3);
    overflow: hidden;
}
</style>
