<template>
  <ClientOnly>
    <div class="container">
      <div v-if="post.folder !== 'page'">
        <FolderContent v-if="post.folder" :title="post.title" />
      </div>

      <!-- Carousel -->
      <div v-if="post.imagegallery.carouselgrid == 'carousel'">
        <p v-if="post.imagegallery.gallerytitle" class="text-xl font-bold pb-2">
          {{ post.imagegallery.gallerytitle }}
        </p>
        <p v-if="post.imagegallery.gallerytext" class="pb-2">{{ post.imagegallery.gallerytext }}</p>

        <el-carousel indicator-position="none" motion-blur>
          <el-carousel-item v-for="(item, index) in post.imagegallery.galleryImages" :key="index">
            <div class="relative h-full flex items-center justify-center">
              <!-- Show loader until the image is fully loaded -->
              <div v-if="imageLoading[index]" class="absolute inset-0 flex items-center justify-center bg-gray-200">
                <p>Loading image...</p>
              </div>
              <NuxtImg
                :src="item"
                alt="Gallery Image"
                loading="lazy"
                @load="imageLoaded(index)"
                @click="openFullscreen(item)"
                class="w-full h-auto max-h-full object-contain"
              />
            </div>
          </el-carousel-item>
        </el-carousel>
      </div>

      <!-- Grid -->
      <div v-if="post.imagegallery.carouselgrid == 'grid'">
        <p v-if="post.imagegallery.gallerytitle" class="text-xl font-bold pb-2">
          {{ post.imagegallery.gallerytitle }}
        </p>
        <p v-if="post.imagegallery.gallerytext" class="pb-2">{{ post.imagegallery.gallerytext }}</p>

        <!-- Masonry -->
        <div class="masonry">
          <div class="masonry-item" v-for="(item, index) in post.imagegallery.galleryImages" :key="index">
            <div class="relative masonry-image">
              <!-- Show loader until the image is fully loaded -->
              <div v-if="imageLoading[index]" class="absolute inset-0 flex items-center justify-center bg-gray-200">
                <p>Loading image...</p>
              </div>
              <NuxtImg
                :src="item"
                alt="Gallery Image"
                loading="lazy"
                @click="openFullscreen(item)"
                @load="imageLoaded(index)"
                class="cursor-pointer w-full object-cover no-hover-effect"
              />
            </div>
          </div>
        </div>

        <!-- Fullscreen Overlay -->
        <div v-if="isOverlayVisible" class="fullscreen-overlay" @click="closeFullscreen">
          <NuxtImg :src="currentImage" alt="Fullscreen Image" class="fullscreen-image" />
          <button @click="closeFullscreen" class="close-button">
            <svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24">
              <path fill="currentColor" d="m6.4 18.308l-.708-.708l5.6-5.6l-5.6-5.6l.708-.708l5.6 5.6l5.6-5.6l.708.708l-5.6 5.6l5.6 5.6l-.708.708l-5.6-5.6z"></path>
            </svg>
          </button>
        </div>
      </div>
    </div>
  </ClientOnly>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { useRoute, useAsyncData } from '#app';

const imageLoading = ref([]);
const route = useRoute();
const actualPath = route.path.replace(/\/$/, '');
const { data: post } = await useAsyncData('post', () => queryContent(actualPath).findOne());

const isOverlayVisible = ref(false);
const currentImage = ref('');

const openFullscreen = (image) => {
  currentImage.value = image;
  isOverlayVisible.value = true;
};

const closeFullscreen = () => {
  isOverlayVisible.value = false;
  currentImage.value = '';
};

const imageLoaded = (index) => {
  imageLoading.value[index] = false;
};

onMounted(() => {
  if (post.value && post.value.imagegallery && post.value.imagegallery.galleryImages) {
    imageLoading.value = post.value.imagegallery.galleryImages.map(() => true);
  }
});
</script>
