<template>
    <div class="nav-section" id="navigation">
        <div class="custom-container nav">
            <ul class="nav">
                <li class="nav-item"><a href="#" class="nav-link">PHIM MỚI</a></li>
                <li class="nav-item">
                    <a href="#" class="nav-link">THỂ LOẠI</a>
                    <ul class="dropdown-list categories">
                        <li 
                        v-for="category in categories"
                        :key="category._id"
                        class="dropdown-item">
                            <a href="#"
                                @click.prevent="$emit('changeUrl', `/movie/category/${category._id}`)">
                                {{category.title}}
                            </a>
                        </li>    
                    </ul>
                </li>
                <li class="nav-item"><a href="#" class="nav-link">QUỐC GIA</a>
                    <ul class="dropdown-list countries">
                        <li 
                        v-for="country in countries"
                        :key="country._id"
                        class="dropdown-item">
                            <a href="#"
                                @click.prevent="$emit('changeUrl',`/movie/country/${country._id}`)">
                                {{country.title}}
                            </a>
                        </li>  
                    </ul>
                </li>
                <li class="nav-item"><a href="#" @click.prevent="$emit('changeUrl',`/movie/movies`)" class="nav-link">PHIM LẺ</a></li>
                <li class="nav-item"><a href="#" @click.prevent="$emit('changeUrl',`/movie/series`)" class="nav-link">PHIM BỘ</a></li>
                <li class="nav-item"><a href="#" @click.prevent="" class="nav-link">PHIM THUYẾT MINH</a></li>
                <li class="nav-item"><a href="#" @click.prevent="" class="nav-link">PHIM CHIẾU RẠP</a></li>
                <li class="nav-item"><a href="#" @click.prevent="" class="nav-link">TRAILER</a></li>
                <li class="nav-item"><a href="#" @click.prevent="" class="nav-link">TOP IMDB 2018</a></li>
            </ul>
        </div>
    </div>
</template>

<script>
    import axios from 'axios';

    export default {
        name: 'navigation',
        data () {
            return {
                getMoviesUrl: '/movie/movies',
                getSeriesUrl: '/movie/series',
                getCountriesUrl: '/country/get-all',
                getCategoriesUrl: '/category/get-all',
                categories: [],
                countries: []
            }
        },
        methods: {
            
        },
        created() {
            try {
                axios.get('http://localhost:3000' + this.getCategoriesUrl)
                .then(res => {
                    this.categories = res.data;
                });
                axios.get('http://localhost:3000' + this.getCountriesUrl)
                .then(res => {
                    this.countries = res.data;
                });
            } catch (error) {
                console.log(error);
            }
        },
        mounted() {
            dropdown();
        }
    }
</script>

<style>

</style>
