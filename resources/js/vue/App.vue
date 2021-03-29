<template>
    <div class="todoListContainer">
        <div class="heading">
            <h2 id="Title"> Todo List </h2>
            <add-item-form 
                v-on:reloadlist="getList()"
            />
        </div>
        <list-view 
            :items="items" 
            v-on:reloadlist="getList()"
        />
    </div>
</template>

<script>
import AddItemForm from './AddItemForm.vue'
import ListView from './ListView.vue'

export default {
    components: {
        AddItemForm,
        ListView
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
.todoListContainer {
    width: 350px;
    margin: auto;
}

.heading {
    background: #f5f5f5;
    padding: 10px 20px;
}

.title {
    text-align: center;
}
