<template>
  <form @submit.prevent="handleSubmit">
      <label>Email:</label>
      <input type="email" required v-model="email">

      <label>Password:</label>
      <input type="password" required v-model="password">
      <div v-if="passwordError" class="error">{{ passwordError }}</div>

      <label>Role</label>
      <select v-model="role">
          <option value="developer">Web Developer</option>
          <option value="designer">Web Designer</option>
      </select>

      <div class="terms">
          <input type="checkbox" required v-model="terms">
          <label > Accept terms and conditions</label>
      </div>

      <label >Skills:</label>
      <input type="text" v-model="tempSkills" @keyup="addskill">
      <div v-for="skill in skills" :key="skill" class="pill">
          <span @click="deleteskill (skill)">{{ skill }}</span>
      </div>

      <div class="submit">
          <button>Create an Account</button>
      </div>
  </form>

  <p>Email: {{ email }}</p>
    <p>Password: {{ password }}</p>
    <p>Role: {{ role }}</p>

</template>

<script>
export default {
    data() {
        return{
            email: '',
            password: '',
            role: '',
            terms:'false',
            tempSkills:'',
            skills: [],
            passwordError: ''
        }
    },
   methods: {
       addskill(e) {
           if (e.key === ',' && this.tempSkills !== ",") {
                let strToAdd = this.tempSkills.substring(0, this.tempSkills.length - 1);

               if (!this.skills.includes(strToAdd)){
                    this.skills.push(strToAdd)
               }
               this.tempSkills = ''
           }
       },
       deleteskill(skill) {
            this.skills = this.skills.filter(item => item != skill) 
       },
       handleSubmit() {
         //validate password
         this.passwordError = this.password.length > 5 ? '': 'password must be at least 6 chars long'
       }
   }
}
</script>
    
}
<style>
form {
    max-width: 420px;
    margin: 30px auto;
    background: white;
    text-align: left;
    padding: 40px;
    border-radius: 10px;
}

label {
    color: #aaa;
    display: inline-block;
    margin: 25px 0 15px;
    font-size: 0.8em;
    text-decoration: uppercase;
    letter-spacing: 1px;
    font-weight: bold;
}

input {
    display: block;
    padding: 10px 6px;
    width: 100%;
    box-sizing: border-box;
    border: none;
    border-bottom: 1px solid #ddd;
    color: #555;
}

select{
     width: 100%;
     border: none;
     border-bottom: 1px solid #ddd;
     color: #555;
}

input[type="checkbox"] {
    display: inline-block;
    width: 16px;
    margin: 0 10px 0 0;
    position: relative;
    top: 2px;
}
.pill {
    display: inline-block;
    margin: 20px 10px 0 0;
    padding: 6px 12px;
    background: #eee;
    font-size: 12px;
    letter-spacing: 1px;
    font-weight: bold;
    color: #777;
    cursor: pointer;
    border-radius: 20px;
}

button {
    background: #0b6dff;
    border: 0;
    padding: 12px 20px;
    margin-top: 20px;
    color: white;
    border-radius: 20px;
    font-size: 15px;
}

.submit {
    text-align: center;
}

.error {
    color: tomato;
}
</style>