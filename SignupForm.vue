<template>
  <form @submit.prevent="handelSubmit">
    <label for="">Email</label>
    <input type="email" required v-model="email" />
    <label for="">password</label>
    <input type="password" required v-model="password" />
    <div v-if="passwordError" class="error">{{passwordError}}</div>

    <label>Role :</label>
    <select v-model="role">
      <option value="developer">Web Developer</option>
      <option value="designer">Web Designer</option>
    </select>

    <label>Skills:</label>
    <input type="text" v-model="tempSkill" @keyup="addSkill" />
    <div v-for="skill in skills" :key="skill" class="pill">
      <span @click="deleteHandler(skill)">{{ skill }}</span>
    </div>

    <div class="terms">
      <input type="checkbox" v-model="terms" required />
      <label>Accept terms and conditions</label>
    </div>

    <div class="submit">
      <button>create an account</button>
    </div>

    <!-- <div>
        <input type="checkbox" value="saeed" v-model="names">
        <label>saeed</label>
    </div>
    <div>
        <input type="checkbox" value="medi" v-model="names">
        <label>medi</label>
    </div>
    <div>
        <input type="checkbox" value="saeed" v-model="names">
        <label>erf</label>
    </div> -->
  </form>

  <!-- <p>emial : {{ email }}</p>
  <p>password : {{ password }}</p>
  <p>Role : {{ role }}</p>
  <p>Terms : {{ terms  }}</p>
  <p>names: {{ names }}</p> -->
</template>

<script>
export default {
  data() {
    return {
      email: "",
      password: "",
      role: "designer",
      terms: false,
      names: [],
      tempSkill: "",
      skills: [],
      passwordError : ''
    };
  },
  methods: {
    addSkill(e) {
      if (e.key === "," && this.tempSkill) {
        if (!this.skills.includes(this.tempSkill)) {
          this.skills.push(this.tempSkill);
        }
        this.tempSkill = "";
      }
    },
    deleteHandler(skill) {
      // console.log(skill)
      this.skills = this.skills.filter((item) => {
        return skill !== item;
      });
    },
    handelSubmit(){
        this.passwordError = this.password.length > 5 ? "" : 'Password must be at least 6 chars long'
        if(!this.passwordError){
            console.log('email :', this.email)
            console.log('password :', this.password)
            console.log('role :', this.role)
            console.log('skills :', this.skills)
            console.log('term accepted:', this.term === false ? "didnt Accept" : "Accepted")
        }
    }
  },
};
</script>













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
  font-size: 0.6rem;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: bold;
}
input,
select {
  display: block;
  padding: 10px 6px;
  width: 100%;
  box-sizing: border-box;
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
  border-radius: 20px;
  font-size: 12px;
  letter-spacing: 1px;
  font-weight: bold;
  color: #777;
  cursor: pointer;
}
button {
  background: #0b6dff;
  border: 0;
  padding: 10px 20px;
  margin-top: 20px;
  color: white;
  border-radius: 20px;
}
.submit {
  text-align: center;
}
.error{
    color: red;
    margin-top: 10px;
    font-size: 0.8em;
    font-weight: bold;
}
</style>  