<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>TodoModa - Tienda Online</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            color: #333;
            background-color: #f9f9f9;
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
            background: white;
            position: sticky;
            top: 0;
            z-index: 100;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }
        .header .logo img {
            height: 60px;
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
            transition: color 0.3s;
        }
        .header nav ul li a:hover {
            color: #d81b60;
        }
        .header-icons {
            display: flex;
            gap: 15px;
        }
        .cart-icon {
            position: relative;
            cursor: pointer;
            font-size: 1.4rem;
        }
        .cart-count {
            position: absolute;
            top: -8px;
            right: -10px;
            background: #d81b60;
            color: white;
            border-radius: 50%;
            width: 20px;
            height: 20px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 0.7rem;
            font-weight: bold;
        }
        /* Carousel */
        .carousel {
            position: relative;
            width: 100%;
            overflow: hidden;
            margin: 20px 0;
            border-radius: 10px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
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
            loading: lazy;
        }
        .carousel .banner-text {
            position: absolute;
            bottom: 30px;
            left: 50%;
            transform: translateX(-50%);
            font-size: 1.8em;
            font-weight: bold;
            color: #fff;
            background: rgba(0,0,0,0.6);
            padding: 12ദ
            border-radius: 30px;
            cursor: pointer;
            transition: all 0.3s;
            text-transform: uppercase;
        }
        .carousel .banner-text:hover {
            background: rgba(0,0,0,0.8);
            transform: translateX(-50%) scale(1.05);
        }
        .carousel .dots {
            position: absolute;
            bottom: 15px;
            left: 50%;
            transform: translateX(-50%);
            display: flex;
            gap: 10px;
        }
        .carousel .dots span {
            width: 12px;
            height: 12px;
            background-color: rgba(255,255,255,0.6);
            border-radius: 50%;
            cursor: pointer;
            transition: all 0.3s;
        }
        .carousel .dots span.active {
            background-color: white;
            transform: scale(1.2);
        }
        .carousel-controls {
            position: absolute;
            top: 50%;
            width: 100%;
            display: flex;
            justify-content: space-between;
            transform: translateY(-50%);
            padding: 0 10px;
            box-sizing: border-box;
        }
        .carousel-controls button {
            background: rgba(0,0,0,0.5);
            color: white;
            border: none;
            padding: 10px;
            cursor: pointer;
            font-size: 1.2rem;
            border-radius: 50%;
            transition: background 0.3s;
        }
        .carousel-controls button:hover {
            background: rgba(0,0,0,0.8);
        }
        /* Products */
        .section-title {
            text-align: center;
            margin: 30px 0 20px;
            font-size: 1.8rem;
            position: relative;
            padding-bottom: 10px;
        }
        .section-title::after {
            content: '';
            position: absolute;
            bottom: 0;
            left: 50%;
            transform: translateX(-50%);
            width: 80px;
            height: 3px;
            background: #d81b60;
        }
        .products {
            display: flex;
            flex-direction: row;
            overflow-x: auto;
            margin: 20px 0;
            padding: 0 20px;
            width: 100%;
            box-sizing: border-box;
            gap: 15px;
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
            background: white;
            border-radius: 10px;
            overflow: hidden;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }
        .product:hover {
            transform: scale(1.03);
            box-shadow: 0 5px 15px rgba(0,0,0,0.15);
        }
        .product-badge {
            position: absolute;
            top: 10px;
            left: 10px;
            color: white;
            padding: 3px 8px;
            border-radius: 3px;
            font-size: 0.8rem;
            font-weight: bold;
            z-index: 1;
        }
        .featured-badge {
            background: #d81b60;
        }
        .new-badge {
            background: #4caf50;
        }
        .product img {
            width: 100%;
            height: 180px;
            object-fit: cover;
            loading: lazy;
        }
        .product-info {
            padding: 15px;
        }
        .product-name {
            font-weight: 600;
            margin-bottom: 5px;
            font-size: 1rem;
            height: 45px;
            overflow: hidden;
        }
        .product-price {
            font-weight: bold;
            color: #d81b60;
            font-size: 1.2rem;
            margin: 8px 0;
        }
        .product-rating {
            color: #f1c40f;
            margin: 5px 0;
            font-size: 0.9rem;
        }
        .add-to-cart {
            width: 100%;
            background: #d81b60;
            color: white;
            border: none;
            padding: 10px;
            border-radius: 5px;
            cursor: pointer;
            font-weight: 600;
            transition: all 0.3s;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
            position: absolute;
            top: 180px;
            left: 0;
            opacity: 0;
            transform: translateY(20px);
            z-index: 2;
        }
        .product:hover .add-to-cart {
            opacity: 1;
            transform: translateY(0);
        }
        .add-to-cart:hover {
            background: #ad1457;
        }
        /* Model Section */
        .model-section {
            display: flex;
            justify-content: space-between;
            margin: 40px 0;
            width: 100%;
            flex-wrap: nowrap;
            padding: 0 20px;
            gap: 20px;
            box-sizing: border-box;
        }
        .model-item {
            position: relative;
            text-align: center;
            width: 50%;
            max-width: none;
            border-radius: 10px;
            overflow: hidden;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }
        .model-item img {
            width: 100%;
            height: 280px;
            object-fit: cover;
            display: block;
            cursor: pointer;
            transition: transform 0.5s;
            loading: lazy;
        }
        .model-item:hover img {
            transform: scale(1.05);
        }
        .model-btn {
            position: absolute;
            bottom: 20px;
            left: 50%;
            transform: translateX(-50%);
            background: rgba(0, 0, 0, 0.7);
            color: white;
            border: none;
            padding: 10px 25px;
            border-radius: 30px;
            font-size: 1.1rem;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s;
            width: 80%;
            max-width: 250px;
            text-align: center;
            backdrop-filter: blur(2px);
        }
        .model-btn:hover {
            background: rgba(0, 0, 0, 0.9);
            transform: translateX(-50%) scale(1.05);
        }
        /* Carrito de compras */
        .cart-modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.5);
            z-index: 2000;
            justify-content: flex-end;
        }
        .cart-content {
            background: white;
            width: 100%;
            max-width: 450px;
            height: 100%;
            padding: 20px;
            overflow-y: auto;
            transform: translateX(100%);
            transition: transform 0.4s ease;
            position: relative;
        }
        .cart-content.active {
            transform: translateX(0);
        }
        .cart-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding-bottom: 15px;
            border-bottom: 1px solid #e0e0e0;
            margin-bottom: 20px;
        }
        .close-cart {
            background: none;
            border: none;
            font-size: 1.5rem;
            cursor: pointer;
            color: #333;
        }
        .cart-items {
            margin-bottom: 20px;
        }
        .cart-item {
            display: flex;
            gap: 15px;
            padding: 15px 0;
            border-bottom: 1px solid #e0e0e0;
        }
        .cart-item-img {
            width: 80px;
            height: 80px;
            object-fit: cover;
            border-radius: 5px;
            loading: lazy;
        }
        .cart-item-details {
            flex: 1;
        }
        .cart-item-name {
            font-weight: 600;
            margin-bottom: 5px;
        }
        .cart-item-price {
            color: #d81b60;
            font-weight: bold;
        }
        .cart-item-actions {
            display: flex;
            align-items: center;
            gap: 10px;
            margin-top: 8px;
        }
        .quantity-btn {
            width: 30px;
            height: 30px;
            border-radius: 50%;
            background: #e0e0e0;
            border: none;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        .remove-item {
            color: #e74c3c;
            background: none;
            border: none;
            cursor: pointer;
            margin-left: auto;
        }
        .cart-total {
            font-size: 1.2rem;
            font-weight: bold;
            text-align: right;
            margin: 20px 0;
        }
        .checkout-btn {
            width: 100%;
            background: #4caf50;
            color: white;
            border: none;
            padding: 15px;
            border-radius: 5px;
            font-weight: bold;
            cursor: pointer;
            transition: background 0.3s;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
        }
        .checkout-btn:hover {
            background: #388e3c;
        }
        .empty-cart {
            text-align: center;
            padding: 30px 0;
            color: #777;
        }
        /* Modal de producto */
        .product-modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.5);
            z-index: 3000;
            justify-content: center;
            align-items: center;
        }
        .modal-content {
            background: #fff;
            padding: 15px;
            border-radius: 10px;
            max-width: 500px;
            width: 90%;
            text-align: center;
            position: relative;
            box-shadow: 0 5px 30px rgba(0,0,0,0.3);
            max-height: 95vh;
            overflow-y: auto;
        }
        .modal-content img {
            width: 100%;
            max-height: 200px;
            object-fit: contain;
            border-radius: 5px;
            margin-bottom: 10px;
            loading: lazy;
        }
        .modal-content h3 {
            margin: 0 0 8px;
            font-size: 1.3em;
        }
        .modal-content .description {
            margin: 10px 0;
            font-size: 0.9em;
            color: #555;
        }
        .modal-content .rating {
            margin: 10px 0;
            color: #f1c40f;
            font-size: 1em;
        }
        .modal-content .price {
            font-weight: bold;
            margin: 10px 0;
            font-size: 1.2em;
            color: #d81b60;
        }
        .modal-content .color-palette {
            display: flex;
            gap: 10px;
            justify-content: center;
            flex-wrap: wrap;
            margin: 15px 0;
        }
        .modal-content .color-circle {
            width: 35px;
            height: 35px;
            border-radius: 50%;
            border: 1px solid #ddd;
            cursor: pointer;
            transition: transform 0.2s;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }
        .modal-content .color-circle.selected {
            transform: scale(1.2);
            border: 2px solid #d81b60;
        }
        .modal-content .quantity {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
            margin: 15px 0;
        }
        .modal-content .quantity-btn {
            background: #d81b60;
            color: #fff;
            border: none;
            width: 30px;
            height: 30px;
            border-radius: 50%;
            cursor: pointer;
            font-size: 1em;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        .modal-content .quantity-btn:hover {
            background: #ad1457;
        }
        .modal-content .quantity-input {
            width: 50px;
            height: 35px;
            text-align: center;
            border: 1px solid #ddd;
            border-radius: 5px;
            font-size: 1em;
        }
        .modal-content .close-btn {
            position: absolute;
            top: 10px;
            right: 10px;
            font-size: 1.3em;
            cursor: pointer;
            color: #333;
            background: none;
            border: none;
        }
        .modal-content .btn-add-cart {
            background: #d81b60;
            color: #fff;
            border: none;
            padding: 10px;
            border-radius: 5px;
            cursor: pointer;
            width: 100%;
            margin-top: 10px;
            font-size: 1em;
            font-weight: 600;
            transition: background 0.3s;
        }
        .modal-content .btn-add-cart:hover {
            background: #ad1457;
        }
        /* View All and Category Modals */
        .category-modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.5);
            z-index: 2500;
            justify-content: center;
            align-items: center;
            overflow-y: auto;
        }
        .category-modal-content {
            background: #fff;
            padding: 25px;
            border-radius: 10px;
            max-width: 90%;
            width: 90%;
            max-height: 90vh;
            overflow-y: auto;
            position: relative;
            box-sizing: border-box;
            box-shadow: 0 5px 30px rgba(0,0,0,0.3);
        }
        .category-modal-content h2 {
            margin: 0 0 20px;
            font-size: 1.8em;
            text-align: center;
            color: #d81b60;
            padding-bottom: 10px;
            border-bottom: 2px solid #e0e0e0;
        }
        .search-container {
            margin: 20px 0;
            text-align: center;
        }
        .search-input {
            width: 80%;
            max-width: 500px;
            padding: 12px;
            border: 1px solid #e0e0e0;
            border-radius: 30px;
            font-size: 1em;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }
        .search-input:focus {
            outline: none;
            border-color: #d81b60;
        }
        .view-all-products, .clips-damas-products, .clips-ninas-products {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
            gap: 25px;
            padding: 15px;
        }
        .view-all-products .product, .clips-damas-products .product, .clips-ninas-products .product {
            width: 100%;
            min-width: unset;
        }
        .category-modal-content .close-btn {
            position: absolute;
            top: 15px;
            right: 15px;
            font-size: 1.5em;
            cursor: pointer;
            color: #333;
            background: none;
            border: none;
        }
        /* Responsive */
        @media (max-width: 768px) {
            .header {
                flex-wrap: wrap;
            }
            .header nav ul {
                width: 100%;
                justify-content: center;
                margin-top: 10px;
            }
            .header .logo img {
                height: 50px;
            }
            .product {
                width: 160px;
                min-width: 160px;
            }
            .model-section {
                flex-direction: column;
                gap: 15px;
            }
            .model-item {
                width: 100%;
            }
            .model-item img {
                height: 220px;
            }
            .cart-content {
                max-width: 100%;
            }
            .modal-content {
                padding: 10px;
            }
            .modal-content img {
                max-height: 180px;
                margin-bottom: 8px;
            }
            .modal-content h3 {
                font-size: 1.2em;
                margin-bottom: 6px;
            }
            .modal-content .description {
                margin: 8px 0;
                font-size: 0.85em;
            }
            .modal-content .rating {
                margin: 8px 0;
                font-size: 0.9em;
            }
            .modal-content .price {
                margin: 8px 0;
                font-size: 1.1em;
            }
            .modal-content .color-palette {
                margin: 10px 0;
                gap: 8px;
            }
            .modal-content .color-circle {
                width: 30px;
                height: 30px;
            }
            .modal-content .quantity {
                margin: 10px 0;
                gap: 8px;
            }
            .modal-content .quantity-btn {
                width: 28px;
                height: 28px;
                font-size: 0.9em;
            }
            .modal-content .quantity-input {
                width: 45px;
                height: 32px;
                font-size: 0.9em;
            }
            .modal-content .btn-add-cart {
                margin-top: 8px;
                padding: 8px;
                font-size: 0.9em;
            }
            .modal-content .close-btn {
                top: 8px;
                right: 8px;
                font-size: 1.2em;
            }
        }
        @media (max-width: 480px) {
            .header nav ul {
                gap: 10px;
                font-size: 0.9rem;
            }
            .carousel .banner-text {
                font-size: 1.3em;
                padding: 8px 15px;
            }
            .product {
                width: 140px;
                min-width: 140px;
            }
            .product img {
                height: 150px;
            }
            .add-to-cart {
                top: 150px;
            }
            .section-title {
                font-size: 1.5rem;
            }
            .view-all-products, .clips-damas-products, .clips-ninas-products {
                grid-template-columns: 1fr;
            }
            .modal-content {
                padding: 8px;
            }
            .modal-content img {
                max-height: 160px;
                margin-bottom: 6px;
            }
            .modal-content h3 {
                font-size: 1.1em;
                margin-bottom: 5px;
            }
            .modal-content .description {
                margin: 6px 0;
                font-size: 0.8em;
            }
            .modal-content .rating {
                margin: 6px 0;
                font-size: 0.85em;
            }
            .modal-content .price {
                margin: 6px 0;
                font-size: 1em;
            }
            .modal-content .color-palette {
                margin: 8px 0;
                gap: 6px;
            }
            .modal-content .color-circle {
                width: 28px;
                height: 28px;
            }
            .modal-content .quantity {
                margin: 8px 0;
                gap: 6px;
            }
            .modal-content .quantity-btn {
                width: 26px;
                height: 26px;
                font-size: 0.85em;
            }
            .modal-content .quantity-input {
                width: 40px;
                height: 30px;
                font-size: 0.85em;
            }
            .modal-content .btn-add-cart {
                margin-top: 6px;
                padding: 7px;
                font-size: 0.85em;
            }
            .modal-content .close-btn {
                top: 6px;
                right: 6px;
                font-size: 1.1em;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- Header -->
        <header class="header">
            <div class="logo">
                <img src="https://lh3.googleusercontent.com/gps-cs/AIky0YXTTJyLqUwcNn1yduyV6i82lmL4ukvEZp-ePVd_P_Wa_y1VGwXNJOPpVxro2IxUZ55xE4oEndno5MItmJf7wjkFn0RYFCLtB4bOG2AHYHrupD1pkX8cf3jOUBHNUJOFEYOrwzTGEMSJj6j8=w1000-h1000-p-k-no" alt="TodoModa Logo" loading="lazy">
            </div>
            <nav>
                <ul>
                    <li><a href="#" aria-label="Ir a la página de inicio"><i class="fas fa-home"></i> Inicio</a></li>
                    <li><a href="#" aria-label="Ver productos para mujer"><i class="fas fa-tshirt"></i> Mujer</a></li>
                    <li><a href="#" aria-label="Ver productos para niñas"><i class="fas fa-child"></i> Niñas</a></li>
                    <li><a href="#" aria-label="Ver ofertas"><i class="fas fa-percent"></i> Ofertas</a></li>
                    <li><a href="#" aria-label="Contacto"><i class="fas fa-phone"></i> Contacto</a></li>
                </ul>
            </nav>
            <div class="header-icons">
                <div class="search-icon">
                    <i class="fas fa-search" aria-label="Buscar productos"></i>
                </div>
                <div class="user-icon">
                    <i class="fas fa-user" aria-label="Perfil de usuario"></i>
                </div>
                <div class="cart-icon" id="cartIcon" role="button" aria-label="Abrir carrito de compras">
                    <i class="fas fa-shopping-cart"></i>
                    <span class="cart-count">0</span>
                </div>
            </div>
        </header>

        <!-- Carousel -->
 <div class="carousel">
            <div class="slides">
                <div class="slide-container">
                    <img src="https://pe.todomoda.com/media/wysiwyg/TM_DISNEY_STITCH_-_BANNERS_Desk_new_1.jpg" alt="Banner 1" loading="lazy">
                </div>
                <div class="slide-container">
                    <img src="https://lh3.googleusercontent.com/gps-cs/AIky0YUd2bofobsLtUl3qONXRSiTNou1a9W74yTaVYEr6h64PAuOOqQ-g_w6Ifs8arhOVjWboOrUFEcEDZlmtSBZkgS1YjEnSIw1f3w4IZRdMBwxibVChvNz2c93C78bOxNsx68MuBmN-4iYNCg=w2000-h2000-p-k-no" alt="Banner 2" loading="lazy">
                </div>
            </div>
            <div class="banner-text" id="viewAllBtn" role="button" aria-label="Ver todos los productos">VER TODO</div>
            <div class="dots">
                <span class="active" role="button" aria-label="Ir a la diapositiva 1"></span>
                <span role="button" aria-label="Ir a la diapositiva 2"></span>
            </div>
            <div class="carousel-controls">
                <button class="prev-slide" aria-label="Diapositiva anterior"><i class="fas fa-chevron-left"></i></button>
                <button class="next-slide" aria-label="Diapositiva siguiente"><i class="fas fa-chevron-right"></i></button>
            </div>
        </div>

        <!-- Productos destacados -->
 <h2 class="section-title">Productos Destacados</h2>
        <div class="products" id="featuredProducts">
            <!-- Los productos se insertarán dinámicamente aquí -->
        </div>

        <!-- Model Section -->
<div class="model-section">
            <div class="model-item">
                <img src="https://lh3.googleusercontent.com/gps-cs/AIky0YUGuPXaSC1mPGUKkOYa5z7JyvELvbIy0B4-WtB3tMHIKm2D6Sbg1cTWwU0MsxRJR_5lKb5t1MnVOStZk-tNPdUudQ6-h7M7ueR4l8N5IgmuOrhlNRMi0B_uohBDRomdzQUIHP7y244Zc150=w1024-h1024-p-k-no" alt="Clips Damas" loading="lazy">
                <button class="model-btn" id="clipsDamasBtn" aria-label="Ver Clips Damas">CLIPS DAMAS</button>
            </div>
            <div class="model-item">
                <img src="https://lh3.googleusercontent.com/gps-cs/AIky0YUDER3L7ISerfG6uiIU8ISdgKkibO-SXwGGNL1azb_TJ0qYIN3T7LsJyU-qc9-kQtucnOkLr5rPYtWt0fW0UL8-7RDD46bg_0JnGLkD8RSfQvGydDvq6L_ZLBoj4hnIhwHB3CEx1fPtJ58O=w1024-h1024-p-k-no" alt="Clips Niñas" loading="lazy">
                <button class="model-btn" id="clipsNinasBtn" aria-label="Ver Clips Niñas">CLIPS NIÑAS</button>
            </div>
        </div>

        <!-- Nuevos productos -->
 <h2 class="section-title">Nuevos Productos</h2>
        <div class="products" id="newProducts">
            <!-- Los productos se insertarán dinámicamente aquí -->
        </div>
    </div>
    
    <!-- Carrito de compras -->
<div class="cart-modal" id="cartModal">
        <div class="cart-content" id="cartContent">
            <div class="cart-header">
                <h2>Tu Carrito</h2>
                <button class="close-cart" id="closeCart" aria-label="Cerrar carrito">
                    <i class="fas fa-times"></i>
                </button>
            </div>
            <div class="cart-items" id="cartItems">
                <div class="empty-cart">
                    <i class="fas fa-shopping-cart fa-3x"></i>
                    <p>Tu carrito está vacío</p>
                </div>
            </div>
            <div class="cart-total" id="cartTotal">
                Total: S/ 0.00
            </div>
            <button class="checkout-btn" id="checkoutBtn" aria-label="Realizar pedido">
                <i class="fas fa-check"></i> Realizar Pedido
            </button>
        </div>
    </div>
    
    <!-- Modal de producto -->
 <div class="product-modal" id="productModal">
        <div class="modal-content">
            <button class="close-btn" aria-label="Cerrar modal de producto">×</button>
            <img id="modalImage" alt="Product Image" src="" loading="lazy">
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
            <button class="btn-add-cart" id="btnAddToCart" aria-label="Agregar al carrito">Agregar al carrito</button>
        </div>
    </div>
    
    <!-- View All Products Modal -->
 <div class="category-modal" id="viewAllModal">
        <div class="category-modal-content">
            <button class="close-btn" aria-label="Cerrar modal de todos los productos">×</button>
            <h2>Todos los Productos</h2>
            <div class="search-container">
                <input type="text" class="search-input" id="productSearch" placeholder="Buscar productos..." aria-label="Buscar productos">
            </div>
            <div class="view-all-products" id="viewAllProducts"></div>
        </div>
    </div>
    
    <!-- Clips Damas Modal -->
 <div class="category-modal" id="clipsDamasModal">
        <div class="category-modal-content">
            <button class="close-btn" aria-label="Cerrar modal de Clips Damas">×</button>
            <h2>CLIPS DAMAS</h2>
            <div class="search-container">
                <input type="text" class="search-input" id="clipsDamasSearch" placeholder="Buscar en Clips Damas..." aria-label="Buscar en Clips Damas">
            </div>
            <div class="clips-damas-products" id="clipsDamasProducts"></div>
        </div>
    </div>
    
    <!-- Clips Niñas Modal -->
 <div class="category-modal" id="clipsNinasModal">
        <div class="category-modal-content">
            <button class="close-btn" aria-label="Cerrar modal de Clips Niñas">×</button>
            <h2>CLIPS NIÑAS</h2>
            <div class="search-container">
                <input type="text" class="search-input" id="clipsNinasSearch" placeholder="Buscar en Clips Niñas..." aria-label="Buscar en Clips Niñas">
            </div>
            <div class="clips-ninas-products" id="clipsNinasProducts"></div>
        </div>
    </div>
    
 <script>
        // Datos de productos
        const productsData = [
            {
                id: 1,
                name: "Maxilazos - 5 Colores",
                price: 7.00,
                image: "https://lh3.googleusercontent.com/gps-cs/AIky0YXdnjCFtJm5EhEvClhpsqjsYwwH2Xdqql3H45tWmgLdhiRX--KLwloCAl85SxTImNaOYYbS1MOrlGYrDwH31YoIyFBBn7KapQIKbAHVfoyNmbRBjjgmF0_SefXWn6udgSSaO19kdNtmnQBd=w2000-h2000-p-k-no",
                rating: "⭐⭐⭐⭐☆ (4.2)",
                description: "Maxilazos coloridos, perfectos para cualquier peinado.",
                colors: [
                    {color: "#ffeb3b", title: "Amarillo"},
                    {color: "#d32f2f", title: "Rojo"},
                    {color: "#e1bee7", title: "Lila"},
                    {color: "#145a32", title: "Verde"},
                    {color: "#d6eaf8", title: "Celeste"}
                ],
                featured: true,
                category: "damas"
            },
            {
                id: 2,
                name: "Mini Gancho Corazón",
                price: 2.50,
                image: "https://lh3.googleusercontent.com/gps-cs/AIky0YUd2bofobsLtUl3qONXRSiTNou1a9W74yTaVYEr6h64PAuOOqQ-g_w6Ifs8arhOVjWboOrUFEcEDZlmtSBZkgS1YjEnSIw1f3w4IZRdMBwxibVChvNz2c93C78bOxNsx68MuBmN-4iYNCg=w2000-h2000-p-k-no",
                rating: "⭐⭐⭐☆☆ (3.2)",
                description: "Ganchos en forma de corazón, ideales para looks delicados.",
                colors: [
                    {color: "#17202a", title: "Negro"},
                    {color: "#fff9c4", title: "Crema"},
                    {color: "#fdebd0", title: "Piel"},
                    {color: "#fdfefe", title: "Crema"}
                ],
                featured: true,
                category: "damas"
            },
            {
                id: 3,
                name: "Ganchos Navideños",
                price: 4.00,
                image: "https://lh3.googleusercontent.com/gps-cs/AIky0YV8A_P0YjCC6AIfC2B6HFvCKobK0UJZjVWMnzr6lfYPVXUk0gsszvJXojCK_ycIVH0cOD1-Qw3ICj1Bi9eLIf2TH0ZFaL14TuisJOWESznCPwqs2AAn_lgVOo2yGLhrKuG1yjgsGrWPIZ0k=w2000-h2000-p-k-no",
                rating: "⭐⭐⭐⭐⭐ (5.0)",
                description: "Ganchos temáticos navideños para un estilo festivo.",
                colors: [
                    {color: "#FFFFFF", title: "Blanco"},
                    {color: "#FF0000", title: "Rojo"},
                    {color: "#008000", title: "Verde"}
                ],
                featured: true,
                category: "damas"
            },
            {
                id: 4,
                name: "Gancho Hawaiano",
                price: 5.00,
                image: "https://lh3.googleusercontent.com/gps-cs/AIky0YVaD4OrbInMGPZXKiKtKplaYEn2Ck-9KCl8p9FJbJIXPMWFCDw9Dd5lrbO-8FfXeJZKvIEr-K5UpFwrCnofwtR30imdZTojz2gxrHqZLSM3qody1gDhWdXAm_C4le7hQ4zKL3imga1TIh_j=w2000-h2000-p-k-no",
                rating: "⭐⭐⭐⭐☆ (4.0)",
                description: "Ganchos hawaianos vibrantes para un look tropical.",
                colors: [
                    {color: "#FFD700", title: "Amarillo"}
                ],
                featured: true,
                category: "damas"
            },
            {
                id: 5,
                name: "Ganchos Acrílicos Color Celeste",
                price: 5.00,
                image: "https://lh3.googleusercontent.com/gps-cs/AIky0YXULCa-2ZSbLgwDDlphVpkyxIs_jH2pp8AIHp25rY65c3VTGPdLnesGcrtuCiDtLbovSHvwiSUpzfWiwyle1UmqeO6d0OEvhBLqp_6k4YBo2QzMGd9aduXbKMXqGVHIB0FKSWvBYE1FNgj_=w2000-h2000-p-k-no",
                rating: "⭐⭐⭐⭐☆ (4.0)",
                description: "Ganchos acrílicos elegantes en tonos celestes.",
                colors: [
                    {color: "#5dade2", title: "Celeste"},
                    {color: "#ebf5fb", title: "Agua"},
                    {color: "#FFFFFF", title: "Blanco"}
                ],
                new: true,
                category: "damas"
            },
            {
                id: 6,
                name: "Ganchos",
                price: 4.50,
                image: "https://lh3.googleusercontent.com/gps-cs/AIky0YUepENF6loS0sqfXxEEZlTcAEQ7R-6iS6rmphnT9YjPc9whL2WIk8tCzVNnHDeaj6AaV3e6-k4yeUx9j6nSHq-l2Tc_t0dGMQLhBQrbdREDnxR65_tbipCAL3NCKmRQYWk5geU5V_jn3EiW=w2000-h2000-p-k-no",
                rating: "⭐⭐⭐☆☆ (3.1)",
                description: "Ganchos clásicos para un estilo minimalista.",
                colors: [
                    {color: "#8d6e63", title: "Marrón"},
                    {color: "#fef9e7", title: "Crema"}
                ],
                new: true,
                category: "damas"
            },
            {
                id: 7,
                name: "Ganchos Torna Sol en forma de Flor",
                price: 6.00,
                image: "https://lh3.googleusercontent.com/gps-cs/AIky0YX2NRiy9kc9B9F5EY9kAoTjy699I8L7qzIaAFyN6ktzntZDbknG5_v1B6_JgD_hJDZQ7pAonmz2ynxpJqX4tYXVpt2EJISwaxV7Vd5er2HXevBcfzH_2KoEuxffPMG6wVLrMxkXZaJcUGxc=w2000-h2000-p-k-no",
                rating: "⭐⭐⭐⭐☆ (4.1)",
                description: "Ganchos en forma de flor con diseño inspirado en el sol.",
                colors: [],
                new: true,
                category: "damas"
            },
            {
                id: 8,
                name: "Ganchos Kawai en forma de Flor",
                price: 4.50,
                image: "https://lh3.googleusercontent.com/gps-cs/AIky0YXzdeSiF8Ekcd_sbWEkePfXIFlDCt8BeIvwjgW0_jHy1u9d3KWkRPGKY0IPp8ADAmGFn46hFm8U5vXqhoZ738QBNnwuwb-UXng4k1wKXRwyarfw7ST9PYntIH_SA_XEF0lDF6STVaLz16z2=w2000-h2000-p-k-no",
                rating: "⭐⭐⭐☆☆ (3.5)",
                description: "Ganchos kawai con diseño floral, ideales para niños.",
                colors: [
                    {color: "#FFFF66", title: "Amarillo"},
                    {color: "#CCFF00", title: "Verde"},
                    {color: "#FF8C00", title: "Anaranjado"}
                ],
                new: true,
                category: "ninas"
            },
            {
                id: 9,
                name: "Ganchos de Flores",
                price: 5.00,
                image: "https://lh3.googleusercontent.com/gps-cs/AIky0YUem5vYUL5I1PM57jknLifOO7yf5kSVMtMghU4lP6w0ZMUkV2L9UYoqFLTR_8PcGATvSRKyf0IVg5IYHBQzc5_aND9V8BvtQS47MAT--YXhLlrk645yFo2vaWRADuVRrnbiL5rs4ubhXvU=w2000-h2000-p-k-no",
                rating: "⭐⭐⭐⭐☆ (4.0)",
                description: "Ganchos florales en tonos cálidos para un look vibrante.",
                colors: [
                    {color: "#FFB347", title: "Melón"},
                    {color: "#FFD700", title: "Amarillo"}
                ],
                category: "damas"
            },
            {
                id: 14,
                name: "Par de mini ganchitos en forma de flor",
                price: 3.00,
                image: "https://lh3.googleusercontent.com/gps-cs/AIky0YVcDqGO_EKNry0Eb-BkdsNH0V0lOhwW7AM5WEqz8IiNlbpTs2U3Io9_kt4yCGgt5haYI5RgwRDHv-LMBqc5bvmX245QMyriwIoyJyniPQH9cJJ9iCC2fC8hY06M9BU9nFd6NhCLGVGCC34N=w2000-h2000-p-k-no",
                rating: "⭐⭐⭐⭐☆ (4.0)",
                description: "Mini ganchitos florales para destacar tu peinado.",
                colors: [],
                category: "ninas"
            },
            {
                id: 15,
                name: "Mini ganchitos en forma de mariposa",
                price: 2.00,
                image: "https://lh3.googleusercontent.com/gps-cs/AIky0YW1eFtqiwT_PM-xOZnd2iVogh-XQVJclLEtgsh0i5wUGm9NvOCot9LJLfDmZE58abznArTin0EgjEMw3HuKeK9_9hoODK0kla3nM-GYGSvA8_xXCBmu_qiSuoHzgpSaO_2EtqXLAjnCs34l=w2000-h2000-p-k-no",
                rating: "⭐⭐★☆☆ (3.5)",
                description: "Ganchitos en forma de mariposa, perfectos para peinados infantiles.",
                colors: [],
                category: "ninas"
            },
            {
                id: 16,
                name: "Mini ganchitos",
                price: 1.50,
                image: "https://lh3.googleusercontent.com/gps-cs/AIky0YUgnWieVRURnUHds0U4E5FROmRmvztpc0ynONqB5wFO-tvCmbrBn0-E971IAl2YG7r7cobC9Hx-g0AbDpTP71ukEEb6n20lHQz-aPBoI5xDWtVwABfSJFIbqdRT6_YJzOT7x8uhaX-KBSLE=w2000-h2000-p-k-no",
                rating: "⭐⭐⭐☆☆ (3.3)",
                description: "Mini ganchitos versátiles para cualquier ocasión.",
                colors: [],
                category: "ninas"
            },
            {
                id: 17,
                name: "Ligas colores pasteles y fuertes",
                price: 1.00,
                image: "https://lh3.googleusercontent.com/gps-cs/AIky0YVwhLWhfaBVh3ChmdRjktxd6WCi7W6fTmz2_7TvWPHTT_-3tX1zci-DGspLNMmn3SpAYgh9RN5G_lHRBehTbWzF16lZ9CNiBbjgj5-EVSXMU3aVjCsYaPQ5Maahznx9Fi79zzSnwLxM_nkC=w2000-h2000-p-k-no",
                rating: "⭐⭐⭐⭐☆ (4.0)",
                description: "Ligas en colores pasteles y fuertes, ideales para cualquier estilo.",
                colors: [
                    {color: "#FFC0CB", title: "Rosa Pastel"},
                    {color: "#FFD700", title: "Amarillo"},
                    {color: "#00BFFF", title: "Azul"},
                    {color: "#FF4500", title: "Naranja"},
                    {color: "#008000", title: "Verde"}
                ],
                new: true,
                category: "ninas"
            },
            {
                id: 18,
                name: "Colets negros",
                price: 1.00,
                image: "https://lh3.googleusercontent.com/gps-cs/AIky0YWE3Z0a1qVkSdmBI9RQzayKeT8bgvXn5RTJNXmMJjHG9uzg5VUrwt4-PKEq6AdcYPITi3LkJvKtdxDXq6PucsAOpzZGm2J8QGEYCR4Ff59f3YXXaKQ_Ww8lgm4vOYlRuyCNXxPuyWPFWf23=w2000-h2000-p-k-no",
                rating: "⭐⭐★☆☆ (3.3)",
                description: "Colets negros clásicos y resistentes.",
                colors: [
                    {color: "#000000", title: "Negro"}
                ],
                new: true,
                category: "ninas"
            },
            {
                id: 19,
                name: "Colets colores pasteles",
                price: 1.00,
                image: "https://lh3.googleusercontent.com/gps-cs/AIky0YVVXgYaHEulEuraO7tX6LShXlnoogs6cvwc7jryv8vOVwEt2wCEPWyj0ihUEHTjGMKv0HpL3uglAD96vZsANfdnMrLB4hRI1quw3OaPX-ewOFjUY9eF2ggyG4sMZLcBfJ8amsKoKsAgOXPG=w2000-h2000-p-k-no",
                rating: "⭐⭐★☆☆ (3.4)",
                description: "Colets en tonos pasteles para un look suave y elegante.",
                colors: [
                    {color: "#FFB6C1", title: "Rosa Pastel"},
                    {color: "#87CEFA", title: "Azul Pastel"},
                    {color: "#98FB98", title: "Verde Pastel"}
                ],
                new: true,
                category: "ninas"
            }
        ];

        // Generar productos en la página
        function generateProducts(products, containerId) {
            const container = document.getElementById(containerId);
            container.innerHTML = '';
            
            products.forEach(product => {
                const productElement = document.createElement('div');
                productElement.className = 'product';
                productElement.setAttribute('data-id', product.id);
                productElement.setAttribute('data-colors', JSON.stringify(product.colors));
                productElement.setAttribute('data-rating', product.rating);
                productElement.setAttribute('data-description', product.description);
                
                let badge = '';
                if (product.featured) {
                    badge = '<span class="product-badge featured-badge">Destacado</span>';
                } else if (product.new) {
                    badge = '<span class="product-badge new-badge">Nuevo</span>';
                }
                
                productElement.innerHTML = `
                    ${badge}
                    <img src="${product.image}" alt="${product.name}" class="product-img" loading="lazy">
                    <div class="product-info">
                        <h3 class="product-name">${product.name}</h3>
                        <div class="product-rating">${product.rating}</div>
                        <p class="product-price">S/ ${product.price.toFixed(2)}</p>
                        <button class="add-to-cart" aria-label="Agregar ${product.name} al carrito">
                            <i class="fas fa-shopping-cart"></i> Agregar al carrito
                        </button>
                    </div>
                `;
                
                container.appendChild(productElement);
            });
            
            // Asignar eventos a los productos
            document.querySelectorAll(`#${containerId} .product`).forEach(product => {
                product.addEventListener('click', (e) => {
                    openProductModal(product);
                });
            });
        }
        
        // Inicializar productos
        const featuredProducts = productsData.filter(p => p.featured);
        const newProducts = productsData.filter(p => p.new);
        
        generateProducts(featuredProducts, 'featuredProducts');
        generateProducts(newProducts, 'newProducts');
        
        // Carrito de compras
        let cart = [];
        const cartIcon = document.getElementById('cartIcon');
        const cartModal = document.getElementById('cartModal');
        const cartContent = document.getElementById('cartContent');
        const closeCart = document.getElementById('closeCart');
        const cartItems = document.getElementById('cartItems');
        const cartTotal = document.getElementById('cartTotal');
        const checkoutBtn = document.getElementById('checkoutBtn');
        
        // Cargar carrito desde localStorage
        function loadCart() {
            const savedCart = localStorage.getItem('cart');
            if (savedCart) {
                cart = JSON.parse(savedCart);
                updateCart();
            }
        }
        
        // Guardar carrito en localStorage
        function saveCart() {
            localStorage.setItem('cart', JSON.stringify(cart));
        }
        
        // Abrir carrito
        cartIcon.addEventListener('click', () => {
            cartModal.style.display = 'flex';
            setTimeout(() => {
                cartContent.classList.add('active');
            }, 10);
        });
        
        // Cerrar carrito
        closeCart.addEventListener('click', () => {
            cartContent.classList.remove('active');
            setTimeout(() => {
                cartModal.style.display = 'none';
            }, 300);
        });
        
        // Cerrar al hacer clic fuera del carrito
        cartModal.addEventListener('click', (e) => {
            if (e.target === cartModal) {
                cartContent.classList.remove('active');
                setTimeout(() => {
                    cartModal.style.display = 'none';
                }, 300);
            }
        });
        
        // Añadir producto al carrito
        function addToCart(productElement, quantity, colorTitle) {
            const id = productElement.getAttribute('data-id');
            const product = productsData.find(p => p.id === Number(id));
            
            if (!product) return;
            
            const existingItem = cart.find(item => 
                item.id === Number(id) && item.color === colorTitle
            );
            
            if (existingItem) {
                existingItem.quantity += quantity;
            } else {
                cart.push({
                    id: product.id,
                    name: product.name,
                    price: product.price,
                    image: product.image,
                    quantity: quantity,
                    color: colorTitle
                });
            }
            
            updateCart();
            saveCart();
            showAddedNotification(product.name);
        }
        
        // Mostrar notificación de producto añadido
        function showAddedNotification(productName) {
            const notification = document.createElement('div');
            notification.innerHTML = `
                <div style="position: fixed; bottom: 20px; right: 20px; background: #4caf50; color: white; padding: 15px 20px; border-radius: 5px; display: flex; align-items: center; gap: 10px; z-index: 3000; box-shadow: 0 2px 10px rgba(0,0,0,0.1);" role="alert">
                    <i class="fas fa-check-circle"></i>
                    <span>¡${productName} añadido al carrito!</span>
                </div>
            `;
            document.body.appendChild(notification);
            
            setTimeout(() => {
                notification.remove();
            }, 3000);
        }
        
        // Actualizar carrito
        function updateCart() {
            const cartCount = document.querySelector('.cart-count');
            const totalItems = cart.reduce((total, item) => total + item.quantity, 0);
            cartCount.textContent = totalItems;
            
            if (cart.length === 0) {
                cartItems.innerHTML = `
                    <div class="empty-cart">
                        <i class="fas fa-shopping-cart fa-3x"></i>
                        <p>Tu carrito está vacío</p>
                    </div>
                `;
                cartTotal.textContent = 'Total: S/ 0.00';
                checkoutBtn.style.display = 'none';
                return;
            }
            
            checkoutBtn.style.display = 'block';
            
            cartItems.innerHTML = '';
            let total = 0;
            
            cart.forEach((item, index) => {
                const itemTotal = item.price * item.quantity;
                total += itemTotal;
                
                const cartItemElement = document.createElement('div');
                cartItemElement.classList.add('cart-item');
                cartItemElement.innerHTML = `
                    <img src="${item.image}" alt="${item.name}" class="cart-item-img" loading="lazy">
                    <div class="cart-item-details">
                        <h3 class="cart-item-name">${item.name}</h3>
                        ${item.color ? `<p>Color: ${item.color}</p>` : ''}
                        <p class="cart-item-price">S/ ${item.price.toFixed(2)}</p>
                        <div class="cart-item-actions">
                            <button class="quantity-btn decrease" data-index="${index}" aria-label="Disminuir cantidad">-</button>
                            <span>${item.quantity}</span>
                            <button class="quantity-btn increase" data-index="${index}" aria-label="Aumentar cantidad">+</button>
                            <button class="remove-item" data-index="${index}" aria-label="Eliminar ${item.name} del carrito">
                                <i class="fas fa-trash"></i>
                            </button>
                        </div>
                    </div>
                `;
                
                cartItems.appendChild(cartItemElement);
            });
            
            cartTotal.textContent = `Total: S/ ${total.toFixed(2)}`;
            
            document.querySelectorAll('.decrease').forEach(button => {
                button.addEventListener('click', () => {
                    const index = button.getAttribute('data-index');
                    if (cart[index].quantity > 1) {
                        cart[index].quantity--;
                    } else {
                        cart.splice(index, 1);
                    }
                    updateCart();
                    saveCart();
                });
            });
            
            document.querySelectorAll('.increase').forEach(button => {
                button.addEventListener('click', () => {
                    const index = button.getAttribute('data-index');
                    cart[index].quantity++;
                    updateCart();
                    saveCart();
                });
            });
            
            document.querySelectorAll('.remove-item').forEach(button => {
                button.addEventListener('click', () => {
                    const index = button.getAttribute('data-index');
                    cart.splice(index, 1);
                    updateCart();
                    saveCart();
                });
            });
        }
        
        // Finalizar compra
        checkoutBtn.addEventListener('click', () => {
            if (cart.length === 0) return;
            
            alert(`¡Gracias por tu compra! Total: S/ ${cart.reduce((total, item) => total + (item.price * item.quantity), 0).toFixed(2)}`);
            cart = [];
            updateCart();
            saveCart();
            cartContent.classList.remove('active');
            setTimeout(() => {
                cartModal.style.display = 'none';
            }, 300);
        });
        
        // Modal de producto
        const productModal = document.getElementById('productModal');
        const modalImage = document.getElementById('modalImage');
        const modalTitle = document.getElementById('modalTitle');
        const modalDescription = document.getElementById('modalDescription');
        const modalRating = document.getElementById('modalRating');
        const modalPrice = document.getElementById('modalPrice');
        const modalColors = document.getElementById('modalColors');
        const decreaseQty = document.getElementById('decreaseQty');
        const increaseQty = document.getElementById('increaseQty');
        const quantityInput = document.getElementById('quantityInput');
        const btnAddToCart = document.getElementById('btnAddToCart');
        const modalCloseBtn = document.querySelector('#productModal .close-btn');
        
        let selectedProduct = null;
        let selectedColor = null;
        let selectedColorTitle = null;
        
        function openProductModal(productElement) {
            const id = productElement.getAttribute('data-id');
            const product = productsData.find(p => p.id === Number(id));
            
            if (!product) return;
            
            selectedProduct = product;
            
            modalImage.src = product.image;
            modalTitle.textContent = product.name;
            modalDescription.textContent = product.description;
            modalRating.textContent = product.rating;
            modalPrice.textContent = `S/ ${product.price.toFixed(2)}`;
            
            modalColors.innerHTML = '';
            if (product.colors.length > 0) {
                product.colors.forEach(color => {
                    const colorCircle = document.createElement('span');
                    colorCircle.className = 'color-circle';
                    colorCircle.style.backgroundColor = color.color;
                    colorCircle.title = color.title;
                    colorCircle.setAttribute('data-color', color.color);
                    colorCircle.dataset.colorTitle = color.title;
                    colorCircle.setAttribute('role', 'button');
                    colorCircle.setAttribute('aria-label', `Seleccionar color ${color.title}`);
                    
                    colorCircle.addEventListener('click', () => {
                        modalColors.querySelectorAll('.color-circle').forEach(c => c.classList.remove('selected'));
                        colorCircle.classList.add('selected');
                        selectedColor = color.color;
                        selectedColorTitle = color.title;
                    });
                    
                    modalColors.appendChild(colorCircle);
                });
                
                if (product.colors.length > 0) {
                    modalColors.firstChild.click();
                }
            } else {
                modalColors.innerHTML = '<p>No hay colores disponibles</p>';
                selectedColor = null;
                selectedColorTitle = null;
            }
            
            quantityInput.value = '1';
            
            productModal.style.display = 'flex';
        }
        
        // Cerrar modal de producto
        modalCloseBtn.addEventListener('click', () => {
            productModal.style.display = 'none';
        });
        
        productModal.addEventListener('click', (e) => {
            if (e.target === productModal) {
                productModal.style.display = 'none';
            }
        });
        
        document.addEventListener('keydown', (e) => {
            if (e.key === 'Escape' && productModal.style.display === 'flex') {
                productModal.style.display = 'none';
            }
        });
        
        // Controles de cantidad
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
            let value = parseInt(quantityInput.value);
            if (isNaN(value) || value < 1) {
                quantityInput.value = 1;
            }
        });
        
        // Añadir al carrito desde modal
        btnAddToCart.addEventListener('click', () => {
            if (!selectedProduct) return;
            
            const quantity = parseInt(quantityInput.value);
            
            const existingItem = cart.find(item => 
                item.id === selectedProduct.id && 
                item.color === selectedColorTitle
            );
            
            if (existingItem) {
                existingItem.quantity += quantity;
            } else {
                cart.push({
                    id: selectedProduct.id,
                    name: selectedProduct.name,
                    price: selectedProduct.price,
                    image: selectedProduct.image,
                    quantity: quantity,
                    color: selectedColorTitle
                });
            }
            
            updateCart();
            saveCart();
            showAddedNotification(selectedProduct.name);
            productModal.style.display = 'none';
        });
        
        // Modal "Ver Todo"
        const viewAllModal = document.getElementById('viewAllModal');
        const viewAllBtn = document.getElementById('viewAllBtn');
        const viewAllProductsContainer = document.getElementById('viewAllProducts');
        const viewAllCloseBtn = document.querySelector('#viewAllModal .close-btn');
        const productSearch = document.getElementById('productSearch');
        
        viewAllBtn.addEventListener('click', () => {
            generateProducts(productsData, 'viewAllProducts');
            viewAllModal.style.display = 'flex';
        });
        
        viewAllCloseBtn.addEventListener('click', () => {
            viewAllModal.style.display = 'none';
        });
        
        viewAllModal.addEventListener('click', (e) => {
            if (e.target === viewAllModal) {
                viewAllModal.style.display = 'none';
            }
        });
        
        // Búsqueda de productos con debounce
        function debounce(func, wait) {
            let timeout;
            return function executedFunction(...args) {
                const later = () => {
                    clearTimeout(timeout);
                    func(...args);
                };
                clearTimeout(timeout);
                timeout = setTimeout(later, wait);
            };
        }
        
        productSearch.addEventListener('input', debounce(() => {
            const searchTerm = productSearch.value.toLowerCase();
            const filteredProducts = productsData.filter(product => 
                product.name.toLowerCase().includes(searchTerm)
            );
            generateProducts(filteredProducts, 'viewAllProducts');
        }, 300));
        
        // Modal "Clips Damas"
        const clipsDamasModal = document.getElementById('clipsDamasModal');
        const clipsDamasBtn = document.getElementById('clipsDamasBtn');
        const clipsDamasProductsContainer = document.getElementById('clipsDamasProducts');
        const clipsDamasCloseBtn = document.querySelector('#clipsDamasModal .close-btn');
        const clipsDamasSearch = document.getElementById('clipsDamasSearch');
        
        clipsDamasBtn.addEventListener('click', () => {
            const damasProducts = productsData.filter(p => p.category === 'damas' || !p.category);
            generateProducts(damasProducts, 'clipsDamasProducts');
            clipsDamasModal.style.display = 'flex';
        });
        
        clipsDamasCloseBtn.addEventListener('click', () => {
            clipsDamasModal.style.display = 'none';
        });
        
        clipsDamasModal.addEventListener('click', (e) => {
            if (e.target === clipsDamasModal) {
                clipsDamasModal.style.display = 'none';
            }
        });
        
        clipsDamasSearch.addEventListener('input', debounce(() => {
            const searchTerm = clipsDamasSearch.value.toLowerCase();
            const filteredProducts = productsData
                .filter(p => p.category === 'damas' || !p.category)
                .filter(product => product.name.toLowerCase().includes(searchTerm));
            generateProducts(filteredProducts, 'clipsDamasProducts');
        }, 300));
        
        // Modal "Clips Niñas"
        const clipsNinasModal = document.getElementById('clipsNinasModal');
        const clipsNinasBtn = document.getElementById('clipsNinasBtn');
        const clipsNinasProductsContainer = document.getElementById('clipsNinasProducts');
        const clipsNinasCloseBtn = document.querySelector('#clipsNinasModal .close-btn');
        const clipsNinasSearch = document.getElementById('clipsNinasSearch');
        
        clipsNinasBtn.addEventListener('click', () => {
            const ninasProducts = productsData.filter(p => p.category === 'ninas');
            generateProducts(ninasProducts, 'clipsNinasProducts');
            clipsNinasModal.style.display = 'flex';
        });
        
        clipsNinasCloseBtn.addEventListener('click', () => {
            clipsNinasModal.style.display = 'none';
        });
        
        clipsNinasModal.addEventListener('click', (e) => {
            if (e.target === clipsNinasModal) {
                clipsNinasModal.style.display = 'none';
            }
        });
        
        clipsNinasSearch.addEventListener('input', debounce(() => {
            const searchTerm = clipsNinasSearch.value.toLowerCase();
            const filteredProducts = productsData
                .filter(p => p.category === 'ninas')
                .filter(product => product.name.toLowerCase().includes(searchTerm));
            generateProducts(filteredProducts, 'clipsNinasProducts');
        }, 300));
        
        // Carrusel
        const slides = document.querySelector('.slides');
        const dots = document.querySelectorAll('.carousel .dots span');
        const prevSlide = document.querySelector('.prev-slide');
        const nextSlide = document.querySelector('.next-slide');
        let currentIndex = 0;
        let autoSlide;
        
        function startAutoSlide() {
            autoSlide = setInterval(() => {
                currentIndex = (currentIndex + 1) % dots.length;
                slideShow(currentIndex);
            }, 3000);
        }
        
        function stopAutoSlide() {
            clearInterval(autoSlide);
        }
        
        function slideShow(index) {
            slides.style.transform = `translateX(-${index * 100}%)`;
            dots.forEach((dot, i) => {
                dot.classList.toggle('active', i === index);
            });
        }
        
        dots.forEach((dot, i) => {
            dot.addEventListener('click', () => {
                stopAutoSlide();
                currentIndex = i;
                slideShow(currentIndex);
                startAutoSlide();
            });
        });
        
        prevSlide.addEventListener('click', () => {
            stopAutoSlide();
            currentIndex = (currentIndex - 1 + dots.length) % dots.length;
            slideShow(currentIndex);
            startAutoSlide();
        });
        
        nextSlide.addEventListener('click', () => {
            stopAutoSlide();
            currentIndex = (currentIndex + 1) % dots.length;
            slideShow(currentIndex);
            startAutoSlide();
        });
        
        slides.addEventListener('mouseenter', stopAutoSlide);
        slides.addEventListener('mouseleave', startAutoSlide);
        
        // Hacer clicables las imágenes de la sección de modelos
        const modelItems = document.querySelectorAll('.model-item');
        modelItems.forEach(item => {
            const img = item.querySelector('img');
            const btn = item.querySelector('.model-btn');
            img.addEventListener('click', (e) => {
                e.preventDefault();
                btn.click();
            });
        });
        
        // Inicializar
        document.addEventListener('DOMContentLoaded', () => {
            loadCart();
            startAutoSlide();
        });
    </script>
</body>
</html>
```
