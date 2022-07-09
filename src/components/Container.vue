<template>
  <div class="container">
    <h2>Projects</h2>
    <router-link to="/create" class="btn btn-primary"
      ><i class="bx bxs-edit-alt"></i>+</router-link
    >
    <div class="row">
      <div
        v-for="(project, i) in projects"
        :key="i"
        class="col-lg-4 col-md-6 mt-3"
      >
        <Card :data="project" />
      </div>
    </div>
  </div>
</template>

<script>
import Card from "./Card.vue";
export default {
  components: { Card },

  data() {
    return {
      projects: [],
    };
  },

  mounted() {
    this.getprojects();
  },
  created() {
    this.opp();
  },

  methods: {
    async getprojects() {
      const user = JSON.parse(localStorage.getItem("user"));
      const res = await fetch(
        `https://tasks-bac0f-default-rtdb.firebaseio.com/projects/${user.localId}.json?auth=${user.idToken}`
      );
      const data = await res.json();

      for (let i in data) {
        this.projects.push({
          id: i,
          data: data[i],
        });
      }
    },

    opp() {},
  },
};
</script>

<style scoped>
.container {
  text-align: center;
}
</style>
