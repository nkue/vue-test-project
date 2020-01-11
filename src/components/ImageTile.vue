<template>
  <div class="tile">
    <a :href="image.url" target="_blank" v-on:click="handleClick">
      <img :src="image.src" :alt="`An image by ${image.author}`" />
    </a>
    <div class="info">
      <span class="author">{{ image.author }}</span>
      <span>#{{ image.id }}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: "ImageTile",
  props: {
    image: {},
    selectImage: Function
  },
  methods: {
    handleClick: function(event) {
      event.preventDefault();
      this.selectImage(this.image);
    }
  }
};
</script>

<style scoped lang="scss">
$tile-color: white;

.tile {
  border: 1px solid black;
  background-color: $tile-color;
}

img {
  width: 100%;
}

.info {
  display: grid;
  grid-template-columns: auto min-content;
  margin: 5px;
}

.author {
  text-overflow: ellipsis;
  white-space: nowrap;
  overflow: hidden;
}
</style>
