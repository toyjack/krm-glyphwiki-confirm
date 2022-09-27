<script setup lang="ts">
const route =  useRoute()
</script>

<template>
  <div class="h-screen flex flex-col">

    <header class="bg-gradient-to-r from-green-500 to-teal-300 flex flex-col justify-between">
      <div class="flex flex-row justify-between px-2 pt-7 pb-2 md:p-20 ">
        <div class="flex flex-col">
          <h6 class="text-sm md:text-xl text-white">krm glyphwiki confirm</h6>
          <h3 class="text-left text-xl md:text-3xl font-serif text-white  uppercase">
            <NuxtLink to="/" class="hover:underline">KRM作字プラットフォーム字形確認</NuxtLink>
          </h3>
        </div>
      </div>

      <div class="tabs md:px-20">
        <NuxtLink class="tab tab-lifted" to="/" activeClass="tab-active">Home</NuxtLink>
        <NuxtLink class="tab tab-lifted" to="/radicals" activeClass="tab-active">Radical List</NuxtLink>
      </div>

    </header>



    <main class="flex-grow">
      <slot />
    </main>

    <footer class="bg-gradient-to-r from-green-500 to-teal-300 text-white flex flex-col items-center justify-center">
      <div class="text-sm md:text-base p-2 md:p-4">Copyright 2022 <a href="https://researchmap.jp/liuguanwei"
          target="blank" class="underline">Guanwei Liu</a></div>
    </footer>
  </div>
</template>