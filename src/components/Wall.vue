<template>
  <div class="container">
    <header>
      <div class="searchInput">
        <i class="fas fa-search"></i>
        <input type="text" placeholder="Search for a country..." v-model="searchInput">
      </div>
      <select name="" id="" v-model="selectOption">
        <option value="">Filter by Region</option>
        <option value="Africa" selected>Africa</option>
        <option value="America">America</option>
        <option value="Asia">Asia</option>
        <option value="Europe">Europe</option>
        <option value="Oceania">Oceania</option>
      </select>
    </header>

    <main>

      <div class="wrapper-item" v-for="item in filteredWithRegion" :key="item.name">
        <router-link :to="'/country/'+item.name">
          <div class="wrapper-item__image">
            <img :src="item.flag" alt="flag">
          </div>

          <div class="wrapper-item__body">
            <h2>{{ item.name }}</h2>
            <p><span>Population:</span> {{ item.population}}</p>
            <p><span>Region:</span> {{ item.region }}</p>
            <p><span>Capital:</span> {{ item.capital }}</p>
          </div>
        </router-link>
      </div>

    </main>
  </div>
</template>

<script>
import {ref, onMounted, computed} from 'vue'
export default {
  name: 'Wall',
  setup(){

    const infos = ref([])
    const selectOption = ref('')
    const searchInput = ref('')

    const fetchData = async () => {
      const res = await fetch("https://restcountries.eu/rest/v2/all?fields=name;nativeName;population;region;subregion;capital;topLevelDomain;currencies;languages;borders;flag")
      const data = await res.json()
      infos.value = data
    }

    onMounted(() => {
      fetchData()
    })

    const filterByName = computed ( () => {
      return infos.value.filter(item => item.name.toLowerCase().includes(searchInput.value.toLowerCase()))
    })  	

    const filteredWithRegion =  computed( () => {
      return filterByName.value.filter(item => item.region.toLowerCase().includes(selectOption.value.toLowerCase()))
    })

    return {infos, selectOption,searchInput,fetchData, filterByName, filteredWithRegion}

  }
}
</script>


<style scoped lang="scss">
*{
  box-sizing: border-box;
}
.container{
  background: hsl(0, 0%, 98%);
  width: 100%;
  padding: 100px 5%;
}
header{
  margin-top: 30px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
  input{
    display: inline-block;
    outline: none;
    padding: 20px 0;
    border: none;
    width: 540px;
      
    font-size: 1.1rem;
  }
  select{
    width: 200px;
    display: inline-block;
    outline: none;
    padding: 20px;
    border: none;
    color: hsl(0, 0%, 52%);
    border-radius: 5px;
    font-family: "Nunito Sans", sans-serif;
    margin-bottom: 10px;
    font-size: 1rem;
    box-shadow: 0 0 5px rgba($color: #000000, $alpha: 0.1);
    option{
      font-family: "Nunito Sans", sans-serif;
      color: hsl(0, 0%, 52%);
      
    }
  }
}
.searchInput{
  width: 600px;
  display: flex;
  align-items: center;
  background: white;
  margin-bottom: 10px;
  border-radius: 5px;
  box-shadow: 0 0 5px rgba($color: #000000, $alpha: 0.1);
  i{
    width: 60px;
    font-size: 1.1rem;
    text-align: center;
    color: hsl(0, 0%, 52%);
    cursor: pointer;
  }
}
//section principale
main{
  margin-top: 30px;
  width: 100%;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
  align-items: center;
}

a{
  text-decoration: none;
}

.wrapper-item{
  width: 300px;
  margin-bottom:60px;
  height: 400px;
  border-radius: 5px;
  overflow: hidden;
  box-shadow: 0 0 5px rgba($color: #000000, $alpha: 0.15);
  &__image{
    width: 100%;
    height: 50%;
    img{
      width: 100%;
      height: 100%;
      object-fit: cover;
    }
  }
  &__body{
    padding: 30px 20px;
    color: black;
    h2{
      font-size: 1.3rem;
      text-overflow: ellipsis;
      overflow: hidden;
      white-space: nowrap;
    }
    p{
      margin-top: 14px;
      span{
        font-weight: 600;
      }
    }
  }
}
h4{
  font-weight: 600;
  font-size: 1.5rem;
  text-align: center;
  span{
    font-weight: 900;
    font-size: 1.4rem;
    color:gray;
  }
};
@media screen and (max-width:600px){
  header{
    input{
      width: 85%;
    }
    select{
      width: 100%;
    }
  }
  .searchInput{
    width: 100%;
    i{
      width: 15%;
    }
  }
  main{
    justify-content: center;
  }
}
</style>
