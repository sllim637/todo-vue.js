<template>
  <div>
    <carousel>
      <carousel-slide>
      Salut les gens
      <img src="https://picsum.photos/200/300?grayscale" alt="images">
      </carousel-slide>
      <carousel-slide>
      aurevoir les gens
      </carousel-slide>
    </carousel>
   <todos></todos>
  </div>
</template>

<script>
import Todos from './components/Todos.vue'
import Carousel from './components/carousel/carousel.vue'
import CarouselSlide from './components/carousel/CarouselSlide.vue'
export default {
  name: 'App',
  components: {
    Todos,
    Carousel,
    CarouselSlide
  }
}
</script>
