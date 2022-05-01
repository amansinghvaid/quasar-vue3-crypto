<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated class="frosted-glass">
      <q-toolbar>
        <q-toolbar-title>
          Crypto App
        </q-toolbar-title>
      </q-toolbar>
    </q-header>


    <q-page-container>
      <transition
        mode="in-out"
        enter-active-class="animate__animated animate_slideInLeft"
        leave-active-class="animate__animated animate_slideOutRight"
      >
        <router-view />
      </transition>
    </q-page-container>

    <q-footer class="frosted-glass">
      <q-toolbar>
        <q-toolbar-title>
          <div class="flex flex-center">
            Crypto App - Expandable Technologies
          </div>
        </q-toolbar-title>
      </q-toolbar>
    </q-footer>
  </q-layout>
</template>

<script>
import { defineComponent } from 'vue'
import "animate.css"

export default defineComponent({
  name: 'MainLayout',

  components: {
  },

  setup () {
    return {
    }
  }
})
</script>
<style scoped>
  .frosted-glass {
    backdrop-filter: blur(7px);
    background-color: goldenrod;
    color: black;
  }
</style>
