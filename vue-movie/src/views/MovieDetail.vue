<template>
    <div class="movie-detail">
        <h2> Tên Phim: {{ movie.Title }}</h2>
        <p class="year">Năm Phát Hành: {{ movie.Year }}</p>
        <img :src="movie.Poster" alt="Movie Poster" class="featured-img" />
        <p class="rated"><span> Xếp Hạng:</span> {{ movie.Rated }}</p>
        <p class="time"><span>Thời Gian Phát:</span> {{ movie.Runtime }}</p>
        <p class="genre"><span>Thể Loại:</span> {{ movie.Genre }}</p>
        <p class="lang"><span>Ngôn Ngữ:</span> {{ movie.Language }}</p>
         <p class="plot"><span>Mô Tả:</span> {{ movie.Plot }}</p>
    </div>

</template>

<script>
import { ref, onBeforeMount } from 'vue';
import { useRoute } from 'vue-router';


export default {
    setup() {
        const movie = ref({});
        const route = useRoute();
        const API = "496b5cfc";

        onBeforeMount(() => {
            fetch(`http://www.omdbapi.com/?apikey=${API}&i=${route.params.id}&plot=full`)
                .then(response => response.json())
                .then(data => {
                    movie.value = data;
                });
        });

        return {
            movie
        }
    }
}
</script>

<style lang="scss">
.movie-detail {
    padding: 30px;

    h2 {
        color: #FFF;
        font-size: 28px;
        font-weight: 600;
        margin-bottom: 16px;
    }

    .featured-img {
        display: block;
        max-width: 300px;
        margin-bottom: 16px;
    }

    p {
        color: #FFF;
        font-size: 18px;
        line-height: 1.4;
    }
span {
    color: rgb(240, 191, 100);
}
    .year {
        padding-bottom: 10px;
    }

    .rated {
        padding-bottom: 10px;
    }

    .time {
        padding-bottom: 10px;
    }

    .genre {
        padding-bottom: 10px;
    }

    .lang {
        padding-bottom: 10px;
    }
    .plot{
        padding-bottom: 10px;
    }
}

</style>