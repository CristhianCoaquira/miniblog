<template>
  <div class="container">
    <AboutMe />
    <div class="content">
      <main>
        <ArticleCard
          v-for="article in articles"
          :key="article.slug"
          v-bind="article"
        />
      </main>
    </div>
  </div>
</template>

<script>
export default {
  name: 'IndexPage',
  data() {
    return {}
  },
  async asyncData({ isDev, $http }) {
    const url = isDev
      ? 'http://localhost:9999'
      : 'https://miniblog-dadas.netlify.app'
    const res = await $http.get(`${url}/.netlify/functions/articles`)
    let { articles } = await res.json()
    articles = articles.map((article) => {
      return {
        ...article.fields,
        author: article.fields['author-name'][0],
        date: new Date(article.fields.updated),
        cover: article.fields.cover[0]?.thumbnails.large.url,
      }
    })
    return {
      articles,
    }
  },
}
</script>

<style lang="scss">
.container {
  @apply m-auto;
}
.container .content {
  @apply flex flex-col justify-center items-center sm:p-2 md:p-4 lg:p-8 xl:p-16;
  main {
    @apply max-w-5xl grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6;
  }
}
</style>
