<template>
  <div class="modal" v-if="isModal">
    <div class="inner">
      <h3>{{ data[selectedMovie].title }}</h3>
      <p>영화 상세정보</p>
      <button @click="$emit('closeModal')">닫기</button>  <!-- 자식은 부모의 데이터를 변경할 수 없다. 이벤트를 발생시켜 부모에게 변경을 요청한다. -->
    </div>
  </div>
</template>
<script>
export default {
  name: "ModalComponent",
  props: {
    data: Array,
    isModal: Boolean,
    selectedMovie: Number,
  }
};
</script>
<style></style>