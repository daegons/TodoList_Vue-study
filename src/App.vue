<template>
  <div id="container">
     <TodoHeader></TodoHeader>
     <TodoInput v-on:addTodo="addTodo"></TodoInput>
     <TodoList v-bind:todos="todos" v-on:onRemove="onRemove" v-on:onUpdate="onUpdate" v-on:onToggle="onToggle"></TodoList>
     <TodoFooter v-on:allRemove="allRemove"></TodoFooter>
  </div>
</template>

<script>
  import './assets/reset.css'

  import TodoHeader from './components/TodoHeader.vue'
  import TodoInput from './components/TodoInput.vue'
  import TodoList from './components/TodoList.vue'
  import TodoFooter from './components/TodoFooter.vue'

  export default {
    name:'App',
    data() {
      return {
        id:0,
        todos: []    // { id:0, text:'할일', modify:false }
      }
    },
    created(){
      // console.log(typeof localStorage.id)
      // console.log(typeof localStorage.todos)
      if (localStorage.id){
        this.id = JSON.parse(localStorage.id)
      }
      if ( localStorage.todos ) {
        let item = JSON.parse(localStorage.todos)
        this.todos = item
      }
      console.log(this.id, this.todos)
    },
    methods:{
      addTodo(text){
         this.todos.push( { id:this.id, text:text, modify:false } )
         this.id++
         localStorage.id = JSON.stringify(this.id)
         localStorage.todos = JSON.stringify(this.todos)
      },
      // 전부삭제
      allRemove(){
        this.todos.splice(0, this.todos.length)   // 배열 전체요소 삭제
        localStorage.removeItem('todos')          // 로컬스토리지의 todos(키) 삭제함
      },
      // 한개씩 삭제
      onRemove(num){
        this.todos.splice(num, 1)                 // 자식이 보내준 번호 요소 1개 삭제
        localStorage.todos = JSON.stringify(this.todos)
      },
      // 새로 수정된 내용으로 데이터 업데이트
      onUpdate(id, value){
        this.todos.map((item)=>{
          if ( item.id === id) {
            if ( value ) {
              item.text = value
            } else {
              return false
            }
          }
        })
        localStorage.todos = JSON.stringify(this.todos)
      },
      // 아이콘 토글
      onToggle(id){
        this.todos.map((item)=>{
          if (item.id===id) {
            item.modify = !item.modify     // false => true
          }
        })
        localStorage.todos = JSON.stringify(this.todos)
      }
    },
    components:{
       'TodoHeader' : TodoHeader,
       'TodoInput' : TodoInput,
       'TodoList' : TodoList,
       'TodoFooter':TodoFooter
    }
  }
</script>

<!-- scoped 속성을 가지고 있으면, css는 현재 컴포넌트의 요소에만 적용 -->
<style scoped>
    
    #container { max-width:500px; margin:50px auto; }

</style>