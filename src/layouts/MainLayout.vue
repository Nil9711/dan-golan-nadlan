<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated class="main-header" @click="reload()">
      <img src="../assets/logo-dan.png" />
      <h3>דן גולן</h3>
    </q-header>

    <q-page-container>
      <router-view />
    </q-page-container>
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
