<template>
  <div
    class="retro-cursor-text"
    :class="{wideFont: type === 'wide',
              normalFont: type === 'normal'}"
    :style="{fontSize: size + 'px'}"
  >
    {{ this.printedText }}<div class="terminal-cursor">{{ this.cursor }}</div>
  </div>
</template>

<script>
export default {
  name: 'RetroCursorText',
  data() {
    return ({
      printedText: '',
      cursor: '▊',
    })
  },
  props: {
    text: {
      type: String,
      required: true,
    },
    type: {
      type: String,
      required: false,
      default: 'normal'
    },
    size: {
      type: Number,
      required: false,
      default: 20
    }
  },
  mounted() {
    setTimeout(() => {
      this.textAnimation();
    }, 1500);
  },
  methods: {
    textAnimation() {
      const l = this.text.length;
      let i = 0;
      let interval = setInterval(() => {
        this.printedText += this.text[i];
        if (i < l - 1)
          i++;
        else {
          this.printedText = this.text;
          clearInterval(interval);
        }
      }, 40);
    }
  }
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css?family=Press+Start+2P|VT323&display=swap');

.wideFont {
  font-family: 'Press Start 2P', monospace;
}

.normalFont {
  font-family: 'VT323', monospace;
}

.retro-cursor-text {
  color: rgb(0, 225, 0);
}

.terminal-cursor {
    opacity: 0;
    display: inline-block;
    animation: blink;
    animation-duration: 850ms;
    animation-iteration-count: infinite;
  }

  @keyframes blink {
    0% {opacity: 1;}
    15% {opacity: 0;}
    60% {opacity: 0;}
    75% {opacity: 1;}
    100% {opacity: 1;}
  }

</style>
