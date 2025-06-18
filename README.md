<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE html>
<html b:css='false' xmlns='http://www.w3.org/1999/xhtml' xmlns:b='http://www.google.com/2005/gml/b' xmlns:data='http://www.google.com/2005/gml/data' xmlns:expr='http://www.google.com/2005/gml/expr'>
<head>
<b:include data='blog' name='all-head-content'/>
<meta content='width=device-width, initial-scale=1.0' name='viewport'/>
<title>Tienda Online - Ganchos y Accesorios</title>
<b:skin><![CDATA[
/* Reset y base */
* {
  box-sizing: border-box;
}

html, body {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  margin: 0;
  padding: 0;
  color: #333;
  background-color: #f8f9fa;
  line-height: 1.6;
}

/* Variables CSS para consistencia */
:root {
  --primary-color: #ff5722;
  --primary-hover: #e64a19;
  --secondary-color: #d81b60;
  --secondary-hover: #ad1457;
  --success-color: #4caf50;
  --warning-color: #ff9800;
  --error-color: #f44336;
  --text-primary: #333;
  --text-secondary: #666;
  --text-muted: #999;
  --border-color: #ddd;
  --shadow-light: 0 2px 8px rgba(0,0,0,0.1);
  --shadow-medium: 0 4px 12px rgba(0,0,0,0.15);
  --shadow-heavy: 0 8px 24px rgba(0,0,0,0.2);
  --border-radius: 8px;
  --border-radius-lg: 12px;
  --transition: all 0.3s ease;
}

/* Header mejorado */
.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 15px 20px;
  background: white;
  box-shadow: var(--shadow-light);
  position: sticky;
  top: 0;
  z-index: 100;
  border-bottom: 1px solid var(--border-color);
}

.header .logo img {
  height: 60px;
  width: auto;
  transition: var(--transition);
}

.header .logo img:hover {
  transform: scale(1.05);
}

.header nav ul {
  list-style: none;
  display: flex;
  gap: 25px;
  margin: 0;
  padding: 0;
}

.header nav ul li a {
  text-decoration: none;
  color: var(--text-primary);
  font-weight: 600;
  transition: var(--transition);
  padding: 8px 12px;
  border-radius: var(--border-radius);
}

.header nav ul li a:hover {
  color: var(--primary-color);
  background-color: rgba(255, 87, 34, 0.1);
}

/* Cart icon mejorado */
.cart-icon {
  position: relative;
  cursor: pointer;
  font-size: 1.5rem;
  padding: 10px;
  border-radius: 50%;
  transition: var(--transition);
}

.cart-icon:hover {
  background-color: rgba(255, 87, 34, 0.1);
  transform: scale(1.1);
}

.cart-count {
  position: absolute;
  top: -5px;
  right: -5px;
  background: var(--primary-color);
  color: white;
  border-radius: 50%;
  width: 22px;
  height: 22px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 0.75rem;
  font-weight: bold;
  animation: pulse 2s infinite;
}

@keyframes pulse {
  0% { transform: scale(1); }
  50% { transform: scale(1.1); }
  100% { transform: scale(1); }
}

/* Carousel mejorado */
.carousel {
  position: relative;
  width: 100%;
  max-width: 1200px;
  margin: 20px auto;
  border-radius: var(--border-radius-lg);
  overflow: hidden;
  box-shadow: var(--shadow-medium);
}

.carousel-inner img {
  width: 100%;
  height: 300px;
  object-fit: cover;
  transition: var(--transition);
}

.carousel-item {
  position: relative;
}

.banner-text {
  position: absolute;
  bottom: 30px;
  left: 50%;
  transform: translateX(-50%);
  background: rgba(0,0,0,0.7);
  color: white;
  padding: 12px 24px;
  border-radius: 25px;
  font-weight: bold;
  cursor: pointer;
  transition: var(--transition);
  backdrop-filter: blur(10px);
  border: 2px solid rgba(255,255,255,0.2);
}

.banner-text:hover {
  background: rgba(0,0,0,0.9);
  transform: translateX(-50%) scale(1.05);
  box-shadow: var(--shadow-heavy);
}

/* Categories mejoradas */
.categories {
  display: flex;
  overflow-x: auto;
  padding: 30px 20px;
  gap: 20px;
  justify-content: center;
  scrollbar-width: none;
  -ms-overflow-style: none;
}

.categories::-webkit-scrollbar {
  display: none;
}

.category {
  flex: 0 0 auto;
  display: flex;
  flex-direction: column;
  align-items: center;
  cursor: pointer;
  transition: var(--transition);
  padding: 10px;
  border-radius: var(--border-radius-lg);
}

.category:hover {
  transform: translateY(-5px);
}

.category-image {
  width: 90px;
  height: 90px;
  border-radius: 50%;
  overflow: hidden;
  border: 3px solid transparent;
  transition: var(--transition);
  position: relative;
}

.category-image::before {
  content: '';
  position: absolute;
  inset: -3px;
  border-radius: 50%;
  background: linear-gradient(45deg, var(--primary-color), var(--secondary-color));
  opacity: 0;
  transition: var(--transition);
  z-index: -1;
}

.category.active .category-image::before,
.category:hover .category-image::before {
  opacity: 1;
}

.category-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: var(--transition);
}

.category:hover .category-image img {
  transform: scale(1.1);
}

.category-title {
  text-align: center;
  color: var(--text-primary);
  font-size: 14px;
  margin-top: 12px;
  font-weight: 600;
  transition: var(--transition);
}

.category.active .category-title,
.category:hover .category-title {
  color: var(--primary-color);
}

/* Products grid mejorado */
.products-container {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: 20px;
  padding: 20px;
  max-width: 1400px;
  margin: 0 auto;
}

.product-item {
  background: white;
  border-radius: var(--border-radius-lg);
  box-shadow: var(--shadow-light);
  overflow: hidden;
  cursor: pointer;
  transition: var(--transition);
  position: relative;
  border: 1px solid rgba(0,0,0,0.05);
}

.product-item:hover {
  transform: translateY(-8px);
  box-shadow: var(--shadow-heavy);
  border-color: var(--primary-color);
}

.product-item img {
  width: 100%;
  height: 200px;
  object-fit: cover;
  transition: var(--transition);
}

.product-item:hover img {
  transform: scale(1.05);
}

.badge-offer {
  position: absolute;
  top: 12px;
  left: 12px;
  background: linear-gradient(45deg, var(--error-color), #ff6b6b);
  color: white;
  font-size: 11px;
  font-weight: 700;
  padding: 4px 8px;
  border-radius: var(--border-radius);
  text-transform: uppercase;
  z-index: 10;
  box-shadow: var(--shadow-light);
}

.product-info {
  padding: 16px;
}

.product-info h3 {
  margin: 0 0 8px 0;
  color: var(--text-primary);
  font-size: 16px;
  font-weight: 600;
  line-height: 1.4;
  min-height: 44px;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

.product-info .price {
  margin: 12px 0;
  font-size: 20px;
  color: var(--primary-color);
  font-weight: 700;
}

.btn-add-cart {
  width: 100%;
  background: linear-gradient(45deg, var(--primary-color), var(--primary-hover));
  color: white;
  border: none;
  border-radius: var(--border-radius);
  padding: 12px;
  font-weight: 600;
  cursor: pointer;
  transition: var(--transition);
  text-transform: uppercase;
  letter-spacing: 0.5px;
  font-size: 14px;
}

.btn-add-cart:hover {
  background: linear-gradient(45deg, var(--primary-hover), var(--primary-color));
  transform: translateY(-2px);
  box-shadow: var(--shadow-medium);
}

.btn-add-cart:active {
  transform: translateY(0);
}

/* Color palette mejorada */
.color-palette {
  display: flex;
  justify-content: center;
  gap: 8px;
  margin: 12px 0;
  flex-wrap: wrap;
}

.color-circle {
  width: 24px;
  height: 24px;
  border-radius: 50%;
  border: 2px solid white;
  cursor: pointer;
  transition: var(--transition);
  box-shadow: 0 2px 4px rgba(0,0,0,0.2);
  position: relative;
}

.color-circle:hover {
  transform: scale(1.2);
  box-shadow: 0 4px 8px rgba(0,0,0,0.3);
}

.color-circle.selected {
  transform: scale(1.3);
  border-color: var(--primary-color);
  box-shadow: 0 0 0 3px rgba(255, 87, 34, 0.3);
}

/* Modales mejorados */
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0,0,0,0.6);
  backdrop-filter: blur(5px);
  z-index: 3000;
  display: flex;
  align-items: center;
  justify-content: center;
  opacity: 0;
  visibility: hidden;
  transition: var(--transition);
}

.modal-overlay.active {
  opacity: 1;
  visibility: visible;
}

.modal-content {
  background: white;
  border-radius: var(--border-radius-lg);
  max-width: 500px;
  width: 90%;
  max-height: 90vh;
  overflow-y: auto;
  position: relative;
  box-shadow: var(--shadow-heavy);
  transform: scale(0.9);
  transition: var(--transition);
}

.modal-overlay.active .modal-content {
  transform: scale(1);
}

.modal-header {
  position: sticky;
  top: 0;
  background: white;
  padding: 20px;
  border-bottom: 1px solid var(--border-color);
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.modal-close {
  background: none;
  border: none;
  font-size: 24px;
  cursor: pointer;
  color: var(--text-muted);
  transition: var(--transition);
  padding: 5px;
  border-radius: 50%;
}

.modal-close:hover {
  color: var(--text-primary);
  background-color: rgba(0,0,0,0.1);
}

/* Cart mejorado */
#cart {
  position: fixed;
  top: 0;
  right: -100%;
  width: 100%;
  max-width: 400px;
  height: 100%;
  background: white;
  box-shadow: var(--shadow-heavy);
  z-index: 2000;
  transition: var(--transition);
  display: flex;
  flex-direction: column;
}

#cart.active {
  right: 0;
}

.cart-header {
  padding: 20px;
  border-bottom: 1px solid var(--border-color);
  background: linear-gradient(45deg, var(--primary-color), var(--primary-hover));
  color: white;
}

.cart-body {
  flex: 1;
  overflow-y: auto;
  padding: 20px;
}

.cart-footer {
  padding: 20px;
  border-top: 1px solid var(--border-color);
  background: #f8f9fa;
}

.cart-item {
  display: flex;
  gap: 15px;
  padding: 15px;
  background: #f8f9fa;
  border-radius: var(--border-radius);
  margin-bottom: 15px;
  transition: var(--transition);
}

.cart-item:hover {
  background: #e9ecef;
}

.cart-item img {
  width: 60px;
  height: 60px;
  object-fit: cover;
  border-radius: var(--border-radius);
}

.cart-item-details {
  flex: 1;
}

.cart-item-name {
  font-weight: 600;
  margin-bottom: 5px;
  color: var(--text-primary);
}

.cart-item-price {
  color: var(--primary-color);
  font-weight: 600;
}

.quantity-controls {
  display: flex;
  align-items: center;
  gap: 10px;
  margin-top: 10px;
}

.quantity-btn {
  width: 30px;
  height: 30px;
  border: none;
  background: var(--primary-color);
  color: white;
  border-radius: 50%;
  cursor: pointer;
  transition: var(--transition);
  display: flex;
  align-items: center;
  justify-content: center;
}

.quantity-btn:hover {
  background: var(--primary-hover);
  transform: scale(1.1);
}

/* Formularios mejorados */
.form-group {
  margin-bottom: 20px;
}

.form-input {
  width: 100%;
  padding: 12px 16px;
  border: 2px solid var(--border-color);
  border-radius: var(--border-radius);
  font-size: 16px;
  transition: var(--transition);
  background: white;
}

.form-input:focus {
  outline: none;
  border-color: var(--primary-color);
  box-shadow: 0 0 0 3px rgba(255, 87, 34, 0.1);
}

.form-input.error {
  border-color: var(--error-color);
}

.form-input.success {
  border-color: var(--success-color);
}

/* Botones mejorados */
.btn {
  padding: 12px 24px;
  border: none;
  border-radius: var(--border-radius);
  font-weight: 600;
  cursor: pointer;
  transition: var(--transition);
  text-transform: uppercase;
  letter-spacing: 0.5px;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
}

.btn-primary {
  background: linear-gradient(45deg, var(--primary-color), var(--primary-hover));
  color: white;
}

.btn-primary:hover {
  background: linear-gradient(45deg, var(--primary-hover), var(--primary-color));
  transform: translateY(-2px);
  box-shadow: var(--shadow-medium);
}

.btn-success {
  background: linear-gradient(45deg, var(--success-color), #45a049);
  color: white;
}

.btn-success:hover {
  background: linear-gradient(45deg, #45a049, var(--success-color));
  transform: translateY(-2px);
  box-shadow: var(--shadow-medium);
}

/* Notificaciones */
.notification {
  position: fixed;
  top: 20px;
  right: 20px;
  padding: 16px 20px;
  border-radius: var(--border-radius);
  color: white;
  font-weight: 600;
  z-index: 4000;
  transform: translateX(400px);
  transition: var(--transition);
  box-shadow: var(--shadow-heavy);
}

.notification.show {
  transform: translateX(0);
}

.notification.success {
  background: linear-gradient(45deg, var(--success-color), #45a049);
}

.notification.error {
  background: linear-gradient(45deg, var(--error-color), #d32f2f);
}

.notification.warning {
  background: linear-gradient(45deg, var(--warning-color), #f57c00);
}

/* Loading spinner */
.loading-spinner {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 4000;
  background: rgba(0,0,0,0.8);
  color: white;
  padding: 20px;
  border-radius: var(--border-radius);
  display: none;
}

.spinner {
  width: 40px;
  height: 40px;
  border: 4px solid rgba(255,255,255,0.3);
  border-top: 4px solid white;
  border-radius: 50%;
  animation: spin 1s linear infinite;
  margin: 0 auto 10px;
}

@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}

/* Responsive mejorado */
@media (max-width: 768px) {
  .header {
    flex-wrap: wrap;
    padding: 10px 15px;
  }
  
  .header nav ul {
    width: 100%;
    justify-content: center;
    margin-top: 10px;
    gap: 15px;
  }
  
  .header .logo img {
    height: 45px;
  }
  
  .products-container {
    grid-template-columns: repeat(auto-fill, minmax(160px, 1fr));
    gap: 15px;
    padding: 15px;
  }
  
  .category-image {
    width: 70px;
    height: 70px;
  }
  
  .categories {
    padding: 20px 15px;
    gap: 15px;
  }
  
  #cart {
    max-width: 100%;
  }
  
  .modal-content {
    width: 95%;
    margin: 10px;
  }
}

@media (max-width: 480px) {
  .products-container {
    grid-template-columns: repeat(auto-fill, minmax(140px, 1fr));
    gap: 10px;
    padding: 10px;
  }
  
  .product-item img {
    height: 150px;
  }
  
  .category-image {
    width: 60px;
    height: 60px;
  }
  
  .banner-text {
    font-size: 14px;
    padding: 8px 16px;
  }
}

/* Mejoras de accesibilidad */
.sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  white-space: nowrap;
  border: 0;
}

/* Focus visible para navegación por teclado */
*:focus-visible {
  outline: 2px solid var(--primary-color);
  outline-offset: 2px;
}

/* Animaciones suaves para usuarios que prefieren menos movimiento */
@media (prefers-reduced-motion: reduce) {
  * {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }
}
]]></b:skin>

<!-- Preload de recursos críticos -->
<link rel="preload" href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" as="style">
<link rel="preconnect" href="https://lh3.googleusercontent.com">

<!-- Scripts optimizados -->
<script src='https://code.jquery.com/jquery-3.6.0.min.js' defer></script>
<script src='https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js' defer></script>
</head>

<body>
<!-- Header mejorado -->
<header class='header' role="banner">
  <div class="logo">
    <img alt='Logo de la tienda' src='https://lh3.googleusercontent.com/gps-cs/AIky0YUOK1y_heZD6_UmmHTc9KTq4o6s2AzES1vSi6W5i0WvonBd3-Ts-DXS0eKOqtgT_1e5e4H_NGSezIvujiKdxxOEcYgeTap-tfwuQItGSZrinwaFKubdFlg-4PmJQ2UGe-Pj7rcdWiYhqMPw=w1500-h1000-p-k-no'/>
  </div>
  
  <nav role="navigation" aria-label="Navegación principal">
    <ul>
      <li><a href="#inicio">Inicio</a></li>
      <li><a href="#productos">Productos</a></li>
      <li><a href="#ofertas">Ofertas</a></li>
      <li><a href="#contacto">Contacto</a></li>
    </ul>
  </nav>
  
  <div class="cart-icon" onclick="toggleCart()" role="button" aria-label="Abrir carrito de compras" tabindex="0">
    🛒
    <span class='cart-count' aria-label="Cantidad de productos en el carrito">0</span>
  </div>
</header>

<!-- Carousel mejorado -->
<section class='carousel' role="region" aria-label="Promociones destacadas">
  <div class='carousel-inner'>
    <div class='carousel-item active'>
      <img alt='Promoción especial de productos' src='https://pe.todomoda.com/media/wysiwyg/TM_DISNEY_STITCH_-_BANNERS_Desk_new_1.jpg' loading="lazy"/>
    </div>
    <div class='carousel-item'>
      <img alt='Nuevos productos disponibles' src='https://lh3.googleusercontent.com/gps-cs/AIky0YUd2bofobsLtUl3qONXRSiTNou1a9W74yTaVYEr6h64PAuOOqQ-g_w6Ifs8arhOVjWboOrUFEcEDZlmtSBZkgS1YjEnSIw1f3w4IZRdMBwxibVChvNz2c93C78bOxNsx68MuBmN-4iYNCg=w2000-h2000-p-k-no' loading="lazy"/>
    </div>
  </div>
  
  <div class='banner-text' id='viewAllBtn' role='button' tabindex="0" aria-label='Ver todos los productos'>
    👁️ VER TODOS LOS PRODUCTOS
  </div>
</section>

<!-- Categories mejoradas -->
<section class='categories' role="navigation" aria-label="Categorías de productos">
  <div class='category active' onclick='filterProducts("Ganchos")' role="button" tabindex="0" aria-label="Filtrar por ganchos">
    <div class='category-image'>
      <img alt='Categoría Ganchos' src='https://lh3.googleusercontent.com/gps-cs/AIky0YUGuPXaSC1mPGUKkOYa5z7JyvELvbIy0B4-WtB3tMHIKm2D6Sbg1cTWwU0MsxRJR_5lKb5t1MnVOStZk-tNPdUudQ6-h7M7ueR4l8N5IgmuOrhlNRMi0B_uohBDRomdzQUIHP7y244Zc150=w1024-h1024-p-k-no' loading="lazy"/>
    </div>
    <div class='category-title'>Ganchos</div>
  </div>
  
  <div class='category' onclick='filterProducts("GanchosNiñas")' role="button" tabindex="0" aria-label="Filtrar por ganchos para niñas">
    <div class='category-image'>
      <img alt='Categoría Ganchos Niñas' src='https://lh3.googleusercontent.com/gps-cs/AIky0YUDER3L7ISerfG6uiIU8ISdgKkibO-SXwGGNL1azb_TJ0qYIN3T7LsJyU-qc9-kQtucnOkLr5rPYtWt0fW0UL8-7RDD46bg_0JnGLkD8RSfQvGydDvq6L_ZLBoj4hnIhwHB3CEx1fPtJ58O=w1024-h1024-p-k-no' loading="lazy"/>
    </div>
    <div class='category-title'>Ganchos Niñas</div>
  </div>
  
  <div class='category' onclick='filterProducts("cerveza")' role="button" tabindex="0" aria-label="Filtrar por cerveza">
    <div class='category-image'>
      <img alt='Categoría Cerveza' src='https://lh5.googleusercontent.com/p/AF1QipPTv840Ia5cUZM77OFrOKfiEpKJgbf_5bX-50WC=w1000-h1000-p-k-no' loading="lazy"/>
    </div>
    <div class='category-title'>Cerveza</div>
  </div>
</section>

<!-- Products container -->
<main role="main">
  <section class='products-container' id='products' aria-label="Lista de productos"></section>
</main>

<!-- Modal de producto mejorado -->
<div id='product-modal' class="modal-overlay" role="dialog" aria-labelledby="modal-title" aria-hidden="true">
  <div class="modal-content">
    <div class="modal-header">
      <h2 id="modal-title">Detalles del producto</h2>
      <button class="modal-close" id='close-product-modal' aria-label="Cerrar modal">&times;</button>
    </div>
    
    <div style="padding: 20px;">
      <img id='modal-product-image' alt='Imagen del producto' style='width:100%; height:250px; object-fit:cover; border-radius:8px; margin-bottom:15px;' loading="lazy"/>
      
      <h3 id='modal-product-name' style='margin-bottom:10px; color: var(--text-primary);'></h3>
      <p id='modal-product-description' style='margin-bottom:15px; color: var(--text-secondary); line-height: 1.6;'></p>
      <p id='modal-product-rating' style='margin-bottom:10px; color: var(--warning-color);'></p>
      <p id='modal-product-price' style='font-weight:bold; font-size:24px; margin-bottom:20px; color: var(--primary-color);'></p>
      
      <div id='modal-product-colors' class='color-palette' style='margin-bottom:20px;'></div>
      
      <div class="quantity-controls" style='justify-content: center; margin-bottom:20px;'>
        <button class="quantity-btn" id='modal-quantity-decrease' aria-label="Disminuir cantidad">-</button>
        <input id='modal-quantity' type='number' value='1' min='1' readonly style='width:60px; text-align:center; padding:8px; border:2px solid var(--border-color); border-radius:var(--border-radius);'/>
        <button class="quantity-btn" id='modal-quantity-increase' aria-label="Aumentar cantidad">+</button>
      </div>
      
      <button class="btn btn-primary" id='modal-add-to-cart' style='width:100%; font-size:16px;'>
        🛒 Agregar al carrito
      </button>
    </div>
  </div>
</div>

<!-- Modal todos los productos mejorado -->
<div id='all-products-modal' class="modal-overlay" role="dialog" aria-labelledby="all-products-title" aria-hidden="true">
  <div class="modal-content" style="max-width: 1200px; width: 95%;">
    <div class="modal-header">
      <h2 id="all-products-title">Todos los Productos</h2>
      <button class="modal-close" id='close-all-products-modal' aria-label="Cerrar modal">&times;</button>
    </div>
    
    <div style="padding: 20px;">
      <div class="form-group">
        <input class="form-input" id='all-products-search' placeholder='🔍 Buscar producto por nombre...' type='text' aria-label="Buscar productos"/>
      </div>
      <section class='products-container' id='all-products-container' aria-label="Todos los productos"></section>
    </div>
  </div>
</div>

<!-- Carrito mejorado -->
<aside id='cart' role="complementary" aria-label="Carrito de compras">
  <div class="cart-header">
    <h2 style='margin:0; display:flex; align-items:center; gap:10px;'>
      🛒 Carrito de Compras
    </h2>
  </div>
  
  <div class="cart-body">
    <div class="form-group">
      <label for="client-name" class="sr-only">Nombre del cliente</label>
      <input class="form-input" id='client-name' placeholder='Nombre completo' type='text' required aria-describedby="name-help"/>
      <small id="name-help" style="color: var(--text-muted); font-size: 12px;">Ingrese su nombre completo</small>
    </div>
    
    <div class="form-group">
      <label for="client-dni" class="sr-only">DNI del cliente</label>
      <input class="form-input" id='client-dni' placeholder='DNI (8 dígitos)' type='text' maxlength='8' pattern='[0-9]{8}' required aria-describedby="dni-help"/>
      <small id="dni-help" style="color: var(--text-muted); font-size: 12px;">Ingrese su DNI de 8 dígitos</small>
    </div>
    
    <div id='cart-items'></div>
  </div>
  
  <div class="cart-footer">
    <p id='cart-total' style='font-size:20px; font-weight:bold; margin:0 0 15px 0; text-align:center; color: var(--text-primary);'></p>
    <button class="btn btn-success" id='order-button' style='width:100%; font-size:16px;'>
      📱 Realizar Pedido por WhatsApp
    </button>
  </div>
</aside>

<!-- Overlay para cerrar carrito -->
<div id="cart-overlay" style="display:none; position:fixed; top:0; left:0; width:100%; height:100%; background:rgba(0,0,0,0.5); z-index:1999;" onclick="toggleCart()"></div>

<!-- Loading spinner mejorado -->
<div class="loading-spinner" id='loading-spinner'>
  <div class="spinner"></div>
  <div>Procesando...</div>
</div>

<!-- Container para notificaciones -->
<div id="notifications-container"></div>

<script>
// Datos de productos mejorados
const products = [
  // Ganchos
  {
    id: 1,
    name: 'Maxilazos - 5 Colores',
    category: 'Ganchos',
    price: 7.00,
    image: 'https://lh3.googleusercontent.com/gps-cs/AIky0YXdnjCFtJm5EhEvClhpsqjsYwwH2Xdqql3H45tWmgLdhiRX--KLwloCAl85SxTImNaOYYbS1MOrlGYrDwH31YoIyFBBn7KapQIKbAHVfoyNmbRBjjgmF0_SefXWn6udgSSaO19kdNtmnQBd=w2000-h2000-p-k-no',
    description: 'Maxilazos vibrantes y duraderos con una mezcla de cinco colores llamativos, perfectos para peinados versátiles.',
    colors: ['#ffeb3b', '#d32f2f', '#e1bee7', '#145a32', '#d6eaf8'],
    rating: 4.5
  },
  {
    id: 2,
    name: 'Mini Gancho Corazón',
    category: 'Ganchos',
    price: 2.50,
    image: 'https://lh3.googleusercontent.com/gps-cs/AIky0YUd2bofobsLtUl3qONXRSiTNou1a9W74yTaVYEr6h64PAuOOqQ-g_w6Ifs8arhOVjWboOrUFEcEDZlmtSBZkgS1YjEnSIw1f3w4IZRdMBwxibVChvNz2c93C78bOxNsx68MuBmN-4iYNCg=w2000-h2000-p-k-no',
    description: 'Delicados clips en forma de corazón en tonos neutros elegantes, ideales para acentos sutiles.',
    rating: 4.2
  },
  {
    id: 3,
    name: 'Ganchos Navideños',
    category: 'Ganchos',
    price: 4.00,
    image: 'https://lh3.googleusercontent.com/gps-cs/AIky0YV8A_P0YjCC6AIfC2B6HFvCKobK0UJZjVWMnzr6lfYPVXUk0gsszvJXojCK_ycIVH0cOD1-Qw3ICj1Bi9eLIf2TH0ZFaL14TuisJOWESznCPwqs2AAn_lgVOo2yGLhrKuG1yjgsGrWPIZ0k=w2000-h2000-p-k-no',
    description: 'Clips festivos con temática navideña en colores clásicos de temporada.',
    colors: ['#FFFFFF', '#FF0000', '#008000'],
    rating: 4.8
  },
  {
    id: 4,
    name: 'Gancho Hawaiano',
    category: 'Ganchos',
    price: 5.00,
    image: 'https://lh3.googleusercontent.com/gps-cs/AIky0YVaD4OrbInMGPZXKiKtKplaYEn2Ck-9KCl8p9FJbJIXPMWFCDw9Dd5lrbO-8FfXeJZKvIEr-K5UpFwrCnofgtR30imdZTojz2gxrHqZLSM3qody1gDhWdXAm_C4le7hQ4zKL3imga1TIh_j=w2000-h2000-p-k-no',
    description: 'Clips amarillos brillantes inspirados en Hawái, evocando playas soleadas y vibraciones tropicales.',
    colors: ['#FFD700'],
    rating: 4.3
  },
  {
    id: 5,
    name: 'Ganchos Acrílicos Color Celeste',
    category: 'Ganchos',
    price: 5.00,
    image: 'https://lh3.googleusercontent.com/gps-cs/AIky0YXULCa-2ZSbLgwDDlphVpkyxIs_jH2pp8AIHp25rY65c3VTGPdLnesGcrtuCiDtLbovSHvwiSUpzfWiwyle1UmqeO6d0OEvhBLqp_6k4YBo2QzMGd9aduXbKMXqGVHIB0FKSWvBYE1FNgj_=w2000-h2000-p-k-no',
    description: 'Clips acrílicos ligeros en azul cielo y blanco, ofreciendo un look fresco y moderno.',
    colors: ['#5dade2', '#ebf5fb', '#FFFFFF'],
    rating: 4.6
  },
  // GanchosNiñas
  {
    id: 14,
    name: 'Par de mini ganchitos en forma de flor',
    category: 'GanchosNiñas',
    price: 3.00,
    image: 'https://lh3.googleusercontent.com/gps-cs/AIky0YVcDqGO_EKNry0Eb-BkdsNH0V0lOhwW7AM5WEqz8IiNlbpTs2U3Io9_kt4yCGgt5haYI5RgwRDHv-LMBqc5bvmX245QMyriwIoyJyniPQH9cJJ9iCC2fC8hY06M9BU9nFd6NhCLGVGCC34N=w2000-h2000-p-k-no',
    description: 'Mini clips en forma de flor, ideales para detalles sutiles en peinados.',
    rating: 4.4
  },
  {
    id: 15,
    name: 'Mini ganchitos en forma de mariposa',
    category: 'GanchosNiñas',
    price: 2.00,
    image: 'https://lh3.googleusercontent.com/gps-cs/AIky0YW1eFtqiwT_PM-xOZnd2iVogh-XQVJclLEtgsh0i5wUGm9NvOCot9LJLfDmZE58abznArTin0EgjEMw3HuKeK9_9hoODK0kla3nM-GYGSvA8_xXCBmu_qiSuoHzgpSaO_2EtqXLAjnCs34l=w2000-h2000-p-k-no',
    description: 'Encantadores clips en forma de mariposa, agregando un toque juguetón y caprichoso.',
    rating: 4.7
  },
  {
    id: 16,
    name: 'Ligas colores pasteles y fuertes',
    category: 'GanchosNiñas',
    price: 1.00,
    image: 'https://lh3.googleusercontent.com/gps-cs/AIky0YVwhLWhfaBVh3ChmdRjktxd6WCi7W6fTmz2_7TvWPHTT_-3tX1zci-DGspLNMmn3SpAYgh9RN5G_lHRBehTbWzF16lZ9CNiBbjgj5-EVSXMU3aVjCsYaPQ5Maahznx9Fi79zzSnwLxM_nkC=w2000-h2000-p-k-no',
    description: 'Ligas elásticas duraderas en colores pastel y vibrantes, versátiles y cómodas.',
    rating: 4.1
  },
  // Cerveza
  {
    id: 13,
    name: 'Cusqueña Dorada 12-Pack 620ml',
    category: 'cerveza',
    price: 38.00,
    image: 'https://lh5.googleusercontent.com/p/AF1QipNoTsJrETd6q5R_4NE-3J7NFqBZ2_lDVDz_qgFP=w1000-h1000-p-k-no',
    description: 'Cerveza lager peruana con 5% ABV, de color dorado claro y sabor refrescante.',
    rating: 4.5
  },
  {
    id: 20,
    name: 'Cusqueña Dorada 6-Pack 355ml',
    category: 'cerveza',
    price: 22.00,
    image: 'https://lh5.googleusercontent.com/p/AF1QipPxFbOmsmYehzvFwrsgO7n7sYIVmGNIhbyIkTfB=w1000-h1000-p-k-no',
    description: 'Cerveza lager peruana ligera y equilibrada con 5% ABV.',
    rating: 4.3
  }
];

// Mapeo de colores mejorado
const colorNames = {
  '#ffeb3b': 'Amarillo',
  '#d32f2f': 'Rojo Oscuro', 
  '#e1bee7': 'Lila',
  '#145a32': 'Verde Oscuro',
  '#d6eaf8': 'Celeste Claro',
  '#FFFFFF': 'Blanco',
  '#FF0000': 'Rojo',
  '#008000': 'Verde',
  '#FFD700': 'Dorado',
  '#5dade2': 'Azul Claro',
  '#ebf5fb': 'Celeste'
};

// Variables globales
let cart = JSON.parse(localStorage.getItem('cart')) || [];
let modalQuantity = 1;
let modalCurrentProduct = null;
let selectedColor = null;

// Utilidades mejoradas
const utils = {
  formatCurrency: (amount) => `S/ ${parseFloat(amount).toFixed(2)}`,
  
  debounce: (func, wait) => {
    let timeout;
    return function executedFunction(...args) {
      const later = () => {
        clearTimeout(timeout);
        func(...args);
      };
      clearTimeout(timeout);
      timeout = setTimeout(later, wait);
    };
  },
  
  showNotification: (message, type = 'success') => {
    const notification = document.createElement('div');
    notification.className = `notification ${type}`;
    notification.textContent = message;
    
    const container = document.getElementById('notifications-container') || document.body;
    container.appendChild(notification);
    
    setTimeout(() => notification.classList.add('show'), 100);
    
    setTimeout(() => {
      notification.classList.remove('show');
      setTimeout(() => container.removeChild(notification), 300);
    }, 3000);
  },
  
  showLoading: () => document.getElementById('loading-spinner').style.display = 'block',
  hideLoading: () => document.getElementById('loading-spinner').style.display = 'none',
  
  validateForm: (formData) => {
    const errors = [];
    
    if (!formData.name || formData.name.trim().length < 2) {
      errors.push('El nombre debe tener al menos 2 caracteres');
    }
    
    if (!formData.dni || !/^\d{8}$/.test(formData.dni)) {
      errors.push('El DNI debe tener exactamente 8 dígitos');
    }
    
    return errors;
  }
};

// Renderizado de productos mejorado
function renderProducts(containerId = 'products') {
  const container = document.getElementById(containerId);
  if (!container) return;
  
  let productsHTML = '';
  
  products.forEach(product => {
    const rating = product.rating ? '⭐'.repeat(Math.floor(product.rating)) : '';
    const colorsHTML = product.colors ? 
      `<div class='color-palette'>
        ${product.colors.slice(0, 4).map(color => 
          `<span class='color-circle' style='background-color: ${color};' title='${colorNames[color] || color}'></span>`
        ).join('')}
        ${product.colors.length > 4 ? `<span style="font-size:12px; color: var(--text-muted);">+${product.colors.length - 4}</span>` : ''}
      </div>` : '';
    
    productsHTML += `
      <article class='product-item ${product.category}' data-id='${product.id}' role="button" tabindex="0" aria-label="Ver detalles de ${product.name}">
        <div class='badge-offer'>Oferta</div>
        <img alt='${product.name}' src='${product.image}' loading="lazy"/>
        <div class='product-info'>
          <h3>${product.name}</h3>
          <p class='description' style='display:none;'>${product.description}</p>
          <div class='rating' style='font-size:14px; margin:5px 0;'>${rating} ${product.rating ? `(${product.rating})` : ''}</div>
          <p class='price'>${utils.formatCurrency(product.price)}</p>
          ${colorsHTML}
          <button class='btn-add-cart' data-id='${product.id}' aria-label="Agregar ${product.name} al carrito">
            🛒 Agregar
          </button>
        </div>
      </article>
    `;
  });
  
  container.innerHTML = productsHTML;
}

// Gestión del carrito mejorada
function updateCart() {
  const cartItemsContainer = document.getElementById('cart-items');
  const cartTotal = document.getElementById('cart-total');
  const cartCount = document.querySelector('.cart-count');
  
  if (!cartItemsContainer || !cartTotal || !cartCount) return;
  
  let cartItemsHTML = '';
  let total = 0;
  let itemCount = 0;
  
  if (cart.length === 0) {
    cartItemsHTML = `
      <div style="text-align:center; padding:40px 20px; color: var(--text-muted);">
        <div style="font-size:48px; margin-bottom:16px;">🛒</div>
        <p>Tu carrito está vacío</p>
        <p style="font-size:14px;">Agrega algunos productos para comenzar</p>
      </div>
    `;
  } else {
    cart.forEach((item, index) => {
      const colorDisplay = item.color ? (colorNames[item.color] || item.color) : 'Sin color';
      const itemTotal = item.price * item.quantity;
      
      cartItemsHTML += `
        <div class='cart-item'>
          <img alt='${item.name}' src='${item.image}' loading="lazy"/>
          <div class='cart-item-details'>
            <div class='cart-item-name'>${item.name}</div>
            <div style='font-size:12px; color: var(--text-muted); margin:2px 0;'>Color: ${colorDisplay}</div>
            <div class='cart-item-price'>${utils.formatCurrency(item.price)} c/u</div>
            <div class="quantity-controls">
              <button class="quantity-btn decrease-quantity" data-index="${index}" aria-label="Disminuir cantidad">-</button>
              <span style="min-width:30px; text-align:center; font-weight:600;">${item.quantity}</span>
              <button class="quantity-btn increase-quantity" data-index="${index}" aria-label="Aumentar cantidad">+</button>
              <button class="btn" style="background:var(--error-color); color:white; padding:5px 8px; font-size:12px; margin-left:10px;" onclick="removeFromCart(${index})" aria-label="Eliminar producto">🗑️</button>
            </div>
            <div style='font-weight:600; color: var(--primary-color); margin-top:5px;'>
              Subtotal: ${utils.formatCurrency(itemTotal)}
            </div>
          </div>
        </div>
      `;
      
      total += itemTotal;
      itemCount += item.quantity;
    });
  }
  
  cartItemsContainer.innerHTML = cartItemsHTML;
  cartTotal.textContent = `Total: ${utils.formatCurrency(total)}`;
  cartCount.textContent = itemCount;
  
  // Guardar en localStorage
  localStorage.setItem('cart', JSON.stringify(cart));
  
  // Actualizar estado del botón de pedido
  const orderButton = document.getElementById('order-button');
  if (orderButton) {
    orderButton.disabled = cart.length === 0;
    orderButton.style.opacity = cart.length === 0 ? '0.5' : '1';
  }
}

// Funciones del carrito
function addToCart(product, quantity = 1, color = null) {
  const existingIndex = cart.findIndex(item => 
    item.id === product.id && item.color === color
  );
  
  if (existingIndex >= 0) {
    cart[existingIndex].quantity += quantity;
  } else {
    cart.push({
      id: product.id,
      name: product.name,
      price: product.price,
      image: product.image,
      quantity: quantity,
      color: color
    });
  }
  
  updateCart();
  utils.showNotification(`${product.name} agregado al carrito`, 'success');
}

function removeFromCart(index) {
  if (index >= 0 && index < cart.length) {
    const item = cart[index];
    cart.splice(index, 1);
    updateCart();
    utils.showNotification(`${item.name} eliminado del carrito`, 'warning');
  }
}

function updateQuantity(index, change) {
  if (index >= 0 && index < cart.length) {
    cart[index].quantity += change;
    if (cart[index].quantity <= 0) {
      removeFromCart(index);
    } else {
      updateCart();
    }
  }
}

// Gestión de modales mejorada
function openModal(modalId) {
  const modal = document.getElementById(modalId);
  if (modal) {
    modal.classList.add('active');
    modal.setAttribute('aria-hidden', 'false');
    document.body.style.overflow = 'hidden';
  }
}

function closeModal(modalId) {
  const modal = document.getElementById(modalId);
  if (modal) {
    modal.classList.remove('active');
    modal.setAttribute('aria-hidden', 'true');
    document.body.style.overflow = '';
  }
}

// Filtrado de productos mejorado
function filterProducts(category) {
  const products = document.querySelectorAll('.product-item');
  const categories = document.querySelectorAll('.category');
  
  // Actualizar productos visibles
  products.forEach(product => {
    if (category === 'all' || product.classList.contains(category)) {
      product.style.display = 'block';
    } else {
      product.style.display = 'none';
    }
  });
  
  // Actualizar categorías activas
  categories.forEach(cat => cat.classList.remove('active'));
  const activeCategory = document.querySelector(`[onclick*="${category}"]`);
  if (activeCategory) {
    activeCategory.classList.add('active');
  }
}

// Toggle del carrito mejorado
function toggleCart() {
  const cart = document.getElementById('cart');
  const overlay = document.getElementById('cart-overlay');
  
  if (cart.classList.contains('active')) {
    cart.classList.remove('active');
    overlay.style.display = 'none';
    document.body.style.overflow = '';
  } else {
    cart.classList.add('active');
    overlay.style.display = 'block';
    document.body.style.overflow = 'hidden';
  }
}

// Búsqueda mejorada con debounce
const searchProducts = utils.debounce((searchTerm) => {
  const products = document.querySelectorAll('#all-products-container .product-item');
  const term = searchTerm.toLowerCase();
  
  products.forEach(product => {
    const name = product.querySelector('h3').textContent.toLowerCase();
    const description = product.querySelector('.description')?.textContent.toLowerCase() || '';
    
    if (name.includes(term) || description.includes(term)) {
      product.style.display = 'block';
    } else {
      product.style.display = 'none';
    }
  });
}, 300);

// Event listeners mejorados
document.addEventListener('DOMContentLoaded', function() {
  // Renderizar productos iniciales
  renderProducts();
  renderProducts('all-products-container');
  updateCart();
  
  // Filtrar por primera categoría
  filterProducts('Ganchos');
  
  // Event listeners para productos
  document.addEventListener('click', function(e) {
    // Agregar al carrito desde botón
    if (e.target.classList.contains('btn-add-cart')) {
      e.stopPropagation();
      const productId = parseInt(e.target.dataset.id);
      const product = products.find(p => p.id === productId);
      if (product) {
        addToCart(product);
      }
      return;
    }
    
    // Abrir modal de producto
    if (e.target.closest('.product-item') && !e.target.classList.contains('btn-add-cart')) {
      const productItem = e.target.closest('.product-item');
      const productId = parseInt(productItem.dataset.id);
      const product = products.find(p => p.id === productId);
      
      if (product) {
        modalCurrentProduct = product;
        
        // Llenar modal
        document.getElementById('modal-product-image').src = product.image;
        document.getElementById('modal-product-name').textContent = product.name;
        document.getElementById('modal-product-description').textContent = product.description;
        document.getElementById('modal-product-price').textContent = utils.formatCurrency(product.price);
        
        // Rating
        const ratingElement = document.getElementById('modal-product-rating');
        if (product.rating) {
          ratingElement.textContent = `⭐ ${product.rating}/5`;
          ratingElement.style.display = 'block';
        } else {
          ratingElement.style.display = 'none';
        }
        
        // Colores
        const colorsContainer = document.getElementById('modal-product-colors');
        if (product.colors && product.colors.length > 0) {
          colorsContainer.innerHTML = product.colors.map(color => 
            `<span class='color-circle' data-color='${color}' style='background-color: ${color};' title='${colorNames[color] || color}' role="button" tabindex="0" aria-label="Seleccionar color ${colorNames[color] || color}"></span>`
          ).join('');
          colorsContainer.style.display = 'flex';
        } else {
          colorsContainer.style.display = 'none';
        }
        
        // Reset valores
        modalQuantity = 1;
        selectedColor = null;
        document.getElementById('modal-quantity').value = modalQuantity;
        
        openModal('product-modal');
      }
    }
    
    // Seleccionar color en modal
    if (e.target.classList.contains('color-circle') && e.target.dataset.color) {
      document.querySelectorAll('#modal-product-colors .color-circle').forEach(circle => {
        circle.classList.remove('selected');
      });
      e.target.classList.add('selected');
      selectedColor = e.target.dataset.color;
    }
    
    // Controles de cantidad en carrito
    if (e.target.classList.contains('increase-quantity')) {
      const index = parseInt(e.target.dataset.index);
      updateQuantity(index, 1);
    }
    
    if (e.target.classList.contains('decrease-quantity')) {
      const index = parseInt(e.target.dataset.index);
      updateQuantity(index, -1);
    }
  });
  
  // Controles de cantidad en modal
  document.getElementById('modal-quantity-increase').addEventListener('click', () => {
    modalQuantity++;
    document.getElementById('modal-quantity').value = modalQuantity;
  });
  
  document.getElementById('modal-quantity-decrease').addEventListener('click', () => {
    if (modalQuantity > 1) {
      modalQuantity--;
      document.getElementById('modal-quantity').value = modalQuantity;
    }
  });
  
  // Agregar al carrito desde modal
  document.getElementById('modal-add-to-cart').addEventListener('click', () => {
    if (modalCurrentProduct) {
      addToCart(modalCurrentProduct, modalQuantity, selectedColor);
      closeModal('product-modal');
    }
  });
  
  // Cerrar modales
  document.getElementById('close-product-modal').addEventListener('click', () => {
    closeModal('product-modal');
  });
  
  document.getElementById('close-all-products-modal').addEventListener('click', () => {
    closeModal('all-products-modal');
  });
  
  // Ver todos los productos
  document.getElementById('viewAllBtn').addEventListener('click', () => {
    openModal('all-products-modal');
  });
  
  // Búsqueda de productos
  document.getElementById('all-products-search').addEventListener('input', (e) => {
    searchProducts(e.target.value);
  });
  
  // Validación de formulario en tiempo real
  const nameInput = document.getElementById('client-name');
  const dniInput = document.getElementById('client-dni');
  
  nameInput.addEventListener('input', (e) => {
    const value = e.target.value.trim();
    if (value.length >= 2) {
      e.target.classList.remove('error');
      e.target.classList.add('success');
    } else {
      e.target.classList.remove('success');
      if (value.length > 0) e.target.classList.add('error');
    }
  });
  
  dniInput.addEventListener('input', (e) => {
    const value = e.target.value;
    // Solo permitir números
    e.target.value = value.replace(/\D/g, '');
    
    if (/^\d{8}$/.test(e.target.value)) {
      e.target.classList.remove('error');
      e.target.classList.add('success');
    } else {
      e.target.classList.remove('success');
      if (e.target.value.length > 0) e.target.classList.add('error');
    }
  });
  
  // Procesar pedido
  document.getElementById('order-button').addEventListener('click', () => {
    const clientName = nameInput.value.trim();
    const clientDni = dniInput.value.trim();
    
    const errors = utils.validateForm({ name: clientName, dni: clientDni });
    
    if (errors.length > 0) {
      utils.showNotification(errors[0], 'error');
      return;
    }
    
    if (cart.length === 0) {
      utils.showNotification('El carrito está vacío', 'warning');
      return;
    }
    
    // Generar boleta
    generateReceipt(clientName, clientDni);
  });
  
  // Cerrar modales con Escape
  document.addEventListener('keydown', (e) => {
    if (e.key === 'Escape') {
      closeModal('product-modal');
      closeModal('all-products-modal');
      if (document.getElementById('cart').classList.contains('active')) {
        toggleCart();
      }
    }
  });
  
  // Navegación por teclado
  document.addEventListener('keydown', (e) => {
    if (e.key === 'Enter' || e.key === ' ') {
      if (e.target.hasAttribute('role') && e.target.getAttribute('role') === 'button') {
        e.preventDefault();
        e.target.click();
      }
    }
  });
});

// Generar boleta mejorada
function generateReceipt(clientName, clientDni) {
  const fecha = new Date();
  const fechaStr = fecha.toLocaleDateString('es-PE');
  const horaStr = fecha.toLocaleTimeString('es-PE', { hour: '2-digit', minute: '2-digit' });
  const total = cart.reduce((sum, item) => sum + item.price * item.quantity, 0);
  
  const enLetras = (n) => {
    const parts = n.toFixed(2).split('.');
    return `${Number(parts[0])} CON ${parts[1]}/100 SOLES`;
  };
  
  let boletaHTML = `
    <div style='font-family: monospace; font-size: 14px; line-height: 1.4; max-width: 400px; margin: 0 auto; background: white; padding: 20px; border-radius: 10px;'>
      <h3 style='text-align: center; margin-bottom: 20px; color: var(--text-primary);'>BOLETA DE VENTA ELECTRÓNICA</h3>
      
      <div style='text-align: center; margin: 20px 0; padding: 15px; background: #f8f9fa; border-radius: 8px;'>
        <img src='https://i.ibb.co/Kz9NwFym/yape-qr.jpg' style='width: 200px; border-radius: 10px; box-shadow: var(--shadow-light);' alt="Código QR para pago"/>
        <p style='margin: 10px 0 5px; font-size: 12px; color: var(--text-secondary);'>💳 Paga aquí con Yape</p>
        <p style='margin: 0; font-size: 12px; font-weight: 600; color: var(--text-primary);'>Jhonny David Palacios Gutierrez</p>
      </div>
      
      <div style='margin: 20px 0; padding: 15px; background: #f8f9fa; border-radius: 8px;'>
        <p style='margin: 5px 0;'><strong>CLIENTE:</strong> ${clientName}</p>
        <p style='margin: 5px 0;'><strong>DNI:</strong> ${clientDni}</p>
        <p style='margin: 5px 0;'><strong>FECHA:</strong> ${fechaStr} <strong>HORA:</strong> ${horaStr}</p>
      </div>
      
      <hr style='border: none; border-top: 2px solid var(--border-color); margin: 20px 0;'/>
      
      <div style='margin: 15px 0;'>
        <div style='display: flex; justify-content: space-between; font-weight: bold; margin-bottom: 10px; padding-bottom: 5px; border-bottom: 1px solid var(--border-color);'>
          <span>PRODUCTO</span>
          <span>TOTAL</span>
        </div>
  `;
  
  cart.forEach(item => {
    const colorDisplay = item.color ? (colorNames[item.color] || item.color) : '';
    const itemTotal = item.price * item.quantity;
    
    boletaHTML += `
      <div style='display: flex; justify-content: space-between; margin: 8px 0; padding: 8px; background: white; border-radius: 4px;'>
        <div style='flex: 1;'>
          <div style='font-weight: 600; font-size: 12px;'>${item.name}</div>
          ${colorDisplay ? `<div style='font-size: 10px; color: var(--text-muted);'>Color: ${colorDisplay}</div>` : ''}
          <div style='font-size: 10px; color: var(--text-muted);'>${item.quantity} x ${utils.formatCurrency(item.price)}</div>
        </div>
        <div style='font-weight: 600; color: var(--primary-color);'>${utils.formatCurrency(itemTotal)}</div>
      </div>
    `;
  });
  
  boletaHTML += `
      </div>
      
      <hr style='border: none; border-top: 2px solid var(--border-color); margin: 20px 0;'/>
      
      <div style='display: flex; justify-content: space-between; font-size: 18px; font-weight: bold; margin: 20px 0; padding: 10px; background: var(--primary-color); color: white; border-radius: 8px;'>
        <span>TOTAL (S/)</span>
        <span>${utils.formatCurrency(total)}</span>
      </div>
      
      <p style='margin: 15px 0; font-size: 11px; text-align: center; color: var(--text-muted);'>
        <strong>SON:</strong> ${enLetras(total)}
      </p>
      
      <div style='display: flex; gap: 10px; margin-top: 20px;'>
        <button id='capture-receipt' class='btn btn-primary' style='flex: 1; font-size: 12px; padding: 10px;'>
          📸 Capturar
        </button>
        <button onclick='window.print()' class='btn' style='flex: 1; background: var(--secondary-color); color: white; font-size: 12px; padding: 10px;'>
          🖨️ Imprimir
        </button>
      </div>
      
      <button id='confirm-purchase' class='btn btn-success' style='width: 100%; margin-top: 15px; font-size: 14px; padding: 12px;'>
        ✅ Confirmar Compra
      </button>
    </div>
  `;
  
  // Crear modal de boleta
  const modal = document.createElement('div');
  modal.className = 'modal-overlay active';
  modal.style.zIndex = '4000';
  modal.innerHTML = `<div class="modal-content" style="max-width: 450px;">${boletaHTML}</div>`;
  
  document.body.appendChild(modal);
  
  // Event listeners para la boleta
  document.getElementById('capture-receipt').addEventListener('click', () => {
    utils.showLoading();
    
    const receiptContent = modal.querySelector('.modal-content > div');
    
    html2canvas(receiptContent, {
      useCORS: true,
      allowTaint: false,
      scale: 2,
      backgroundColor: '#ffffff'
    }).then(canvas => {
      utils.hideLoading();
      
      const link = document.createElement('a');
      link.download = `boleta-${clientDni}-${Date.now()}.png`;
      link.href = canvas.toDataURL('image/png');
      link.click();
      
      utils.showNotification('Boleta capturada exitosamente', 'success');
    }).catch(error => {
      utils.hideLoading();
      console.error('Error al capturar:', error);
      utils.showNotification('Error al capturar la boleta', 'error');
    });
  });
  
  document.getElementById('confirm-purchase').addEventListener('click', () => {
    let orderDetails = `¡Hola! 👋 Quiero realizar un pedido:\n\n`;
    orderDetails += `👤 Cliente: ${clientName}\n`;
    orderDetails += `🆔 DNI: ${clientDni}\n\n`;
    orderDetails += `🛍️ Productos:\n`;
    
    cart.forEach(item => {
      const colorDisplay = item.color ? ` (${colorNames[item.color] || item.color})` : '';
      orderDetails += `• ${item.quantity}x ${item.name}${colorDisplay} - ${utils.formatCurrency(item.price * item.quantity)}\n`;
    });
    
    orderDetails += `\n💰 Total: ${utils.formatCurrency(total)}`;
    orderDetails += `\n\n📎 Adjuntar:\n📸 Captura de boleta\n💳 Comprobante de pago`;
    
    const whatsappURL = `https://wa.me/51975842622?text=${encodeURIComponent(orderDetails)}`;
    window.open(whatsappURL, '_blank');
    
    // Limpiar y cerrar
    document.body.removeChild(modal);
    cart = [];
    localStorage.removeItem('cart');
    updateCart();
    toggleCart();
    
    // Limpiar formulario
    document.getElementById('client-name').value = '';
    document.getElementById('client-dni').value = '';
    document.getElementById('client-name').classList.remove('success', 'error');
    document.getElementById('client-dni').classList.remove('success', 'error');
    
    utils.showNotification('¡Pedido enviado por WhatsApp!', 'success');
  });
  
  // Cerrar modal al hacer clic fuera
  modal.addEventListener('click', (e) => {
    if (e.target === modal) {
      document.body.removeChild(modal);
    }
  });
}

// Exponer funciones globales necesarias
window.toggleCart = toggleCart;
window.filterProducts = filterProducts;
</script>

<b:section class='main' id='main' maxwidgets='1' name='main' showaddelement='yes'/>
</body>
</html>
