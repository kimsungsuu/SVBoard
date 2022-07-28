<template>
  <div id="app">
<!--    추가한 컴포넌트 태그 추가-->
    <regist-board></regist-board>
    <board-list></board-list>
  </div>
</template>


<script>
// 컴포넌트 import
import RegistBoard from "@/components/RegistBoard";
import BoardList from "@/components/BoardList";
import RegistForm from "@/components/RegistForm";

export default {
  name: 'App',
  //변경한 component 이름 추가
  components: {
    BoardList,
    RegistForm,
    RegistBoard,
  },
};
</script>