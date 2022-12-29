<template>
    <div class="item">
        <input type="checkbox"
        @change="updateCheck()"
        v-model="item.completed"
        />
        <span :class="[item.completed ? 'completed': '','itemText']">
            {{ item.name }}
        </span>
        <button class="trashCan" @click="removeItem()">
            <font-awesome-icon icon="trash"/>
        </button>
    </div>
</template>

<script>

export default {
    props: ['item'],
    methods: {
        updateCheck(){
            axios.put('api/item/' + this.item.id, {
                item: this.item
            })
            .then( response => {
                if( response.status == 200){
                    this.$emit('itemchanged');
                }
            })
            .catch( error => {
                console.log( error );
            })
        },
        removeItem(){
            axios.delete('api/item/' + this.item.id, {
                item: this.item
            })
            .then( response => {
                if (response.status == 200) {
                    this.$emit('itemchanged');
                }
            })
            .catch( error => {
                console.log( error );
            })
        }
    }
}
</script>

<style scoped>
    .completed{
        color: #999;
        text-decoration: line-through;
    }
    .itemText{
        width: 100%;
        margin-left: 20px;
    }
    .item{
        display: flex;
        justify-content: center;
        align-items: center;
    }
    .trashCan{
        background: #e6e6e6;
        border: none;
        outline: none;
        color: red;
    }
</style>
