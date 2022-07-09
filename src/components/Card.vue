<template>
  <div class="container">
    <div
      class="card border border-1 border-dark"
      style="width: 21.5rem"
      v-if="data.data.stade"
    >
      <div class="card-body">
        <h5 class="card-title">{{ data.data.title }}</h5>
        <p class="card-text">
          {{ data.data.body }}
        </p>
        <div class="row">
          <router-link :to="`/edit/${data.id}`" class="col-6 btn btn-success"
            ><i class="bx bxs-edit-alt"></i
          ></router-link>

          <button @click.prevent="dele()" class="col-6 btn btn-danger">
            <i class="bx bxs-trash-alt"></i>
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      x: true,
    };
  },
  props: {
    data: Object,
  },

  methods: {
    async dele() {
      const user = JSON.parse(localStorage.getItem("user"));
      const xr = this.data.id;
      const del = await fetch(
        `https://tasks-bac0f-default-rtdb.firebaseio.com/projects/${user.localId}/${xr}.json?auth=${user.idToken}`,
        {
          method: "DELETE",
        }
      );

      const data = await del.json();
      this.data.data.stade = data;
    },
  },
};
</script>

<style scoped>
.container {
}
</style>
