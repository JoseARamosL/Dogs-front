<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="toggleLeftDrawer"
        />

        <q-toolbar-title>
          <img class="logo" src="src/statics/images/europe_language_jobs_logo.jpeg" alt="logoEurope" height="50px" width="50px">
        </q-toolbar-title>

        <q-btn class="custom-button"
          flat
          dense
          round
          square
          aria-label="Jobs"
          label="Jobs"
        />

        <q-btn class="custom-button"
               flat
               dense
               round
               square
               aria-label="Candidates"
               label="Candidates"
        />

        <q-btn class="custom-button"
               flat
               dense
               round
               square
               aria-label="For Employers"
               label="For Employers"
        />

        <q-btn class="custom-button"
               flat
               dense
               round
               square
               aria-label="Career Advice"
               label="Career Advice"
        />

        <q-btn class="custom-button"
               flat
               dense
               round
               square
               aria-label="Log in/Sign Up"
               label="Log in/Sign Up"
        />

      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      bordered
    >
      <q-list>
        <q-item-label
          header
        >
          Links
        </q-item-label>

        <EssentialLink
          v-for="link in essentialLinks"
          :key="link.title"
          v-bind="link"
        />
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import { defineComponent, ref } from 'vue'
import EssentialLink from 'components/EssentialLink.vue'

const linksList = [
  {
    title: 'Maquetación',
    caption: 'Europe Languages',
    icon: 'html',
    link: 'model'
  }
]

export default defineComponent({
  name: 'MainLayout',

  components: {
    EssentialLink
  },

  setup () {
    const leftDrawerOpen = ref(false)

    return {
      essentialLinks: linksList,
      leftDrawerOpen,
      toggleLeftDrawer () {
        leftDrawerOpen.value = !leftDrawerOpen.value
      }
    }
  }
})
</script>

<style scoped>
.logo {
  margin-top: 5px;
}

.q-header {
  background-color: rgb(13, 56, 102);
}

.custom-button {
  border-radius: 3px;
  margin-right: 10px;
  text-transform: none;
}
</style>
