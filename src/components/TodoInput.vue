<template>
    <div>
        <form v-on:submit.prevent="getTodo">       
            <input type="text" v-model="newText" placeholder="할일">
            <button type="submit">
                <i class="fa-solid fa-plus"></i>
            </button>
        </form>
    </div>
</template>

<script>
    export default {
        name:'TodoInput',
        data() {
            return {
                newText: ''
            }
        },
        methods:{
            getTodo(){
                if ( this.newText ) {
                    let value = this.newText
                    // console.log(value)
                    this.$emit('addTodo', value)
                    this.newText = ''
                }
            }
        }
    }
</script>

<style lang="scss" scoped>
    form { display:flex; height:43px;
        input { flex:1; padding-left:1em; background:#555; color:#fff }
        button { width:56px; font-size:20px; 
            transition:all 0.5s; 
            &:hover { background:#999 }
        }
    }
</style>