<template>
  <nav class="navbar navbar-dark bg-dark">
    <div class="container-fluid">
      <a class="navbar-brand">Marvel</a>
      <form class="d-flex">
        <!--передача значения поиска в переменную search, trim убираем пробелы-->
        <input class="form-control me-2"
               type="search"
               placeholder="Поиск..."
               aria-label="Search"

               v-model.trim="search"
               @input="changeSearch(search)"
        >
        <button class="btn btn-outline-success" type="submit">Все</button>

      </form>
    </div>
  </nav>
</template>

<script>
    export default {
        name: "AppHeader",
        props: ['changeSearch'],
        data() {
            return {
              /*получаем данные поиска*/
              search: '',
            }
        },
    }
</script>

<style scoped>

</style>
