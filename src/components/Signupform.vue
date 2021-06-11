<template>
  <form @submit.prevent="handlesubmit">
    <label>Email : </label>
    <input type="email" required v-model="email">

    <label>Password : </label>
    <input type="password" required v-model="password">
    <div v-if="passworderror" class="error"> {{ passworderror }} </div>

    <label>Role : </label>
    <select v-model="role">
      <option value="designer">Web Designer</option>
      <option value="developer">Web Developer</option>
    </select>

      <label>Skill: </label>
      <input type="text" v-model="termskill" @keydown="addskill">
    <div  v-for="skill in skills" :key="skill" class="pill">
    <span @click="deleteskill(skill) "> {{ skill }}</span>
    </div>

    <div class="terms" >
      <input type="checkbox" v-model="term" required>
      <label>Accept All Terms & Conditions</label>
    </div>

    <div class="submit">
      <button>Create an Account</button>
    </div>

  </form>

  <p>Email : {{ email }}</p>
  <p>Password : {{ password }}</p>
  <p>Role : {{ role }}</p>
  <p>Accept Condition : {{ term }}</p>



</template>

<script>
export default {
  data(){
    return{
      email: '',
      password: '',
      role: 'designer',
      term: false,
     termskill: '',
      skills: [],
      passworderror: ' ',
    }
  },
  methods: {
    addskill(e){
      if (e.key === ',' && this.termskill){
        if (!this.skills.includes(this.termskill)){
          this.skills.push(this.termskill)
        }
        this.termskill = ' '


      }
    },
    deleteskill(skill){
      this.skills = this.skills.filter((item) => {
        return skill !== item
      })
    },
    handlesubmit(){
      this.passworderror = this.password.length > 5 ?
          ' ' &&
          confirm("From Submitted")
          : 'password error : password must be more then 6 digit'

console.log("Email : " + this.email + " Password : " +this.password + " Position : " + this.role + " Skills : " + this.skills )    }
  }
}
</script>
<style>
form{
  max-width: 420px;
  margin: 30px auto;
  background: white;
  text-align: left;
  padding: 40px;
  border-radius: 10px;
}
label{
  color: #aaa;
  display: inline-block;
  margin: 25px 0 15px;
  font-size: 0.6em;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: bold;
}
input,select{
  display: block;
  padding: 10px 6px;
  width: 100%;
  box-sizing: border-box;
  border: none;
  border-bottom: 1px solid #ddd;
  color: #555;
}
input[type="checkbox"]{
  display: inline-block;
  width: 16px;
  margin: 0 10px 0 0;
  position: relative;
  cursor: pointer;
  top: 2px;
}
.pill{
  display: inline-block;
  margin: 20px 10px 0 0;
  padding: 6px 12px;
  background-color: #eee;
  border-radius: 20px;
  color: #777;
  font-size: 12px;
  letter-spacing: 1px;
  font-weight: bold;
  cursor: pointer;
}
button{
  background: #0b6dff;
  border: 0;
  padding: 10px 20px;
  margin-top: 20px;
  color: white;
  border-radius: 20px;
  cursor: pointer;
}
.submit{
  text-align: center;
}
.error{
  color: #ff0062;
  margin-top: 10px;
  font-size: 0.8em;
  font-weight: bold;
}
.pass_error{
  border: 1px solid red;
}
</style>
