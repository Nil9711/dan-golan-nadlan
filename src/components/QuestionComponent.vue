<template>
  <div class="qa-box">
    <div class="flex flex-center row inline">
      <a>{{ title }}</a>
    </div>
    <div class="flex flex-center answer-div">
      <p v-if="isOpen">{{ text }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "QuestionComponent",
  props: {
    title: {
      type: String,
      required: true,
    },
    text: {
      type: String,
      required: true,
    },
    isOpen: {
      type: Boolean,
      required: true,
    },
  },
  setup() {
    return {};
  },
};
</script>
<style lang="scss" scoped>
.qa-box {
  margin: 20px auto;
  padding: 20px auto;
  background-color: lavender;
  border-radius: 30px;
  width: 55%;
  cursor: pointer;

  a,
  span {
    padding: 5px;
    margin: 0 10px;
    font-size: 20px;
    font-weight: bolder;
  }

  .answer-div {
    width: 100%;
    p {
      width: 75%;
      text-align: center;
      padding: 16px;
    }
  }
}

@media (max-width: 480px) {
  /* smartphones, Android phones, landscape iPhone */

  .qa-box {
    width: 80%;
    a {
      font-size: 14px;
      padding: 5px;
    }
  }
}
</style>
