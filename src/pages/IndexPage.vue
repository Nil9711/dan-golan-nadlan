<template>
  <q-page class="flex column">
    <header v-if="step < 2" class="flex column flex-center q-my-lg">
      <h3>יועץ משכנתאות ופיננסים</h3>
      <h4>חבר בהתאחדות היועצים</h4>
    </header>
    <section class="flex flex-center row index-section-one q-my-lg">
      <div class="flex flex-center col-10 justify-evenly">
        <div class="col-2">
          <ProgressStepper :step="step" @clickStep="stepClicked" />
        </div>
        <div class="col-10 flex flex-center column">
          <div class="q-my-lg">
            <h6>מחשבון משכנתא לפי קריטריונים אישיים</h6>
          </div>
          <FlowStep1 v-if="step === 1" @nextStep="step = 2" />
          <FlowStep2 v-if="step === 2" @nextStep="step = 3" />
          <FlowStep3 v-if="step === 3" @nextStep="step = 4" />
          <FlowStep4 v-if="step === 4" @nextStep="step = 5" />
          <FlowStep5 v-if="step === 5" />
        </div>
      </div>
      <div class="col-2 flex flex-center" v-if="step < 2">
        <img src="../assets/target.jpg" class="left-side-img" />
      </div>
    </section>
    <section
      v-show="step < 2"
      class="flex justify-evenly full-width second-section section-margin"
    >
      <div>
        <h3>הדרך הנכונה לחישוב משכנתא</h3>
        <ul>
          <li>
            מחשבון זה יעזור לך לחשב נכון את ההחזר החודשי, לפריסת התשלומים ותקופת
            הזמן.
          </li>
          <li>
            בעזרת מחשבון זה, תקבלו תמהיל מומלץ ומותאם עבורכם, ניהול נכון לחישוב
            הריביות, טיפים לחסכון ועוד.
          </li>
          <li>כל שנדרש להירשם באתר בחינם.</li>
          <li>אנו נחשב עבורכם את התמהיל ללא עלות.</li>
        </ul>
      </div>
      <img src="../assets/contract-image.png" />
    </section>
    <section
      v-show="step < 2"
      class="flex flex-center full-width third-section"
    >
      <div class="card-box">
        <span>🧑‍💻</span>
        <p>
          הזנת נתוני המשכנתא כגון: מיקום הנכס, מחיר, גובה משכנתא, גובה ההכנסות
          ועוד
        </p>
      </div>
      <div class="card-box">
        <span>📊</span>
        <p>אנו נחשב לך החזר חודשי בהתאם לנתונים ובחישוב ניהול הסיכונים</p>
      </div>
      <div class="card-box">
        <span>📩</span>
        <p>
          אנו נשלח לך תמהיל אישי ע"פ הנתונים שנרשמו אצלנו, ובנוסף תקבל הדרכה
          וליווי אישי.
        </p>
      </div>
      <div class="card-box">
        <span>🗝️</span>
        <p>
          קבלת התמהיל הסופי הכולל: ריבית נכונה, החזר חודשי נוח, והכל בליווי אנשי
          מקצוע ולכל לקוחות הבנקים.
        </p>
      </div>
    </section>
    <section
      v-show="step < 2"
      class="flex flex-center full-width section-margin text-center fourth-section"
    >
      <h3 class="full-width">שאלות ותשובות - מחשבון משכנתאות</h3>
      <QuestionComponent
        title="מה הרכב המשתנים שמחשבון זה כולל ?"
        text="מחשבון זה כולל בתוכו את המרכיבים הקובעים את סוג המשכנתא, סכום ההחזר, מספר השנים, ריביות ממוצעות למסלול."
        :isOpen="questionActive === 1"
        @click="toggleOpenedQuestion(1)"
      />
      <QuestionComponent
        title="מה האינפורמציה שאקבל מהמחשבון ?"
        text='בסיום החישוב אדע, מה תקופת המשכנתא המומלצת, וההחזר החודשי, אחוז המימון והכל ע"פ הנחיות בנק ישראל. בסוף התהליך אקבל תמהיל אישי ע"פ הנתונים שסופקו.'
        :isOpen="questionActive === 2"
        @click="toggleOpenedQuestion(2)"
      />
      <QuestionComponent
        title="מדוע נדרש להשאיר פרטים אישיים?"
        text="ככל שהפרטים יהיו מדויקים ומלאים, כך תבנה לך תוכנית מותאמת על הצד הטוב ביותר כגון: העסקה, ריביות, אורך המשכנתא, וההחזר החודשי, אנו מדגשים שהפרטים האישיים ישמשו לצורך חישובי תמהיל בלבד."
        :isOpen="questionActive === 3"
        @click="toggleOpenedQuestion(3)"
      />
      <QuestionComponent
        title="שאלה"
        text="תשובה"
        :isOpen="questionActive === 4"
        @click="toggleOpenedQuestion(4)"
      />
    </section>
  </q-page>
</template>

<script>
import { defineComponent } from "vue";
import ProgressStepper from "../components/ProgressStepper.vue";
import QuestionComponent from "../components/QuestionComponent.vue";
import FlowStep1 from "../components/FlowStep1.vue";
import FlowStep2 from "../components/FlowStep2.vue";
import FlowStep3 from "../components/FlowStep3.vue";
import FlowStep4 from "../components/FlowStep4.vue";
import FlowStep5 from "src/components/FlowStep5.vue";

import { ref } from "vue";

export default defineComponent({
  name: "IndexPage",
  components: {
    ProgressStepper,
    QuestionComponent,
    FlowStep1,
    FlowStep2,
    FlowStep3,
    FlowStep4,
    FlowStep5,
  },
  setup() {
    const questionActive = ref(0);
    const assetPrice = ref(0);
    const step = ref(1);

    const nextStep = () => {
      step.value += 1;
    };

    const toggleOpenedQuestion = (index) => {
      if (questionActive.value === index) {
        questionActive.value = 0;
        return;
      }
      questionActive.value = index;
    };

    const stepClicked = (index) => {
      step.value = index;
    };

    return {
      step,
      questionActive,
      toggleOpenedQuestion,
      assetPrice,
      nextStep,
      stepClicked,
    };
  },
});
</script>
<style lang="scss" scoped>
h3,
h4,
h6 {
  margin: 10px auto;
}
.index-section-one {
  .left-side-img {
    width: 60%;
  }
}

.second-section {
  margin: 150px auto;
  h3 {
    margin: 0px 0px 32px 0px;
  }
  ul {
    li {
      margin: 5px 0px;
    }
  }
  img {
    height: 200px;
    width: 200px;
    padding: 5px;
    margin: 45px 0px;
  }
}

.section-margin {
  margin: 100px auto;
}

.third-section {
  font-size: 40px;
}

.card-box {
  width: 250px;
  display: flex;
  flex-direction: column;
  justify-items: center;
  align-items: center;
  margin: 16px;
  border-radius: 15%;
  box-shadow: 10px 10px 15px 10px rgb(0 0 0 / 10%);

  span {
    margin-top: 10px;
    border-radius: 50%;
  }
  p {
    margin: 10px auto;
    padding: 16px;
    font-size: 16px;
    text-align: center;
    height: 150px;
  }
}
.fourth-section {
  h3 {
    margin: 24px auto;
  }
}
</style>
