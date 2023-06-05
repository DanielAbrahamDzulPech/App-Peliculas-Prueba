<template>
  <div>
    <v-container>
      <v-row>
        <v-col
          v-for="(movie, movi) in movies"
          :key="movi"
          cols="12"
          sm="6"
          md="4"
        >
          <v-card class="mx-auto" max-width="400">
            <v-img
              class="align-end text-white"
              height="500"
              :src="'https://image.tmdb.org/t/p/w500/' + movie.poster_path"
              cover
            >
            </v-img>
            <v-card-text>
              <div class="my-2">
                <h2 class="font-weight-medium text-capitalize">
                  {{ movie.title }}
                </h2>
              </div>
              <v-btn
                :class="{ favorito: favs.includes(movie.id) }"
                @click="toggleFav(movie.id)"
              >
                Favorito
              </v-btn>
            </v-card-text>
            <v-row justify="space-around">
              <v-col cols="auto">
                <v-dialog transition="dialog-bottom-transition" width="auto">
                  <template v-slot:activator="{ props }">
                    <v-btn
                      color="orange"
                      v-bind="props"
                      @click="obtenerMovi(movie.id)"
                      >Ver mas</v-btn
                    >
                  </template>
                  <template v-slot:default="{ isActive }">
                    <v-card>
                      <v-toolbar
                        color="primary"
                        :title="'Ver mas acerca de ' + movie.title"
                      ></v-toolbar>
                      <v-card-text>
                        <div class="text-h3 pa-12">
                          <v-container>
                            <v-row>
                              <v-col cols="12" sm="6" md="4">
                                <v-img
                                  class="bg-white"
                                  width="300"
                                  :aspect-ratio="1"
                                  :src="
                                    'https://image.tmdb.org/t/p/w500/' +
                                    movieUnico.poster_path
                                  "
                                  cover
                                ></v-img>
                              </v-col>
                              <v-col cols="12" sm="6" md="8">
                                <h2
                                  class="text-h4 font-weight-bold text-capitalize"
                                >
                                  {{ movie.title }}
                                </h2>
                                <h3 class="mt-4 text-h5">
                                  {{ movie.release_date }}
                                </h3>
                                <v-chip
                                  v-for="(genero, geneu) in movieUnico.genres"
                                  :key="geneu"
                                  class="ma-2"
                                >
                                  {{ genero.name }}
                                </v-chip>
                                <h4 class="text-h6"><b>Overview</b></h4>
                                <p class="text-body-2">
                                  {{ movieUnico.overview }}
                                </p>
                                <v-chip class="ma-2 text-h6" color="primary">
                                  {{ movieUnico.vote_average.toPrecision(2) }}
                                </v-chip>
                                <v-row class="py-2">
                                  <v-col
                                    v-for="(person, people) in cast"
                                    :key="people"
                                    cols="12"
                                    sm="6"
                                    md="4"
                                  >
                                    <v-card class="mx-auto" max-width="344">
                                      <v-img
                                        :src="
                                          'https://image.tmdb.org/t/p/w500/' +
                                          person.profile_path
                                        "
                                        height="300px"
                                        cover
                                      ></v-img>

                                      <v-card-title>
                                        {{ person.name }}
                                      </v-card-title>

                                      <v-card-subtitle class="text-h6 pb-3">
                                        {{ person.character }}
                                      </v-card-subtitle>
                                    </v-card>
                                  </v-col>
                                </v-row>
                              </v-col>
                            </v-row>
                          </v-container>
                        </div>
                      </v-card-text>
                      <v-card-actions class="justify-end">
                        <v-btn
                          color="blue"
                          variant="text"
                          @click="isActive.value = false"
                          >Close</v-btn
                        >
                      </v-card-actions>
                    </v-card>
                  </template>
                </v-dialog>

                <v-row justify="space-around" class="my-2">
                  <v-col cols="auto">
                    <v-dialog
                      transition="dialog-bottom-transition"
                      width="auto"
                    >
                      <template v-slot:activator="{ props }">
                        <v-btn
                          color="green"
                          v-bind="props"
                          @click="obtenerMovi(movie.id)"
                          >Actualizar</v-btn
                        >
                      </template>
                      <template v-slot:default="{ isActive }">
                        <v-card>
                          <v-toolbar
                            color="blue"
                            title="Opening from the movie"
                          ></v-toolbar>
                          <v-card-text>
                            <div class="text-body-2 pa-12">
                              {{ movie.title }}
                            </div>

                            <div>
                              <form @submit.prevent="submit">
                                <v-text-field
                                  :value="movieUnico.title"
                                  v-model="title"
                                  label="Nombre de pelicula"
                                ></v-text-field>

                                <v-text-field
                                  :counter="7"
                                  :value="movieUnico.overview"
                                  v-model="overview"
                                  label="overview"
                                ></v-text-field>

                                <v-text-field
                                  label="Raking"
                                  :v-model="vote_average"
                                  :value="movieUnico.vote_average"
                                ></v-text-field>

                                <v-btn class="me-4" type="submit">
                                  Actualizar
                                </v-btn>
                              </form>
                            </div>
                          </v-card-text>
                          <v-card-actions class="justify-end">
                            <v-btn
                              variant="text"
                              @click="isActive.value = false"
                              >Close</v-btn
                            >
                          </v-card-actions>
                        </v-card>
                      </template>
                    </v-dialog>
                  </v-col>

                  <v-col cols="auto">
                    <v-dialog transition="dialog-top-transition" width="auto">
                      <template v-slot:activator="{ props }">
                        <v-btn color="red" v-bind="props" @click="remove(movi)"
                          >Eliminar</v-btn
                        >
                      </template>
                      <template v-slot:default="{ isActive }">
                        <v-card>
                          <v-toolbar
                            color="red"
                            title="Eliminando...."
                          ></v-toolbar>
                          <!-- :text="movieUnico.title + ' ha sido eliminado'" -->
                          <v-card-text>
                            <v-alert
                              type="success"
                              title="Eliminando Pelicula"
                              text="ha sido eliminado"
                            ></v-alert>
                            <!-- <div class="text-h2 pa-12">{{ movieUnico.title }} Eliminado</div> -->
                          </v-card-text>
                          <v-card-actions class="justify-end">
                            <v-btn
                              color="purple"
                              variant="text"
                              @click="isActive.value = false"
                              >Close</v-btn
                            >
                          </v-card-actions>
                        </v-card>
                      </template>
                    </v-dialog>
                  </v-col>
                </v-row>
              </v-col>
            </v-row>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>
<script>
import { ref, onMounted, toRefs, reactive } from "vue";
import axios from "axios";
import VueAxios from "vue-axios";
export default {
  name: "Home2",
  setup() {
    const movies = ref([]);
    const movieUnico = ref([]);
    const fecha = ref("");
    const cast = ref([]);
    const favs = ref([]);
    const movieinfo = reactive({
      title: "",
      overview: "",
      vote_average: "",
    });

    const lista = () => {
      const token =
        "eyJhbGciOiJIUzI1NiJ9.eyJhdWQiOiI0MTdjYjRkMDg3ZDYwM2VhNzI0M2M5YmZmOTZlOTcwYyIsInN1YiI6IjY0N2EzMTg2OTM4MjhlMDBmOWQ2YjYwMiIsInNjb3BlcyI6WyJhcGlfcmVhZCJdLCJ2ZXJzaW9uIjoxfQ.SxFOa584buuqa2uRoOnmaKjhgJCNdgSCwd3icAlAdPY";
      const config = {
        headers: {
          Authorization: `Bearer ${token}`,
        },
      };
      const limit = 10;
      axios
        .get(
          "https://api.themoviedb.org/3/movie/top_rated?language=es-ES",
          config
        )
        .then((response) => {
          (movies.value = response.data.results.slice(0, limit)),
            console.log(movies.value);
        });
    };

    const obtenerMovi = (idP) => {
      const token =
        "eyJhbGciOiJIUzI1NiJ9.eyJhdWQiOiI0MTdjYjRkMDg3ZDYwM2VhNzI0M2M5YmZmOTZlOTcwYyIsInN1YiI6IjY0N2EzMTg2OTM4MjhlMDBmOWQ2YjYwMiIsInNjb3BlcyI6WyJhcGlfcmVhZCJdLCJ2ZXJzaW9uIjoxfQ.SxFOa584buuqa2uRoOnmaKjhgJCNdgSCwd3icAlAdPY";
      const config = {
        headers: {
          Authorization: `Bearer ${token}`,
        },
      };
      // const id = idP;
      axios
        .get(
          "https://api.themoviedb.org/3/movie/" + idP + "?language=es-ES",
          config
        )
        .then((response) => {
          (movieUnico.value = response.data),
            (fecha.value = response.data.release_date),
            console.log(movieUnico.value);
        });

      axios
        .get("https://api.themoviedb.org/3/movie/" + idP + "/credits", config)
        .then((response) => {
          (cast.value = response.data.cast.slice(0, 5)),
            console.log(cast.value);
        });
    };

    const toggleFav = (idP) => {
      const index = favs.value.indexOf(idP);
      if (index > -1) {
        favs.value.splice(index, 1);
      } else {
        favs.value.push(idP);
        console.log(favs.value);
      }
    };

    const remove = (i) => {
      movies.value.splice(i, 1);
    };

    const addMovie = () => {
      movies.value.push({
        title: title.value,
      });
    };

    onMounted(() => {
      const token =
        "eyJhbGciOiJIUzI1NiJ9.eyJhdWQiOiI0MTdjYjRkMDg3ZDYwM2VhNzI0M2M5YmZmOTZlOTcwYyIsInN1YiI6IjY0N2EzMTg2OTM4MjhlMDBmOWQ2YjYwMiIsInNjb3BlcyI6WyJhcGlfcmVhZCJdLCJ2ZXJzaW9uIjoxfQ.SxFOa584buuqa2uRoOnmaKjhgJCNdgSCwd3icAlAdPY";
      const config = {
        headers: {
          Authorization: `Bearer ${token}`,
        },
      };
      const limit = 10;
      axios
        .get(
          "https://api.themoviedb.org/3/movie/top_rated?language=es-ES",
          config
        )
        .then((response) => {
          (movies.value = response.data.results.slice(0, limit)),
            console.log(movies.value);
        });
    });

    return {
      movies,
      movieUnico,
      cast,
      favs,
      lista,
      obtenerMovi,
      toggleFav,
      remove,
      addMovie,
      ...toRefs(movieinfo),
    };
  },
};
</script>
<style>
.favorito {
  background: red;
  color: white;
}
</style>
