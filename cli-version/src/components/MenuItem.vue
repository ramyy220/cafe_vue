<script>
export default {
    name: "MenuItem",
    props: ["addToShoppingCart", "image", "inStock", "name", "quantity"],
    data() {
        return {
            localQuantity: this.quantity
        }
    },
    watch: {
        quantity(newVal) {
            this.localQuantity = newVal
        }
    }
}
</script>

<template>
    <div class="menu-item">
        <img class="menu-item__image" :src="image.source" :alt="image.alt" />
        <div>
            <h3>{{ name }}</h3>
            <p v-if="inStock">En stock</p>
            <p v-else>En rupture de stock</p>
            <div>
                <label :for="'add-item-quantity-' + name">Quantité : {{ localQuantity }}</label>
                <input v-model.number="localQuantity" :id="'add-item-quantity-' + name" type="number" />
                <button @click="addToShoppingCart(Number(localQuantity))">
                    Ajouter au panier
                </button>
            </div>
        </div>
    </div>
</template>

<style></style>