<template>
  <div class="space">
    <v-row class="space-item" no-gutters>
      <v-col v-for="game in gameList" :key="game.id" cols="12" sm="6" md="4">
        <nuxt-link :to="{ name: 'detail-item', params: { item: game.id } }">
          <div class="card">
            <v-row no-gutters>
              <v-col cols="5" sm="12">
                <div class="card-img">
                  <v-img :src="game.thumbnail"></v-img>
                </div>
              </v-col>
              <v-col cols="7" sm="12">
                <div class="content">
                  <p class="title hideUnderLine">{{ game.title }}</p>
                  <p class="description overflow-dis hideUnderLine">
                    {{ game.short_description }}
                  </p>
                </div>
              </v-col>
            </v-row>
          </div>
        </nuxt-link>
      </v-col>
    </v-row>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'IndexPage',
  data() {
    return {
      gameList: {},
    }
  },
  methods: {
    loadData() {
      axios
        .get('https://free-to-play-games-database.p.rapidapi.com/api/games', {
          headers: {
            'x-rapidapi-key':
              '2a50aee9e6msh55cf8498c0e6c1ap1c932fjsn9403eb2b255d',
            'x-rapidapi-host': 'free-to-play-games-database.p.rapidapi.com',
          },
        })
        .then((res) => {
          this.gameList = res.data
        })
        .catch((error) => {
          console.log(error)
        })
    },
  },
  created() {
    this.loadData()
  },
}
</script>

<style>
.card-img {
  padding: 15px;
  margin: 0;
}
.card-img div {
  border-radius: 8px;
}

.title {
  color: #273253;
  font-family: 'PT Sans', sans-serif;
  font-size: 14px;
  font-weight: 700;
  line-height: 18px;
  margin-bottom: 8px;
  display: block;
}
.description {
  color: #838383;
  font-family: 'Prompt', sans-serif;
  font-size: 11px;
  font-weight: 500;
  line-height: 17px;
  margin-bottom: 0px;
  padding-bottom: 15px;
  width: 100%;
}
</style>

<style scoped>
.hideUnderLine {
  display: inline-block;
  text-decoration: none;
  margin: 0;
}
.card {
  margin: 5px;
  background-color: #fff;
  overflow: hidden;
}
.card:hover {
  filter: drop-shadow(0 10px 8px rgb(0 0 0 / 0.04))
    drop-shadow(0 4px 3px rgb(0 0 0 / 0.1));
}

.content {
  padding: 15px 15px 15px 15px;
}
.overflow-dis {
  height: 60px;
  text-overflow: ellipsis;
  overflow: hidden;
}
.space {
  padding-top: 53px;
  margin: 0 228px;
}
@media only screen and (max-width: 1280px) {
  .space {
    padding-top: 53px;
    margin: 0 30px;
  }
}
@media only screen and (max-width: 540px) {
  .space {
    padding-top: 18px;
    margin: 0 24px;
  }
  .content {
    padding: 0px 6px 6px 0;
  }
  .card-img {
    padding: 6px;
  }
  .description {
    padding-bottom: 0px;
  }
  .overflow-dis {
    height: auto;
  }
}
</style>
