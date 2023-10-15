<template>
  <div>
     <div class="container-fluid bg_color">
        <div class="row">
            <div class="col">
                <form>
                    <input class="search_display" type="search" v-model="search" placeholder="Поиск">
                </form>
                <img src="@/assets/images/Line.png" />
            </div>
        </div>
        <Tags />
     </div>
     <div class="container">
        <div class="row">
           <div class="col">
              <div class="inline_display">
                <router-link to="/">
                   <IconsJustify class="sort_ver" />
                </router-link>
                <router-link to="/">
                  <IconsHeading class="sort_ver" />
                </router-link>
              </div>
           </div>
        </div>
     </div>
     <div class="container">
        <div class="row mb-5" v-if="searchImageFilter">
            <div 
                v-for="img in searchImageFilter"
                :key="img.id"
                class="col-4 card_block"
            >
            <router-link :to="'/photo/' + img.id">
                <div class="card">
                    <img :src="img.urls.regular" :width="img.width" class="card-img-top">
                </div>
            </router-link>
            </div>
        </div>
     </div> 
  </div>
</template>

<script>
import axios from 'axios';

export default {
    data() {
        return {
            images: [],
            search: ''
        }
    },
    computed: {
        searchImageFilter(){
            return this.images.filter(el => {
                return el.alt_description.includes(this.search);
            });
        }
    },
    async beforeMount(){
        const ClientId = "i9KK1kmO9x2ZHK2t6Mu35bbaQzqIdgtWKtzgwmUvNCA";
        const response = await axios.get('https://api.unsplash.com/photos/random', {
            params: { count: 20},
            headers: {
                Authorization: `Client-ID ${ClientId}`
            }
        })
        this.images = response.data;
    },
}
</script>

<style lang="scss" scoped>
.inline_display{
   text-align: center;
   margin-top: 3%;
   margin-bottom: 3%;
}
.sort_ver{
   margin-right: 3%;
   color: black;
}
.sort_ver:hover{
   color: #BDBDBD;
}
.search_display{
  border: none;
  margin: 0 0 0 0;
  font-size: 3em;
  color: white;
  width: 100%;
  background-color: black;
  text-align: center;
}
.search_display:focus{
  outline: 0; 
}
.bg_color{
  background-color: black;
}
</style>