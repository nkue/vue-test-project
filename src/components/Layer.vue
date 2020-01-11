<template>
  <div class="shim" v-on:click="handleClick">
    <div class="layer">
      <button v-on:click="handleClick">✗</button>
      <img :src="url" />
    </div>
  </div>
</template>

<script>
export default {
  name: "Layer",
  props: {
    url: String,
    handleClose: Function
  },
  methods: {
    handleClick: function (event) {
      event.preventDefault();
      this.handleClose()
    } 
  }
};
</script>

<style scoped lang="scss">
.shim {
  position: fixed;
  width: 100vw;
  height: 100vh;
  top: 0;
  left: 0;
  right: 0;
  overflow: scroll;
  background-color: rgba(0, 0, 0, 0.5);
}

.layer {
  max-width: 90vw;
  margin: 5vh auto 0 auto;

  & button {
    position: absolute;
  }
}

img {
  width: 100%;
}
</style>