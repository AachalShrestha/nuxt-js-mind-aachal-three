<template>
  <div class="opacity-80 animate-fade animate-once animate-delay-[10ms] pt-5">
    <div v-show="navigations.mainmenu?.mainavigation_on_off">
      <div class="animate-fade animate-once animate-delay-[150ms]">
        <NuxtLink to="/" class="border-none home-button">Home</NuxtLink>

        <!-- Dropdown -->
        <el-collapse v-model="activePanels" accordion>
          <el-collapse-item title="Works" name="1" class="custom-collapse-item works-nav">
            <MainNavigation />
          </el-collapse-item>
        </el-collapse>
        <NuxtLink to="/about" class="border-none home-button">About me</NuxtLink>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import MainNavigation from './global/navs/MainNavigation.vue';

// Initialize navigation with a default structure
const navigations = ref({
  mainmenu: {
    mainavigation_on_off: false,
  },
});

// Load navigation data
const { data, error } = await useFetch('/_data/menus.json');

// Set navigation data if available
if (data.value) {
  navigations.value = data.value;
} else if (error.value) {
  console.error('Error loading navigations:', error.value);
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&display=swap');

hr {
  opacity: 0.1;
}
.el-collapse-item__header{
  border: none;
}

.custom-collapse-item{
  border: none;
}

.custom-collapse-item button{
  background-color: transparent;
  font-family: 'poppins', sans-serif;
  font-size: 32px;
  font-weight: 600;
  border: none;
}

.home-button{
  font-family: 'poppins', sans-serif;
  font-size: 32px;
  font-weight: 600;
  border-style: none;
}

.dark-mode .el-collapse-item__header {
  color: white !important; /* Change to your desired color */
}

.dark-mode .el-collapse-item__wrap{
  background-color: transparent;
  color: white;
}

.dark-mode a{
  color: white;
}
</style>
