<script setup>
import { ref, onMounted } from "vue";

// Fetch JSON files
const homepageSettings = ref(null);
const generalSettings = ref(null);
const isLoading = ref(true);
const hasError = ref(false);

// Fetch and load settings
onMounted(async () => {
  try {
    const homepageResponse = await fetch("/_data/homepage.json");
    const settingsResponse = await fetch("/_data/settings.json");

    if (!homepageResponse.ok || !settingsResponse.ok) {
      throw new Error("Failed to fetch settings");
    }

    homepageSettings.value = await homepageResponse.json();
    generalSettings.value = await settingsResponse.json();
    isLoading.value = false;
  } catch (error) {
    hasError.value = true;
    console.error("Error loading settings:", error);
  }
});
</script>

<template>
  <div>
    <MouseGradient />
    <!-- Loading State -->
    <div v-if="isLoading" class="flex items-center justify-center h-screen">
      <p>Loading...</p>
    </div>

    <!-- Error State -->
    <div v-else-if="hasError" class="flex items-center justify-center h-screen">
      <p>Error loading settings. Please try again later.</p>
    </div>

    <!-- Main Content -->
    <div v-else class="relative">
      <!-- Background -->
<!--       <div
        class="absolute inset-0 bg-cover bg-center"
        :style="{ backgroundImage: homepageSettings?.thumbnail ? `url(${homepageSettings.thumbnail})` : 'none'}"
      ></div> -->

      <!-- Menu or Drawer -->
      <div class="relative z-10">
        <Drawer />
      </div>

      <!-- Title Section -->
      <div class="title-container flex justify-center content-center bg">
        <div class="h-0">
            <h1 class=" text-6xl lg:text-8xl font-bold mt-[35vh]">
              {{ generalSettings?.site_title || "Default Title" }}
            </h1>
        </div>
      </div>
      <!-- Background Layer -->
<!--       <div class="absolute bottom-0 left-0 w-full h-[100vh] bg-[#F7DCE4]" style="z-index: -1;"></div> -->
<TrailImg />
    </div>

    <!-- Load pages -->
	<WorksTable />
  </div>
  
</template>

<style>
</style>
