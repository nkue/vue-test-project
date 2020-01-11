<template>
  <div class="header">
    <div class="headline">
      <h1>{{ msg }}</h1>
    </div>
    <div class="header_interactions">
      <Button :disabled="!showPreviousButton" :onClick="onPreviousClick">previous page</Button>
      <span>
        Current page: {{ page }}
      </span>
      <label>
        Images per Page:
        <input v-on:change="onChange" type="number" value="30" min="1" max="100"/>
        <button>Submit</button>
      </label>
      <Button :disabled="!showNextButton" :onClick="onNextClick">next page</Button>
    </div>
  </div>
</template>

<script>
import Button from "./Button.vue";

export default {
  name: "Header",
  components: {
    Button
  },
  props: {
    msg: String,
    onPreviousClick: Function,
    onNextClick: Function,
    onChange: Function,
    showPreviousButton: Boolean,
    showNextButton: Boolean,
    page: Number
  }
};
</script>

<style scoped lang="scss">
$page-background: rgb(166, 194, 221);

.header {
  display: flex;
  flex-direction: column;
  position: sticky;
  top: 0;
  text-align: center;
  background-color: $page-background;
  padding-bottom: 5px;
}

.headline {
  width: 100%;
}

.header_interactions {
  display: flex;
  justify-content: space-around;
}
</style>
