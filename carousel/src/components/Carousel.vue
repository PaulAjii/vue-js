<template>
  <Carousel
    :wrap-around="true"
    :autoplay="5000"
    :mouse-drag="true"
>
    <Slide
        v-for="slide in 10"
        :key="slide"
    >
        <div class="carousel__item">
            {{ slide }}
        </div>
    </Slide>

    <template #addons>
      <Navigation />
      <Pagination />
    </template>
  </Carousel>
</template>

<script setup>
import 'vue3-carousel/dist/carousel.css'
import { Carousel, Slide, Navigation, Pagination } from 'vue3-carousel'
</script>

<style scoped>
.carousel__item {
    min-height: 250px;
    width: 100%;
    background-color: rgb(0, 255, 136);
    color: rgb(255, 255, 255);
    font-size: 20px;
    border-radius: 8px;
    display: flex;
    justify-content: center;
    align-items: center;
}

.carousel__slide {
    padding: 10px;
}

.carousel__prev, 
.carousel__next {
    box-sizing: content-box;
    border: 2px solid white;
}
</style>