<template>
  <div class="flex flex-center column flow-step-5">
    <p class="step-3-header">
      מעולה, עד כאן נראה כי קיימת היתכנות גבוהה מצד הבנקים לעסקת המשכנתא
      המבוקשת. כעת אשאל אותך מספר שאלות אישיות ובנוגע לניהול הסיכונים של הבנקים.
      2 דקות וסיימנו, בואו נמשיך
    </p>
    <q-form @submit="onSubmit" class="flex column full-width">
      <div class="row justify-evenly">
        <q-input
          style="width: 330px"
          v-model="name"
          label="שם"
          :rules="[(val) => !!val || 'שדה חובה']"
        >
          <template v-slot:prepend>
            <q-icon name="badge" />
          </template>
        </q-input>
        <q-input
          style="width: 330px"
          v-model="phone"
          label="טלפון"
          :rules="[(val) => !!val || 'שדה חובה']"
        >
          <template v-slot:prepend>
            <q-icon name="phone_iphone" />
          </template>
        </q-input>
      </div>
      <div class="row justify-evenly q-my-md">
        <q-checkbox
          v-model="agreement"
          label="אני מאשר שקראתי ומסכים לתנאי השימוש והפרטיות , וכי הפרטים שמסרתי ישמשו לקבלת פניות, הצעות שיווקיות מאיתנו או מצדדים שלישיים."
        />
      </div>
      <div class="row flex flex-center">
        <q-btn
          color="primary"
          icon-right="arrow_circle_left"
          label="סיום"
          type="submit"
        />
      </div>
    </q-form>
  </div>
</template>

<script>
import { ref } from "vue";

export default {
  name: "FlowStep5",
  emits: ["nextStep"],
  setup(props, ctx) {
    const onSubmit = () => {
      ctx.emit("nextStep");
    };
    return {
      onSubmit,
      name: ref("ניל גולן"),
      phone: ref("0546437537"),
      agreement: ref(true),
    };
  },
};
</script>
<style scoped lang="scss">
.flow-step-5 {
  width: 500px;
}
</style>
