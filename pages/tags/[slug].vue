<!-- ./pages/tags/[slug].vue -->
<script setup>
// get current route
const {
  params: { slug },
} = useRoute();

const filter = slug;
// console.log({ filter });
// set meta for page
useHead({
  title: `All articles with ${slug}`,
  meta: [{ name: "description" }],
});
</script>

<template>
<div>
  <Drawer />
<div class="container mt-10 mb-20">
  <div>
    </div>
    <div class="text-xl mb-8 lg:text-3xl lg:mb-6 font-bold5"><p>Works with the tag "{{ slug }}"</p></div>
    <section class="page-section">
      <!-- Render list of all articles in ./content/blog using `path` -->
      <!-- Provide only defined fieldsin the `:query` prop -->
      <ContentList
        path="/"
        :query="{
          only: ['title', 'description', 'tags', '_path'],
          where: {
            tags: {
              $contains: filter,
            },
          },
          $sensitivity: 'base',
        }"
      >
        <!-- Default list slot -->
        <template v-slot="{ list }">
          <ul class="article-list">
            <li v-for="article in list" :key="article._path" class="article-item w-full">
              <NuxtLink :to="article._path">

                    <h1 class="text-2xl font-bold">{{ article.title }}</h1>
                    <p m-0>{{ article.description }}</p>
                    <ul class="article-tags">

                    </ul>
                    <hr>
              </NuxtLink>
            </li>
          </ul>
        </template>

        <!-- Not found slot to display message when no content us is found -->
        <template #not-found>
          <p>No articles found.</p>
        </template>
      </ContentList>
    </section>
</div>  
</div>
</template>

<style scoped>
li { 
list-style: none;
display: inline-block;
padding: 4px;
}
p{
  margin: 0;
}
</style>