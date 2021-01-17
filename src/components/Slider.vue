<template>
  <div>



    <div class="slider-item-wrapper">
      <div v-for="(slide, index) in slides" :key="slide.background">
        <transition name="slide-fade">
          <div v-if="currentSlide == index"
               :style="{backgroundColor: slide.background}"
               class="slider-item">
          </div>
        </transition>
      </div>
    </div>




    <div class="slide-dots-wrapper">
      <div v-for="(slideDot, index) in slideDots" :key="slideDot">
        <div @click="changeSlide(index)" class="slide-dot" :class="index === currentSlide ? 'activeSlideDot' : 'inActiveSlideDot'">
        </div>
      </div>
    </div>




  </div>
</template>

<script>
export default {
  name: "Slider",
  data() {
    return {
      slides: [
        {background: 'blue'},
        {background: 'yellow'},
        {background: 'green'}
      ],
      currentSlide: 0,
      sliderTimeOut: '',
      slideDots: 3
    }
  },
  methods: {
    changeSlide(slide) {
      this.currentSlide = slide
      clearTimeout(this.sliderTimeOut)
      this.sliderTimeOut = setInterval(() => {
        this.currentSlide = this.currentSlide === 2 ? 0 : this.currentSlide + 1
      }, 3000)
    }
  },
  mounted() {
    this.sliderTimeOut = setInterval(() => {
      this.currentSlide = this.currentSlide === 2 ? 0 : this.currentSlide + 1
    }, 3000)
  },
  beforeUnmount() {
    clearTimeout(this.sliderTimeOut)
  }
}
</script>

<style scoped>

.slider-item {
  width: 100%;
  height: 500px;
  position: absolute;
  top: 0;
}

.slider-item-wrapper {
  height: 440px;
}

.slide-dots-wrapper {
  display: flex;
  justify-content: center;
  position: absolute;
  width: 100%;
}

.activeSlideDot {
  background: white;
}

.inActiveSlideDot {
  background: black;
}

.slide-dot {
  width: 20px;
  height: 20px;
  border-radius: 50%;
  margin-right: 5px;
  opacity: 0.9;
  cursor: pointer;
}

.slide-fade-enter-active {
  transition: all 1s ease;
}

.slide-fade-leave-active {
  transition: all 1s ease;
}

.slide-fade-enter-from {
  transform: translateX(-100%);
  opacity: 0;
}

.slide-fade-leave-to {
  transform: translateX(100%);
  opacity: 0;
}
</style>