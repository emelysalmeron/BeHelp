<script>
import languages from "../assets/jsondata/languages.json";
import cities from "../assets/jsondata/cities.json";
import skills from "../assets/jsondata/skills.json";

export default {
  data() {
    return {
      results: "",
      languageOptions: languages,
      cityOptions: cities,
      skillOptions: skills,
      filterLanguages: "",
      filterCities: "",
      filterSkills: "",
    };
  },
  methods: {
    async filterBtn() {
      try {
        if (
          this.filterSkills === "" ||
          this.filterLanguages === "" ||
          this.filterCities === "" ||
          this.filterSkills === null ||
          this.filterLanguages === null ||
          this.filterCities === null
        ) {
          alert("Please select one filter for each category");
          return;
        }
        const filter = {
          skills: this.filterSkills["name"],
          location: this.filterCities["city"],
          languages: this.filterLanguages["name"],
        };
        console.log(
          JSON.stringify({
            skills: filter.skills,
            location: filter.location,
            languages: filter.languages,
          })
        );

        const res = await fetch("http://localhost:5000/users/", {
          method: "POST",
          headers: {
            "Content-Type": "application/json",
          },
          body: JSON.stringify({
            skills: filter.skills,
            location: filter.location,
            languages: filter.languages,
          }),
        });
        const searchResult = await res.json();
        this.$emit("searchCompleted", searchResult);
        // this.results = searchResult[0].firstName;
        // console.log(this.results);
      } catch (error) {
        console.log(error);
      }
    },
  },
};
</script>

<template>
  <section class="search">
    <div class="search__background">
      <img
        v-if="$route.name === 'Home'"
        src="../assets/homepage-search.png"
        class="search__background-img"
      />
      <div
        v-else
        style="margin-top: 200px"
        class="search__background-img"
      ></div>
      <div class="search__background-decor">
        <h1 v-if="$route.name === 'Home'">FIND YOUR VOLUNTEER</h1>
        <h1 v-else>VOLUNTEERS WHO CAN HELP</h1>

        <div class="search__background-panel">
          <div class="search__dropdown">
            <div>
              <v-select
                class="style-chooser"
                v-model="filterSkills"
                :options="skillOptions"
                :placeholder="'Skill'"
                label="name"
              />
            </div>
          </div>
          <div class="search__dropdown">
            <div>
              <v-select
                class="style-chooser"
                v-model="filterCities"
                :options="cityOptions"
                :placeholder="'City'"
                label="city"
              />
            </div>
          </div>
          <div class="search__dropdown">
            <div>
              <v-select
                class="style-chooser"
                v-model="filterLanguages"
                :options="languageOptions"
                :placeholder="'Language'"
                label="name"
              />
            </div>
          </div>

          <button @click="filterBtn" class="search-btn">
            <img src="../assets/fas/search-solid.svg" class="search-icon" />
          </button>
          <span class="flare"></span>
        </div>
      </div>
    </div>
  </section>
</template>

<style lang="scss">
@import "../components/styles/abstract/_variables.scss";
@import "../components/styles/abstract/_base.scss";
@import "../components/styles/layout/_search.scss";
@import "../components/styles/layout/_dropdown.scss";
@import "vue-select/src/scss/vue-select.scss";
</style>
