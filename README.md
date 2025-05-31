<html lang="es">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <link href="https://maxcdn.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css" rel="stylesheet" />
    <style>

 html, body {
            height: 100%;
            margin: 0;
            padding: 0;
            background-image: url('');
            background-size: cover;
            background-repeat: no-repeat;
            background-attachment: fixed;
            background-position: center center;
        }
           .header {
    padding: 10px;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 150px; /* ajusta según necesites */
}

.header img {
    background-color: transparent;
    max-width: 150px;
    height: auto;
    display: block;
}


 .carousel {
            width: 100%;
            margin: auto;
            padding: 10px;
            overflow: hidden;
            border-radius: 20px;
        }
        .carousel-inner img {
            background-color: transparent !important;
            width: auto;
            height: auto;
            padding: 10px;
            object-fit: cover;
            border-radius: 20px;
        }
        .carousel-item {
            aspect-ratio: 16 / 9;
            height: auto;
        }
        .categories {
            display: flex;
            overflow-x: auto;
            padding: 20px;
        }
        .category {
            position: relative;
            flex: 0 0 auto;
            width: 120px;
            height: 120px;
            margin-right: 10px;
            border-radius: 10px;
            overflow: hidden;
            cursor: pointer;
            border: 2px solid transparent;
            transition: box-shadow 0.3s ease, border-color 0.3s ease;
        }

 .category.active {
              border: 2px solid #ff5722;
              box-shadow: 0 0 10px 3px #ff5722, 0 0 20px 5px #ff7043;
         }

 .category:hover {
               box-shadow: 0 0 8px 2px #ff5722, 0 0 16px 4px #ff7043;
               border-color: #ff5722;
        }

 .category img {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }
        .category-title {
            position: absolute;
            top: 3px;
            left: 3px;
            background-color: rgba(0, 0, 0, 0.5);
            color: white;
            padding: 2px;
            border-radius: 2px;
            font-size: 12px;
        }
        .products-container {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            padding: 10px;
        }
        .product-item {
            width: 125px;
            margin: 10px;
            background-color: #C0C0C0;
            border-radius: 10px;
            padding: 0px;
            text-align: center;
            position: relative;
            cursor: pointer;
        }
        .product-item img {
            width: 100%;
            height: 120px;
            object-fit: cover;
            border-radius: 10px;
        }
        .product-info h3 {
            position: absolute;
            top: 5px;
            left: 5px;
            font-size: 14px;
            margin: 0;
            color: white;
            background-color: rgba(0, 0, 0, 0.5);
            padding: 2px;
            border-radius: 2px;
        }
        #cart {
            display: none;
            position: fixed;
            top: 0;
            right: 0;
            width: 100%;
            height: 100%;
            background-image: url('https://lh3.googleusercontent.com/gps-cs/AIky0YWZF8wu37kpyKmtSowVsNaeNGpRMtvKeWkCZif90TIR3x-SxoKtOhnsCjpKQy82BoA-1rwQT5Y5PM-iy0Ko_pymybn_Ep_RsCCd3tB7tbdzJuTVLMEHIEJhWNijbZBBri_rwnZ_eAbuC70=w1024-h1536-p-k-no');
            background-size: cover;
            background-repeat: no-repeat;
            background-position: center;
            box-shadow: -5px 0px 15px rgba(0, 0, 0, 0.1);
            z-index: 1000;
            padding: 0px;
            overflow-y: auto;
        }
        .cart h2 {
            font-size: 24px;
            margin-bottom: 20px;
            color: #333;
        }
        .cart-item {
            display: flex;
            flex-direction: column;
            background-color: #f9f9f9;
            margin-bottom: 10px;
            padding: 10px;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
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
        }
        #order-button {
            width: 100%;
            padding: 15px;
            background-color: #ff5722;
            color: white;
            border: none;
            font-size: 18px;
            border-radius: 20px;
            cursor: pointer;
            transition: background-color 0.3s;
        }
        #order-button:hover {
            background-color: #e64a19;
        }
        #cart-button {
            position: fixed;
            top: 20px;
            right: 20px;
            background-color: #ff5722;
            color: white;
            padding: 15px;
            border-radius: 50%;
            cursor: pointer;
            z-index: 2000;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
            font-size: 24px;
        }
        #cart-button:hover {
            background-color: #e64a19;
        }
        #product-modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.7);
            z-index: 3000;
            align-items: center;
            justify-content: center;
        }
        #product-modal > div {
            background: #fff;
            border-radius: 10px;
            max-width: 400px;
            width: 90%;
            padding: 20px;
            position: relative;
            box-sizing: border-box;
        }
        #close-product-modal {
            position: absolute;
            top: 10px;
            right: 15px;
            font-size: 20px;
            background: none;
            border: none;
            cursor: pointer;
        }
        #modal-product-image {
            width: 100%;
            height: auto;
            border-radius: 10px;
            margin-bottom: 15px;
        }
        #modal-quantity-decrease,
        #modal-quantity-increase {
            width: 30px;
            height: 30px;
            cursor: pointer;
        }
        #modal-quantity {
            width: 40px;
            text-align: center;
            pointer-events: none;
        }
        #loading-spinner {
            display: none;
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            z-index: 4000;
            background: rgba(0,0,0,0.5);
            color: white;
            padding: 20px;
            border-radius: 10px;
        }
       /* Móvil (menos de 600px) — mantiene el estilo original o auto */

 /* Tablet (entre 600px y 1023px) */
        @media (min-width: 600px) and (max-width: 1023px) {
    .carousel {
        max-width: 600px; /* ancho máximo para tablet */
        margin: 10px auto;
        padding: 0;
    }
    .carousel-inner img {
        width: 100%;
        height: auto;
        object-fit: cover;
        padding: 0;
        border-radius: 20px;
    }
    .carousel-item {
        height: auto;
        aspect-ratio: 16 / 9;
    }
    }

 /* Escritorio (1024px en adelante) */
     @media (min-width: 1024px) {
    .carousel {
        max-width: 900px; /* ancho máximo para escritorio */
        margin: 10px auto;
        padding: 0;
    }
    .carousel-inner img {
        width: 100%;
        height: auto;
        object-fit: cover;
        padding: 0;
        border-radius: 20px;
    }
    .carousel-item {
        height: auto;
        aspect-ratio: 16 / 9;
    }
    }

 @media (min-width: 600px) and (max-width: 1023px) {
    .categories {
        max-width: 600px;
        margin: 0 auto;
        justify-content: center;
        padding: 20px;
        overflow-x: auto;
    }
    }

 @media (min-width: 1024px) {
    .categories {
        max-width: 900px;
        margin: 0 auto;
        justify-content: center;
        padding: 20px;
        overflow-x: auto;
    }
    }
    </style>
    </head>
    <body>
    <div class="header">
    <img alt="Logo de la tienda de cervezas" src="https://lh3.googleusercontent.com/gps-cs/AIky0YUu_iHb76HWQOsSQBflySl2faKq5R4GyoZzZFn0mTwGFQB_CSITg3e5OYfI0N85MvqdxIGu82itcWGacnVBJQneFQAI3amSYcVYVmNcpzOu-3_kikJ7KAounBFfEZcWru_N9hjsVSGLLfG3=w1000-h1000-p-k-no" style="width: 150px; height: auto;"/>
</div>


<!-- Carousel Bootstrap -->
<div id="carouselExampleIndicators" class="carousel slide" data-ride="carousel" style="max-width:900px; margin: 10px auto; border-radius:20px;">
    <ol class="carousel-indicators">
        <li data-target="#carouselExampleIndicators" data-slide-to="0" class="active"></li>
        <li data-target="#carouselExampleIndicators" data-slide-to="1"></li>
        <li data-target="#carouselExampleIndicators" data-slide-to="2"></li>
        <li data-target="#carouselExampleIndicators" data-slide-to="3"></li>
    </ol>
    <div class="carousel-inner" style="border-radius:20px;">
        <div class="carousel-item active">
            <a href="https://example.com/pizza1"><img src="https://lh5.googleusercontent.com/p/AF1QipOli16Cun-MRC1UGtxmeyAZrXRaWNRlW5WNTht9=w1440-h810-p-k-no" class="d-block w-100" alt="Promoción de cerveza 1" /></a>
        </div>
        <div class="carousel-item">
            <a href="https://example.com/pizza2"><img src="https://lh5.googleusercontent.com/p/AF1QipNCgWE4Qpjjp5XlMh8OZOsypLkacxMuibiukmj7=w1440-h810-p-k-no" class="d-block w-100" alt="Promoción de cerveza 2" /></a>
        </div>
        <div class="carousel-item">
            <a href="https://example.com/pizza3"><img src="https://lh5.googleusercontent.com/p/AF1QipO2Op3Q793bR54eGAG94_ElqH7-_OT7bnkf-m51=w1440-h810-p-k-no" class="d-block w-100" alt="Promoción de cerveza 3" /></a>
        </div>
        <div class="carousel-item">
            <a href="https://example.com/pizza4"><img src="https://lh5.googleusercontent.com/p/AF1QipOSEw1a5xTziJUVCCWPlBgmnenFYQjFczpsHolX=w1440-h810-p-k-no" class="d-block w-100" alt="Promoción de cerveza 4" /></a>
        </div>
    </div>
    <a class="carousel-control-prev" href="#carouselExampleIndicators" role="button" data-slide="prev">
        <span class="carousel-control-prev-icon" aria-hidden="true"></span>
        <span class="sr-only">Anterior</span>
    </a>
    <a class="carousel-control-next" href="#carouselExampleIndicators" role="button" data-slide="next">
        <span class="carousel-control-next-icon" aria-hidden="true"></span>
        <span class="sr-only">Siguiente</span>
    </a>
    </div>

<!-- Barra de búsqueda -->
 <div style="text-align:center; margin: 10px;">
    <input id="search-input" placeholder="Buscar producto por nombre..." style="padding: 8px; width: 80%; max-width: 400px; border-radius: 8px; border: 1px solid #ddd;" type="text" />
    </div>

<!-- Categorías -->
<section class="categories">
    <div class="category active" onclick="filterProducts('category1')">
        <img alt="Cerveza Pilsen" src="https://lh5.googleusercontent.com/p/AF1QipN0zZRSSPIXHijb0sKIsoEwiA98_Mav3NcWx0PJ=w1000-h1000-p-k-no"/>
        <div class="category-title">Pilsen</div>
    </div>
    <div class="category" onclick="filterProducts('category2')">
        <img alt="Cerveza Cristal" src="https://lh5.googleusercontent.com/p/AF1QipOHscAFNrYkSVbYd2izphnpyRgznyotLfIXZ9FX=w1000-h1000-p-k-no"/>
        <div class="category-title">Cristal</div>
    </div>
    <div class="category" onclick="filterProducts('category3')">
        <img alt="Cerveza Cusqueña" src="https://lh5.googleusercontent.com/p/AF1QipPTv840Ia5cUZM77OFrOKfiEpKJgbf_5bX-50WC=w1000-h1000-p-k-no"/>
        <div class="category-title">Cusqueña</div>
    </div>
    <div class="category" onclick="filterProducts('category4')">
        <img alt="Cerveza Corona" src="https://lh5.googleusercontent.com/p/AF1QipMKukYDijPnCrcbfRTUVW5c8DPfagwxBg5C4P_A=w1000-h1000-p-k-no"/>
        <div class="category-title">Corona</div>
    </div>
    </section>

 <main>
    <section class='products-container' id='products'>
        <!-- Category 1: Pilsen -->
        <div class='product-item category1'>
            <img alt='Pilsen 12 unidades botella 630ml' src='https://lh5.googleusercontent.com/p/AF1QipPZb3yAXAe7pDYGN-WHrI8XfLF-FgeCTXjMttWK=w1000-h1000-p-k-no'/>
            <div class='product-info'>
                <h3>12UND</h3>
                <p>S/ 78.00</p>
                <input class='product-checkbox' data-name='PILSEN 12UND BOTELLA 630ML' data-price='78.00' data-product='1' type='checkbox'/>
            </div>
        </div>
        <div class='product-item category1'>
            <img alt='Pilsen 6 unidades lata 355ml' src='https://lh5.googleusercontent.com/p/AF1QipOD1yGcFQqXf6b4ubdw3sjbHg622D4C7qPBwwCk=w1000-h1000-p-k-no'/>
            <div class='product-info'>
                <h3>6UND</h3>
                <p>S/ 20.00</p>
                <input class='product-checkbox' data-name='PILSEN 6UND LATA 355ML' data-price='20.00' data-product='2' type='checkbox'/>
            </div>
        </div>
        <div class='product-item category1'>
            <img alt='Pilsen 6 unidades lata 473ml' src='https://lh5.googleusercontent.com/p/AF1QipNe18mvnzinRNWs1jCD0Dx7YR492_Ml9qRtv-Hv=w1000-h1000-p-k-no'/>
            <div class='product-info'>
                <h3>6UND</h3>
                <p>S/ 15.00</p>
                <input class='product-checkbox' data-name='PILSEN 6UND LATA 473ML' data-price='15.00' data-product='3' type='checkbox'/>
            </div>
        </div>
        <div class='product-item category1'>
            <img alt='Pilsen 12 unidades lata 355ml' src='https://lh5.googleusercontent.com/p/AF1QipMafbqYE7_EZabCXHhcluvniEn3cF0zubYYwha5=w1000-h1000-p-k-no'/>
            <div class='product-info'>
                <h3>12UND</h3>
                <p>S/ 12.00</p>
                <input class='product-checkbox' data-name='PILSEN 12UND LATA 355ML' data-price='12.00' data-product='4' type='checkbox'/>
            </div>
        </div>
        <div class='product-item category1'>
            <img alt='Pilsen 1 unidad botella 630ml' src='https://lh5.googleusercontent.com/p/AF1QipPCd6xQ3r2wWxGqEjWtqWNqRgZJJ5VyQBxaN_6E=w1000-h1000-p-k-no'/>
            <div class='product-info'>
                <h3>1UND</h3>
                <p>S/ 18.00</p>
                <input class='product-checkbox' data-name='PILSEN 1UND BOTELLA 630ML' data-price='18.00' data-product='5' type='checkbox'/>
            </div>
        </div>
        <div class='product-item category1'>
            <img alt='Pilsen 6 unidades botella 305ml' src='https://lh5.googleusercontent.com/p/AF1QipN8fUcEFPjUF7awsxiM-fidX0SB8thYKs8ejOXS=w1000-h1000-p-k-no'/>
            <div class='product-info'>
                <h3>6UND</h3>
                <p>S/ 25.00</p>
                <input class='product-checkbox' data-name='PILSEN 6UND BOTELLA 305ML' data-price='25.00' data-product='6' type='checkbox'/>
            </div>
        </div>
        <!-- Category 2: Cristal -->
        <div class='product-item category2'>
            <img alt='Cristal 12 unidades botella 650ml' src='https://lh5.googleusercontent.com/p/AF1QipMwIXT-b-_Jh8ftZ_yo804TBOKRodxZhyHzxZe6=w1000-h1000-p-k-no'/>
            <div class='product-info'>
                <h3>12UND</h3>
                <p>S/ 70.00</p>
                <input class='product-checkbox' data-name='CRISTAL 12UND BOTELLA 650ML' data-price='70.00' data-product='7' type='checkbox'/>
            </div>
        </div>
        <div class='product-item category2'>
            <img alt='Cristal 6 unidades lata 355ml' src='https://lh5.googleusercontent.com/p/AF1QipPAClUh4j1yLjhHxE8brWPaaA7HVshqCGtw9yTg=w1000-h1000-p-k-no'/>
            <div class='product-info'>
                <h3>6UND</h3>
                <p>S/ 45.00</p>
                <input class='product-checkbox' data-name='CRISTAL 6UND LATA 355ML' data-price='45.00' data-product='8' type='checkbox'/>
            </div>
        </div>
        <div class='product-item category2'>
            <img alt='Cristal 6 unidades lata 473ml' src='https://lh5.googleusercontent.com/p/AF1QipMmeTY_iOvLQx_jr36upcAriesRVHIQEsCEOeVp=w1000-h1000-p-k-no'/>
            <div class='product-info'>
                <h3>6UND</h3>
                <p>S/ 52.00</p>
                <input class='product-checkbox' data-name='CRISTAL 6UND LATA 473ML' data-price='52.00' data-product='9' type='checkbox'/>
            </div>
        </div>
        <div class='product-item category2'>
            <img alt='Cristal 12 unidades lata 355ml' src='https://lh5.googleusercontent.com/p/AF1QipPrDRBNwHDUxaluZYC6G06DLRqT8hJ4Q1ygCPfI=w1000-h1000-p-k-no'/>
            <div class='product-info'>
                <h3>12UND</h3>
                <p>S/ 48.00</p>
                <input class='product-checkbox' data-name='CRISTAL 12UND LATA 355ML' data-price='48.00' data-product='10' type='checkbox'/>
            </div>
        </div>
        <div class='product-item category2'>
            <img alt='Cristal 1 unidad botella 650ml' src='https://lh5.googleusercontent.com/p/AF1QipOApNU9kkwkfamFNGZrV5I7EhSSyxKZwGiMywT-=w1000-h1000-p-k-no'/>
            <div class='product-info'>
                <h3>1UND</h3>
                <p>S/ 65.00</p>
                <input class='product-checkbox' data-name='CRISTAL 1UND BOTELLA 650ML' data-price='65.00' data-product='11' type='checkbox'/>
            </div>
        </div>
        <div class='product-item category2'>
            <img alt='Cristal 6 unidades botella 330ml' src='https://lh5.googleusercontent.com/p/AF1QipOPC7nDmiTptTVoT-ZopqtoLhhdy4Y1_UnYxSmm=w1000-h1000-p-k-no'/>
            <div class='product-info'>
                <h3>6UND</h3>
                <p>S/ 75.00</p>
                <input class='product-checkbox' data-name='CRISTAL 6UND BOTELLA 330ML' data-price='75.00' data-product='12' type='checkbox'/>
            </div>
        </div>
        <!-- Category 3: Cusqueña -->
        <div class='product-item category3'>
            <img alt='Cusqueña Dorada 12 unidades botella 620ml' src='https://lh5.googleusercontent.com/p/AF1QipNoTsJrETd6q5R_4NE-3J7NFqBZ2_lDVDz_qgFP=w1000-h1000-p-k-no'/>
            <div class='product-info'>
                <h3>12UND</h3>
                <p>S/ 38.00</p>
                <input class='product-checkbox' data-name='CUSQUEÑA DORADA BOTELLA 12UND 620ML' data-price='38.00' data-product='13' type='checkbox'/>
            </div>
        </div>
        <div class='product-item category3'>
            <img alt='Cusqueña Dorada 6 unidades lata 355ml' src='https://lh5.googleusercontent.com/p/AF1QipPxFbOmsmYehzvFwrsgO7n7sYIVmGNIhbyIkTfB=w1000-h1000-p-k-no'/>
            <div class='product-info'>
                <h3>6UND</h3>
                <p>S/ 40.00</p>
                <input class='product-checkbox' data-name='CUSQUEÑA DORADA LATA 6UND 355ML' data-price='40.00' data-product='14' type='checkbox'/>
            </div>
        </div>
        <div class='product-item category3'>
            <img alt='Cusqueña Dorada 6 unidades botella 310ml' src='https://lh5.googleusercontent.com/p/AF1QipNwwrJABQhcpzwphwpj65nWj5mOzy8UkcEXEs-J=w1000-h1000-p-k-no'/>
            <div class='product-info'>
                <h3>6UND</h3>
                <p>S/ 45.00</p>
                <input class='product-checkbox' data-name='CUSQUEÑA DORADA BOTELLA 310ML 6UND' data-price='45.00' data-product='15' type='checkbox'/>
            </div>
        </div>
        <div class='product-item category3'>
            <img alt='Cusqueña Dorada 1 unidad botella 620ml' src='https://lh5.googleusercontent.com/p/AF1QipNgCBjfQQwmp2D6M1GW7CNcVbI4Z1chuRiB4A4a=w1000-h1000-p-k-no'/>
            <div class='product-info'>
                <h3>1UND</h3>
                <p>S/ 50.00</p>
                <input class='product-checkbox' data-name='CUSQUEÑA DORADA BOTELLA 620ML 1UND' data-price='50.00' data-product='16' type='checkbox'/>
            </div>
        </div>
        <div class='product-item category3'>
            <img alt='Cusqueña Negra 12 unidades botella 620ml' src='https://lh5.googleusercontent.com/p/AF1QipP0tdefcLaVakf85cGytfRKC1KZlc1b4NmhF4Ah=w1000-h1000-p-k-no'/>
            <div class='product-info'>
                <h3>12UND</h3>
                <p>S/ 55.00</p>
                <input class='product-checkbox' data-name='CUSQUEÑA NEGRA BOTELLA 620ML 12UND' data-price='55.00' data-product='17' type='checkbox'/>
            </div>
        </div>
        <div class='product-item category3'>
            <img alt='Cusqueña Negra 6 unidades lata 355ml' src='https://lh5.googleusercontent.com/p/AF1QipPAuHP_o-OlN8_h7ckQOA7FLivnddGWzW9Qd4W0=w1000-h1000-p-k-no'/>
            <div class='product-info'>
                <h3>6UND</h3>
                <p>S/ 38.00</p>
                <input class='product-checkbox' data-name='CUSQUEÑA NEGRA LATA 355ML 6UND' data-price='38.00' data-product='18' type='checkbox'/>
            </div>
        </div>
        <div class='product-item category3'>
            <img alt='Cusqueña Negra 6 unidades botella 310ml' src='https://lh5.googleusercontent.com/p/AF1QipNek4gSJN5hB1ZsFgHeb_Sncfcevv-PGJRzjV2f=w1000-h1000-p-k-no'/>
            <div class='product-info'>
                <h3>6UND</h3>
                <p>S/ 40.00</p>
                <input class='product-checkbox' data-name='CUSQUEÑA NEGRA BOTELLA 310ML 6UND' data-price='40.00' data-product='19' type='checkbox'/>
            </div>
        </div>
        <div class='product-item category3'>
            <img alt='Cusqueña Negra 1 unidad botella 620ml' src='https://lh3.googleusercontent.com/gps-cs/ADgaOlqzhG9TUv81NyUehZcMYJAyyULJ8N0oQECaipB79kewLW5fVvAZbNkSe8wG2Gk8Y0PYgPBScdnDHUzGmDE5ZVL8SIIN-a2jNPz50RLV6IFm_nN_cj0dWiDCbe_mbdCr3p5z9wNlPnVK0cc=w1000-h1000-p-k-no'/>
            <div class='product-info'>
                <h3>1UND</h3>
                <p>S/ 45.00</p>
                <input class='product-checkbox' data-name='CUSQUEÑA NEGRA BOTELLA 620ML 1UND' data-price='45.00' data-product='20' type='checkbox'/>
            </div>
        </div>
        <div class='product-item category3'>
            <img alt='Cusqueña Trigo 12 unidades botella 620ml' src='https://lh5.googleusercontent.com/p/AF1QipM4Nx30hCWjzmP-xBj8g25xnOPTdyGnaYQh3w7Z=w1000-h1000-p-k-no'/>
            <div class='product-info'>
                <h3>12UND</h3>
                <p>S/ 50.00</p>
                <input class='product-checkbox' data-name='CUSQUEÑA TRIGO BOTELLA 620ML 12UND' data-price='50.00' data-product='21' type='checkbox'/>
            </div>
        </div>
        <div class='product-item category3'>
            <img alt='Cusqueña Trigo 6 unidades lata 355ml' src='https://lh5.googleusercontent.com/p/AF1QipO4iyindkHDjnUINGJQq6qvPhbwKopod8HAqpCk=w1000-h1000-p-k-no'/>
            <div class='product-info'>
                <h3>6UND</h3>
                <p>S/ 55.00</p>
                <input class='product-checkbox' data-name='CUSQUEÑA TRIGO LATA 355ML 6UND' data-price='55.00' data-product='22' type='checkbox'/>
            </div>
        </div>
        <div class='product-item category3'>
            <img alt='Cusqueña Trigo 6 unidades botella 310ml' src='https://lh5.googleusercontent.com/p/AF1QipMMdiCbLWstSI1zorN9ORMoOwRMEkISgX5LMTVA=w1000-h1000-p-k-no'/>
            <div class='product-info'>
                <h3>6UND</h3>
                <p>S/ 38.00</p>
                <input class='product-checkbox' data-name='CUSQUEÑA TRIGO BOTELLA 310ML 6UND' data-price='38.00' data-product='23' type='checkbox'/>
            </div>
        </div>
        <div class='product-item category3'>
            <img alt='Cusqueña Trigo 1 unidad botella 620ml' src='https://lh5.googleusercontent.com/p/AF1QipN0hF8bRUE_5xFtWuNK7tBoEjwte5qvAkO6azO_=w1000-h1000-p-k-no'/>
            <div class='product-info'>
                <h3>1UND</h3>
                <p>S/ 40.00</p>
                <input class='product-checkbox' data-name='CUSQUEÑA TRIGO BOTELLA 620ML 1UND' data-price='40.00' data-product='24' type='checkbox'/>
            </div>
        </div>
        <!-- Category 4: Corona -->
        <div class='product-item category4'>
            <img alt='Corona 6 unidades botella 330ml' src='https://lh5.googleusercontent.com/p/AF1QipOb0rNDzoT3u3yvvnUzNfaEnxZTQrjGLQe76nVO=w1000-h1000-p-k-no'/>
            <div class='product-info'>
                <h3>6UND</h3>
                <p>S/ 38.00</p>
                <input class='product-checkbox' data-name='CORONA BOTELLA 330ML 6UND' data-price='38.00' data-product='25' type='checkbox'/>
            </div>
        </div>
        <div class='product-item category4'>
            <img alt='Corona 6 unidades lata 355ml' src='https://lh5.googleusercontent.com/p/AF1QipNpxGslUgp2AU6xtgihRkNiMoOHI9olKgj7D22d=w1000-h1000-p-k-no'/>
            <div class='product-info'>
                <h3>6UND</h3>
                <p>S/ 40.00</p>
                <input class='product-checkbox' data-name='CORONA LATA 355ML 6UND' data-price='40.00' data-product='26' type='checkbox'/>
            </div>
        </div>
    </section>
    </main>


<!-- Carrito -->
<section id="cart">
    <h2>Carrito de Compras</h2>
    <div style="margin:10px 0;">
        <input id="client-name" placeholder="Nombre del cliente" style="width:90%; padding:8px; margin:5px auto; display:block; border:1px solid #ddd; border-radius:5px;" type="text" />
        <input id="client-dni" placeholder="DNI del cliente (8 dígitos)" style="width:90%; padding:8px; margin:5px auto; display:block; border:1px solid #ddd; border-radius:5px;" type="text" />
    </div>
    <div id="cart-items"></div>
    <p id="cart-total">Total: S/ 0.00</p>
    <button id="order-button">Realizar Pedido</button>
    </section>

<div id="cart-button" onclick="toggleCart()">🛒</div>

<!-- Modal Producto -->
<div id="product-modal">
    <div>
        <button id="close-product-modal">&#10006;</button>
        <img alt="Producto" id="modal-product-image" src="" />
        <h3 id="modal-product-name"></h3>
        <p id="modal-product-price" style="font-weight:bold; font-size:18px;"></p>
        <div style="display:flex; align-items:center; gap:10px; margin-bottom:15px;">
            <button id="modal-quantity-decrease">-</button>
            <input id="modal-quantity" readonly="readonly" type="text" value="1" />
            <button id="modal-quantity-increase">+</button>
        </div>
        <button id="modal-add-to-cart" style="width:100%; padding:10px; background:#ff5722; color:#fff; border:none; border-radius:10px; cursor:pointer;">Agregar al carrito</button>
    </div>
    </div>

 <div id="loading-spinner">Cargando...</div>

<!-- Scripts JS -->
 <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/@popperjs/core@2.5.4/dist/umd/popper.min.js"></script>
 <script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.5.2/js/bootstrap.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>

 <script>

    $(document).ready(function() {
    let cart = JSON.parse(localStorage.getItem('cart')) || [];
    let modalQuantity = 1;
    let modalCurrentProduct = null;

    function formatCurrency(amount) {
        return `S/ ${parseFloat(amount).toFixed(2)}`;
    }

    function updateCart() {
        let cartItemsHtml = '';
        let total = 0;
        cart.forEach(item => {
            cartItemsHtml += `
                <div class='cart-item'>
                    <div class='product-info'>
                        <img alt='${item.name}' src='${item.image}'/>
                        <div class='product-details'>
                            <p style='margin: 0; font-weight: bold;'>${item.name}</p>
                            <p style='margin: 0;'>Precio unitario: ${formatCurrency(item.price)}</p>
                            <p style='margin: 0;'>Cantidad: ${item.quantity}</p>
                        </div>
                    </div>
                    <div class='actions'>
                        <button class='increase-quantity' data-product='${item.id}'>+</button>
                        <button class='decrease-quantity' data-product='${item.id}'>-</button>
                        <button class='remove-item' data-product='${item.id}'>🗑️ Eliminar</button>
                    </div>
                </div>
            `;
            total += item.price * item.quantity;
        });
        $('#cart-items').html(cartItemsHtml);
        $('#cart-total').text(`Total: ${formatCurrency(total)}`);
        localStorage.setItem('cart', JSON.stringify(cart));
    }

    $('.product-checkbox').change(function() {
        const productId = $(this).data('product');
        const productPrice = parseFloat($(this).data('price'));
        const productName = $(this).data('name');
        const productImage = $(this).closest('.product-item').find('img').attr('src');

        if ($(this).is(':checked')) {
            let existingProduct = cart.find(item => item.id === productId);
            if (existingProduct) {
                existingProduct.quantity++;
            } else {
                cart.push({ id: productId, name: productName, price: productPrice, quantity: 1, image: productImage });
            }
        } else {
            cart = cart.filter(item => item.id !== productId);
        }
        updateCart();
    });
    document.addEventListener('DOMContentLoaded', () => {
    document.querySelector('.categories').addEventListener('click', (event) => {
        const category = event.target.closest('.category');
        if (category) {
            document.querySelectorAll('.category').forEach(cat => cat.classList.remove('active'));
            category.classList.add('active');
        }
    });
    });
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
                $(`.product-checkbox[data-product=${productId}]`).prop('checked', false);
            }
            updateCart();
        }
    });

    $(document).on('click', '.remove-item', function() {
        const productId = $(this).data('product');
        cart = cart.filter(item => item.id !== productId);
        $(`.product-checkbox[data-product=${productId}]`).prop('checked', false);
        updateCart();
    });

    window.toggleCart = function() {
        $('#cart').toggle();
    };

    window.filterProducts = function(category) {
        // Limpiar el input de búsqueda cuando se cambia la categoría
        $('#search-input').val('');
        $('.product-item').hide();
        $('.product-item.' + category).show();
        $('.category').removeClass('active');
        $(`.category[onclick="filterProducts('${category}')"]`).addClass('active');
    };

    // Nuevo filtro de búsqueda por texto para nombre del producto
    $('#search-input').on('input', function() {
        const searchText = $(this).val().toLowerCase().trim();

        if (searchText.length > 0) {
            $('.product-item').each(function() {
                const productName = $(this).find('.product-checkbox').data('name').toLowerCase();
                if (productName.includes(searchText)) {
                    $(this).show();
                } else {
                    $(this).hide();
                }
            });
            $('.category').removeClass('active');
        } else {
            // Si está vacío el input, mostrar la categoría activa
            let activeCategory = $('.category.active').attr('onclick');
            if (activeCategory) {
                const match = activeCategory.match(/filterProducts\('(.+)'\)/);
                if (match && match[1]) {
                    filterProducts(match[1]);
                } else {
                    $('.product-item').show();
                }
            } else {
                $('.product-item').show();
            }
        }
    });

    $('.product-item').click(function(e) {
        if ($(e.target).is('input[type=checkbox], button')) return;
        modalCurrentProduct = $(this);
        const imgSrc = modalCurrentProduct.find('img').attr('src');
        const name = modalCurrentProduct.find('.product-checkbox').data('name');
        const price = parseFloat(modalCurrentProduct.find('.product-checkbox').data('price'));
        modalQuantity = 1;
        $('#modal-product-image').attr('src', imgSrc);
        $('#modal-product-name').text(name);
        $('#modal-product-price').text(formatCurrency(price));
        $('#modal-quantity').val(modalQuantity);
        $('#product-modal').fadeIn(200);
    });

    $('#close-product-modal').click(function() {
        $('#product-modal').fadeOut(200);
    });

    $('#modal-quantity-increase').click(function() {
        modalQuantity++;
        $('#modal-quantity').val(modalQuantity);
    });

    $('#modal-quantity-decrease').click(function() {
        if (modalQuantity > 1) {
            modalQuantity--;
            $('#modal-quantity').val(modalQuantity);
        }
    });

    $('#modal-add-to-cart').click(function() {
        if (!modalCurrentProduct) return;
        const productId = modalCurrentProduct.find('.product-checkbox').data('product');
        const productName = modalCurrentProduct.find('.product-checkbox').data('name');
        const productPrice = parseFloat(modalCurrentProduct.find('.product-checkbox').data('price'));
        const productImage = modalCurrentProduct.find('img').attr('src');
        let existingProduct = cart.find(item => item.id === productId);
        if (existingProduct) {
            existingProduct.quantity += modalQuantity;
        } else {
            cart.push({ id: productId, name: productName, price: productPrice, quantity: modalQuantity, image: productImage });
        }
        updateCart();
        $(`.product-checkbox[data-product="${productId}"]`).prop('checked', true);
        $('#product-modal').fadeOut(200);
    });

    $('#product-modal').click(function(e) {
        if (e.target === this) {
            $(this).fadeOut(200);
        }
    });

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
            <div style='font-family: monospace; font-size: 14px; line-height: 1.4; text-align: left;'>
                <h3 style='text-align: center; margin-bottom: 5px;'>BOLETA DE VENTA ELECTRÓNICA</h3>
               
                 <div style='text-align: center; margin: 15px 0;'>
                    <img id='qr-image' src='https://i.ibb.co/Kz9NwFym/yape-qr.jpg' style='width: 200px; border-radius: 10px;'/>
                    <p style='margin: 5px 0; font-size: 12px;'>Paga aquí con Yape</p>
                    <p style='margin: 0; font-size: 12px;'>Jhonny David Palacios Gutierrez</p>
                </div>
                <p style='margin:0;'><strong>CLIENTE:</strong> ${clientName}</p>
                <p style='margin:0;'><strong>DNI:</strong> ${clientDni}</p>
                <p style='margin:0;'><strong>FECHA:</strong> ${fechaStr}   <strong>HORA:</strong> ${horaStr}</p>
                <hr/>
                <p style='margin: 0;'><strong>Cant U.M PRODUCTO P.U. TOTAL</strong></p>`;
        cart.forEach(item => {
            boletaHtml += `
                <p style='margin: 0;'>${item.quantity} UNIDAD ${item.name.substring(0,24)} ${formatCurrency(item.price)} ${formatCurrency(item.price * item.quantity)}</p>`;
        });
        boletaHtml += `
                <hr/>
                <table style='width: 100%; font-size: 14px;'>
                    <tr>
                        <td style='text-align: left;'><strong>TOTAL (S/)</strong></td>
                        <td style='text-align: right;'><strong>${formatCurrency(total)}</strong></td>
                    </tr>
                </table>
                <hr/>
                <p style='margin: 0;'><strong>SON:</strong> ${enLetras(total)}</p>

                <button id='capture-button' style='margin-top:10px; background:#FF9800; color:white; padding:10px 20px; border:none; border-radius:5px;'>📸 Capturar Imagen</button>
                <button onclick='window.print()' style='margin-top:10px; background:#2196F3; color:white; padding:10px 20px; border:none; border-radius:5px;'>🖨 Imprimir</button>
                <button id='confirm-purchase' style='margin-top:10px; padding:10px 20px; background-color:#4CAF50; color:white; border:none; border-radius:5px; font-size:16px;'>Confirmar Compra</button>
            </div>`;

        const modal = document.createElement('div');
        modal.id = "boleta-modal";
        modal.style = "position:fixed; top:0; left:0; width:100%; height:100%; background:rgba(0,0,0,0.6); display:flex; align-items:center; justify-content:center; z-index:2000;";
        modal.innerHTML = `<div style='background:white; padding:20px; border-radius:10px; max-width:400px; width:90%; max-height:80vh; overflow-y:auto;'>${boletaHtml}</div>`;
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
            let whatsappURL = `https://wa.me/51975842622?text=${encodeURIComponent(orderDetails)}`;
            window.open(whatsappURL, '_blank');
            document.body.removeChild(modal);
            cart = [];
            localStorage.removeItem('cart');
            updateCart();
            const successMsg = document.createElement('div');
            successMsg.textContent = "✅ Mensaje de WhatsApp listo";
            successMsg.style = "position:fixed; top:20px; right:20px; background:#4CAF50; color:white; padding:10px 20px; border-radius:5px; font-size:16px; z-index:3000;";
            document.body.appendChild(successMsg);
            setTimeout(() => {
        window.location.reload();
    }, 2000);
    });

        modal.addEventListener('click', function(e) {
            if (e.target === modal) {
                document.body.removeChild(modal);
            }
        });
    });

    window.onload = function() {
        filterProducts('category1');
    };
    });

    </script>
</body>
</html>
