<template>
   <div></div>
</template>

<script>
export default {
   name: "Keyboard",
   data() {
      return {
         letters: "abcdefghijklmnopqrstuvwxyz",
      };
   },
   methods: {
      renderKeyboard() {
         this.letters.split("").forEach((letter) => {
            console.log(letter);
         });
      },
   },
   created() {
      this.renderKeyboard();
   },
};
</script>

<style lang="scss">
</style>