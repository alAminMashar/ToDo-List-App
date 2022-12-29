<template>
   <div class="todoListContainer">
    <div class="heading">
        <h2 id="title">
            Task List
        </h2>
        <add-item-form-vue
         v-on:reloadlist="getList()"
        />
    </div>
    <list-view-vue
    :items="items"
    v-on:reloadlist="getList()"
    />
    </div>
</template>

<script>
// import { response } from 'express';
import addItemFormVue from './addItemForm.vue';
    import listViewVue from './listView.vue';

        export default {
            components: {
                addItemFormVue,
                listViewVue
            },
            data: function () {
                return {
                    items: []
                }
            },
            methods: {
                getList () {
                    axios.get('api/items')
                    .then( response => {
                        this.items = response.data
                    })
                    .catch( error => {
                            console.log( error );
                    })
                }
            },
            created() {
                this.getList();
            }
        }
</script>
<style scoped>
.todoListContainer{
        background-color: #8a8888;
        border-radius: 5px;
        width: 30%;
        margin: 25px 35% 25px;
        height: auto;
        padding: 10px 10px 5px;
        font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        box-shadow: 0px 0px 3px 0px rgba(0,0,0,.3);
        text-align: center;
    }
    .heading{
        color: #FFF;
        font-weight: 100;
        font-size: 20px;
    }
</style>
