<template>
  <div class="flow-step-4 flex flex-center column">
    <h6 class="q-my-sm">הערכת סיכון</h6>
    <q-form @submit="onSubmit" class="flex column full-width">
      <div class="row justify-evenly">
        <q-select
          v-model="overDraft"
          :options="booleans"
          label="חריגה ממסגרות אשראי ב3 שנים האחרונות?"
          :rules="[(val) => !!val || 'שדה חובה']"
        >
          <template v-slot:no-option>
            <q-item>
              <q-item-section class="text-grey"> נא לבחור </q-item-section>
            </q-item>
          </template>
        </q-select>
        <q-select
          v-model="loanReturnsDelay"
          :options="booleans"
          label="איחור בתשלומי הלוואות קיימות?"
          :rules="[(val) => !!val || 'שדה חובה']"
        >
          <template v-slot:no-option>
            <q-item>
              <q-item-section class="text-grey"> נא לבחור </q-item-section>
            </q-item>
          </template>
        </q-select>
      </div>
      <div class="row justify-evenly">
        <q-select
          v-model="returnedChecks"
          :options="booleans"
          label="המחאות חוזרות ב-3 השנים האחרונות?"
          :rules="[(val) => !!val || 'שדה חובה']"
        >
          <template v-slot:no-option>
            <q-item>
              <q-item-section class="text-grey"> נא לבחור </q-item-section>
            </q-item>
          </template>
        </q-select>
        <q-select
          v-model="files"
          :options="booleans"
          label="קיימים תיקים בהוצאה לפועל?"
          :rules="[(val) => !!val || 'שדה חובה']"
        >
          <template v-slot:no-option>
            <q-item>
              <q-item-section class="text-grey"> נא לבחור </q-item-section>
            </q-item>
          </template>
        </q-select>
      </div>
      <div class="row flex flex-center q-pb-md">
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
import { ref } from "vue";

export default {
  name: "FlowStep4",
  emits: ["nextStep"],
  setup(props, ctx) {
    const overDraft = ref();
    const loanReturnsDelay = ref();
    const returnedChecks = ref();
    const files = ref();
    const onSubmit = () => {
      let prevDetails = JSON.parse(localStorage.getItem("clientInfo"))
      localStorage.setItem("clientInfo", JSON.stringify({
        ...prevDetails,
        "overDraft": overDraft.value,
        "loanReturnsDelay": loanReturnsDelay.value,
        "returnedChecks": returnedChecks.value,
        "files": files.value
      }))
      ctx.emit("nextStep");
    };
    return {
      onSubmit,
      booleans: ref(["כן", "לא"]),
      overDraft,
      loanReturnsDelay,
      returnedChecks,
      files,
    };
  },
};
</script>
<style scoped lang="scss">
.flow-step-4 {
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
  .q-field {
    width: 300px !important ;
    margin: 10px;
  }
}
</style>
