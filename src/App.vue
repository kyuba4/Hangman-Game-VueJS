<template>
   <div id="app">
      <router-view />
   </div>
</template>

<script>
export default {
   methods: {
      setTheme() {
         const theme = localStorage.getItem("theme");

         if (theme == "light") {
            document.body.className = "light-theme";
         } else {
            document.body.className = "dark-theme";
         }
      },
   },
   created() {
      this.setTheme();
   },
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@400;700&display=swap");

* {
   margin: 0;
   padding: 0;
   box-sizing: border-box;
   font-family: "Poppins", sans-serif;
}

html {
   height: 100%;
}

body {
   height: 100%;
   background: var(--bg-color);
   transition: background 300ms;
}

#app {
   width: 100%;
   height: 100%;
   padding: 15px;
}

.light-theme {
   --text-color: #323232;
   --bg-color: #fff;
}

.dark-theme {
   --text-color: #fff;
   --bg-color: #323232;
}
</style>
