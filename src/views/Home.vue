<template>
   <div>
      <div class="switch-wrap"><ThemeSwitcher /></div>
      <h1>Hangman</h1>
      <div class="loader-wrap">
         <Loader v-show="loading" />
      </div>
      <div v-show="!loading" style="padding-bottom: 5px">
         <div class="chances-left">Chances Left: {{ chancesLeft }}</div>
         <div class="clue">Clue: {{ clue }}</div>
         <div class="hangman-img">
            <img :src="require(`../../src/assets/${currentImage}.jpg`)" alt="Hangman Image" draggable="false" />
         </div>
         <div class="word">
            {{ currentStateOfWord }}
         </div>
         <Keyboard @btnClicked="checkLetterInWord" v-show="!gameLost && !gameWon" />
         <div class="msg msg--lost" v-show="gameLost && word">
            You lost<br /><span>The word was: {{ gameLost ? word : "" }}</span>
         </div>
         <div class="msg msg--won" v-show="gameWon && word">
            Congrats!<br />
            <span>You Won!</span>
         </div>
         <ResetGameButton @clicked="resetGame" />
      </div>
   </div>
</template>

<script>
import ThemeSwitcher from "../components/ThemeSwitcher.vue";
import Keyboard from "../components/Keyboard.vue";
import ResetGameButton from "../components/ResetGameButton.vue";
import Loader from "../components/Loader.vue";

export default {
   name: "Home",
   components: {
      ThemeSwitcher,
      Keyboard,
      ResetGameButton,
      Loader,
   },
   data() {
      return {
         loading: false,
         chancesLeft: 6,
         currentImage: 0,
         clue: "",
         word: "",
         currentStateOfWord: "",
      };
   },
   methods: {
      async setWord() {
         this.loading = true;
         const response = await fetch("https://random-words-api.vercel.app/word");
         const data = await response.json();

         this.word = data[0].word.toLowerCase();
         this.clue = data[0].definition;

         if (this.word.includes("-")) {
            this.setWord();
         }

         // Change word's letters to '_' e.g. horse = _ _ _ _ _
         this.currentStateOfWord = this.word
            .split("")
            .map((letter) => {
               letter = "_";
               return letter;
            })
            .join("");

         this.loading = false;
      },
      checkLetterInWord(id) {
         // Index of guessing letter
         let letterIndex = [];

         if (this.word.includes(id)) {
            this.word.split("").forEach((letter, index) => {
               letter == id ? letterIndex.push(index) : null;
            });
            this.currentStateOfWord = this.updateCurrentStateOfWord(letterIndex);
         } else {
            this.chancesLeft--;
            this.currentImage++;
         }
      },
      updateCurrentStateOfWord(index) {
         let newWordState = this.currentStateOfWord.split("");
         for (let i in index) {
            newWordState[index[i]] = this.word.split("")[index[i]];
         }

         return newWordState.join("");
      },
      resetGame() {
         this.setWord();
         this.chancesLeft = 6;
         this.currentImage = 0;
         this.$el.querySelectorAll(".button").forEach((button) => {
            button.removeAttribute("disabled");
         });
      },
   },
   created() {
      this.setWord();
   },
   computed: {
      gameLost() {
         return this.chancesLeft == 0;
      },
      gameWon() {
         return this.word == this.currentStateOfWord;
      },
   },
};
</script>
<style lang="scss" scoped>
h1 {
   color: var(--text-color);
   font-size: 5rem;
   text-align: center;
   transition: color 300ms;
}

.switch-wrap {
   position: absolute;
   top: 30px;
   right: 30px;
}

.chances-left,
.word,
.clue {
   color: var(--text-color);
   transition: color 300ms;
   text-align: center;
   margin: 10px 0;
}

.loader-wrap {
   position: fixed;
   top: 50%;
   left: 50%;
   transform: translate(-50%, -50%);
}

.chances-left {
   font-size: 2rem;
   font-weight: bold;
}

.clue {
   font-size: 1.1rem;
}

.word {
   margin: 40px 0;
   font-size: 2rem;
   text-transform: uppercase;
}

.hangman-img {
   margin: 0 auto;
   position: relative;
   width: 100px;
   height: 175px;

   img {
      position: absolute;
      left: 30%;
      width: 100%;
      height: 100%;
   }
}

.msg {
   text-transform: uppercase;
   font-size: 2.5rem;
   font-weight: bold;
   text-align: center;

   span {
      color: var(--text-color);
      font-size: 2rem;
      transition: color 300ms;
   }

   &--lost {
      color: red;
   }

   &--won {
      color: greenyellow;
   }
}

@media (max-width: 500px) {
   h1 {
      font-size: 3rem;
   }

   .chances-left {
      font-size: 1.4rem;
   }

   .clue {
      font-size: 0.9rem;
   }
}

@media (max-width: 650px) {
   .switch-wrap {
      top: 15px;
      right: 10px;
      transform: scale(0.9);
   }
}
</style>