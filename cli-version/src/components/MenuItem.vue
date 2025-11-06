<script>
import BaseButton from "./BaseButton.vue";
import BaseButton from "./BaseButton.vue"

export default {
    name: "MenuItem",
props: {
		image: {
			type: Object,
			required: true
		},
		inStock: {
			type: Boolean,
			required: true
		},
		name: {
			type: String,
			required: true
		},
		price: {
			type: Number,
			required: true
		},
		quantity: {
			type: Number,
			defaut: 1
		}
	},    data() {
        return {
            localQuantity: this.quantity,
            onSale : false,
        }
    },
    watch: {
        quantity(newVal) {
            this.localQuantity = newVal
        }
    },
    computed: {
		generatedPrice() {
			if (this.onSale) {
				return (this.price * 0.9).toFixed(2)
			} else {
				return this.price
			}
		}
	},
    methods: {
        updateShoopingCart() {
            this.$emit("add-items-to-cart", this.quantity)
    },
},
    beforeMount() {
		const today = new Date().getDate()

		if (today % 2 === 0) {
			this.onSale = true
		}
	},
}
</script>

<template>
    <div class="menu-item">
        <img class="menu-item__image" :src="image.source" :alt="image.alt" />
        <div>
            <h3>{{ name }}</h3>
            <p>Prix : {{ generatedPrice }}</p>
            <p v-if="inStock">En stock</p>
            <p v-else>En rupture de stock</p>
            <div>
                <label :for="'add-item-quantity-' + name">Quantité : {{ localQuantity }}</label>
                <input v-model.number="localQuantity" :id="'add-item-quantity-' + name" type="number" />
                <BaseButton @click="updateShoopingCart(Number(localQuantity))">
                    Ajouter au panier
                </BaseButton>
            </div>
        </div>
    </div>
</template>

<style lang="scss">
.menu-item {
	display: flex;
	width: 500px;
	justify-content: space-between;
	margin-bottom: 30px;

	&__image {
		max-width: 300px;
	}
}
</style>