<template>
    <div>
        <div>
            <h4>{{ $route.params.joke }}</h4>
            <div>
                <img :src="'https://icanhazdadjoke.com/j/' + $route.params.jokes + '.png'" alt="img was here">
            </div>
            <h4>{{ jokeNew }}</h4>
        </div>
    </div>
</template>
<script>
export default {
    // const url = 'https://icanhazdadjoke.com/j/<joke_id>'
        //Test
    data() {
        return {
            jokeNew: ''
        }
    },
    methods: {

    },
    created() {
        fetch('https://icanhazdadjoke.com/j/' + this.$route.params.jokes, { headers: { 'Accept': 'application/json' } })
            .then(
                (response) => {
                    response.json()
                        .then((data) => {
                            this.jokeNew = data.joke
                        });

                }
            )
    }
}

</script>

<style></style>