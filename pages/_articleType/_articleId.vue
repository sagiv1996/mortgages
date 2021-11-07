<template lang="pug">
    v-sheet
        v-card( )
        v-row( align="center")
            v-col( cols="12" sm="6" md="8" )
                v-card-title( class="justify-center" ) {{article.title}}
                v-card-subtitle( class="text-center")  {{article.description}}
            v-col( cols="12" sm='6' md="4" )
                v-img(:alt="article.title" :src="require('assets/' + article.image)" width="500" contain )
                    template( v-slot:placeholder)
                        v-row( class="fill-height ma-0" align="center" justify="center")
                            v-progress-circular( indeterminate color="grey lighten-5")
            v-col( cols="12")
                v-card-text( class="align-center justify-center text-center" )
                    nuxt-content(:document="article")
</template>
<script>
export default {
  async asyncData ({ $content, params }) {
    const article = await $content(`/${params.articleType}/${params.articleId}`).fetch()
    return { article }
  }
}
</script>
