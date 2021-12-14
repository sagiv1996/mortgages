<template lang="pug">
    v-row
        v-col( cols="12")
            v-card( )
                v-card-title.mb-7 מאמרים עם תגיות עבור {{$route.params.tag}}
            lazy-article( url='articles' :where="{ tags: { $contains: [$route.params.tag.replace('-', ' ')] } }")
</template>
<script>
export default {
  head () {
    return {
      title: 'תג - ' + this.$route.params.tag.replace('-', ' ')
    }
  }
}
</script>
