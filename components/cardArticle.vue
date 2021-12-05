<template lang="pug">
    v-card( hover)
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
    }
  }
}
</script>
