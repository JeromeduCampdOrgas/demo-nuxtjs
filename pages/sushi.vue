<template>
  <div>
    <h1>Hello here are my Sushis</h1>
    <div v-for="sushi of sushis" :key="sushi.id">
      <nuxtLink :to="'/sushis/' + sushi.id">
        <img :src="sushi.image" alt="" />
        <h2>{{ sushi.title }}</h2></nuxtLink
      >
    </div>
  </div>
</template>
<script>
export default {
  head: {
    title: 'Mes Sushis trop cool',
    meta: [
      { charset: 'utf-8' },
      { name: 'viewport', content: 'width=device-width, initial-scale=1' },
      {
        hid: 'description',
        name: 'description',
        content: 'my website description',
      },
    ],
    link: [{ rel: 'icon', type: 'image/x-icon', href: '/favicon.ico' }],
  },
  data() {
    return {
      sushis: [],
    }
  },
  async fetch() {
    this.sushis = await fetch(
      'https://www.wawasensei.dev/api/demo-nuxt/getSushis'
    )
      .then((res) => {
        return res.json()
      })
      .then((response) => response.Table)
  },
}
</script>
