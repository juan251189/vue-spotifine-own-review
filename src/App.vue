<template>
<div id="app">
  <div class="container-fluid">
    <div class="header-page">
      <h1>Guitar<span>Covers</span></h1>
    </div>

    <div class="main" >
      <section id="front" class="container-fluid">
        <div class="row">
        <div class="col-sm-12 col-md-4  p-0" >
          <img class="image-front" :src="current.image" alt="">
        </div>

        <div class="col-sm-12 col-md-8 " >
          <h1>{{current.title}}</h1>  <h3>{{current.artist}}</h3>
          <p>{{current.paragraph}}</p>

        </div>
</div>
      </section>




      <div class="title-player"></div>
      <div class="image-player"></div>



      <div class="list-container">

        <div class="row list-header" >
          <div class="col-sm-6 col-7" >title</div>
          <div class="col-sm-6 col-5"  >album</div>
        </div>
        <div class="list-songs" v-for="(song,i) in songs" :key="i">
          <div class="row" style="margin-bottom:5px;">

            <div class="col-sm-6 col-7" ><span class="icon"><i class="fab fa-itunes-note " /></span>
              <div class="content">
                <img :src="song.image" alt="" class="song-image">
                <a>
                  <p class="list-song-title" @click="selectSong(song,i)" :class="(song.src === current.src) ? 'playing' :''">{{song.title}}</p>
                </a>
                <p>{{song.artist}}</p>
              </div>
            </div>
            <div class="col-sm-6 col-5 song-album"  >
              <p :class="(current.src == song.src) ? 'playing' : ''">{{song.album}}</p>
            </div>
          </div>
        </div>
      </div>

      <div class="buttons">
        <button v-on:click="randomactive=!randomactive"
        :class="(randomactive === true) ? 'playing' :''">Random</button>
        <button @click="prev">prev</button>
        <button class="far fa-pause-circle" v-if="isPlaying" @click="pauseSong"></button>
        <button class="far fa-play-circle" v-else @click="playSong"></button>
        <button @click="next">Next</button>
        <button >Repeat</button>

      </div>


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
          album: "Right the lightning",
          src: require("./assets/songs/metallica/forwhom.mp3"),
          image: require("./assets/songs/metallica/ride-the-lightning2.jpeg"),
          paragraph:"is a song by American heavy metal band Metallica. It was first released on the group's second album, Ride the Lightning (1984). Elektra Records also released it as a promotional single, with both edited and full-length versions. The song is generally regarded as one of Metallica's most popular; by March 2018, it ranked number five on the band's live performance count.[2] Several live albums and video albums include the song."
        },
        {
          artist: "Metallica",
          title: "Creeping Death",
          album: "Ride the lightning",
          src: require("./assets/songs/metallica/creeping-death.mp3"),
          image: require("./assets/songs/metallica/ride-the-lightning2.jpeg"),
          paragraph:"Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."
        },
        {
          artist: "Megadeath",
          title: "A tout le monde",
          album: " to be researched ",
          src: require("./assets/songs/megadeath/a-toute-le-monde.mp3"),
          image: require("./assets/songs/megadeath/Megadeth-Youthanasia.jpg"),
          paragraph:"Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."
        },
        {
          artist: "Scorpions",
          title: "Still Loving You",
          album: " to be research",
          src: require("./assets/songs/scorpions/still-loving-you.mp3"),
          image: require("./assets/songs/scorpions/scorpions-logo.jpeg"),
          paragraph:"Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."
        },
        {
          artist: "The Eagles",
          title: "Hotel California Solo",
          album: " to be research",
          src: require("./assets/songs/hotel-california-solo.mp3"),
          image: require("./assets/logo.png"),
          paragraph:""
        },
         {
          artist: "Korn",
          title: "Blind",
          album: "Korn reharsal",
          src: require("./assets/songs/blind-korn.mp3"),
          image: require("./assets/korn-logo.jpeg"),
          paragraph:"is an American nu metal band from Bakersfield, California, formed in 1993. The band is notable for pioneering the nu metal genre and bringing it into the mainstream."
        }
      ],
      isPlaying: false,
      player: new Audio(),
      index: 0,
      randomactive:false



    }
  },

  methods: {


    playSong() {
      /*  if (typeof song.src !="undefined"){
        this.current=song;
      }
      this.player.src=this.current.src;
      this.player.play();
      this.isPlaying=true;
!
*/
      if (Object.keys(this.current).length === 0) {
        this.current = this.songs[0];
        console.log(this.current);
        this.player.src = this.current.src;
        this.player.play();
        this.isPlaying = true;
      } else {
        this.player.play();
        this.isPlaying = true;
      }

    },
    pauseSong() {
      this.player.pause();
      this.isPlaying = false;

    },
    prev() {
      this.index--;
      if (this.index < 0) {
        this.index = this.songs.length - 1;
        console.log(this.current);
      }
      this.current = this.songs[this.index];
      this.player.src = this.current.src;
      this.player.play();
    },
    next() {
       if(this.randomactive== true){


    var number=Math.floor(Math.random()*(this.songs.length));
           this.index=number;
           this.current = this.songs[this.index];
           this.player.src = this.current.src;
           this.player.play();
             console.log(this.index);
       }

else{
      this.index++;
      if (this.index > this.songs.length - 1) {
        //this.index=this.songs.length-1;
        this.index = 0;
      }
      this.current = this.songs[this.index];
      this.player.src = this.current.src;
      this.player.play();
      console.log(this.index);
    }},
    selectSong(song, i) {
      if (typeof song.src != "undefined") {
        this.current = song;
      }

      this.player.pause();
      this.current = song;
      this.player.src = this.current.src;
      this.player.play();
      this.isPlaying = true;
      this.index = i;
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
  margin: 0;
  padding: 0;
  background-color: #131313;
  overflow-x: hidden;

}



.container-fluid {
  padding: 0;
  width: 100vw;
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

  position: fixed;
  z-index: 1;
}

.header-page h1 {
  color: #FFFFFF;
  font-weight: 400;
}

.header-page span {
  color: #41a8e2;
  font-weight: 600;
}

.main {
  padding-top: 80px;

  height: 1500px;
}

#front {
  background-image: linear-gradient(#525252, #2C2C2C);
  height: 450px;
  padding: 15px;
  overflow-y:hidden;
  color: #C2C2C2;
  

  font-family: "montserrat",sans-serif;


}
#front h1{
  font-size: 3.5em;
  color: #f3f3f3;

  font-weight: 700;
}
#front h3{
  color:#F3F3F3;

}

#front .image-front{
  height:70%;
  width: 100%;
  padding-left: 0px;
  margin-left: 0px;
  text-align: ri;

  

}
.list-songs {



  width: 100vw;
  color: #F3F3F3;

  font-size: 13px;
  font-family: 'montserrat', sans-serif;
  font-weight: 400;
  line-height: 22px;

  padding: 10px 45px;


}
.list-header{
  padding: 10px 45px;

  color:#f3f3f3;
  border-bottom: 2px solid #383838;

}
.list-container {
  background-color: #131313;
  height: 100vh;
  margin: 0 20%;
 
}


.song-image{
  width: 100px;
  height: 90px;
  float: left;
  margin-right: 15px;

}

.list-song-title {
  font-size: 17px;
  cursor: pointer;
  padding-top: 10px;
}

.list-songs .icon {
  float: left;
  margin-right: 8px;
  position: relative;

}

.list-songs .content {
  margin-top: 0px;
  margin-left: 21px;

}

.list-songs .song-album{
  padding-top: 10px;
}
.playing {
  color: #4ef002;

}

.buttons {
  position: fixed;
  bottom: 0;
  display: flex;
  height: 80px;
  width: 100vw;

  justify-content: center;
  align-items: center;
  border: 1px solid white;

  background-color: #282828;

}

.buttons button {
  
 

  padding: 10px;
  margin: 0 15px;


  border-radius: 7px;







}


.fa-pause-circle:hover {

  font-size: 1em;
  transition: 1s;
}


@media (max-width:900px){
  .list-container {
  background-color: #131313;
  height: 100vh;
  width: 100%;
  margin:0px;
}
}
</style>
