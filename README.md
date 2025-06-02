<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>TodoModa - Tienda Online</title>
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
            height: 100px; /* Set logo height */
            width: auto; /* Maintain aspect ratio */
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
            font-size: 1.2em; /* Reduced font size */
            font-weight: bold;
            color: #fff;
            background: rgba(0, 0, 0, 0.5);
            padding: 4px 10px; /* Smaller padding */
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
            flex-wrap: nowrap; /* Prevent wrapping to keep images side by side */
        }
        .model-item {
            position: relative;
            text-align: center;
            width: 50%; /* Each item takes half the container width */
            max-width: none; /* Remove max-width to allow full expansion */
        }
        .model-item img {
            width: 100%;
            height: auto;
            border-radius: 5px;
            display: block;
            cursor: pointer; /* Indicate clickability */
        }
        .model-item .category-btn {
            position: absolute;
            bottom: 10px;
            left: 50%;
            transform: translateX(-50%);
            width: 80%; /* Ensure button fits within image */
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
                font-size: 1em; /* Smaller font for smaller screens */
                padding: 4px 8px;
            }
            .model-item {
                width: 50%; /* Maintain equal width */
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
                grid-template-columns: repeat(auto-fill, minmax(120px, 1fr));
            }
            .search-input {
                width: 95%;
            }
            .category-btn {
                font-size: 0.9em; /* Even smaller font for mobile */
                padding: 3px 6px;
            }
            .model-item {
                width: 50%; /* Maintain equal width */
            }
            .model-item img {
                width: 100%;
            }
        }
    </style>
</head>
<body>     <div class="container">         <!-- Header -->         <div class="header">             <div class="logo">                 <img src="https://lh3.googleusercontent.com/gps-cs/AIky0YXTTJyLqUwcNn1yduyV6i82lmL4ukvEZp-ePVd_P_Wa_y1VGwXNJOPpVxro2IxUZ55xE4oEndno5MItmJf7wjkFn0RYFCLtB4bOG2AHYHrupD1pkX8cf3jOUBHNUJOFEYOrwzTGEMSJj6j8=w1000-h1000-p-k-no" alt="TodoModa Logo">             </div>             <nav>                 <ul>                 </ul>             </nav>             <div class="icons">             </div>         </div>

        <!-- Carousel -->
 <div class="carousel">
            <div class="slides">
                <div class="slide-container">
                    <img src="https://pe.todomoda.com/media/wysiwyg/TM_DISNEY_STITCH_-_BANNERS_Desk_new_1.jpg" alt="Banner 1">
                </div>
                <div class="slide-container">
                    <img src="https://lh3.googleusercontent.com/gps-cs/AIky0YUd2bofobsLtUl3qONXRSiTNou1a9W74yTaVYEr6h64PAuOOqQ-g_w6Ifs8arhOVjWboOrUFEcEDZlmtSBZkgS1YjEnSIw1f3w4IZRdMBwxibVChvNz2c93C78bOxNsx68MuBmN-4iYNCg=w2000-h2000-p-k-no" alt="Banner 2">
                </div>
            </div>
            <div class="banner-text" id="viewAllBtn">VER TODO</div>
            <div class="dots">
                <span class="active"></span>
                <span></span>
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

        <!-- Modal -->
 <div class="modal" id="colorModal" role="dialog" aria-labelledby="modalTitle" aria-hidden="true">
            <div class="modal-content">
                <span class="close-btn" aria-label="Cerrar modal">×</span>
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
                <span class="close-btn" aria-label="Cerrar modal">×</span>
                <h2 id="viewAllModalTitle">Todos los Productos</h2>
                <div class="search-container">
                    <input type="text" class="search-input" id="productSearch" placeholder="Buscar productos..." aria-label="Buscar productos">
                </div>
                <div class="view-all-products" id="viewAllProducts"></div>
            </div>
        </div>

        <!-- Clips Damas Modal -->
 <div class="clips-damas-modal" id="clipsDamasModal" role="dialog" aria-labelledby="clipsDamasModalTitle" aria-hidden="true">
            <div class="clips-damas-modal-content">
                <span class="close-btn" aria-label="Cerrar modal">×</span>
                <h2 id="clipsDamasModalTitle">CLIPS DAMAS</h2>
                <div class="search-container">
                    <input type="text" class="search-input" id="clipsDamasSearch" placeholder="Buscar en Clips Damas..." aria-label="Buscar en Clips Damas">
                </div>
                <div class="clips-damas-products" id="clipsDamasProducts"></div>
            </div>
        </div>

        <!-- Clips Niñas Modal -->
 <div class="clips-ninas-modal" id="clipsNinasModal" role="dialog" aria-labelledby="clipsNinasModalTitle" aria-hidden="true">
            <div class="clips-ninas-modal-content">
                <span class="close-btn" aria-label="Cerrar modal">×</span>
                <h2 id="clipsNinasModalTitle">CLIPS NIÑAS</h2>
                <div class="search-container">
                    <input type="text" class="search-input" id="clipsNinasSearch" placeholder="Buscar en Clips Niñas..." aria-label="Buscar en Clips Niñas">
                </div>
                <div class="clips-ninas-products" id="clipsNinasProducts"></div>
            </div>
        </div>
    </div>

<script>
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

        // Modal functionality
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

        function openProductModal(product) {
            const id = product.getAttribute('data-id');
            const name = product.querySelector('p').textContent;
            const price = product.querySelector('.price').textContent;
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
            modalPrice.textContent = price;
            modalAddCart.setAttribute('data-id', id);
            modalAddCart.setAttribute('data-name', name);
            modalAddCart.setAttribute('data-price', price.replace('S/ ', ''));

            modalColors.innerHTML = colors.map(color => 
                `<span class="color-circle" style="background-color: ${color.color};" title="${color.title}" data-color="${color.color}"></span>`
            ).join('');

            quantityInput.value = 1;
            selectedColor = null;
            modalColors.querySelectorAll('.color-circle').forEach(circle => {
                circle.classList.remove('selected');
                circle.addEventListener('click', () => {
                    modalColors.querySelectorAll('.color-circle').forEach(c => c.classList.remove('selected'));
                    circle.classList.add('selected');
                    selectedColor = circle.getAttribute('data-color');
                });
            });

            modal.style.display = 'flex';
            modal.setAttribute('aria-hidden', 'false');
        }

        // Quantity controls
        decreaseQty.addEventListener('click', () => {
            let qty = parseInt(quantityInput.value);
            if (qty > 1) quantityInput.value = qty - 1;
        });

        increaseQty.addEventListener('click', () => {
            let qty = parseInt(quantityInput.value);
            quantityInput.value = qty + 1;
        });

        quantityInput.addEventListener('input', () => {
            if (quantityInput.value < 1) quantityInput.value = 1;
        });

        // Add to cart (placeholder functionality)
        modalAddCart.addEventListener('click', () => {
            const id = modalAddCart.getAttribute('data-id');
            const name = modalAddCart.getAttribute('data-name');
            const price = modalAddCart.getAttribute('data-price');
            const quantity = quantityInput.value;
            alert(`Añadido al carrito: ${name}, Cantidad: ${quantity}, Color: ${selectedColor || 'Ninguno'}, Precio: S/ ${(price * quantity).toFixed(2)}`);
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

        document.addEventListener('keydown', (e) => {
            if (e.key === 'Escape' && modal.style.display === 'flex') {
                modal.style.display = 'none';
                modal.setAttribute('aria-hidden', 'true');
            }
        });

        // Product event listeners
        function attachProductListeners(products) {
            products.forEach(product => {
                product.addEventListener('click', (e) => {
                    if (e.target.classList.contains('btn-add-cart') || e.target.classList.contains('quantity-btn') || e.target.classList.contains('quantity-input')) return;
                    openProductModal(product);
                });
                product.querySelector('.add-to-cart').addEventListener('click', (e) => {
                    e.stopPropagation();
                    openProductModal(product);
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

        function updateViewAllProducts(searchTerm = '') {
            viewAllProductsContainer.innerHTML = '';
            const filteredProducts = Array.from(allProducts).filter(product => {
                const name = product.querySelector('p').textContent.toLowerCase();
                return name.includes(searchTerm.toLowerCase());
            });

            filteredProducts.forEach(product => {
                const productClone = product.cloneNode(true);
                viewAllProductsContainer.appendChild(productClone);
            });

            attachProductListeners(viewAllProductsContainer.querySelectorAll('.product'));
        }

        viewAllBtn.addEventListener('click', () => {
            productSearch.value = '';
            updateViewAllProducts();
            viewAllModal.style.display = 'flex';
            viewAllModal.setAttribute('aria-hidden', 'false');
            productSearch.focus();
        });

        productSearch.addEventListener('input', () => {
            updateViewAllProducts(productSearch.value);
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

        function updateClipsDamasProducts(searchTerm = '') {
            clipsDamasProductsContainer.innerHTML = '';
            const damasProducts = Array.from(allProducts).filter(product => {
                const id = parseInt(product.getAttribute('data-id'));
                return id >= 1 && id <= 9;
            });
            const filteredProducts = damasProducts.filter(product => {
                const name = product.querySelector('p').textContent.toLowerCase();
                return name.includes(searchTerm.toLowerCase());
            });

            filteredProducts.forEach(product => {
                const productClone = product.cloneNode(true);
                clipsDamasProductsContainer.appendChild(productClone);
            });

            attachProductListeners(clipsDamasProductsContainer.querySelectorAll('.product'));
            clipsDamasProductsContainer.querySelectorAll('.product').forEach(product => {
                product.addEventListener('click', (e) => {
                    if (e.target.classList.contains('btn-add-cart') || e.target.classList.contains('quantity-btn') || e.target.classList.contains('quantity-input')) return;
                    clipsDamasModal.style.display = 'none';
                    clipsDamasModal.setAttribute('aria-hidden', 'true');
                    openProductModal(product);
                });
                product.querySelector('.add-to-cart').addEventListener('click', (e) => {
                    e.stopPropagation();
                    clipsDamasModal.style.display = 'none';
                    clipsDamasModal.setAttribute('aria-hidden', 'true');
                    openProductModal(product);
                });
            });
        }

        clipsDamasBtn.addEventListener('click', () => {
            clipsDamasSearch.value = '';
            updateClipsDamasProducts();
            clipsDamasModal.style.display = 'flex';
            clipsDamasModal.setAttribute('aria-hidden', 'false');
            clipsDamasSearch.focus();
        });

        clipsDamasSearch.addEventListener('input', () => {
            updateClipsDamasProducts(clipsDamasSearch.value);
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

        function updateClipsNinasProducts(searchTerm = '') {
            clipsNinasProductsContainer.innerHTML = '';
            const ninasProducts = Array.from(allProducts).filter(product => {
                const id = parseInt(product.getAttribute('data-id'));
                return id >= 14 && id <= 19;
            });
            const filteredProducts = ninasProducts.filter(product => {
                const name = product.querySelector('p').textContent.toLowerCase();
                return name.includes(searchTerm.toLowerCase());
            });

            filteredProducts.forEach(product => {
                const productClone = product.cloneNode(true);
                clipsNinasProductsContainer.appendChild(productClone);
            });

            attachProductListeners(clipsNinasProductsContainer.querySelectorAll('.product'));
            clipsNinasProductsContainer.querySelectorAll('.product').forEach(product => {
                product.addEventListener('click', (e) => {
                    if (e.target.classList.contains('btn-add-cart') || e.target.classList.contains('quantity-btn') || e.target.classList.contains('quantity-input')) return;
                    clipsNinasModal.style.display = 'none';
                    clipsNinasModal.setAttribute('aria-hidden', 'true');
                    openProductModal(product);
                });
                product.querySelector('.add-to-cart').addEventListener('click', (e) => {
                    e.stopPropagation();
                    clipsNinasModal.style.display = 'none';
                    clipsNinasModal.setAttribute('aria-hidden', 'true');
                    openProductModal(product);
                });
            });
        }

        clipsNinasBtn.addEventListener('click', () => {
            clipsNinasSearch.value = '';
            updateClipsNinasProducts();
            clipsNinasModal.style.display = 'flex';
            clipsNinasModal.setAttribute('aria-hidden', 'false');
            clipsNinasSearch.focus();
        });

        clipsNinasSearch.addEventListener('input', () => {
            updateClipsNinasProducts(clipsNinasSearch.value);
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

        // Make model section images clickable
        const modelItems = document.querySelectorAll('.model-item');
        modelItems.forEach(item => {
            const img = item.querySelector('img');
            const btn = item.querySelector('.category-btn');
            img.addEventListener('click', (e) => {
                e.preventDefault();
                btn.click(); // Trigger the button's click event
            });
        });

        // Close modals on Escape key
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
            }
        });
    </script>
</body>
</html>
