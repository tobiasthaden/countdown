<template>
  <div id="app">
    <div>
      <p>Stay tuned</p>
      <div class="countdown">
        <p>{{ (days < 10) ? '0' : '' }}{{ days }} day{{(days != 1) ? 's ' : ' '}}</p>
        <p>{{ (hours < 10) ? '0' : '' }}{{ hours }} hour{{(hours != 1) ? 's ' : ' '}}</p>
        <p>{{ (minutes < 10) ? '0' : '' }}{{ minutes }} minute{{(minutes != 1) ? 's ' : ' '}}</p>
        <p>{{ (seconds < 10) ? '0' : '' }}{{ seconds }} second{{(seconds != 1) ? 's ' : ' '}}</p>
      </div>
      <p>
        <a href="mailto:hello@tobiasthaden.com">hello@tobiasthaden.com</a>
      </p>
    </div>
  </div>
</template>

<script>

export default {
  name: 'app',

  data() {
    return {
      now: new Date(),
      end: new Date('2018-08-01 12:00:00'.replace(/-/g, "/")) // REGEX to 2018/08/01 12:00:00 'cause of that shitty Safari Date.parse Bug!
    };
  },

  mounted() {
      setInterval( () => {
          this.now = new Date();
      }, 1000);
  },

  computed: {
    days() {
      return Math.floor(this.remaining / (1000 * 60 * 60 * 24));
    },

    hours() {
      return Math.floor(this.remaining / (1000 * 60 * 60) % 24);
    },

    minutes() {
      return Math.floor( (this.remaining / 1000 / 60) % 60 );
    },

    seconds() {
      return Math.floor( (this.remaining / 1000) % 60 );
    },

    remaining() {
      return this.end.getTime() - this.now.getTime();
    }
  }
}
</script>

<style lang="scss">
@import url('https://cdn.rawgit.com/tonsky/FiraCode/1.205/distr/fira_code.css');
* {
  margin: 0;
  padding: 0;
  font-feature-settings: "calt" 1;
  font-variant-ligatures: contextual;
  text-decoration: none;
  color: inherit;
}
#app {
  font-family: 'Fira Code', monospace;
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
}
.countdown {
  font-size: 5vw;
}
p{
  margin-bottom: 20px;
}
</style>
