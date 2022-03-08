<template>
  <div class="nasa-banner">
    <div class="nav">
      <router-link to="/pictureoftheday">Photo du jour</router-link>
      <router-link to="#">Asteroïdes News</router-link>
      <router-link to="#">Images polychromatiques</router-link>
      <router-link to="#">Photos de Mars</router-link>
    </div>
    <router-link to="/">
      <div class="logo">
        <img src="../assets/logo-rs2.png" alt="logo Nasa" class="nasa-logo" />
        <h1 class="nasa-title">{{ title }}</h1>
      </div>
    </router-link>  
  </div>
</template>

<script>
export default {
  name: 'Banner',
  props: {
    title: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.nasa-banner {
    color: white;
    /*text-align: right;*/
    //padding: 32px;
    border-bottom: solid 3px #ffffff;
    justify-content: right;
}

.logo {
    display: flex;
    justify-content: flex-end;
    flex-direction: row;
    align-items: center;
    margin-top: -50px;
}

.nav {
    align-items: center;
    display: flex;
    justify-content: flex-start;
}

a {
    margin-right: 20px;
    text-decoration: none;
    color: white;
}
</style>
