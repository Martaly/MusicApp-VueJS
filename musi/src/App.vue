<template>
  <div id="app">
<header>
<h1>My Music</h1>
</header>
<main>
  <section class="player">
    <h2 class="song-title">{{current.title}} - <span>{{current.artist}}</span></h2>
    <div class="controls">
      <button class="prev" @click="prev">Prev</button>
            <button class="play" v-if="!isPlaying" @click="play">Play</button>
                        <button class="pause" v-else @click="pause">Pause</button>
      <button class="next" @click="next">Next</button>
    </div>
    </section>
    <section class="playlist">
      <h3>The Playlist</h3>
      <button v-for="song in songs" :key="song.src" @click="play(song)" :class="(song.src == current.src ) ?'song playing' : 'song'">
        {{song.title}} - {{song.artist}}
      </button>
    </section>
</main>
  </div>
</template>

<script>

export default {
  name: 'App',
  data () {
    return {
      current: {},
      index:0,
      isPlaying:false,
  songs:[
    {
     title:"Am I Wrong",
      artist:"Nico-Vinz",
      src: require("/home/aly/Desktop/MusicApp-VueJS/musi/src/assets/nico-vinz-am-i-wrong-gryffin-remix.mp3"),
      },
      {
        title: "Love Story",
        artist : "Taylor Swift",
        src: require ("/home/aly/Desktop/MusicApp-VueJS/musi/src/assets/taylor-swift-love-story-lyrics-disco-lines-remix-tiktok-song.mp3"),
      }
      ],
      player: new Audio()
  }
  },
  methods:{
       play (song) {
      if (typeof song.src != "undefined") {
        this.current = song;
        this.player.src = this.current.src;
      }
      this.player.play();
      this.player.addEventListener('ended', function () {
        this.index++;
        if (this.index > this.songs.length - 1) {
          this.index = 0;
        }
        this.current = this.songs[this.index];
        this.play(this.current);
      }.bind(this));
      this.isPlaying = true;
    },
      pause() {
        this.player.pause();
        this.isPlaying = false;
        },
        next() {
          this.index++;
          if(this.index > this.songs.lenght - 1) {
            this.index = 0;
            }
            this.current = this.songs[this.index];

            this.play(this.current);
        },
        prev() {
          this.index--;
          if(this.index < 0) {
            this.index = this.songs.lenght - 1;
            }
            this.current = this.songs[this.index];

            this.play(this.current);
        },
        },
  created() {
    this.current = this.songs[this.index];
    this.player.src= this.current.src;
    //this.player.play();
    }
   }

</script>

<style>
*{
  margin:0;
  padding:0;
  box-sizing: border-box;
  
  }
body{
  font-family: monospace;
  display: flex;
flex-direction: column;
justify-content: center;
align-items: center;
    padding: 3rem;
    background-color: black;
  }
header{
  display: flex;
  justify-content: center;
  align-items: center;
  padding:3rem;
  background-color: #44ffd2;
  color:white;
      border-radius: 10px;

  }
  main{
    width: 30rem;
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    align-items: center;
    font-family: monospace;
        height: 20rem;
}


    
   
    section  {
      color: white;
      background-color: #616163;
    height: 10rem;
    padding: 1rem;
        width: 100%;
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    text-align: center;
        border-radius: 10px;

    }
    section .controls{
      display: flex;
      flex-direction: row;
      justify-content: space-evenly;
    
    }
    section .controls button{
      padding:0.5em;
      color:white;
      border-radius: 10px;
      border:none;
      background-color:#616163 ;
      width:20%;
      box-shadow:  20px 20px 60px #525254, 
             -20px -20px 60px #707072;
    }
    section .controls button:hover{
      background-color: #44ffd2;
    }
    .playlist{
      height:8rem;
      }
.playlist button{
  height:2rem;
  border-radius:5px;
  border:none;
  background-color: #FFBFA0;
  }
</style>
