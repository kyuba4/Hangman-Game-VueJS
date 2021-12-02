<template>
   <div class="keyboard">
      <button
         class="button"
         v-for="(button, index) in buttons"
         :key="index"
         :id="button"
         @click="
            $emit('btnClicked', button);
            disableButton(button);
         "
      >
         {{ button }}
      </button>
   </div>
</template>

<script>
export default {
   name: "Keyboard",
   data() {
      return {
         letters: "abcdefghijklmnopqrstuvwxyz",
         buttons: [],
      };
   },
   methods: {
      renderKeyboard() {
         this.letters.split("").forEach((letter) => {
            this.buttons += letter;
         });
      },
      disableButton(letter) {
         document.getElementById(letter).disabled = true;
      },
   },
   created() {
      this.renderKeyboard();
   },
};
</script>

<style lang="scss">
.keyboard {
   display: flex;
   gap: 20px;
   justify-content: center;
   align-items: center;
   flex-wrap: wrap;
   max-width: 1000px;
   margin: 0 auto;

   .button {
      text-align: center;
      width: 50px;
      height: 50px;
      font-size: 1.3rem;
      border-radius: 5px;
      border: 0;
      outline: 0;
      background: transparent;
      cursor: pointer;
      box-shadow: 0 0 3px 0 var(--text-color);
      color: var(--text-color);
      transition: all 300ms;
      text-transform: uppercase;

      &:hover {
         transform: scale(0.95);
      }

      &:disabled {
         background: var(--text-color);
         color: var(--bg-color);
         pointer-events: none;
         transform-origin: center;
         transform: scale(0.9) rotateY(360deg);
      }
   }

   @media (max-width: 650px) {
      gap: 15px;

      .button {
         width: 40px;
         height: 40px;
         font-size: 1rem;
         padding: 0;
      }
   }
}
</style>