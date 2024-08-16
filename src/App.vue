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



const metaData = ref({
      title: 'NRN Legal by MeroAdda®',
      description: `NRN Legal is a prominent legal service of
      MeroAdda® catering to the needs of Nepali citizens living
      abroad. It aims to support and provide legal assistance to
      Nepali expatriates around the world. NRN Legal plays an
      important role in safeguarding the rights and interests
      of Nepali nationals residing outside their home country.
      NRN Legal, provided by MeroAdda®, an online service provider,
      collaborates with legal professionals and experts to ensure
      that Nepali expatriates receive comprehensive legal solutions.`,
      url: `https://www.google.com`,
    })

useHead({
      title: metaData.value.title,
      meta: [
        {
          name: 'description',
          content: () => metaData.value.description,
        },
      ],
    })
    useSeoMeta({
      ogImage: () => "https://cdn.dummyjson.com/products/images/beauty/Essence%20Mascara%20Lash%20Princess/thumbnail.png",
      ogUrl: () => metaData.value.url,
      ogTitle: () => metaData.value.title,
      ogDescription: () => metaData.value.description,
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
