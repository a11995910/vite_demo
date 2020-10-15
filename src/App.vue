<template>
  <div>
    <p>{{name}}</p>
    <button @click="myname">clik</button>
    <p>{{ref.name2}}</p>
    <button @click="myname2">clik</button>

    <div>
      <button @click="myFn">change</button>
      <div>{{state.a}}</div>
      <div>{{state.gf.f.c}}</div>
    </div>
    <div>
      <button @click="shaoolwmyFn">change</button>
      <div>{{shaoolwstate.a}}</div>
      <div>{{shaoolwstate.gf.f.c}}</div>
    </div>
  </div>
</template>

<script>
// setup函数需要引入ref函数，在vue里
/**
 * setup执行时间：beforecreate 和created之间，
 * 注意⚠️：所以setup被创建好了后是无法使用data和methods的方法，尤大为了不让咱们迷糊，直接吧这里的this指向改成underfind而不是vue
 * 
*递归监听：reactive是递归监听变化的，不管多深的层级 也是可以变化的，但是耗费资源
*非递归监听：引入shallowreactive和shallowRef，使用这两个就是非递归
 */
import { ref } from 'vue';
import { reactive } from 'vue';
import {shallowReactive} from 'vue';
import {shallowRef} from 'vue';

export default {
  name: 'App',
  components: {

  },  
  data(){
    return {
      name:'asd'
    }
  },
  //composition API 和option API的混用   组合api和原生methods混用
  setup(){
    let ref = reactive({
      name2:'eee'
    })
    function myname2(){
      console.log('3a4b')
    }

    let state = reactive({
      a:'a',
      gf:{
        b:'b',
        f:{
          c:'c',
          cf:{
            d:"d"
          }
        }
      }
    });
    function myFn(){
      state.a = Math.random();
      state.gf.f.c = 2
    }
    let shaoolwstate = shallowReactive({
      a:'a',
      gf:{
        b:'b',
        f:{
          c:'c',
          cf:{
            d:"d"
          }
        }
      }
    })
    function shaoolwmyFn(){
      //当不修改第一层时，就不会更新UI，如果修改 那么大家一起执行,shallowRef的.value同理
      // shaoolwstate.a = Math.random();
      shaoolwstate.gf.f.c = 2
    }
    return {ref,myname2,state,myFn,shaoolwmyFn,shaoolwstate}
  },
  methods:{
    myname(){
      console.log('2a2b');
    }
  }
}
</script>
