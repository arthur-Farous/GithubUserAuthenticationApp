<script setup>
import GitDetails from "./UserAuthentication.vue";
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
            type="text"
            class="inputs"
            placeholder="Search GitHub username…"
          />
          <button>search</button>
        </div>
      </div>
    </div>

    <!-- <GitDetails /> -->
  </div>
</template>

<style scoped>
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

.header h5 {
  font-size: 13px;
  font-weight: 700;
  line-height: 19px;
  letter-spacing: 2.5px;
  text-align: right;
  color: #4b6a9b;
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
}

button {
  border: none;
  background-color: #0079ff;
  border-radius: 5px;
  padding: 12.5px 18px;
}

.searchIcon {
  max-height: 100%;
  height: 20.04px;
  align-self: center;
}
</style>
