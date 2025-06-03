<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>TodoModa - Tienda Online</title>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            color: #333;
        }
        .container {
            width: 100%;
            margin: 0;
            padding: 20px 0;
        }
        /* Header */
        .header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 10px 20px;
            border-bottom: 1px solid #ddd;
            width: 100%;
            box-sizing: border-box;
        }
        .header .logo img {
            height: 100px;
            width: auto;
        }
        .header nav ul {
            list-style: none;
            display: flex;
            gap: 20px;
            margin: 0;
            padding: 0;
        }
        .header nav ul li a {
            text-decoration: none;
            color: #333;
            font-weight: bold;
        }
        .header .icons {
            display: flex;
            gap: 10px;
            align-items: center;
        }
        .header .icons img {
            width: 20px;
            height: 20px;
            cursor: pointer;
        }
        .header .icons .cart-icon {
            position: relative;
        }
        .header .icons .cart-counter {
            position: absolute;
            top: -10px;
            right: -10px;
            background: #ff5722;
            color: #fff;
            border-radius: 50%;
            padding: 2px 6px;
            font-size: 0.8em;
        }
        #cart-button {
            background-color: #ff5722;
            color: white;
            padding: 10px;
            border-radius: 50%;
            cursor: pointer;
            font-size: 20px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
        }
        #cart-button:hover {
            background-color: #e64a19;
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
        /* Products */
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
            text-align: center;
            cursor: pointer;
            transition: transform 0.2s;
            position: relative;
            scroll-snap-align: start;
        }
        .product:hover {
            transform: scale(1.05);
        }
        .product img {
            width: 100%;
            height: auto;
            border-radius: 0;
            loading: lazy;
        }
        .product p {
            margin: 5px 0;
        }
        .product .price {
            font-weight: bold;
        }
        .product .add-to-cart {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, 80px);
            background: rgba(51, 51, 51, 0.8);
            color: #fff;
            border: none;
            padding: 10px 20px;
            border-radius: 5px;
            cursor: pointer;
            opacity: 0;
            transition: opacity 0.3s ease, transform 0.3s ease;
            font-size: 0.9em;
            width: 90%;
        }
        .product:hover .add-to-cart {
            opacity: 1;
            transform: translate(-50%, -50%);
        }
        .product .add-to-cart:hover {
            background: #555;
        }
        /* Modal */
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.5);
            z-index: 1000;
            justify-content: center;
            align-items: center;
            transition: opacity 0.3s ease;
        }
        .modal-content {
            background: #fff;
            padding: 20px;
            border-radius: 5px;
            max-width: 400px;
            width: 90%;
            text-align: center;
            position: relative;
        }
        .modal-content img {
            width: 100%;
            height: auto;
            border-radius: 5px;
            margin-bottom: 15px;
            loading: lazy;
        }
        .modal-content h3 {
            margin: 0 0 10px;
            font-size: 1.2em;
        }
        .modal-content .description {
            margin: 10px 0;
            font-size: 0.9em;
            color: #555;
        }
        .modal-content .rating {
            margin: 10px 0;
            color: #f1c40f;
        }
        .modal-content .price {
            font-weight: bold;
            margin: 10px 0;
        }
        .modal-content .color-palette {
            display: flex;
            gap: 10px;
            justify-content: center;
            flex-wrap: wrap;
            margin: 10px 0;
        }
        .modal-content .color-circle {
            width: 30px;
            height: 30px;
            border-radius: 50%;
            border: 1px solid #ddd;
            cursor: pointer;
            transition: transform 0.2s;
        }
        .modal-content .color-circle.selected {
            transform: scale(1.2);
            border: 2px solid #333;
        }
        .modal-content .quantity {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
            margin: 10px 0;
        }
        .modal-content .quantity-btn {
            background: #333;
            color: #fff;
            border: none;
            width: 30px;
            height: 30px;
            border-radius: 50%;
            cursor: pointer;
            font-size: 1.2em;
        }
        .modal-content .quantity-btn:hover {
            background: #555;
        }
        .modal-content .quantity-input {
            width: 40px;
            text-align: center;
            border: 1px solid #ddd;
            border-radius: 3px;
        }
        .modal-content .btn-add-cart {
            background: #333;
            color: #fff;
            border: none;
            padding: 10px;
            border-radius: 5px;
            cursor: pointer;
            width: 100%;
            margin-top: 10px;
        }
        .modal-content .btn-add-cart:hover {
            background: #555;
        }
        .modal-content .close-btn {
            position: absolute;
            top: 10px;
            right: 10px;
            font-size: 1.2em;
            cursor: pointer;
            color: #333;
        }
        /* Cart */
        #cart {
            display: none;
            position: fixed;
            top: 0;
            right: 0;
            width: 100%;
            height: 100%;
            background-image: url('https://via.placeholder.com/1024x1536?text=CartBackground');
            background-size: cover;
            background-repeat: no-repeat;
            background-position: center;
            box-shadow: -5px 0px 15px rgba(0, 0, 0, 0.1);
            z-index: 1000;
            padding: 0px;
            overflow-y: auto;
        }
        #cart h2 {
            font-size: 24px;
            margin-bottom: 20px;
            color: #333;
            text-align: center;
        }
        .cart-item {
            display: flex;
            flex-direction: column;
            background-color: #f9f9f9;
            margin-bottom: 10px;
            padding: 10px;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
            margin-left: 10px;
            margin-right: 10px;
        }
        .cart-item .product-info {
            display: flex;
            align-items: center;
            margin-bottom: 10px;
        }
        .cart-item .product-info img {
            width: 70px;
            height: 70px;
            border-radius: 8px;
            margin-right: 15px;
        }
        .cart-item .product-details {
            flex: 1;
        }
        .cart-item .actions {
            display: flex;
            gap: 8px;
            justify-content: flex-end;
        }
        #cart .cart-item .actions button {
            font-size: 12px;
            padding: 5px 8px;
            background-color: #f5f5f5;
            border: 1px solid #ccc;
            border-radius: 5px;
            cursor: pointer;
            transition: background-color 0.3s;
        }
        #cart .cart-item .actions button:hover {
            background-color: #e1e1e1;
        }
        #cart-total {
            font-size: 22px;
            font-weight: bold;
            color: #333;
            margin-bottom: 20px;
            text-align: center;
        }
        #order-button {
            width: 90%;
            padding: 15px;
            background-color: #ff5722;
            color: white;
            border: none;
            font-size: 18px;
            border-radius: 20px;
            cursor: pointer;
            transition: background-color 0.3s;
            display: block;
            margin: 0 auto 20px;
        }
        #order-button:hover {
            background-color: #e64a19;
        }
        #client-name, #client-dni {
            width: 90%;
            padding: 8px;
            margin: 5px auto;
            display: block;
            border: 1px solid #ddd;
            border-radius: 5px;
        }
        #loading-spinner {
            display: none;
            border: 4px solid #f3f3f3;
            border-top: 4px solid #333;
            border-radius: 50%;
            width: 24px;
            height: 24px;
            animation: spin 1s linear infinite;
            margin: 10px auto;
        }
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
        #boleta-modal div {
            background: white;
            padding: 20px;
            border-radius: 10px;
            max-width: 400px;
            width: 90%;
            max-height: 80vh;
            overflow-y: auto;
            font-family: monospace;
            font-size: 14px;
            line-height: 1.4;
            text-align: left;
        }
        #boleta-modal h3 {
            text-align: center;
            margin-bottom: 5px;
        }
        #boleta-modal img {
            width: 200px;
            border-radius: 10px;
            display: block;
            margin: 0 auto;
        }
        #boleta-modal p {
            margin: 0;
        }
        #boleta-modal hr {
            margin: 5px 0;
        }
        #boleta-modal table {
            width: 100%;
            font-size: 14px;
        }
        #boleta-modal button {
            margin-top: 10px;
            padding: 10px 20px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            color: white;
            width: 100%;
        }
        #capture-button {
            background: #FF9800;
        }
        #confirm-purchase {
            background: #4CAF50;
        }
        #boleta-modal button[onclick='window.print()'] {
            background: #2196F3;
        }
        /* View All and Category Modals */
        .view-all-modal, .clips-damas-modal, .clips-ninas-modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.5);
            z-index: 1000;
            justify-content: center;
            align-items: center;
            overflow-y: auto;
        }
        .view-all-modal-content, .clips-damas-modal-content, .clips-ninas-modal-content {
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
        .view-all-modal-content h2, .clips-damas-modal-content h2, .clips-ninas-modal-content h2 {
            margin: 0 0 20px;
            font-size: 1.5em;
            text-align: center;
        }
        .search-container {
            margin: 10px 0;
            text-align: center;
            position: relative;
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
        .sort-container {
            margin: 10px 0;
            text-align: center;
        }
        .sort-select {
            padding: 8px;
            border: 1px solid #ddd;
            border-radius: 5px;
            font-size: 1em;
        }
        .loading-spinner {
            display: none;
            border: 4px solid #f3f3f3;
            border-top: 4px solid #333;
            border-radius: 50%;
            width: 24px;
            height: 24px;
            animation: spin 1s linear infinite;
            margin: 10px auto;
        }
        .no-results {
            text-align: center;
            color: #555;
            margin: 20px 0;
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
        }
        .view-all-modal-content .close-btn, .clips-damas-modal-content .close-btn, .clips-ninas-modal-content .close-btn {
            position: absolute;
            top: 10px;
            right: 10px;
            font-size: 1.2em;
            cursor: pointer;
            color: #333;
        }
        /* Category Buttons */
        .category-buttons {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin: 20px 0;
        }
        .category-btn {
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
        .category-btn:hover {
            background: rgba(0, 0, 0, 0.7);
        }
        /* Model Section */
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
            loading: lazy;
        }
        .model-item .category-btn {
            position: absolute;
            bottom: 10px;
            left: 50%;
            transform: translateX(-50%);
            width: 80%;
        }
        /* Responsive */
        @media (max-width: 768px) {
            .product {
                width: 150px;
                min-width: 150px;
            }
            .product .add-to-cart {
                padding: 8px 15px;
                font-size: 0.8em;
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
            .product .add-to-cart {
                padding: 6px 10px;
                font-size: 0.7em;
            }
            .view-all-products, .clips-damas-products, .clips-ninas-products {
                grid-template-columns: repeat(auto-fill, minmax(100px, 1fr));
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
                <img src="https://lh3.googleusercontent.com/gps-cs/AIky0YXTTJyLqUwcNn1yduyV6i82lmL4ukvEZp-ePVd_P_Wa_y1VGwXNJOPpVxro2IxUZ55xE4oEndno5MItmJf7wjkFn0RYFCLtB4bOG2AHYHrupD1pkX8cf3jOUBHNUJOFEYOrwzTGEMSJj6j8=w1000-h1000-p-k-no" alt="TodoModa Logo" onerror="this.src='https://via.placeholder.com/100x100?text=Logo'">
            </div>
            <nav>
                <ul>
                    <li><a href="#inicio">Inicio</a></li>
                    <li><a href="#categorias">Categorías</a></li>
                    <li><a href="#contacto">Contacto</a></li>
                </ul>
            </nav>
            <div class="icons">
                <img src="https://via.placeholder.com/20x20?text=Search" alt="Ícono de búsqueda" class="search-icon">
                <img src="https://via.placeholder.com/20x20?text=Profile" alt="Ícono de perfil" class="profile-icon">
                <div class="cart-icon">
                    <div id="cart-button" onclick="toggleCart()" role="button" aria-label="Abrir carrito de compras">🛒</div>
                    <span class="cart-counter" id="cartCounter">0</span>
                </div>
            </div>
        </div>

        <!-- Carousel -->
 <div class="carousel">
            <div class="slides">
                <div class="slide-container">
                    <img src="https://pe.todomoda.com/media/wysiwyg/TM_DISNEY_STITCH_-_BANNERS_Desk_new_1.jpg" alt="Banner de promoción de accesorios" onerror="this.src='https://via.placeholder.com/1200x675?text=Banner'">
                </div>
                <div class="slide-container">
                    <img src="https://lh3.googleusercontent.com/gps-cs/AIky0YUd2bofobsLtUl3qONXRSiTNou1a9W74yTaVYEr6h64PAuOOqQ-g_w6Ifs8arhOVjWboOrUFEcEDZlmtSBZkgS1YjEnSIw1f3w4IZRdMBwxibVChvNz2c93C78bOxNsx68MuBmN-4iYNCg=w2000-h2000-p-k-no" alt="Banner de accesorios coloridos" onerror="this.src='https://via.placeholder.com/1200x675?text=Banner'">
                </div>
            </div>
            <div class="banner-text" id="viewAllBtn">VER TODO</div>
            <div class="dots">
                <span class="active" aria-label="Ir a la diapositiva 1"></span>
                <span aria-label="Ir a la diapositiva 2"></span>
            </div>
        </div>

        <!-- Product Listings -->
<div class="products">
            <!-- Categoría: Damas -->
            <div class="product" data-id="1" data-category="damas" data-colors='[{"color": "#ffeb3b", "title": "Amarillo"}, {"color": "#d32f2f", "title": "Rojo"}, {"color": "#e1bee7", "title": "Lila"}, {"color": "#145a32", "title": "Verde"}, {"color": "#d6eaf8", "title": "Celeste"}]' data-rating="⭐⭐⭐⭐☆ (4.2)" data-description="Maxilazos coloridos, perfectos para cualquier peinado.">
                <img alt="Maxilazos coloridos en amarillo, rojo, lila, verde y celeste" src="https://lh3.googleusercontent.com/gps-cs/AIky0YXdnjCFtJm5EhEvClhpsqjsYwwH2Xdqql3H45tWmgLdhiRX--KLwloCAl85SxTImNaOYYbS1MOrlGYrDwH31YoIyFBBn7KapQIKbAHVfoyNmbRBjjgmF0_SefXWn6udgSSaO19kdNtmnQBd=w2000-h2000-p-k-no" onerror="this.src='https://via.placeholder.com/200x200?text=Producto'" loading="lazy"/>
                <p>Maxilazos - 5 Colores</p>
                <p class="price">S/ 7.00</p>
                <button class="add-to-cart" data-id="1" role="button" aria-label="Agregar Maxilazos - 5 Colores al carrito">Agregar al carrito</button>
            </div>
            <div class="product" data-id="2" data-category="damas" data-colors='[{"color": "#17202a", "title": "Negro"}, {"color": "#fff9c4", "title": "Crema"}, {"color": "#fdebd0", "title": "Piel"}, {"color": "#fdfefe", "title": "Crema"}]' data-rating="⭐⭐⭐☆☆ (3.2)" data-description="Ganchos en forma de corazón, ideales para looks delicados.">
                <img alt="Mini ganchos en forma de corazón en negro, crema y piel" src="https://via.placeholder.com/200x200?text=Corazon" onerror="this.src='https://via.placeholder.com/200x200?text=Producto'" loading="lazy"/>
                <p>Mini Gancho Corazón</p>
                <p class="price">S/ 2.50</p>
                <button class="add-to-cart" data-id="2" role="button" aria-label="Agregar Mini Gancho Corazón al carrito">Agregar al carrito</button>
            </div>
            <div class="product" data-id="3" data-category="damas" data-colors='[{"color": "#FFFFFF", "title": "Blanco"}, {"color": "#FF0000", "title": "Rojo"}, {"color": "#008000", "title": "Verde"}]' data-rating="⭐⭐⭐⭐⭐ (5.0)" data-description="Ganchos temáticos navideños para un estilo festivo.">
                <img alt="Ganchos navideños en blanco, rojo y verde" src="https://via.placeholder.com/200x200?text=Navidenos" onerror="this.src='https://via.placeholder.com/200x200?text=Producto'" loading="lazy"/>
                <p>Ganchos Navideños</p>
                <p class="price">S/ 4.00</p>
                <button class="add-to-cart" data-id="3" role="button" aria-label="Agregar Ganchos Navideños al carrito">Agregar al carrito</button>
            </div>
            <div class="product" data-id="4" data-category="damas" data-colors='[{"color": "#FFD700", "title": "Amarillo"}]' data-rating="⭐⭐⭐⭐☆ (4.0)" data-description="Ganchos hawaianos vibrantes para un look tropical.">
                <img alt="Ganchos hawaianos en amarillo vibrante" src="https://via.placeholder.com/200x200?text=Hawaiano" onerror="this.src='https://via.placeholder.com/200x200?text=Producto'" loading="lazy"/>
                <p>Gancho Hawaiano</p>
                <p class="price">S/ 5.00</p>
                <button class="add-to-cart" data-id="4" role="button" aria-label="Agregar Gancho Hawaiano al carrito">Agregar al carrito</button>
            </div>
            <div class="product" data-id="5" data-category="damas" data-colors='[{"color": "#5dade2", "title": "Celeste"}, {"color": "#ebf5fb", "title": "Agua"}, {"color": "#FFFFFF", "title": "Blanco"}]' data-rating="⭐⭐⭐⭐☆ (4.0)" data-description="Ganchos acrílicos elegantes en tonos celestes.">
                <img alt="Ganchos acrílicos en celeste, agua y blanco" src="https://via.placeholder.com/200x200?text=Acrilicos" onerror="this.src='https://via.placeholder.com/200x200?text=Producto'" loading="lazy"/>
                <p>Ganchos Acrílicos Color Celeste</p>
                <p class="price">S/ 5.00</p>
                <button class="add-to-cart" data-id="5" role="button" aria-label="Agregar Ganchos Acrílicos Color Celeste al carrito">Agregar al carrito</button>
            </div>
            <div class="product" data-id="6" data-category="damas" data-colors='[{"color": "#8d6e63", "title": "Marrón"}, {"color": "#fef9e7", "title": "Crema"}]' data-rating="⭐⭐⭐☆☆ (3.1)" data-description="Ganchos clásicos para un estilo minimalista.">
                <img alt="Ganchos clásicos en marrón y crema" src="https://via.placeholder.com/200x200?text=Clasicos" onerror="this.src='https://via.placeholder.com/200x200?text=Producto'" loading="lazy"/>
                <p>Ganchos</p>
                <p class="price">S/ 4.50</p>
                <button class="add-to-cart" data-id="6" role="button" aria-label="Agregar Ganchos al carrito">Agregar al carrito</button>
            </div>
            <div class="product" data-id="7" data-category="damas" data-colors='[]' data-rating="⭐⭐⭐⭐☆ (4.1)" data-description="Ganchos en forma de flor con diseño inspirado en el sol.">
                <img alt="Ganchos en forma de flor inspirados en el sol" src="https://via.placeholder.com/200x200?text=FlorSol" onerror="this.src='https://via.placeholder.com/200x200?text=Producto'" loading="lazy"/>
                <p>Ganchos Torna Sol en forma de Flor</p>
                <p class="price">S/ 6.00</p>
                <button class="add-to-cart" data-id="7" role="button" aria-label="Agregar Ganchos Torna Sol en forma de Flor al carrito">Agregar al carrito</button>
            </div>
            <div class="product" data-id="8" data-category="damas" data-colors='[{"color": "#FFFF66", "title": "Amarillo"}, {"color": "#CCFF00", "title": "Verde"}, {"color": "#FF8C00", "title": "Anaranjado"}]' data-rating="⭐⭐⭐☆☆ (3.5)" data-description="Ganchos kawai con diseño floral, ideales para niños.">
                <img alt="Ganchos kawai en forma de flor en amarillo, verde y anaranjado" src="https://via.placeholder.com/200x200?text=Kawai" onerror="this.src='https://via.placeholder.com/200x200?text=Producto'" loading="lazy"/>
                <p>Ganchos Kawai en forma de Flor</p>
                <p class="price">S/ 4.50</p>
                <button class="add-to-cart" data-id="8" role="button" aria-label="Agregar Ganchos Kawai en forma de Flor al carrito">Agregar al carrito</button>
            </div>
            <div class="product" data-id="9" data-category="damas" data-colors='[{"color": "#FFB347", "title": "Melón"}, {"color": "#FFD700", "title": "Amarillo"}]' data-rating="⭐⭐⭐⭐☆ (4.0)" data-description="Ganchos florales en tonos cálidos para un look vibrante.">
                <img alt="Ganchos florales en melón y amarillo" src="https://via.placeholder.com/200x200?text=Florales" onerror="this.src='https://via.placeholder.com/200x200?text=Producto'" loading="lazy"/>
                <p>Ganchos de Flores</p>
                <p class="price">S/ 5.00</p>
                <button class="add-to-cart" data-id="9" role="button" aria-label="Agregar Ganchos de Flores al carrito">Agregar al carrito</button>
            </div>
            <!-- Categoría: Niñas -->
            <div class="product" data-id="14" data-category="ninas" data-colors='[]' data-rating="⭐⭐⭐⭐☆ (4.0)" data-description="Mini ganchitos florales para destacar tu peinado.">
                <img alt="Par de mini ganchitos en forma de flor" src="https://lh3.googleusercontent.com/gps-cs/AIky0YVcDqGO_EKNry0Eb-BkdsNH0V0lOhwW7AM5WEqz8IiNlbpTs2U3Io9_kt4yCGgt5haYI5RgwRDHv-LMBqc5bvmX245QMyriwIoyJyniPQH9cJJ9iCC2fC8hY06M9BU9nFd6NhCLGVGCC34N=w2000-h2000-p-k-no" onerror="this.src='https://via.placeholder.com/200x200?text=Producto'" loading="lazy"/>
                <p>Par de mini ganchitos en forma de flor</p>
                <p class="price">S/ 3.00</p>
                <button class="add-to-cart" data-id="14" role="button" aria-label="Agregar Par de mini ganchitos en forma de flor al carrito">Agregar al carrito</button>
            </div>
            <div class="product" data-id="15" data-category="ninas" data-colors='[]' data-rating="⭐⭐⭐☆☆ (3.5)" data-description="Ganchitos en forma de mariposa, perfectos para peinados infantiles.">
                <img alt="Mini ganchitos en forma de mariposa" src="https://lh3.googleusercontent.com/gps-cs/AIky0YW1eFtqiwT_PM-xOZnd2iVogh-XQVJclLEtgsh0i5wUGm9NvOCot9LJLfDmZE58abznArTin0EgjEMw3HuKeK9_9hoODK0kla3nM-GYGSvA8_xXCBmu_qiSuoHzgpSaO_2EtqXLAjnCs34l=w2000-h2000-p-k-no" onerror="this.src='https://via.placeholder.com/200x200?text=Producto'" loading="lazy"/>
                <p>Mini ganchitos en forma de mariposa</p>
                <p class="price">S/ 2.00</p>
                <button class="add-to-cart" data-id="15" role="button" aria-label="Agregar Mini ganchitos en forma de mariposa al carrito">Agregar al carrito</button>
            </div>
            <div class="product" data-id="16" data-category="ninas" data-colors='[]' data-rating="⭐⭐⭐☆☆ (3.3)" data-description="Mini ganchitos versátiles para cualquier ocasión.">
                <img alt="Mini ganchitos versátiles" src="https://lh3.googleusercontent.com/gps-cs/AIky0YUgnWieVRURnUHds0U4E5FROmRmvztpc0ynONqB5wFO-tvCmbrBn0-E971IAl2YG7r7cobC9Hx-g0AbDpTP71ukEEb6n20lHQz-aPBoI5xDWtVwABfSJFIbqdRT6_YJzOT7x8uhaX-KBSLE=w2000-h2000-p-k-no" onerror="this.src='https://via.placeholder.com/200x200?text=Producto'" loading="lazy"/>
                <p>Mini ganchitos</p>
                <p class="price">S/ 1.50</p>
                <button class="add-to-cart" data-id="16" role="button" aria-label="Agregar Mini ganchitos al carrito">Agregar al carrito</button>
            </div>
            <div class="product" data-id="17" data-category="ninas" data-colors='[{"color": "#FFC0CB", "title": "Rosa Pastel"}, {"color": "#FFD700", "title": "Amarillo"}, {"color": "#00BFFF", "title": "Azul"}, {"color": "#FF4500", "title": "Naranja"}, {"color": "#008000", "title": "Verde"}]' data-rating="⭐⭐⭐⭐☆ (4.0)" data-description="Ligas en colores pasteles y fuertes, ideales para cualquier estilo.">
                <img alt="Ligas en colores pasteles y fuertes" src="https://lh3.googleusercontent.com/gps-cs/AIky0YVwhLWhfaBVh3ChmdRjktxd6WCi7W6fTmz2_7TvWPHTT_-3tX1zci-DGspLNMmn3SpAYgh9RN5G_lHRBehTbWzF16lZ9CNiBbjgj5-EVSXMU3aVjCsYaPQ5Maahznx9Fi79zzSnwLxM_nkC=w2000-h2000-p-k-no" onerror="this.src='https://via.placeholder.com/200x200?text=Producto'" loading="lazy"/>
                <p>Ligas colores pasteles y fuertes</p>
                <p class="price">S/ 1.00</p>
                <button class="add-to-cart" data-id="17" role="button" aria-label="Agregar Ligas colores pasteles y fuertes al carrito">Agregar al carrito</button>
            </div>
            <div class="product" data-id="18" data-category="ninas" data-colors='[{"color": "#000000", "title": "Negro"}]' data-rating="⭐⭐⭐☆☆ (3.3)" data-description="Colets negros clásicos y resistentes.">
                <img alt="Colets negros clásicos" src="https://lh3.googleusercontent.com/gps-cs/AIky0YWE3Z0a1qVkSdmBI9RQzayKeT8bgvXn5RTJNXmMJjHG9uzg5VUrwt4-PKEq6AdcYPITi3LkJvKtdxDXq6PucsAOpzZGm2J8QGEYCR4Ff59f3YXXaKQ_Ww8lgm4vOYlRuyCNXxPuyWPFWf23=w2000-h2000-p-k-no" onerror="this.src='https://via.placeholder.com/200x200?text=Producto'" loading="lazy"/>
                <p>Colets negros</p>
                <p class="price">S/ 1.00</p>
                <button class="add-to-cart" data-id="18" role="button" aria-label="Agregar Colets negros al carrito">Agregar al carrito</button>
            </div>
            <div class="product" data-id="19" data-category="ninas" data-colors='[{"color": "#FFB6C1", "title": "Rosa Pastel"}, {"color": "#87CEFA", "title": "Azul Pastel"}, {"color": "#98FB98", "title": "Verde Pastel"}]' data-rating="⭐⭐⭐☆☆ (3.4)" data-description="Colets en tonos pasteles para un look suave y elegante.">
                <img alt="Colets en tonos pasteles rosa, azul y verde" src="https://lh3.googleusercontent.com/gps-cs/AIky0YVVXgYaHEulEuraO7tX6LShXlnoogs6cvwc7jryv8vOVwEt2wCEPWyj0ihUEHTjGMKv0HpL3uglAD96vZsANfdnMrLB4hRI1quw3OaPX-ewOFjUY9eF2ggyG4sMZLcBfJ8amsKoKsAgOXPG=w2000-h2000-p-k-no" onerror="this.src='https://via.placeholder.com/200x200?text=Producto'" loading="lazy"/>
                <p>Colets colores pasteles</p>
                <p class="price">S/ 1.00</p>
                <button class="add-to-cart" data-id="19" role="button" aria-label="Agregar Colets colores pasteles al carrito">Agregar al carrito</button>
            </div>
        </div>

        <!-- Model Section -->
 <div class="model-section">
            <div class="model-item">
                <img src="https://lh3.googleusercontent.com/gps-cs/AIky0YUGuPXaSC1mPGUKkOYa5z7JyvELvbIy0B4-WtB3tMHIKm2D6Sbg1cTWwU0MsxRJR_5lKb5t1MnVOStZk-tNPdUudQ6-h7M7ueR4l8N5IgmuOrhlNRMi0B_uohBDRomdzQUIHP7y244Zc150=w1024-h1024-p-k-no" alt="Accesorios para damas" onerror="this.src='https://via.placeholder.com/512x512?text=Damas'" loading="lazy">
                <button class="category-btn" id="clipsDamasBtn">CLIPS DAMAS</button>
            </div>
            <div class="model-item">
                <img src="https://lh3.googleusercontent.com/gps-cs/AIky0YUDER3L7ISerfG6uiIU8ISdgKkibO-SXwGGNL1azb_TJ0qYIN3T7LsJyU-qc9-kQtucnOkLr5rPYtWt0fW0UL8-7RDD46bg_0JnGLkD8RSfQvGydDvq6L_ZLBoj4hnIhwHB3CEx1fPtJ58O=w1024-h1024-p-k-no" alt="Accesorios para niñas" onerror="this.src='https://via.placeholder.com/512x512?text=Niñas'" loading="lazy">
                <button class="category-btn" id="clipsNinasBtn">CLIPS NIÑAS</button>
            </div>
        </div>

        <!-- Product Modal -->
  <div class="modal" id="colorModal" role="dialog" aria-labelledby="modalTitle" aria-hidden="true">
            <div class="modal-content">
                <span class="close-btn" role="button" aria-label="Cerrar modal" tabindex="0">×</span>
                <img id="modalImage" alt="" src="">
                <h3 id="modalTitle"></h3>
                <p class="description" id="modalDescription"></p>
                <div class="rating" id="modalRating"></div>
                <p class="price" id="modalPrice"></p>
                <div class="color-palette" id="modalColors"></div>
                <div class="quantity">
                    <button class="quantity-btn" id="decreaseQty" aria-label="Disminuir cantidad">−</button>
                    <input type="number" class="quantity-input" id="quantityInput" value="1" min="1" aria-label="Cantidad">
                    <button class="quantity-btn" id="increaseQty" aria-label="Aumentar cantidad">+</button>
                </div>
                <button class="btn-add-cart" id="modalAddCart">Agregar al carrito</button>
            </div>
        </div>

        <!-- View All Products Modal -->
 <div class="view-all-modal" id="viewAllModal" role="dialog" aria-labelledby="viewAllModalTitle" aria-hidden="true">
            <div class="view-all-modal-content">
                <span class="close-btn" role="button" aria-label="Cerrar modal" tabindex="0">×</span>
                <h2 id="viewAllModalTitle">Todos los Productos</h2>
                <div class="search-container">
                    <input type="text" class="search-input" id="productSearch" placeholder="Buscar productos..." aria-label="Buscar productos">
                    <div class="loading-spinner" id="viewAllSpinner"></div>
                </div>
                <div class="sort-container">
                    <select class="sort-select" id="viewAllSort" aria-label="Ordenar productos">
                        <option value="default">Orden por defecto</option>
                        <option value="price-asc">Precio: Menor a Mayor</option>
                        <option value="price-desc">Precio: Mayor a Menor</option>
                    </select>
                </div>
                <div class="view-all-products" id="viewAllProducts"></div>
            </div>
        </div>

        <!-- Clips Damas Modal -->
 <div class="clips-damas-modal" id="clipsDamasModal" role="dialog" aria-labelledby="clipsDamasModalTitle" aria-hidden="true">
            <div class="clips-damas-modal-content">
                <span class="close-btn" role="button" aria-label="Cerrar modal" tabindex="0">×</span>
                <h2 id="clipsDamasModalTitle">CLIPS DAMAS</h2>
                <div class="search-container">
                    <input type="text" class="search-input" id="clipsDamasSearch" placeholder="Buscar en Clips Damas..." aria-label="Buscar en Clips Damas">
                    <div class="loading-spinner" id="damasSpinner"></div>
                </div>
                <div class="sort-container">
                    <select class="sort-select" id="clipsDamasSort" aria-label="Ordenar productos">
                        <option value="default">Orden por defecto</option>
                        <option value="price-asc">Precio: Menor a Mayor</option>
                        <option value="price-desc">Precio: Mayor a Menor</option>
                    </select>
                </div>
                <div class="clips-damas-products" id="clipsDamasProducts"></div>
            </div>
        </div>

        <!-- Clips Niñas Modal -->
 <div class="clips-ninas-modal" id="clipsNinasModal" role="dialog" aria-labelledby="clipsNinasModalTitle" aria-hidden="true">
            <div class="clips-ninas-modal-content">
                <span class="close-btn" role="button" aria-label="Cerrar modal" tabindex="0">×</span>
                <h2 id="clipsNinasModalTitle">CLIPS NIÑAS</h2>
                <div class="search-container">
                    <input type="text" class="search-input" id="clipsNinasSearch" placeholder="Buscar en Clips Niñas..." aria-label="Buscar en Clips Niñas">
                    <div class="loading-spinner" id="ninasSpinner"></div>
                </div>
                <div class="sort-container">
                    <select class="sort-select" id="clipsNinasSort" aria-label="Ordenar productos">
                        <option value="default">Orden por defecto</option>
                        <option value="price-asc">Precio: Menor a Mayor</option>
                        <option value="price-desc">Precio: Mayor a Menor</option>
                    </select>
                </div>
                <div class="clips-ninas-products" id="clipsNinasProducts"></div>
            </div>
        </div>

        <!-- Cart Section -->
 <section id="cart" role="dialog" aria-labelledby="cartTitle" aria-hidden="true">
            <h2 id="cartTitle">Carrito de Compras</h2>
            <div style="margin:10px 0;">
                <input id="client-name" placeholder="Nombre del cliente" type="text" aria-label="Nombre del cliente"/>
                <input id="client-dni" placeholder="DNI del cliente (8 dígitos)" type="text" aria-label="DNI del cliente"/>
            </div>
            <div id="cart-items"></div>
            <p id="cart-total">Total: S/ 0.00</p>
            <button id="order-button" role="button" aria-label="Realizar pedido">Realizar Pedido</button>
        </section>

        <!-- Loading Spinner -->
 <div id="loading-spinner"></div>
    </div>
<script>
$(document).ready(function() {
    // Cart Management
    function getCart() {
        try {
            return JSON.parse(localStorage.getItem('cart') || '[]');
        } catch (e) {
            console.error('Error accessing localStorage:', e);
            return [];
        }
    }

    function saveCart(cart) {
        try {
            localStorage.setItem('cart', JSON.stringify(cart));
        } catch (e) {
            console.error('Error saving to localStorage:', e);
        }
    }

    let cart = getCart();
    const whatsappNumber = '51975842622';

    function formatCurrency(amount) {
        return `S/ ${parseFloat(amount).toFixed(2)}`;
    }

    function updateCartCounter() {
        const totalItems = cart.reduce((sum, item) => sum + parseInt(item.quantity), 0);
        $('#cartCounter').text(totalItems);
    }

    function updateCart() {
        let cartItemsHtml = '';
        let total = 0;
        cart.forEach(item => {
            cartItemsHtml += `
                <div class="cart-item">
                    <div class="product-info">
                        <img alt="${item.name}" src="${item.image}"/>
                        <div class="product-details">
                            <p style="margin: 0; font-weight: bold;">${item.name}</p>
                            <p style="margin: 0;">Precio unitario: ${formatCurrency(item.price)}</p>
                            <p style="margin: 0;">Cantidad: ${item.quantity}</p>
                            ${item.color ? `<p style="margin: 0;">Color: ${item.color}</p>` : ''}
                        </div>
                    </div>
                    <div class="actions">
                        <button class="increase-quantity" data-product="${item.id}" role="button" aria-label="Aumentar cantidad de ${item.name}">+</button>
                        <button class="decrease-quantity" data-product="${item.id}" role="button" aria-label="Disminuir cantidad de ${item.name}">-</button>
                        <button class="remove-item" data-product="${item.id}" role="button" aria-label="Eliminar ${item.name} del carrito">🗑️ Eliminar</button>
                    </div>
                </div>
            `;
            total += item.price * item.quantity;
        });
        $('#cart-items').html(cartItemsHtml || '<p>El carrito está vacío.</p>');
        $('#cart-total').text(`Total: ${formatCurrency(total)}`);
        saveCart(cart);
        updateCartCounter();
    }

    $(document).on('click', '.increase-quantity', function() {
        const productId = $(this).data('product');
        let product = cart.find(item => item.id === productId);
        if (product) {
            product.quantity++;
            updateCart();
        }
    });

    $(document).on('click', '.decrease-quantity', function() {
        const productId = $(this).data('product');
        let product = cart.find(item => item.id === productId);
        if (product) {
            product.quantity--;
            if (product.quantity === 0) {
                cart = cart.filter(item => item.id !== productId);
            }
            updateCart();
        }
    });

    $(document).on('click', '.remove-item', function() {
        const productId = $(this).data('product');
        cart = cart.filter(item => item.id !== productId);
        updateCart();
    });

    function trapFocus(element) {
        const focusableElements = element.querySelectorAll('button, [href], input, select, textarea, [tabindex]:not([tabindex="-1"])');
        const firstFocusable = focusableElements[0];
        const lastFocusable = focusableElements[focusableElements.length - 1];
        element.addEventListener('keydown', (e) => {
            if (e.key === 'Tab') {
                if (e.shiftKey && document.activeElement === firstFocusable) {
                    e.preventDefault();
                    lastFocusable.focus();
                } else if (!e.shiftKey && document.activeElement === lastFocusable) {
                    e.preventDefault();
                    firstFocusable.focus();
                }
            }
        });
    }

    window.toggleCart = function() {
        $('#cart').toggle();
        $('#cart').attr('aria-hidden', $('#cart').is(':hidden'));
        if (!$('#cart').is(':hidden')) {
            $('#client-name').focus();
            trapFocus(document.getElementById('cart'));
        }
    };

    $('#order-button').click(function() {
        const clientName = $('#client-name').val().trim();
        const clientDni = $('#client-dni').val().trim();
        if (!clientName || !clientDni) {
            alert("Por favor, complete nombre y DNI.");
            return;
        }
        if (!/^\d{8}$/.test(clientDni)) {
            alert("El DNI debe tener exactamente 8 dígitos.");
            return;
        }
        if (cart.length === 0) {
            alert("El carrito está vacío. Agregue productos antes de realizar el pedido.");
            return;
        }

        let fecha = new Date();
        let fechaStr = fecha.toLocaleDateString();
        let horaStr = fecha.toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' });
        let total = cart.reduce((sum, item) => sum + item.price * item.quantity, 0);

        const enLetras = (n) => {
            const parts = n.toFixed(2).split('.');
            return `${Number(parts[0])} CON ${parts[1]}/100 SOLES`;
        };

        let boletaHtml = `
            <div style="font-family: monospace; font-size: 14px; line-height: 1.4; text-align: left;">
                <h3 style="text-align: center; margin-bottom: 5px;">BOLETA DE VENTA ELECTRÓNICA</h3>
                <div style="text-align: center; margin: 15px 0;">
                    <img id="qr-image" src="https://via.placeholder.com/200x200?text=QRCode" style="width: 200px; border-radius: 10px;"/>
                    <p style="margin: 5px 0; font-size: 12px;">Paga aquí con Yape</p>
                    <p style="margin: 0; font-size: 12px;">Jhonny David Palacios Gutierrez</p>
                </div>
                <p style="margin:0;"><strong>CLIENTE:</strong> ${clientName}</p>
                <p style="margin:0;"><strong>DNI:</strong> ${clientDni}</p>
                <p style="margin:0;"><strong>FECHA:</strong> ${fechaStr}   <strong>HORA:</strong> ${horaStr}</p>
                <hr/>
                <p style="margin: 0;"><strong>Cant U.M PRODUCTO P.U. TOTAL</strong></p>`;
        cart.forEach(item => {
            boletaHtml += `
                <p style="margin: 0;">${item.quantity} UNIDAD ${item.name.substring(0,24)} ${formatCurrency(item.price)} ${formatCurrency(item.price * item.quantity)}</p>`;
        });
        boletaHtml += `
                <hr/>
                <table style="width: 100%; font-size: 14px;">
                    <tr>
                        <td style="text-align: left;"><strong>TOTAL (S/)</strong></td>
                        <td style="text-align: right;"><strong>${formatCurrency(total)}</strong></td>
                    </tr>
                </table>
                <hr/>
                <p style="margin: 0;"><strong>SON:</strong> ${enLetras(total)}</p>
                <button id="capture-button">📸 Capturar Imagen</button>
                <button onclick="window.print()">🖨 Imprimir</button>
                <button id="confirm-purchase">Confirmar Compra</button>
            </div>`;

        const modal = document.createElement('div');
        modal.id = "boleta-modal";
        modal.style = "position:fixed; top:0; left:0; width:100%; height:100%; background:rgba(0,0,0,0.6); display:flex; align-items:center; justify-content:center; z-index:2000;";
        modal.innerHTML = boletaHtml;
        document.body.appendChild(modal);

        $('#capture-button').click(function() {
            $('#loading-spinner').show();
            const contentDiv = modal.querySelector('div');
            const prevMaxHeight = contentDiv.style.maxHeight;
            const prevOverflow = contentDiv.style.overflowY;
            contentDiv.style.maxHeight = 'none';
            contentDiv.style.overflowY = 'visible';
            html2canvas(contentDiv, {
                useCORS: true,
                allowTaint: false,
                scale: 2
            }).then(canvas => {
                contentDiv.style.maxHeight = prevMaxHeight;
                contentDiv.style.overflowY = prevOverflow;
                $('#loading-spinner').hide();
                const link = document.createElement('a');
                link.download = 'boleta.png';
                link.href = canvas.toDataURL('image/png');
                link.click();
            }).catch(error => {
                $('#loading-spinner').hide();
                console.error('Error al capturar:', error);
                alert('No se pudo capturar la boleta. Por favor, intenta de nuevo.');
            });
        });

        $('#confirm-purchase').click(function() {
            let orderDetails = `Hola! 👋 Quiero realizar un pedido:\n\nCliente: ${clientName}\nDNI: ${clientDni}\n\nProductos:\n`;
            cart.forEach(item => {
                orderDetails += `${item.quantity} x ${item.name} - ${formatCurrency(item.price * item.quantity)}\n`;
            });
            orderDetails += `\nTotal: ${formatCurrency(total)}`;
            orderDetails += `\n\nAdjuntar: (captura de boleta)📸 (pago electrónico)💳`;
            let whatsappURL = `https://wa.me/${whatsappNumber}?text=${encodeURIComponent(orderDetails)}`;
            window.open(whatsappURL, '_blank');
            document.body.removeChild(modal);
            cart = [];
            saveCart(cart);
            updateCart();
            const successMsg = document.createElement('div');
            successMsg.textContent = "✅ Mensaje de WhatsApp listo";
            successMsg.style = "position:fixed; top:20px; right:20px; background:#4CAF50; color:white; padding:10px 20px; border-radius:5px; font-size:16px; z-index:3000;";
            document.body.appendChild(successMsg);
            setTimeout(() => {
                document.body.removeChild(successMsg);
                toggleCart();
            }, 2000);
        });

        modal.addEventListener('click', function(e) {
            if (e.target === modal) {
                document.body.removeChild(modal);
            }
        });
    });

    // Carousel functionality
    const slides = document.querySelector('.carousel .slides');
    const dots = document.querySelectorAll('.carousel .dots span');
    let currentIndex = 0;

    function showSlide(index) {
        slides.style.transform = `translateX(-${index * 100}%)`;
        dots.forEach((dot, i) => {
            dot.classList.toggle('active', i === index);
        });
    }

    dots.forEach((dot, i) => {
        dot.addEventListener('click', () => {
            currentIndex = i;
            showSlide(currentIndex);
        });
    });

    setInterval(() => {
        currentIndex = (currentIndex + 1) % dots.length;
        showSlide(currentIndex);
    }, 5000);

    // Keyboard navigation for carousel
    document.addEventListener('keydown', (e) => {
        if (e.key === 'ArrowLeft') {
            currentIndex = (currentIndex - 1 + dots.length) % dots.length;
            showSlide(currentIndex);
        } else if (e.key === 'ArrowRight') {
            currentIndex = (currentIndex + 1) % dots.length;
            showSlide(currentIndex);
        }
    });

    // Product Modal functionality
    const modal = document.getElementById('colorModal');
    const modalImage = document.getElementById('modalImage');
    const modalTitle = document.getElementById('modalTitle');
    const modalDescription = document.getElementById('modalDescription');
    const modalRating = document.getElementById('modalRating');
    const modalPrice = document.getElementById('modalPrice');
    const modalColors = document.getElementById('modalColors');
    const modalAddCart = document.getElementById('modalAddCart');
    const decreaseQty = document.getElementById('decreaseQty');
    const increaseQty = document.getElementById('increaseQty');
    const quantityInput = document.getElementById('quantityInput');
    const closeBtn = document.querySelector('.modal .close-btn');

    let selectedColor = null;

    function openProductModal(productId) {
        const product = document.querySelector(`.product[data-id="${productId}"]`);
        if (!product) return;
        const id = product.getAttribute('data-id');
        const name = product.querySelector('p').textContent;
        const price = parseFloat(product.querySelector('.price').textContent.replace('S/ ', ''));
        const image = product.querySelector('img').src;
        const alt = product.querySelector('img').alt;
        const colors = JSON.parse(product.getAttribute('data-colors') || '[]');
        const rating = product.getAttribute('data-rating');
        const description = product.getAttribute('data-description');

        modalImage.src = image;
        modalImage.alt = alt;
        modalTitle.textContent = name;
        modalDescription.textContent = description;
        modalRating.textContent = rating;
        modalPrice.textContent = `S/ ${price.toFixed(2)}`;
        modalAddCart.setAttribute('data-id', id);
        modalAddCart.setAttribute('data-name', name);
        modalAddCart.setAttribute('data-price', price);
        modalAddCart.setAttribute('data-img', image);

        modalColors.innerHTML = colors.map(color => 
            `<span class="color-circle" style="background-color: ${color.color};" data-title="${color.title}" data-color="${color.color}"></span>`
        ).join('');
        modalColors.style.display = colors.length === 0 ? 'none' : 'flex';

        quantityInput.value = 1;
        selectedColor = null;
        modalColors.querySelectorAll('.color-circle').forEach(circle => {
            circle.classList.remove('selected');
            circle.addEventListener('click', () => {
                modalColors.querySelectorAll('.color-circle').forEach(c => c.classList.remove('selected'));
                circle.classList.add('selected');
                selectedColor = circle.dataset.color;
            });
        });

        modal.style.display = 'flex';
        modal.setAttribute('aria-hidden', 'false');
        modal.querySelector('.modal-content').focus();
    }

    // Quantity controls
    decreaseQty.addEventListener('click', () => {
        let qty = parseInt(quantityInput.value);
        if (qty > 1) {
            quantityInput.value = qty - 1;
        }
    });

    increaseQty.addEventListener('click', () => {
        let qty = parseInt(quantityInput.value);
        quantityInput.value = qty + 1;
    });

    quantityInput.addEventListener('input', () => {
        if (quantityInput.value < 1) {
            quantityInput.value = 1;
        }
    });

    // Add to cart
    modalAddCart.addEventListener('click', function() {
        const id = modalAddCart.getAttribute('data-id');
        const name = modalAddCart.getAttribute('data-name');
        const price = parseFloat(modalAddCart.getAttribute('data-price'));
        const image = modalAddCart.getAttribute('data-img');
        const quantity = parseInt(quantityInput.value);
        const colors = JSON.parse(document.querySelector(`.product[data-id="${id}"]`).getAttribute('data-colors') || '[]');
        if (colors.length > 0 && !selectedColor) {
            alert('Por favor, selecciona un color antes de añadir al carrito.');
            return;
        }
        const color = colors.length > 0 ? colors.find(c => c.color === selectedColor).title : 'Ninguno';
        const existingItem = cart.find(item => item.id === id && item.color === color);
        if (existingItem) {
            existingItem.quantity += quantity;
        } else {
            cart.push({ id, name, price, quantity, image, color });
        }
        updateCart();
        alert(`Añadido al carrito: ${name}, Cantidad: ${quantity}, Color: ${color}, Precio: ${formatCurrency(price * quantity)}`);
        modal.style.display = 'none';
        modal.setAttribute('aria-hidden', 'true');
    });

    // Close product modal
    closeBtn.addEventListener('click', () => {
        modal.style.display = 'none';
        modal.setAttribute('aria-hidden', 'true');
    });

    modal.addEventListener('click', (e) => {
        if (e.target === modal) {
            modal.style.display = 'none';
            modal.setAttribute('aria-hidden', 'true');
        }
    });

    // Add keyboard support for close buttons
    document.querySelectorAll('.close-btn').forEach(btn => {
        btn.addEventListener('keypress', (e) => {
            if (e.key === 'Enter' || e.key === ' ') {
                btn.click();
            }
        });
    });

    // Product event listeners
    function attachProductListeners(products) {
        products.forEach(product => {
            product.addEventListener('click', (e) => {
                if (e.target.classList.contains('add-to-cart') || e.target.classList.contains('quantity-btn') || e.target.classList.contains('quantity-input')) return;
                openProductModal(product.getAttribute('data-id'));
            });
            product.querySelector('.add-to-cart').addEventListener('click', (e) => {
                e.stopPropagation();
                openProductModal(product.getAttribute('data-id'));
            });
        });
    }

    const allProducts = document.querySelectorAll('.products .product');
    attachProductListeners(allProducts);

    // View All Products Modal functionality
    const viewAllModal = document.getElementById('viewAllModal');
    const viewAllBtn = document.getElementById('viewAllBtn');
    const viewAllProductsContainer = document.getElementById('viewAllProducts');
    const viewAllCloseBtn = document.querySelector('.view-all-modal .close-btn');
    const productSearch = document.getElementById('productSearch');
    const viewAllSort = document.getElementById('viewAllSort');
    const viewAllSpinner = document.getElementById('viewAllSpinner');

    function updateViewAllProducts(searchTerm = '', sort = 'default') {
        viewAllSpinner.style.display = 'block';
        viewAllProductsContainer.innerHTML = '';
        setTimeout(() => {
            let filteredProducts = Array.from(allProducts).filter(product => {
                const name = product.querySelector('p').textContent.toLowerCase();
                const description = product.getAttribute('data-description').toLowerCase();
                return name.includes(searchTerm.toLowerCase()) || description.includes(searchTerm.toLowerCase());
            });

            if (sort === 'price-asc') {
                filteredProducts.sort((a, b) => parseFloat(a.querySelector('.price').textContent.replace('S/ ', '')) - parseFloat(b.querySelector('.price').textContent.replace('S/ ', '')));
            } else if (sort === 'price-desc') {
                filteredProducts.sort((a, b) => parseFloat(b.querySelector('.price').textContent.replace('S/ ', '')) - parseFloat(a.querySelector('.price').textContent.replace('S/ ', '')));
            }

            if (filteredProducts.length === 0) {
                viewAllProductsContainer.innerHTML = '<p class="no-results">No se encontraron productos.</p>';
                viewAllSpinner.style.display = 'none';
                return;
            }

            filteredProducts.forEach(product => {
                const productClone = product.cloneNode(true);
                viewAllProductsContainer.appendChild(productClone);
            });

            attachProductListeners(viewAllProductsContainer.querySelectorAll('.product'));
            viewAllSpinner.style.display = 'none';
        }, 500);
    }

    viewAllBtn.addEventListener('click', () => {
        productSearch.value = '';
        viewAllSort.value = 'default';
        updateViewAllProducts();
        viewAllModal.style.display = 'flex';
        viewAllModal.setAttribute('aria-hidden', 'false');
        productSearch.focus();
    });

    productSearch.addEventListener('input', () => {
        updateViewAllProducts(productSearch.value, viewAllSort.value);
    });

    viewAllSort.addEventListener('change', () => {
        updateViewAllProducts(productSearch.value, viewAllSort.value);
    });

    viewAllCloseBtn.addEventListener('click', () => {
        viewAllModal.style.display = 'none';
        viewAllModal.setAttribute('aria-hidden', 'true');
    });

    viewAllModal.addEventListener('click', (e) => {
        if (e.target === viewAllModal) {
            viewAllModal.style.display = 'none';
            viewAllModal.setAttribute('aria-hidden', 'true');
        }
    });

    // Clips Damas Modal functionality
    const clipsDamasModal = document.getElementById('clipsDamasModal');
    const clipsDamasBtn = document.getElementById('clipsDamasBtn');
    const clipsDamasProductsContainer = document.getElementById('clipsDamasProducts');
    const clipsDamasCloseBtn = document.querySelector('.clips-damas-modal .close-btn');
    const clipsDamasSearch = document.getElementById('clipsDamasSearch');
    const clipsDamasSort = document.getElementById('clipsDamasSort');
    const damasSpinner = document.getElementById('damasSpinner');

    function updateClipsDamasProducts(searchTerm = '', sort = 'default') {
        damasSpinner.style.display = 'block';
        clipsDamasProductsContainer.innerHTML = '';
        setTimeout(() => {
            let filteredProducts = Array.from(allProducts).filter(product => {
                const name = product.querySelector('p').textContent.toLowerCase();
                const description = product.getAttribute('data-description').toLowerCase();
                const category = product.getAttribute('data-category');
                return (name.includes(searchTerm.toLowerCase()) || description.includes(searchTerm.toLowerCase())) && category === 'damas';
            });

            if (sort === 'price-asc') {
                filteredProducts.sort((a, b) => parseFloat(a.querySelector('.price').textContent.replace('S/ ', '')) - parseFloat(b.querySelector('.price').textContent.replace('S/ ', '')));
            } else if (sort === 'price-desc') {
                filteredProducts.sort((a, b) => parseFloat(b.querySelector('.price').textContent.replace('S/ ', '')) - parseFloat(a.querySelector('.price').textContent.replace('S/ ', '')));
            }

            if (filteredProducts.length === 0) {
                clipsDamasProductsContainer.innerHTML = '<p class="no-results">No se encontraron productos.</p>';
                damasSpinner.style.display = 'none';
                return;
            }

            filteredProducts.forEach(product => {
                const productClone = product.cloneNode(true);
                clipsDamasProductsContainer.appendChild(productClone);
            });

            attachProductListeners(clipsDamasProductsContainer.querySelectorAll('.product'));
            damasSpinner.style.display = 'none';
        }, 500);
    }

    clipsDamasBtn.addEventListener('click', () => {
        clipsDamasSearch.value = '';
        clipsDamasSort.value = 'default';
        updateClipsDamasProducts();
        clipsDamasModal.style.display = 'flex';
        clipsDamasModal.setAttribute('aria-hidden', 'false');
        clipsDamasSearch.focus();
    });

    clipsDamasSearch.addEventListener('input', () => {
        updateClipsDamasProducts(clipsDamasSearch.value, clipsDamasSort.value);
    });

    clipsDamasSort.addEventListener('change', () => {
        updateClipsDamasProducts(clipsDamasSearch.value, clipsDamasSort.value);
    });

    clipsDamasCloseBtn.addEventListener('click', () => {
        clipsDamasModal.style.display = 'none';
        clipsDamasModal.setAttribute('aria-hidden', 'true');
    });

    clipsDamasModal.addEventListener('click', (e) => {
        if (e.target === clipsDamasModal) {
            clipsDamasModal.style.display = 'none';
            clipsDamasModal.setAttribute('aria-hidden', 'true');
        }
    });

    // Clips Niñas Modal functionality
    const clipsNinasModal = document.getElementById('clipsNinasModal');
    const clipsNinasBtn = document.getElementById('clipsNinasBtn');
    const clipsNinasProductsContainer = document.getElementById('clipsNinasProducts');
    const clipsNinasCloseBtn = document.querySelector('.clips-ninas-modal .close-btn');
    const clipsNinasSearch = document.getElementById('clipsNinasSearch');
    const clipsNinasSort = document.getElementById('clipsNinasSort');
    const ninasSpinner = document.getElementById('ninasSpinner');

    function updateClipsNinasProducts(searchTerm = '', sort = 'default') {
        ninasSpinner.style.display = 'block';
        clipsNinasProductsContainer.innerHTML = '';
        setTimeout(() => {
            let filteredProducts = Array.from(allProducts).filter(product => {
                const name = product.querySelector('p').textContent.toLowerCase();
                const description = product.getAttribute('data-description').toLowerCase();
                const category = product.getAttribute('data-category');
                return (name.includes(searchTerm.toLowerCase()) || description.includes(searchTerm.toLowerCase())) && category === 'ninas';
            });

            if (sort === 'price-asc') {
                filteredProducts.sort((a, b) => parseFloat(a.querySelector('.price').textContent.replace('S/ ', '')) - parseFloat(b.querySelector('.price').textContent.replace('S/ ', '')));
            } else if (sort === 'price-desc') {
                filteredProducts.sort((a, b) => parseFloat(b.querySelector('.price').textContent.replace('S/ ', '')) - parseFloat(a.querySelector('.price').textContent.replace('S/ ', '')));
            }

            if (filteredProducts.length === 0) {
                clipsNinasProductsContainer.innerHTML = '<p class="no-results">No se encontraron productos.</p>';
                ninasSpinner.style.display = 'none';
                return;
            }

            filteredProducts.forEach(product => {
                const productClone = product.cloneNode(true);
                clipsNinasProductsContainer.appendChild(productClone);
            });

            attachProductListeners(clipsNinasProductsContainer.querySelectorAll('.product'));
            ninasSpinner.style.display = 'none';
        }, 500);
    }

    clipsNinasBtn.addEventListener('click', () => {
        clipsNinasSearch.value = '';
        clipsNinasSort.value = 'default';
        updateClipsNinasProducts();
        clipsNinasModal.style.display = 'flex';
        clipsNinasModal.setAttribute('aria-hidden', 'false');
        clipsNinasSearch.focus();
    });

    clipsNinasSearch.addEventListener('input', () => {
        updateClipsNinasProducts(clipsNinasSearch.value, clipsNinasSort.value);
    });

    clipsNinasSort.addEventListener('change', () => {
        updateClipsNinasProducts(clipsNinasSearch.value, clipsNinasSort.value);
    });

    clipsNinasCloseBtn.addEventListener('click', () => {
        clipsNinasModal.style.display = 'none';
        clipsNinasModal.setAttribute('aria-hidden', 'true');
    });

    clipsNinasModal.addEventListener('click', (e) => {
        if (e.target === clipsNinasModal) {
            clipsNinasModal.style.display = 'none';
            clipsNinasModal.setAttribute('aria-hidden', 'true');
        }
    });

    // Initialize cart
    updateCart();
});
</script>
</body>
</html>
