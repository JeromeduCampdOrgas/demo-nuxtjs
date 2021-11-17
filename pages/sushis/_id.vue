<template>
  <div>
    <h1>{{ sushi.title }}</h1>
    <p>{{ sushi.description }}</p>
    <img :src="sushi.image" alt="" />
  </div>
</template>
<script>
export default {
  watch: {
    '$route.query': '$fetch',
  },
  head() {
    return { title: this.sushi.title }
  },
  async asyncData({ params }) {
    console.log(params)
    let sushis = await fetch(
      `https://www.wawasensei.dev/api/demo-nuxt/getSushi?id=${params.id}`
    )
      .then((res) => {
        return res.json()
      })
      .then((response) => response.Table)
    if (sushis && sushis.length) {
      return {
        sushi: sushis[0],
      }
    } else {
      return {
        sushi: {
          title: "Je n'existe pas",
          description: 'Je suis une 404',
          image: '',
        },
      }
    }
  },
}
</script>
