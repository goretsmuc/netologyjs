<template>
    <div id="app">

        <app-header/>

        <div class="container">
            <h1 class="pt-3 pb-3">Персонажи Marvel</h1>
<!--          <pre>{{characters}}</pre>-->
          <!--         передача атрибута-->
            <app-modal :character="character" />

            <spinner v-if="loading"/>

            <div class="row">
              <!--         -->
              <div v-for="(element, idx) in characters"
                   :key="element.id"
                   class="card mb-3 clo-sm-12 clo-md-6 col-lg-4"
              >
                <div class="row g-0">
                  <div class="col-md-4">
                    <!--         вывод img по ключу-->
                    <img :src="element.thumbnail"
                         :alt="element.name"
                         style="max-width: 100%"
                    >
                  </div>
                  <div class="col-md-8">
                    <div class="card-body">
                      <!--        интерполяция текста-->
                      <h5 class="card-title">{{element.name}}</h5>
                      <!-- Button trigger modal -->
                      <button @click="characterIndex = idx"
                              type="button"
                              class="btn btn-secondary btn-sm"
                              data-bs-toggle="modal"
                              data-bs-target="#exampleModal">
                        Подробнее
                      </button>
                    </div>
                  </div>
                </div>
              </div>
            </div>
        </div>

    </div>
</template>

<script>
    import Spinner from "./components/Spinner";
    import AppModal from "./components/AppModal";
    import AppHeader from "./components/AppHeader";

    export default {
        name: 'App',
        components: {
            AppHeader,
            AppModal,
            Spinner,
        },
        data() {
            return {
                loading: false,
                characters: [],
                characterIndex: 0,
            }
        },
        methods: {
          fetchCharacters: function () {
            fetch('https://netology-api-marvel.herokuapp.com/characters')
              .then(res => res.json())
              .then(json => this.characters = json);

          },
        },
        computed: {
          character: function () {
            return this.characters[this.characterIndex] || null;
          }
        },
      async mounted() {
          this.loading = true;
          await this.fetchCharacters();
          this.loading = false;
      }
    }
</script>

<style>

</style>
