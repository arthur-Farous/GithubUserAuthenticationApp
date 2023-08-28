

<script setup>
import { ref } from "vue";
import axios from "axios";
import moment from "moment";

const username = ref("");
const user = ref(null);
const userNotFound = ref(false);
const loading = ref(false);

const searchUser = async () => {
  if (username.value.trim() === "") {
    alert("Please enter a GitHub username.");
    return;
  }

  console.log("Searching...");
  loading.value = true;
  try {
    const response = await axios.get(
      `https://api.github.com/users/${username.value}`
    );

    // axios automatically converts the response to JSON
    user.value = response?.data;
    loading.value = false;
    console.log(response?.data);
  } catch (error) {
    console.error("Error:", error);
    user.value = null;
    userNotFound.value = true;
    loading.value = false;
    // alert('User not found or an error occurred.');
  }
};
</script>



<template>
  <div class="container">
    <div class="headSaearch">
      <header>
        <div class="header">
          <!-- <img src="@." alt=""> -->
          <h2>devfinder</h2>
          <h5>Dark</h5>
        </div>
      </header>
      <div class="searchPlace">
        <div class="search">
          <img src="@/assets/searchIcons.png" alt="" class="searchIcon" />
          <input
            v-model="username"
            type="text"
            class="inputs"
            placeholder="Search GitHub username…"/>
          <div class="noResultsDiv">
            <p class="noResults" v-if="userNotFound">No results</p>
            <button @click="searchUser">Search</button>
          </div>
        </div>
      </div>
    </div>

    <div class="loadingComponent" v-if="loading">
      <div class="lds-roller">
        <div></div>
        <div></div>
        <div></div>
        <div></div>
        <div></div>
        <div></div>
        <div></div>
        <div></div>
      </div>
    </div>

    <div class="detailsContainer" v-if="user">
      <!-- first div -->
      <div class="firstDiv">
        <img :src="user?.avatar_url" v-if="user?.avatar_url"   alt="No Image" />
        <div class="infor">
          <h3>{{ user?.name }}</h3>
          <p>{{ user?.login }}</p>
          <h6 class="join">Joined {{ moment(user?.created_at).format("D MMM YYYY") }}</h6>
        </div>
      </div> 
      <div class="bioContainer">
        <p>{{ user?.bio || "This profile has no bio" }}</p>
      </div>
      
      <div class="repoContainer">
        <div class="repo">
          <h6>Repos</h6>
          <p>{{ user?.public_repos }}</p>
        </div>
        <div class="followers">
          <h6>Followers</h6>
          <p>{{ user?.followers }}</p>
        </div>
        <div class="following">
          <h6>Following</h6>
          <p>{{ user?.following }}</p>
        </div>
      </div>

      <div class="bottomDiv1">
        <div class="inner-subSet">
        <div class="subSet">
          <img src="@/assets/location.svg" alt="" class="icons" />
          <p>{{ user?.location || "Not Available" }}</p>
        </div>
        <div class="subSet">
          <img src="@/assets/twitter.png" alt="" class="icons" />
          <p>{{ user?.twitter_username || "Not Available" }}</p>
        </div>
      </div>
      <div class="inner-subSet">
        <div class="subSet">
          <img src="@/assets/attacheee.png" alt="" class="icons" />
          <p>{{ user?.url  || "Not Available"}}</p>
        </div>
        <div class="subSet">
          <img src="@/assets/officeBuilding.png" alt="" class="icons" />
          <p>{{ user?.twitter_username || "Not Available" }}</p>
        </div>
      </div>
    </div>
      </div>
    </div>
</template>



<style scoped>
.container {
  height: 100vh;
  overflow: hidden;
}
.headSaearch {
  display: flex;
  flex-direction: column;
  gap: 36px;
}
.header h2 {
  font-size: 26px;
  font-weight: 700;
  line-height: 39px;
  text-align: left;
  color: #222731;
}

h3,
h4,
p {
  color: #222731;
}

.header h5 {
  font-size: 13px;
  font-weight: 700;
  line-height: 19px;
  letter-spacing: 2.5px;
  text-align: right;
  color: #4b6a9b;
}

.noResultsDiv {
  display: flex;
  gap: 5px;
  align-items: center;
  /*width: 80%;*/
}

.noResults {
  font-size: 12px;
  color: red;
}
.header {
  display: flex;
  justify-content: space-between;
}

.search {
  border-radius: 15px;
  display: flex;
  justify-content: space-between;
  background: #fefefe;
  box-shadow: 0px 16px 30px -10px rgba(70, 96, 187, 0.2);
  padding: 6.5px 7px;
}

.inputs {
  border: none;
  width: 100%;
  margin: 0px 5px;
}
.inputs:focus {
  outline: none;
}

button {
  border: none;
  background-color: #0079ff;
  border-radius: 5px;
  padding: 12.5px 18px;
  cursor: pointer;
  color: #fff;
}

.searchIcon {
  height: 20px;
  width: 20px;
  align-self: center;
  margin-top: 10px;
}

.detailsContainer {
  background-color: #fefefe;
  margin-top: 16px;
  border-radius: 10px;
  padding: 32px 24px 48px 24px;
}

.firstDiv {
  display: flex;
  gap: 20px;
  align-items: center;
}

.bioContainer {
  margin-top: 10px;
  padding-left: 24px;
  padding-right: 24px;
  max-width: 480px;
    width: 80%;
flex-shrink: 0;
}

.bioContainer p{
  color: #4B6A9B;
font-size: 13px;
font-style: normal;
font-weight: 400;
line-height: 25px; 
}
.repoContainer {
  display: flex;
  justify-content: space-evenly;
  padding: 18px 14px 19px 15px;
  background-color: #f6f8ff;
  margin-top: 20px;
  margin-bottom: 20px;
}

img {
  width: 100px;
  height: 100px;
  border-radius: 50%;
  margin-bottom: 10px;
}

.bottomDiv1 {
  display: flex;
  justify-content: space-between;
  flex-direction: column;
}

.bottomDiv1 .subSet {
  display: flex;
  gap: 10px;
  align-items: center;
}


.icons {
  width: 20px;
  height: 20px;
}

.lds-roller {
  display: inline-block;
  position: relative;
  width: 80px;
  height: 80px;
}
.lds-roller div {
  animation: lds-roller 1.2s cubic-bezier(0.5, 0, 0.5, 1) infinite;
  transform-origin: 40px 40px;
}
.lds-roller div:after {
  content: " ";
  display: block;
  position: absolute;
  width: 7px;
  height: 7px;
  border-radius: 50%;
  background: #000;
  margin: -4px 0 0 -4px;
}
.lds-roller div:nth-child(1) {
  animation-delay: -0.036s;
}
.lds-roller div:nth-child(1):after {
  top: 63px;
  left: 63px;
}
.lds-roller div:nth-child(2) {
  animation-delay: -0.072s;
}
.lds-roller div:nth-child(2):after {
  top: 68px;
  left: 56px;
}
.lds-roller div:nth-child(3) {
  animation-delay: -0.108s;
}
.lds-roller div:nth-child(3):after {
  top: 71px;
  left: 48px;
}
.lds-roller div:nth-child(4) {
  animation-delay: -0.144s;
}
.lds-roller div:nth-child(4):after {
  top: 72px;
  left: 40px;
}
.lds-roller div:nth-child(5) {
  animation-delay: -0.18s;
}
.lds-roller div:nth-child(5):after {
  top: 71px;
  left: 32px;
}
.lds-roller div:nth-child(6) {
  animation-delay: -0.216s;
}
.lds-roller div:nth-child(6):after {
  top: 68px;
  left: 24px;
}
.lds-roller div:nth-child(7) {
  animation-delay: -0.252s;
}
.lds-roller div:nth-child(7):after {
  top: 63px;
  left: 17px;
}
.lds-roller div:nth-child(8) {
  animation-delay: -0.288s;
}
.lds-roller div:nth-child(8):after {
  top: 56px;
  left: 12px;
}
@keyframes lds-roller {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

.loadingComponent {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 30%;
}
.infor h6{
  color: #697C9A;
text-align: right;
font-size: 15px;
font-style: normal;
font-weight: 400;
line-height: normal;
}

.repo p,.followers p,.following p{
  color: #2B3442;
text-align: center;
font-size: 16px;
font-style: normal;
font-weight: 700;
line-height: normal;
text-transform: uppercase;
}

.repo h6,.followers h6,.following h6{
  color: #4B6A9B;
text-align: center;
font-size: 11px;
font-style: normal;
font-weight: 400;
line-height: normal;
}

@media (min-width: 1024px) { 

  .infor{
    padding-left: 95px;
    padding-right: 60px;
  }
.infor h3{
  color: #2B3442;
font-size: 26px;
font-style: normal;
font-weight: 700;
line-height: normal;
}
.infor p{
  color: #0079FF;
font-size: 16px;
font-style: normal;
font-weight: 400;
line-height: normal;
}
  .bioContainer{
    padding-top: 10px;
    padding-left: 202px;
    padding-right: 60px;
  }
  .bioContainer p{
font-size: 15px;

}
.repoContainer{
  margin-left: 202px;
  margin-right: 48px;
}
.repo p,.followers p,.following p{
font-size: 22px;
font-style: normal;
text-transform: uppercase;
}

.repo h6,.followers h6,.following h6{
font-size: 13px;
font-weight: 400;
}

.bottomDiv1{
  padding-left: 180px;
  padding-right: 60px;
}

.infor h6{
  text-align: right;
  color: #697C9A;
font-size: 15px;
font-style: normal;
font-weight: 400;
line-height: normal;
}
.inner-subSet{
  display: flex;
 justify-content: space-between;
  gap: 30px;
  padding-right: 60px;
  padding-left: 50px;
}
.subSet p{
  color: #4B6A9B;
font-family: Space Mono;
font-size: 15px;
font-style: normal;
font-weight: 400;
line-height: normal;
}

.subSet{
  gap:15px;
  padding-top: 15px;
}

/*.detailsContainer{
  padding: 52px 202px 100px ;
}*/
}
</style>
