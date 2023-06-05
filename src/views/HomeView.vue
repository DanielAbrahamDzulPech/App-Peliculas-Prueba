<template>
  <!-- <HelloWorld /> -->
  <div class="d-flex align-center flex-column">
    <div class="text-subtitle-2">Peliculas</div>
    <v-container>
      <v-row>
        <v-col v-for='movie, movi in movies' :key="movi"
          cols="12"
          sm="6"
          md="4"
        >
            <v-card width="400" :title=movie.title subtitle="This is a subtitle"
              text="This is content" class="my-4">
              <v-img
                class="align-end text-white"
                height="200"
                :src="'https://image.tmdb.org/t/p/w500/'+movie.poster_path"
                cover
              >
                <v-card-title>Top 10 Australian beaches</v-card-title>
              </v-img>
              <v-row justify="space-around">
                <v-col cols="auto">
                  <v-dialog transition="dialog-bottom-transition" width="auto">
                    <template v-slot:activator="{ props }">
                      <v-btn color="primary" v-bind="props" @click="obtenerMovi(movie.id)">Ver Informacion</v-btn>
                    </template>
                    <template v-slot:default="{ isActive }">
                      <v-card>
                        <v-toolbar color="primary" :title="'Ver mas acerca de ' + movie.title"></v-toolbar>
                        <v-card-text>
                          <div class="text-h3 pa-12">
                            <!-- :style="{ 'background-image': url('https://image.tmdb.org/t/p/w500/'+movieunico.poster_path) }" -->
                            <v-container>
                              <v-row>
                                <v-col cols="4">
                                  <v-img
                                    class="bg-white"
                                    width="300"
                                    :aspect-ratio="1"
                                    :src="'https://image.tmdb.org/t/p/w500/'+movieunico.poster_path"
                                    cover
                                  ></v-img>
                                </v-col>
                                <v-col cols="8">
                                  <h2 class="text-h4">
                                  {{ movie.title }}
                                  {{ movieunico.adult }}
                                  </h2>
                                  <h3 class="mt-4 text-h5">{{ movie.release_date }}</h3>
                                  <!-- <h4 v-for="genero, gene in movie.genre_ids" :key="gene">{{ genero }}</h4> -->
                                  <!-- <span class="ml-2" v-for="genero, geneu in movieunico.genres" :key="geneu">{{ genero.name }}</span> -->
                                  <v-chip v-for="genero, geneu in movieunico.genres" :key="geneu"
                                    class="ma-2"
                                  >
                                  {{ genero.name }}
                                  </v-chip>
                                  <p class="text-body-2"><b>Overview</b> - {{movieunico.overview}}</p>
                                  <v-btn>
                                    Editar
                                  </v-btn>
                                  <v-btn>
                                    Eliminar
                                  </v-btn>
                                  
                                </v-col>
                              </v-row>
                            </v-container>
                        </div>
                        </v-card-text>
                        <v-card-actions class="justify-end">
                          <v-btn variant="text" @click="isActive.value = false">Close</v-btn>
                        </v-card-actions>
                      </v-card>
                    </template>
                  </v-dialog>

                  <v-row justify="space-around">
                    <v-col cols="auto">
                      <v-dialog
                        transition="dialog-bottom-transition"
                        width="auto"
                      >
                        <template v-slot:activator="{ props }">
                          <v-btn
                            color="primary"
                            v-bind="props"
                          >Actualizar</v-btn>
                        </template>
                        <template v-slot:default="{ isActive }">
                          <v-card>
                            <v-toolbar
                              color="primary"
                              title="Opening from the bottom"
                            ></v-toolbar>
                            <v-card-text>
                              <div class="text-h2 pa-12">Hello world!</div>
                            </v-card-text>
                            <v-card-actions class="justify-end">
                              <v-btn
                                variant="text"
                                @click="isActive.value = false"
                              >Close</v-btn>
                            </v-card-actions>
                          </v-card>
                        </template>
                      </v-dialog>
                    </v-col>

                    <v-col cols="auto">
                      <v-dialog
                        transition="dialog-top-transition"
                        width="auto"
                      >
                        <template v-slot:activator="{ props }">
                          <v-btn
                            color="primary"
                            v-bind="props"
                          >Eliminar</v-btn>
                        </template>
                        <template v-slot:default="{ isActive }">
                          <v-card>
                            <v-toolbar
                              color="primary"
                              title="Opening from the top"
                            ></v-toolbar>
                            <v-card-text>
                              <div class="text-h2 pa-12">Hello world!</div>
                            </v-card-text>
                            <v-card-actions class="justify-end">
                              <v-btn
                                variant="text"
                                @click="isActive.value = false"
                              >Close</v-btn>
                            </v-card-actions>
                          </v-card>
                        </template>
                      </v-dialog>
                    </v-col>
                  </v-row>
                </v-col>
                <!-- <v-col cols="auto">
                  <v-dialog transition="dialog-top-transition" width="auto">
                    <template v-slot:activator="{ props }">
                      <v-btn color="primary" v-bind="props">From the top</v-btn>
                    </template>
                    <template v-slot:default="{ isActive }">
                      <v-card>
                        <v-toolbar color="primary" title="Opening from the top"></v-toolbar>
                        <v-card-text>
                          <div class="text-h2 pa-12">Hello world!</div>
                        </v-card-text>
                        <v-card-actions class="justify-end">
                          <v-btn variant="text" @click="isActive.value = false">Close</v-btn>
                        </v-card-actions>
                      </v-card>
                    </template>
                  </v-dialog>
                </v-col> -->
              </v-row>
            </v-card>
        </v-col>
      </v-row>
    </v-container>

    <div>
      <form @submit.prevent="submit">
        <v-text-field
          
          :counter="10"
          
          label="Nombre de pelicula"
        ></v-text-field>

        <v-text-field
          
          :counter="7"
          
          label="Fecha de lanzamiento"
        ></v-text-field>

        <v-text-field
          
          
          label="E-mail"
        ></v-text-field>

        <v-select
          
          :items="items"
         
          label="Select"
        ></v-select>

        <v-checkbox
         
          value="1"
          label="Option"
          type="checkbox"
        ></v-checkbox>

        <v-btn
          class="me-4"
          type="submit"
        >
          Registrar
        </v-btn>

        <v-btn @click="handleReset">
          Limpiar campos
        </v-btn>
      </form>
    </div>
  </div>
</template>

<script>
import { defineComponent } from 'vue';

// Components
import HelloWorld from '../components/HelloWorld.vue';

export default defineComponent({
  name: 'HomeView',

  data() {
    return {
      movies: [],
      movieunico: [],
      fecha: '',
    }
  },
  mounted() {
    this.getList(),
    this.getDate()
  },
  methods: {
    getList() {
      const token = 'eyJhbGciOiJIUzI1NiJ9.eyJhdWQiOiI0MTdjYjRkMDg3ZDYwM2VhNzI0M2M5YmZmOTZlOTcwYyIsInN1YiI6IjY0N2EzMTg2OTM4MjhlMDBmOWQ2YjYwMiIsInNjb3BlcyI6WyJhcGlfcmVhZCJdLCJ2ZXJzaW9uIjoxfQ.SxFOa584buuqa2uRoOnmaKjhgJCNdgSCwd3icAlAdPY';
      const config = {
        headers: {
          Authorization: `Bearer ${token}`
        }
      }
      const limit = 10;
      this.axios.get('https://api.themoviedb.org/3/movie/top_rated?language=es-ES', config).then((response) => {
        this.movies = response.data.results.slice(0, limit), console.log(this.movies)
      })
    },
    obtenerMovi(idP) {
      const token = 'eyJhbGciOiJIUzI1NiJ9.eyJhdWQiOiI0MTdjYjRkMDg3ZDYwM2VhNzI0M2M5YmZmOTZlOTcwYyIsInN1YiI6IjY0N2EzMTg2OTM4MjhlMDBmOWQ2YjYwMiIsInNjb3BlcyI6WyJhcGlfcmVhZCJdLCJ2ZXJzaW9uIjoxfQ.SxFOa584buuqa2uRoOnmaKjhgJCNdgSCwd3icAlAdPY';
      const config = {
        headers: {
          Authorization: `Bearer ${token}`
        }
      }
      const id = idP;
      this.axios.get('https://api.themoviedb.org/3/movie/'+idP + '?language=es-ES', config).then((response) => {
        this.movieunico = response.data, this.fecha = response.data.release_date, console.log(this.movieunico)
      })
    },
    getDate() {
      const date = new Date(this.fecha).toLocaleDateString('en-US', {year: 'numeric', month: '2-digit', day: '2-digit'}) // 08/19/2020 (month and day with two digits)
      console.log(date);
    },
  },

  components: {
    HelloWorld,
  },
});
</script>
