<template>
    <div class="layout1">
    <MouseGradient />
    <ClientOnly>
      <div class="pr-5 z-100">
        <Drawer />
      </div>
      <div class="mb-10 container back-button">
      <NuxtLink :to="`/`">
        <span>
          <svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24">
            <path fill="currentColor" d="m6.921 12.5l5.793 5.792L12 19l-7-7l7-7l.714.708L6.92 11.5H19v1z"></path>
          </svg>
        </span>  
        <span class="text-xs">Back</span>
      </NuxtLink>
    </div>
      <div class="container">
        <h1 class="text-xl mb-4 md:text-3xl lg:text-6xl lg:mb-6 font-bold ">{{ data.title }}</h1>
        <p v-if="data.description" class="text-lg md:text-2xl lg:text-xl pb-10 font-bold">
  {{ data.description }}
</p>
      <article v-if="data.tags" class="tags">
        <ul class="flex gap-x-2.5">
          <li
            v-for="(item, index) in data.tags"
            :key="index"
          >
            <NuxtLink :to="`/tags/${item}`" class="p-8 text-xs border border-black hover:border-red-800 transition-all duration-100 rounded-full px-2 py-1">
              {{ item }}
            </NuxtLink>
          </li>
        </ul>
      </article>


        <ContentRenderer :value="data" class="mt-6 md:mt-4" />

        <div v-if="data.imagegallery && data.imagegallery.showgallery == true" class="pt-10 pb-20">
            <ImageGallery />
        </div>

        <div class="text-xs leading-3 container">
          <hr>
          <p class="text-xs opacity-50 hover:opacity-100 pb-5">Last update: {{ formatDate(data.date) }}</p>
        </div>
      </div>
      <ShareButtons />
    
      <!-- SEO metadata -->
      <!-- Regular Meta Tags -->
      <Title>{{ data.title }}</Title>
      <Meta name="description" :content="data.description" />
      <Meta name="tags" :content="data.tags" />
      <Meta name="keywords" :content="data.tags.join(', ')" /> <!-- Add keywords here -->
      <!-- Open Graph Meta Tags -->
      <Meta property="og:title" :content="data.title" />
      <Meta property="og:description" :content="data.description" />
      <Meta property="og:image" :content="data.thumbnail" /> <!-- Add an image URL here -->
      <Meta property="og:url" :content="data.url" /> <!-- Add the current URL -->
      <Meta property="og:type" content="article" /> 
    
    </ClientOnly>
    </div>
  </template>
  
  <script setup>
  defineProps(['data', 'formatDate']);
  </script>
  