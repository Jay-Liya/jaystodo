<template>
    <div class="addItemForm">
        <input type="text" v-model="item.name" />
        <font-awesome-icon
            icon="plus-square"
            @click="addItem()"
            :class="[ item.name ? 'active' : 'inactive', 'plus']"
        />
    </div>
</template>

<script>
export default {
    data: function () {
        return {
            item: {
                name: ""
            }
        }
    },
    methods: {
        addItem() {
            if( this.name == '') {
                return;
            }
            axios.post('api/item/store', {
                item: this.item
            })
            .then( response => {
                if( response.status == 201 ) {
                    this.item.name = "";
                    this.$emit('needreload');
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
.addItemForm {
    display: flex;
    justify-content: center;
    align-items: center;
}

.addItemForm input {
    margin-right:10px;
    background: #f7f7f7;
    ouline:none;
    padding:5px;
    border:0px;
    width:100%;
}

.plus {
    font-size:20px;
}

.active {
    color:#4CAF50;
}

.inactive {
    color:#999;
}
</style>
