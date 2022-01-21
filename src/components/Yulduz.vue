<template>
  <button @click="setYulduz(!yulduz)" class="artist-name">
    Yulduz Usmonova
  </button>
  <div v-if="!yulduz">
    <button 
        :class="t.src == current.src ? 'song playing' : 'song'"
        :key="t.src" v-for="t in tarona[0].yulduz" 
        @click="$emit('play', t)">
        
      {{ t.title }} - {{ t.artist }}
    </button>
  </div>
</template>

<script>
export default {
  name: "yulduz",
  props: ["tarona", "current"],

  data() {
    return {
      yulduz: true,
    };
  },

  methods: {
    setYulduz(y) {
      this.yulduz = y;
    },
  },
};
</script>

