<template>
  <main class="Main">
    <Worldmap :topics="topics" />
  </main>
</template>

<script>
import Worldmap from '../components/Worldmap.vue'
export default {
  name: 'App',
  data() {
    return {
      topics: [],
      sizeOfWorldMap: {
        aspectRatio: Number(2000 / 857).toFixed(3),
        width: '',
        height: '',
      },
    }
  },
  components: {
    Worldmap,
  },
  async fetch() {
    this.topics = await fetch('https://sandy.uber.space/items/topic')
      .then((res) => res.json())
      .then((topics) => topics.data)
  },
  computed: {
    isRatioBiggerThenMap() {
      const { aspectRatio, width, height } = { ...this.sizeOfWorldMap }
      return aspectRatio > width / height
    },
    windowRatio() {
      return this.sizeOfWorldMap.width / this.sizeOfWorldMap.height
    },
  },
  created() {
    this.addWindowHandler()
  },
  destroyed() {
    this.removeWindowHandler()
  },
  methods: {
    handleWindowResize() {
      this.sizeOfWorldMap.width = window.innerWidth
      this.sizeOfWorldMap.height = window.innerHeight
    },
    addWindowHandler() {
      window.addEventListener('resize', this.handleWindowResize)
      this.handleWindowResize()
    },
    removeWindowHandler() {
      window.removeEventListener('resize', this.handleWindowResize)
    },
  },
}
</script>
<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
.Main {
  width: 100vw;
  height: 100vh;
}
</style>
