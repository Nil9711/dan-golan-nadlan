<template>
  <div class="flex flex-center column flow-step-5">
    <h6 class="q-my-sm">פרטים אישיים</h6>
    <q-form @submit="onSubmit" class="flex column full-width flex-center">
      <div class="flex column">
        <q-input v-model="name" label="שם" :rules="[(val) => !!val || 'שדה חובה']">
          <template v-slot:prepend>
            <q-icon name="badge" />
          </template>
        </q-input>
        <q-input v-model="phone" label="טלפון" :rules="[(val) => !!val || 'שדה חובה']">
          <template v-slot:prepend>
            <q-icon name="phone_iphone" />
          </template>
        </q-input>
        <q-input v-model="email" label="מייל" :rules="[(val) => !!val || 'שדה חובה']">
          <template v-slot:prepend>
            <q-icon name="email" />
          </template>
        </q-input>
      </div>
      <div class="row justify-evenly q-my-md">
        <q-checkbox class="checkbox" v-model="agreement"
          label="אני מאשר שקראתי ומסכים לתנאי השימוש והפרטיות , וכי הפרטים שמסרתי ישמשו לקבלת פניות, הצעות שיווקיות מאיתנו או מצדדים שלישיים." />
      </div>
      <div class="row flex flex-center">
        <q-btn color="primary" icon-right="arrow_circle_left" label="סיום" type="submit" class="q-mb-lg" />
      </div>
    </q-form>
  </div>
</template>

<script>
import { ref } from "vue";
import axios from 'axios'

export default {
  name: "FlowStep5",
  emits: ["nextStep"],
  setup(props, ctx) {
    const onSubmit = () => {
      ctx.emit("nextStep");
      axios.post("https://api.sendgrid.com/v3/mail/send",
        { "personalizations": [{ "to": [{ "email": "nil9711@gmail.com" }] }], "from": { "email": "test@example.com" }, "subject": "Sending with SendGrid is Fun", "content": [{ "type": "text/plain", "value": "and easy to do anywhere, even with cURL" }] }
        ,
        {
          "Authorization": `Bearer $${process.env.SG_KEY}`,
          "Content-Type": "application/json"
        })
    };
    return {
      onSubmit,
      name: ref("ניל גולן"),
      phone: ref("0546437537"),
      email: ref("nil9711@gmail.com"),
      agreement: ref(true),
    };
  },
};
</script>
<style scoped lang="scss">
.flow-step-5 {
  .q-field {
    width: 300px !important;
    margin: 10px;
  }

  .checkbox {
    width: 450px !important;
  }
}

@media (max-width: 480px) {

  /* smartphones, Android phones, landscape iPhone */
  .flow-step-5 {
    .checkbox {
      width: auto !important;
    }
  }
}
</style>
