
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
        <div id="player-1" draggable="true" @dragstart="handleDragstart" @drag="handleDrag">
          player 1
        </div>
      </div>
    </div>
    <div class="field">
      <div class="dropzone" dropzone="true" @drop="handleDrop" @dragover="handleDragover"></div>
      <h3>Rect: {{ rectPos }}</h3>
      <h3>Absolute: {{ absPos }}</h3>
      <h3>Relative: {{ dragPos }}</h3>
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

  const el = document.getElementById('player-1')
  const p1a = Math.floor(el.getBoundingClientRect().left)
  const p1b = Math.floor(el.getBoundingClientRect().top)

  console.log(`cursor: ${event.clientX}, ${event.clientY}`)
  console.log(
    `boxsor: ${Math.floor(el.getBoundingClientRect().left)}, ${Math.floor(
      el.getBoundingClientRect().top
    )}`
  )
}

const handleDrop = (event) => {
  event.preventDefault()
  const data = event.dataTransfer.getData('text/plain')
  event.target.appendChild(document.getElementById(data))

  const el = document.getElementById('player-1')

  console.log(
    `NEW boxsor: ${Math.floor(el.getBoundingClientRect().left)}, ${Math.floor(
      el.getBoundingClientRect().top
    )}`
  )
  el.style.position = 'absolute'
  el.style.left = event.clientX - Math.floor(el.getBoundingClientRect().left) + 'px'
  el.style.top = event.clientY - Math.floor(el.getBoundingClientRect().top) + 'px'
  // console.log('XXXX: ', el.style.left, el.style.top)
}
</script>


