<template>
  <div>
    <Section1/>
    <MoviesList :movies="movies" title="Coming soon" :initial-list-view="false"/>
    <MoviesList :movies="movies" title="Most popular" :initial-list-view="true"/>
  </div>
</template>

<script>
import axios from 'axios'

import Header from "../components/Header";
import Section1 from "../components/Section1";
import MoviesList from "../components/Movies-list";
import Footer from "../components/Footer";

export default {
    components: {
        Footer,
        MoviesList,
        Section1,
        Header
    },
    async asyncData({req, params, store}) {
        const movies = await axios.get('https://api.myjson.com/bins/p2dnz').then(res => res.data);
        return {movies}
    }
}
</script>

<style>

</style>
