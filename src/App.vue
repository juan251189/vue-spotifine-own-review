<template>
<div id="app">
  <div class="container">
    <div class="header-page">
      <h1>Spoti<span>Fine</span></h1>
    </div>
    <div class="title-player">{{current.title}}</div>
    <div class="image-player"></div>


    <div class="list-songs" v-for="(song,i) in songs" :key="i">
      <i class="fab fa-itunes-note icon" />
      <div>
        <a v-on:click="next()">
          <h3>{{song.title}}</h3>
        </a>
        <p>{{song.artist}}</p>
      </div>
    </div>

    <div class="buttons">
      <button>prev</button>
      <button class="far fa-pause-circle" v-if="isPlaying" @click="pauseSong"></button>
      <button class="far fa-play-circle" v-else @click="playSong"></button>
      <button>Next</button>
    </div>



  </div>
</div>
</template>

<script>
export default {
  name: 'App',
  components: {

  },
  data() {
    return {
      current: {},
      songs: [{
          artist: "Metallica",
          title: "For whom the bell tolls",
          src: "./assets/bonita.mp3"
        },
        {
          artist: "Metallica",
          title: "Creeping Death",
          src: "./assets/logo.png"
        },
        {
          artist: "Megadeath",
          title: "A tout le mond",
          src: "./assets/logo.png"
        }
      ],
      isPlaying: false,



    }
  },
  created() {
    this.current = this.songs[0];
  },
  methods: {


    playSong() {
      var audio = new Audio(this.current.src);
      audio.play();

      this.isPlaying = !this.isPlaying;


    },
    pauseSong() {
      //player.pause();
      this.isPlaying = !this.isPlaying;
    },
    next(){
        for (var i = 0 ; i < this.songs.length; i++){

          if(this.current.src=this.songs[i].src)
          {
            if(i<this.songs.lenght){
              this.current=this.songs[i];
            }else{
                this.current=this.songs[0];
            }
          }else{
            console.log("hi");
          }

        }
    }
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  background-color: #272727;
}

.container {
  width: 80%;
  justify-content: center;
}

.header-page {
  display: flex;
  min-height: 80px;
  width: 100vw;
  justify-content: space-around;
  align-items: center;

  padding: 0 12px;

  background-color: #090909;

  font-size: 18px;
  font-family: 'montserrate', sans-serif;
}

.header-page h1 {
  color: #FFFFFF;
  font-weight: 400;
}

.header-page span {
  color: #41a8e2;
  font-weight: 600;
}

.list-songs {


  background-color: #101010;
  width: 100vw;
  color: #F3F3F3;

  font-size: 13px;
  font-family: 'montserrat', sans-serif;
  font-weight: 400;
  line-height: 22px;

  padding: 10px 45px;


}

.list-songs .icon {
  float: left;
  margin-right: 8px;
  position: relative;
  top: 3px;
}

.buttons {
  position: fixed;
  bottom: 0;
  display: flex;
  height: 80px;
  width: 100vh;

  justify-content: center;
  align-items: center;
  border: 1px solid white;

}

.buttons button {
  position: relative;
  height: 25px;
  background-color: none;
  margin: 0 15px;


}


.fa-pause-circle:hover {

  font-size: 1em;
  transition: 1s;
}
</style>
