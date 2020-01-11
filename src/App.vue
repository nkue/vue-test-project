<template>
  <div id="app">
    <Header
      msg="Your favourite images in one convenient place!"
      :onPreviousClick="onPreviousClick"
      :onNextClick="onNextClick"
      :showPreviousButton="page > 1"
      :showNextButton="nextImages.length > 0"
      :onChange="onChange"
      :page="page"
    />
    <Layout>
      <ImageTile
        v-for="image in images"
        v-bind:key="image.id"
        :image="image"
        :selectImage="selectImage"
      />
    </Layout>
    <Layer
      v-if="selectedImage.originalSrc"
      :url="selectedImage.originalSrc"
      :handleClose="deselectImage"
    />
  </div>
</template>

<script>
import axios from "axios";
import debounce from "lodash/debounce";
import Header from "./components/Header.vue";
import ImageTile from "./components/ImageTile.vue";
import Layout from "./components/Layout.vue";
import Layer from "./components/Layer.vue";

const getImages = async (page = 1, limit = 30) => {
  if (page <= 0) {
    return [];
  }

  const imageResponse = await axios.get(
    `https://picsum.photos/v2/list?page=${page}&limit=${limit}`
  );

  const data = imageResponse.data.map(image => {
    const { author, download_url, id, url } = image;
    const regexPattern = `.*id/${id}/`;
    const baseUrl = download_url.match(regexPattern);
    const aspectRatio = "367/267";
    const src = `${baseUrl}${aspectRatio}`;
    const originalSrc = download_url;

    return {
      src,
      originalSrc,
      url,
      author,
      id
    };
  });

  return data;
};

const preloadImages = images => {
  images.forEach(image => {
    let img = new Image();
    img.src = image.src;
  });
};

const loadImagesWithNewLimit = async function(event) {
  this.limit = event.target.value;
  this.images = await getImages(this.page, this.limit);
  this.nextImages = await getImages(this.page + 1, this.limit);
  this.previousImages = await getImages(this.page - 1, this.limit);
  preloadImages(this.nextImages);
};

export default {
  name: "app",
  components: {
    Header,
    ImageTile,
    Layout,
    Layer
  },
  data() {
    return {
      images: [],
      nextImages: [],
      previousImages: [],
      selectedImage: {},
      page: 1,
      limit: 30
    };
  },
  methods: {
    onPreviousClick: async function() {
      this.page--;
      this.nextImages = this.images;
      this.images = this.previousImages;
      this.previousImages = await getImages(this.page - 1, this.limit);
    },
    onNextClick: async function() {
      this.page++;
      this.previousImages = this.images;
      this.images = this.nextImages;
      this.nextImages = await getImages(this.page + 1, this.limit);
      preloadImages(this.nextImages);
    },
    onChange: debounce(loadImagesWithNewLimit, 250),
    selectImage: function(image) {
      this.selectedImage = image;
    },
    deselectImage: function() {
      this.selectedImage = {};
    }
  },
  async mounted() {
    this.images = await getImages();
    this.nextImages = await getImages(this.page + 1);
    this.previousImages = await getImages(this.page - 1);
    preloadImages(this.nextImages);
  }
};
</script>

<style lang="scss">
$page-background: rgb(166, 194, 221);

body {
  margin: 0;
  background-color: $page-background;
}
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
