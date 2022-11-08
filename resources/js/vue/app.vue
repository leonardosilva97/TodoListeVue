<template>
    <div id="app" class="container mt-5">
        <div class="row">
            <div class="col-md-6">
                <div class="text-start">
                    <h2 >Adicionar Tarefas</h2>
                    <hr/>
                    <add-item-form
                        v-on:reloadlist="getList()"
                    />
                </div>
            </div>
            <div class="col-md-6">
                <h2 >Lista Tarefas</h2>
                <hr/>
                <list-view :items="items"
                           v-on:reloadlist="getList()"
                />
            </div>
        </div>
    </div>
</template>

<script>
import addItemForm from "./addItemForm"
import listView from "./listView"


export default {
    components: {addItemForm, listView},
    data() {
        return {
            items: []
        }
    },
    methods: {
        getList() {
            axios.get('api/items')
                .then(response => {
                    this.items = response.data;
                })
                .catch(error => {
                    console.log(error);
                })
        }

    },
    created() {
        this.getList();
    }
}
</script>


