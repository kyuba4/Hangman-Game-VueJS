<template>
   <button class="reset" @click="$emit('clicked')">Reset</button>
</template>
<script>
export default {
   name: "ResetGameButton",
};
</script>
<style lang="scss">
.reset {
   display: flex;
   justify-content: center;
   margin: 3rem auto;
   padding: 10px 20px;
   border: 0;
   outline: 0;
   background: var(--text-color);
   color: var(--bg-color);
   cursor: pointer;
   box-shadow: 0 0 3px 0 var(--text-color);
   transition: all 300ms;
   border-radius: 5px;

   &:hover {
      opacity: 0.8;
   }
}
</style>