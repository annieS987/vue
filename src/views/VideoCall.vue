<template>


  <div class="content">
  <div class="logo_and_title">
    <table>
      <tr>
        <td><img  src="../image/logo.png" alt="logo"></td>
        <td><h1>Wisdom Connect</h1></td>
      </tr>
    </table>
  </div>


  <div class="interests_container">
    <div class="interests_form">
      <div class="interests_form_header" style="margin: 30px auto"><p>Your Interest List</p></div>

      <hr>



      <div class="interests_display_container">
        <!--------Table------>

        <!--------Table------>
        <div class="interests_display_content">
          <table>
            <tr>
              <td>
                <img src="@/image/interests/basketball.jpg">
                <p>Basketball</p>
              </td>
              <td>
                <img src="@/image/interests/boardgame.jpg">
                <p>Board Game</p>
              </td>
              <td>
                <img src="@/image/interests/chess.jpg">
                <p>Chess</p>
              </td>
            </tr>
          </table>
        </div>
        <!--------Table------>
        <div class="interests_display_content">
          <table>
            <tr>
              <td>
                <img src="@/image/interests/mountaineering.jpg">
                <p>Mountaineering</p>
              </td>
              <td>
                <img src="@/image/interests/reading.jpg">
                <p>Reading</p>
              </td>
              <td>
                <img src="@/image/interests/skateboarding.jpg">
                <p>Skateboarding</p>
              </td>
            </tr>
          </table>
        </div>
        <!--------Table------>
        <div class="interests_display_content">
          <table>
            <tr>
              <td>
                <img src="@/image/interests/skiing.jpg">
                <p>Skiing</p>
              </td>
              <td>
                <img src="@/image/interests/soccer.jpg">
                <p>Soccer</p>
              </td>
              <td>
                <img src="@/image/interests/surfing.jpg">
                <p>Surfing</p>
              </td>
            </tr>
          </table>
        </div>
        <!--------Table------>
        <div class="interests_display_content">
          <table>
            <tr>
              <td>
                <img src="@/image/interests/videogame.jpg">
                <p>Video Game</p>
              </td>
              <td>
                <img src="@/image/interests/Baseball.jpg">
                <p>Baseball</p>
              </td>
              <td>
                <img src="@/image/interests/Music.jpg">
                <p>Music</p>
              </td>
            </tr>
          </table>
        </div>

      </div>
      <div class="interests_buttons">
        <table>
          <tr>
            <td><button id="remove_btn" @click="$router.push('/interestlist')">Remove</button></td>
            <td><button id="more_btn" @click="$router.push('/moreinterest')">More</button></td>
          </tr>
        </table>
      </div>


    </div>




  </div>

  </div>

</template>

<script>
import request from "@/utils/request";

export default {
  name: "InterestListRemove",
  data(){
    return{
      form: {},
      query: '',
      search: '',
      hobbyTableData:[
      ],
      profile : localStorage.getItem("profile") ? JSON.parse(localStorage.getItem("profile")) : null,
    }
  },
  computed: {
    sliceList() {
      return function (data,count) {
        if (data != undefined) {
          let index = 0;
          let arrTemp = [];
          for (let i = 0; i < data.length; i++) {
            index = parseInt(i / count);
            if (arrTemp.length <= index) {
              arrTemp.push([]);
            }
            arrTemp[index].push(data[i])
          }
          return arrTemp
        }
      }
    }
  },
  created() {
    this.load()
    console.log(this.profile);
  },
  methods:{
    refreshProfile(){
      this.profile = localStorage.getItem("profile") ? JSON.parse(localStorage.getItem("profile")) : {}
      // console.log(this.profile);
      this.privacy = this.profile.privacy;
    },
    load(){
      this.refreshProfile();
      this.getAllHobbies();
      this.getRandomHobbies();

    },
    getAllHobbies(){
      request.get("/hobby/hobbyList", {
        params: {
          profileID: this.profile.id,
        }
      }).then(res =>{
        console.log(res);
        this.hobbyTableData = res.data;
      })
    },
    getRandomHobbies(){
      request.get("/hobby/randomHobbies", {
        params: {
          profileID: this.profile.id,
        }
      }).then(res =>{
        console.log(res);
        this.randomHobbyTableData = res.data;
      })
    },
  }
}
</script>

<style scoped>
.content{
  width: 100%;
  height: 120vh;
  overflow: hidden;
  position:relative;
}
.logo_and_title{
  width: 400px;
  height: 120px;
  text-align: center;
  padding-left: 37%;
  padding-top: 2%;
  position: absolute;
}
.logo_and_title img{
  width: 80px;
}
.logo_and_title h1{
  width: 300px;
}
.interests_container{
  /* background: url('jack-finnigan-M9EctVUPrp4-unsplash.jpg') no-repeat center center fixed; */

  height: 1000px;
  position: absolute;
  padding-left: 33%;
  padding-top: 7%;
  /* background-color: #f3e6f7; */
  /* padding: 50px; */
  /* background-color: azure; */
}

.interests_form{
  width: 540px;
  height: 800px;
  /* border: 2px solid red; */
  margin:20px auto;
  text-align: center;
  border:solid 2px;
  border-color:#864a98;
  border-radius: 5px;
}
.interests_form_header p{
  font-size: 28px;
  font-weight: bold;
  color:#864a98;
  text-align: center;
}
.interests_display_header{
  margin-top: 30px;
}
.interests_display_header p{
  font-size: 18px;
  font-weight: bold;
  color:#864a98;
  text-align: center;
}

.interests_display_container{
  width: 440px;
  overflow-y:auto;
  overflow-x: hidden;
  height: 460px;
  border: solid 2px #bfa0c8;
  border-radius: 5px;
  margin-left: 50px;
  margin-top: 40px;
}

.interests_display_container::-webkit-scrollbar{
  width: 10px;
}
.interests_display_container::-webkit-scrollbar-thumb{
  background-color: #bfa0c8;
  border-radius: 5px;
}
.interests_display_container::-webkit-scrollbar-button{
  display: none;
}
.interests_display_container::-webkit-scrollbar-track{
  background-color: #f3f3f3;
}


.interests_display{
  height: 480px;
  width: 400px;
  margin-left: 70px;
  border:dotted;
  border-radius: 5px;
  border-width:2px;
  border-color: #864a98;
}

.interests_display_content{
  width: 400px;
  height: 140px;
  margin-top: 20px;
  margin-bottom: 10px;
  margin-left: 15px;
}
.interests_display_content img{
  width: 100px;
  height: 100px;
  cursor: pointer;
}

.interests_display_content td{
  width: 240px;
  height: 160px;
}
.interests_display_content tr{
  padding-top: 40px;
}

.interests_display_content p{
  font-size: 14px;
  color:#864a98;
  font-weight: bold;
  text-align: center;
}
.interests_buttons{
  margin-left: 50px;
}
#remove_btn{
  height: 44px;
  width: 215px;
  background-color: #bfa0c8;
  color: white;
  border: 0px;
  margin-top: 70px;
  font-size: 18px;
  border-radius: 5px;
}
#more_btn{
  height: 44px;
  width: 215px;
  background-color: #bfa0c8;
  color: white;
  border: 0px;
  margin-top: 70px;
  font-size: 18px;
  border-radius: 5px;
}



</style>
