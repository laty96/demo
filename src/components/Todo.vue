<template>
    <div class="todoItem">
        <div v-for="item in todosList" :key="item.id">
            <input type="checkbox" v-model="isDone">
            <input type="text" v-bind:readonly="isDone" v-bind:class="{done: isDone}" v-model="item.title">
        </div>
    </div>
</template>

<script>
export default {
    name: "Todo",
    props: {
        todosList: Object
    },
    data() {
        return {
            // todoItem: ''
        }
    },
    methods: {

    }
}
</script>
