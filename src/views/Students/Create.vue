<template>
    <div class="container mt-5">
        <div class="card">
            <div class="card-header">
                <h4>Students</h4>
            </div>
            <div class="card-body">
                <ul class="alert alert-warning" v-if="Object.keys(this.errorList).length > 0">
                    <li class="mb-0 ms-3 " v-for="(error, index) in this.errorList" :key="index">
                        {{ error[0] }}
                    </li>
                </ul>
                <ul v-else>
                    <li>

                    </li>
                </ul>
                <div class="mg-3">
                    <label for="first_name">First Name</label>
                    <input type="text" class="form-control" v-model="model.student.first_name"/>
                </div>
                <div class="mg-3">
                    <label for="last_name">Last Name</label>
                    <input type="text" class="form-control" v-model="model.student.last_name"/>
                </div>
                <div class="mg-3">
                    <label for="email">Email</label>
                    <input type="text" class="form-control" v-model="model.student.email"/>
                </div>
                <div class="mg-3">
                    <button class="btn btn-primary" type="button" @click="saveStudent()">
                        Save
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
import axios from 'axios'
    export default {
        name: 'studentCreate',
        data(){
            return {
                errorList: '',
                model: {
                    student : {
                        first_name: '',
                        last_name: '',
                        email: ''
                    }
                }
            }
        },
        methods: {
            saveStudent(){
                var mythis = this
                axios.post('https://reqres.in/api/users', this.model.student)
                    .then(res => {
                        alert(res.data.message)
                        this.model.student = {
                            first_name: '',
                            last_name: '',
                            email: ''
                        }
                        this.errorList = ''
                    })
                    .catch(function () {
                        if(error.response.status == 422) {
                            mythis.errorList = error.response.data.errors
                        }
                        if (error.response) {
                            console.error(error.response.data);
                            console.error(error.response.status);
                            console.error(error.response.headers);
                        } else if (error.request) {
                            console.error(error.request);
                        } else {
                            console.error('Error', error.message);
                        }
                    })
                }
        }
    }
</script>