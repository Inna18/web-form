<template>
    <form @submit.prevent="handleSubmit">
      <label>Email: </label>
      <input type="email" v-model="email" required>

      <label>Password: </label>
      <input type="password" v-model="password" required>
      <p class="password-error" v-if="passwordError">{{ passwordError }}</p>

      <label>Role: </label>
      <select v-model="role">
        <option value="developer">Web Developer</option>
        <option value="designer">Web Designer</option>
      </select>

      <div class="skills">
        <label>Skills: </label>
        <input type="text" v-model="tempSkills" @keyup.alt="addSkill">
        <div v-for="skill in skills" :key="skill" class="pill">
          <p @click="deleteSkill(skill)">{{ skill }}</p>
        </div>
      </div>

      <div class="terms">
        <input type="checkbox" v-model="terms">
        <label>Terms and Conditions</label>
        <p class="terms-error" v-if="termsError">{{ termsError }}</p>
      </div>

      <div class="btn-area">
        <button class="submit-btn">Submit</button>
      </div>
    </form>

  <p>Email: {{ email }}</p>
  <p>Password: {{ password }}</p>
  <p>Role: {{ role }}</p>
  <p>Agree to Terms: {{ terms }}</p>

</template>

<script>
export default {
  name: "SignupForm",
  data() {
    return {
      email: "",
      password: "",
      role: "developer",
      terms: false,
      tempSkills: "",
      skills: [],
      passwordError: "",
      termsError: ""
    }
  },
  methods: {
    addSkill(e) {
      if (e.key === ",") {
        if (!this.skills.includes(this.tempSkills)) {
          this.skills.push(this.tempSkills);
        }
        this.tempSkills = "";
      }
    },
    deleteSkill(skill) {
      // if (this.skills.includes(skill)) {
      //   let index = this.skills.indexOf(skill);
      //   this.skills.splice(index, 1);
      // }
      this.skills = this.skills.filter(item => {
        return skill !== item;
      });
    },
    handleSubmit() {
      this.passwordError = this.password > 5 ? "" : "Password must be at least 6 chars long";
      this.termsError = this.terms === true ? "" : "Check Terms and Conditions";

      if (!this.passwordError && this.terms === true) {
        console.log("email: ", this.email);
        console.log("password: ", this.password);
        console.log("roles: ", this.role);
        console.log("skills: ", this.skills);
      }
    }
  }
}
</script>

<style scoped>
  form {
    background: white;
    max-width: 420px;
    margin: 30px auto;
    padding: 40px;
    border-radius: 10px;
    text-align: left;
  }
  label {
    color: #aaa;
    display: inline-block;
    margin: 25px 0 15px;
    font-size: 0.6em;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: bold;
  }
  input, select {
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
  .btn-area {
    text-align: center;
  }
  .submit-btn {
    background: dodgerblue;
    margin-top: 10px;
    padding: 10px 20px;
    border-radius: 10px;
    border: none;
    text-transform: uppercase;
    color: white;
  }
  .password-error, .terms-error {
    color: firebrick;
    font-size: 0.6em;
  }
</style>
