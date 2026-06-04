<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>SnackZone - Snacks & Drinks</title>
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;600;700;800&family=Nunito:wght@400;600&display=swap" rel="stylesheet"/>

  <style>
    /* ===== GLOBAL RESET & VARIABLES ===== */
    * { margin: 0; padding: 0; box-sizing: border-box; }

    :root {
      --orange: #FF6B2C;
      --yellow: #FFD600;
      --dark:   #1A1A2E;
      --card:   #FFFFFF;
      --bg:     #F5F6FA;
      --text:   #333;
      --muted:  #777;
      --radius: 16px;
      --shadow: 0 4px 18px rgba(0,0,0,0.10);
    }

    body {
      font-family: 'Nunito', sans-serif;
      background: var(--bg);
      color: var(--text);
    }

    /* ===== NAVBAR ===== */
    nav {
      background: var(--dark);
      padding: 16px 40px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      position: sticky;
      top: 0;
      z-index: 100;
      box-shadow: 0 2px 12px rgba(0,0,0,0.3);
    }

    .logo {
      font-family: 'Poppins', sans-serif;
      font-size: 26px;
      font-weight: 800;
      color: #fff;
      letter-spacing: -1px;
    }

    .logo span { color: var(--orange); }

    nav ul {
      list-style: none;
      display: flex;
      gap: 28px;
    }

    nav ul li a {
      color: #ccc;
      text-decoration: none;
      font-weight: 600;
      font-size: 15px;
      transition: color 0.2s;
    }

    nav ul li a:hover { color: var(--orange); }

    /* ===== HERO ===== */
    .hero {
      background: linear-gradient(135deg, #1A1A2E 0%, #16213E 60%, #FF6B2C22 100%);
      color: white;
      text-align: center;
      padding: 80px 20px 60px;
    }

    .hero h1 {
      font-family: 'Poppins', sans-serif;
      font-size: 52px;
      font-weight: 800;
      line-height: 1.15;
    }

    .hero h1 span { color: var(--orange); }

    .hero p {
      margin: 16px auto 36px;
      font-size: 18px;
      color: #aaa;
      max-width: 500px;
    }

    /* ===== SEARCH BAR ===== */
    .search-area {
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 14px;
      max-width: 640px;
      margin: 0 auto;
    }

    .search-row {
      display: flex;
      width: 100%;
      background: #fff;
      border-radius: 50px;
      overflow: hidden;
      box-shadow: 0 4px 20px rgba(255,107,44,0.25);
    }

    #searchInput {
      flex: 1;
      border: none;
      outline: none;
      padding: 16px 24px;
      font-size: 16px;
      font-family: 'Nunito', sans-serif;
      color: var(--dark);
    }

    #searchBtn {
      background: var(--orange);
      color: white;
      border: none;
      padding: 16px 28px;
      font-size: 16px;
      font-weight: 700;
      cursor: pointer;
      font-family: 'Poppins', sans-serif;
      transition: background 0.2s;
    }

    #searchBtn:hover { background: #e05520; }

    /* ===== CATEGORY FILTER BUTTONS ===== */
    .filter-row {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      gap: 10px;
    }

    .filter-btn {
      background: rgba(255,255,255,0.12);
      color: #fff;
      border: 1.5px solid rgba(255,255,255,0.25);
      padding: 8px 20px;
      border-radius: 50px;
      font-size: 14px;
      font-weight: 600;
      cursor: pointer;
      font-family: 'Nunito', sans-serif;
      transition: all 0.2s;
    }

    .filter-btn:hover,
    .filter-btn.active {
      background: var(--orange);
      border-color: var(--orange);
      color: #fff;
    }

    /* ===== SECTION LAYOUT ===== */
    section {
      padding: 50px 40px;
      max-width: 1200px;
      margin: 0 auto;
    }

    .section-title {
      font-family: 'Poppins', sans-serif;
      font-size: 28px;
      font-weight: 700;
      margin-bottom: 28px;
      color: var(--dark);
      display: flex;
      align-items: center;
      gap: 10px;
    }

    .section-title::after {
      content: '';
      flex: 1;
      height: 3px;
      background: linear-gradient(to right, var(--orange), transparent);
      border-radius: 2px;
      margin-left: 12px;
    }

    /* ===== PRODUCT GRID ===== */
    .product-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(220px, 1fr));
      gap: 24px;
    }

    /* ===== PRODUCT CARD ===== */
    .card {
      background: var(--card);
      border-radius: var(--radius);
      box-shadow: var(--shadow);
      overflow: hidden;
      transition: transform 0.22s, box-shadow 0.22s;
      cursor: pointer;
      display: flex;
      flex-direction: column;
    }

    .card:hover {
      transform: translateY(-6px);
      box-shadow: 0 12px 30px rgba(0,0,0,0.15);
    }

    /* Image container - fixed height so all cards are uniform */
    .card-img {
      width: 100%;
      height: 180px;
      background: #f0f0f5;
      display: flex;
      align-items: center;
      justify-content: center;
      overflow: hidden;
      padding: 16px;
    }

    .card-img img {
      max-width: 100%;
      max-height: 100%;
      object-fit: contain;
      transition: transform 0.3s;
    }

    .card:hover .card-img img { transform: scale(1.06); }

    .card-body {
      padding: 16px 18px 20px;
      flex: 1;
      display: flex;
      flex-direction: column;
      gap: 6px;
    }

    /* Small category badge on card */
    .badge {
      display: inline-block;
      font-size: 11px;
      font-weight: 700;
      text-transform: uppercase;
      letter-spacing: 0.5px;
      padding: 3px 10px;
      border-radius: 50px;
      margin-bottom: 4px;
    }

    .badge-chips      { background: #FFE0CC; color: #C04000; }
    .badge-chocolate  { background: #F5E0C8; color: #7B3F00; }
    .badge-soda       { background: #CCE8FF; color: #0055AA; }
    .badge-juice      { background: #D8F5D0; color: #1A6B00; }
    .badge-energy     { background: #FFFBCC; color: #7A6000; }
    .badge-candy      { background: #FFD6E8; color: #9B004A; }
    .badge-crackers   { background: #E8E4D0; color: #5A4A00; }
    .badge-water      { background: #D6F0FF; color: #005080; }

    .card-name {
      font-family: 'Poppins', sans-serif;
      font-size: 16px;
      font-weight: 700;
      color: var(--dark);
    }

    .card-desc {
      font-size: 13px;
      color: var(--muted);
      line-height: 1.5;
      flex: 1;
    }

    /* Star rating */
    .stars {
      color: #FFB300;
      font-size: 15px;
      letter-spacing: 1px;
    }

    .rating-text {
      font-size: 13px;
      color: var(--muted);
      font-weight: 600;
    }

    .card-footer {
      display: flex;
      align-items: center;
      justify-content: space-between;
      margin-top: 10px;
    }

    .price {
      font-family: 'Poppins', sans-serif;
      font-size: 17px;
      font-weight: 700;
      color: var(--orange);
    }

    .btn-buy {
      background: var(--dark);
      color: #fff;
      border: none;
      padding: 7px 16px;
      border-radius: 50px;
      font-size: 13px;
      font-weight: 700;
      cursor: pointer;
      font-family: 'Nunito', sans-serif;
      transition: background 0.2s;
    }

    .btn-buy:hover { background: var(--orange); }

    /* ===== NO RESULTS MESSAGE ===== */
    #noResults {
      display: none;
      text-align: center;
      padding: 60px 20px;
      color: var(--muted);
      font-size: 18px;
    }

    #noResults span { font-size: 48px; display: block; margin-bottom: 12px; }

    /* ===== FOOTER ===== */
    footer {
      background: var(--dark);
      color: #aaa;
      text-align: center;
      padding: 30px 20px;
      font-size: 14px;
      margin-top: 40px;
    }

    footer strong { color: var(--orange); }

    /* ===== RESPONSIVE ===== */
    @media (max-width: 700px) {
      nav { padding: 14px 20px; flex-direction: column; gap: 12px; }
      .hero h1 { font-size: 34px; }
      section { padding: 36px 16px; }
    }
  </style>
</head>
<body>

<!-- ==================== NAVBAR ==================== -->
<nav>
  <div class="logo">Snack<span>Zone</span></div>
  <ul>
    <li><a href="#snacks">Snacks</a></li>
    <li><a href="#drinks">Drinks</a></li>
    <li><a href="#about">About</a></li>
  </ul>
</nav>

<!-- ==================== HERO ==================== -->
<div class="hero">
  <h1>Your Favourite <span>Snacks</span><br>& Drinks, Rated.</h1>
  <p>Explore top-rated chips, chocolates, sodas, juices and more. All in one place.</p>

  <!-- SEARCH AREA -->
  <div class="search-area">
    <div class="search-row">
      <input type="text" id="searchInput" placeholder="Search snacks or drinks..." oninput="filterProducts()" />
      <button id="searchBtn" onclick="filterProducts()">Search</button>
    </div>

    <!-- CATEGORY FILTER BUTTONS -->
    <div class="filter-row">
      <button class="filter-btn active" onclick="setCategory('all', this)">All</button>
      <button class="filter-btn" onclick="setCategory('chips', this)">🥔 Chips</button>
      <button class="filter-btn" onclick="setCategory('chocolate', this)">🍫 Chocolate</button>
      <button class="filter-btn" onclick="setCategory('candy', this)">🍬 Candy</button>
      <button class="filter-btn" onclick="setCategory('crackers', this)">🥨 Crackers</button>
      <button class="filter-btn" onclick="setCategory('soda', this)">🥤 Soda</button>
      <button class="filter-btn" onclick="setCategory('juice', this)">🍊 Juice</button>
      <button class="filter-btn" onclick="setCategory('energy', this)">⚡ Energy</button>
      <button class="filter-btn" onclick="setCategory('water', this)">💧 Water</button>
    </div>
  </div>
</div>

<!-- ==================== ALL PRODUCTS SECTION ==================== -->
<section id="snacks">
  <div class="section-title">🍿 All Products</div>

  <!-- RESULTS BAR: count + sort -->
  <div style="display:flex; align-items:center; justify-content:space-between; margin-bottom:24px; flex-wrap:wrap; gap:12px;">
    <div id="resultCount" style="font-size:15px; color:var(--muted); font-weight:600;"></div>
    <div style="display:flex; align-items:center; gap:10px;">
      <label for="sortSelect" style="font-size:14px; color:var(--muted); font-weight:600;">Sort by:</label>
      <select id="sortSelect" onchange="filterProducts()"
        style="border:1.5px solid #ddd; border-radius:50px; padding:8px 16px; font-size:14px;
               font-family:'Nunito',sans-serif; background:#fff; color:var(--dark); cursor:pointer; outline:none;">
        <option value="default">Default</option>
        <option value="rating-high">Rating: High to Low</option>
        <option value="rating-low">Rating: Low to High</option>
        <option value="name-az">Name: A to Z</option>
        <option value="name-za">Name: Z to A</option>
        <option value="price-low">Price: Low to High</option>
        <option value="price-high">Price: High to Low</option>
      </select>
    </div>
  </div>

  <div class="product-grid" id="productGrid"></div>
  <div id="noResults"><span>😕</span>No products found. Try a different search!</div>
</section>

<!-- ==================== ABOUT SECTION ==================== -->
<section id="about" style="text-align:center; padding-top:10px;">
  <div style="background:#fff; border-radius:var(--radius); padding:40px; box-shadow:var(--shadow); max-width:700px; margin:0 auto;">
    <h2 style="font-family:'Poppins',sans-serif; font-size:26px; font-weight:700; color:var(--dark); margin-bottom:14px;">About SnackZone 🎉</h2>
    <p style="color:var(--muted); line-height:1.8; font-size:16px;">
      SnackZone is a capstone project website that helps you discover and explore popular snacks and drinks from around the world.
      Browse by category, search for your favourites, and check out honest ratings. Built with love using HTML, CSS &amp; JavaScript.
    </p>
  </div>
</section>

<!-- ==================== FOOTER ==================== -->
<footer>
  <strong>SnackZone</strong> &mdash; Capstone Project &copy; 2025. Made with 🧡 for snack lovers.
</footer>

<!-- ==================== JAVASCRIPT ==================== -->
<script>

  /* ==============================================
     PRODUCT DATA
     To add a new product:
       1. Copy one object below
       2. Fill in name, category, desc, rating, price, image
       3. For 'image': use a direct image URL of the EXACT product
     ============================================== */

  const products = [

    /* ============================================================
       CHIPS & CRISPS  (10 products)
    ============================================================ */
    {
      name: "Lay's Classic",
      category: "chips",
      desc: "Original salted potato chips. Light, thin, and perfectly crispy with every bite.",
      rating: 4.5,
      price: "$2.99",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/d/d5/Lays_Classic_chips.jpg/240px-Lays_Classic_chips.jpg"
    },
    {
      name: "Doritos Nacho Cheese",
      category: "chips",
      desc: "Bold, cheesy, triangular tortilla chips dusted in nacho cheese seasoning.",
      rating: 4.7,
      price: "$3.49",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/d/d0/Bag_of_Doritos_Nacho_Cheese.jpg/240px-Bag_of_Doritos_Nacho_Cheese.jpg"
    },
    {
      name: "Pringles Original",
      category: "chips",
      desc: "Stackable saddle-shaped crisps in the iconic tube. Classic salty flavour.",
      rating: 4.4,
      price: "$3.29",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/b/b3/Pringles_Original_2021.jpg/240px-Pringles_Original_2021.jpg"
    },
    {
      name: "Cheetos Crunchy",
      category: "chips",
      desc: "Crunchy corn puffs coated in bold cheddar cheese flavour. Finger-lickin' good.",
      rating: 4.6,
      price: "$2.89",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/b/b8/Cheetos_Crunchy.jpg/240px-Cheetos_Crunchy.jpg"
    },
    {
      name: "Lay's Sour Cream & Onion",
      category: "chips",
      desc: "Creamy sour cream meets tangy onion in every crispy chip. Irresistible combo.",
      rating: 4.6,
      price: "$3.19",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/4/4e/Lays_Sour_Cream_%26_Onion.jpg/240px-Lays_Sour_Cream_%26_Onion.jpg"
    },
    {
      name: "Doritos Cool Ranch",
      category: "chips",
      desc: "Cool ranch flavoured tortilla chips with a tangy, herby kick. Fan favourite.",
      rating: 4.6,
      price: "$3.49",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/2/26/Doritos_Cool_Ranch.jpg/240px-Doritos_Cool_Ranch.jpg"
    },
    {
      name: "Ruffles Original",
      category: "chips",
      desc: "Thick-cut ridged potato chips that hold more dip in every groove.",
      rating: 4.3,
      price: "$3.29",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/e/e1/Ruffles_chips.jpg/240px-Ruffles_chips.jpg"
    },
    {
      name: "Pringles BBQ",
      category: "chips",
      desc: "Smoky barbecue flavoured Pringles crisps. Sweet, tangy and totally addictive.",
      rating: 4.5,
      price: "$3.29",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/b/b3/Pringles_Original_2021.jpg/240px-Pringles_Original_2021.jpg"
    },
    {
      name: "Takis Fuego",
      category: "chips",
      desc: "Rolled tortilla chips with extreme hot chili pepper and lime flavour. Very spicy!",
      rating: 4.7,
      price: "$3.99",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/0/0f/Takis_Fuego.jpg/240px-Takis_Fuego.jpg"
    },
    {
      name: "Kettle Brand Sea Salt",
      category: "chips",
      desc: "Thick, extra crunchy kettle-cooked potato chips with just the right amount of salt.",
      rating: 4.4,
      price: "$3.79",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/5/51/Kettle_Brand_chips.jpg/240px-Kettle_Brand_chips.jpg"
    },

    /* ============================================================
       CHOCOLATE  (10 products)
    ============================================================ */
    {
      name: "KitKat Original",
      category: "chocolate",
      desc: "Crispy wafer fingers coated in smooth milk chocolate. Take a break!",
      rating: 4.8,
      price: "$1.99",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/5/54/KitKat_-_4_Finger_Bar.jpg/240px-KitKat_-_4_Finger_Bar.jpg"
    },
    {
      name: "Snickers",
      category: "chocolate",
      desc: "Peanuts, caramel and nougat wrapped in rich milk chocolate. Truly satisfying.",
      rating: 4.7,
      price: "$1.89",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/3/33/Snickers_bar.jpg/240px-Snickers_bar.jpg"
    },
    {
      name: "Reese's Peanut Butter Cups",
      category: "chocolate",
      desc: "Creamy peanut butter cups covered in Hershey's milk chocolate. An American classic.",
      rating: 4.9,
      price: "$2.29",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/c/ce/Reese_s_Peanut_Butter_Cups.jpg/240px-Reese_s_Peanut_Butter_Cups.jpg"
    },
    {
      name: "Toblerone Milk Chocolate",
      category: "chocolate",
      desc: "Swiss milk chocolate with honey and almond nougat in an iconic triangular bar.",
      rating: 4.6,
      price: "$4.99",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/4/41/Toblerone_Family_Bars.jpg/240px-Toblerone_Family_Bars.jpg"
    },
    {
      name: "Twix Original",
      category: "chocolate",
      desc: "Crunchy biscuit, smooth caramel and milk chocolate. Two delicious fingers per pack.",
      rating: 4.7,
      price: "$1.99",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/c/c6/TWIX_4To_Go_Candy_Bars.jpg/240px-TWIX_4To_Go_Candy_Bars.jpg"
    },
    {
      name: "Milky Way",
      category: "chocolate",
      desc: "Fluffy nougat and caramel coated in a layer of smooth milk chocolate.",
      rating: 4.5,
      price: "$1.89",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/3/3c/Milky_Way_bar.jpg/240px-Milky_Way_bar.jpg"
    },
    {
      name: "M&M's Milk Chocolate",
      category: "chocolate",
      desc: "Colourful candy shells filled with creamy milk chocolate. Melt in your mouth!",
      rating: 4.8,
      price: "$2.49",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/e/e9/Plain-M%26Ms-Pile.jpg/240px-Plain-M%26Ms-Pile.jpg"
    },
    {
      name: "Hershey's Milk Chocolate Bar",
      category: "chocolate",
      desc: "America's most beloved chocolate bar. Creamy, sweet and perfectly simple.",
      rating: 4.6,
      price: "$1.79",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/b/b2/Hershey_Bar.jpg/240px-Hershey_Bar.jpg"
    },
    {
      name: "Cadbury Dairy Milk",
      category: "chocolate",
      desc: "Rich, creamy British milk chocolate. Made with a glass and a half of fresh milk.",
      rating: 4.8,
      price: "$2.99",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/5/5d/Cadbury_Dairy_Milk_bar%2C_2014.jpg/240px-Cadbury_Dairy_Milk_bar%2C_2014.jpg"
    },
    {
      name: "Ferrero Rocher",
      category: "chocolate",
      desc: "Hazelnut and chocolate bonbons wrapped in gold foil. A luxurious treat.",
      rating: 4.9,
      price: "$5.99",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/6/60/Ferrero_Rocher_2009.jpg/240px-Ferrero_Rocher_2009.jpg"
    },

    /* ============================================================
       CANDY  (8 products)
    ============================================================ */
    {
      name: "Skittles Original",
      category: "candy",
      desc: "Taste the rainbow! Fruit-flavoured chewy candy in 5 bright colours.",
      rating: 4.5,
      price: "$1.79",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/5/53/Skittles-Party-Size.jpg/240px-Skittles-Party-Size.jpg"
    },
    {
      name: "Haribo Gold-Bears",
      category: "candy",
      desc: "The world-famous original gummy bears in 5 fruit flavours. A timeless classic.",
      rating: 4.6,
      price: "$2.49",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/6/6e/Goldb%C3%A4ren_Haribo.jpg/240px-Goldb%C3%A4ren_Haribo.jpg"
    },
    {
      name: "Starburst Original",
      category: "candy",
      desc: "Chewy, juicy fruit chews in strawberry, cherry, orange and lemon flavours.",
      rating: 4.4,
      price: "$1.99",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/0/09/Starburst-Candy-Wrapper.jpg/240px-Starburst-Candy-Wrapper.jpg"
    },
    {
      name: "Sour Patch Kids",
      category: "candy",
      desc: "Sour then sweet! Chewy candy pieces with a tangy sugar coating. Addictively good.",
      rating: 4.7,
      price: "$2.19",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/9/94/Sour_Patch_Kids_Bag.jpg/240px-Sour_Patch_Kids_Bag.jpg"
    },
    {
      name: "Jolly Rancher Hard Candy",
      category: "candy",
      desc: "Long-lasting hard candy in bold fruit flavours — watermelon, apple, cherry and more.",
      rating: 4.4,
      price: "$2.29",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/3/3f/Jolly_Ranchers.jpg/240px-Jolly_Ranchers.jpg"
    },
    {
      name: "Nerds Original",
      category: "candy",
      desc: "Tiny, tangy, crunchy candy in two flavours per box. Wildly fun to eat.",
      rating: 4.3,
      price: "$1.49",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/e/e7/Nerds_candy_box.jpg/240px-Nerds_candy_box.jpg"
    },
    {
      name: "Pop Rocks Original",
      category: "candy",
      desc: "The legendary candy that pops and crackles on your tongue. Strawberry flavour.",
      rating: 4.5,
      price: "$1.29",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/7/77/Pop_Rocks_candy.jpg/240px-Pop_Rocks_candy.jpg"
    },
    {
      name: "Swedish Fish",
      category: "candy",
      desc: "Soft, chewy red fish-shaped candy with a unique sweet berry flavour.",
      rating: 4.4,
      price: "$2.09",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/3/3e/Swedish_fish_candy.jpg/240px-Swedish_fish_candy.jpg"
    },

    /* ============================================================
       CRACKERS & BISCUITS  (6 products)
    ============================================================ */
    {
      name: "Ritz Original",
      category: "crackers",
      desc: "Buttery, flaky round crackers perfect on their own or paired with cheese.",
      rating: 4.5,
      price: "$3.99",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/9/9e/Ritz-Crackers.jpg/240px-Ritz-Crackers.jpg"
    },
    {
      name: "Wheat Thins Original",
      category: "crackers",
      desc: "Crispy whole wheat crackers with a slightly nutty, toasty taste. Light and satisfying.",
      rating: 4.2,
      price: "$3.49",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/8/88/Wheat_Thins.jpg/240px-Wheat_Thins.jpg"
    },
    {
      name: "Triscuit Original",
      category: "crackers",
      desc: "Woven wheat crackers baked with just oil and a pinch of salt. Hearty and crunchy.",
      rating: 4.3,
      price: "$3.69",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/5/52/Triscuit_crackers.jpg/240px-Triscuit_crackers.jpg"
    },
    {
      name: "Goldfish Cheddar",
      category: "crackers",
      desc: "Bite-sized cheddar baked snack crackers shaped like little fish. Kids love them!",
      rating: 4.6,
      price: "$3.29",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/a/a0/Goldfish_Cheddar_Crackers.jpg/240px-Goldfish_Cheddar_Crackers.jpg"
    },
    {
      name: "Cheez-It Original",
      category: "crackers",
      desc: "Square baked snack crackers made with 100% real cheese. Crispy and cheesy.",
      rating: 4.5,
      price: "$3.79",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/d/d0/Cheez-It_crackers.jpg/240px-Cheez-It_crackers.jpg"
    },
    {
      name: "Club Crackers Original",
      category: "crackers",
      desc: "Light, crispy layered crackers with a buttery flavour. Great for entertaining.",
      rating: 4.2,
      price: "$3.49",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/c/c2/Club_crackers.jpg/240px-Club_crackers.jpg"
    },

    /* ============================================================
       SODA / FIZZY DRINKS  (10 products)
    ============================================================ */
    {
      name: "Coca-Cola Classic",
      category: "soda",
      desc: "The world's most iconic fizzy drink. Rich caramel cola taste with perfect carbonation.",
      rating: 4.8,
      price: "$1.49",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/c/c6/Coca-Cola_bottle.jpg/240px-Coca-Cola_bottle.jpg"
    },
    {
      name: "Pepsi Original",
      category: "soda",
      desc: "Crisp, refreshing cola with a slightly sweeter flavour profile than its rival.",
      rating: 4.6,
      price: "$1.49",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/6/6e/Pepsi_can.jpg/240px-Pepsi_can.jpg"
    },
    {
      name: "Sprite",
      category: "soda",
      desc: "Clean, crisp lemon-lime soda. Caffeine-free and super refreshing on a hot day.",
      rating: 4.5,
      price: "$1.49",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/3/3e/Sprite_2009.jpg/240px-Sprite_2009.jpg"
    },
    {
      name: "Dr Pepper",
      category: "soda",
      desc: "A unique blend of 23 flavours unlike anything else. You either love it or you don't.",
      rating: 4.4,
      price: "$1.59",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/4/4c/DrPepper_US_can.jpg/240px-DrPepper_US_can.jpg"
    },
    {
      name: "Fanta Orange",
      category: "soda",
      desc: "Bright, fruity orange soda. Bubbly, sweet and full of fun citrus flavour.",
      rating: 4.3,
      price: "$1.49",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/4/46/Fanta_Orange_bottle.jpg/240px-Fanta_Orange_bottle.jpg"
    },
    {
      name: "Mountain Dew Original",
      category: "soda",
      desc: "Bold, citrus-charged soda with a neon green colour and energizing kick.",
      rating: 4.4,
      price: "$1.59",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/6/6e/Mountain_Dew_Can.jpg/240px-Mountain_Dew_Can.jpg"
    },
    {
      name: "7UP Original",
      category: "soda",
      desc: "Crystal-clear lemon-lime soda. Light, bubbly and totally refreshing. No caffeine.",
      rating: 4.3,
      price: "$1.49",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/8/8b/7up.jpg/240px-7up.jpg"
    },
    {
      name: "Canada Dry Ginger Ale",
      category: "soda",
      desc: "Smooth, subtly spiced ginger ale. Great on its own or as a mixer. Made with real ginger.",
      rating: 4.4,
      price: "$1.59",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/5/55/Canada_Dry_ginger_ale.jpg/240px-Canada_Dry_ginger_ale.jpg"
    },
    {
      name: "Coca-Cola Zero Sugar",
      category: "soda",
      desc: "The same great Coca-Cola taste but with zero sugar and zero calories.",
      rating: 4.5,
      price: "$1.49",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/c/c6/Coca-Cola_bottle.jpg/240px-Coca-Cola_bottle.jpg"
    },
    {
      name: "Barq's Root Beer",
      category: "soda",
      desc: "Classic American root beer with a bold, creamy taste and a slight caffeine kick.",
      rating: 4.3,
      price: "$1.59",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/b/b5/Barqs_root_beer.jpg/240px-Barqs_root_beer.jpg"
    },

    /* ============================================================
       JUICE  (8 products)
    ============================================================ */
    {
      name: "Tropicana Orange Juice",
      category: "juice",
      desc: "100% pure squeezed orange juice. No added sugars, colours or preservatives.",
      rating: 4.6,
      price: "$3.99",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/5/5e/Tropicana_OJ.jpg/240px-Tropicana_OJ.jpg"
    },
    {
      name: "Minute Maid Lemonade",
      category: "juice",
      desc: "Classic lemonade made from real lemons. Sweet, tart and perfectly refreshing.",
      rating: 4.4,
      price: "$2.99",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/1/17/Minute_Maid_Lemonade.jpg/240px-Minute_Maid_Lemonade.jpg"
    },
    {
      name: "Welch's Grape Juice",
      category: "juice",
      desc: "100% Concord grape juice. Deep, rich and naturally sweet with no added sugar.",
      rating: 4.5,
      price: "$3.49",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/b/bf/Welch%27s_Grape_Juice_bottle.jpg/240px-Welch%27s_Grape_Juice_bottle.jpg"
    },
    {
      name: "Ocean Spray Cranberry",
      category: "juice",
      desc: "Tart, tangy cranberry juice cocktail. A classic American refreshment since 1930.",
      rating: 4.4,
      price: "$3.29",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/6/64/Ocean_Spray_Cranberry_Juice.jpg/240px-Ocean_Spray_Cranberry_Juice.jpg"
    },
    {
      name: "Naked Green Machine",
      category: "juice",
      desc: "A powerful green juice smoothie blend of apple, kiwi, mango and banana. No added sugar.",
      rating: 4.5,
      price: "$4.49",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/3/34/Naked_Green_Machine.jpg/240px-Naked_Green_Machine.jpg"
    },
    {
      name: "Snapple Peach Tea",
      category: "juice",
      desc: "Real brewed tea with a sweet peach flavour. Made from the best stuff on earth.",
      rating: 4.5,
      price: "$2.49",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/8/84/Snapple_Peach_Tea.jpg/240px-Snapple_Peach_Tea.jpg"
    },
    {
      name: "Capri Sun Fruit Punch",
      category: "juice",
      desc: "The iconic pouch drink kids love. Fruity, sweet punch with no artificial colours.",
      rating: 4.3,
      price: "$4.99",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/c/c6/Capri_Sun_Fruit_Punch.jpg/240px-Capri_Sun_Fruit_Punch.jpg"
    },
    {
      name: "V8 Original Vegetable Juice",
      category: "juice",
      desc: "A blend of 8 vegetables including tomato, carrot and celery. One serving of veggies per can.",
      rating: 4.2,
      price: "$2.79",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/e/ea/V8_Vegetable_Juice.jpg/240px-V8_Vegetable_Juice.jpg"
    },

    /* ============================================================
       ENERGY DRINKS  (7 products)
    ============================================================ */
    {
      name: "Red Bull Original",
      category: "energy",
      desc: "The original energy drink. Vitalises body and mind with caffeine and taurine.",
      rating: 4.5,
      price: "$2.99",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/8/8f/Red_Bull_can_2020.jpg/240px-Red_Bull_can_2020.jpg"
    },
    {
      name: "Monster Energy Original",
      category: "energy",
      desc: "Big 16oz can, big energy. B-vitamins, caffeine and taurine to get you going.",
      rating: 4.6,
      price: "$3.29",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/7/70/Monster_Energy_can.jpg/240px-Monster_Energy_can.jpg"
    },
    {
      name: "Celsius Sparkling Orange",
      category: "energy",
      desc: "Fitness energy drink with green tea extract and no sugar. Sparkling orange flavour.",
      rating: 4.4,
      price: "$2.49",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/a/a7/Celsius_drink_can.jpg/240px-Celsius_drink_can.jpg"
    },
    {
      name: "Bang Energy Original",
      category: "energy",
      desc: "300mg of caffeine per can, zero sugar and packed with amino acids. For serious athletes.",
      rating: 4.3,
      price: "$2.99",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/5/5c/Bang_Energy_can.jpg/240px-Bang_Energy_can.jpg"
    },
    {
      name: "Rockstar Original",
      category: "energy",
      desc: "Party like a rockstar! Full-flavoured energy drink with taurine and B-vitamins.",
      rating: 4.2,
      price: "$2.89",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/c/c4/Rockstar_energy_drink.jpg/240px-Rockstar_energy_drink.jpg"
    },
    {
      name: "Red Bull Sugar Free",
      category: "energy",
      desc: "All the energy of Red Bull Original, with zero sugar. Same great taste.",
      rating: 4.4,
      price: "$2.99",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/8/8f/Red_Bull_can_2020.jpg/240px-Red_Bull_can_2020.jpg"
    },
    {
      name: "Ghost Energy Sour Patch Kids",
      category: "energy",
      desc: "Officially licensed Sour Patch Kids flavoured energy drink. 200mg caffeine, zero sugar.",
      rating: 4.5,
      price: "$3.49",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/7/70/Monster_Energy_can.jpg/240px-Monster_Energy_can.jpg"
    },

    /* ============================================================
       WATER  (5 products)
    ============================================================ */
    {
      name: "FIJI Natural Artesian Water",
      category: "water",
      desc: "Naturally filtered through volcanic rock aquifers. Soft, smooth and pure tasting.",
      rating: 4.7,
      price: "$2.29",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/e/e8/Fiji_Water_bottle.jpg/240px-Fiji_Water_bottle.jpg"
    },
    {
      name: "Evian Natural Spring Water",
      category: "water",
      desc: "Premium French alpine spring water. Pure, light and perfectly balanced in minerals.",
      rating: 4.6,
      price: "$1.99",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/9/92/Evian_water.jpg/240px-Evian_water.jpg"
    },
    {
      name: "Smartwater",
      category: "water",
      desc: "Vapour-distilled water with added electrolytes. Clean, crisp taste for every occasion.",
      rating: 4.5,
      price: "$2.19",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/a/af/Smartwater_bottle.jpg/240px-Smartwater_bottle.jpg"
    },
    {
      name: "San Pellegrino Sparkling",
      category: "water",
      desc: "Italian natural sparkling mineral water with fine bubbles. Elegant and refined.",
      rating: 4.7,
      price: "$2.49",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/3/3d/San_Pellegrino_sparkling_water.jpg/240px-San_Pellegrino_sparkling_water.jpg"
    },
    {
      name: "Perrier Sparkling Water",
      category: "water",
      desc: "Iconic French sparkling mineral water with bold carbonation. Classic green bottle.",
      rating: 4.6,
      price: "$2.29",
      image: "https://upload.wikimedia.org/wikipedia/commons/thumb/8/87/Perrier_sparkling_water.jpg/240px-Perrier_sparkling_water.jpg"
    }
  ];

  /* ==============================================
     RENDER STARS from a rating number (e.g. 4.5)
  ============================================== */
  function renderStars(rating) {
    let stars = '';
    for (let i = 1; i <= 5; i++) {
      if (rating >= i) stars += '★';
      else if (rating >= i - 0.5) stars += '½';
      else stars += '☆';
    }
    return stars;
  }

  /* ==============================================
     GET BADGE CLASS from category name
  ============================================== */
  function getBadge(cat) {
    const map = {
      chips:     'badge-chips',
      chocolate: 'badge-chocolate',
      soda:      'badge-soda',
      juice:     'badge-juice',
      energy:    'badge-energy',
      candy:     'badge-candy',
      crackers:  'badge-crackers',
      water:     'badge-water'
    };
    return map[cat] || 'badge-chips';
  }

  /* ==============================================
     ACTIVE CATEGORY (tracks which filter is on)
  ============================================== */
  let activeCategory = 'all';

  function setCategory(cat, btn) {
    activeCategory = cat;
    /* Remove active class from all filter buttons */
    document.querySelectorAll('.filter-btn').forEach(b => b.classList.remove('active'));
    /* Add active to the clicked one */
    btn.classList.add('active');
    filterProducts();
  }

  /* ==============================================
     MAIN FILTER + SORT FUNCTION
     Runs on every keypress, category click, or sort change
  ============================================== */
  function filterProducts() {
    const query   = document.getElementById('searchInput').value.toLowerCase().trim();
    const grid    = document.getElementById('productGrid');
    const noRes   = document.getElementById('noResults');
    const sortVal = document.getElementById('sortSelect').value;
    const countEl = document.getElementById('resultCount');

    /* 1. FILTER */
    let filtered = products.filter(p => {
      const matchCat    = (activeCategory === 'all') || (p.category === activeCategory);
      const matchSearch = p.name.toLowerCase().includes(query) ||
                          p.desc.toLowerCase().includes(query) ||
                          p.category.toLowerCase().includes(query);
      return matchCat && matchSearch;
    });

    /* 2. SORT */
    if (sortVal === 'rating-high') {
      filtered.sort((a, b) => b.rating - a.rating);
    } else if (sortVal === 'rating-low') {
      filtered.sort((a, b) => a.rating - b.rating);
    } else if (sortVal === 'name-az') {
      filtered.sort((a, b) => a.name.localeCompare(b.name));
    } else if (sortVal === 'name-za') {
      filtered.sort((a, b) => b.name.localeCompare(a.name));
    } else if (sortVal === 'price-low') {
      /* Strip the $ sign and convert to number for comparison */
      filtered.sort((a, b) => parseFloat(a.price.replace('$','')) - parseFloat(b.price.replace('$','')));
    } else if (sortVal === 'price-high') {
      filtered.sort((a, b) => parseFloat(b.price.replace('$','')) - parseFloat(a.price.replace('$','')));
    }

    /* 3. RENDER */
    if (filtered.length === 0) {
      grid.innerHTML = '';
      noRes.style.display = 'block';
      countEl.textContent = '0 products found';
    } else {
      noRes.style.display = 'none';
      countEl.textContent = filtered.length + ' product' + (filtered.length !== 1 ? 's' : '') + ' found';
      grid.innerHTML = filtered.map(p => `
        <div class="card" data-category="${p.category}">
          <div class="card-img">
            <img
              src="${p.image}"
              alt="${p.name}"
              onerror="this.src='https://via.placeholder.com/200x160?text=No+Image'"
            />
          </div>
          <div class="card-body">
            <span class="badge ${getBadge(p.category)}">${p.category.toUpperCase()}</span>
            <div class="card-name">${p.name}</div>
            <div class="card-desc">${p.desc}</div>
            <div class="stars" title="${p.rating} / 5">${renderStars(p.rating)}</div>
            <div class="rating-text">${p.rating} / 5</div>
            <div class="card-footer">
              <span class="price">${p.price}</span>
              <button class="btn-buy">+ Details</button>
            </div>
          </div>
        </div>
      `).join('');
    }
  }

  /* Load all products when page opens */
  filterProducts();

</script>

</body>
</html>
