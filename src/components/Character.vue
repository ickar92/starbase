<template>
  <div class="col-md-4" >
    <div class="character-card" @click="switchCharacter">
      <div class="card-block">
        <h4 class="card-title">{{character.name}}</h4>
        <p class="card-text">Height: {{character.height}}cm</p>
        <p class="card-text">Mass: {{character.mass}}kg</p>
        <p class="card-text">Hair Color: {{character.hair_color}}</p>
        <p class="card-text">Eye color: {{character.eye_color}}</p>
      </div>
    </div>
    <button class="btn btn-primary" :class="{ disabled: !prevId }" @click="switchBack">Back</button>
  </div>

</template>

<script>
export default {
  props: ['id'],
  data() {
    return {
      character: {},
      prevId: null,
      currentId: this.id
    }
  }, 
  methods: {
    fetchCharacter(id) {
      return fetch(`https://swapi.co/api/people/${id}`, {
        method: 'GET'
      })
        .then(response => response.json())
        .then(json => this.character = json)
        .catch(reason => console.error(reason))
    },
    switchCharacter() {
      this.prevId = this.currentId 
      this.currentId = Math.floor(Math.random() * 83) + 1
      this.fetchCharacter(this.currentId)
    },
    switchBack() {
      if (!this.prevId) {
        return
      }
      this.fetchCharacter(this.prevId)
        .then(() => this.prevId = null)
      
    }
  },
  created () {
    this.fetchCharacter(this.id)
  }
}
</script>

