<template>
    <div class="listitem">
        <input
            type="checkbox"
            @change="updateItem()"
            v-model="item.done"
            />
        <span :class="[item.done ? 'done' : '', 'itemText']">{{ item.name }}</span>
        <button @click="deleteItem()" class="delButton" >
            <font-awesome-icon icon="trash" />
        </button>
    </div>
</template>

<script>
export default {
    props: ['item'],
    methods: {
        updateItem() {
            axios.put('api/item/' + this.item.id, {
                item: this.item
            })
            .then( response => {
                if( response.status == 200 ) {
                    this.$emit('itemchanged');
                }
            })
            .catch( error => {
                console.log( error );
            })
        },
        deleteItem() {
            axios.delete('api/item/' + this.item.id)
            .then( response => {
                if( response.status == 200 ) {
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

<style>
.done {
    text-decoration: line-through;
    color:#999;
}

.itemText {
    width: 100%;
    margin-left:20px;
}

.listitem {
    display: flex;
    justify-content: center;
    align-items: center;
}

.delButton {
    color:red;
    background: #e6e6e6;
    border:none;
    outline: none;
}
</style>
