<template>
    <div>
      <div class="pr-5">
        <Drawer />
      </div>
      WOMP WOMP WOMP
    </div>    
    </template>
    
    <script setup>
    const { data: posts } = await useAsyncData('posts', () => {
      return queryContent('/page')
      .sort({ promoted: 1 })
    
      .find()
    })
    </script>