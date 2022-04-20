<template>
  <v-app-bar
    fixed
    app
    dense
    short
    flat
    elevation="0px"
    height="58px"
    color="#2961e2"
  >
    <div class="headers">
      <span>Morning, Kevin</span>
      <!-- <v-icon size="40" color="#fff" class="account"> -->
      <!-- mdi-account-circle -->
      <!-- </v-icon> -->
      <img
        src="../static/user-img.png"
        class="account"
      ></img>
    </div>
  </v-app-bar>
</template>

<script>
export default {
  name: 'navbar',
}
</script>

<style>
.headers {
  display: flex;
  justify-content: flex-end;
  align-items: center;
  margin: 0 249px;
  height: 58px;
  color: white;
  width: 100%;
  font-family: 'PT Sans', sans-serif;
  font-size: 17px;
  font-weight: 400;
}

@media only screen and (max-width: 1280px) {
  .headers {
    margin: 0 70px;
  }
}
@media only screen and (max-width: 540px) {
  .headers {
    margin: 0 50px;
  }
}
@media only screen and (max-width: 376px) {
  .headers {
    margin: 0 18px 0 0;
    justify-content: space-between;
  }
}
.account {
  margin-left: 41px;
  height: 40px;
  width: 40px;
}
</style>
