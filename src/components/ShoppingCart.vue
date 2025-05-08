<template>
    <div class="shopping-cart">
      <h3>Tu Carrito</h3>
      <ul v-if="cartItems.length > 0">
        <li v-for="(item, index) in cartItems" :key="index" class="cart-item">
          <div class="item-info">
            <span class="item-name">{{ item.name }}</span>
            <span class="item-price">${{ item.price.toFixed(2) }}</span>
          </div>
          <button class="remove-button" @click="$emit('remove-from-cart', index)">Eliminar</button>
        </li>
      </ul>
      <p v-else class="empty-cart">El carrito está vacío.</p>
      <div class="total">
        <span>Total:</span>
        <span class="total-price">${{ calculateTotal().toFixed(2) }}</span>
      </div>
      <button v-if="cartItems.length > 0" class="checkout-button">Finalizar Compra</button>
    </div>
  </template>
  
  <script>
  export default {
    name: 'ShoppingCart',
    props: {
      cartItems: {
        type: Array,
        default: () => []
      }
    },
    methods: {
      calculateTotal() {
        return this.cartItems.reduce((total, item) => total + item.price, 0);
      }
    }
  }
  </script>

<style scoped>
.shopping-cart {
  background-color: white;
  border: 1px solid #ddd;
  padding: 20px;
  margin-top: 30px;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  text-align: left;
}

.shopping-cart h3 {
  margin-top: 0;
  margin-bottom: 20px;
  font-size: 1.3em;
  color: #343a40;
  border-bottom: 2px solid #eee;
  padding-bottom: 10px;
}

.shopping-cart ul {
  list-style: none;
  padding: 0;
  margin-bottom: 20px;
}

.cart-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px 0;
  border-bottom: 1px solid #eee;
}

.cart-item:last-child {
  border-bottom: none;
}

.item-info {
  display: flex;
  justify-content: space-between;
  width: 70%; /* Ajusta según sea necesario */
  align-items: center;
}

.remove-button {
  background-color: #dc3545; /* Rojo */
  color: white;
  padding: 8px 12px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 0.8em;
  transition: background-color 0.3s ease;
}

.remove-button:hover {
  background-color: #c82333;
}

.item-name {
  font-weight: bold;
  color: #343a40;
}

.item-price {
  color: #28a745;
}

.empty-cart {
  color: #6c757d;
  font-style: italic;
}

.total {
  display: flex;
  justify-content: space-between;
  font-weight: bold;
  padding-top: 15px;
  font-size: 1.1em;
}

.total-price {
  color: #28a745;
}

.checkout-button {
  background-color: #28a745;
  color: white;
  padding: 12px 25px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 1em;
  margin-top: 20px;
  transition: background-color 0.3s ease;
  width: 100%; /* Ancho completo para el botón */
}

.checkout-button:hover {
  background-color: #1e7e34;
}
</style>