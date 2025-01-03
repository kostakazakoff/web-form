<template>
  <div class="container-full">
    <form @submit.prevent="handleSubmit">
      <label>Email:</label>
      <input type="email" required v-model="email" />

      <label>Password:</label>
      <input type="password" required v-model="password" />

      <label>Role:</label>
      <select v-model="role">
        <option value="developer">Web developer</option>
        <option value="designer">Web designer</option>
      </select>

      <label>Skills:</label>
      <input type="text" v-model="tempSkill" @keyup="addSkill" />

      <article class="pill-container">
        <p class="pill" v-for="skill in skills" :key="skill" @click="deleteSkill(skill)">
            {{ skill }}
        </p>
      </article>

      <div class="terms">
        <input type="checkbox" required v-model="terms" />
        <label>Accept terms and conditions</label>
      </div>

      <div class="btns-container">
        <button>Create an account</button>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      email: "",
      password: "",
      role: "developer",
      terms: false,
      tempSkill: "",
      skills: []
    };
  },
  methods: {
    addSkill(e) {
      const skill = e.target.value.replace(",", "").trim();
      if (e.key === "," && skill) {
        if (!this.skills.includes(skill)) {
          this.skills.push(skill);
        }
        this.tempSkill = "";
      }
    },
    deleteSkill(skill) {
        this.skills = this.skills.filter(s => s!== skill);
    },
    handleSubmit() {
        console.log("Data: ", this.email, this.password, this.role, this.skills.toString(), this.terms);
    }
  }
};
</script>

<style>
form {
  position: relative;
  max-width: 40vw;
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
.container-full {
  position: relative;
  min-height: 100vh;
  width: 100vw;
}
input,
select {
  background: white;
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
.pill-container {
  margin: 0;
  padding: 10px 0;
  display: flex;
  flex-wrap: wrap;
  align-content: flex-start;
  gap: 4px;
}
.pill-container .pill {
  margin: 0;
  padding: 4px 8px;
  background: #ddd;
  border-radius: 6px;
  cursor: pointer;
}
.btns-container {
  margin: 0;
  padding: 10px 0;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 4px;
}
button {
    cursor: pointer;
    background: blue;
    padding: 8px 16px;
    border: none;
    border-radius: 14px;
    color: white;
}
button:hover {
    background: rgb(66, 66, 252);
}
</style>