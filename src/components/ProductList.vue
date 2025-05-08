<template>
    <div class="product-list">
      <h2>Nuestros Productos</h2>
      <div v-for="product in products" :key="product.id" class="product-card">
        <img :src="product.image" :alt="product.name">
        <h3>{{ product.name }}</h3>
        <p class="description">{{ product.description }}</p>
        <p class="price">${{ product.price.toFixed(2) }}</p>
        <div class="options">
          <div class="sizes" v-if="product.sizes && product.sizes.length > 0">
            Tallas:
            <span v-for="size in product.sizes" :key="size">{{ size }}</span>
          </div>
          <div class="colors" v-if="product.colors && product.colors.length > 0">
            Colores:
            <span v-for="color in product.colors" :key="color" :style="{ backgroundColor: getColorCode(color) }">
              {{ color }}
            </span>
          </div>
        </div>
        <button @click="$emit('add-to-cart', product)">Añadir al carrito</button>
      </div>
    </div>
  </template>
  
  <script>
export default {
  name: 'ProductList',
  props: {
    products: {
      type: Array,
      required: true
    }
  },
  methods: {
    getColorCode(colorName) {
      // Función para obtener el código de color a partir del nombre (ejemplo básico)
      const colorCodes = {
        'Blanco': '#ffffff',
        'Negro': '#000000',
        'Gris': '#808080',
        'Azul': '#0000ff',
        'Rojo': '#ff0000',
        'Verde': '#008000'
        // Agrega más colores según sea necesario
      };
      return colorCodes[colorName] || '#cccccc'; // Devuelve gris claro si no se encuentra el color
    }
  }
}
</script>
  
<style scoped>
.product-list {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 20px;
  padding: 20px;
  background-color: #f8f9fa;
  border-radius: 8px;
}

.product-card {
  background-color: white;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  padding: 20px;
  text-align: center;
  transition: transform 0.2s ease-in-out;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.product-card:hover {
  transform: scale(1.03);
}

.product-card img {
  max-width: 100%;
  height: auto;
  margin-bottom: 15px;
  border-radius: 4px;
}

.product-card h3 {
  margin-top: 0;
  margin-bottom: 10px;
  font-size: 1.2em;
  color: #343a40;
}

.product-card .description {
  font-size: 0.9em;
  color: #666;
  margin-bottom: 15px;
  text-align: left;
}

.product-card .price {
  font-size: 1.1em;
  color: #28a745;
  font-weight: bold;
  margin-bottom: 20px;
}

.product-card .options {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  margin-bottom: 20px;
  gap: 10px;
}

.product-card .sizes {
  display: flex;
  align-items: center;
  gap: 10px;
  font-size: 0.9em;
}

.product-card .sizes span {
  padding: 5px 10px;
  border: 1px solid #ddd;
  border-radius: 4px;
  background-color: #f0f0f0;
  color: #333;
}

.product-card .colors {
  display: flex;
  align-items: center;
  gap: 10px;
  font-size: 0.9em;
}

.product-card .colors span {
  width: 20px;
  height: 20px;
  border-radius: 50%;
  display: inline-block;
  margin-right: 5px;
  border: 1px solid #ccc;
}

.product-card button {
  background-color: #007bff;
  color: white;
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 1em;
  transition: background-color 0.3s ease;
  align-self: flex-start;
  width: 100%; /* Ocupar todo el ancho en pantallas pequeñas */
}

.product-card button:hover {
  background-color: #0056b3;
}

/* Para pantallas más pequeñas (móviles) */
@media (max-width: 600px) {
  .product-list {
    grid-template-columns: 1fr; /* Una sola columna en móviles */
  }

  .product-card {
    width: 100%; /* Ocupar todo el ancho de la lista */
    margin: 10px 0; /* Margen vertical */
  }
}

/* Para pantallas medianas (tabletas en vertical) */
@media (min-width: 601px) and (max-width: 900px) {
  .product-list {
    grid-template-columns: repeat(2, 1fr); /* Dos columnas en tabletas */
  }

  .product-card {
    width: calc(50% - 20px); /* Dos columnas con margen */
    margin: 10px;
  }
}
</style>