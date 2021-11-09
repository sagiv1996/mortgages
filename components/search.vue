<template lang="pug">
    v-card
        v-card-text
            v-text-field( prepend-inner-icon="mdi-briefcase-search-outline" label="חיפוש חופשי" autofocus clearable @click:clear="results = null" @input="search")
            v-list( v-show="results && results.length>0")
                v-list-item( v-for="result in results" :key="result.slug" three-line)
                    v-list-item-avatar
                        v-img( :src="require('assets/' + result.image)" )
                    v-list-item-content( three-line)
                        v-list-item-title {{result.title}}
                        v-list-item-subtitle {{result.description}}
                    v-list-item-action
                        v-btn( icon nuxt :to="result.path")
                            v-icon mdi-link
</template>
<script>
export default {
  data () {
    return {
      results: null
    }
  },
  methods: {
    async search (val) {
      if (val && val.length > 2) {
        this.results = await this.$content('', { deep: true }).only(['slug', 'title', 'description', 'image', 'path']).search(val).fetch()
      } else {
        this.results = null
      }
    }
  }
}
</script>
