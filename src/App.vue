 <script lang='ts' setup>
  import { ref } from 'vue';
  import Home from './components/Home.vue'
  import Message from './components/Message.vue'
  import Mine from './components/Mine.vue'

  const currnetcop = ref()

  const push: (path: string) => void = (path) => {
    history.pushState(null, "", path)
    currnetcop.value = routes.find(v => v.path === path)?.component
  }

  const routes =  [
    { path: "/home", component: Home },
    { path: "/message", component: Message },
    { path: "/mine", component: Mine },
  ]

  window.onpopstate = function() {
    currnetcop.value = routes.find(v => v.path === location.pathname)?.component    
  }


 </script>
 <template>
   <div class="app">
    <button @click="push('/home')">首页</button> | <button @click="push('/message')">消息</button> | <button @click="push('/mine')">我的</button>
    <hr>
    <component :is="currnetcop"></component>
   </div>
 </template>
  
 <style lang='scss' scoped>
 </style>
