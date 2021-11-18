<template lang="pug">
    v-row
        v-col( cols="12")
            v-card( )
                v-card-title מאמרים עם תגיות עבור {{$route.params.tag}}
        v-col( v-for="article in lastArticle" :key="article.slug" cols="12" sm="11" md="6" lg="4")
            card-article( :article="article")
</template>
<script>
export default {
  async asyncData ({ $content, params }) {
    const lastArticle = await $content('/articles', { deep: true }).only(['path', 'title', 'image', 'description', 'createdAt', 'slug']).where({ tags: { $contains: [params.tag.replace('-', ' ')] } }).sortBy('createdAt', 'desc').fetch()
    return { lastArticle }
  },
  head () {
    return {
      title: 'תג - ' + this.$route.params.tag.replace('-', ' ')
    }
  }
}
</script>
