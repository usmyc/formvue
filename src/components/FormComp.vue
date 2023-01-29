<template>
  <div>
    <form @submit.prevent="handleSubmit">
      <label> Email: </label>
      <input type="email" required v-model="email" />
      <label> Pass: </label>
      <input type="password" required v-model="password" />
      <label for="Role"></label>
      <select v-model="role">
        <option value="Admin">Admin</option>
        <option value="User">User</option>
      </select>
      <label>Social:</label>
      <input type="text" v-model="tempSocial" @keypress="addSocial" />
      <ul>
        <li
          v-for="social in socials"
          :key="social"
          @click="deleteItem(social)"
          class="pill"
        >
          {{ social }}
        </li>
      </ul>
      <div>
        <input type="checkbox" v-model="accept" />
        <label>Accept it!</label>
      </div>
      <button type="submit" class="submit">Submit</button>
    </form>
    <div class="form-table">
      <h2>Form Data</h2>
      <div class="form-table-in">
        <p>{{ email }}</p>
        <p>{{ password }}</p>
        <p>{{ role }}</p>
        <p>{{ accept }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      email: "",
      password: "",
      role: "",
      accept: false,
      tempSocial: "",
      socials: [],
    };
  },
  methods: {
    handleSubmit() {
      if (!this.accept) {
        alert("You must accept the terms and conditions");
        return;
      }
      console.log(this.email, this.password, this.role, this.socials);
    },

    addSocial(e) {
      if (e.key === ",") {
        if (this.socials.includes(this.tempSocial)) {
          alert("Social already exists");
          this.tempSocial = "";
          return;
        }
        this.socials.push(this.tempSocial);
        this.tempSocial = "";
      }
    },
    deleteItem(social) {
      this.socials = this.socials.filter((item) => item !== social);
    },
  },
};
</script>

<style scoped>
form {
  display: flex;
  flex-direction: column;
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
input[type="checkbox"] {
  display: inline-block;
  width: auto;
  margin: 0 10px 0 0;
  position: relative;
  top: 2px;
}
li {
  list-style: none;
}
.form-table {
  display: flex;
  gap: 50px;
  position: sticky;
  max-width: 420px;
  margin: 30px auto;
  background: white;
  padding: 40px;
  border-radius: 10px;
}
.form-table-in {
  display: flex;
  flex-direction: column;
  gap: 10px;
  align-items: center;
  justify-items: center;
  margin: 10px;
  padding: 10px;
  border-left: 1px solid rgb(0, 0, 0);
}
.pill {
  display: inline-block;
  margin: 20px 10px 0 0;
  padding: 6px 12px;
  background: #eee;
  border: 1px solid rgb(0, 0, 0);
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
</style>
