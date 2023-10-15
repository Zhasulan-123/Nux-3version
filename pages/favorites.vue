<template>
 <div>
  <div class="container-fluid">
    <div class="row">
        <div class="col text-center mt-5">
            <h2>Избранное</h2>
        </div>
    </div>
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
        <div class="row mb-5">
            <div 
                v-for="img in images"
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
    async beforeMount(){
        const ClientId = "i9KK1kmO9x2ZHK2t6Mu35bbaQzqIdgtWKtzgwmUvNCA";
        const response = await axios.get('https://api.unsplash.com/photos/random', {
            params: { count: 15},
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
</style>