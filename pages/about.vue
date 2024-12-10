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
    <div v-else class="h-screen relative">
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
      <div class="title-container flex justify-center content-center h-screen">
        <div class="h-0">
            <h1 class="text-8xl font-bold mt-[20%]">
              {{ aboutSettings?.site_title || "About Meeee" }}
            </h1>
            <p>{{ aboutSettings?.description || "About Meeee" }}</p>
        </div>
      </div>

      <!-- Background Layer -->
<!--       <div class="absolute bottom-0 left-0 w-full h-[100vh] bg-[#F7DCE4]" style="z-index: -1;"></div> -->
    </div>

    <!-- Load pages -->
	<WorksTable />
  </div>
</template>
<script setup>
import { ref, onMounted } from "vue";


// State variables
const aboutSettings = ref(null);
const isLoading = ref(true);
const hasError = ref(false);

// Fetch JSON data on mount
onMounted(async () => {
  try {
    const response = await fetch("/_data/about.json");

    if (!response.ok) {
      throw new Error("Failed to fetch about settings");
    }

    aboutSettings.value = await response.json();
    isLoading.value = false;
  } catch (error) {
    hasError.value = true;
    console.error("Error loading about settings:", error);
  }
});
</script>
