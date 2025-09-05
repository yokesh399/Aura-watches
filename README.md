[index.html](https://github.com/user-attachments/files/22118512/index.html)
<!DOCTYPE html>
<html>
<head>
  <title> AuraTimes- Premium Watches</title>
  <link rel="stylesheet" href="watchstyle.css">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link rel="icon" type="image/png" href="favicon.png">

  <!-- Firebase SDKs -->
  <script src="https://www.gstatic.com/firebasejs/8.10.0/firebase-app.js"></script>
  <script src="https://www.gstatic.com/firebasejs/8.10.0/firebase-database.js"></script>
  <script src="https://www.gstatic.com/firebasejs/8.10.0/firebase-auth.js"></script>
  <script src="https://maps.googleapis.com/maps/api/js?key=AIzaSyD9D5HUEng-7WuqbqX5oNl_sLRS1AYaTJU&libraries=places"></script>
</head>
<body>

<!-- NAVIGATION BAR -->
<header>
  <div class="logo">
    <img src="logo.jpg" alt="Logo" class="navbar-logo">
    <span>AuraTimes</span>
    <div class="menu-toggle">☰ Menu</div>
  </div>
  <nav>
    <ul>
      <li><a href="#">Home</a></li>
      <li><a href="#popular-section">Watches</a></li>
      <li><a href="#contact">Contact</a></li>
      <li><a href="#" onclick="openCart()">View Cart 🛒</a></li>
      <li><a href="javascript:void(0)" onclick="viewOrders()">View Order</a></li>
      <li><a href="javascript:void(0)" onclick="showLoginPopup()">Login / Sign Up</a></li>
    </ul>
  </nav>
</header>

<!-- Cart Overlay (unchanged) -->
<div id="cart-overlay" style="display:none; position:fixed; top:0; left:0; width:100%; height:100%; 
  background: rgba(0,0,0,0.5); z-index:1000; overflow-y:auto; padding: 60px 20px; box-sizing: border-box;">

  <div id="cart-popup" style="background:white; padding:30px 20px; border-radius:10px; 
    box-shadow:0 0 15px rgba(0,0,0,0.3); max-width:700px; width:100%; margin:auto;">

    <h2 style="text-align:center; margin-bottom: 20px;">🛍️ Your Cart</h2>
    
    <div id="cart-container" style="display:flex; flex-wrap:wrap; gap:20px; justify-content:center; margin-bottom: 20px;"></div>

    <div style="text-align:center;">
      <button onclick="placeOrder()" style="background:green; color:white; padding:12px 24px; border:none; border-radius:5px; font-size:16px; margin-right:10px;">Place Order</button>
      <button onclick="closeCart()" style="background:red; color:white; padding:12px 24px; border:none; border-radius:5px; font-size:16px;">Close</button>
    </div>

  </div>
</div>

<!-- Order View Popup (unchanged) -->
<div id="order-popup" style="display:none; position:fixed; top:10%; left:50%; transform:translateX(-50%);
 background:white; padding:20px; border-radius:10px; box-shadow:0 0 15px rgba(0,0,0,0.3); z-index:999; max-width:90%; max-height:80%; overflow-y:auto;">
  <h2 style="text-align:center; color:gold;"><br>Your Order Details</h2>
  <div id="order-container" style="margin-top:15px;"></div>
  <button onclick="closeOrderPopup()" style="margin-top:15px; background:red; color:white; padding:8px 16px; border:none; border-radius:5px;">Close</button>
</div>

<!-- Login / Signup Popup -->
<!-- Login / Signup Popup -->
<div id="login-popup" style="display:none; position:fixed; top:0; left:0; width:100%; height:100%;
background: rgba(0,0,0,0.6); z-index:1002; display:flex; justify-content:center; align-items:center;">
  <div style="background:white; padding:30px; border-radius:10px; width:90%; max-width:400px; text-align:center;">
    <h3>🔐 Login / Sign Up</h3>
    <input type="email" id="loginEmail" placeholder="Email" style="width:100%; padding:10px; margin-top:10px;"><br>
    <input type="password" id="loginPassword" placeholder="Password" style="width:100%; padding:10px; margin-top:10px;">
<input type="checkbox" id="showPassword" style="margin-top:10px;"> Show Password

    <button onclick="login()">Login</button>
    <button onclick="signUp()">Sign Up</button>
    <button onclick="guestLogin()">Continue as Guest</button>
    
  </div>
</div>

<script>
// Show login popup automatically if no user is logged in
document.addEventListener("DOMContentLoaded", () => {
  firebase.auth().onAuthStateChanged(user => {
    if (!user) {
      // No user logged in, show login popup
      showLoginPopup();
    } else {
      // User is logged in, load their cart
      loadCart(user.uid);
    }
  });
});

// Function to show login popup
function showLoginPopup() {
  document.getElementById("login-popup").style.display = "flex";
}

// Function to close login popup
function closeLoginPopup() {
  document.getElementById("login-popup").style.display = "none";
}
</script>

<!-- Navbar button example -->
<li><a href="javascript:void(0)" onclick="showLoginPopup()">Login / Sign Up</a></li>






<!-- Scrolling Slogan Banner (unchanged) -->
<div class="scroll-slogan">
  <p>⏱️ Discover Timeless Elegance with TimeAura — Luxury Watches for Every Style! ⌚</p>
</div>

<!-- IMAGE SLIDER + HERO TEXT (unchanged) -->
<section class="slider" style="position: relative; margin-top: 70px;">
  <div class="slides">
    <img src="watch.jpg" class="slide" style="display:block; width: 100%; height: 700px; object-fit: cover;">
    <img src="watch1.jpg" class="slide" style="width: 100%; height: 700px; object-fit: cover;">
    <img src="watch2.jog.jpg" class="slide" style="width: 100%; height: 700px; object-fit: cover;">
    <img src="watch8.png" class="slide" style="width: 100%; height: 700px; object-fit: cover;">
    <img src="watch5.jpg" class="slide" style="width: 100%; height: 700px; object-fit: cover;">
    <img src="watch4.jpg" class="slide" style="width: 100%; height: 700px; object-fit: cover;">
  </div>

  <!-- Hero Text scrolling word -->
  <div class="hero-text">
    <h1>Luxury That Defines You</h1>
    <p>Explore premium watches built for timeless elegance.</p>
    <a href="#popular-section" class="hero-btn">Shop Now</a>
  </div>

  <!-- Why Us merged below hero -->
  <div class="home-why-us">
    <div class="features">
      <div class="feature-box">🕰️ 100% Authentic</div>
      <div class="feature-box">🚚 Free Shipping</div>
      <div class="feature-box">💰 7-Day Return</div>
      <div class="feature-box">🔒 Secure Payment</div>
    </div>
  </div>
</section>

<!-- POPULAR WATCHES (unchanged) -->
<section id="popular-section">
  <div class="popular-header">
    <h2>Popular Watches</h2>
    <div class="filter-buttons">
      <button onclick="filterWatches('all')">All</button>
      <button onclick="filterWatches('men')">Men</button>
      <button onclick="filterWatches('women')">Women</button>
      <button onclick="filterWatches('couple')">Couples</button>
    </div>
  </div>
  <div id="popular-container"></div>
</section>

<!-- CONTACT (unchanged) -->
<section id="contact">
  <div class="contact-container">
    <div class="contact-header">
      <img src="logo.jpg" alt="TimeAura Logo" class="contact-logo">
      <h2>AuraTimes Watches</h2>
      <p>Premium Timepieces for Every Style</p>
    </div>

    <div class="contact-details">
      <div class="contact-box">
        <h4>Email</h4>
        <p>support@shobaselvara.com</p>
      </div>
      <div class="contact-box">
        <h4>Phone</h4>
        <p>+91 98765 43210</p>
      </div>
      <div class="contact-box">
        <h4>Address</h4>
        <p>123, Anna Nagar, Chennai, Tamil Nadu</p>
      </div>
    </div>

     <div class="map-container">
      <iframe
        src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3916.458773004662!2d80.23283721533444!3d13.08268029078947!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x3a5265eaf9a1e2c5%3A0x4d63c47e65d3ae0a!2sChennai%20Central!5e0!3m2!1sen!2sin!4v1691575427481!5m2!1sen!2sin"
        width="100%" height="300" style="border:0;" allowfullscreen="" loading="lazy">
      </iframe>
    </div>
  </div>
</section>

<!-- Mouse Cursor Follower (unchanged) -->
<div class="cursor-follower"></div>

<!-- Toast Message (unchanged) -->
<div id="toast" style="position: fixed; bottom: 30px; right: 30px; background-color: black; color: gold;
padding: 12px 20px; border-radius: 5px; display: none; font-weight: bold; z-index: 9999;">
  Item added to cart!
</div>

<!-- Place Order Popup (unchanged) -->
<div id="order-form-popup" style="display:none; position:fixed; top:0; left:0; width:100%; height:100%;
background: rgba(0,0,0,0.6); z-index:1001;  justify-content: center; align-items: center;">
  <div style="background:white; padding:30px 25px; border-radius:10px; width:90%; max-width:400px; text-align:center;">
    <h3>📝 Confirm Your Order</h3>
    <input type="text" id="customer-name" placeholder="Your Name" style="width:100%; padding:10px; margin-top:10px;"><br>
    <input type="number" id="customer-phone" placeholder="Phone Number" style="width:100%; padding:10px; margin-top:10px;"><br>
    <select id="payment-method" style="width:100%; padding:10px; margin-top:10px;">
      <option value="Select">Select Payment Method</option>
      <option value="Cash on Delivery">Cash on Delivery</option>
      <option value="GPay">GPay</option>
    </select><br><br>

    <!-- New Location Field -->
    <input type="text" id="customer-location" placeholder="Paste Google Maps link here" style="width:100%; padding:10px; margin-top:10px;">
    <a href="https://www.google.com/maps" target="_blank" style="display:block; margin-top:5px; color:blue;">🔍 Search your location on Google Maps</a>

    <button type="button" onclick="submitOrder()" style="background:green; color:white; padding:10px 20px; border:none; border-radius:5px;">
  Confirm Order
</button>
    <button onclick="closeOrderForm()" style="background:red; color:white; padding:10px 20px; border:none; border-radius:5px; margin-left:10px;">Cancel</button>
  </div>
</div>

<script src="wathchscript.js"></script>
</body>
</html>
[watchstyle.css](https://github.com/user-attachments/files/22169925/watchstyle.css)
/* BASE STYLES */
body, html {
  margin: 0;
  padding: 0;
  font-family: 'Segoe UI', sans-serif;
  overflow-x: hidden;
}

body {
  position: relative;
  overflow-x: hidden;
  z-index: 0;
}

/* HEADER */
header {
  position: fixed;
  top: 0;
  width: 100%;
  background: black;
  color: white;
  padding: 15px 40px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  z-index: 1000;
  box-sizing: border-box;
  overflow: hidden;

  /* ✅ Add this line */
  border-bottom: 2px solid gold;
}

.logo {
  display: flex;
  align-items: center;
  gap: 10px;
  font-size: 22px;
  font-weight: bold;
  color: gold;
}

.navbar-logo {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  object-fit: cover;
  border: 2px solid gold;[wathchscript.js](https://github.com/user-attachments/files/22169927/wathchscript.js)// Firebase Configuration
const firebaseConfig = {
  apiKey: "AIzaSyCZxhX_WjofN9anAS2hrp9eU3YgFQfyFyc",
  authDomain: "timeaura-watches.firebaseapp.com",
  databaseURL: "https://timeaura-watches-default-rtdb.firebaseio.com",
  projectId: "timeaura-watches",
  storageBucket: "timeaura-watches.appspot.com",
  messagingSenderId: "1051941165219",
  appId: "1:1051941165219:web:a76b6d8bcf8148592f0716"
};
firebase.initializeApp(firebaseConfig);
const database = firebase.database();



// Slider Function
let slideIndex = 0;
const slides = document.querySelectorAll(".slide");

function showSlides() {
  slides.forEach(slide => (slide.style.display = "none"));
  slideIndex = (slideIndex + 1) % slides.length;
  slides[slideIndex].style.display = "block";
  setTimeout(showSlides, 5000);
}
showSlides();

// All Watches Data
const allWatches = [
  { id: "M101", img: "watch.jpg", name: "Titan Edge", price: "₹2,999", category: "men" },
  { id: "M102", img: "watch1.jpg", name: "Fastrack Bold", price: "₹4,999", category: "men" },
  { id: "W201", img: "watch5.jpg", name: "Titan Raga", price: "₹3,299", category: "women" },
  { id: "W202", img: "watch6.jpg", name: "Sonata Chic", price: "₹2,199", category: "women" },
  { id: "C301", img: "watch7.jpg", name: "Couple Classic Set", price: "₹5,999", category: "couple" },
  { id: "C302", img: "watch4.jpg", name: "Elegant Gold Pair", price: "₹6,499", category: "couple" },
  { id: "M101", img: "watch.jpg", name: "Titan Edge", price: "₹2,999", category: "men" },
  { id: "M102", img: "watch1.jpg", name: "Fastrack Bold", price: "₹4,999", category: "men" },
  { id: "W201", img: "watch5.jpg", name: "Titan Raga", price: "₹3,299", category: "women" },
  { id: "W202", img: "watch6.jpg", name: "Sonata Chic", price: "₹2,199", category: "women" },
  { id: "C301", img: "watch7.jpg", name: "Couple Classic Set", price: "₹5,999", category: "couple" },
  { id: "C302", img: "watch4.jpg", name: "Elegant Gold Pair", price: "₹6,499", category: "couple" },
  { id: "M101", img: "watch.jpg", name: "Titan Edge", price: "₹2,999", category: "men" },
  { id: "M102", img: "watch1.jpg", name: "Fastrack Bold", price: "₹4,999", category: "men" },
  { id: "W201", img: "watch5.jpg", name: "Titan Raga", price: "₹3,299", category: "women" },
  { id: "W202", img: "watch6.jpg", name: "Sonata Chic", price: "₹2,199", category: "women" },
  { id: "C301", img: "watch7.jpg", name: "Couple Classic Set", price: "₹5,999", category: "couple" },
  { id: "C302", img: "watch4.jpg", name: "Elegant Gold Pair", price: "₹6,499", category: "couple" }
];

// Filter Watches
function filterWatches(category) {
  const container = document.getElementById("popular-container");
  const filtered = category === "all" ? allWatches : allWatches.filter(w => w.category === category);

  container.innerHTML = filtered.map(watch => `
    <div class="watch-card">
      <img src="${watch.img}" alt="${watch.name}">
      <h4>${watch.name}</h4>
      <p>${watch.price}</p>
      <p><strong>Model ID:</strong> ${watch.id}</p>
      <button class="buy-btn" onclick="addToCart('${watch.id}', '${watch.name}', '${watch.price}', '${watch.img}')">Add to Cart</button>
    </div>
  `).join('');
}

window.onload = () => filterWatches("all");

// Cart Functions
let cart = [];

function addToCart(id, name, price, img) {
  cart.push({ id, name, price, img });
  showToast(`${name} added to cart!`);
}

function openCart() {
  const cartContainer = document.getElementById("cart-container");
  const cartOverlay = document.getElementById("cart-overlay");
  cartContainer.innerHTML = "";

  if (cart.length === 0) {
    cartContainer.innerHTML = "<p>No items in cart.</p>";
  } else {
    cart.forEach((item, index) => {
      cartContainer.innerHTML += `
        <div class="watch-card">
          <img src="${item.img}" width="100">
          <h4>${item.name}</h4>
          <p>${item.price}</p>
          <button class="buy-btn" onclick="removeItem(${index})">Remove</button>
        </div>
      `;
    });
  }

  cartOverlay.style.display = "block";
  document.body.style.overflow = "hidden";
}

function closeCart() {
  document.getElementById("cart-overlay").style.display = "none";
  document.body.style.overflow = "auto";
}

function removeItem(index) {
  cart.splice(index, 1);
  openCart();
}

function placeOrder() {
  if (cart.length === 0) {
    alert("Your cart is empty!");
    return;
  }
  document.getElementById("order-form-popup").style.display = "flex";

  // Initialize map picker after a short delay to ensure container is visible
  setTimeout(initMapPicker, 100);
}

// submit orderr
// ✅ Updated Submit Order
function submitOrder() {
  console.log("🚀 Confirm Order button clicked!");  // Debug line

  const name = document.getElementById("customer-name").value.trim();
  const phone = document.getElementById("customer-phone").value.trim();
  const paymentMethod = document.getElementById("payment-method").value;
  const location = document.getElementById("customer-location").value.trim();

  if (!name || phone.length < 10 || !paymentMethod || paymentMethod === "Select" || !location) {
    alert("⚠️ Please fill all fields correctly!");
    return;
  }

  console.log("✅ Passed validation. Saving to Firebase...");

  let totalAmount = cart.reduce((sum, item) => {
    return sum + parseInt(item.price.replace(/[₹,]/g, ""));
  }, 0);

  const orderRef = database.ref("orders").child(name + "_" + phone);

  orderRef.set({
    customer: name,
    phone: phone,
    payment: paymentMethod,
    location: location,
    total: `₹${totalAmount}`
  }).then(() => {
    console.log("✅ Order saved to Firebase!");

    const itemsRef = orderRef.child("items");
    cart.forEach(item => {
      itemsRef.push(item);
    });

    alert("✅ Your order has been placed successfully!");
    cart = [];

    document.getElementById("customer-name").value = "";
    document.getElementById("customer-phone").value = "";
    document.getElementById("payment-method").value = "Select";
    document.getElementById("customer-location").value = "";

    closeCart();
    document.getElementById("order-form-popup").style.display = "none";
  }).catch(err => {
    console.error("❌ Firebase Error:", err);
    alert("❌ Failed to place order. Check console for details.");
  });
}


function closeOrderForm() {
  document.getElementById("order-form-popup").style.display = "none";
}


function viewOrders() {
  const phone = prompt("Enter your phone number to view your order:");
  if (!phone || phone.trim().length < 10) {
    alert("Please enter a valid phone number.");
    return;
  }

  const ordersRef = database.ref("orders");
  ordersRef.once("value", snapshot => {
    const orders = snapshot.val();
    let found = false;

    for (let name in orders) {
      if (orders[name].phone === phone) {
        found = true;
        const order = orders[name];
        let html = `
          <p><strong>Name:</strong> ${order.customer}</p>
          <p><strong>Phone:</strong> ${order.phone}</p>
          <p><strong>Payment:</strong> ${order.payment}</p>
          <p><strong>Total:</strong> ${order.total}</p>
          <h4>Ordered Items:</h4>
          <div id="order-items-container">
        `;

        if (order.items) {
          for (let key in order.items) {
            const item = order.items[key];
            html += `
              <div class="ordered-item">
                <img src="${item.img}" width="100"><br>
                <strong>${item.name}</strong><br>
                Price: ${item.price}<br>
                <button onclick="removeItemFromOrder('${name}', '${key}')" class="remove-btn">Remove Item</button>
              </div>
            `;
          }
        }

        html += `</div>
          <button onclick="cancelOrder('${name}')" style="background:black; color:white; padding:10px 20px; border:none; border-radius:5px; margin-top:10px;">
            Cancel Order
          </button>
        `;

        document.getElementById("order-container").innerHTML = html;
        document.getElementById("order-popup").style.display = "block";
        break;
      }
    }

    if (!found) {
      alert("❌ No order found with this phone number.");
    }
  });
}

function removeItemFromOrder(customerName, itemId) {
  if (confirm("Are you sure you want to remove this item from your order?")) {
    const itemRef = database.ref(`orders/${customerName}/items/${itemId}`);
    itemRef.remove()
      .then(() => {
        alert("✅ Item removed successfully.");
        viewOrders();
      })
      .catch(() => {
        alert("❌ Failed to remove the item. Please try again.");
      });
  }
}

function cancelOrder(name) {
  if (confirm("Are you sure you want to cancel this order?")) {
    database.ref("orders").child(name).remove()
      .then(() => {
        alert("✅ Your order has been cancelled.");
        closeOrderPopup();
      })
      .catch(() => {
        alert("❌ Failed to cancel the order. Try again.");
      });
  }
}

function closeOrderPopup() {
  document.getElementById("order-popup").style.display = "none";
}

function showToast(message) {
  const toast = document.getElementById("toast");
  toast.textContent = message;
  toast.style.display = "block";
  toast.style.animation = "fadeInOut 3s ease-in-out";

  setTimeout(() => {
    toast.style.display = "none";
    toast.style.animation = "";
  }, 3000);
}
document.querySelector(".menu-toggle").addEventListener("click", function () {
  document.querySelector("nav ul").classList.toggle("show");
});

// map location 
let map, marker, autocomplete;

function initMapPicker() {
  const defaultLocation = { lat: 13.0301, lng: 80.2212 }; // Velachery approx

  // Initialize the map
  map = new google.maps.Map(document.getElementById("map-picker"), {
    center: defaultLocation,
    zoom: 15
  });

  // Initialize the marker
  marker = new google.maps.Marker({
    map: map,
    draggable: true,
    position: defaultLocation
  });

  // Update input when marker is dragged
  marker.addListener("dragend", function () {
    const pos = marker.getPosition();
    document.getElementById("customer-location").value = `https://www.google.com/maps?q=${pos.lat().toFixed(5)},${pos.lng().toFixed(5)}`;
  });

  // Initialize autocomplete
  const input = document.getElementById("customer-location");
  autocomplete = new google.maps.places.Autocomplete(input);
  autocomplete.bindTo("bounds", map);

  autocomplete.addListener("place_changed", function () {
    const place = autocomplete.getPlace();
    if (!place.geometry) {
      alert("No details available for input: '" + place.name + "'");
      return;
    }

    // Move map & marker to the selected place
    if (place.geometry.viewport) {
      map.fitBounds(place.geometry.viewport);
    } else {
      map.setCenter(place.geometry.location);
      map.setZoom(17);
    }
    marker.setPosition(place.geometry.location);

    // Update input with Google Maps link
    const lat = place.geometry.location.lat();
    const lng = place.geometry.location.lng();
    input.value = `https://www.google.com/maps?q=${lat.toFixed(5)},${lng.toFixed(5)}`;
  });
}

// Call map picker when order form opens
function placeOrder() {
  if (cart.length === 0) {
    alert("Your cart is empty!");
    return;
  }
  document.getElementById("order-form-popup").style.display = "flex";

  // Delay to ensure map container is visible
  setTimeout(initMapPicker, 100);
}


// Firebase Auth + Database
// Firebase Auth + Database
const auth = firebase.auth();
const db = firebase.database();

// Show / Close Popup
function showLoginPopup() {
  document.getElementById("login-popup").style.display = "flex";
}

function closeLoginPopup() {
  document.getElementById("login-popup").style.display = "none";
}

// Sign Up
function signUp() {
  const email = document.getElementById("loginEmail").value;
  const password = document.getElementById("loginPassword").value;

  if (!email || !password) {
    alert("Please enter both email and password!");
    return;
  }

  auth.createUserWithEmailAndPassword(email, password)
    .then(userCredential => {
      alert("✅ Account created successfully!");
      saveCart(userCredential.user.uid); // Save empty cart initially
      closeLoginPopup();
    })
    .catch(error => {
      console.error("Sign Up Error:", error);
      alert("❌ Sign Up Error: " + error.message);
    });
}

function login() {
  const email = document.getElementById("loginEmail").value;
  const password = document.getElementById("loginPassword").value;

  if (!email || !password) {
    alert("Please enter both email and password!");
    return;
  }

  auth.signInWithEmailAndPassword(email, password)
    .then(userCredential => {
      alert("✅ Logged in successfully!");
      loadCart(userCredential.user.uid); // Load cart from DB
      closeLoginPopup();
    })
    .catch(error => {
      console.error("Login Error:", error);
      alert("❌ Login Error: " + error.message);
    });
}
// Guest Login (does NOT appear in Auth users)
function guestLogin() {
  const guestUID = "guest_" + Date.now();
  alert("Guest login successful! UID: " + guestUID);
  closeLoginPopup();
  loadCart(guestUID); // Load or create temporary cart
}



// SAVE CART TO DB
function saveCart(uid) {
  db.ref("users/" + uid + "/cart").set(cart)
    .then(() => console.log("Cart saved for UID:", uid))
    .catch(err => console.log("Error saving cart:", err));
}


// LOAD CART FROM DB
function loadCart(uid) {
  db.ref("users/" + uid + "/cart").once("value", snapshot => {
    if (snapshot.exists()) {
      cart = snapshot.val(); // load cart
      renderCart();
    } else {
      cart = [];
      renderCart();
    }
  });
}


// AUTH STATE CHANGE
// Show login popup automatically if no user is logged in
document.addEventListener("DOMContentLoaded", () => {
  firebase.auth().onAuthStateChanged(user => {
    if (!user) {
      // No user logged in, show login popup
      showLoginPopup();
    } else {
      // User is logged in, load their cart
      loadCart(user.uid);
    }
  });
});


// EMAIL VALIDATION FUNCTION
function validateEmail(email) {
  const re = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
  return re.test(email);
}

function showLoginPopup() {
  const popup = document.getElementById("login-popup");
  if (popup) {
    popup.style.display = "flex";
  } else {
    console.error("Login popup element not found!");
  }
}

function closeLoginPopup() {
  document.getElementById("login-popup").style.display = "none";
}


document.getElementById("showPassword").addEventListener("change", function () {
  const passwordInput = document.getElementById("loginPassword");
  if (this.checked) {
    passwordInput.type = "text";
  } else {
    passwordInput.type = "password";
  }
});


}

/* NAVIGATION */
nav ul {
  list-style: none;
  display: flex;
  gap: 25px;
  padding: 0;
  margin: 0;
}

nav ul li a {
  color: white;
  text-decoration: none;
  font-size: 16px;
  padding: 8px 12px;
  transition: all 0.3s ease;
  position: relative;
}

nav ul li a::after {
  content: '';
  position: absolute;
  width: 0%;
  height: 2px;
  background-color: gold;
  left: 0;
  bottom: 0;
  transition: width 0.3s;
}

nav ul li a:hover::after {
  width: 100%;
}

nav ul li a:hover {
  color: gold;
}

/* SLIDER */
.slider {
  margin-top: 70px;
  position: relative;
  height: 700px;
  overflow: hidden;
}

.slide {
  width: 100%;
  max-height: 700px;
  display: none;
  object-fit: cover;
}

/* HERO TEXT ON SLIDER */
.hero-text {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  text-align: center;
  color: gold;
  background: rgba(0, 0, 0, 0.5);
  padding: 30px;
  border-radius: 10px;
  z-index: 10;
}
.home-why-us {
  position: absolute;
  bottom: 30px;
  left: 50%;
  transform: translateX(-50%);
  width: 100%;
  display: flex;
  justify-content: center;
  z-index: 5;
}

.features {
  display: flex;
  justify-content: center;
  gap: 20px;
  flex-wrap: wrap;
  background: rgba(0,0,0,0.5);
  padding: 15px 20px;
  border-radius: 10px;
  max-width: 90%;
}

.feature-box {
  background: white;
  color: black;
  padding: 15px 25px;
  border-radius: 10px;
  font-weight: bold;
  font-size: 16px;
  box-shadow: 0 2px 6px rgba(0,0,0,0.2);
}


.hero-text h1 {
  font-size: 40px;
  margin-bottom: 10px;
}

.hero-text p {
  font-size: 18px;
  margin-bottom: 20px;
  color: #eee;
}

.hero-btn {
  margin-top: 15px;
  display: inline-block;
  padding: 12px 24px;
  background: gold;
  color: black;
  font-weight: bold;
  border-radius: 5px;
  text-decoration: none;
}

.hero-btn:hover {
  background: #e5c100;
}

/* POPULAR SECTION */
#popular-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 25px;
  margin-top: 20px;
  max-height: 600px;     /* set max height */
  overflow-y: auto;      /* enable vertical scroll */
  padding-right: 10px;   /* for scrollbar space */
  pointer-events: auto;  /*  important to allow mouse events */
}

#popular-section {
  padding: 50px 20px;
  background-color: #f9d342;
  position: relative;
  z-index: 1;
  overflow: visible !important;
  pointer-events: auto;  /*  important to allow mouse events */
}

.popular-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
  margin-bottom: 20px;
}

#popular-section h2 {
  font-size: 28px;
  margin: 0;
}

.filter-buttons button {
  padding: 10px 20px;
  margin-left: 10px;
  border: none;
  background: black;
  color: white;
  cursor: pointer;
  border-radius: 5px;
  transition: 0.3s;
}

.filter-buttons button:hover {
  background: #333;
}

/* WATCH CARD */
#popular-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 25px;
  margin-top: 20px;
  pointer-events: auto;  /* important to allow mouse events */
}

.watch-card {
  background: white;
  padding: 15px;
  border-radius: 10px;
  width: 220px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.15);
  text-align: center;
  transition: transform 0.2s ease;
}

.watch-card img {
  width: 100%;
  height: 200px;
  object-fit: contain;
}

.watch-card h4 {
  margin: 10px 0 5px;
}

.watch-card p {
  font-weight: bold;
  color: green;
}

.buy-btn {
  padding: 8px 15px;
  background: black;
  color: white;
  border: none;
  margin-top: 10px;
  border-radius: 5px;
  cursor: pointer;
}

.buy-btn:hover {
  background: #333;
}

.watch-card:hover {
  transform: scale(1.05);
  box-shadow: 0 0 15px gold;
}

/* WHY US SECTION */
#why-us {
  padding: 60px 20px;
  background: #f4f4f4;
  text-align: center;
}

#why-us h2 {
  font-size: 30px;
  margin-bottom: 30px;
}

.features {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  gap: 25px;
}

.feature-box {
  background: white;
  padding: 20px;
  border-radius: 10px;
  width: 220px;
  box-shadow: 0 0 10px rgba(0,0,0,0.1);
  font-size: 18px;
  font-weight: 500;
}

/* CONTACT SECTION */
#contact {
  background: #1a1a1a;
  color: white;
  padding: 60px 20px;
  text-align: center;
  position: relative;
  z-index: 1;
  overflow: visible !important;
   pointer-events: auto;  /*  important to allow mouse events */
}

.contact-container {
  max-width: 1000px;
  margin: auto;
}

.contact-logo {
  width: 80px;
  height: 80px;
  border-radius: 50%;
  object-fit: cover;
  border: 2px solid gold;
  margin-bottom: 10px;
}

.contact-header h2 {
  font-size: 32px;
  color: gold;
  margin: 10px 0 5px;
}

.contact-header p {
  font-size: 16px;
  color: #ccc;
}

.contact-details {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  margin: 40px 0;
  gap: 30px;
}

.contact-box h4 {
  font-size: 18px;
  color: gold;
  margin-bottom: 5px;
}

.contact-box p {
  margin: 0;
  font-size: 15px;
  color: #eee;
}

.map-container iframe {
  width: 100%;
  max-width: 1000px;
  border: none;
  border-radius: 10px;
}
/* view cart option*/
.view-cart-btn {
  position: fixed;
  top: 100px;
  right: 20px;
  z-index: 999;
  background: gold;
  color: black;
  border: none;
  padding: 10px 16px;
  border-radius: 50px;
  font-weight: bold;
  cursor: pointer;
}

.cart-modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0,0,0,0.6);
  display: none;
  justify-content: center;
  align-items: center;
  z-index: 1000;
}

.cart-content {
  background: white;
  padding: 30px;
  width: 90%;
  max-width: 500px;
  border-radius: 10px;
  overflow-y: auto;
  max-height: 80vh;
}

.cart-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 15px;
  border-bottom: 1px solid #ddd;
  padding-bottom: 10px;
}
.cart-item img {
  width: 60px;
  height: 60px;
  object-fit: cover;
}
/* scrolling slogan in head section*/

.scroll-slogan {
  position: relative;
  top: 70px; /* Pushes it below fixed header */
  width: 100%;
  background-color: black;
  color: gold;
  overflow: hidden;
  white-space: nowrap;
  border-top: 2px solid gold;
  border-bottom: 2px solid gold;
  padding: 8px 0;
  font-size: 16px;
  font-weight: bold;
  z-index: 999;
}

.scroll-slogan p {
  display: inline-block;
  padding-left: 100%;
  animation: scroll-left 15s linear infinite;
  white-space: nowrap;
}

@keyframes scroll-left {
  0% {
    transform: translateX(0%);
  }
  100% {
    transform: translateX(-100%);
  }
}
/*curser flow section*/

.trail-star {
  position: fixed;
  width: 6px;
  height: 6px;
  background: rgb(245, 55, 8);
  border-radius: 50%;
  box-shadow: 0 0 10px gold, 0 0 20px gold;
  pointer-events: none;
  animation: tail-fade 0.8s ease-out forwards;
  z-index: 9999;
}

@keyframes tail-fade {
  0% {
    opacity: 1;
    transform: scale(1) translateY(0);
  }
  100% {
    opacity: 0;
    transform: scale(2.5) translateY(-20px);
  }
}

/* pop up of add cart*/
@keyframes fadeInOut {
  0% { opacity: 0; bottom: 10px; }
  10% { opacity: 1; bottom: 30px; }
  90% { opacity: 1; bottom: 30px; }
  100% { opacity: 0; bottom: 10px; }
}
/* order popup*/
#order-form-popup {
  backdrop-filter: blur(4px);
}
/* remove button on view order*/
.order-items-wrapper {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
  justify-content: center;
  margin-top: 20px;
}

.order-card {
  border: 1px solid #ddd;
  padding: 10px;
  width: 180px;
  text-align: center;
  border-radius: 8px;
  background: white;
  box-shadow: 0 0 10px rgba(0,0,0,0.1);
}

.order-card img {
  width: 100%;
  height: 120px;
  object-fit: contain;
  margin-bottom: 10px;
}

.remove-btn {
  background: red;
  color: white;
  padding: 6px 10px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  margin-top: 5px;
}

/* ORDERED ITEMS WRAPPER */
/* ORDERED ITEM CARD STYLE */
#order-items-container {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
  margin-top: 15px;
  justify-content: center;
}

.ordered-item {
  background: white;
  border: 2px solid gold;
  border-radius: 10px;
  padding: 15px;
  width: 200px;
  text-align: center;
  box-shadow: 0 0 10px rgba(0,0,0,0.1);
}

.ordered-item img {
  width: 100%;
  height: 120px;
  object-fit: contain;
  margin-bottom: 10px;
}

.ordered-item strong {
  display: block;
  margin: 5px 0;
  color: black;
}

.remove-btn {
  background: red;
  color: white;
  border: none;
  padding: 8px 12px;
  border-radius: 5px;
  cursor: pointer;
  font-weight: bold;
  margin-top: 8px;
  transition: background 0.3s ease;
}

.remove-btn:hover {
  background: darkred;
}

/* ===== MOBILE FIXES ===== */
@media (max-width: 768px) {

  /* Header */
  header {
    flex-direction: column;
    align-items: flex-start;
    padding: 10px 20px;
  }

  nav ul {
    flex-direction: column;
    gap: 10px;
    width: 100%;
    display: none; /* hidden until menu icon clicked */
    background: black;
    padding: 10px 0;
  }

  nav ul.show {
    display: flex;
  }

  nav ul li {
    width: 100%;
    text-align: center;
  }

  nav ul li a {
    display: block;
    width: 100%;
  }

  /* Mobile Menu Icon */
  .menu-toggle {
    display: block;
    cursor: pointer;
    color: gold;
    font-size: 22px;
    margin-top: 5px;
  }

  /* Slider */
  .slider {
    height: 300px;
    margin-top: 60px;
  }

  .slide {
    max-height: 300px;
    object-fit: cover;
  }

  .hero-text {
    padding: 15px;
    font-size: 14px;
  }

  .hero-text h1 {
    font-size: 22px;
  }

  .hero-text p {
    font-size: 14px;
  }

  /* Features under slider */
  .home-why-us {
    bottom: 10px;
    padding: 5px;
  }
  .feature-box {
    font-size: 14px;
    padding: 10px;
  }

  /* Popular section cards */
  .watch-card {
    width: 45%;
    padding: 10px;
  }
  .watch-card img {
    height: 150px;
  }

  /* Why us cards */
  .feature-box {
    width: 100%;
  }

  /* Contact details stack */
  .contact-details {
    flex-direction: column;
    gap: 15px;
  }

  /* Cart Button */
  .view-cart-btn {
    top: 70px;
    right: 10px;
    padding: 8px 12px;
    font-size: 14px;
  }
}

/* ===== VERY SMALL PHONES ===== */
@media (max-width: 480px) {
  .watch-card {
    width: 100%;
  }
  .hero-text h1 {
    font-size: 18px;
  }
  .hero-text p {
    font-size: 12px;
  }
}
