<template>
  <div class="home">
    <h1>Cohere Job Post Maker</h1>
    <form v-if="qindex < 4">
      <p>{{questions[qindex]}}</p>
      <div class="input-area">
        <div class="input-and-button">
          <input v-model="input" type="text"/>
          <button :disabled="qindex === 0 ? false : input.length < 20" @click.prevent="set(info[qindex].title)">Next</button>
        </div>
        <p class="counter" v-if="qindex !== 0">
          (<span :style="{color: input.length < 20 ? 'red' : 'green'}">{{input.length}}</span>/45)
          </p>
      </div>
    </form>
    <div class="job">
      <div class="title">
        <h3>{{jobTitle}}</h3>
        <p>({{employeeModel.title}})</p>
      </div>
      <p>
        <strong>Role Description:</strong>{{employeeModel.desc}}
      </p>
      <p>
        <strong>Cohere's Culture:</strong>{{employeeModel.culture}}
      </p>
      <p>
        <strong>Your Skills:</strong>{{employeeModel.skills}}
      </p>
    </div>
  </div>
</template>

<script>
import Vue from 'vue';

export default Vue.extend({
  name: 'Home',
  data() {
    return {
      resultWords: '',
      qindex: 0,
      jobTitle: '',
      info: [
        {
          title: 'title',
          tokens: 15
        },
        {
          title: 'desc',
          tokens: 30
        },
        {
          title: 'culture',
          tokens: 30
        },
        {
          title: 'skills',
          tokens: 20
        },
      ],
      questions: [
        'What type of role do you want to hire?',
        'Write a little bit about the role',
        'What was Cohere\'s culture like this week?',
        'What are some required skills?'
      ],
      communicate: 'What role do you want to hire?',
      longword: '',
      input: '',
      employeeModel: {
        'title': '',
        'desc': '',
        'culture': '',
        'skills': '',
      }
    }
  },
  created: async function () {
  },
  methods: {
    set(answer) {
      if (this.qindex === 0) this.jobTitle = this.input
      this.generate(this.input, answer, this.info[this.qindex].tokens)
      this.input = ''
      this.qindex++
    },
    generate: function (seed, answer, tokens) {
      this.$http.post('/.netlify/functions/generate',{
        "prompt": seed,
        "max_tokens": tokens,
        "temperature": 1,
        "k": 5,
        "p": 1
      }).then(response => {
        this.employeeModel[answer] = response.data.text
      })
    },
  }
});
</script>
<style scoped src="./home.styl" lang="stylus"></style>
