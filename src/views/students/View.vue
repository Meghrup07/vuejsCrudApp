
<script>
import axios from 'axios'
export default {
    name: 'student',
    data() {
        return {
            students: []
        }
    },
    mounted() {
        this.getStudentsData();
    },
    methods: {
        getStudentsData() {
            axios.get('http://localhost:3000/Student').then((res) => {
                this.students = res.data;
            })
        },
        deleteStudent(id) {
            axios.delete(`http://localhost:3000/Student/${id}`).then((res) => {
                alert("Student data deleted successfully!")
                this.getStudentsData();
            })
        }
    }
}

</script>


<template>
    <div class="view">
        <div class="container">
            <div class="card mt-4">
                <div class=" card-header">
                    <h4>
                        Students
                        <RouterLink to="/student/create" class="btn btn-primary float-end">Add Student</RouterLink>
                    </h4>
                </div>
                <div class="card-body">
                    <div class="responsive-table">
                        <table class="table table-striped table-bordered">
                            <thead>
                                <tr>
                                    <th scope="col">Id</th>
                                    <th scope="col">Name</th>
                                    <th scope="col">Course</th>
                                    <th scope="col">Email</th>
                                    <th scope="col">Phone</th>
                                    <th scope="col">Action</th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr v-for="(student, index) in this.students" :key="index">
                                    <th>{{ student.id }}</th>
                                    <td>{{ student.name }}</td>
                                    <td>{{ student.course }}</td>
                                    <td>{{ student.email }}</td>
                                    <td>{{ student.phone }}</td>
                                    <td>
                                        <RouterLink :to="{ path: '/student/edit/' + student.id }"
                                            class="btn btn-success me-2">
                                            Edit
                                        </RouterLink>
                                        <button @click="deleteStudent(student.id)" type="button" class="btn btn-danger">
                                            Delete
                                        </button>
                                    </td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
