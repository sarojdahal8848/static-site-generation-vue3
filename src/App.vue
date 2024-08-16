<script setup>
import { onMounted, ref } from 'vue';
import { useHead, useSeoMeta } from '@unhead/vue'

const product = ref({})

onMounted(async () => {
  const res = await fetchData();
  product.value = res;
})

async function fetchData() {
  const res = await fetch('https://dummyjson.com/products/1')
  return res.json()
}


const metaUrl = () => `https://example.com/products/${product.value.id}`

useHead({
      title: () => product.value.title,
      meta: [
        {
          name: 'description',
          content: () => product.value.description,
        },
      ],
    })
    useSeoMeta({
      ogImage: () => product.value.thumbnail,
      ogUrl: () => metaUrl,
      ogTitle: () => product.value.title,
      ogDescription: () => product.value.description,
    })

</script>

<template>
  <div>
    <img :src="product.thumbnail" alt="">
    <p>{{ product.title }}</p>
  </div>
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
