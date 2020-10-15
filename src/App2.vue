<template>
  <div>
    <p>{{count}}</p>
    <button @click="fn">button</button>
    <ul>
      <li v-for="(item,index) in state.status" 
      v-bind:key="item.id"
      @click="statestu(index)"
      >is {{index}} name:{{item.name}}</li>
    </ul>
  </div>
</template>

<script>
// setup函数需要引入ref函数，在vue里
import { ref } from 'vue';
import { reactive } from 'vue';
export default {
  name: 'App',
  components: {

  },  
  data(){
    return {

    }
  },
  //setup函数是组合API的入口函数
  setup(){
    // 定义一个叫conunt 的变量，初始值为0，变量改变后 vue会自动更新UI
    //组合API的方法、变量 要在外界使用 得return 暴漏出去
    let {
      count:count,
      fn:fn,
      state:state,
      statestu:statestu
    } = setup_ref_fuction();
    return {
      count:count,
      fn:fn,
      state:state,
      statestu:statestu
    }
  },
  methods:{
    
  }
}
//抽离功能代码块，做成独立封装形式,更可以建立独立js页面 import引入就行
/*ref和reactive区别
*ref自动加上了个value reactive没有
*更新数据的时候，ref可以直接变更，reactive需要精确到变更到哪一项a.value这样,
*/
function setup_ref_fuction(){
  let count = ref(12123);
    function fn(){
      console.log(++count.value)
    }
    let state = reactive({
      status:[
        {name:'jk',value:12,id:1},
        {name:'sd',value:22,id:2},
        {name:'qw',value:32,id:3}
      ]
    })
    function statestu(index){
      state.status = state.status.filter((item,ind)=>{ind!=index;console.log(ind)})
    }
    return {
      count:count,
      fn:fn,
      state:state,
      statestu:statestu
    }
}
</script>
