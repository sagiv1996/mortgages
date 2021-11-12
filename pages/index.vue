<template lang="pug">
  v-row
    v-col( cols="12")
      v-parallax( src="index.jpeg" height="700" )
    v-col( v-for="article in lastArticle" :key="article.slug")
      card-article( :article="article")
    v-col( cols="12")
      v-expansion-panels( focusable popout )
        v-expansion-panel( v-for="(question, i) in questions" :key="i")
          v-expansion-panel-header {{question.question}}
          v-expansion-panel-content {{question.answer}}
</template>
<script>
export default {
  async asyncData ({ $content }) {
    const lastArticle = await $content('/articles', { deep: true }).only(['path', 'title', 'image', 'description', 'createdAt', 'slug']).limit(10).sortBy('createdAt', 'desc').fetch()
    const questions = await $content('').only(['answer', 'question']).fetch()
    return { lastArticle, questions }
  }
}
</script>
