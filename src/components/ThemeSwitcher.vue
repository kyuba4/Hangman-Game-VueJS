<template>
   <div class="switch-wrapper">
      <span class="change-theme-txt">Change Theme</span>
      <label>
         <input
            class="switch"
            type="checkbox"
            v-model="checkbox"
            @click="
               setTheme(checkbox);
               saveThemeChoice(checkbox);
            "
         />
         <div>
            <div></div>
         </div>
      </label>
   </div>
</template>

<script>
export default {
   name: "ThemeSwitcher",
   data() {
      return {
         checkbox: this.checkbox,
      };
   },
   methods: {
      saveThemeChoice(theme) {
         if (theme) {
            localStorage.setItem("theme", "light-theme");
         } else {
            localStorage.setItem("theme", "dark-theme");
         }
      },
      setTheme(theme) {
         if (theme) {
            document.body.className = "light-theme";
         } else {
            document.body.className = "dark-theme";
         }
      },
   },
   created() {
      const savedTheme = localStorage.getItem("theme");

      if (savedTheme == "light-theme") {
         this.checkbox = false;
      } else {
         this.checkbox = true;
      }

      this.setTheme(!this.checkbox);
   },
};
</script>

<style lang="scss" scoped>
.change-theme-txt {
   font-size: 0.8rem;
   color: var(--text-color);
   transition: color 300ms;

   @media (max-width: 650px) {
      display: none;
   }
}

.switch-wrapper {
   display: flex;
   flex-direction: column;
   justify-content: center;
   align-items: center;
   gap: 10px;
}

.switch {
   display: none;
}

.switch + div {
   width: 40px;
   height: 16px;
   border-radius: 12px;
   background-color: #fde68a;
   transition: background-color 200ms;
   cursor: pointer;
}

.switch:checked + div {
   background-color: #111827;
}

.switch + div > div {
   width: 16px;
   height: 16px;
   border-radius: 23px;
   background-color: #fff;
   transition: transform 250ms;
   pointer-events: none;
   box-shadow: 0 0 5px 0 #212121;
}

.switch:checked + div > div {
   transform: translateX(28px);
}
</style>