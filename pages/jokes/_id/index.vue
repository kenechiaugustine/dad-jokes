<template>
    <div>
        <div>
            <nuxt-link to="/jokes"> Back </nuxt-link>
        </div>
        <h2>
            {{ joke }}
        </h2>
        <hr />
        <small>Joke ID: {{ $route.params.id }}</small>
    </div>
</template>

<script>
import axios from 'axios'

export default {

    data() {
        return {
            joke: {}
        };
    },

    async created() {
        const config = {
            headers: {
                "Accept": "application/json"
            }
        };
        try {
            const res = await axios.get(`https://icanhazdadjoke.com/j/${this.$route.params.id}`, config);
            this.joke = res.data.joke;
        }
        catch (error) {
            console.log(error);
        }
    },

    head() {
        return {
            title: this.$route.params.id,
            meta: [
                {
                    hid: "description",
                    meta: "description",
                    content: "Best dad jokes",
                },
            ],
        };
    }

}
</script>

<style>

</style>