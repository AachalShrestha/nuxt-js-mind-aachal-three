<template>
  <div class="w-full bg-[#e4a8c4] mt-16 footer">
    <div class="p-16 flex justify-evenly flex-wrap gap-10">
      <div class="footer-item">
        <p>Thank you for reviewing my</p>
        <h1 class="text-3xl mt-2">Portfolio</h1>
      </div>

        <div class="footer-item">
          <h1 class="text-xl">Contact me</h1>
          <div class="flex space-x-4">
            <!-- Email Link -->
            <NuxtLink to="mailto:aachalshresth@gmail.com?subject=Hello%20Aachal&body=This%20is%20a%20test%20email!" class="p-8 mt-2 text-xs border border-black hover:border-white hover:text-white transition-all duration-100 rounded-full px-2 py-1">
              Email
            </NuxtLink>
            <!-- LinkedIn Link -->
            <NuxtLink to="https://www.linkedin.com/in/aachal-shrestha-002068234/" class="p-8  mt-2 text-xs border border-black hover:border-white hover:text-white transition-all duration-100 rounded-full px-2 py-1">
              LinkedIn
            </NuxtLink>
        </div>
    </div>
    </div>

  </div>
</template>

  
  <script setup>

  </script>
  
  <style>
  .footer-item{
    width: 250PX;
  }

  .dark-mode.footer-item{
    color: black;
  }

  .light-mode.footer{
    color: white;
  }

</style>