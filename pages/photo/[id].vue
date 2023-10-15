<template>
  <div>
    <div class="bg_img">
      <div class="container">
          <div class="row pt-5 pb-5">
            <div class="col">
                <div>
                  <img src="@/assets/images/user.png" class="float-start mt-1" alt="user">
                </div>
                <div class="d-flex flex-column flex_margin_r">
                  <h4 class="text-light float-start">{{user}}</h4>
                  <h6 class="text-light float-start">@{{ email }}</h6>
                </div>
            </div>
            <div class="col-8">
                  <div class="float-end">
                      <div class="icon_heart d-inline p-2">
                        <IconsHeartIcon class=""/>
                      </div>

                      <div class="d-inline p-2">
                        <button type="button" class="btn btn-success"><IconsDownload />Downloand</button>
                      </div>
                  </div>
            </div>
          </div>
      </div>
      <div class="container">
        <div class="row">
          <div class="col">
            <img :src="regular" class="block_img"/>
          </div>
        </div>
      </div>
      <div class="container">
        <div class="row">
           <div class="col text-center color_bg_size">
              <h4>Похожии теги</h4>
           </div>
        </div>
        <div class="row">
           <div class="col text-center mb-5">
              <PageTags />
           </div>
        </div>
      </div>
    </div>
    <div class="container">
        <div class="row mb-5">
            <h2 class="mb-5 mt-5">Похожие фотографии</h2>
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
   data(){
        return {
            regular: '',
            user: '',
            email: '',
            data: '',
            favorites: [],
            images: []
        }
    },
    watch: {
        $route (toR){
          this.id = toR.params['id']
        }
    },
    async beforeMount(){
        const ClientId = "i9KK1kmO9x2ZHK2t6Mu35bbaQzqIdgtWKtzgwmUvNCA";

        const response = await axios.get(`https://api.unsplash.com/photos/${this.$route.params['id']}`, {
            headers: {
                Authorization: `Client-ID ${ClientId}`
            }
        })

        const responseData = await axios.get('https://api.unsplash.com/photos/random', {
            params: { count: 9},
            headers: {
                Authorization: `Client-ID ${ClientId}`
            }
        })
        this.images = responseData.data;
        this.regular = response.data.urls.full;
        this.user = response.data.user.name;
        this.email = response.data.user.username;
        this.data = response.data;
    },
}
</script>

<style lang="scss" scoped>
.bg_img{
    background: rgba(0, 0, 0, 0.5) url("@/assets/images/Rectangle.png") no-repeat;
}
.color_bg_size{
  color: white;
}
.block_img{
  height: 474px;
  width: 100%;
  margin-bottom: 5%;
}
.icon_heart{
  background: white;
  padding: 10px;
  border-radius: 20%;
  cursor: pointer;
}

.flex_margin_r{
  padding-left: 2%;
}
</style>