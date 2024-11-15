<template>
    <div>
        <h2>Shopping Cart</h2>
        <ul>
            <li v-for="item in cart" :key="item.id">
                {{ item.name }} - {{ item.quantity }}
                <button @click="removeFromCart(item)">Remove</button>
            </li>
        </ul>

        <!-- Checkout Form -->
        <form @submit.prevent="checkout">
            <input type="text" v-model="name" placeholder="Name" />
            <input type="text" v-model="phone" placeholder="Phone" />
            <button :disabled="!isValid">Checkout</button>
        </form>
    </div>
</template>

<script>
export default {
    props: ["cart"],
    data() {
        return {
            name: "",
            phone: "",
        };
    },
    computed: {
        isValid() {
            return /^[A-Za-z\s]+$/.test(this.name) && /^\d+$/.test(this.phone);
        },
    },
    methods: {
        removeFromCart(item) {
            this.$emit("removeFromCart", item);
        },
        checkout() {
            if (this.isValid) {
                alert("Order placed successfully!");
            }
        },
    },
};
</script>

<style>
form {
    margin-top: 20px;
}

input {
    display: block;
    margin-bottom: 10px;
    padding: 5px;
    border: 1px solid #ccc;
    border-radius: 5px;
}

button {
    padding: 5px 10px;
    background-color: #28a745;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
}

button:disabled {
    background-color: #ccc;
}
</style>
