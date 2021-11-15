<template lang="pug">
    span {{differenceValue}}
</template>
<script>
export default {
  props: {
    agoTime: {
      type: String,
      default: new Date().toString()
    }
  },
  computed: {
    differenceValue () {
      const difference = new Date() - new Date(this.agoTime)
      const minut = 60000
      return difference < minut * 15 ? 'ממש לאחרונה' : difference < minut * 60 ? 'בשעה האחרונה' : difference < minut * 60 * 24 ? `לפני ${Math.floor((difference / (1000 * 60 * 60)) % 24)} שעות` : `לפני ${Math.floor((difference / (1000 * 60 * 60)) / 24)} ימים`
    }
  }
}
</script>
