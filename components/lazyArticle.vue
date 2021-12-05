<template lang="pug">
    v-row()
        v-col( v-for="(article, index) in articles" :key="index" cols="12" sm="11" md="6" lg="4")
            card-article( :article="article"  v-intersect.once="index === articles.length-1 ? onIntersect : false")
</template>

<script>
export default {
  data () {
    return {
      articles: []
    }
  },
  props: {
    url: {
      type: String,
      require: true
    },
    only: {
      type: Array,
      default: () => ['path', 'title', 'image', 'description', 'createdAt', 'slug']
    },
    deep: {
      type: Boolean,
      default: true
    },
    where: {
      type: Object,
      default: null
    }
  },
  computed: {
    skip () {
      return this.$vuetify.breakpoint.mobile ? 2 : 6
    }
  },
  // fetch data on page is loadied
  created () {
    this.fetchData()
  },
  methods: {
    // fetch data and add to artiles
    async fetchData () {
      const articles = await this.$content(this.url, { deep: this.deep }).only(this.only).limit(this.skip).sortBy('createdAt', 'desc').skip(this.articles.length).where(this.where).fetch()
      articles.forEach((article) => {
        this.articles.push(article)
      })
    },
    // load more data on scrolling
    onIntersect (entries, observer, isIntersecting) {
      if (isIntersecting) {
        this.fetchData()
      }
    }
  }
}
</script>
