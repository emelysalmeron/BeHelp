<template>
  <div class="cards">
    <div class="cards__picture col-md-4">
      <img
        v-bind:src="volunteer.photoURL"
        class="img-fluid rounded-start"
        alt="volunteer-profile-picture"
      />
    </div>
    <div class="card__body">
      <h5 class="card__title">
        {{ volunteer.firstName }} {{ volunteer.lastName }}
      </h5>
      <p class="card__text">
        {{ volunteer.description }}
      </p>
      <div class="geo__text">
        <img
          class="geo__logo"
          src="../assets/logos/geo__logo.svg"
          alt="geo logo"
        />
        {{ volunteer.location[1] }}
      </div>
      <a class="card__contact-btn" style="color:red"
       href="#" role="button">CONTACT ME</a>
    </div>
  </div>
</template>

<script>
export default {
  name: "Card",
  props: ["volunteer"],
  components: {},
};
</script>

<style lang="scss">
@import "../components/styles/abstract/_variables.scss";
@import "../components/styles/layout/_card.scss";
</style>
