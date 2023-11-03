<script setup>
import navbar from '../components/Header.vue';
</script>
<template>
  <!-- <br /> -->
  <!-- <br /> -->
  <section>
    <navbar />
    <div class="container">
      <NuxtLink
        to="/IsiProduct"
        class="bg-white border border-slate-300 w-max flex items-center gap-1 py-2 px-5 rounded-full mb-7 cursor-pointer mt-8"
      >
        <i class="ri-arrow-left-s-line text-base font-medium"></i>
        <span class="text-base font-medium">Kembali</span>
      </NuxtLink>
      <FormsCategoryForm />
    </div>
  </section>
  <br />
  <br />
  <br />
</template>
