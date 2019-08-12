<template>
  <div>
    <div class="score">
      <div>Player</div>
      <div>{{playerScore}} - {{computerScore}}</div>
      <div>Computer</div>
    </div>
    <div class="player-hands">
      <div>{{ playerDisplayEmoji }}</div>
      <div>{{ computerDisplayEmoji }}</div>
    </div>
    <ul class="hand-choices">
      <li :class="{ selected: playerHand === 'rock' }" @click="sumbmitHand('rock')">✊</li>
      <li :class="{ selected: playerHand === 'scissors' }" @click="sumbmitHand('scissors')">✌️</li>
      <li :class="{ selected: playerHand === 'paper' }" @click="sumbmitHand('paper')">🖐️</li>
    </ul>
  </div>
</template>

<script>
import { value, computed } from "vue-function-api";

export default {
  setup() {
    const handsToEmoji = { rock: "✊", scissors: "✌️", paper: "🖐️" };

    const isShowGameHands = value(false);

    const playerScore = value(0);
    const computerScore = value(0);

    const playerHand = value(null);
    const computerHand = value(null);

    const playerDisplayEmoji = computed(() =>
      isShowGameHands.value
        ? handsToEmoji[playerHand.value]
        : handsToEmoji["rock"]
    );

    const computerDisplayEmoji = computed(() =>
      isShowGameHands.value
        ? handsToEmoji[computerHand.value]
        : handsToEmoji["rock"]
    );

    function sumbmitHand(hand) {
      playerHand.value = hand;
      runGame();
    }

    function randomHand() {
      const hands = Object.keys(handsToEmoji);
      return hands[Math.floor(Math.random() * hands.length)];
    }

    function runGame() {
      computerHand.value = randomHand();
      isShowGameHands.value = true;
    }

    return {
      isShowGameHands,
      playerScore,
      computerScore,
      playerHand,
      computerHand,
      sumbmitHand,
      playerDisplayEmoji,
      computerDisplayEmoji
    };
  }
};
</script>

<style>
.score {
  display: flex;
  justify-content: space-between;
  margin-top: 40px;
  font-size: 5vw;
  font-weight: bold;
}
.score div:nth-child(1) {
  width: 35%;
  text-align: right;
}
.score div:nth-child(2) {
  width: 30%;
  text-align: center;
}
.score div:nth-child(3) {
  width: 35%;
  text-align: left;
}
.player-hands {
  display: flex;
  justify-content: space-between;
  margin-top: 80px;
  font-size: 20vh;
}
.hand-choices {
  display: flex;
  justify-content: space-between;
  margin-top: 60px;
  padding: 0;
}
.hand-choices li {
  font-size: 15vh;
  list-style: none;
  cursor: pointer;
}
.hand-choices li.selected {
  text-decoration: lightblue underline;
  transition: font-size 0.2s;
}
</style>
