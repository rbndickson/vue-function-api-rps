<template>
  <div>
    <div class="score">
      <div>Player</div>
      <div>{{playerScore}} - {{computerScore}}</div>
      <div>Computer</div>
    </div>
    <div class="player-hands">
      <div>✊</div>
      <div>✊</div>
    </div>
    <ul class="hand-choices">
      <li>✊</li>
      <li>✌️</li>
      <li>🖐️</li>
    </ul>
  </div>
</template>

<script>
import { value } from "vue-function-api";

export default {
  setup() {
    const playerScore = value(0);
    const computerScore = value(0);

    return {
      playerScore,
      computerScore
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
}
</style>
