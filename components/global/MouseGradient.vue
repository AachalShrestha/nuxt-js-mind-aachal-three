<template>
  <div>
    <!-- The div that follows the mouse -->
    <div
      class="follower"
      :style="{ top: `${position.y}px`, left: `${position.x}px` }"
    >
      <img src="/img/Gradient.png" alt="Follower Image" />
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from "vue";

// Reactive object to store mouse position
const position = ref({ x: 0, y: 0 });

const updatePosition = (event) => {
  // Use pageX and pageY to account for scrolling
  position.value.x = event.pageX ;
  position.value.y = event.pageY ;
};

onMounted(() => {
  // Add event listener when component is mounted
  window.addEventListener("mousemove", updatePosition);
});

onUnmounted(() => {
  // Remove event listener when component is unmounted
  window.removeEventListener("mousemove", updatePosition);
});
</script>

<style scoped>
.follower {
  position: absolute;
  width: 350px; /* Adjust size as needed */
  height: 350px;
  pointer-events: none; /* Prevent the div from interfering with mouse events */
  transform: translate(-50%, -50%); /* Center the image on the cursor */
}

.follower img {
  width: 100%;
  object-fit: cover;
  opacity: 0.2; /* 50% transparent */
}
  
</style>
