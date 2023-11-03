<script>
import axios from "axios";

export default {
  name: "HomePage",
  data() {
    return {
      doctors: [],
      typologies: []
    };
  },
  mounted() {
    this.getDoctors();
    this.getTypology();
  },
  methods: {

    getTypology() {

      axios.get("http://localhost:8000/api/typologies", {
      }).then((resp) => {
        this.typologies = resp.data.result;
      })
        .catch((error) => {
          console.error(error);
        });;
    },

    getDoctors() {
      axios
        .get("http://localhost:8000/api/doctors")
        .then((resp) => {
          this.doctors = resp.data.result;
        })
        .catch((error) => {
          console.error(error);
        });
    },
  },
};
</script>

<template>
  <div class="container text-center my-4">
    <h1>Home Page</h1>
    <div class="row row-cols-3">
      <div class="col" v-for="doctor in doctors" :key="doctor.id">
        <div class="card">
          <img :src="doctor.photo" class="card-img-top" alt="..." />
          <div class="card-body">
            <h5 class="card-title">{{ doctor.user.name }}</h5>
            <p class="card-text">
              {{ doctor.description }}
            </p>
          </div>
          <ul class="list-group list-group-flush">
            <li class="list-group-item">{{ doctor.user.email }}</li>
            <li class="list-group-item">{{ doctor.address }}</li>
            <div v-for="typology in typologies" :key="typology.id">
              <li class="list-group-item">asdad{{ typology.name }}</li>
            </div>

          </ul>
          <div class="card-body">
            <a href="#" class="card-link">Card link</a>
            <a href="#" class="card-link">Another link</a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped></style>
