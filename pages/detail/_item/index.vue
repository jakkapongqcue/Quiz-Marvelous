<template>
  <div class="space">
    <p class="breadcrumb">
      <span @click="$router.push('/')">List</span> /
      {{ gameDetail.title }}
    </p>

    <div class="card-img">
      <!-- <img class="img" :src="gameDetail.thumbnail"></img> -->
      <v-carousel height="100%">
        <v-carousel-item
          v-for="(img, i) in imageAll"
          :key="i"
          :src="img.image"
        ></v-carousel-item>
      </v-carousel>
    </div>

    <div class="card-content">
      <p class="title">{{ gameDetail.title }}</p>
      <p class="description">{{ gameDetail.description }}</p>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'Item',
  data() {
    return {
      gameDetail: {},
      imageAll: [],
    }
  },
  validate(data) {
    return /^\d+$/.test(data.params.item)
  },
  methods: {
    loadItemDetail() {
      axios
        .get('https://free-to-play-games-database.p.rapidapi.com/api/game', {
          params: { id: this.$route.params.item },
          headers: {
            'x-rapidapi-key':
              '2a50aee9e6msh55cf8498c0e6c1ap1c932fjsn9403eb2b255d',
            'x-rapidapi-host': 'free-to-play-games-database.p.rapidapi.com',
          },
        })
        .then((res) => {
          this.gameDetail = res.data
          this.compileImg()
        })
        .catch((error) => {
          console.log(error)
        })
    },
    compileImg() {
      this.imageAll = this.gameDetail.screenshots.map((item) => {
        return { image: item.image }
      })
      this.imageAll.unshift({ image: this.gameDetail.thumbnail })
    },
  },
  created() {
    this.loadItemDetail()
  },
}
</script>

<style scoped>
.img {
  object-fit: contain;
  object-fit: cover;
  height: 100%;
  width: 100%;
}

.card-img {
  padding: 35px 35px 15px 35px;
  background-color: #fff;
  height: 560px;
}

.card-content {
  padding: 0px 35px;
  background-color: #fff;
  margin-bottom: 50px;
}

.breadcrumb {
  display: inline-block;
  text-decoration: none;
  font-family: 'PT Sans', sans-serif;
  color: #273253;
  font-size: 14px;
  font-weight: 700;
  line-height: 18px;
  cursor: default;
}
.breadcrumb span {
  cursor: pointer;
}
.title {
  height: 37px;
  margin-bottom: 15px;
}
.description {
  margin: 0;
  padding-bottom: 30px;
}
.space {
  padding-top: 25px;
  margin: 0 260px;
}

@media only screen and (max-width: 1280px) {
  .space {
    padding-top: 53px;
    margin: 0 30px;
  }
  .card-img {
    height: 460px;
  }
}
@media only screen and (max-width: 540px) {
  .space {
    padding-top: 35px;
    margin: 0 24px;
  }
  .card-img {
    padding: 15px 15px 15px 15px;
    background-color: #fff;
    height: 260px;
  }
}
@media only screen and (max-width: 376px) {
  .space {
    padding-top: 18px;
    margin: 0 24px;
  }
  .card-img {
    padding: 0;
    background-color: transparent;
    margin-bottom: 13px;
    height: 195px;
  }
  .card-content {
    padding: 20px 15px 15px 15px;
    background-color: #fff;
    border-radius: 8px;
  }
  .title {
    margin-bottom: 8px;
  }
  .description {
    padding-bottom: 20px;
  }
}
</style>
