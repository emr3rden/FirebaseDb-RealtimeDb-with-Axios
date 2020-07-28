<template>

    <div>

        <h3>Using Firebase Database - Realtime Database with Axios</h3>

        <hr>

        <div class="container">
            <div class="row">
                <div class="col-md-12 col-md-offset-3">
                    <form @submit.prevent="onSubmit">
                        <div class="form-group">
                            <label>Name</label>
                            <input type="text" class="form-control" v-model="usersInfo.name">
                        </div>
                        <div class="form-group">
                            <label>Surname</label>
                            <input type="text" class="form-control" v-model="usersInfo.surname">
                        </div>
                        <div class="form-group">
                            <label>Age</label>
                            <input type="text" class="form-control" v-model="usersInfo.age">
                        </div>
                        <div class="form-group">
                            <label>Thumbnail</label>
                            <input type="text" class="form-control" v-model="usersInfo.thumbnail" placeholder="Thumbnail Link">
                        </div>
                        <button class="btn btn-primary">Submit</button>
                    </form>
                </div>
            </div>
        </div>

        <hr>

        <div class="d-flex flex-wrap flex-row justify-content-center align-items-center">
            <div class="card" v-for="lt in list" :key="lt.id">
                <img class="card-img-top" :src="lt.thumbnail">
                <div class="card-body">
                    <p class="card-title">Date: {{ lt.date }} </p>
                    <p class="card-text">Name: {{ lt.name }}</p>
                    <p class="card-text">Surname: {{ lt.surname }}</p>
                    <p class="card-text">Age: {{ lt.age }}</p>
                    <button class="btn btn-primary" @click="deleteUser(lt.id)">Delete</button>
                </div>
            </div>
        </div>



    </div>

</template>



<script>

    import axios from 'axios';

    export default {

        name: "onSubmit",

        data(){
            return {
                usersInfo : {
                    name : '',
                    surname : '',
                    age : '',
                    thumbnail : '',
                    // date : '',
                },

                list : [],
            }
        },

        methods : {
            onSubmit(){
                if (this.usersInfo.name !== '' && this.usersInfo.surname !== '' && this.usersInfo.age !== '' && this.usersInfo.thumbnail !== '') {
                    axios.post('/users.json', { ...this.usersInfo, date : new Date()})
                        .then(response => {
                            console.log(response)
                            this.usersInfo = {}
                            location.reload()
                        })
                } else {
                    return alert('Please fill in the blank fields...')
                }
            },

            deleteUser(listKey){
                axios.delete('/users/' + listKey + '.json')
                    .then(response => {
                        console.log(response)
                    })
            }
        },

        created(){
            axios.get('/users.json')
                .then(response => {
                    let data = response.data;
                    for(let key in data){
                        this.list.push({ ...data[key], id : key })
                    }
                })
                .catch(e => console.log(e))
        },



    }

</script>



<style scoped>

    .card {
        width: 300px;
        margin: 50px;
    }



</style>