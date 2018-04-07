<template>
  <div id="app">
    <h3>{{ title }}</h3>
    <div class="col-md-12">
      <character v-for="(id, idx) in initial_ids" :id="id" :key="idx" />
    </div>
  </div>
</template>

<script>
import Character from './components/Character'

export default {
  components: { Character },
  data() {
    return {
      title: 'Generate your team',
      initial_ids: [1, 13, 14]
    }
  },
}
</script>

