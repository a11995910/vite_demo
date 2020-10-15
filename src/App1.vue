<template>
  <div>
    <img alt="Vue logo" src="./assets/logo.png" @click="login" />
    <form>
      <input type="text" name="" id="" v-model="lu.id">
      <input type="text" name="" id="" v-model="lu.value">
      <input type="text" name="" id="" v-model="lu.name">
      <input type="submit" @click="change">
    </form>
    <ul>
      <li v-for="(item,index) in ul" :key="item.id" @click="change(index)">{{item.name}} - {{item.value}}</li>
    </ul>
  </div>
</template>

<script>

export default {
  name: 'App',
  components: {

  },  
  data(){
    return {
      ul:[
        {name:'jk',value:12,id:1},
        {name:'sd',value:22,id:2},
        {name:'qw',value:32,id:3}
      ],
      lu:{name:'jkk',value:12,id:1}
    }
  },
  methods:{
    /**
     * vue2的写法，数据和业务逻辑分离，抽离性比较大。vue3的是可以聚合在一起，也就是组合api功能，吧多个业务逻辑聚合在一起。方便管理以及迭代开发。
     */
    login:()=>{
      console.log(1);
    },
    change(e){
      e.preventDefault();
      const stu = Object.assign({},this.lu);
      this.ul.push(stu);
    }
  }
}
</script>
