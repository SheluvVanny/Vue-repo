<template>
    <div>
        <h1>Clothing & Accessories</h1>
        <!-- Sorting Dropdown -->
        <label for="sort">Sort By:</label>
        <select v-model="sortBy" id="sort" @change="sortProducts">
            <option value="name">Name</option>
            <option value="category">Category</option>
            <option value="price">Price</option>
            <option value="stock">Stock</option>
        </select>

        <!-- Products List -->
        <div v-for="product in products" :key="product.id" class="product">
            <img :src="product.image" :alt="product.name" />
            <p><strong>{{ product.name }}</strong> - {{ product.category }}</p>
            <p>\${{ product.price }}</p>
            <p>Stock: {{ product.stock }}</p>
            <button :disabled="product.stock === 0" @click="addToCart(product)">
                Add to Cart
            </button>
        </div>
    </div>
</template>
<!--Script-->
<script>
export default {
    data() {
        return {
            products: [
                {
                    id: 1,
                    name: "T-shirt",
                    category: "Clothing",
                    price: 20,
                    stock: 10,
                    image: "tshirt.jpg",
                },
                {
                    id: 2,
                    name: "Sneakers",
                    category: "Footwear",
                    price: 50,
                    stock: 5,
                    image: "sneakers.jpg",
                },
                {
                    id: 3,
                    name: "Cap",
                    category: "Accessories",
                    price: 15,
                    stock: 8,
                    image: "cap.jpg",
                },
            ],
            sortBy: "name",
        };
    },
    methods: {
        sortProducts() {
            this.products.sort((a, b) => {
                if (this.sortBy === "price" || this.sortBy === "stock") {
                    return a[this.sortBy] - b[this.sortBy];
                }
                return a[this.sortBy].localeCompare(b[this.sortBy]);
            });
        },
        addToCart(product) {
            product.stock--;
            this.$emit("addToCart", product);
        },
    },
};
</script>
<!--Style-->
<style>
.product {
    border: 1px solid #ccc;
    padding: 10px;
    margin: 10px 0;
    border-radius: 5px;
    display: flex;
    align-items: center;
}

img {
    width: 50px;
    height: 50px;
    margin-right: 10px;
}

button {
    background-color: #007bff;
    color: white;
    border: none;
    padding: 5px 10px;
    cursor: pointer;
    border-radius: 5px;
}

button:disabled {
    background-color: #ccc;
    cursor: not-allowed;
}
</style>

