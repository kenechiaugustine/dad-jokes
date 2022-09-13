<template>
    <div>
        <SearchJokes v-on:search-text="searchText" />
        <Joke v-for="joke in jokes" :key="joke.id" :id="joke.id" :joke="joke.joke" />
    </div>
</template>

<script>
import axios from 'axios'
import Joke from '~/components/Joke.vue';
import SearchJokes from '~/components/SearchJokes.vue';

export default {
    data() {
        return {
            jokes: []
        };
    },
    async created() {
        const config = {
            headers: {
                "Accept": "application/json"
            }
        };
        try {
            const res = await axios.get("https://icanhazdadjoke.com/search", config);
            this.jokes = res.data.results;
        }
        catch (error) {
            console.log(error);
        }
    },

    methods: {
        async searchText(text) {
            const config = {
                headers: {
                    "Accept": "application/json"
                }
            };
            try {
                const res = await axios.get(`https://icanhazdadjoke.com/search?term=${text}`, config);
                this.jokes = res.data.results;
            }
            catch (error) {
                console.log(error);
            }
        }
    },

    head() {
        return {
            title: "Dad jokes",
            meta: [
                {
                    hid: "description",
                    meta: "description",
                    content: "Best dad jokes",
                },
            ],
        };
    },
    components: { Joke, SearchJokes }
}
</script>

<style>

</style>