<template>
  <button :disabled="disabled" v-on:click="onClick">
      <slot></slot>
  </button>
</template>

<script>
export default {
    name: "Button",
    props: {
        disabled: Boolean,
        onClick: Function,
    }
}
</script>

<style scoped lang="scss">

</style>