<template>
    <div class="container">
        <div class="row mt-5">
            <div class="offset-11 col-md-1">
                <button type="button" class="btn btn-success btn-lg" @click="back()">Back</button>
            </div>
        </div>
         <h1 class="mt-3 mb-5 text-warning fw-bold">{{ film.title }}</h1> 
        <div class="row mb-4">
            <div class="col-md-7">
                <img v-bind:src="film.poster" />
            </div>
            <table class=" col-md-5 table table-dark table-striped">
                <tbody>
                    <tr>
                        <th>Released date of the film:</th>
                        <td>{{ film.released }}</td>
                    </tr>
                    <tr>
                        <th>Released year of the film:</th>
                        <td>{{ film.year }}</td>
                    </tr>
                     <tr>
                        <th>Runtime of the film:</th>
                        <td>{{ film.runtime }}</td>
                    </tr>
                     <tr>
                        <th>Film language:</th>
                        <td>{{ film.language }}</td>
                    </tr>
                     <tr>
                        <th>Genre of the film:</th>
                        <td>{{ film.genre }}</td>
                    </tr>
                     <tr>
                        <th>The director of the film:</th>
                        <td>{{ film.director }}</td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
            idx: '',
            film: {},
            loading: false
            }
            },
            beforeMount(){
                this.fetchFilm(this.$route.params.idx)
            },
            methods: {
            async fetchFilm(idx) {
            const res = await fetch(`http://47.242.250.90:18888/film/${idx}`)
            const data = await res.json();
            this.film = data[0]
            },
            back() {
            return this.$router.go(-1)
            }
        }
}
</script>

<style scoped>
img{
    width: 30em;
}

th{
    text-align: right;
}

td{
    text-align: left;
}

p{
    font-size: 1.5em;
}

table{
    height: 8em;
}
</style>