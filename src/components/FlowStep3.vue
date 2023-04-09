<template>
  <div class="flow-step-3 flex flex-center column">
    <p class="step-3-header">
      מצויין , אנו נמצאים בסיכוי מירבי לאישור המשכנתא המבוקשת , בואו נעבור לשלב
      הפרטים האישיים לאישור ביטחונות הבנק . רגע קצר וסיימנו ...
    </p>
    <q-form @submit="onSubmit" class="flex column full-width">
      <div class="row justify-evenly">
        <q-input
          v-model="age"
          label="מה גילך?"
          :rules="[
            (val) => !!val || 'שדה חובה',
            (val) => val < 20 || val < 85 || 'לא תקין',
          ]"
        >
          <template v-slot:prepend>
            <q-icon name="person"/>
          </template>
        </q-input>
        <q-select
          v-model="status"
          :options="statusOptions"
          label="מצב משפחתי"
          :rules="[(val) => !!val || 'שדה חובה']"
        >
          <template v-slot:no-option>
            <q-item>
              <q-item-section class="text-grey"> נא לבחור</q-item-section>
            </q-item>
          </template>
          <template v-slot:prepend>
            <q-icon name="family_restroom"/>
          </template>
        </q-select>
      </div>
      <div class="row justify-evenly">
        <q-input
          v-model="totalIncome"
          label="הכנסה נטו למשק הבית"
          :rules="[(val) => !!val || 'שדה חובה']"
        >
          <template v-slot:prepend>
            <q-icon name="savings"/>
          </template>
        </q-input>
        <q-input
          v-model="extraIncome"
          label="הכנסות נוספות"
          hint="אם יש לך הכנסות נוספות הזן כאן את הסכום שלהן"
        >
          <template v-slot:prepend>
            <q-icon name="price_change"/>
          </template>
        </q-input>
      </div>
      <div class="row justify-evenly">
        <q-input
          v-model="extraLoans"
          label="האם יש הלוואות נוספות?"
          hint="אם יש לך הלוואות נוספות הזן כאן את הסכום שלהן"
        >
          <template v-slot:prepend>
            <q-icon name="production_quantity_limits"/>
          </template>
        </q-input>
        <q-input
          v-model="targetMonthlyPayment"
          label="ההחזר חודשי רצוי?"
          :rules="[(val) => !!val || 'שדה חובה']"
        >
          <template v-slot:prepend>
            <q-icon name="adjust"/>
          </template>
        </q-input>
      </div>
      <div class="row flex flex-center q-mt-md q-pb-md">
        <q-btn
          color="primary"
          icon-right="arrow_circle_left"
          label="המשך"
          type="submit"
          class="q-mb-lg"
        />
      </div>
    </q-form>
  </div>
</template>

<script>
import {ref} from "vue";

export default {
  name: "FlowStep3",
  emits: ["nextStep"],
  setup(props, ctx) {
    const statusOptions = ref([
      "בזוגיות",
      "בזוגיות עם ילדים",
      "רווק/ה",
      "גרוש/ה",
      "חד הורי",
    ])
    const age = ref();
    const extraIncome = ref();
    const extraLoans = ref();
    const status = ref();
    const totalIncome = ref();
    const targetMonthlyPayment = ref();
    const onSubmit = () => {
      let prevDetails = JSON.parse(localStorage.getItem("clientInfo"))
      localStorage.setItem("clientInfo", JSON.stringify({
        ...prevDetails,
        "age": age.value,
        "extraIncome": extraIncome.value,
        "extraLoans": extraLoans.value,
        "status": status.value,
        "totalIncome": totalIncome.value,
        "targetMonthlyPayment": targetMonthlyPayment.value
      }))
      ctx.emit("nextStep");
    };
    return {
      onSubmit,
      statusOptions,
      age,
      extraIncome,
      extraLoans,
      status,
      totalIncome,
      targetMonthlyPayment,
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
  width: 300px !important;
  margin: 10px;
}

@media (max-width: 480px) {
  /* smartphones, Android phones, landscape iPhone */
  .step-3-header {
    width: 305px !important;
    text-align: center;
  }
}
</style>
