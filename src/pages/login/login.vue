<template>
  <div class="box">
    <div class="con">
      <h3>登录</h3>
      <div class="inp"><input type="text" /></div>
      <div class="inp"><input type="text" /></div>
      <div class="inp"><button>登录</button></div>
    </div>
  </div>
</template>
<script>
export default {
  components: {},
  data() {
    return {};
  },
  methods: {},
  mounted() {},
};
</script>
<style scoped>
.box {
  width: 100vw;
  height: 100vh;
  background: linear-gradient(to right, #563443, #303d60);
  overflow: hidden;
}
.con {
  width: 400px;
  height: 250px;
  background-color: #fff;
  margin: 30px auto;
  text-align: center;
  padding-top: 50px;
  border-radius: 10px;
}
.inp input{
  outline: none;
  /* border: none; */
}
.con .inp {
  width: 60%;
  height: 30px;
  margin:10px auto
}
.inp input{
    width: 100%;
    height: 30px;   
}
.inp button {
  width: 100%;
  height: 30px;
  background: #409eff;
  color: #fff;
  outline: none;
  border: none;
  margin-top: 10px;
  border-radius: 15px;
}
</style>