<template lang="pug">
    v-card()
        v-card-title {{article.title}}
            v-subheader {{agoTime}}
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
  },
  computed: {
    agoTime () {
      const difference = new Date() - new Date(this.article.createdAt)
      const minut = 60000
      return difference < minut * 15 ? 'ממש לאחרונה' : difference < minut * 60 ? 'בשעה האחרונה' : difference < minut * 60 * 24 ? `לפני ${Math.floor((difference / (1000 * 60 * 60)) % 24)} שעות` : `לפני ${Math.floor((difference / (1000 * 60 * 60)) / 24)} ימים`
    }
  }
}
</script>
