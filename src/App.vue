
<template>
  <header>
    <h1>comic builder</h1>
    <!-- <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
      </nav> -->
  </header>
  <!-- <RouterView /> -->
  <div class="stadium">
    <div class="dugout" dropzone="true" @drop="handleDrop" @dragover="handleDragover">
      <h2>dugout</h2>
      <div class="dropzone" id="dugout">
        <!-- PLAYERS -->
        <div id="player-1" draggable="true" @dragstart="handleDragstart" @drag="handleDrag">
          some text
        </div>
      </div>
    </div>
    <div class="field">
      <h2>field</h2>
      <div class="dropzone" dropzone="true" @drop="handleDrop" @dragover="handleDragover"></div>
    </div>
  </div>
</template>

<script setup>
// import { RouterLink, RouterView } from 'vue-router'
import { ref, computed, onMounted } from 'Vue'

// DRAG STUFF
const handleDragstart = (event) => {
  event.dataTransfer.setData('text/plain', event.target.id)

  event.dataTransfer.dropEffect = 'move'
}

const handleDragover = (event) => {
  event.preventDefault()
  event.dataTransfer.dropEffect = 'move'
}

const handleDrop = (event) => {
  event.preventDefault()

  const data = event.dataTransfer.getData('text/plain')

  event.target.appendChild(document.getElementById(data))
}
</script>


