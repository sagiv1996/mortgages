<template lang="pug">
    v-card()
        v-card-title {{article.title}}
        v-card-subtitle
            ago-time( :agoTime="article.createdAt")
        v-card-text {{article.description.slice(0, length)}}
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
    }
  }
}
</script>
