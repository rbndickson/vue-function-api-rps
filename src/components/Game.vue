<template>
  <div>
    <div v-if="isEditingName" class="emoji-button" @click="submitName">🆗</div>
    <div v-else class="emoji-button" @click="isEditingName = true">✏️</div>

    <div class="score">
      <div class="input-wrapper" v-if="isEditingName">
        <input v-model="playerName" @keyup.enter="submitName" type="text" maxlength="7" />
      </div>
      <div v-else>{{ playerName }}</div>
      <div>{{ playerScore }} - {{ computerScore }}</div>
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

    const playerName = value("Player");
    const isEditingName = value(false);

    const playerScore = value(0);
    const computerScore = value(0);

    const playerHand = value(null);
    const computerHand = value(null);

    const computeds = {
      playerDisplayEmoji: computed(() =>
        isShowGameHands.value
          ? handsToEmoji[playerHand.value]
          : handsToEmoji["rock"]
      ),
      computerDisplayEmoji: computed(() =>
        isShowGameHands.value
          ? handsToEmoji[computerHand.value]
          : handsToEmoji["rock"]
      )
    };

    function sumbmitHand(hand) {
      playerHand.value = hand;
      runGame();
    }

    function randomHand() {
      const hands = Object.keys(handsToEmoji);
      return hands[Math.floor(Math.random() * hands.length)];
    }

    function addPointToWinner() {
      const handToWeakness = {
        rock: "paper",
        scissors: "rock",
        paper: "scissors"
      };

      if (handToWeakness[computerHand.value] === playerHand.value) {
        playerScore.value++;
      } else if (handToWeakness[playerHand.value] === computerHand.value) {
        computerScore.value++;
      }
    }

    function runGame() {
      computerHand.value = randomHand();
      isShowGameHands.value = true;
      addPointToWinner();
    }

    function submitName() {
      isEditingName.value = false;
    }

    return {
      isShowGameHands,
      playerName,
      isEditingName,
      playerScore,
      computerScore,
      playerHand,
      computerHand,
      sumbmitHand,
      submitName,
      ...computeds
    };
  }
};
</script>

<style>
.score {
  display: flex;
  justify-content: space-between;
  margin-top: 40px;
  font-size: 18px;
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
.score div {
  padding: 5px 0;
}
.score .input-wrapper {
  padding: 0;
}
input[type="text"] {
  width: 110px;
  padding: 5px;
  margin: 0 0 0 15px;
  border: 2px solid #ccc;
  border-radius: 5px;
  font-family: "Courier New", Courier, monospace;
}
.emoji-button {
  position: fixed;
  top: 10px;
  left: 10px;
  cursor: pointer;
}
</style>
