<script>

import axios from 'axios'

export default {
    name: 'studentEreate',
    data() {
        return {
            studentId: '',
            model: {
                student: {
                    name: '',
                    email: '',
                    phone: '',
                    course: ''
                }
            }
        }
    },

    mounted() {
        this.studentId = this.$route.params.id
        this.getStudentsData(this.$route.params.id);
    },

    methods: {

        getStudentsData(studentId) {
            axios.get('http://localhost:3000/Student/' + studentId).then((res) => {
                this.model.student = res.data
            })
        },

        updateStudent() {
            const reqObj = this.model.student
            axios.put(`http://localhost:3000/Student/${this.studentId}`, reqObj).then((res) => {
                alert("User Updated Successfully!")
            })
        }
    }
}

</script>

<template>
    <div class="create">
        <div class="container mt-4">
            <div class="card">
                <div class="card-header">
                    <h4>Edit Students</h4>
                </div>
                <div class="card-body">
                    <div class="row">
                        <div class="col-md-6">
                            <div class="form-group mb-3">
                                <label class="form-label">Name</label>
                                <input type="text" v-model="model.student.name" class="form-control">
                            </div>
                        </div>
                        <div class="col-md-6">
                            <div class="form-group mb-3">
                                <label class="form-label">Email</label>
                                <input type="text" v-model="model.student.email" class="form-control">
                            </div>
                        </div>
                        <div class="col-md-6">
                            <div class="form-group mb-3">
                                <label class="form-label">Course</label>
                                <input type="text" v-model="model.student.course" class="form-control">
                            </div>
                        </div>
                        <div class="col-md-6">
                            <div class="form-group mb-3">
                                <label class="form-label">Phone</label>
                                <input type="text" v-model="model.student.phone" class="form-control">
                            </div>
                        </div>
                    </div>
                    <div class="button-wraper text-center mt-2">
                        <button type="submit" @click="updateStudent" class="btn btn-success me-3"> Save </button>
                        <RouterLink to="/students" class="btn btn-primary">Back</RouterLink>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>