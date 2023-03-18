<template>
  <q-stepper
    v-model="getStep"
    :vertical="true"
    color="primary"
    animated
    flat
  >
    <q-step
      :name="1"
      title="הנכס"
      icon="home"
      :done="getStep > 1"
      @click="ctx.emit('clickStep', 1)"
    >
    </q-step>
    <q-step
      :name="2"
      title="המשכנתא"
      icon="credit_score"
      :done="getStep > 2"
      @click="ctx.emit('clickStep', 2)"
    >
    </q-step>
    <q-step
      :name="3"
      title="הלווה"
      icon="account_circle"
      :done="getStep > 3"
      @click="ctx.emit('clickStep', 3)"
    >
    </q-step>
    <q-step
      :name="4"
      title="סיכון"
      icon="emergency"
      :done="getStep > 4"
      @click="ctx.emit('clickStep', 4)"
    >
    </q-step>
    <q-step
      :name="5"
      title="פרטים"
      icon="info"
      :done="getStep > 5"
      @click="ctx.emit('clickStep', 5)"
    >
    </q-step>
  </q-stepper>
</template>

<script>
import { ref } from "vue";
import { useQuasar } from "quasar";

export default {
  name: "ProgressStepper",
  emits: ["clickStep"],
  props: {
    step: {
      type: Number,
      required: true,
    },
  },
  computed: {
    getStep() {
      return this.step;
    },
  },
  setup(props, ctx) {
    const $q = useQuasar();
    return {
      isMobile: ref($q.platform.is.mobile),
      ctx,
    };
  },
};
</script>
<style lang="scss" scoped>
.q-stepper {
  background-color: ghostwhite;
  cursor: pointer;
}
</style>
