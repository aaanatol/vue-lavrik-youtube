<template>
  <div class="container">
    <button class="btn" 
						v-on:click="showH2 = !showH2"> 
			{{ btnText }} 
		</button>

		<br>

		<transition name="slide">
			<h2 v-show="showH2">Hello, {{ name }} </h2>
    </transition>

    <hr>
    
    <app-progress v-bind:val="sum" v-bind:max="maxNumbers * 5"> </app-progress>

		<button class="btn red" 
            v-on:click="addNumber"
            v-bind:disabled="done"> 
			add number 
    </button>
    
    <app-progress v-bind:val="numbers.length" v-bind:max="maxNumbers"> </app-progress>

		<ul class="collection">
			<li class="collection-item"
					v-for="number in numbers"
          v-bind:key="number * Math.random()">
				{{ number }}	
			</li>
		</ul>

		<h2> Your profit: {{ sum }} </h2>
  </div>
</template>

<script>
  import Progress from './Progress.vue';

  export default {
    data() {
      return {
        showH2: true,
				name: 'anatol',
				title: "ttttile",
				numbers: [2],
        maxNumbers: 10,
      }
    },

    methods: {
      addNumber() {
        if (!this.done) {
          let rndm = Math.floor(Math.random() * 11) - 5;
          this.numbers.push(rndm);
        }
      }
    },

    computed: {
      sum() {
        console.log('1');
        let sum = 0;

        for (let i = 0; i < this.numbers.length; i++) {
          sum += this.numbers[i];
        }

        return sum;
      },

      btnText() {
        return this.showH2 ? 'Hide' : 'Show';
      },

      done() {
        return this.numbers.length >= this.maxNumbers;
      }
    },

    components: {
      AppProgress: Progress
    }
  }
</script>

<style scope>
  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }

  .container {
    margin: 0 auto;
    max-width: 500px;
  }

  h1,
  h2,
  h3 {
    margin: 10px 0;
  }

  #app {
    margin: 30px auto;
    max-width: 700px;
  }

  .slide-enter {
    opacity: 0;
  }

  .slide-enter-active {
    transition: opacity 0.5s;
  }

  .slide-leave-active {
    transition: opacity 0.5s;
  }

  .slide-leave-to {
    opacity: 0;
  }
</style>