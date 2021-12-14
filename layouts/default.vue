<template lang="pug">
  v-app
    v-navigation-drawer(app right v-model="showNavigation" bottom)
      template(v-for="item in articles" )
        div( :key="item.name")
        v-list-item(v-if="!item.childs" eager :key="item.name" nuxt :to='`${item.action}`')
          v-list-item-icon
            v-icon( v-text="item.icon")
          v-list-item-content
              v-list-item-title {{item.name}}
        v-list-group(v-else-if="item.childs && item.childs.length> 0" eager :group="item.dir" active-class="deep-orange lighten-1" :key="item.name")
          template(v-slot:activator)
            v-list-item-icon
              v-icon( v-text="item.icon")
            v-list-item-content
              v-list-item-title {{item.name}}
          v-list-item( v-for="child in item.childs" :key="child.name" nuxt :to='`${child.path}/`')
            v-list-item-avatar( v-text="child.title[0]" color="#FF8A65" size="30"  )
            v-list-item-content( two-line)
              v-list-item-subtitle {{child.title}}
    v-app-bar(app elevate-on-scroll )
      v-app-bar-nav-icon( @click="showNavigation = !showNavigation")
      v-spacer
      v-dialog( transition="dialog-top-transition" max-width="600" :fullscreen="fullScreen" )
        template( v-slot:activator="{ on, attrs }")
          v-text-field( readonly prepend-inner-icon="mdi-briefcase-search-outline" label="חיפוש חופשי" solo class="mt-7" v-on="on" v-bind="attrs" type="search"  )
        template( v-slot:default="dialog")
          v-toolbar( color="success")
            v-toolbar-title חיפוש חופשי
            v-spacer
            v-btn-toggle
              v-btn(@click="fullScreen = !fullScreen" icon)
                v-icon(v-text="fullScreen? 'mdi-fullscreen-exit' :'mdi-fullscreen'")
              v-btn(@click="dialog.value = false" icon)
                v-icon mdi-close
          search( @navigator="dialog.value = false" )
      v-spacer
      v-avatar
        v-img(:src="$icon(512)" alt="לוגו צב משכנתאות")
    v-main
      v-container( )
        nuxt
        v-btn( fixed left bottom icon x-large fab)
          v-icon( color="success" x-large  ) mdi-whatsapp
    v-footer(app inset absolute height="100"  )
        v-img( src="logo-text.png" width="100vw" contain max-height="100" eager  )
</template>

<script>
export default {
  async fetch () {
    const data = await this.$content('/articles', { deep: true }).only(['path', 'title', 'dir', 'slug', 'dirHebrew', 'dirIcon']).fetch()
    const result = data.reduce(function (r, a) {
      r[a.dir] = r[a.dir] || []
      r[a.dir].push(a)
      return r
    }, Object.create(null))
    Object.keys(result).forEach((key) => {
      if (result[key]) {
        this.articles.push({ name: result[key][0].dirHebrew, dir: result[key][0].dir, icon: result[key][0].dirIcon, childs: result[key] })
      }
    })
  },
  data () {
    return {
      showNavigation: null,
      fullScreen: false,
      articles: [
        {
          name: 'דף הבית',
          icon: 'mdi-home',
          action: '/'
        }
      ]
    }
  }
}
</script>
