<template>
  <div>
    <el-dialog :title="info.title" :visible.sync="info.isShow">
      <el-form :model="form">
        <el-form-item label="菜单名称" :label-width="width">
          <el-input v-model="form.title" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="上级菜单" :label-width="width">
          <el-select
            v-model="form.pid"
            placeholder="--请选择--"
            @change="changePid">
            
            <el-option label="顶级菜单" :value="0"></el-option>
            <!-- value="0"  默认内容区为0    顶级菜单--0  -->
            <!-- 动态循环添加数据  菜单分类 -->
            <el-option
              v-for="item in menuList"
              :key="item.id"
              :label="item.title"
              :value="item.id"
            ></el-option>
          </el-select>
        </el-form-item>

        <el-form-item label="菜单类型" :label-width="width">
          <el-radio v-model="form.type" :label="1" disabled>目录</el-radio>
          <el-radio v-model="form.type" :label="2" disabled>菜单</el-radio>
        </el-form-item>

        <!-- type:类型：1目录2菜单 -->
        <el-form-item
          label="菜单图标"
          :label-width="width"
          v-if="form.type == 1"
        >
          <el-select v-model="form.icon" placeholder="请选择活动区域">
            <el-option label="派大星" value="el-icon-star-on">
              <i class="el-icon-star-on"></i>
            </el-option>
            <el-option label="包包" value="el-icon-goods">
              <i class="el-icon-goods"></i>
            </el-option>
            <el-option label="饿了么" value="el-icon-eleme">
              <i class="el-icon-eleme"></i>
            </el-option>
            <el-option label="小铃铛" value="el-icon-bell">
              <i class="el-icon-bell"></i>
            </el-option>
          </el-select>
        </el-form-item>

        <!-- | status | 状态   1正常2禁用   number类型 | number | -->
        <el-form-item label="菜单地址" :label-width="width" v-else>
          <el-select v-model="form.url" placeholder="请选择活动区域">
            <el-option
              v-for="item in indexRouters"
              :key="item.path"
              :label="'/' + item.path"
              :value="item.name"
            ></el-option>
            <!-- lable:分组的组名,选项的标签，若不设置则默认与 value 相同  -->
          </el-select>
        </el-form-item>

        <!-- 设置active-value和inactive-value属性，接受Boolean, String或Number类型的值。 -->
        <!-- 1正常2禁用   active-value="1" inactive-value="2" -->
        <el-form-item label="状态" :label-width="width">
          <el-switch
            v-model="form.status"
            active-color="#13ce66"
            inactive-color="#ff4949"
            :active-value="1"
            :inactive-value="2"
          >
          </el-switch
          >{{ form.status }}
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="info.isShow = false">取 消</el-button>
        <el-button type="primary" @click="add" v-if="info.isAdd">添 加</el-button>
        <el-button type="primary" @click="updata" v-else>修 改</el-button>
      </div>
    </el-dialog>
  </div>
</template>
<script>
import { indexRouters } from "../../../router/index";
import { reqMenuAdd, reqMenuListOne,reqMenuEdit} from "../../../util/request";
import { mapGetters, mapActions } from "vuex";
export default {
  props: ["info"],
  computed: {
    ...mapGetters({
      menuList: "menu/list",
    }),
  },
  components: {},
  data() {
    return {
      width: "160px",
      //   isShow: true,
      form: {
        pid: "",
        title: "",
        type: 0,
        icon: "",
        url: "",
        status: 1,
      },
      indexRouters: indexRouters,
    };
  },
  methods: {
    //   取消弹框
    hide() {
      this.info.isShow = false;
    },
    // 重置
    empty() {
      this.form = {
        pid: "",
        title: "",
        type: 0,
        icon: "",
        url: "",
        status: 1,
      };
    },
    //  添加操作
    add() {
      reqMenuAdd(this.form).then((res) => {
        this.hide();  //弹框隐藏
        this.requestMenuList();//点击添加列表刷新
      });
    },
    // 修改type的状态
    changePid() {
      this.form.type = this.form.pid == 0 ? 1 : 2;
    },

    // 查看一条数据
    look(id) {
      reqMenuListOne({ id: id }).then((res) => {
        this.form = res.data.list;
        this.form.id = id;
      });
    },
    ...mapActions({
      requestMenuList: "menu/requestMenuList",
    }),

    //修改
    updata(){
     reqMenuEdit(this.form).then(res=>{ //内容实现
         this.requestMenuList();  //自动刷新
         this.hide();  //弹框隐藏
         this.empty();  //清空--添加按钮内容
     })
    }
  },
  mounted() {},
};
</script>
<style scoped>
</style>