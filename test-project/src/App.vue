<template>
  <div
    class="flex h-screen w-screen flex-col items-center justify-center bg-slate-400"
  >
    <div class="flex">
      <div v-for="x in GameSpaceArr">
        <div v-for="y in x">
          <div v-show="y != 1" class="h-10 w-10 border-[1px] bg-slate-600">
            {{ y }}
          </div>
        </div>
      </div>
    </div>

    {{ GameSpaceArr[0][0] }}
    {{ playerRun }}
    {{ gameStartState }}
    <button
      @click="gameStartState = true"
      class="h-10 w-20 rounded-lg bg-slate-500"
    >
      start
    </button>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";

const Gamebackground = ref({ X: 12, Y: 12 });

let GameSpaceArr = [
  [0, 0, 0, 0],
  [0, 0, 0, 0],
];
let GameSpaceY = [];

for (let SpaceX = 0; SpaceX < Gamebackground.value.X; SpaceX++) {
  for (let SpaceY = 0; SpaceY < Gamebackground.value.Y; SpaceY++) {
    if (SpaceX == 0) {
      GameSpaceY[SpaceY] = 1;
    } else if (SpaceX == Gamebackground.value.X - 1) {
      GameSpaceY[SpaceY] = 1;
    } else if (SpaceY == 0) {
      GameSpaceY[SpaceY] = 1;
    } else if (SpaceY == Gamebackground.value.Y - 1) {
      GameSpaceY[SpaceY] = 1;
    } else {
      GameSpaceY[SpaceY] = 0;
    }
    if (SpaceY === Gamebackground.value.Y - 1) {
      GameSpaceArr[SpaceX] = GameSpaceY;
      GameSpaceY = [];
    }
    console.log(GameSpaceY);
  }
}

const gameStartState = ref(false);
const player = ref(0);

const playerRun = computed(() => {
  if (gameStartState.value) {
    player.value = 1;
  }
  return player.value;
});
</script>
