<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>
        <q-btn
                flat
                dense
                round
                @click="leftDrawerOpen = !leftDrawerOpen"
                aria-label="Menu"
                icon="menu"
        />

        <q-toolbar-title>
         Labs for JS
        </q-toolbar-title>
      </q-toolbar>
    </q-header>

    <q-drawer
            v-model="leftDrawerOpen"
            show-if-above
            bordered
            content-class="bg-grey-2"
    >
      <q-list>
        <q-item-label header>Menu</q-item-label>
        <q-item clickable tag="a" rel="noopener" :to="{'path':'battleship'}">
          <q-item-section avatar>
            <q-icon name="directions_boat" />
          </q-item-section>
          <q-item-section>
            <q-item-label>Морской бой</q-item-label>
            <q-item-label caption>Lab 1</q-item-label>
          </q-item-section>
        </q-item>
        <q-item clickable tag="a" rel="noopener" :to="{'path':'conditions'}">
          <q-item-section avatar>
            <q-icon name="call_merge" />
          </q-item-section>
          <q-item-section>
            <q-item-label>Условия</q-item-label>
            <q-item-label caption>Lab 2</q-item-label>
          </q-item-section>
        </q-item>
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
  export default {
    name: 'MyLayout',
    data () {
      return {
        leftDrawerOpen: false
      }
    }
  }
</script>
