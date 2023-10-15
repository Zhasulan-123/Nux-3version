<template>
  <div class="row justify-content-center">
    <div class="col-6 bg_margin">
      <nav>
        <router-link v-for="img in images" :key="img.id" :to="'/photo/' + img.id">
          {{img.user.name}}
        </router-link>
      </nav>
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
nav
{
    right: 0;
    left: 0;
    display: table;
    margin: 0 auto;
}

nav a
{
    width: 33.333%;
    display: table-cell;
    text-align: center;
    color: #949494;
    text-decoration: none;
    font-weight: bold;
    padding: 10px 15px;
    text-overflow: ellipsis;
    white-space: nowrap;
    overflow: hidden;
    width: 300px;
}
.bg_margin{
    margin-bottom: 5%;
}
</style>