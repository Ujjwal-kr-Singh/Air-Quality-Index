<template>
    <!-- <img alt="Vue logo" src="../assets/signup.png"> -->
    <!-- <!DOCTYPE html> -->
    <html lang="en">

    <head>
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <title>Create Course</title>
        <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet"
            integrity="sha384-QWTKZyjpPEjISv5WaRU9OFeRpok6YctnYmDr5pNlyT2bRjXh0JMhjY6hW+ALEwIH" crossorigin="anonymous">
    </head>

    <body>
       
        <div class="container">
            <div class="alert bg-warning my-3">
                <h4 class="text-center" style="color: golden">create Course(signup) </h4>
            </div>
        </div>
        <div class="container">
            <div class="row">
                <div class="col"></div>
                <div class="col">
                     <!--either get or post-->
                        <div class="field my-3">
                            <label for="" class="form-label">CourseCode:</label>
                            <input type="text" class="form-control" v-model='CourseCode'>
                        </div>
                        <div class="field my-3">
                            <label for="" class="form-label">CourseFullName:</label>
                            <input type="text" class="form-control" v-model='CourseFullName'>
                        </div>
                        <div class="field my-3">
                            <label for="" class="form-label">CourseNickName:</label>
                            <input type="text" class="form-control" v-model='CourseNickName'>
                            <div class="field my-3">
                                <label for="" class="form-label">CourseDuration:</label>
                                <input type="text" class="form-control" v-model='CourseDuration'>
                            </div>
                            <div class="field my-3">
                                <label for="" class="form-label">CourseMode:</label>
                                <!-- <input type="text" class="form-control" v-model='CourseMode'> -->
                                <select class="form-control" v-model="CourseMode">
                                    <option value="Semester">Semester</option>
                                    <option value="Yearly">Yearly</option>
                                    </select>

                            </div>
                            <div class="field my-3">
                                <label for="" class="form-label">affiliatedUniversity:</label>
                                <input type="text" class="form-control" v-model='affiliatedUniversity'>
                            </div>
                        </div>

                   <input type="submit" value="CREATE" class="btn btn-warning my-3 w-100" @click="adduser()"/>
                    
                </div>
                <div class="col"></div>
            </div>
        </div>
    </body>

    </html>



</template>

<script>
import axios from 'axios';
import router from '@/router';
export default {
    name: 'SignUp',
    data() {
        return {
            CourseCode: '',
            CourseFullName: '',
            CourseNickName: '',
            CourseDuration: '',
            CourseMode: '',
            affiliatedUniversity: ''

        }
    },
    methods: {
        async adduser() {
            try {
                let data = {
                    CourseCode: this.CourseCode,
                    CourseFullName: this.CourseFullName,
                    CourseNickName: this.CourseNickName,
                    CourseDuration: this.CourseDuration,
                    CourseMode: this.CourseMode,
                    affiliatedUniversity: this.affiliatedUniversity,

                }
              let result=  await axios({
                    method: 'post',
                    url: 'http://localhost:3000/course/create',
                    data: data,
                })
                console.log(result,'this is result');
                if(result.data.success){
                    router.push({'path':'/courselist'})

                }
            } catch (err) {
                console.log(err);
            }

        },
    },
};




</script>
<style scoped>
body{
    background-image:url("@/assets/scope.jpg");
    background-repeat:no-repeat;
    background:cover;
    background-size:cover
 
    
}

 label {
    color: rgb(47, 215, 223) !important;
}

</style >