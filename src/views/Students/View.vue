
<template>
    <div class="container mt-5">
        <div class="card">
            <div class="card-header">
                <h4>Students</h4>
                <RouterLink to="/students/create" class="btn btn-primary float-end">
                    Add student
                </RouterLink>
            </div>
            <div class="card-body">
                <table class="table table-bordered">
                    <thead>
                        <tr>
                            <th> ID </th>
                            <th>First Name </th>
                            <th>Last Name </th>
                            <th>Email</th>
                            <th>Actions </th>
                        </tr>
                    </thead>
                    <tbody v-if="this.students.length > 0">
                        <tr v-for="(student, index) in this.students" :key="index">
                            <td>{{ student.id }}</td>
                            <td>{{ student.first_name }}</td>
                            <td>{{ student.last_name }}</td>
                            <td>{{ student.email }}</td>
                            <td>
                                <RouterLink :to="{path : '/students/'+student.id+'/update'}" class="btn btn-success mx-2">
                                    Edit
                                </RouterLink>
                                <button class="btn btn-danger mx-2">
                                    Delete
                                </button>
                            </td>
                        </tr>
                    </tbody>
                    <tbody v-else>
                        <tr>
                            <td colspan="6">
                                Loading...
                            </td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>
    </div>
</template>
<script>
import axios from 'axios'
    export default {
        name: 'students',
        data(){
            return {
                students: []
            }
        },
        mounted(){
            this.getStudents()
        },
        methods: {
            getStudents(){
                axios.get('https://reqres.in/api/users')
                    .then( res => {
                        this.students = res.data.data
                    })
            }
        }
    }
</script>