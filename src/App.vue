<template>
  <div>
    <Navbar />
    <Event text="NEPLIX 강렬한 운명의 드라마, 경기크리처" />
    <SearchBar :data="data_temp" @searchMovie="searchMovie($event)" />
    <p>
      <button @click="showAllMovie">전체보기</button>
    </p>
    <Movies :data="data_temp" @openModal="isModal = true; selectedMovie = $event" @increseLike="increseLike($event)" />
    <Modal :data="data" :isModal="isModal" :selected-movie="selectedMovie" @closeModal="isModal = false" />
  </div>
</template>

<script>
import data from "./assets/movies"; // 영화 데이터
import Navbar from "./components/Navbar.vue";
import Event from "./components/Event.vue";
import Modal from "./components/Modal.vue";
import Movies from "./components/Movies.vue";
import SearchBar from "./components/SearchBar.vue"; // 검색창
console.log(data);

export default {
  name: "App",
  data() {
    return {
      isModal: false,
      data: data, // 원본
      data_temp: [...data], // 검색을 위한 복사본
      selectedMovie: 0, // modal에 표시할 영화의 인덱스
    };
  },
  methods: {
    increseLike(i) { // 좋아요 증가
      this.data[i].like++;
    },
    searchMovie(title) { // 검색 데이터 가져오기
      // 영화제목이 포함된 데이터를 가져옴
      this.data_temp = this.data.filter(movie => {
        return movie.title.includes(title);
      })
    },
    showAllMovie() { // 전체 데이터 가져오기
      this.data_temp = [...this.data];
    }
  },
  components: {
    Navbar: Navbar,
    Modal: Modal,
    Movies: Movies,
    Event: Event,
    SearchBar: SearchBar,
  },
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
}

body {
  max-width: 768px;
  margin: 0 auto;
  padding: 20px;
}

h1,
h2,
h3 {
  margin-bottom: 1rem;
}

p {
  margin-bottom: 0.5rem;
}

button {
  margin-right: 10px;
}

.item {
  width: 100%;
  border: 1px solid #999999;
  display: flex;
  margin-bottom: 20px;
  padding: 1rem;
}

.item figure {
  width: 30%;
  margin-right: 1rem;
}

.item img {
  width: 100%;
}

.item .info {
  width: 100%;
}

.modal {
  background: rgba(0, 0, 0, 0.7);
  position: fixed;
  left: 0;
  top: 0;
  width: 100%;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-content: center;
}

.modal .inner {
  background: #fff;
  width: 80%;
  height: 17vh;
  padding: 20px;
  border-radius: 10px;
}
</style>
