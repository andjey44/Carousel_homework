<template>
  <div id="app">
    <div class="carousel">
      <div class="carousel-inner">
        <div v-for="(image, index) in images" :key="index" :class="{ active: index === currentIndex }">
          <img :src="image.src" :alt="image.alt">
        </div>
      </div>
      <a class="carousel-control-prev" @click="prevImage"><span class="carousel-control-prev-icon"></span></a>
      <a class="carousel-control-next" @click="nextImage"><span class="carousel-control-next-icon"></span></a>
      <ol class="carousel-indicators">
        <li v-for="(image, index) in images" :key="index" :class="{ active: index === currentIndex }" @click="setCurrentIndex(index)"></li>
      </ol>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data() {
    return {
      images: [
        { src: "'../assets/image1.svg'", alt: "Image 1" },
        { src: "'../assets/image2.svg'", alt: "Image 2" },
        { src: "'../assets/image3.svg'", alt: "Image 3" }
      ],
      currentIndex: 0
    };
  },
  methods: {
    prevImage() {
      this.currentIndex = (this.currentIndex === 0) ? this.images.length - 1 : this.currentIndex - 1;
    },
    nextImage() {
      this.currentIndex = (this.currentIndex === this.images.length - 1) ? 0 : this.currentIndex + 1;
    },
    setCurrentIndex(index) {
      this.currentIndex = index;
    }
  },
  mounted() {
    setInterval(() => {
      this.nextImage();
    }, 10000);
  }
}
</script>
<style>
.carousel {
  position: relative;
}

.carousel-inner {
  position: relative;
  overflow: hidden;
}

.carousel-inner > div {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  opacity: 0;
  transition: opacity 0.5s ease-in-out;
}

.carousel-inner > .active {
  opacity: 1;
}

.carousel-indicators {
  position: absolute;
  bottom: 0;
  left: 50%;
  transform: translateX(-50%);
  margin: 0;
  padding: 0;
  list-style: none;
}

.carousel-indicators li {
  display: inline-block;
  width: 10px;
  height: 10px;
  margin: 0 5px;
  background-color: #ccc;
  border-radius: 50%;
  cursor: pointer;
}

.carousel-indicators li.active {
  background-color: #333;
}

.carousel-control-prev,
.carousel-control-next {
  position: absolute;
  top: 50%;
  z-index: 1;
  display: flex;
  justify-content: center;
  align-items: center;
  width: auto;
  height: auto;
  padding: 10px;
  font-size: 32px;
  color: #fff;
  background-color: rgba(0,0,0,0.5);
  border-radius: 50%;
  cursor: pointer;
}

.carousel-control-prev {
  left: 0;
}

.carousel-control-next {
  right: 0;
}

img{
  width: 500px;
  height: 500px;
}
</style>
