<template>
    <div class="opacity-80 animate-fade animate-once animate-delay-[100ms]">
      <div
      class="text-2xl font-bold">
      <h3>{{ settings.site_title }}</h3></div>
      <div class="text-sm opacity-80">
      <p>{{ settings.site_subtitle }}</p>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  
  const settings = ref({});
  // Use useFetch to load the JSON data from the public folder
  const { data, error } = await useFetch('/_data/settings.json');
  
  // Set the data to the settings ref
  if (data.value) {
    settings.value = data.value;
  } else if (error.value) {
    console.error('Error loading settings:', error.value);
  }
  </script>

  <style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&display=swap');

h3{
  font-family: 'Poppins', sans-serif;
  font-weight: 400;
}
</style>