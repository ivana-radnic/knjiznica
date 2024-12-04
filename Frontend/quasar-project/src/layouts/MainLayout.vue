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
          Knjižnica
        </q-toolbar-title>

        <div>Quasar v{{ $q.version }}</div>
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
          Essential Links
        </q-item-label>

        <EssentialLink
          v-for="link in linksList"
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

<script setup>
import { ref } from 'vue'
import EssentialLink from 'components/EssentialLink.vue'

defineOptions({
  name: 'MainLayout'
})

const linksList = [
  {
    title: 'Naslovnica',
    caption: 'Naslovna stranica',
    icon: 'home',
    link: '#'
  },
  {
    title: 'Popis knjiga',
    caption: 'Popis svih knjiga',
    icon: 'list',
    link: '#/PopisKnjiga'
  },
  {
    title: 'Trazi knjigu',
    caption: 'Pronađite svoju knjigu',
    icon: 'book',
    link: '#/TraziKnjigu'
  },
  {
    title: 'O Nama',
    caption: 'Naša povijest',
    icon: 'history',
    link: '#/ONama'
  },
  {
    title: 'Lokacija',
    caption: 'Pronađite nas',
    icon: 'map',
    link: '#/Lokacija'
  },
  {
    title: 'Login',
    caption: 'Prijava',
    icon: 'login',
    link: '#/Login'
  },
  {
    title: 'Registracija',
    caption: 'Postanite član!',
    icon: 'man',
    link: '#/Registracija'
  }
]

const leftDrawerOpen = ref(false)

function toggleLeftDrawer () {
  leftDrawerOpen.value = !leftDrawerOpen.value
}
</script>
