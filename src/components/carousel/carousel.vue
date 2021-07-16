<template>
    <div class="carousel">
        <slot></slot>
        <button class="carousel__nav carousel__next" @click.prevent="next"></button>
        <button class="carousel__nav carousel__prev" @click.prevent="prev"></button>
    </div>
</template>
<script>
export default {
  data () {
    console.log(this.$children)
    return {
      index: 0,
      slides: []
    }
  },
  mounted () {
    this.slides = this.$children
    this.slides.forEach((slide, i) => {
      slide.index = i
    })
  },
  methods: {
    next () {
      this.index++
      if (this.index === this.slidesCount) {
        this.index = 0
      }
    },
    prev () {
      this.index--
      if (this.index < 0) {
        this.index = this.slidesCount - 1
      }
    }
  },
  computed: {
    slidesCount () {
      return this.slides.length
    }
  }
}
</script>
<style>
.carousel {
  position: relative;
}
.carousel__nav {
  position: absolute;
  top: 50% ;
  left: 10px;
  background: url('https://www.google.com/url?sa=i&url=https%3A%2F%2Fwww.shutterstock.com%2Fnl%2Fsearch%2Fnext%2Bbutton&psig=AOvVaw3fd5uN2lV06bQ1SAfctKit&ust=1626423479167000&source=images&cd=vfe&ved=0CAoQjRxqFwoTCIC60-DR5PECFQAAAAAdAAAAABAJ');
  width: 63px;
  height: 63px;
}
</style>
