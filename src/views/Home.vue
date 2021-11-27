<template>
   <div>
      <h1>Hangman</h1>
      <div class="switch-wrap">
         <ThemeSwitcher />
      </div>
      <Keyboard @btnClicked="btnClicked" />
   </div>
</template>

<script>
import ThemeSwitcher from "../components/ThemeSwitcher.vue";
import Keyboard from "../components/Keyboard.vue";

export default {
   name: "Home",
   components: {
      ThemeSwitcher,
      Keyboard,
   },
   methods: {
      btnClicked(letter) {
         console.log(letter);
      },
   },
};
</script>
<style lang="scss" scoped>
h1 {
   color: var(--text-color);
   font-size: 4rem;
   text-align: center;
}

.switch-wrap {
   position: absolute;
   top: 30px;
   right: 30px;
}
</style>