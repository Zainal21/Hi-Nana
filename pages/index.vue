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
        :strings="[greetings() + ', ' + nicknames + '! ^5000', 'I always wanted to tell you... ^2500', 'Nevermind! >///<', `I just wanna say something. I Love U. That's all`]"
        :backDelay="500"
        :typeSpeed="100"
        :backSpeed="20"
        :contentType="'null'"
      >
        <h1 class="typing"></h1>
      </vue-typed-js>

      <!-- Quotes -->
      <h1 class="quotes quotes-main"><strong>{{ quotes.quotes }}</strong></h1>
      <h3 class="quotes author">Created ♥  <a href="https://github.com/Zainal21">Muhamad Zainal Arifin</a></h3>
    </div>
  </div>
</template>

<script>
import quotesFile from "~/assets/quotes.js";
import variables from "~/assets/variables.js";

// Define greetings
const { greetings } = variables;

// Get time
const now = new Date().getHours();

// Client-side rendering
if (process.browser) {
  function random(arr) {
    return arr[Math.floor(Math.random() * arr.length)];
  }

  // Window on ready (server has rendered everything)
  window.onNuxtReady(app => {
    // Add event for click
    document.addEventListener("click", function(ev) {
      // Get coordinates where user clicks (X & Y)
      const x = ev.clientX;
      const y = ev.clientY;

      // Make a new element
      let el = document.createElement("div");

      // Fill with ♥
      el.innerHTML = `<h1>${random(["♥", "♥♥", "♥♥♥"])}</h1>`;

      // Add "popup" class
      el.classList.add("popup");

      // Define the position based on where user's clicked
      el.style.left = `${x}px`;
      el.style.top = `${y}px`;

      // Render it (show it to user)
      document.body.appendChild(el);

      // Set timeout before deletes after 3 secs it to reduce lags
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
      // prettier-ignore
      nicknames: this.random(variables.nicknames), // random the nicknames (from variables.js)
      quotes: this.random(quotesFile), // random the quotes (from variables.js)
      greetings: function() {
        // If right now is equals to or greater than 18 (6pm), show evening greeting
        if (now >= 18) return greetings.evening;

        // If right now is equals to or greater than 15 (3pm), show afternoon greeting
        if (now >= 15) return greetings.afternoon;

        // If right now is equals to or greater than 11 (11am), show day greeting
        if (now >= 11) return greetings.day;

        // If right now is equals to or greater than 5 (5am), show morning greeting
        if (now >= 5) return greetings.morning;

        // If right now is equals to or greater than 0 (12am), show sleep greeting
        if (now >= 0) return greetings.night;
      },
      darkMode: function() {
        // If right now is equals to or greater than 18 (6pm), turn on darkmode
        if (now >= 18) return true;

        // If right now is equals to or greater than 15 (3pm), turn on daymode
        if (now >= 15) return false;

        // If right now is equals to or greater than 11 (11am), turn on daymode
        if (now >= 11) return false;

        // If right now is equals to or greater than 5 (5am), turn on daymode
        if (now >= 5) return false;

        // If right now is equals to or greater than 0 (12am), turn on darkmode
        if (now >= 0) return true;
      }
    };
  },
  methods: {
    /* server side methods */
    // Randomize array element
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
