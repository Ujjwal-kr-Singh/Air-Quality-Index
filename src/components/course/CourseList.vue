<template>
    <!-- <img alt="Vue logo" src="../assets/USERLIST.png"> -->
    <html lang="en">
    <body>
   
        <!-- <h1>{{courselist}}</h1> -->
       <!-- <h1> {{course.CourseCode }}</h1> -->
        <h1>COURSE LIST IS PROVIDED HERE</h1>
    <div>
    <!--{{ userlist }}--><!--to show the list of array object [userlist]   (data in mongodb)-->
    
    <!--                -->
    <div>
        <h2>Course List Table</h2>
        <table>
          <thead>
            <tr>
              <th>Course Code</th>
              <th>Course FullName</th>
              <th>Course NickName</th>
              <th>Course Duration</th>
              <th>Course Mode</th>
              <th>Affiliated University</th>
              <th>Action</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(course, index) in courselist" :key="index">
              <td>{{ course.CourseCode }}</td>
              <td>{{ course.CourseFullName }}</td>
              <td>{{ course.CourseNickName }}</td>
              <td>{{ course.CourseDuration }}</td>
              <td>{{ course.CourseMode }}</td>
              <td>{{ course.affiliatedUniversity }}</td>
              <td><input type="button" value="edit"  @click="openEditpage(course._id)" ><input type="button" value="del" @click="deletecourse(course._id)" ></td>
            </tr>
          </tbody>
        </table>
      </div>
    
    <!--                          -->
    
    </div>
    </body>
    </html>
    </template>
    <script>
    import axios from 'axios';
    import router from '@/router';
    export default{
        name:'CourseList',
        data() {
            return {
               courselist:[]
            }
        },
       
        created(){
            this.getcourselist();
        },
        methods:{
           async getcourselist(){
            let result= await axios({
                method:'get',
                url:'http://localhost:3000/course/list'
            })
            console.log(result);
            this.courselist=result.data.data
    
            },
        openEditpage(id){
          router.push({path:'/courseedit'+'/'+id})
        },
        async deletecourse(id){
          let result= await axios({
            method:'delete',
            url:'http://localhost:3000/course/delete/'+id
          })
          console.log(result)
          this.getcourselist()
    
        }
        
        }
    };
    </script>
    <style scoped >
    body{
        background-image:url("@/assets/puppy.jpg");
        background-repeat:no-repeat;
        background:cover;
        background-size:cover
        
    }
    
    table {
        width: 95%;
        border-collapse: collapse;
      }
      
      th, td {
        border: 2px solid #e85d4b;
        padding: 15px;
        text-align: center;
      }
      
      th {
        background-color: #b850a1;
      }
      td {
        background-color: #7c6ddd;
      }
    #app{
      margin-top: 40px;
    }
    
    label {
      color: rgb(61, 230, 58) !important;
    }
    
    
    
    </style>