<template>
  <div class="container">
    <div class="row justify-content-center mt-3">
        <div class="col-6">
          <nav>
            <ul class="pagination margin_left">
                <li v-for="img in images" :key="img.id">
                    <router-link :to="'/photo/' + img.id">
                      <span class="badge text-bg-light circle_color">{{img.user.name}}</span>
                    </router-link>
                </li>
            </ul>
          </nav>
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
            params: { count: 4},
            headers: {
                Authorization: `Client-ID ${ClientId}`
            }
        })
        this.images = response.data;
    },
}
</script>

<style lang="scss" scoped>
.margin_left > li{
    margin-right: 5%;
}
.circle_color{
    color: #828282 !important;
}

</style>