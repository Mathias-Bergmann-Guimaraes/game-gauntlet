<template>
  <div class="background-board">
    <input v-model="newName" placeholder="Enter player name">
    <button @click="addPlayer(newName)">Add Player</button>

    <div class="floating-ring" @drop="onDrop($event, 1)" @dragenter.prevent @dragover.prevent
      style="left: 36.5%; top: 68%;">
      <div v-for="player in getList(1)" :key="player.id" class="drag-el" draggable="true"
        @dragstart="startDrag($event, player)">
        {{ player.name }}
      </div>
    </div>

    <div class="floating-ring" @drop="onDrop($event, 2)" @dragenter.prevent @dragover.prevent
      style="left: 33.5%; top: 78%;">
      <div v-for="player in getList(2)" :key="player.id" class="drag-el" draggable="true"
        @dragstart="startDrag($event, player)">
        {{ player.name }}
      </div>
    </div>
    <div class="floating-ring" @drop="onDrop($event, 3)" @dragenter.prevent @dragover.prevent
      style="left: 37%; top: 87%;">
      <div v-for="player in getList(3)" :key="player.id" class="drag-el" draggable="true"
        @dragstart="startDrag($event, player)">
        {{ player.name }}
      </div>
    </div>
    <div class="floating-ring" @drop="onDrop($event, 4)" @dragenter.prevent @dragover.prevent
      style="left: 39%; top: 68%;">
      <div v-for="player in getList(4)" :key="player.id" class="drag-el" draggable="true"
        @dragstart="startDrag($event, player)">
        {{ player.name }}
      </div>
    </div>


  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const players = ref([
      { id: 0, name: "A", tile: 1 },
      { id: 1, name: "b", tile: 1 },
      { id: 2, name: "c", tile: 1 },
      { id: 3, name: "d", tile: 2 }
    ])

    const getList = (tile) => {
      return players.value.filter((player) => player.tile == tile)
    }

    const startDrag = (event, player) => {
      console.log(player)
      event.dataTransfer.dropEffect = 'move'
      event.dataTransfer.effectAllowed = 'move'
      event.dataTransfer.setData('playerID', player.id)
    }

    const onDrop = (event, tile) => {
      const playerID = event.dataTransfer.getData('playerID')
      const player = players.value.find((player) => player.id == playerID)
      player.tile = tile
    }

    const addPlayer = (name) => {
      console.log("LOL");

      players.value.push({ id: players.value.length, name: name, tile: 3 })
    }

    return {
      getList,
      startDrag,
      onDrop,
      addPlayer
    }
  }
}

</script>

<style scoped>
.background-board {
  background-image: url(../assets/Board_V5.png);
  background-size: contain;
  background-repeat: no-repeat;
  background-position: center;
  max-width: 100%;
  max-height: 100%;
  bottom: 0;
  left: 0;
  margin: auto;
  overflow: auto;
  position: fixed;
  right: 0;
  top: 0;
  -o-object-fit: contain;
  object-fit: contain;
}

.floating-ring {
  min-width: 5%;
  margin: 10px auto;
  background-color: red;
  min-height: 8.5%;
  position: absolute;
}
</style>