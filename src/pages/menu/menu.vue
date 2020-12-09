<template>
  <div>
    <el-button type="primary" @click="willAdd">添加</el-button>
    
    <!-- 添加 -->
    <v-add :info='info' ref='one'></v-add>
    <!-- 1.ref 操作普通元素  就是获取到的dom元素
         2.ref 操作的组件    获取的就是组件的数据和方法
         3.使用ref  需要通过this.$refs来获取 -->

    <!-- 列表 -->
    <v-list @edit='edit($event)'></v-list>
    <!-- <v-list @edit='edit'></v-list> -->
  </div>
</template> 
<script>
import vAdd from "./components/add";
import vList from "./components/list";
export default {
  components: {
    vAdd,
    vList,
  },
  data() {
    return {
      info: {
        isShow: false,
         isAdd:true,  //给添加按钮增加一个标识 用来判断弹框中的按钮到底是添加还是编辑
         title:'菜单添加11'
      },
    };
  },
  methods: {
    // 点击添加
    willAdd() {
      this.info.isShow = !this.info.isShow
      this.info.isAdd = true 
      this.info.title = '菜单添加'
      this.$refs.one.empty() //点击添加按钮--清空数据
    },
    // 编辑
    edit(e){ //e形参
        // console.log(e)
        this.info.isShow = true
        this.info.isAdd = false
        this.info.title = '菜单编辑'

        console.log(this.$refs.one)
        this.$refs.one.look(e)
    }
  },
  mounted() {},
};
</script>
<style scoped>
</style>