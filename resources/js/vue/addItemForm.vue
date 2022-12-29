<template>
  <div>
   <div class="addItem">
        <input type="text" v-model="item.name">
        <font-awesome-icon
        icon="plus-square"
        @click="addItem()"
        :class="[item.name ? 'active' : 'inactive', 'plus']"
        />
   </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
 data: function(){
    return{
        item: {
            name: ""
        }
    }
 },
 methods: {
    addItem(){
        if(this.item.name == ''){
            return;
        }

        axios.post('api/item/store', {
            item: this.item
        })
        .then( response => {
            if( response.status == 201){
                this.item.name = "";
                this.$emit('reloadlist')
            }
        })
        .catch( error => {
            console.log( error);
        })
    }
 }
}
</script>

<style scoped>
    .addItem{
        display:flex;
        justify-content: center;
        align-items: center;
    }

    input{
        background: white;
        border: 0px;
        outline: none;
        margin-right: 10px;
        width: 100%;
        height: 40px;
        line-height: 40px;
        border-radius: 5px;
        font-size: 18px;
        text-transform: capitalize;
    }

    .plus{
        font-size: 25px;;
    }

    .active{
        color: #00CE25;
    }

    .inactive{
        color: #CECECE;
    }
</style>
