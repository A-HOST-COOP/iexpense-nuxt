<template>
  <v-app dark>
    <v-navigation-drawer
      v-model="drawer"
      :mini-variant="miniVariant"
      :clipped="clipped"
      fixed
      app
    >
      <v-list router exact color="primary" dark>
          <v-list-item>
            <v-list-item-action @click.stop="miniVariant = !miniVariant">
              <v-icon>mdi-{{ `chevron-${miniVariant ? 'right' : 'left'}` }}</v-icon>
            </v-list-item-action>
            <v-list-item-title>
                <h1 class="font-weight-thin">A-HOST</h1>
            </v-list-item-title>
          </v-list-item>
      </v-list>
      <v-list>
        <v-list-item
          v-for="(item, i) in items"
          :key="i"
          :to="item.to"
          router
          exact
        >
          <v-list-item-action>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title v-text="item.title" />
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-app-bar
      :clipped-left="clipped"
      fixed
      app
    >
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
      <v-spacer></v-spacer>
      <v-icon>mdi-account</v-icon>
    </v-app-bar>
    <v-main>
      <v-container>
        <Nuxt />
      </v-container>
    </v-main>
    <v-footer
      :absolute="!fixed"
      app
    >
      <span>&copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
  </v-app>
</template>

<script lang="ts">
import { defineComponent, reactive, toRefs } from '@vue/composition-api'
export default defineComponent({
    setup(){
      const state = reactive({
        clipped: false,
        drawer: false,
        fixed: false,
        items: [
          {
            icon: 'mdi-apps',
            title: 'Dashboard',
            to: '/'
          },
          {
            icon: 'mdi-chart-bubble',
            title: 'Expense',
            to: '/expense'
          }
        ],
        miniVariant: false
      })

      return { ...toRefs(state) }
    }
})
</script>
