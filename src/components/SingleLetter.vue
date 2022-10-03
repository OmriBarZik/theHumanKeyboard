<script>
import theHumanKeyboard from '../assets/theHumanKeyboard.jpeg';

const img = new Image();
img.src = theHumanKeyboard;

const ABC = 'abcdefghijklmnopqrstuvwxyz';
const LETTER_WIDTH = 126;
const LETTER_HIGHT = 126;
const LETTER_ROW_LENGTH = 6;

/** @type {Record<string, {offsetX: number, offsetY: number}>} */
const letterArrangement = {
  a: {
    offsetX: 7,
    offsetY: 7,
  },
};

export default {
  props: {
    letters: String,
  },
  updated() {
    this.draw();
  },
  data() {
    return {
      theHumanKeyboard,
      letterArrangement,
    };
  },
  methods: {
    getOffsetX() {
      if (!this.letterArrangement[this.letter]) {
        return { offsetX: 0 };
      }

      return this.letterArrangement[this.letter].offsetX;
    },
    getOffsetY() {
      if (!this.letterArrangement[this.letter]) {
        return { offsetY: 0 };
      }

      return this.letterArrangement[this.letter].offsetY;
    },
    draw() {
      if (!this.letters) {
        return;
      }
      /** @type {HTMLCanvasElement} */
      const canvasLetters = this.$refs.canvasLetters;
      const ctx = canvasLetters.getContext('2d');
      ctx.clearRect(0, 0, canvasLetters.width, canvasLetters.height);
      let letterPosition = 0;

      this.letters.split('').forEach((letter) => {
        const letterIndex = ABC.indexOf(letter.toLowerCase());
        if (letterIndex === -1) {
          return;
        }

        const letterTopPadding = Math.floor(letterIndex / LETTER_ROW_LENGTH);
        const letterLeftPadding = Math.floor(letterIndex % LETTER_ROW_LENGTH);

        ctx.drawImage(
          img,
          7 + letterLeftPadding * LETTER_WIDTH + 7 * letterLeftPadding,
          7 + letterTopPadding * LETTER_HIGHT + 7 * letterTopPadding,
          LETTER_WIDTH,
          LETTER_HIGHT,
          LETTER_WIDTH * letterPosition,
          0,
          LETTER_WIDTH,
          LETTER_HIGHT
        );

        letterPosition++;
      });

      // ctx.drawImage(img, 7, 7, 126, 126, 0, 0, 126, 126);
      // ctx.drawImage(img, 140, 7, 126, 126, 130, 0, 126, 126);
    },
  },
};
</script>

<template>
  <canvas width="1200" height="500" ref="canvasLetters"></canvas>
</template>
