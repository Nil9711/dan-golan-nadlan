<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated class="main-header" @click="reload()">
      <div class="cursor-pointer flex flex-center column">
        <img src="../assets/logo-dan.png" />
        <h3>דן גולן</h3>
      </div>
    </q-header>

    <q-page-container>
      <router-view />
    </q-page-container>
    <q-footer reveal elevated>
      <q-toolbar>
        <q-toolbar-title class="text-center">כל הזכויות שמורות לדן גולן,
          <a href="https://docs.google.com/document/d/e/2PACX-1vSh4yHqFxDVUgupFa-qa7nYVBws-WVgC5jijqJfE2z4K8L5CZjKqKqvQ4_AZG-inRavUnxc7ZVovuwt/pub"
            class="text-white">לתקנון האתר</a>
        </q-toolbar-title>
      </q-toolbar>
    </q-footer>
  </q-layout>
</template>

<script>
import { defineComponent, ref } from "vue";

export default defineComponent({
  name: "MainLayout",

  components: {},

  setup() {
    const leftDrawerOpen = ref(false);

    return {
      leftDrawerOpen,
      toggleLeftDrawer() {
        leftDrawerOpen.value = !leftDrawerOpen.value;
      },
      reload: ref(() => {
        window.location.href = "/#/";
        window.location.reload();
      }),
    };
  },
});
</script>
