<script>
import Search from "../components/Search.vue";
import Card from "../components/Card.vue";

export default {
  data() {
    return {
      volunteers: [],
    };
  },
  components: {
    Search,
    Card,
  },

  methods: {
    searchCompleted: function (results) {
      this.volunteers = results;
      console.log(results);
    },
  },
};
</script>

<template>
  <div>
    <div class="volunteers">
      <Search v-on:searchCompleted="searchCompleted" />
      <div class="volunteers__container">
        <div class="volunteers__searchresults">
          <div class="volunteers__searchresults-h1">Results:</div>
          <pre id="json">
          <!-- {{ this.results }} -->
          
        </pre>
          <div class="col-6">
            <div class="cards__columns">
              <Card
                v-for="volunteer in volunteers"
                v-bind:volunteer="volunteer"
              />
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
@import "../components/styles/abstract/_variables.scss";
@import "../components/styles/layout/_card.scss";

.cards__columns {
  justify-content: space-evenly;
  width: 100%;
  padding: 1em;
  display: flex;
  flex-direction: column;
  flex-flow: column wrap;
  align-self: center;
  margin: 1em;
  flex-wrap: wrap;
}

.cards__columns > .cards {
  flex: 1;
  justify-content: space-around;
  display: flex;
  flex-wrap: wrap;
  flex: 1 1 160px;
  margin: 0.6rem;
}

.cards {
  border-radius: 25px;
  border: 0.25rem solid #99c5e8;
  background: #f5f4ef;
  align-items: center;
  justify-content: center;
  display: flex;
}
.cards__picture {
  align-self: flex-start;
  border-radius: 25px;
  border: 5px solid #a00000;
}

.card__body {
  display: flex;
  align-items: center;
  justify-content: center;
}

.card__contact-btn {
  align-items: center;
  justify-content: center;
}

.geo__logo {
  justify-items: stretch;
}

.geo__text {
  color: #99c5e8;
}
</style>
