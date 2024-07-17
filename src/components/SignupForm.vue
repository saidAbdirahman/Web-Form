<template>
    <form>
      <label>Email:</label>
      <input type="email" v-model="email" required>
  
      <label>Password:</label>
      <input
        type="password"
        v-model="password"
        @input="evaluatePasswordStrength"
        required
      />
      <p class="password-strength" :class="strengthClass">{{ passwordStrength }}</p>
  
      <select v-model="role">
        <option value="developer">Web developer</option>
        <option value="designer">Web designer</option>
      </select>
  
      <div class="terms">
        <input type="checkbox" v-model="terms" required>
        <label>Accept terms and conditions</label>
      </div>
  
      <label>Skills</label>
      <input type="text" v-model="tempSkill" @keyup.ctrl="addSkill">
      <div v-for="skill in skills" :key="skill" class="pill">
        {{ skill }}
      </div>
    </form>
  
    <p>Email: {{ email }}</p>
    <p>Password: {{ password }}</p>
    <p>Role: {{ role }}</p>
    <p>Terms Accept: {{ terms }}</p>
  </template>
  
  <script>
  export default {
    data() {
      return {
        email: '',
        password: '',
        role: '',
        terms: false,
        tempSkill: '',
        skills: [],
            passwordStrength: '',
            strengthClass: '',
      };
    },
    methods: {
      evaluatePasswordStrength() {
        const length = this.password.length;
        const hasNumbers = /\d/.test(this.password);
        const hasLetters = /[a-zA-Z]/.test(this.password);
        const hasSpecialChars = /[!@#$%^&*(),.?":{}|<>]/.test(this.password);
  
        if (length === 0) {
          this.passwordStrength = '';
          this.strengthClass = '';
        } else if (length < 8 || !hasNumbers || !hasLetters || !hasSpecialChars) {
          this.passwordStrength = 'Weak';
          this.strengthClass = 'weak';
        } else if (length < 12) {
          this.passwordStrength = 'Medium';
          this.strengthClass = 'medium';
        } else {
          this.passwordStrength = 'Strong';
          this.strengthClass = 'strong';
        }
      },
      addSkill(e) {
        if (e.key === ',' && this.tempSkill) {
          if (!this.skills.includes(this.tempSkill)) {
            this.skills.push(this.tempSkill);
          }
          this.tempSkill = '';
        }
      },
    },
  };
  </script>
  
  <style scoped>
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
    font-size: 0.6em;
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
  input[type='checkbox'] {
    display: inline-block;
    width: 16px;
    margin: 0 10px 0 0;
    position: relative;
    top: 2px;
  }
  .password-strength {
    font-size: 0.75em;
    margin-top: 5px;
  }
  .weak {
    color: #e74c3c;
  }
  .medium {
    color: #f39c12;
  }
  .strong {
    color: #27ae60;
  }
  .pill {
    display: inline-block;
    background: #e0e0e0;
    padding: 5px 10px;
    margin: 5px;
    border-radius: 20px;
  }
  </style>
  