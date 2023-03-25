<template>
  <div class="flow-step-2">
    <div class="row q-my-md flex flex-center">
      <h6>פרטי המשכנתא</h6>
    </div>
    <div class="row flex-center">
      <CardOption
        icon="night_shelter"
        title="רכישת נכס ראשון"
        @click="activateCard(1)"
        id="card-el-1"
        class="card-option"
      />
      <CardOption
        icon="cottage"
        title="רכישת נכס נוסף"
        @click="activateCard(2)"
        id="card-el-2"
        class="card-option"
      />
      <CardOption
        icon="contact_support"
        title="מטרה אחרת"
        @click="activateCard(3)"
        id="card-el-3"
        class="card-option"
      />
    </div>
    <div class="row flex-center">
      <CardOption
        icon="sell"
        title="איחוד הלוואות נוספות"
        @click="activateCard(4)"
        id="card-el-4"
        class="card-option"
      />
      <CardOption
        icon="recycling"
        title="מחזור משכנתא קיימת"
        @click="activateCard(5)"
        id="card-el-5"
        class="card-option"
      />
      <CardOption
        icon="rotate_90_degrees_ccw"
        title="משכנתא הפוכה"
        @click="activateCard(6)"
        id="card-el-6"
        class="card-option"
      />
    </div>
    <q-form class="flex flex-center q-mt-md column" @submit="onSubmit">
      <q-input
        v-model="mortgageHeight"
        label="ציין סכום"
        :rules="[(val) => !!val || 'שדה זה הוא שדה חובה']"
      >
        <template v-slot:prepend>
          <q-icon name="paid" />
        </template>
        <template v-slot:hint>{{ hintText }}</template>
      </q-input>
      <br />
      <q-btn
        color="primary"
        icon-right="arrow_circle_left"
        label="המשך"
        type="submit"
        class="q-mb-lg"
      />
    </q-form>
  </div>
</template>

<script>
import { ref } from "vue";
import CardOption from "./CardOption.vue";

export default {
  name: "FlowStep2",
  emits: ["nextStep"],
  props: {},
  setup(props, ctx) {
    const cardActive = ref(0);
    const hintText = ref("");
    const mortgageHeight = ref(1500000);
    const assetPrice = ref(localStorage.getItem("assetPrice"));

    const activateCard = (index) => {
      $(`#card-el-${cardActive.value}`).removeClass("active");
      cardActive.value = index;
      $(`#card-el-${index}`).addClass("active");
      hintText.value = `ניתן לבחור עד ${assetPrice.value * 0.75}`;
    };

    const onSubmit = () => {
      if (!activateCard) {
        alert("please select");
        return;
      } else {
        ctx.emit("nextStep");
      }
    };

    return {
      mortgageHeight,
      cardActive,
      activateCard,
      onSubmit,
      hintText,
    };
  },
  components: { CardOption },
};
</script>
<style scoped lang="scss">
.flow-step-2 {
  h6 {
    font-weight: normal;
    margin: 0px auto;
  }
  hr {
    width: 100%;
  }
  .my-card {
    margin: 5px 10px;
  }
  .active {
    background-color: rgba(214, 156, 255, 0.2) !important;
  }
  .card-option {
    width: 200px;
    text-align: center;
    cursor: pointer;
  }
}
</style>
