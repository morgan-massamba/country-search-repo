<template>
  <div class="country">
    <Navigation />
    <div class="container">
      <router-link to="/" class="back-btn">
        <i class="fas fa-arrow-left"></i>
        <span>Back</span>
      </router-link>

      <div class="wrapper">
        <div class="wrapper__image">
          <img :src="country.flag" alt="flag" />
        </div>

        <div class="wrapper__body">
          <h2 class="country-name">{{ country.name }}</h2>

          <div class="content">
            <div class="content-inner">
              <p><span>Native Name: </span>{{ country.nativeName }}</p>
              <p><span>Population: </span>{{ country.population }}</p>
              <p><span>Region: </span>{{ country.region }}</p>
              <p><span>Sub Region: </span>{{ country.subregion }}</p>
              <p><span>Capital: </span>{{ country.capital }}</p>
            </div>
          </div>

          <div class="bottom">
            <p>Border Countries:</p>
            <span v-for="country in country.borders" :key="country">{{
              country
            }}</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, onMounted } from 'vue';
import Navigation from '../components/Navigation.vue';
export default {
  components: { Navigation },
  name: 'Country',
  props: ['id'],
  setup(props) {
    const country = ref([]);

    onMounted(() => {
      fetchSingleData();
    });

    const fetchSingleData = async () => {
      const res = await fetch(
        `https://restcountries.eu/rest/v2/name/${props.id}?fullText=true`
      );
      const informations = await res.json();
      country.value = informations[0];
    };

    return { country };
  },
};
</script>

<style lang="scss" scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  list-style-type: none;
  font-family: 'Nunito Sans', sans-serif;
}
.container {
  background: hsl(0, 0%, 98%);
  width: 100%;
  padding: 100px 5%;
}
a {
  text-decoration: none;
}
.back-btn {
  padding: 10px 40px;
  cursor: pointer;
  outline: none;
  margin: 50px 0 60px;
  font-family: 'Nunito Sans', sans-serif;
  font-weight: 600;
  font-size: 1rem;
  display: inline-flex;
  color: #000000;
  justify-content: space-between;
  align-items: center;
  border: none;
  box-shadow: 0 0 5px rgba($color: #000000, $alpha: 0.2);
  background: white;
  border-radius: 5px;
  i {
    margin-right: 10px;
    font-family: 'Font Awesome 5 Free';
  }
}
.wrapper {
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
  align-items: center;

  &__image {
    width: 45%;
    img {
      display: block;
      width: 100%;
      object-fit: cover;
    }
  }
  &__body {
    width: 50%;
  }
  .content {
    display: flex;
    flex-wrap: wrap;
    margin-bottom: 30px;
    &-inner{
      width: 100%;
      p {
        margin-bottom: 10px;
      }
      span {
        font-weight: 600;
      }
    }
  }

  .bottom {
    display: flex;
    flex-wrap:wrap;
    align-items: center;
    p {
      font-weight: 600;
    }
    span {
      padding: 5px 10px;
      margin-left: 20px;
      box-shadow: 0 0 5px rgba($color: #000000, $alpha: 0.15);
    }
  }
}
    .country-name {
      font-weight: 900;
      font-size: 2rem;
      margin-bottom: 40px;
    }
@media screen and (max-width:768px) {
  .wrapper{
    &__image{
      width: 100%;
      margin-bottom: 30px;
    }
    &__body{
      width: 100%;
    }
  }
  .country-name{
    text-align: center;
    margin-bottom: 20px;
  }
  .wrapper .content{
    margin-bottom: 20px;
  }
  .back-btn{
    margin: 20px 0 30px;
  }
}
</style>
