<template>
    <div class="">
        <textarea class="form-control" aria-label="With textarea" v-model="item.name"/>
        <button 
            class="mt-3 btn btn-success btn-block btn-save"
            @click="addItem()"
            icon="plus-square"
        >Salvar</button>
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
            if (this.item.name === '') {
                return;
            }

            axios.post('api/item/store', {
                item: this.item
            })
                .then(response => {
                  if (response.status === 201) {
                    this.item.name = "";
                    this.$emit('reloadlist');
                  }
                })
                .catch(error => {
                  console.log(error);
                })
        }
    }
}
</script>

<style scoped>
.btn-save{
    width:  100%;
}
</style>

