<template>
  <div class="layout">
    <slot></slot>
  </div>
</template>

<script>
export default {
  name: "Layout"
};
</script>

<style scoped lang="scss">
$stage-background: grey;

.layout {
  display: grid;
  column-gap: 20px;
  row-gap: 40px;
  margin-bottom: 10px;
  padding: 10px 10px;
  background-color: $stage-background;

  @media (min-width: 560px) {
    grid-template-columns: repeat(2, 1fr);
  }

  @media (min-width: 720px) {
    grid-template-columns: repeat(3, 1fr);
  }

  @media (min-width: 920px) {
    grid-template-columns: repeat(4, 1fr);
  }

  @media (min-width: 1240px) {
    grid-template-columns: repeat(5, 1fr)
  }

  @media (min-width: 1600px) {
    grid-template-columns: repeat(6, 1fr)
  }
}
</style>
