<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>TodoModa - Tienda Online con Carrito y Boleta + WhatsApp</title>
<style>
    /* --- Estilos originales TodoModa + carrito integrado --- */
    body {
        font-family: Arial, sans-serif;
        margin: 0;
        padding: 0;
        color: #333;
        background: #f9f9f9;
    }
    .container {
        width: 100%;
        margin: 0;
        padding: 20px 20px 40px;
        box-sizing: border-box;
    }
    /* Header */
    .header {
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding: 10px 20px;
        border-bottom: 1px solid #ddd;
    }
    .header .logo img {
        height: 100px;
        width: auto;
    }
    nav ul {
        list-style: none;
        display: flex;
        gap: 20px;
        margin: 0;
        padding: 0;
    }
    nav ul li a {
        text-decoration: none;
        color: #333;
        font-weight: bold;
    }
    .header .icons {
        display: flex;
        gap: 10px;
    }
    .header .icons img {
        width: 20px;
        height: 20px;
    }

    /* Carousel */
  .carousel {
        position: relative;
        width: 100%;
        overflow: hidden;
        margin: 20px 0;
    }
    .carousel .slides {
        display: flex;
        transition: transform 0.5s ease-in-out;
    }
    .carousel .slide-container {
        width: 100%;
        aspect-ratio: 16 / 9;
        position: relative;
        flex-shrink: 0;
    }
    .carousel .slides img {
        width: 100%;
        height: 100%;
        object-fit: cover;
        position: absolute;
        top: 0;
        left: 0;
    }
    .carousel .banner-text {
        position: absolute;
        bottom: 20px;
        left: 50%;
        transform: translateX(-50%);
        font-size: 1.5em;
        font-weight: bold;
        color: #fff;
        background: rgba(0, 0, 0, 0.5);
        padding: 5px 15px;
        border-radius: 5px;
        cursor: pointer;
    }
    .carousel .banner-text:hover {
        background: rgba(0, 0, 0, 0.7);
    }
    .carousel .dots {
        position: absolute;
        bottom: 10px;
        left: 50%;
        transform: translateX(-50%);
        display: flex;
        gap: 10px;
    }
    .carousel .dots span {
        width: 10px;
        height: 10px;
        background-color: #bbb;
        border-radius: 50%;
        cursor: pointer;
    }
    .carousel .dots span.active {
        background-color: #333;
    }

    /* Products scroll horizontal */
 .products {
        display: flex;
        flex-direction: row;
        overflow-x: auto;
        margin: 20px 0;
        padding: 0 20px;
        width: 100%;
        box-sizing: border-box;
        gap: 5px;
        scroll-snap-type: x mandatory;
        scrollbar-width: thin;
        scrollbar-color: #bbb #f1f1f1;
    }
    .products::-webkit-scrollbar {
        height: 8px;
    }
    .products::-webkit-scrollbar-track {
        background: #f1f1f1;
    }
    .products::-webkit-scrollbar-thumb {
        background: #bbb;
        border-radius: 4px;
    }
    .product {
        width: 200px;
        min-width: 200px;
        background: #fff;
        border-radius: 8px;
        box-shadow: 0 0 5px rgba(0,0,0,0.1);
        padding: 10px;
        text-align: center;
        position: relative;
        cursor: pointer;
        scroll-snap-align: start;
        display: flex;
        flex-direction: column;
        gap: 8px;
        user-select: none;
    }
    .product img {
        width: 100%;
        height: auto;
        border-radius: 5px;
        flex-shrink: 0;
    }
    .product p {
        margin: 0;
        font-weight: 600;
        font-size: 14px;
    }
    .price {
        font-weight: bold;
        color: #444;
        font-size: 15px;
    }
    /* Paleta de colores */
    .color-palette {
        display: flex;
        justify-content: center;
        gap: 6px;
        flex-wrap: wrap;
        margin-top: 4px;
        margin-bottom: 8px;
    }
    .color-circle {
        width: 25px;
        height: 25px;
        border-radius: 50%;
        border: 1.5px solid #ccc;
        cursor: pointer;
        transition: transform 0.2s, border-color 0.3s;
        flex-shrink: 0;
    }
    .color-circle.selected {
        border-color: #333;
        transform: scale(1.2);
    }
    /* Botón agregar */
    .add-to-cart {
        background: #333;
        color: white;
        border: none;
        border-radius: 5px;
        padding: 8px 10px;
        width: 100%;
        cursor: pointer;
        font-weight: 600;
        font-size: 14px;
        transition: background 0.3s;
        flex-shrink: 0;
    }
    .add-to-cart:hover:not(:disabled) {
        background: #555;
    }
    .add-to-cart:disabled {
        background: #999;
        cursor: default;
    }

    /* Model Section (categorías con botones) */
 .model-section {
        display: flex;
        justify-content: space-between;
        margin: 20px 0;
        width: 100%;
        flex-wrap: nowrap;
    }
    .model-item {
        position: relative;
        text-align: center;
        width: 50%;
        max-width: none;
    }
    .model-item img {
        width: 100%;
        height: auto;
        border-radius: 5px;
        display: block;
        cursor: pointer;
    }
    .model-item .category-btn {
        position: absolute;
        bottom: 10px;
        left: 50%;
        transform: translateX(-50%);
        width: 80%;
        font-size: 1.2em;
        font-weight: bold;
        color: #fff;
        background: rgba(0, 0, 0, 0.5);
        padding: 4px 10px;
        border-radius: 5px;
        cursor: pointer;
        border: none;
        transition: background 0.3s;
    }
    .model-item .category-btn:hover {
        background: rgba(0, 0, 0, 0.7);
    }

    /* Modal base */
.modal, .view-all-modal, .clips-damas-modal, .clips-ninas-modal {
        display: none;
        position: fixed;
        top: 0; left: 0; width: 100%; height: 100%;
        background: rgba(0,0,0,0.5);
        z-index: 1000;
        justify-content: center;
        align-items: center;
        overflow-y: auto;
    }
    .modal-content, .view-all-modal-content, .clips-damas-modal-content, .clips-ninas-modal-content {
        background: #fff;
        padding: 20px;
        border-radius: 5px;
        max-width: 90%;
        width: 100%;
        max-height: 90vh;
        overflow-y: auto;
        position: relative;
        box-sizing: border-box;
    }
    .modal-content img {
        width: 100%;
        height: auto;
        border-radius: 5px;
        margin-bottom: 15px;
    }
    .modal-content h3, .view-all-modal-content h2, .clips-damas-modal-content h2, .clips-ninas-modal-content h2 {
        margin: 0 0 20px;
        font-size: 1.5em;
        text-align: center;
    }
    .search-container {
        margin: 10px 0 20px;
        text-align: center;
    }
    .search-input {
        width: 80%;
        max-width: 400px;
        padding: 8px;
        border: 1px solid #ddd;
        border-radius: 5px;
        font-size: 1em;
    }
    .search-input:focus {
        outline: none;
        border-color: #333;
    }
    .view-all-products, .clips-damas-products, .clips-ninas-products {
        display: grid;
        grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
        gap: 20px;
        padding: 0 10px;
    }
    .view-all-products .product, .clips-damas-products .product, .clips-ninas-products .product {
        width: 100%;
        min-width: unset;
        cursor: pointer;
    }
    .close-btn {
        position: absolute;
        top: 10px;
        right: 10px;
        font-size: 1.5em;
        cursor: pointer;
        color: #333;
        user-select: none;
        border: none;
        background: none;
    }
    .close-btn:hover {
        color: #000;
    }

    /* Carrito flotante */
 #cart-button {
        position: fixed;
        top: 20px;
        right: 20px;
        background: #ff5722;
        color: white;
        border-radius: 50%;
        width: 50px;
        height: 50px;
        font-size: 24px;
        display: flex;
        align-items: center;
        justify-content: center;
        cursor: pointer;
        box-shadow: 0 4px 10px rgba(0,0,0,0.3);
        z-index: 10000;
    }
    /* Carrito panel */
    #cart {
        display: none;
        background: white;
        padding: 20px;
        border-radius: 10px;
        max-width: 420px;
        position: fixed;
        top: 80px;
        right: 20px;
        box-shadow: 0 0 15px rgba(0,0,0,0.3);
        z-index: 9999;
        font-size: 14px;
        max-height: 80vh;
        overflow-y: auto;
    }
    #cart h2 {
        margin-top: 0;
        font-size: 1.4em;
    }
    #cart input[type=text] {
        width: 100%;
        padding: 8px;
        margin-bottom: 10px;
        box-sizing: border-box;
        border: 1px solid #ddd;
        border-radius: 5px;
        font-size: 14px;
    }
    .cart-item {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 10px;
        border-bottom: 1px solid #eee;
        padding-bottom: 6px;
    }
    .cart-item > div:first-child {
        display: flex;
        flex-direction: column;
    }
    .cart-item strong {
        font-weight: 600;
        margin-bottom: 2px;
    }
    .cart-item small {
        font-size: 12px;
        color: #666;
        margin-bottom: 3px;
    }
    .cart-item-controls {
        display: flex;
        align-items: center;
        gap: 6px;
        flex-wrap: nowrap;
    }
    .cart-item-controls button {
        background: #eee;
        border: none;
        border-radius: 3px;
        cursor: pointer;
        padding: 4px 8px;
        font-weight: bold;
        font-size: 14px;
        transition: background 0.3s;
    }
    .cart-item-controls button:hover {
        background: #ddd;
    }
    .cart-item-price {
        min-width: 70px;
        text-align: right;
        font-weight: 600;
        white-space: nowrap;
    }
    #cart-total {
        font-weight: bold;
        margin-top: 10px;
        text-align: right;
    }
    #order-button {
        background: #ff5722;
        color: white;
        width: 100%;
        padding: 10px;
        font-size: 16px;
        border: none;
        border-radius: 6px;
        cursor: pointer;
        margin-top: 12px;
        transition: background 0.3s;
    }
    #order-button:hover {
        background: #e64a19;
    }

    /* Modal boleta */
  #boleta-modal {
        position: fixed;
        top:0; left:0; width:100%; height:100%;
        background: rgba(0,0,0,0.7);
        display: none;
        align-items: center;
        justify-content: center;
        z-index: 100000;
        font-family: monospace;
    }
    #boleta-content {
        background: white;
        padding: 20px;
        border-radius: 10px;
        max-width: 420px;
        width: 90%;
        max-height: 85vh;
        overflow-y: auto;
        color: #222;
        outline: none;
    }
    #boleta-content h3 {
        text-align: center;
        margin-top: 0;
    }
    #boleta-content table {
        width: 100%;
        border-collapse: collapse;
        margin-top: 10px;
    }
    #boleta-content table, #boleta-content th, #boleta-content td {
        border: 1px solid #ccc;
    }
    #boleta-content th, #boleta-content td {
        padding: 6px;
        text-align: left;
    }
    #boleta-buttons button {
        margin-top: 10px;
        width: 100%;
        padding: 10px;
        border: none;
        border-radius: 6px;
        cursor: pointer;
        font-size: 15px;
        transition: background 0.3s;
    }
    #capture-button { background: #FF9800; color: white; }
    #capture-button:hover { background: #fb8c00; }
    #print-button { background: #2196F3; color: white; }
    #print-button:hover { background: #1976D2; }
    #confirm-purchase { background: #4CAF50; color: white; }
    #confirm-purchase:hover { background: #388E3C; }

    /* Loading spinner */
  #loading-spinner {
        display:none;
        position: fixed;
        top:50%; left:50%;
        transform: translate(-50%, -50%);
        background: rgba(0,0,0,0.7);
        color: white;
        padding: 15px 30px;
        border-radius: 10px;
        font-size: 18px;
        z-index: 100001;
    }

    /* Responsive */
   @media (max-width: 768px) {
        .product {
            width: 150px;
            min-width: 150px;
        }
        .view-all-products, .clips-damas-products, .clips-ninas-products {
            grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
        }
        .search-input {
            width: 90%;
        }
        .category-btn {
            font-size: 1em;
            padding: 4px 8px;
        }
        .model-item {
            width: 50%;
        }
        .model-item img {
            width: 100%;
        }
    }
    @media (max-width: 480px) {
        .product {
            width: 120px;
            min-width: 120px;
        }
        .product p {
            font-size: 0.9em;
        }
        .view-all-products, .clips-damas-products, .clips-ninas-products {
            grid-template-columns: repeat(auto-fill, minmax(120px, 1fr));
        }
        .search-input {
            width: 95%;
        }
        .category-btn {
            font-size: 0.9em;
            padding: 3px 6px;
        }
        .model-item {
            width: 50%;
        }
        .model-item img {
            width: 100%;
        }
    }
</style>
</head>
<body>
<div class="container">
    <!-- Header -->
    <div class="header">
        <div class="logo">
            <img src="https://lh3.googleusercontent.com/gps-cs/AIky0YXTTJyLqUwcNn1yduyV6i82lmL4ukvEZp-ePVd_P_Wa_y1VGwXNJOPpVxro2IxUZ55xE4oEndno5MItmJf7wjkFn0RYFCLtB4bOG2AHYHrupD1pkX8cf3jOUBHNUJOFEYOrwzTGEMSJj6j8=w1000-h1000-p-k-no" alt="TodoModa Logo" />
        </div>
        <nav>
            <ul>
                <!-- Puedes añadir links si quieres -->
            </ul>
        </nav>
        <div class="icons">
            <!-- Iconos si quieres -->
        </div>
    </div>

    <!-- Carousel -->
 <div class="carousel" aria-label="Carrusel de banners">
        <div class="slides">
            <div class="slide-container">
                <img src="https://pe.todomoda.com/media/wysiwyg/TM_DISNEY_STITCH_-_BANNERS_Desk_new_1.jpg" alt="Banner 1">
            </div>
            <div class="slide-container">
                <img src="https://lh3.googleusercontent.com/gps-cs/AIky0YUd2bofobsLtUl3qONXRSiTNou1a9W74yTaVYEr6h64PAuOOqQ-g_w6Ifs8arhOVjWboOrUFEcEDZlmtSBZkgS1YjEnSIw1f3w4IZRdMBwxibVChvNz2c93C78bOxNsx68MuBmN-4iYNCg=w2000-h2000-p-k-no" alt="Banner 2">
            </div>
        </div>
        <div class="banner-text" id="viewAllBtn" tabindex="0" role="button" aria-label="Ver todos los productos">VER TODO</div>
        <div class="dots" role="tablist">
            <span class="active" role="tab" tabindex="0" aria-selected="true"></span>
            <span role="tab" tabindex="0" aria-selected="false"></span>
        </div>
    </div>


        <!-- Product Listings -->
<div class="products">
            <!-- Categoría 1: Pilsen -->
            <div class="product" data-id="1" data-colors='[{"color": "#ffeb3b", "title": "Amarillo"}, {"color": "#d32f2f", "title": "Rojo"}, {"color": "#e1bee7", "title": "Lila"}, {"color": "#145a32", "title": "Verde"}, {"color": "#d6eaf8", "title": "Celeste"}]' data-rating="⭐⭐⭐⭐☆ (4.2)" data-description="Maxilazos coloridos, perfectos para cualquier peinado.">
                <img alt="Maxilazos" src="https://lh3.googleusercontent.com/gps-cs/AIky0YXdnjCFtJm5EhEvClhpsqjsYwwH2Xdqql3H45tWmgLdhiRX--KLwloCAl85SxTImNaOYYbS1MOrlGYrDwH31YoIyFBBn7KapQIKbAHVfoyNmbRBjjgmF0_SefXWn6udgSSaO19kdNtmnQBd=w2000-h2000-p-k-no"/>
                <p>Maxilazos - 5 Colores</p>
                <p class="price">S/ 7.00</p>
                <button class="add-to-cart" data-id="1">Agregar al carrito</button>
            </div>
            <div class="product" data-id="2" data-colors='[{"color": "#17202a", "title": "Negro"}, {"color": "#fff9c4", "title": "Crema"}, {"color": "#fdebd0", "title": "Piel"}, {"color": "#fdfefe", "title": "Crema"}]' data-rating="⭐⭐⭐☆☆ (3.2)" data-description="Ganchos en forma de corazón, ideales para looks delicados.">
                <img alt="Mini Gancho Corazón" src="https://lh3.googleusercontent.com/gps-cs/AIky0YUd2bofobsLtUl3qONXRSiTNou1a9W74yTaVYEr6h64PAuOOqQ-g_w6Ifs8arhOVjWboOrUFEcEDZlmtSBZkgS1YjEnSIw1f3w4IZRdMBwxibVChvNz2c93C78bOxNsx68MuBmN-4iYNCg=w2000-h2000-p-k-no"/>
                <p>Mini Gancho Corazón</p>
                <p class="price">S/ 2.50</p>
                <button class="add-to-cart" data-id="2">Agregar al carrito</button>
            </div>
            <div class="product" data-id="3" data-colors='[{"color": "#FFFFFF", "title": "Blanco"}, {"color": "#FF0000", "title": "Rojo"}, {"color": "#008000", "title": "Verde"}]' data-rating="⭐⭐⭐⭐⭐ (5.0)" data-description="Ganchos temáticos navideños para un estilo festivo.">
                <img alt="Ganchos Navideños" src="https://lh3.googleusercontent.com/gps-cs/AIky0YV8A_P0YjCC6AIfC2B6HFvCKobK0UJZjVWMnzr6lfYPVXUk0gsszvJXojCK_ycIVH0cOD1-Qw3ICj1Bi9eLIf2TH0ZFaL14TuisJOWESznCPwqs2AAn_lgVOo2yGLhrKuG1yjgsGrWPIZ0k=w2000-h2000-p-k-no"/>
                <p>Ganchos Navideños</p>
                <p class="price">S/ 4.00</p>
                <button class="add-to-cart" data-id="3">Agregar al carrito</button>
            </div>
            <div class="product" data-id="4" data-colors='[{"color": "#FFD700", "title": "Amarillo"}]' data-rating="⭐⭐⭐⭐☆ (4.0)" data-description="Ganchos hawaianos vibrantes para un look tropical.">
                <img alt="Gancho Hawaiano" src="https://lh3.googleusercontent.com/gps-cs/AIky0YVaD4OrbInMGPZXKiKtKplaYEn2Ck-9KCl8p9FJbJIXPMWFCDw9Dd5lrbO-8FfXeJZKvIEr-K5UpFwrCnofwtR30imdZTojz2gxrHqZLSM3qody1gDhWdXAm_C4le7hQ4zKL3imga1TIh_j=w2000-h2000-p-k-no"/>
                <p>Gancho Hawaiano</p>
                <p class="price">S/ 5.00</p>
                <button class="add-to-cart" data-id="4">Agregar al carrito</button>
            </div>
            <div class="product" data-id="5" data-colors='[{"color": "#5dade2", "title": "Celeste"}, {"color": "#ebf5fb", "title": "Agua"}, {"color": "#FFFFFF", "title": "Blanco"}]' data-rating="⭐⭐⭐⭐☆ (4.0)" data-description="Ganchos acrílicos elegantes en tonos celestes.">
                <img alt="Ganchos Acrílicos Color Celeste" src="https://lh3.googleusercontent.com/gps-cs/AIky0YXULCa-2ZSbLgwDDlphVpkyxIs_jH2pp8AIHp25rY65c3VTGPdLnesGcrtuCiDtLbovSHvwiSUpzfWiwyle1UmqeO6d0OEvhBLqp_6k4YBo2QzMGd9aduXbKMXqGVHIB0FKSWvBYE1FNgj_=w2000-h2000-p-k-no"/>
                <p>Ganchos Acrílicos Color Celeste</p>
                <p class="price">S/ 5.00</p>
                <button class="add-to-cart" data-id="5">Agregar al carrito</button>
            </div>
            <div class="product" data-id="6" data-colors='[{"color": "#8d6e63", "title": "Marrón"}, {"color": "#fef9e7", "title": "Crema"}]' data-rating="⭐⭐⭐☆☆ (3.1)" data-description="Ganchos clásicos para un estilo minimalista.">
                <img alt="Ganchos" src="https://lh3.googleusercontent.com/gps-cs/AIky0YUepENF6loS0sqfXxEEZlTcAEQ7R-6iS6rmphnT9YjPc9whL2WIk8tCzVNnHDeaj6AaV3e6-k4yeUx9j6nSHq-l2Tc_t0dGMQLhBQrbdREDnxR65_tbipCAL3NCKmRQYWk5geU5V_jn3EiW=w2000-h2000-p-k-no"/>
                <p>Ganchos</p>
                <p class="price">S/ 4.50</p>
                <button class="add-to-cart" data-id="6">Agregar al carrito</button>
            </div>
            <div class="product" data-id="7" data-colors='[]' data-rating="⭐⭐⭐⭐☆ (4.1)" data-description="Ganchos en forma de flor con diseño inspirado en el sol.">
                <img alt="Ganchos Torna Sol en forma de Flor" src="https://lh3.googleusercontent.com/gps-cs/AIky0YX2NRiy9kc9B9F5EY9kAoTjy699I8L7qzIaAFyN6ktzntZDbknG5_v1B6_JgD_hJDZQ7pAonmz2ynxpJqX4tYXVpt2EJISwaxV7Vd5er2HXevBcfzH_2KoEuxffPMG6wVLrMxkXZaJcUGxc=w2000-h2000-p-k-no"/>
                <p>Ganchos Torna Sol en forma de Flor</p>
                <p class="price">S/ 6.00</p>
                <button class="add-to-cart" data-id="7">Agregar al carrito</button>
            </div>
            <div class="product" data-id="8" data-colors='[{"color": "#FFFF66", "title": "Amarillo"}, {"color": "#CCFF00", "title": "Verde"}, {"color": "#FF8C00", "title": "Anaranjado"}]' data-rating="⭐⭐⭐☆☆ (3.5)" data-description="Ganchos kawai con diseño floral, ideales para niños.">
                <img alt="Ganchos Kawai en forma de Flor" src="https://lh3.googleusercontent.com/gps-cs/AIky0YXzdeSiF8Ekcd_sbWEkePfXIFlDCt8BeIvwjgW0_jHy1u9d3KWkRPGKY0IPp8ADAmGFn46hFm8U5vXqhoZ738QBNnwuwb-UXng4k1wKXRwyarfw7ST9PYntIH_SA_XEF0lDF6STVaLz16z2=w2000-h2000-p-k-no"/>
                <p>Ganchos Kawai en forma de Flor</p>
                <p class="price">S/ 4.50</p>
                <button class="add-to-cart" data-id="8">Agregar al carrito</button>
            </div>
            <div class="product" data-id="9" data-colors='[{"color": "#FFB347", "title": "Melón"}, {"color": "#FFD700", "title": "Amarillo"}]' data-rating="⭐⭐⭐⭐☆ (4.0)" data-description="Ganchos florales en tonos cálidos para un look vibrante.">
                <img alt="Ganchos de Flores" src="https://lh3.googleusercontent.com/gps-cs/AIky0YUem5vYUL5I1PM57jknLifOO7yf5kSVMtMghU4lP6w0ZMUkV2L9UYoqFLTR_8PcGATvSRKyf0IVg5IYHBQzc5_aND9V8BvtQS47MAT--YXhLlrk645yFo2vaWRADuVRrnbiL5rs4ubhXvU=w2000-h2000-p-k-no"/>
                <p>Ganchos de Flores</p>
                <p class="price">S/ 5.00</p>
                <button class="add-to-cart" data-id="9">Agregar al carrito</button>
            </div>
            <!-- Categoría 2: Cristal -->
            <div class="product" data-id="14" data-colors='[]' data-rating="⭐⭐⭐⭐☆ (4.0)" data-description="Mini ganchitos florales para destacar tu peinado.">
                <img alt="Par de mini ganchitos en forma de flor" src="https://lh3.googleusercontent.com/gps-cs/AIky0YVcDqGO_EKNry0Eb-BkdsNH0V0lOhwW7AM5WEqz8IiNlbpTs2U3Io9_kt4yCGgt5haYI5RgwRDHv-LMBqc5bvmX245QMyriwIoyJyniPQH9cJJ9iCC2fC8hY06M9BU9nFd6NhCLGVGCC34N=w2000-h2000-p-k-no"/>
                <p>Par de mini ganchitos en forma de flor</p>
                <p class="price">S/ 3.00</p>
                <button class="add-to-cart" data-id="14">Agregar al carrito</button>
            </div>
            <div class="product" data-id="15" data-colors='[]' data-rating="⭐⭐⭐☆☆ (3.5)" data-description="Ganchitos en forma de mariposa, perfectos para peinados infantiles.">
                <img alt="Mini ganchitos en forma de mariposa" src="https://lh3.googleusercontent.com/gps-cs/AIky0YW1eFtqiwT_PM-xOZnd2iVogh-XQVJclLEtgsh0i5wUGm9NvOCot9LJLfDmZE58abznArTin0EgjEMw3HuKeK9_9hoODK0kla3nM-GYGSvA8_xXCBmu_qiSuoHzgpSaO_2EtqXLAjnCs34l=w2000-h2000-p-k-no"/>
                <p>Mini ganchitos en forma de mariposa</p>
                <p class="price">S/ 2.00</p>
                <button class="add-to-cart" data-id="15">Agregar al carrito</button>
            </div>
            <div class="product" data-id="16" data-colors='[]' data-rating="⭐⭐⭐☆☆ (3.3)" data-description="Mini ganchitos versátiles para cualquier ocasión.">
                <img alt="Mini ganchitos" src="https://lh3.googleusercontent.com/gps-cs/AIky0YUgnWieVRURnUHds0U4E5FROmRmvztpc0ynONqB5wFO-tvCmbrBn0-E971IAl2YG7r7cobC9Hx-g0AbDpTP71ukEEb6n20lHQz-aPBoI5xDWtVwABfSJFIbqdRT6_YJzOT7x8uhaX-KBSLE=w2000-h2000-p-k-no"/>
                <p>Mini ganchitos</p>
                <p class="price">S/ 1.50</p>
                <button class="add-to-cart" data-id="16">Agregar al carrito</button>
            </div>
            <div class="product" data-id="17" data-colors='[{"color": "#FFC0CB", "title": "Rosa Pastel"}, {"color": "#FFD700", "title": "Amarillo"}, {"color": "#00BFFF", "title": "Azul"}, {"color": "#FF4500", "title": "Naranja"}, {"color": "#008000", "title": "Verde"}]' data-rating="⭐⭐⭐⭐☆ (4.0)" data-description="Ligas en colores pasteles y fuertes, ideales para cualquier estilo.">
                <img alt="Ligas colores pasteles y fuertes" src="https://lh3.googleusercontent.com/gps-cs/AIky0YVwhLWhfaBVh3ChmdRjktxd6WCi7W6fTmz2_7TvWPHTT_-3tX1zci-DGspLNMmn3SpAYgh9RN5G_lHRBehTbWzF16lZ9CNiBbjgj5-EVSXMU3aVjCsYaPQ5Maahznx9Fi79zzSnwLxM_nkC=w2000-h2000-p-k-no"/>
                <p>Ligas colores pasteles y fuertes</p>
                <p class="price">S/ 1.00</p>
                <button class="add-to-cart" data-id="17">Agregar al carrito</button>
            </div>
            <div class="product" data-id="18" data-colors='[{"color": "#000000", "title": "Negro"}]' data-rating="⭐⭐⭐☆☆ (3.3)" data-description="Colets negros clásicos y resistentes.">
                <img alt="Colets negros" src="https://lh3.googleusercontent.com/gps-cs/AIky0YWE3Z0a1qVkSdmBI9RQzayKeT8bgvXn5RTJNXmMJjHG9uzg5VUrwt4-PKEq6AdcYPITi3LkJvKtdxDXq6PucsAOpzZGm2J8QGEYCR4Ff59f3YXXaKQ_Ww8lgm4vOYlRuyCNXxPuyWPFWf23=w2000-h2000-p-k-no"/>
                <p>Colets negros</p>
                <p class="price">S/ 1.00</p>
                <button class="add-to-cart" data-id="18">Agregar al carrito</button>
            </div>
            <div class="product" data-id="19" data-colors='[{"color": "#FFB6C1", "title": "Rosa Pastel"}, {"color": "#87CEFA", "title": "Azul Pastel"}, {"color": "#98FB98", "title": "Verde Pastel"}]' data-rating="⭐⭐⭐☆☆ (3.4)" data-description="Colets en tonos pasteles para un look suave y elegante.">
                <img alt="Colets colores pasteles" src="https://lh3.googleusercontent.com/gps-cs/AIky0YVVXgYaHEulEuraO7tX6LShXlnoogs6cvwc7jryv8vOVwEt2wCEPWyj0ihUEHTjGMKv0HpL3uglAD96vZsANfdnMrLB4hRI1quw3OaPX-ewOFjUY9eF2ggyG4sMZLcBfJ8amsKoKsAgOXPG=w2000-h2000-p-k-no"/>
                <p>Colets colores pasteles</p>
                <p class="price">S/ 1.00</p>
                <button class="add-to-cart" data-id="19">Agregar al carrito</button>
            </div>
        </div>
        <!-- Model Section -->
 <div class="model-section">
            <div class="model-item">
                <img src="https://lh3.googleusercontent.com/gps-cs/AIky0YUGuPXaSC1mPGUKkOYa5z7JyvELvbIy0B4-WtB3tMHIKm2D6Sbg1cTWwU0MsxRJR_5lKb5t1MnVOStZk-tNPdUudQ6-h7M7ueR4l8N5IgmuOrhlNRMi0B_uohBDRomdzQUIHP7y244Zc150=w1024-h1024-p-k-no" alt="Bufandas">
                <button class="category-btn" id="clipsDamasBtn">CLIPS DAMAS</button>
            </div>
            <div class="model-item">
                <img src="https://lh3.googleusercontent.com/gps-cs/AIky0YUDER3L7ISerfG6uiIU8ISdgKkibO-SXwGGNL1azb_TJ0qYIN3T7LsJyU-qc9-kQtucnOkLr5rPYtWt0fW0UL8-7RDD46bg_0JnGLkD8RSfQvGydDvq6L_ZLBoj4hnIhwHB3CEx1fPtJ58O=w1024-h1024-p-k-no" alt="Carteras">
                <button class="category-btn" id="clipsNinasBtn">CLIPS NIÑAS</button>
            </div>
        </div>



    <!-- Model Section -->
<div class="model-section">
        <div class="model-item">
            <img src="https://lh3.googleusercontent.com/gps-cs/AIky0YUGuPXaSC1mPGUKkOYa5z7JyvELvbIy0B4-WtB3tMHIKm2D6Sbg1cTWwU0MsxRJR_5lKb5t1MnVOStZk-tNPdUudQ6-h7M7ueR4l8N5IgmuOrhlNRMi0B_uohBDRomdzQUIHP7y244Zc150=w1024-h1024-p-k-no" alt="Bufandas" />
            <button class="category-btn" id="clipsDamasBtn">CLIPS DAMAS</button>
        </div>
        <div class="model-item">
            <img src="https://lh3.googleusercontent.com/gps-cs/AIky0YUDER3L7ISerfG6uiIU8ISdgKkibO-SXwGGNL1azb_TJ0qYIN3T7LsJyU-qc9-kQtucnOkLr5rPYtWt0fW0UL8-7RDD46bg_0JnGLkD8RSfQvGydDvq6L_ZLBoj4hnIhwHB3CEx1fPtJ58O=w1024-h1024-p-k-no" alt="Carteras" />
            <button class="category-btn" id="clipsNinasBtn">CLIPS NIÑAS</button>
        </div>
    </div>
</div>

<!-- Botón flotante abrir/cerrar carrito -->
<div id="cart-button" title="Abrir carrito" aria-label="Abrir carrito de compras">🛒</div>

<!-- Carrito -->
<section id="cart" aria-live="polite" aria-label="Carrito de compras">
    <h2>Carrito de Compras</h2>
    <input type="text" id="client-name" placeholder="Nombre del cliente" aria-label="Nombre del cliente" autocomplete="name" />
    <input type="text" id="client-dni" placeholder="DNI del cliente (8 dígitos)" aria-label="DNI del cliente" maxlength="8" autocomplete="off" />
    <div id="cart-items" aria-relevant="additions removals"></div>
    <p id="cart-total"><strong>Total: S/ 0.00</strong></p>
    <button id="order-button">Realizar Pedido</button>
</section>

<!-- Modal boleta -->
<div id="boleta-modal" role="dialog" aria-modal="true" aria-labelledby="boleta-title" style="display:none;">
    <div id="boleta-content" tabindex="0"></div>
</div>

<!-- View All Products Modal -->
<div class="view-all-modal" id="viewAllModal" role="dialog" aria-labelledby="viewAllModalTitle" aria-hidden="true">
    <div class="view-all-modal-content">
        <button class="close-btn" aria-label="Cerrar modal">&times;</button>
        <h2 id="viewAllModalTitle">Todos los Productos</h2>
        <div class="search-container">
            <input type="text" class="search-input" id="productSearch" placeholder="Buscar productos..." aria-label="Buscar productos" />
        </div>
        <div class="view-all-products" id="viewAllProducts"></div>
    </div>
</div>

<!-- Clips Damas Modal -->
<div class="clips-damas-modal" id="clipsDamasModal" role="dialog" aria-labelledby="clipsDamasModalTitle" aria-hidden="true">
    <div class="clips-damas-modal-content">
        <button class="close-btn" aria-label="Cerrar modal">&times;</button>
        <h2 id="clipsDamasModalTitle">CLIPS DAMAS</h2>
        <div class="search-container">
            <input type="text" class="search-input" id="clipsDamasSearch" placeholder="Buscar en Clips Damas..." aria-label="Buscar en Clips Damas" />
        </div>
        <div class="clips-damas-products" id="clipsDamasProducts"></div>
    </div>
</div>

<!-- Clips Niñas Modal -->
<div class="clips-ninas-modal" id="clipsNinasModal" role="dialog" aria-labelledby="clipsNinasModalTitle" aria-hidden="true">
    <div class="clips-ninas-modal-content">
        <button class="close-btn" aria-label="Cerrar modal">&times;</button>
        <h2 id="clipsNinasModalTitle">CLIPS NIÑAS</h2>
        <div class="search-container">
            <input type="text" class="search-input" id="clipsNinasSearch" placeholder="Buscar en Clips Niñas..." aria-label="Buscar en Clips Niñas" />
        </div>
        <div class="clips-ninas-products" id="clipsNinasProducts"></div>
    </div>
</div>

<!-- Loading Spinner -->
<div id="loading-spinner" role="alert" aria-live="assertive">Cargando...</div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
<script>
/* === Variables y funciones base === */
let cart = JSON.parse(localStorage.getItem('cart')) || [];

// Formatea número a moneda Soles
function formatCurrency(amount) {
    return `S/ ${parseFloat(amount).toFixed(2)}`;
}

// Número a letras (simplificado)
function numberToLetters(n) {
    const parts = n.toFixed(2).split('.');
    return `${parseInt(parts[0])} CON ${parts[1]}/100 SOLES`;
}

// Actualiza botones de agregar para producto y carrito
function updateAddButtons() {
    document.querySelectorAll('.product').forEach(prod => {
        const prodId = prod.dataset.id;
        const selectedColorCircle = prod.querySelector('.color-circle.selected');
        const prodColor = selectedColorCircle ? selectedColorCircle.getAttribute('data-color') : null;
        const inCart = cart.some(item => item.id === prodId && item.color === prodColor);
        const btn = prod.querySelector('.add-to-cart');
        btn.disabled = !prodColor || inCart;
        btn.textContent = inCart ? 'Agregado' : 'Agregar al carrito';
    });
}

// Actualiza la vista del carrito
function updateCart() {
    const cartItemsDiv = document.getElementById('cart-items');
    let html = '';
    let total = 0;
    cart.forEach(item => {
        total += item.price * item.quantity;
        html += `
        <div class="cart-item" data-id="${item.id}" data-color="${item.color}">
            <div>
                <strong>${item.name}</strong><br />
                <small>Color: <span style="color:${item.color}; font-weight:bold;">${item.colorName}</span></small><br />
                <div class="cart-item-controls">
                    <button class="decrease" aria-label="Disminuir cantidad de ${item.name}">−</button>
                    <span aria-live="polite" aria-atomic="true">${item.quantity}</span>
                    <button class="increase" aria-label="Aumentar cantidad de ${item.name}">+</button>
                    <button class="remove" aria-label="Eliminar ${item.name} del carrito" style="color:#f44336;">🗑️</button>
                </div>
            </div>
            <div class="cart-item-price">${formatCurrency(item.price * item.quantity)}</div>
        </div>`;
    });
    cartItemsDiv.innerHTML = html;
    document.getElementById('cart-total').innerHTML = `<strong>Total: ${formatCurrency(total)}</strong>`;
    localStorage.setItem('cart', JSON.stringify(cart));
    updateAddButtons();
}

// Añade producto al carrito
function addToCart(id, name, price, color, colorName) {
    let item = cart.find(i => i.id === id && i.color === color);
    if (item) {
        item.quantity++;
    } else {
        cart.push({ id, name, price, quantity: 1, color, colorName });
    }
    updateCart();
    alert(`Producto "${name}" con color "${colorName}" agregado al carrito.`);
}

/* === Eventos selección color === */
document.querySelectorAll('.product').forEach(prod => {
    const colors = prod.querySelectorAll('.color-circle');
    colors.forEach(colorCircle => {
        colorCircle.addEventListener('click', () => {
            colors.forEach(c => {
                c.classList.remove('selected');
                c.setAttribute('aria-checked', 'false');
            });
            colorCircle.classList.add('selected');
            colorCircle.setAttribute('aria-checked', 'true');
            updateAddButtons();
        });
        // Keyboard support for color selection
        colorCircle.addEventListener('keydown', e => {
            if(e.key === "Enter" || e.key === " "){
                e.preventDefault();
                colorCircle.click();
            }
        });
    });
});

/* === Botones agregar al carrito === */
document.querySelectorAll('.add-to-cart').forEach(button => {
    button.addEventListener('click', e => {
        const prod = e.target.closest('.product');
        const id = prod.dataset.id;
        const name = prod.dataset.name;
        const price = parseFloat(prod.dataset.price);
        const selectedColorCircle = prod.querySelector('.color-circle.selected');
        if (!selectedColorCircle) {
            alert('Por favor, seleccione un color.');
            return;
        }
        const color = selectedColorCircle.getAttribute('data-color');
        const colorName = selectedColorCircle.getAttribute('data-colorname');
        addToCart(id, name, price, color, colorName);
    });
});

/* === Botón abrir/cerrar carrito === */
const cartButton = document.getElementById('cart-button');
const cartSection = document.getElementById('cart');
cartButton.addEventListener('click', () => {
    if (cartSection.style.display === 'block') {
        cartSection.style.display = 'none';
        cartButton.setAttribute('aria-label', 'Abrir carrito de compras');
    } else {
        cartSection.style.display = 'block';
        cartButton.setAttribute('aria-label', 'Cerrar carrito de compras');
    }
});

/* === Botones en carrito: aumentar, disminuir, eliminar === */
document.getElementById('cart-items').addEventListener('click', e => {
    if (!e.target.matches('button')) return;
    const cartItemDiv = e.target.closest('.cart-item');
    const id = cartItemDiv.dataset.id;
    const color = cartItemDiv.dataset.color;
    let item = cart.find(i => i.id === id && i.color === color);
    if (!item) return;

    if (e.target.classList.contains('increase')) {
        item.quantity++;
    } else if (e.target.classList.contains('decrease')) {
        item.quantity--;
        if (item.quantity <= 0) {
            cart = cart.filter(i => !(i.id === id && i.color === color));
        }
    } else if (e.target.classList.contains('remove')) {
        cart = cart.filter(i => !(i.id === id && i.color === color));
    }
    updateCart();
});

/* === Botón realizar pedido === */
document.getElementById('order-button').addEventListener('click', () => {
    const clientName = document.getElementById('client-name').value.trim();
    const clientDni = document.getElementById('client-dni').value.trim();

    if (!clientName || !clientDni) {
        alert('Por favor, complete nombre y DNI.');
        return;
    }
    if (!/^\d{8}$/.test(clientDni)) {
        alert('El DNI debe tener 8 dígitos.');
        return;
    }
    if (cart.length === 0) {
        alert('El carrito está vacío.');
        return;
    }

    let total = cart.reduce((sum, i) => sum + i.price * i.quantity, 0);
    let date = new Date();
    let dateStr = date.toLocaleDateString();
    let timeStr = date.toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' });

    let html = `
    <h3 id="boleta-title">BOLETA DE VENTA ELECTRÓNICA</h3>
    <div style="text-align:center; margin-bottom:10px;">
        <img src="https://i.ibb.co/Kz9NwFym/yape-qr.jpg" alt="QR Pago" style="width:150px; border-radius:10px;" />
        <p style="margin:5px 0; font-size:12px;">Paga aquí con Yape</p>
        <p style="margin:0; font-size:12px;">Jhonny David Palacios Gutierrez</p>
    </div>
    <p><strong>Cliente:</strong> ${clientName}</p>
    <p><strong>DNI:</strong> ${clientDni}</p>
    <p><strong>Fecha:</strong> ${dateStr} <strong>Hora:</strong> ${timeStr}</p>
    <hr/>
    <table>
        <thead>
            <tr><th>Cant</th><th>Producto</th><th>Color</th><th>Precio Unit.</th><th>Total</th></tr>
        </thead>
        <tbody>
    `;
    cart.forEach(item => {
        html += `<tr>
            <td>${item.quantity}</td>
            <td>${item.name}</td>
            <td style="color:${item.color}; font-weight:bold;">${item.colorName}</td>
            <td>${formatCurrency(item.price)}</td>
            <td>${formatCurrency(item.price * item.quantity)}</td>
        </tr>`;
    });
    html += `
        </tbody>
    </table>
    <hr/>
    <p><strong>Total S/:</strong> ${formatCurrency(total)}</p>
    <p><strong>Son:</strong> ${numberToLetters(total)}</p>
    <div id="boleta-buttons">
        <button id="capture-button">📸 Capturar Imagen</button>
        <button id="print-button">🖨 Imprimir</button>
        <button id="confirm-purchase">Confirmar Compra</button>
    </div>
    `;

    const modal = document.getElementById('boleta-modal');
    const content = document.getElementById('boleta-content');
    content.innerHTML = html;
    modal.style.display = 'flex';
    content.focus();

    // Capturar imagen con html2canvas
    document.getElementById('capture-button').onclick = () => {
        document.getElementById('loading-spinner').style.display = 'block';
        html2canvas(content).then(canvas => {
            document.getElementById('loading-spinner').style.display = 'none';
            const link = document.createElement('a');
            link.download = 'boleta.png';
            link.href = canvas.toDataURL('image/png');
            link.click();
        }).catch(() => {
            alert('Error al capturar la imagen.');
            document.getElementById('loading-spinner').style.display = 'none';
        });
    };

    // Imprimir boleta
    document.getElementById('print-button').onclick = () => {
        let printWindow = window.open('', '', 'width=600,height=700');
        printWindow.document.write('<html><head><title>Imprimir Boleta</title></head><body>');
        printWindow.document.write(content.innerHTML);
        printWindow.document.write('</body></html>');
        printWindow.document.close();
        printWindow.focus();
        printWindow.print();
        printWindow.close();
    };

    // Confirmar compra - enviar por WhatsApp
    document.getElementById('confirm-purchase').onclick = () => {
        let orderText = `Hola! 👋%0AQuiero realizar un pedido:%0ACliente: ${clientName}%0ADNI: ${clientDni}%0AProductos:%0A`;
        cart.forEach(item => {
            orderText += `${item.quantity} x ${item.name} (Color: ${item.colorName}) - ${formatCurrency(item.price * item.quantity)}%0A`;
        });
        orderText += `Total: ${formatCurrency(total)}%0A%0AAdjunto (captura de boleta)📸 (pago electrónico)💳`;

        // Cambia el número por tu número real con código país sin "+"
        const whatsappURL = `https://wa.me/51975842622?text=${orderText}`;
        window.open(whatsappURL, '_blank');

        // Limpiar carrito y cerrar modal
        cart = [];
        localStorage.removeItem('cart');
        updateCart();
        modal.style.display = 'none';
        alert('Pedido enviado. ¡Gracias por su compra!');
    };
});

/* === Cerrar modal boleta al hacer clic fuera === */
document.getElementById('boleta-modal').addEventListener('click', e => {
    if (e.target.id === 'boleta-modal') {
        e.target.style.display = 'none';
    }
});

/* === Inicialización carrito al cargar === */
updateCart();

/* === Funciones y eventos para el carousel === */
const slides = document.querySelector('.carousel .slides');
const dots = document.querySelectorAll('.carousel .dots span');
let currentIndex = 0;
function showSlide(index) {
    slides.style.transform = `translateX(-${index * 100}%)`;
    dots.forEach((dot, i) => {
        dot.classList.toggle('active', i === index);
        dot.setAttribute('aria-selected', i === index ? 'true' : 'false');
    });
}
dots.forEach((dot, i) => {
    dot.addEventListener('click', () => {
        currentIndex = i;
        showSlide(currentIndex);
    });
    dot.addEventListener('keydown', e => {
        if(e.key === 'Enter' || e.key === ' ') {
            e.preventDefault();
            dot.click();
        }
    });
});
setInterval(() => {
    currentIndex = (currentIndex + 1) % dots.length;
    showSlide(currentIndex);
}, 5000);

/* === Modal "Ver Todo" === */
const viewAllModal = document.getElementById('viewAllModal');
const viewAllBtn = document.getElementById('viewAllBtn');
const viewAllProductsContainer = document.getElementById('viewAllProducts');
const viewAllCloseBtn = viewAllModal.querySelector('.close-btn');
const productSearch = document.getElementById('productSearch');

function cloneProductWithColorSelection(prod) {
    const clone = prod.cloneNode(true);
    // Reset color selection and buttons
    const colors = clone.querySelectorAll('.color-circle');
    colors.forEach(c => {
        c.classList.remove('selected');
        c.setAttribute('aria-checked', 'false');
        c.addEventListener('click', () => {
            colors.forEach(cc => {
                cc.classList.remove('selected');
                cc.setAttribute('aria-checked', 'false');
            });
            c.classList.add('selected');
            c.setAttribute('aria-checked', 'true');
            updateAddButtons();
        });
        c.addEventListener('keydown', e => {
            if(e.key === 'Enter' || e.key === ' ') {
                e.preventDefault();
                c.click();
            }
        });
    });
    const btn = clone.querySelector('.add-to-cart');
    btn.disabled = true;
    btn.textContent = 'Agregar al carrito';
    btn.addEventListener('click', e => {
        const prodElem = e.target.closest('.product');
        const id = prodElem.dataset.id;
        const name = prodElem.dataset.name;
        const price = parseFloat(prodElem.dataset.price);
        const selectedColorCircle = prodElem.querySelector('.color-circle.selected');
        if (!selectedColorCircle) {
            alert('Por favor, seleccione un color.');
            return;
        }
        const color = selectedColorCircle.getAttribute('data-color');
        const colorName = selectedColorCircle.getAttribute('data-colorname');
        addToCart(id, name, price, color, colorName);
    });
    return clone;
}

function updateViewAllProducts(searchTerm = '') {
    viewAllProductsContainer.innerHTML = '';
    const allProducts = document.querySelectorAll('.products .product');
    const filtered = Array.from(allProducts).filter(p => {
        const name = p.dataset.name.toLowerCase();
        return name.includes(searchTerm.toLowerCase());
    });
    filtered.forEach(p => {
        const clone = cloneProductWithColorSelection(p);
        viewAllProductsContainer.appendChild(clone);
    });
}

viewAllBtn.addEventListener('click', () => {
    productSearch.value = '';
    updateViewAllProducts();
    viewAllModal.style.display = 'flex';
    viewAllModal.setAttribute('aria-hidden', 'false');
    productSearch.focus();
});
viewAllCloseBtn.addEventListener('click', () => {
    viewAllModal.style.display = 'none';
    viewAllModal.setAttribute('aria-hidden', 'true');
});
viewAllModal.addEventListener('click', e => {
    if (e.target === viewAllModal) {
        viewAllModal.style.display = 'none';
        viewAllModal.setAttribute('aria-hidden', 'true');
    }
});
productSearch.addEventListener('input', () => {
    updateViewAllProducts(productSearch.value);
});

/* === Clips Damas Modal === */
const clipsDamasModal = document.getElementById('clipsDamasModal');
const clipsDamasBtn = document.getElementById('clipsDamasBtn');
const clipsDamasProductsContainer = document.getElementById('clipsDamasProducts');
const clipsDamasCloseBtn = clipsDamasModal.querySelector('.close-btn');
const clipsDamasSearch = document.getElementById('clipsDamasSearch');

function updateClipsDamasProducts(searchTerm = '') {
    clipsDamasProductsContainer.innerHTML = '';
    const allProducts = document.querySelectorAll('.products .product');
    const damasProducts = Array.from(allProducts).filter(p => {
        const id = parseInt(p.dataset.id);
        return id >= 1 && id <= 9; // Ajusta rango según tus productos Clips Damas
    });
    const filtered = damasProducts.filter(p => {
        const name = p.dataset.name.toLowerCase();
        return name.includes(searchTerm.toLowerCase());
    });
    filtered.forEach(p => {
        const clone = cloneProductWithColorSelection(p);
        clipsDamasProductsContainer.appendChild(clone);
    });
}
clipsDamasBtn.addEventListener('click', () => {
    clipsDamasSearch.value = '';
    updateClipsDamasProducts();
    clipsDamasModal.style.display = 'flex';
    clipsDamasModal.setAttribute('aria-hidden', 'false');
    clipsDamasSearch.focus();
});
clipsDamasCloseBtn.addEventListener('click', () => {
    clipsDamasModal.style.display = 'none';
    clipsDamasModal.setAttribute('aria-hidden', 'true');
});
clipsDamasModal.addEventListener('click', e => {
    if (e.target === clipsDamasModal) {
        clipsDamasModal.style.display = 'none';
        clipsDamasModal.setAttribute('aria-hidden', 'true');
    }
});
clipsDamasSearch.addEventListener('input', () => {
    updateClipsDamasProducts(clipsDamasSearch.value);
});

/* === Clips Niñas Modal === */
const clipsNinasModal = document.getElementById('clipsNinasModal');
const clipsNinasBtn = document.getElementById('clipsNinasBtn');
const clipsNinasProductsContainer = document.getElementById('clipsNinasProducts');
const clipsNinasCloseBtn = clipsNinasModal.querySelector('.close-btn');
const clipsNinasSearch = document.getElementById('clipsNinasSearch');

function updateClipsNinasProducts(searchTerm = '') {
    clipsNinasProductsContainer.innerHTML = '';
    const allProducts = document.querySelectorAll('.products .product');
    const ninasProducts = Array.from(allProducts).filter(p => {
        const id = parseInt(p.dataset.id);
        return id >= 14 && id <= 19; // Ajusta rango según tus productos Clips Niñas
    });
    const filtered = ninasProducts.filter(p => {
        const name = p.dataset.name.toLowerCase();
        return name.includes(searchTerm.toLowerCase());
    });
    filtered.forEach(p => {
        const clone = cloneProductWithColorSelection(p);
        clipsNinasProductsContainer.appendChild(clone);
    });
}
clipsNinasBtn.addEventListener('click', () => {
    clipsNinasSearch.value = '';
    updateClipsNinasProducts();
    clipsNinasModal.style.display = 'flex';
    clipsNinasModal.setAttribute('aria-hidden', 'false');
    clipsNinasSearch.focus();
});
clipsNinasCloseBtn.addEventListener('click', () => {
    clipsNinasModal.style.display = 'none';
    clipsNinasModal.setAttribute('aria-hidden', 'true');
});
clipsNinasModal.addEventListener('click', e => {
    if (e.target === clipsNinasModal) {
        clipsNinasModal.style.display = 'none';
        clipsNinasModal.setAttribute('aria-hidden', 'true');
    }
});
clipsNinasSearch.addEventListener('input', () => {
    updateClipsNinasProducts(clipsNinasSearch.value);
});

/* === Model Section imágenes clickables === */
document.querySelectorAll('.model-item').forEach(item => {
    const img = item.querySelector('img');
    const btn = item.querySelector('.category-btn');
    img.addEventListener('click', (e) => {
        e.preventDefault();
        btn.click();
    });
});

/* === Cerrar modales con Escape === */
document.addEventListener('keydown', (e) => {
    if (e.key === 'Escape') {
        if (viewAllModal.style.display === 'flex') {
            viewAllModal.style.display = 'none';
            viewAllModal.setAttribute('aria-hidden', 'true');
        }
        if (clipsDamasModal.style.display === 'flex') {
            clipsDamasModal.style.display = 'none';
            clipsDamasModal.setAttribute('aria-hidden', 'true');
        }
        if (clipsNinasModal.style.display === 'flex') {
            clipsNinasModal.style.display = 'none';
            clipsNinasModal.setAttribute('aria-hidden', 'true');
        }
        const boletaModal = document.getElementById('boleta-modal');
        if(boletaModal.style.display === 'flex'){
            boletaModal.style.display = 'none';
        }
    }
});
</script>
</body>
</html>
