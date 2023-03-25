<script>
import StopWatch from "@/components/Stop-Watch.vue";

export default {
  components: {StopWatch},
  data() {
    return {
      items: 4,
    }
  },
  methods:{

  }

};

</script>

<template>
  <div class="app">
    <div class="container">

      <div class="stopwatch-page">
        <stop-watch
            v-for="item in items" :key="item"></stop-watch>
        <div class="stopwatch-page-item add-timer-btn" @click="items++">
          <button class="btn">
            <svg width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
              <rect x="8.5" width="3" height="20" fill="#9E9E9E"/>
              <rect y="11.5" width="3" height="20" transform="rotate(-90 0 11.5)" fill="#9E9E9E"/>
            </svg>
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<style lang="scss">

@import "assets/fonts/GothamPro/stylesheet.css";
@import "assets/variables";


* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.app {
  min-height: 100vh;
  min-width: 320px;
  background: #353638;
  color: $main-gray;
  font-family: "Gotham Pro";
  font-size: 1.375rem;
}

.container {
  padding: 0 3rem;
  margin: 0 auto;
}

.btn {
  background: none;
  border: none;
  outline: none;
  cursor: pointer;
}

.stopwatch-page {
  padding: 4.5rem 0;
  display: grid;
  gap: 2.8rem;

  &-item {
    background: #696969;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 120px;
    width: 225px;
    margin: 0 auto;
    text-align: center;
    flex-direction: column;
  }
}

.add-timer-btn {
  cursor: pointer;

  & svg {
    & path, & rect {
      transition: $tr;
    }
  }

  &:hover {
    & svg {
      & path, & rect {
        fill: white;
      }
    }
  }
}

@media (min-width: $md) {

  .container {
    max-width: 768px;
  }

  .stopwatch-page {
    grid-template-columns: 1fr 1fr;
    column-gap: 3.1rem;

    &-item {
      margin: 0;

      &:nth-child(odd) {
        justify-self: end;
      }
    }
  }
}

@media (min-width: $lg) {

  .container {
    max-width: 900px;
  }

  .stopwatch-page {
    grid-template-columns: 1fr 1fr 1fr;

    &-item {
      margin: 0;

      &:nth-child(odd) {
        justify-self: inherit;
      }
    }
  }
}

</style>
