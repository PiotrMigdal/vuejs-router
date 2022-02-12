<template>
  <section>
    <input type="text" :value="experience.name" />
    <div class="experience-details">
      <img :src="require(`@/assets/${experience.image}`)" />
      <input type="text" :value="experience.description" />
      <input type="text" v-model="newDestinationName" />
    </div>
    <router-link
      :to="{
        name: 'DestinationDetails',
        params: {
          newDestinationName: newDestinationName,
          slug: slug
        }
      }"
    >
      <span class="card__text">
        Save
      </span>
    </router-link>
  </section>
</template>
<script>
import store from "@/store.js";
export default {
  data() {
    return {
      newDestinationName: "Poland"
    };
  },
  props: {
    slug: {
      type: String,
      required: true
    },
    experienceSlug: {
      type: String,
      required: true
    }
  },
  computed: {
    destination() {
      return store.destinations.find(
        destination => destination.slug === this.slug
      );
    },
    experience() {
      return this.destination.experiences.find(
        experience => experience.slug === this.experienceSlug
      );
    }
  }
};
</script>

<style scoped>
img {
  max-width: 600px;
  height: auto;
  width: 100%;
  max-height: 400px;
}
.experience-details {
  display: flex;
  justify-content: space-between;
  padding: 40px 0;
}
p {
  margin: 0 40px;
  font-size: 20px;
  text-align: left;
}
</style>
