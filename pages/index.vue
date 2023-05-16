<template>
    <div class="maindiv">
        <div>
            <div v-if='loading' class="loader"></div>
            <Nuxt-Link v-for="(joke, i) in jokes" :key="i" :to="'/' + joke.id" class="p divJoke">{{ joke.joke }}</Nuxt-Link>
        </div>
    </div>
</template>
<script>
export default {
    data() {
        return {
            jokes: [],
            loading: false
        }
    },
    methods: {
        openJoke(joke) {
            this.$router.push('/' + joke)
        }
    },
    created() {
        this.loading = true
        fetch('https://icanhazdadjoke.com/search', { headers: { 'Accept': 'application/json' } })
            .then(
                (response) => {
                    response.json()
                        .then((data) => {
                            console.log(data.results)
                            this.jokes = data.results
                        });
                }
            )
            .finally(() => (this.loading = false))
    }
}
</script>
<style>
body {
    margin: 0;
    font-family: sans-serif;
}

.divJoke {
    border: 1px solid gray;
    padding: 10px;
}

.p {
    text-decoration: none;
    color: black;
    display: block;
}

.loader {
    border: 16px solid #f3f3f3;
    position: fixed;
    left: calc(50% - 60px);
    top: calc(50% - 60px);
    border-radius: 50%;
    border-top: 16px solid #3498db;
    width: 120px;
    height: 120px;
    -webkit-animation: spin 2s linear infinite;
    /* Safari */
    animation: spin 2s linear infinite;
}

/* Safari */
@-webkit-keyframes spin {
    0% {
        -webkit-transform: rotate(0deg);
    }

    100% {
        -webkit-transform: rotate(360deg);
    }
}

@keyframes spin {
    0% {
        transform: rotate(0deg);
    }

    100% {
        transform: rotate(360deg);
    }
}
</style>