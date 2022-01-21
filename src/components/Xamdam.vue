<template>
  <button @click="setXamdam(!xamdam)" class="artist-name">
    Xamdam Sobirov
  </button>
  <div v-if="!xamdam">
    <button 
        :class="t.src == current.src ? 'song playing' : 'song'"
        :key="t.src" v-for="t in tarona[0].xamdam" 
        @click="$emit('play', t)">
        
      {{ t.title }} - {{ t.artist }}
    </button>
  </div>
</template>

<script>
export default {
  name: "xamdam",
  props: ["tarona", "current"],

  data() {
    return {
      xamdam: true,
    };
  },

  methods: {
    setXamdam(y) {
      this.xamdam = y;
    },
  },
};
</script>

