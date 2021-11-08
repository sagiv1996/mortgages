<template lang="pug">
  v-app
    v-navigation-drawer(app right v-model="showNavigation" bottom)
      template(v-for="item in articles" )
        v-list-item(v-if="!item.items" eager :key="item.name" nuxt :to='`/${item.action}`')
          v-list-item-icon
            v-icon( v-text="item.icon")
          v-list-item-content
              v-list-item-title {{item.name}}
        v-list-group(v-else-if="item.items" eager :group="item.action" active-class="deep-orange lighten-1" :key="item.name")
          template(v-slot:activator)
            v-list-item-icon
              v-icon( v-text="item.icon")
            v-list-item-content
              v-list-item-title {{item.name}}
          v-list-item(v-for="child in item.items" :key="child.name" nuxt :to='`/${item.action}/${child.action}`')
            v-list-item-avatar( v-text="child.name[0]" color="#FF8A65" size="30"  )
            v-list-item-content( two-line)
              v-list-item-subtitle {{child.name}}
    v-app-bar(app clipped-left)
      v-app-bar-nav-icon( @click="showNavigation = !showNavigation")
      v-spacer
      v-dialog( transition="dialog-top-transition" max-width="600" :fullscreen="fullScreen")
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
          search
      v-spacer
      v-avatar logo be here
    v-main
      v-container()
        nuxt
        v-btn( fixed left bottom icon x-large fab)
          v-icon( color="success" x-large  ) mdi-whatsapp
    v-footer(app inset absolute )
      v-sheet this is the footer text
</template>

<script>
export default {
  data () {
    return {
      showNavigation: null,
      fullScreen: false,
      articles: [
        {
          name: 'דף הבית',
          icon: 'mdi-home',
          action: ''
        },
        {
          name: 'מחשבון משכנתא',
          icon: 'mdi-script-text-outline',
          action: 'calculator',
          items: [
            {
              name: 'מה זה מחשבון משכנתא',
              action: 'what-is-this'
            },
            {
              name: 'איך משתמשים במחשבון משכנתא',
              action: 'how-to-use'
            },
            {
              name: 'מה זה שפיצר וקרן שווה',
              action: 'spitzer'
            },
            {
              name: 'מה ההבדל בין תמהיל לריבית',
              action: 'mix-versus-interest'
            },
            {
              name: 'מה זה תמהיל ולמה זה חשוב',
              action: 'when-use-mix'
            }
          ]
        },
        {
          name: 'מחשבונים',
          icon: 'mdi-calculator-variant',
          action: 'articles',
          items: [
            {
              name: 'מחשבונים'
            },
            {
              name: 'סרטון הדרכה על מחשבונים'
            }
          ]
        }
      ]
    }
  }
}
</script>
