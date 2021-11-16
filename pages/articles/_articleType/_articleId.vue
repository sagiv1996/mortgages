<template lang="pug">
    v-sheet
        v-card( )
        v-row( align="center")
            v-col( cols="12" sm="6" md="8" )
                v-card-title.justify-center {{article.title}}
                ago-time.subtitle( :agoTime="article.createdAt")
                v-card-subtitle.text-center {{article.description}}
            v-col( cols="12" sm='6' md="4" )
                v-img(:alt="article.title" :src="require('assets/' + article.image)" width="500" contain )
                    template( v-slot:placeholder)
                        v-row.fill-height.ma-0( align="center" justify="center")
                            v-progress-circular( indeterminate color="grey lighten-5")
            v-col( cols="12")
                v-card-subtitle.text-center {{article.readingTime}}
                v-card-text.align-center.justify-center.text-center
                    nuxt-content(:document="article")
                v-card-actions
            v-col(cols="12" v-if="article.tags")
                v-chip-group( column )
                    v-chip( v-for="tag in article.tags" :key="tag") {{tag}}
</template>
<script>
export default {
  async asyncData ({ $content, params }) {
    const article = await $content(`/articles/${params.articleType}/${params.articleId}`).fetch()
    return { article }
  },
  head () {
    return {
      title: this.article.title,
      meta: [
        {
          hid: this.article.description,
          name: this.article.description,
          content: this.article.description
        }
      ]
    }
  }
}
</script>
