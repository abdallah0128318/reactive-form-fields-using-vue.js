<template>
  <form @submit.prevent='handleSubmit'>
      <label>Email:</label><br>
      <input type="text" required v-model='email'><br><br>
       <label>password:</label><br>
      <input type="password" required v-model='password'><br>
      <div v-if="passwordError" class="error">
          {{passwordError}}
      </div>
      <br>
      <label>Role:</label><br>
      <select v-model="role">
          <option value="developer">web developer</option>
          <option value="designer">web designer</option>
      </select><br><br><br>
      <label>Skilss:</label><br>
      <input type="text" v-model='tempSkill' @keyup="addSkill"><br><br>
      <div v-for="skill in skills" :key='skill' @click='deleteSkill(skill)'>
          {{skill}}
      </div><br><br><br>
      <input type="checkbox" required v-model='terms'><label>accept terms</label><br><br>
      <button>Submit</button>
  </form>
  <p>Email: {{email}} </p>
  <p>password: {{password}} </p>
  <p>role: {{role}} </p>
  <p>termas accepted: {{terms}} </p>
</template>

<script>
export default {
    name: 'SignupForm',
    data(){
        return {
            email: '',
            password: '',
            passwordError:'',
            role: 'designer',
            terms: false,
            tempSkill: '',
            skills: []
        }
    },
    methods: {
        addSkill(e)
        {
            if(this.tempSkill && e.key=='Enter' && this.tempSkill !== ',')
            {
                if(!this.skills.includes(this.tempSkill))
                {
                    this.skills.push(this.tempSkill)
                }
                this.tempSkill = ''
            }
        },
        deleteSkill(skill)
        {
            this.skills = this.skills.filter((item)=>{
                return skill !== item
            })
        },
        handleSubmit()
        {
            // validate password
            this.passwordError = this.password < 5 ? 'password must be at least 5 chars' : ''



        }

    }

}
</script>

<style>
button 
{
    background-color: blueviolet;
    color: white;
    text-align: center;
    padding: 10px 20px;
    border: none;
    outline: none;
    cursor: pointer;
    border-radius: 10px;
}
.error 
{
    color: red;
}
</style>