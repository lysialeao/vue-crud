<template>
    <div class="container mt-5">
        <div class="card">
            <div class="card-header">
                <h4>Edit Students</h4>
            </div>
            <div class="card-body">
                <ul class="alert alert-warning" v-if="Object.keys(this.errorList).length > 0">
                    <li class="mb-0 ms-3 " v-for="(error, index) in this.errorList" :key="index">
                        {{ error[0] }}
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
                    <button class="btn btn-primary" type="button" @click="updateStudent()">
                        Update
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
import axios from 'axios'
    export default {
        name: 'studentUpdate',
        data(){
            return {
                studentId: '',
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
        mounted(){
            this.student = this.$route.params.id
            this.getStudentData(this.$route.params.id)
        },
        methods: {
            getStudentData(studentId) {
                axios.get(`https://reqres.in/api/users/${studentId}`)
                    .then( res => {
                        console.log(res.data.data)
                        this.model.student = res.data.data
                    })
                    .catch((error) => {
                        mythis.errorList = error.response.data.errors
                    })
            },
            updateStudent(){
                var mythis = this
                axios.put(`https://reqres.in/api/users/${this.studentId}`, this.model.student)
                    .then(res => {
                        alert(res.statusText)
                        this.errorList = ''
                    })
                    .catch((error) => {
                        mythis.errorList = error.response.data.errors
                    })
                }
        }
    }
</script>