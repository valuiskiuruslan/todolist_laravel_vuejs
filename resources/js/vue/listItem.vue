<template>
    <div class="item">
        <input
            type="checkbox"
            @change="updateCheck()"
            v-model="item.completed"
        />
        <span :class="[item.completed ? 'completed' : '', 'itemText']">
            {{ item.name }}
        </span>
        <button @click="removeItem()" class="trashcan">
            <font-awesome-icon  icon="trash" />
        </button>
    </div>
</template>

<script>
    export default {
        name: "listItem",
        props: ["item"],
        methods: {
            updateCheck() {
                axios.put('api/item/' + this.item.id, {
                    item: this.item
                }).then(response => {
                    if (response.status === 200) {
                        this.$emit('itemChanged');
                    }
                }).catch(error => {
                   console.log(error);
                });
            },
            removeItem() {
                axios.delete('api/item/' + this.item.id, {
                    item: this.item
                }).then(response => {
                    if (response.status === 200) {
                        this.$emit('itemChanged');
                    }
                }).catch(error => {
                    console.log(error);
                });
            }
        },
    }
</script>

<style scoped>
    .item {
        display: flex;
        align-items: center;
    }
    .completed {
        text-decoration: line-through;
        color: #999;
    }
    .itemText {
        width: 100%;
        margin-left: 5px;
    }
    .trashcan {
        background: #e6e6e6;
        border: none;
        color: #ff0000;
        outline: none;
    }
</style>
