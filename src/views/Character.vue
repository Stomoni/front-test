<template>
    <div class="character">
        <p>Nom: {{this.character.name}}, 
          Poids: {{this.character.mass}}, 
          Couleur des yeux: {{this.character.eye_color}}
        </p>
    </div>
</template>

<script>
import axios from 'axios'

export default {
    name: 'Character',
  
    data() {
        return {
            character: {},
        }
    },

    created() {
        if (this.$route.params.id) {
            axios.get("https://swapi.dev/api/people/" + this.$route.params.id + "/")
            .then(res => {
                this.character = res.data
            })
            .catch(e => {console.log(e)})
        }
    }
}
</script>
