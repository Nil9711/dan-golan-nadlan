<template>
  <div class="flex flex-center column flow-step-5">
    <h6 class="q-my-sm">פרטים אישיים</h6>
    <q-form @submit="onSubmit" class="flex column full-width flex-center">
      <div class="flex column">
        <q-input v-model="name" label="שם מלא" :rules="[(val) => !!val || 'שדה חובה']">
          <template v-slot:prepend>
            <q-icon name="badge" />
          </template>
        </q-input>
        <q-input v-model="phone" label="טלפון" :rules="[(val) => !!val || 'שדה חובה', isNumberValid]">
          <template v-slot:prepend>
            <q-icon name="phone_iphone" />
          </template>
        </q-input>
        <q-input v-model="email" label="מייל" :rules="[(val) => !!val || 'שדה חובה', isValidEmail]">
          <template v-slot:prepend>
            <q-icon name="email" />
          </template>
        </q-input>
      </div>
      <div class="row justify-evenly q-my-md">
        <q-checkbox class="checkbox" v-model="agreement" label="אני מאשר שקראתי ומסכים לתנאי השימוש והפרטיות , וכי הפרטים שמסרתי ישמשו לקבלת פניות, הצעות שיווקיות מאיתנו או מצדדים שלישיים." />
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
  setup (props, ctx) {
    const name = ref();
    const phone = ref();
    const email = ref();
    const onSubmit = () => {
      let prevDetails = JSON.parse(localStorage.getItem("clientInfo"))
      localStorage.setItem("clientInfo", JSON.stringify({
        ...prevDetails,
        "name": name.value,
        "phone": phone.value,
        "email": email.value,
      }))
      axios.post("https://dangolanserver-env.eba-jrciayxr.us-east-2.elasticbeanstalk.com/api/email/sendFormData",
        {
          "emailParams": JSON.parse(localStorage.getItem("clientInfo"))
        },
        {
          "Access-Control-Allow-Origin": "*",
          "Access-Control-Allow-Credentials": "true",
          "Content-Type": "application/json"
        })
      window.location.reload()
    };
    return {
      onSubmit,
      name: ref(),
      phone: ref(),
      email: ref(),
      agreement: ref(true),
      isValidEmail (val) {
        const emailPattern = /^(?=[a-zA-Z0-9@._%+-]{6,254}$)[a-zA-Z0-9._%+-]{1,64}@(?:[a-zA-Z0-9-]{1,63}\.){1,8}[a-zA-Z]{2,63}$/;
        return emailPattern.test(val) || 'אימייל לא תקין';
      },
      isNumberValid (val) {
        return !isNaN(val) || 'מספר טלפון לא תקין';
      }
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
