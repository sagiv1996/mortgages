<template lang="pug">
    v-row
        v-col( v-for="article in lastArticle" :key="article.slug" cols="12" sm="11" md="6" lg="4")
            card-article( :article="article")
</template>
<script>
export default {
  async asyncData ({ $content, params }) {
    const article = await $content(`tag/${params.tag}`).only(['path', 'title', 'image', 'description', 'createdAt', 'slug']).limit(10).sortBy('createdAt', 'desc').fetch()
    return { article }
  }
}
</script>
