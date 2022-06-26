<template>
  <div id="app">
    <div class="container">
      <div class="first-div">
        <input v-model="number" type="number" />
      </div>
      <div class="second-div">
        <select v-model="option">
          <option>isPrime</option>
          <option>isFibonacci</option>
        </select>
      </div>
      <div class="third-div">
        {{ result }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      number: 0,
      option: "isPrime",
      result: null,
    };
  },
  methods: {
    isPrime() {
      for (let i = 2; i < this.number; i++)
        if (this.number % i === 0) return false;
      return this.number > 1;
    },
    isSquare(x) {
      let s = parseInt(Math.sqrt(x));
      return s * s == x;
    },
    isFibonacci() {
      const n = this.number;
      return this.isSquare(5 * n * n + 4) || this.isSquare(5 * n * n - 4);
    },
  },
  watch: {
    number: {
      handler() {
        if (this.number) {
          if (this.number < 0) {
            this.number = 1;
          }
          this.number = Math.round(this.number);
          this.result = this[this.option]();
        }
      },
    },
    option: {
      handler() {
        if (this.number) {
          this.result = this[this.option]();
        }
      },
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
* {
  box-sizing: border-box;
}
body {
  margin: 0;
  padding: 0;
}
.container {
  height: 100vh;
  min-width: 600px;
  display: flex;
  border: 1px solid;
}
.first-div {
  height: 100%;
  min-width: 200px;
  border: 1px solid;
}
.second-div {
  height: 100%;
  flex-grow: 1;
  width: 100%;
  min-width: 100px;
  border: 1px solid;
}
.third-div {
  height: 100%;
  min-width: 300px;
  border: 1px solid;
}
</style>
