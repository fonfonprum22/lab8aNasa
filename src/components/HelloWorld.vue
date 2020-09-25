<template>
  <v-app>
    <v-row justify="center">
      <v-col cols="12" sm="6">
        <h1>MARS</h1>
        <v-text-field v-model="search" solo label="Search ID" clearable />
      </v-col>
    </v-row>

    <v-row justify="center">
      <v-col v-if="isloading">
        <v-row justify="center">
          <v-progress-circular
            indeterminate
            color="primary"
          ></v-progress-circular>
        </v-row>
      </v-col>
      <v-col v-else>
        <div v-if="searchmarsInput">
          <div v-if="searchmars != undefiled">
            <v-card class="mx-auto" max-width="344">
              <v-img
                class="white--text align-end"
                height="200px"
                v-bind:src="searchmars.img_src"
              />
              <v-card-title>{{ searchmars.camera.full_name }}</v-card-title>
              <v-card-text>ID : {{ searchmars.id }}</v-card-text>
            </v-card>
          </div>
        </div>
        <v-row v-else>
          <v-col v-for="item in mars" v-bind:key="item.id">
          <v-card class="mx-auto" max-width="344">
            <v-img
              class="white--text align-end"
              height="200px"
              v-bind:src="item.img_src"
            />
            <v-card-title>{{ item.camera.full_name }}</v-card-title>
            <v-card-text>ID : {{ item.id }}</v-card-text>
          </v-card>
          </v-col>
        </v-row>
      </v-col>
    </v-row>
  </v-app>
</template>

<script>
import Axios from "axios";
export default {
  data: () => ({
    search: "",
    mars: [],
    searchmars: {
      camera: { full_name: "" },
      img_src: "",
      id: "",
    },
    searchmarsInput: false,
    isloading: false,
  }),
  methods: {
    fetchMarsData() {
      this.isloading = true;
      Axios.get(
        "https://api.nasa.gov/mars-photos/api/v1/rovers/curiosity/photos?sol=1000&api_key=p1v9iusZJSsWsj5taNVjJIfAGOg9mdzezScnD7G1&fbclid=IwAR2ELljNBooebWE-Wxr09YjVnqZKCSLCjn8bAYPTW-DkUWY0pwF8BHo9SJg"
      ).then((res) => {
        this.mars = res.data.photos;
        this.isloading = false;
      });
    },
    searchData() {
      this.searchmars = this.mars.find((res) => 
      res.id === Number(this.search));
    },
  },
  created() {
    this.fetchMarsData();
  },
  updated() {
    if (this.search !== " " && this.search !== "") {
      this.searchmarsInput = true;
      this.searchData();
    } else {
      this.searchmarsInput = false;
    }
  },
};
</script>
