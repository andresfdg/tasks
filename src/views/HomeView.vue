<template>
  <div class="container mt-3rem">
    <div class="login">
      <h1 class="text-center">Welcome!</h1>

      <form @submit.prevent="login()" class="needs-validation">
        <div class="form-group was-validated">
          <label class="form-label" for="email">Email address</label>
          <input
            class="form-control"
            type="email"
            id="email"
            required
            v-model="email"
          />
          <div class="invalid-feedback">Please enter your email address</div>
        </div>
        <div class="form-group was-validated">
          <label class="form-label" for="password">Password</label>
          <input
            class="form-control"
            type="password"
            id="password"
            required
            v-model="pass"
          />
          <div class="invalid-feedback">Please enter your password</div>
        </div>

        <input class="btn btn-success w-100" type="submit" value="SIGN IN" />
      </form>
    </div>
  </div>
</template>

<script>
import router from "@/router";
export default {
  data() {
    return {
      email: "",
      pass: "",
    };
  },

  methods: {
    async login() {
      if (this.email != "" && this.pass.length > 6) {
        const API_KEY = "AIzaSyCsAxH7fMsv7qvU3EZhktpWg2nr8s4FMlo";
        const res = await fetch(
          `https://identitytoolkit.googleapis.com/v1/accounts:signInWithPassword?key=${API_KEY}`,
          {
            method: "POST",
            body: JSON.stringify({
              email: this.email,
              password: this.pass,
              returnSecureToken: true,
            }),
          }
        );
        const data = await res.json();
        console.log(data);
        localStorage.setItem("user", JSON.stringify(data));
        router.push("/projects");
      } else {
        return console.log("bad");
      }
    },
  },
};
</script>

<style scoped>
body {
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  background: #0d6efd;
}

.login {
  width: 360px;
  height: min-content;
  padding: 20px;
  border-radius: 12px;
  background: #ffffff;
}

.login h1 {
  font-size: 36px;
  margin-bottom: 25px;
}

.login form {
  font-size: 20px;
}

.login form .form-group {
  margin-bottom: 12px;
}

.login form input[type="submit"] {
  font-size: 20px;
  margin-top: 15px;
}

.container {
  display: flex;
  justify-content: center;
  margin-top: 3rem;
}
.login {
}
</style>
