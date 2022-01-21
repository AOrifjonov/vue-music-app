<template>
  <button @click="setJaloliddin(!jaloliddin)" class="artist-name">
    Jaloliddin Ahmadaliyev
  </button>
  <div v-if="!jaloliddin">
    <button 
        :class="t.src == current.src ? 'song playing' : 'song'"
        :key="t.src" v-for="t in tarona[0].jaloliddin" 
        @click="$emit('play', t)">
        
      {{ t.title }} - {{ t.artist }}
    </button>
  </div>
</template>

<script>
export default {
  name: "jaloliddin",
  props: ["tarona", "current"],

  data() {
    return {
      jaloliddin: true,
    };
  },

  methods: {
    setJaloliddin(y) {
      this.jaloliddin = y;
    },
  },
};
</script>

