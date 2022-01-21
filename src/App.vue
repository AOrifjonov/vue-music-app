<template>
  <div id="app">
    <header>
      <h1>My favorite music</h1>
    </header>
    <main>
      <section class="player">
        <h2 class="song-title">
          {{ current.title }} - <span> {{ current.artist }} </span>
        </h2>
        <div class="controls">
          <button class="prev" @click="prev">Prev</button>
          <button class="play" v-if="!isPlaying" @click="play">Play</button>
          <button class="pause" v-else @click="pause">Pause</button>
          <button class="next" @click="next">Next</button>
        </div>
      </section>

      <section class="playlist">
        <h3>The playslist</h3>
        <Yulduz :tarona="tarona" :current="current" @play="play" />
        <Jaloliddin :tarona="tarona" :current="current" @play="play" />
        <Xamdam :tarona="tarona" :current="current" @play="play" />
      </section>

    </main>
  </div>
</template>

<script>
import Jaloliddin from './components/Jaloliddin.vue';
import Xamdam from './components/Xamdam.vue'
import Yulduz from './components/Yulduz.vue'

export default {
  name: "App",
  components: {
    Yulduz,
    Xamdam,
    Jaloliddin,
  },
  data() {
    return {
      current: {},
      index: 0,
      isPlaying: false,
      jaloliddin: true,
      
      
      tarona: [
        {
          yulduz: [
            {
              title: "Yurak",
              artist: "Yulduz Usmonova",
              src: require("@/assets/yulduz/yurak-YulduzUsmonova.mp3"),
            },
            {
              title: "Muhabbat",
              artist: "Yulduz Usmonova",
              src: require("@/assets/yulduz/Muhabbat-YulduzUsmonova.mp3"),
            },
          ],
          xamdam: [
            {
              title: "Xolimga qara",
              artist: "Xamdam Sobirov",
              src: require("@/assets/xamdam/dil.mp3"),
            },
            {
              title: "Maktabimda",
              artist: "Xamdam Sobirov",
              src: require("@/assets/xamdam/Maktabimda-XamdamSobirov.mp3"),
            },
            {
              title: "Sevgisi arzonim",
              artist: "Xamdam Sobirov",
              src: require("@/assets/xamdam/sevgisiarzonim.mp3"),
            },
            {
              title: "Yaxshi qol",
              artist: "Xamdam Sobirov",
              src: require("@/assets/xamdam/yaxshiqol.mp3"),
            },
          ],
          jaloliddin: [
            {
              title: "Qalaysiz",
              artist: "Jaloliddin Ahmadaliyev",
              src: require("@/assets/jaloliddin/Qalaysiz.mp3"),
            },
            {
              title: "Unutganim rost",
              artist: "Jaloliddin Ahmadaliyev",
              src: require("@/assets/jaloliddin/ona.mp3"),
            },
            {
              title: "Do'stlarim",
              artist: "Jaloliddin Ahmadaliyev",
              src: require("@/assets/jaloliddin/dostlarim.mp3"),
            },
            {
              title: "Ex jo'ralar",
              artist: "Jaloliddin Ahmadaliyev",
              src: require("@/assets/jaloliddin/joralar.mp3"),
            },
          ],
        },
      ],
      player: new Audio(),
    };
  },
  methods:{

    play(song) {
      if (typeof song.src != "undefined") {
        this.current = song;
        this.player.src = this.current.src;
      }
      this.player.play();
      this.isPlaying = true;
    },

    pause() {
      this.player.pause();
      this.isPlaying = false;
    },

    next() {
      this.index++;
      if (this.index > this.tarona[0].jaloliddin.length - 1) {
        this.index = 0;
      }
      this.current = this.tarona[0].jaloliddin[this.index];
      this.play(this.current);
      this.player
        .addEventListener("ended", function () {
          this.index++;
          if (this.index < 0) {
            this.index = this.songs.length - 1;
          }
          this.current = this.songs[this.index];
        })
        .bind(this);
      this.isPlaying = true;
    },

    prev() {
      this.index--;
      if (this.index < 0) {
        this.index = this.tarona[0].jaloliddin.length - 1;
      }
      this.current = this.tarona[0].jaloliddin[this.index];
      this.play(this.current);
      this.isPlaying = true;
    },
  },

  created() {
    this.current = this.tarona[0].xamdam[this.index];
    this.player.src = this.current.src;
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: sans-serif;
}

header {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 15px;
  background-color: #212121;
  color: #fff;
}

main {
  width: 100%;
  max-width: 768px;
  margin: 0 auto;
  padding: 25px;
}

.song-title {
  color: #53565a;
  font-size: 32px;
  font-weight: 700;
  text-transform: uppercase;
  text-align: center;
}

.song-title span {
  font-weight: 400;
  font-style: italic;
}

.controls {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 30px 15px;
}

button {
  appearance: none;
  cursor: pointer;
  border: none;
  background: none;
  outline: none;
}

button:hover {
  opacity: 0.8;
}

.play,
.pause {
  font-size: 20px;
  font-weight: 700;
  padding: 15px 25px;
  margin: 0 15px;
  background: #cc2e5d;
  border-radius: 8px;
  color: #fff;
}

.next,
.prev {
  font-size: 16px;
  font-weight: 700;
  padding: 10px 20px;
  margin: 0 15px;
  background: #ff5858;
  border-radius: 8px;
  color: #fff;
}

.playlist {
  padding: 0 30px;
}

.playlist h3 {
  color: #212121;
  font-size: 28px;
  font-weight: 400;
  margin-bottom: 30px;
  text-align: center;
}

.playlist .song {
  display: block;
  width: 100%;
  padding: 15px;
  font-size: 20px;
  font-weight: 700;
  cursor: pointer;
}

.playlist .song:hover {
  color: #ff5858;
}
.playlist .song.playing {
  color: rgb(77, 71, 71);
  border-radius: 5px;
  box-shadow: 3px 4px 7px rgb(48, 46, 46);
}

.artist-name {
  display: block;
  width: 100%;
  font-size: 30px;
  align-items: center;
  padding: 10px;
  margin: 5px;
  border-radius: 5px;
  background-color: rgb(212, 212, 212);
}
</style>
