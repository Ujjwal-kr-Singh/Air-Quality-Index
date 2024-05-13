<template>
    <!-- <h1>welcome to edit page (edit here)</h1> -->
    
    <h1 style="background-color: red;">welcome to edit page (edit here)</h1>
                    <!-- <div>{{ usereditlist }}</div>
                   <div> {{ id }}{{}}
                    {{ firstname }}</div> -->
    
    <html lang="en">
        <head>
            
            <meta charset="utf-8">
            <meta name="viewport" content="width=device-width, initial-scale=1">
            <title>edit demo</title>
            <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet"
                integrity="sha384-QWTKZyjpPEjISv5WaRU9OFeRpok6YctnYmDr5pNlyT2bRjXh0JMhjY6hW+ALEwIH" crossorigin="anonymous">
        </head>
    
        <body style="background-color: aqua;">
           
            <div class="container">
                <div class="alert bg-success my-3">
                    <h4 class="text-center" style="color: yellow">Edit Course.Edit </h4>
                </div>
            </div>
            <div class="container">
                <div class="row">
                    <div class="col"></div>
                    <div class="col">
                      <!--  <div class="field my-3">
                            <label for="" class="form-label">id:</label>
                            <input type="text" class="form-control" v-model='user._id'>-->
                        </div>
                         <div class="field my-3">
                            <label for="" class="form-label">CourseCode:</label>
                            <input type="text" class="form-control" v-model='course.CourseCode'>
                        </div>
                        <div class="field my-3">
                            <label for="" class="form-label">CourseFullName:</label>
                            <input type="text" class="form-control" v-model='course.CourseFullName'>
                        </div>
                        <div class="field my-3">
                            <label for="" class="form-label">Course NickName:</label>
                            <input type="text" class="form-control" v-model='course.CourseNickName'>
                          
                            <div class="field my-3">
                                <label for="" class="form-label">CourseDuration:</label>
                                <input type="text" class="form-control" v-model='course.CourseDuration'>
                            </div>
                            <div class="field my-3">
                                <!-- <label for="" class="form-label">CourseMode:</label> -->
                                <!-- <input type="text" class="form-control" v-model='course.CourseMode'> -->
                                
                                <!-- <select class="form-control" v-model="course.CourseMode">
                                    <option value="Semester">Semester</option>
                                    <option value="Yearly">Yearly</option>
                                    </select> -->


                            </div>
                            <div class="field my-3">
                                <label for="" class="form-label">Affiliated University:</label>
                                <input type="text" class="form-control" v-model="course.affiliatedUniversity">
                            </div>
                        </div>
    
                   <input type="submit" value="Edit" class="btn btn-danger my-3 w-100" @click="editcourse(course._id)"/>
                    
                </div>
                <div class="col"></div>
            </div>
      <!--  </div>-->
        
    </body>
    
    </html>
    
    
    </template>
    <script>
    import axios from 'axios';
    import router from '@/router';
    import {useRoute}from 'vue-router';
    
    
    export default{
        name:'UserEdit',
        data(){
            return{
                course:{
    
                }
                // usereditlist:{
    
                    //change
                //   id:'',
                //   firstname:'',
                //   Lastname: '',
                //   mobno: '',
                //  email: '',
                //   password: '',
                //   usertype: ''
                     //change
    
                //  }//usereditlist
    
            }
        },
        created(){
            this.getcoursedata()
        },
        methods:{
            async editcourse(id) {
            let data = {
            CourseCode: this.course.CourseCode,
            CourseFullName: this.course.CourseFullName,
            CourseNickName: this.course.CourseNickName,
            CourseDuration: this.course.CourseDuration,
         //   CourseMode: this.user.CourseMode,
            affiliatedUniversity: this.course.affiliatedUniversity
                         
            
          };
          let result = await axios({
            method: "put",
            url: "http://localhost:3000/course/edit/" + id,
            data:data,
          });
          console.log(result);
          if(result.data.success){
                        router.push({name:"CourseList"})}
        },
           async getcoursedata(){
               const route=useRoute()
               let id=route.params.id
               console.log(id,"....id")
               let result=await axios({
                    method:'get',
                    url:'http://localhost:3000/course/for/edit/'+id
                })
               // this.id=result.data.data._id;
                   //change
                // this.firstname=result.data.data.firstname;
                // this.Lastname=result.data.data.Lastname;
                // this.mobno=result.data.data.mobno;
                // this.email=result.data.data.email;
                // ze;
               // console.log(id,'unique id')
                console.log(result,'result is here');
                //change
                this.course=result.data.data;
              //  console.log(result.data.data._id,'idgh');
               // console.log(result.data.data.email,'mail...');
                //this.usereditlist=result.data.data;//list where edit id and data is placed
            }
        }
    }
    
    </script>
    <style scoped>
    body{
        background-image:url("@/assets/scope.jpg");
        background-repeat:no-repeat;
        background:cover;
        background-size:cover
        
    }
     label {
        color: rgb(255, 18, 208) !important;
    }
    
    </style>