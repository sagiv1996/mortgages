<template lang="pug">
    v-card( hover v-intersect="listenScroll? onIntersect: false")
        v-card-title {{article.title}}
        v-card-subtitle
            ago-time( :agoTime="article.createdAt")
        v-card-text( v-if="article.description") {{article.description.slice(0, length)}}
        v-card-actions
            v-spacer
            v-btn( :to="article.path" nuxt text) להמשך קריאה
</template>
<script>
export default {
  props: {
    article: {
      type: Object,
      require: true
    },
    length: {
      type: Number,
      default: 500
    },
    listenScroll: {
      type: Boolean,
      default: false
    }
  },
  methods: {
    onIntersect (entries, observer, isIntersecting) {
      if (isIntersecting) {
        this.$emit('endPage')
      }
    }
  }
}
</script>
