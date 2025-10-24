<script>

    export default { 
        // Add code in appropriate places
        data() {
            return {
                items: ['keyboard', 'mouse', 'iPhone', 'macbook', 'adapter'],
                newItem: ""
            }
        },
        methods:{
            deleteItem(id){
                this.items.splice(id, 1);
            },
            addItem(){
                this.items.push(this.newItem);
                this.newItem = "";
            }
        }
    }
</script>

<template>

    <h2>Shopping Cart</h2>
    <!-- TODO: Add Code Here -->
     <ul v-for="(name, idx) in items">
        <li>{{ name }} <button v-on:click="deleteItem(idx)">Delete</button></li>
     </ul>

     <input type="text" v-model="newItem"></input> <button v-on:click="addItem()">Add</button>
   
</template>
