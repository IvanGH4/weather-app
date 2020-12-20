<template>
  <div class="home">
    <BaseWeather />
  </div>
</template>

<script>
// @ is an alias to /src
import BaseWeather from '@/components/share-tools/BaseWeather'
export default {
  name: 'Home',
  components: {
    BaseWeather
  }
}
</script>
