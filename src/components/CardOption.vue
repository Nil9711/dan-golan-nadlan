<template>
  <q-card class="card-option bg-secondary">
    <q-card-section class="flex flex-center column card-options-wrapper">
      <div class="text-h6"><q-icon :name="icon" /></div>
      <hr />
      <div>{{ title }}</div>
    </q-card-section>
  </q-card>
</template>

<script>
export default {
  name: "CardOption",
  props: {
    icon: {
      type: String,
      required: true,
    },
    title: {
      type: String,
      required: true,
    }
  },
  setup() {
    return {};
  },
};
</script>
<style scoped lang="scss">
.card-option {
  margin: 5px 10px;
  background-color: transparent !important;

  hr {
    width: 100%;
  }
}
</style>
