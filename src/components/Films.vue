<template>
    <div class="container mb-5">
        <h2>Check out our upcoming HOT MOVIES below!</h2>      
            <div class="row" v-if="!loading">
                <div class="col" v-for="film in data" :key="film._id">
                    <img v-bind:src="film.poster" @click="showDetail(film._id)" alt="Image 1"  />
                    <h3 class="text-start mb-4" @click="showDetail(film._id)">{{film.title}}</h3>
                </div>
            </div>
    </div>
</template>

<script>


export default {
    name:"Films",
    data () {
        return {
            data:[],
            loading:false
        }
    },
    beforeMount() {
    this.fetchFilm()
    },
    methods: {
    async fetchFilm() {
        const res = await fetch('http://47.242.250.90:18888/list')
        const data = await res.json();
        this.data = data
        },
        showDetail(id){
            this.$router.push({name:'DetailFilm', params:{idx: id}})
        }
    }
}
</script>

<style scoped>

h2{
    margin-top: 1em;
    margin-bottom: 1em;
    color: #ffb703;
    font-size: 3em;
    font-weight: 700;
}

h3{
    font-size: 1em;
    padding-top: 1em;
    color: #ffb703;
}

img{
    width:15em;
    height:22em;
}
  

</style>