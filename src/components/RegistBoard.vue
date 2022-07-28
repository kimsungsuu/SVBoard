<template>
  <div>
<!--    글쓰기 버튼-->
    <el-button type="danger" @click="openPopup = true">글쓰기</el-button>
    <el-dialog title = "글쓰기" :visible.sync="openPopup" width="30%" center>
<!--      v-model : Dto 객체 명 -->
      <el-select v-model="category">
        <el-option value="Java">Java</el-option>
        <el-option value="Javascript">Javascript</el-option>
        <el-option value="Database">Database</el-option>
      </el-select>
      <el-input placeholder="작성자명을 입력해 주세요" v-model="writer"></el-input>
      <el-input v-model="password"></el-input>
      <el-input placeholder="제목을 입력해 주세요" v-model="title"></el-input>
      <el-input
          style="margin-top: 30px"
        placeholder="내용을 입력해주세요"
        type="textarea"
        v-model="text">
      </el-input>
      <span slot="footer" class="dialog-footer">
        <el-button type="primary" @click="registBoard()" >확인</el-button>
        <el-button @click="openPopup=false">취소</el-button>
      </span>
    </el-dialog>
  </div>

</template>

<script>
import axios from 'axios';

export default {

  name: "RegistBoard",

  //$data와 같은 기능
  data(){
    return {
      openPopup:false,
      title:'',
      text:'',
      writer: '',
      category:'',
      password:'',
    };
  },

  //입력한 parameter 값
  computed:{
    setParams(){
      const params = {
        title : this.title,
        content: this.text,
        writer: this.writer,
        category: this.category,
        password: this.password,
      };
      return params;
    },
  },

  methods:{
    registBoard(){
      axios
          .post('http://localhost:8080/boards/regist-board', this.setParams)
          .then((response) => {
            if(response.data.success){
              console.log(response);
            }
          })
          .catch(function (error){
            console.log(error);
          });
    },
  },
};
</script>

<style scoped>

</style>