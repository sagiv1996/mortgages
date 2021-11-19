<template lang="pug">
  v-row(justify="center" )
    v-col( cols="12")
      v-parallax( src="index.jpeg" height="700" )
      lazy-article( url='articles')
    v-col( cols="12")
      v-expansion-panels( focusable popout )
        v-expansion-panel( v-for="(question, i) in questions" :key="i")
          v-expansion-panel-header {{question.question}}
          v-expansion-panel-content {{question.answer}}
</template>
<script>
export default {
  async asyncData ({ $content }) {
    const questions = await $content('').only(['answer', 'question']).fetch()
    return { questions }
  },
  head () {
    return {
      title: 'דף הבית'
    }
  }
}
</script>
