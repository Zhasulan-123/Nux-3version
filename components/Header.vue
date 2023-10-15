<template>
  <header>
    <nav class="navbar bg_color navbar_height">
      <div class="container">
          <router-link class="navbar-brand logo_color" to="/">
            <img src="@/assets/images/Vector.png" class="display_online"/>
            ImageStock
          </router-link>
          <ul class="nav justify-content-end">
            <li class="nav-item" v-if="$route.path !== '/'">
              <router-link class="nav-link" to="/"><IconsSearch /><span>Поиск</span></router-link>
            </li>
            <li class="nav-item">
              <router-link class="nav-link" to="/favorites"><IconsHeart /><span>Избранное</span></router-link>
            </li>
            <li class="nav-item">
              <router-link class="nav-link" to="/favorites"><IconsEscape /><span>История поиска</span></router-link>
            </li>
          </ul>
      </div>
    </nav>
  </header>
</template>


<style lang="scss" scoped>
.display_online{
  margin-right: 8%;
  margin-top: 2%;
}
.logo_color{
  color: white;
  font-size: 23px;
}
.bg-dark{
  background: #000;
}
.navbar_height{
  height: 148px !important;
}
.nav-link span{
   color: #fff;
   margin-left: 10px;
}
.bg_color{
  background-color: black;
}

@media only screen and (max-width: 768px) {
  .nav-link span{
    display: none;
  }
}
</style>