<template>
  <div>
    <q-form @submit="onSubmit">
      <h6 class="text-center">
        מחשבון משכנתא <br />
        לפי קריטריונים אישיים
      </h6>
      <div class="flex flex-center">
        <div class="col-6 q-mx-md">
          <q-input
            v-model="price"
            label="מחיר הנכס"
            :rules="[
              (val) => !!val || 'שדה חובה',
              (val) => val > 499999 || 'המחיר המינימלי הינו 500,000',
            ]"
          >
            <template v-slot:prepend>
              <q-icon name="paid" />
            </template>
          </q-input>
        </div>
        <div class="col-6 q-mx-md input-area">
          <q-select
            v-model="area"
            :options="options"
            label="מיקום הנכס"
            :rules="[(val) => !!val || 'שדה חובה']"
          >
            <template v-slot:no-option>
              <q-item>
                <q-item-section class="text-grey"> נא לבחור </q-item-section>
              </q-item>
            </template>
            <template v-slot:prepend>
              <q-icon name="place" />
            </template>
          </q-select>
        </div>
      </div>
      <div class="q-my-lg flex flex-center">
        <q-btn
          color="primary"
          icon-right="arrow_circle_left"
          label="חישוב"
          type="submit"
        />
      </div>
    </q-form>
  </div>
</template>

<script>
import { ref } from "vue";
export default {
  name: "FlowStep1",
  emits: ["nextStep"],
  setup(props, ctx) {
    const price = ref();
    const area = ref();
    const onSubmit = () => {
      localStorage.setItem("clientInfo", JSON.stringify({"assetPrice": price.value, "area": area.value}))
      ctx.emit("nextStep");
    };
    return {
      area,
      price,
      options: ref([
        "הגליל והגולן",
        "אריאל והשומרון",
        "חיפה והקריות",
        "ירושלים והסביבה",
        " באר שבע והסביבה",
        "אשקלון אשדוד והסביבה",
        "המרכז והשרון",
        "הערבה ואילת",
      ]),
      onSubmit,
    };
  },
};
</script>
<style scoped lang="scss">
.input-area {
  width: 215px;
  span {
    font-size: 13px;
  }
}

@media (max-width: 480px) {
  /* smartphones, Android phones, landscape iPhone */
}
</style>
