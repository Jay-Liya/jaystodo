<template>
    <div class="listContainer">
        <div class="heading">
            <h1 id="title">Jays ToDo List</h1>
            <add-item
                v-on:needreload="getList()"
                />
        </div>
        <list
            :items="items"
            v-on:needreload="getList()"
            />
    </div>
</template>

<script>
import addItem from "./addItem";
import list from "./list";

export default {
    components: {
        addItem,
        list
    },
    data: function () {
        return {
            items: []
        }
    },
    methods: {
        getList() {
            axios.get('api/items')
            .then( response => {
                this.items = response.data;
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

<style>
.listContainer {
    width:400px;
    margin:auto;
}

.heading {
    background: #ccc;
    padding: 10px;
}

#title {
    text-align: center;
}
</style>
