<template>
  <div class="home">
    <Banner title="Nasa-API"/>
    <div className="presentation">
      <p>Bienvenue sur Nasa-API. Ici vous découvrirez tous les clichés de la Nasa, qu'ils proviennent de satellites, de sondes, de télescopes ou des rovers qui arpentent le sol de Mars.
        Cette application utilise les données de l'API public de la Nasa.<br />
        Bonne découverte !!!
      </p>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import Banner from '@/components/Banner.vue'

export default {
  name: 'Home',
  components: {
    Banner
  }
}
</script>

<style lang="scss" scoped>
.presentation {
  margin-left: auto;
  margin-right: auto;
  width: 80%;
  height: 70vh;
  display: flex;
  align-items: center;
}

p {
  color: white;
  font-size: 1.5rem;
}
</style>
