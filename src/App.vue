<template>
  <!--html code-->
  <div id="app">
    <header>
      <h1>My music</h1>
    </header>
    <main>
      <section class="player">
        <h2 class="songTitle">{{ current.title }} - <span>{{current.artist}}</span></h2>
        <!--placing controls here-->
        <div class="controls">
          <button>Previous</button>
          <button>Play</button>
          <button>Pause</button>
          <button>Next</button>
        </div>
      </section>
    </main>
  </div>
</template>

<script>
/*Javascript code*/
export default {
  name: 'App',
  /*  data works similar to state in react in this case*/
  data() {
    return {
      current: {
  /*      title: 'SONG TITLE'*/
      },
      index: 1,
      songs: [
        {
          /*Example song obtained from Bensound: https://www.bensound.com/royalty-free-music/track/enigmatic*/
        title: 'Enigmatic',
          artist: 'Bensound',
          src: require('./assets/bensound-enigmatic.mp3')
        },
        {
         /* Example song obtained from Bensound: https://www.bensound.com/royalty-free-music/track/epic*/
          title: 'Epic',
          artist: 'Bensound',
          src: require('./assets/bensound-epic.mp3')
        },
        {
          /* Example song obtained from Bensound: https://www.bensound.com/royalty-free-music/track/evolution*/
          title: 'Epic',
          artist: 'Bensound',
          src: require('./assets/bensound-evolution.mp3')
        }
      ],
      player: new Audio(),
    }
  },
  created (){
      this.current = this.songs[this.index];
      this.player.src = this.current.src;
     /* comment/uncomment to test wether it plays*/
      this.player.play();
  }

}
</script>

<style>
/*css code*/

* {
  /*removes browser default settings*/
  margin: 0;
  padding: 0;
}

header {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 20px;
  background-color: darkslateblue;
  color: white;
}
h2{
  padding: 3px;
}
</style>
