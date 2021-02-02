<template>

  <div :class="darkMode() ? 'darkBG' : 'lightBG'">
    <vue-particles
      class="particles"
      hoverMode="grab"
      clickMode="push"
      linesColor="#dedede"
      shapeType="circle"
      :color="darkMode() ? '#f5f5f5' : '#171717'"
      :particleOpacity="0.7"
      :particlesNumber="30"
      :particleSize="4"
      :linesWidth="1"
      :lineLinked="true"
      :lineOpacity="0.4"
      :linesDistance="150"
      :moveSpeed="3"
      :hoverEffect="true"
      :clickEffect="true"
    />
    <!-- Main -->
    <div class="main">
      <vue-typed-js
        class="vue-typed"
        :showCursor="false"
        :loop="true"
        :strings="[greetings() + ', ' + nicknames + '! ^5000', 'I always wanted to tell you... ^2500', `I just wanna say something. I Love U. That's all`, 'Nevermind! >///<',]"
        :backDelay="500"
        :typeSpeed="100"
        :backSpeed="20"
        :contentType="'null'"
      >
        <h1 class="typing"></h1>
      </vue-typed-js>

      <!-- Quotes -->
      <h1 class="quotes quotes-main"><strong>{{ quotes.quotes }}</strong></h1>
      <h5 class="quotes author">Created ♥  <a href="https://github.com/Zainal21">Muhamad Zainal Arifin</a></h5>
    </div>
  </div>
</template>

<script>
import quotesFile from "~/assets/quotes.js";
import variables from "~/assets/variables.js";

const { greetings } = variables;

const now = new Date().getHours();

if (process.browser) {
  function random(arr) {
    return arr[Math.floor(Math.random() * arr.length)];
  }

  window.onNuxtReady(app => {
    document.addEventListener("click", function(ev) {
      const x = ev.clientX;
      const y = ev.clientY;
      let el = document.createElement("div");
      el.innerHTML = `<h1>${random(["♥", "♥♥", "♥♥♥"])}</h1>`;
      el.classList.add("popup");
      el.style.left = `${x}px`;
      el.style.top = `${y}px`;
      document.body.appendChild(el)
      setTimeout(function() {
        el.style.display = "none";
      }, 3000);
    });
  });
}

export default {
  transition: "slide-x-transition",
  data() {
    return {
      nicknames: this.random(variables.nicknames),
      quotes: this.random(quotesFile), 
      greetings: function() {
        if (now >= 18) return greetings.evening;
        if (now >= 15) return greetings.afternoon;
        if (now >= 11) return greetings.day;
        if (now >= 5) return greetings.morning;
        if (now >= 0) return greetings.night;
      },
      darkMode: function() {
        if (now >= 18) return true;
        if (now >= 15) return false;
        if (now >= 11) return false;
        if (now >= 5) return false;
        if (now >= 0) return true;
      }
    };
  },
  methods: {
    random: function(arr) {
      return arr[Math.floor(Math.random() * arr.length)];
    }
  }
};
</script>

<style lang="scss">
@import "~/assets/css/animation.scss";
@import "~/assets/css/background.scss";
@import "~/assets/css/main.scss";
</style>
