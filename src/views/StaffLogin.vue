<template>
    <div class="container center">
        <h2 class="mt-4">Film editing page (Staff only)</h2>
        <div class="input-group mb-3 mt-5 w-50 ">
        <input type="text" class="form-control" v-model="title" placeholder="Enter the movie title to search" aria-label="Recipient's username" aria-describedby="button-addon2">
        <button class="btn btn-success" type="button" id="button-addon2" @click="fetchFilm(title)">Search</button>
        </div>

    <div class="container">
        <form @submit="updateFilm" method="post">
           <div class="row mb-4 mt-5" >
            <div class="col-md-5">
                <img v-bind:src="film.poster" class="img-fluid" />
            </div>
           <table class=" col-md-7 table table-dark table-striped">
                <tbody>

                    <tr>
                        <th>Film title:</th>
                        <td><input type="text" name="title" class="form-control bg-dark text-light" v-model="film.title" readonly></td>
                    </tr>
                    <tr>
                        <th>Released date of the film:</th>
                        <td><input type="text" class="form-control bg-dark text-light"  v-model="film.released" required></td>
                    </tr>
                    <tr>
                        <th>Released year of the film:</th>
                        <td><input type="text" class="form-control bg-dark text-light"  v-model="film.year" required> </td>
                    </tr>
                     <tr>
                        <th>Runtime of the film:</th>
                        <td><input type="text" class="form-control bg-dark text-light" v-model="film.runtime" required></td>
                    </tr>
                     <tr>
                        <th>Film language:</th>
                        <td><input type="text" class="form-control bg-dark text-light" v-model="film.language" required></td>
                    </tr>
                     <tr>
                        <th>Genre of the film:</th>
                        <td><input type="text" class="form-control bg-dark text-light" v-model="film.genre" required></td>
                    </tr>
                     <tr>
                        <th>The director of the film:</th>
                        <td><input type="text" class="form-control bg-dark text-light" v-model="film.director" required></td>
                    </tr>
                    <tr>
                        <th>Poster:</th>
                        <td><textarea type="textarea" class="form-control bg-dark text-light" v-model="film.poster" readonly /></td>
                    </tr>
                   
                </tbody>

            </table>
            <div class="offset-9 row p-2">
                <div>
                    <button type="submit" class="btn btn-success btn-lg mb-3 mr-3" @click="cancelUpdate" >Cancle</button> 
                </div>
                 <div>
                    <button type="submit" class="btn btn-danger btn-lg mb-3" >Update</button> 
                </div>
            </div>
            

        </div> 
        </form>
        
    </div>
    </div>

</template>

<script>
export default {
    name: 'StaffLogin',
    data() {
            return {
                title: '',
                film: {},
                loading: false
            }
            },
             beforeMount(){
    if(localStorage.getItem('name')){
      const n = JSON.parse(localStorage.getItem('name'))
      if(n.role!=1){
         this.$router.push('/')
        alert("You have no right to access")
      }
    }else{
      this.$router.push('/')
      alert("You have no right to access")
    }
  },
            methods: {
                async fetchFilm(title) {
                const res = await fetch(`http://47.242.250.90:18888/infofilm/${title}`)
                const data = await res.json();
                this.film = data
                },
                updateFilm(e){
                    console.log(this.film)
                    this.axios.post("http://47.242.250.90:18888/imfilm", this.film)
                    .then((result)=>{
                        console.log(result)
                    })
                    e.preventDefault();
                },
                cancelUpdate(){
                    this.$router.push('/')
                }

    }
}
</script>

<style scoped>
th{
    text-align: left;
}

td{
    text-align: left;
}

</style>