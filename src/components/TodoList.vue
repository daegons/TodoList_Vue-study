<template>
    <div id="list">
        <ul>
            <li v-for="(item, num) in todos" v-bind:key="item.id">
                <i v-bind:class="{'fa-solid':true, 'fa-pen-to-square':!item.modify, 'fa-floppy-disk':item.modify }" @click="onToggle(item.id)"></i>
                <input type="text" @input="onInput(item.id, $event)" v-bind:value="item.text" v-bind:disabled="!item.modify">  
                {{  item.id }}
                <i class="fa-solid fa-trash-can" @click="onRemove(num)"></i>
            </li>
        </ul>
    </div>
</template>

<script>
    export default {
        name:'TodoList',
        props:['todos'],
        methods:{
            onToggle(id){
                this.$emit('onToggle', id)
            },
            onInput(id, e){
                // console.log(e.target.value)
               this.$emit('onUpdate', id, e.target.value)
            },
            onRemove(num) {
                this.$emit('onRemove', num)
            }
        }
    }
</script>

<style lang="scss" scoped>
  #list { 
    ul {
        background: #fff;
        li {
            min-height:50px;
            height:50px;
            line-height:50px;
            margin:5px 0;
            padding:0 1em;
            display:flex; align-items:center;
            input { flex:1; background:none; padding:5px 5px; margin:0 5px}
        }
    }
  }
  
</style>