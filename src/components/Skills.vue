<template>
  <div class="hello">
    <div class="holder">
      <form @submit.prevent="addSkill">
        <input type="text" placeholder="Enter your skills" v-model="skill" v-validate="'min: 5'" name="skill">
        <p class="alert" v-if="errors.has('skill')">{{ errors.first('skill') }}</p>
      </form>
      <ul>
        <li v-for="(data, index) in skills" :key="index">{{ data.skill }}</li>
        <p v-if="skills.length >= 2">you have more than 2 skills</p>
        <p v-else>You have lessthan 2 skills</p>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Skills',
  data() {
    return {
      skill: '',
      skills: [
        { skill: "vue.js"},
        { skill: "Ruby on Rails"}
      ]
    }
  },
  methods: {
    addSkill() {
      this.$validator.validateAll().then((result) => {
        if(result){
          this.skills.push({skill: this.skill})
          this.skill = '';
        } else {
          console.log('Not Valid');
        } 
      })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

input {
  width: calc(100% - 40px);
  border: 0;
  padding: 20px;
  font-size: 1.3em;
  background-color: #323333;
  color: #687F7F
}

.alert {
  background: #fdf2c3;
  font-weight: bold;
  display: inline-block;
  padding: 5px;
  /* margin-top: -20px; */
}
</style>
