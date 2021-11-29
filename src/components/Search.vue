<template>
    <div class="search">
        <input v-model="input" @change="search(input)"/>
    </div>
</template>

<script>

export default {
    data() {
        return {
            input: null
        }
    },

    methods: {
        search(input) {
            this.$emit('searchCharacter', input)
        }
    }
}
</script>
