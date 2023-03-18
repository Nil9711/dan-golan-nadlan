<template>
  <div class="flow-step-3 flex flex-center column">
    <p class="step-3-header">
      מעולה, עד כאן נראה כי קיימת היתכנות גבוהה מצד הבנקים לעסקת המשכנתא
      המבוקשת. כעת אשאל אותך מספר שאלות אישיות ובנוגע לניהול הסיכונים של הבנקים.
      2 דקות וסיימנו, בואו נמשיך
    </p>
    <q-form @submit="onSubmit" class="flex column full-width">
      <div class="row justify-evenly">
        <q-input
          style="width: 330px"
          v-model="age"
          label="מה גילך?"
          :rules="[
            (val) => !!val || 'שדה חובה',
            (val) => val < 20 || val < 85 || 'לא תקין',
          ]"
        >
          <template v-slot:prepend>
            <q-icon name="person" />
          </template>
        </q-input>
        <q-select
          v-model="status"
          style="width: 330px"
          :options="statusOptions"
          label="מצב משפחתי"
          :rules="[(val) => !!val || 'שדה חובה']"
        >
          <template v-slot:no-option>
            <q-item>
              <q-item-section class="text-grey"> נא לבחור </q-item-section>
            </q-item>
          </template>
          <template v-slot:prepend>
            <q-icon name="family_restroom" />
          </template>
        </q-select>
      </div>
      <div class="row justify-evenly">
        <q-input
          style="width: 330px"
          v-model="totalIncome"
          label="הכנסה נטו למשק הבית"
          :rules="[(val) => !!val || 'שדה חובה']"
        >
          <template v-slot:prepend>
            <q-icon name="savings" />
          </template>
        </q-input>
        <q-input
          v-model="extraIncome"
          label="הכנסות נוספות"
          :rules="[(val) => !!val || 'שדה חובה']"
          hint="אם יש לך הכנסות נוספות הזן כאן את הסכום שלהן"
        >
          <template v-slot:prepend>
            <q-icon name="price_change" />
          </template>
        </q-input>
      </div>
      <div class="row justify-evenly">
        <q-input
          style="width: 330px"
          v-model="extraLoans"
          label="האם יש הלוואות נוספות?"
          :rules="[(val) => !!val || 'שדה חובה']"
          hint="אם יש לך הלוואות נוספות הזן כאן את הסכום שלהן"
        >
          <template v-slot:prepend>
            <q-icon name="production_quantity_limits" />
          </template>
        </q-input>
        <q-input
          style="width: 330px"
          v-model="targetMonthlyPayment"
          label="ההחזר חודשי רצוי?"
          :rules="[(val) => !!val || 'שדה חובה']"
        >
          <template v-slot:prepend>
            <q-icon name="adjust" />
          </template>
        </q-input>
      </div>
      <div class="row flex flex-center q-mt-md">
        <q-btn
          color="primary"
          icon-right="arrow_circle_left"
          label="המשך"
          type="submit"
        />
      </div>
    </q-form>
  </div>
</template>

<script>
import { ref } from "vue";
export default {
  name: "FlowStep3",
  emits: ["nextStep", "prevStep"],
  setup(props, ctx) {
    const onSubmit = () => {
      ctx.emit("nextStep");
    };
    return {
      onSubmit,
      statusOptions: ref(["נשוי", "רווק"]),
      age: ref(30),
      extraIncome: ref(4000),
      extraLoans: ref(2000),
      status: ref('רווק'),
      totalIncome: ref(10000),
      targetMonthlyPayment: ref(4000) ,
    };
  },
};
</script>
<style scoped lang="scss">
.flow-step-3 {

  .step-3-header {
    width: 500px;
    text-align: center;
  }
  form {
    input {
      width: 200px;
    }
    select {
      width: 200px;
    }
  }
}

.q-field {
  width: 200px !important ;
  margin: 10px auto;
}
</style>
