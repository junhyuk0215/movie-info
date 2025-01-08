<template>
    <div class="search-box">
        <input type="search" placeholder="검색어를 입력하세요" @change="$emit('searchMovie', $event.target.value)
        inputText = $event.target.value;
        $event.target.value = ''
            " />
        <!-- @input="inputText = $event.target.value"  -->
        <button>검색</button>
    </div>
    <p>{{ inputText }}</p>
</template>
<script>
export default {
    name: "SearchBarComponent",
    data() {
        return {
            inputText: "",
        }
    },
    props: {
        data: Array,
    },
    watch: {
        inputText(name) {
            // 입력한 영화제목이 데이터에 있는지 확인
            const findName = this.data.filter(movie => {
                return movie.title.includes(name);
            })
            if (findName.length == 0) {
                alert("검색 결과가 없습니다.");
            }
        }
    }
}
</script>
<style>
.search-box {
    display: flex;
    margin-bottom: 5px;
}

.search-box input {
    width: 200px;
    height: 30px;
    padding: 0 10px;
    border: 1px solid #ccc;
    border-radius: 5px;
}

.search-box button {
    height: 30px;
    margin-left: 10px;
    border: 1px solid #ccc;
    border-radius: 5px;
    cursor: pointer;
}
</style>