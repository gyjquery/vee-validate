<template>
  <div id="app">
    <form>
      <label>用户名:</label><input v-model="userName" v-validate="'required|max:6|min:2'" name="用户名" type="text" autocomplete="false">
      <span>{{ errors.first('用户名') }}</span>
      <br>
      <label>密&nbsp;&nbsp;&nbsp;码:</label><input v-model="pwd" v-validate="{required:true,min:6,max:15,regex:/^([0-9]+)$/}" name="密码" type="password">
      <span>{{ errors.first('密码') }}</span>
      <br/>
      <label>email:</label><input v-model="email" v-validate="'required|min:2|email'" name="邮箱" type="text">
      <span>{{ errors.first('邮箱') }}</span>
      <br>
      <label>身份证:</label><input v-model="userID" v-validate="{required:true,regex: /(^\d{15}$)|(^\d{18}$)|(^\d{17}(\d|X|x)$)/}" name="身份证号" type="text">
      <span>{{ errors.first('身份证号') }}</span>
      <br>
      <!--<label>身份证:</label><input v-model="userID" v-validate="{required:true,regex: /(^\d{15}$)|(^\d{18}$)|(^\d{17}(\d|X|x)$)/}" name="身份证号" type="text">-->
      <!--<span>{{ errors.first('身份证号') }}</span>-->
      <!--<br>-->
      <br/><button @click.prevent="hander">提交</button>
    </form>
  </div>
</template>

<script>
  import Vue from 'vue'
  import VeeValidate from 'vee-validate';
 export default {
  name: 'App',
  data(){
    return{
      email:'',
      userName:'',
      pwd:'',
      userID:''

    }
  },
  mounted() {
     this.Verification()  //    校验
  },
   methods:{
//    点击提交表单
     hander(){
       this.$validator.validateAll().then((msg)=>{
         if(msg){
           alert('验证成功！');
         }else{

         }
       })
     },
//    校验
     Verification(){
       VeeValidate.Validator.localize({
         zh_CN: {
           messages: {
             required: function (name) { return name + '不能为空' },
           }
         } })
       VeeValidate.Validator.extend('email',{
         getMessage: function () { return "请输入正确格式的email号！哈哈"},
         validate: function (value) {
//           自定义判断逻辑
           const x=/^[a-zA-Z0-9_.-]+@[a-zA-Z0-9-]+(\.[a-zA-Z0-9-]+)*\.[a-zA-Z0-9]{2,6}$/.test(value)
           return x
         }
       })
     }
   }
}
</script>

<style scoped>

</style>
