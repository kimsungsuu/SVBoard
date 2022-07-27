<template>
  <div>
    <el-table border :data="boardList">
<!--      prop : key(Dto 객체 값), label : 이름-->
      <el-table-column prop="num" label="글번호"></el-table-column>
      <el-table-column prop="category" label="카테고리"></el-table-column>
      <el-table-column prop="title" label="제목"></el-table-column>
      <el-table-column prop="writer" label="작성자"></el-table-column>
      <el-table-column prop="hit" label="조회수"></el-table-column>
      <el-table-column prop="createDate" label="등록일"></el-table-column>
      <el-table-column prop="modDate" label="수정일"></el-table-column>
    </el-table>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'BoardList',

  data(){
    return {
      boardList : [],
    };
  },

  created() {
    this.findAll();
  },

  methods: {
    findAll(){
      axios
          //주소를 통해 백엔드에 데이터 요청
          .get('http://localhost:8080/boards')
          .then((response) => {
            //데이터를 받아오는데 성공했다면
            if(response.data.success){
              console.log(response.data.result);
              let result = response.data.result;
              //boardList 배열에 data response로 받은 데이터를 담아준다.
              this.boardList = result;
            }
          })
          .catch(function (error){
            console.log(error);
          });
      },
    },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
