<template>
  <div class="qa-box">
    <div class="flex justify-between">
      <a>{{ title }}</a>
      <span>{{ isOpen ? "-" : "+" }}</span>
    </div>
    <p v-if="isOpen">{{ text }}</p>
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
  background-color: rgba($color: grey, $alpha: 0.3);
  border-radius: 30px;
  width: 80%;
  cursor: pointer;
  a,
  span {
    padding: 5px;
    margin: 0px 10px;
    font-size: 25px;
    font-weight: bolder;
  }
  p {
    text-align: start;
    padding: 16px;
  }
}
</style>
