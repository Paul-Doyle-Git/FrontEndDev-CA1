<template>
  <div class="container">
    <div class="title">
      All Countries
    </div>
    <paginate name="countries" :list="countries" :per="6">
      <div class="row-Container marginLeft">
        <b-card-group>
          <CountryCard
            v-for="country in paginated('countries')"
            :key="country.ccn3"
            :country="country"
          />
        </b-card-group>
      </div>
    </paginate>

    <div class="row-Container">
      <paginate-links
        for="countries"
        class="linkCSS w-50"
        :simple="{
          prev: '← Back   ',
          next: 'Next →',
        }"
      ></paginate-links>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import CountryCard from "@/components/CountryCard";

export default {
  name: "AllCountries",
  components: {
    CountryCard,
  },
  data() {
    return {
      countries: [],
      paginate: ["countries"],
    };
  },
  mounted() {
    axios
      .get("https://restcountries.com/v3.1/all")
      .then((response) => {
        console.log(response);
        this.countries = response.data;
      })
      .catch((error) => console.log(error));
  },
};
</script>

<style scoped>
.container {
  display: flex;
  align-content: flex-start;
  flex-wrap: wrap;
}

.row-Container {
  margin-top: 20px;
  display: flex;
  justify-content: center;
  width: 100%;
  height: 100%;
}

.marginLeft {
  margin-left: 55px;
}

.linkCSS {
  list-style: none;
  display: flex;
  justify-content: space-evenly;
  font-weight: 700;
}
.title {
  margin-top: 20px;
  margin-bottom: 20px;
  font-size: 64px;
  font-weight: 700;
}
</style>
