<template>
  <div id="app">
    <div class="container">
      <h1>Mi Tienda Online</h1>
      <ProductList :products="products" @add-to-cart="addToCart" />
      <h2>Carrito de Compras</h2>
      <ShoppingCart :cart-items="cart" @remove-from-cart="removeFromCart" />
    </div>
  </div>
</template>

<script>
import ProductList from './components/ProductList.vue';
import ShoppingCart from './components/ShoppingCart.vue';

export default {
  name: 'App',
  components: {
    ProductList,
    ShoppingCart
  },
  data() {
    return {
      products: [
        {
          id: 1,
          name: 'Camiseta básica',
          price: 15.99,
          image: 'https://via.placeholder.com/150/771796',
          description: 'Camiseta de algodón suave y cómoda para el uso diario.',
          sizes: ['S', 'M', 'L', 'XL'],
          colors: ['Blanco', 'Negro', 'Gris', 'Azul']
        },
        {
          id: 2,
          name: 'Pantalón vaquero',
          price: 39.99,
          image: 'https://via.placeholder.com/150/24f5ea',
          description: 'Pantalón vaquero clásico de corte recto.',
          sizes: ['28', '30', '32', '34', '36'],
          colors: ['Azul', 'Negro', 'Gris']
        },
        {
          id: 3,
          name: 'Zapatillas deportivas',
          price: 59.99,
          image: 'https://via.placeholder.com/150/f66b97',
          description: 'Zapatillas para correr de alto rendimiento con amortiguación.',
          sizes: ['37', '38', '39', '40', '41', '42'],
          colors: ['Rojo', 'Azul', 'Negro', 'Blanco']
        },
        // Agrega más productos con descripciones, tallas y colores
      ],
      cart: []
    };
  },
  methods: {
    addToCart(product) {
      this.cart.push(product);
    },
    removeFromCart(index) {
      // Elimina el item del carrito usando el índice
      this.cart.splice(index, 1);
    }
  }
}
</script>

<style>
body {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  background-color: #f8f9fa;
  margin: 0;
  padding: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh; /* Para que ocupe toda la altura de la pantalla */
}

#app {
  background-color: white;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  overflow: hidden; /* Para que el border-radius funcione correctamente con el contenido */
  margin: 20px;
}

.container {
  width: 90%;
  max-width: 1200px;
  padding: 30px;
  text-align: center;
}

@media (max-width: 600px) {
  .container {
    width: 95%; /* O un valor similar para dar más espacio en móviles */
    padding: 20px;
  }
}

h1, h2 {
  color: #343a40;
  margin-bottom: 25px;
}
</style>

<style scoped>

/* Los estilos con 'scoped' siguen aquí */
</style>