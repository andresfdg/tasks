<template>
  <div class="container mt-1">
    <div class="come">
      <router-link to="/projects" class="btn btn-warning"
        ><i class="bx bx-arrow-back"></i
      ></router-link>
    </div>

    <form @submit.prevent="postproject()">
      <div class="mb-3">
        <label for="exampleFormControlInput1" class="form-label"
          ><h2>Title</h2></label
        >
        <input
          class="form-control"
          id="exampleFormControlInput1"
          placeholder="create yout title"
          v-model="project.title"
        />
      </div>
      <div class="mb-3">
        <label for="exampleFormControlTextarea1" class="form-label"
          ><h2>Body</h2></label
        >
        <textarea
          class="form-control"
          id="exampleFormControlTextarea1"
          rows="3"
          v-model="project.body"
        ></textarea>
      </div>
      <div class="x">
        <button
          @click="window.history.back()"
          type="submit"
          class="btn btn-primary"
        >
          <i class="bx bxs-send"></i>
        </button>
        <div class="m">
          <button @click.prevent="tmet()" class="btn btn-success">
            <i class="bx bxs-calculator"></i>
          </button>
          <button @click.prevent="tnet()" class="btn btn-danger">
            <i class="bx bxs-calculator"></i>
          </button>
        </div>
      </div>
    </form>
    <Calcu v-if="stade" />
  </div>
</template>

<script>
import Calcu from "@/components/Calcu.vue";
export default {
  data() {
    return {
      project: {
        title: "",
        body: "",
      },
      stade: false,
    };
  },
  mounted() {
    this.getproject();
  },
  methods: {
    tmet() {
      this.stade = true;
    },
    tnet() {
      this.stade = false;
    },
    async getproject() {
      const user = JSON.parse(localStorage.getItem("user"));
      const rr = this.$route.params.id;
      const get = await fetch(
        `https://tasks-bac0f-default-rtdb.firebaseio.com/projects/${user.localId}/${rr}.json?auth=${user.idToken}`
      );
      const data = await get.json();
      this.project = data;
    },
    async postproject() {
      const user = JSON.parse(localStorage.getItem("user"));
      const xr = this.$route.params.id;
      const post = await fetch(
        `https://tasks-bac0f-default-rtdb.firebaseio.com/projects/${user.localId}/${xr}.json?auth=${user.idToken}`,
        {
          method: "PATCH",
          body: JSON.stringify(this.project),
        }
      );
      window.history.back();
    },
  },
  components: { Calcu },
};
</script>

<style scoped>
.x {
  text-align: center;
}

.come {
  text-align: right;
}
.m {
  text-align: right;
}
</style>
