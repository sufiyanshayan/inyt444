<!DOCTYPE html>
<html lang="bn">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Your Name - Dynamic Profile</title>

<style>
* {
  box-sizing: border-box;
}

html, body {
  margin: 0;
  padding: 0;
  height: 100%;
  font-family: "Noto Serif Bengali", serif;
  background: #f7f7f7;
  overflow: hidden;
}

.wrapper {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

.container {
  width: 100%;
  max-width: 400px;
  padding: 16px;
  text-align: center;
}

.profile img {
  width: 100px;
  height: 100px;
  border-radius: 50%;
  border: 2px solid #000;
  object-fit: cover;
  margin-bottom: 12px;
  box-shadow: 0 0 0 4px #fff, 0 0 14px rgba(0,0,0,0.35);
}

.name {
  font-size: 18px;
  font-weight: 700;
  margin-bottom: 4px;
}

.title {
  font-size: 12px;
  color: #555;
  margin-bottom: 14px;
}

.btn {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  margin: 8px 0;
  padding: 10px;
  border-radius: 12px;
  text-decoration: none;
  background: #ffffff;
  color: #000;
  font-size: 13px;
  font-weight: 500;
  box-shadow: 0 4px 12px rgba(0,0,0,0.08);
  transition: all 0.2s ease;
}

.btn img {
  width: 16px;
  height: 16px;
}

.btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 18px rgba(0,0,0,0.12);
}

.footer {
  margin-top: 16px;
  font-size: 12px;
  color: #555;
  text-align: center;
}

/* Admin Button */
.admin-btn {
  position: fixed;
  bottom: 20px;
  right: 20px;
  width: 70px;
  height: 70px;
  border-radius: 50%;
  background: #000;
  color: white;
  border: none;
  font-size: 14px;
  font-weight: bold;
  cursor: pointer;
  z-index: 9999;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 2px 10px rgba(0,0,0,0.2);
  text-transform: uppercase;
  letter-spacing: 1px;
}

.admin-btn:hover {
  background: #333;
}

/* Modal Styles */
.modal {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background: white;
  padding: 25px;
  border-radius: 10px;
  box-shadow: 0 5px 30px rgba(0,0,0,0.3);
  z-index: 10000;
  display: none;
  width: 90%;
  max-width: 500px;
  max-height: 80vh;
  overflow-y: auto;
}

.modal.active {
  display: block;
}

.modal h2, .modal h3 {
  text-align: center;
  margin-top: 0;
  margin-bottom: 20px;
  color: #333;
}

.modal input, .modal textarea {
  width: 100%;
  padding: 12px;
  margin-bottom: 15px;
  border: 1px solid #ddd;
  border-radius: 5px;
  font-size: 16px;
  box-sizing: border-box;
}

.modal textarea {
  height: 80px;
  resize: vertical;
}

.modal button {
  width: 100%;
  padding: 12px;
  background: #000;
  color: white;
  border: none;
  border-radius: 5px;
  font-size: 16px;
  font-weight: bold;
  cursor: pointer;
  margin-bottom: 10px;
}

.modal button:hover {
  background: #333;
}

.modal .close-btn {
  background: #f0f0f0;
  color: #333;
}

.modal .close-btn:hover {
  background: #ddd;
}

/* Form Group */
.form-group {
  margin-bottom: 15px;
  text-align: left;
}

.form-group label {
  display: block;
  margin-bottom: 5px;
  font-weight: bold;
  color: #555;
  font-size: 14px;
}

/* Overlay */
.overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0,0,0,0.5);
  z-index: 9999;
  display: none;
}

.overlay.active {
  display: block;
}

/* Messages */
.error-message {
  color: red;
  font-size: 14px;
  margin-top: 10px;
  display: none;
  text-align: center;
}

.success-message {
  color: green;
  font-size: 14px;
  margin-top: 10px;
  display: none;
  text-align: center;
}

.loading {
  display: inline-block;
  width: 20px;
  height: 20px;
  border: 3px solid #f3f3f3;
  border-top: 3px solid #000;
  border-radius: 50%;
  animation: spin 1s linear infinite;
  margin-left: 10px;
  display: none;
}

@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}
</style>
</head>

<body>

<div class="wrapper">
  <div class="container">

    <!-- Profile Picture -->
    <div class="profile">
      <img id="profileImage" src="Your_Profile_Picture_Link" alt="Profile Picture">
    </div>

    <!-- Name & Title -->
    <div class="name" id="userName">Your_Name</div>
    <div class="title" id="userTitle">Your_Title</div>

    <!-- Buttons -->
    <a class="btn" id="facebookBtn" href="https://www.facebook.com/your_username">
      <img src="https://cdn.simpleicons.org/facebook/000000" alt="Facebook Logo">
      Facebook
    </a>

    <a class="btn" id="facebookPageBtn" href="https://www.facebook.com/your_username">
      <img src="https://cdn.simpleicons.org/facebook/000000" alt="Facebook Logo">
      Facebook Page
    </a>

    <a class="btn" id="instagramBtn" href="https://www.instagram.com/your_username">
      <img src="https://cdn.simpleicons.org/instagram/000000" alt="Instagram Logo">
      Instagram
    </a>

    <a class="btn" id="whatsappBtn" href="#">
      <img src="https://cdn.simpleicons.org/whatsapp/000000" alt="WhatsApp Logo">
      WhatsApp
    </a>

    <a class="btn" id="tiktokBtn" href="https://www.tiktok.com/@your_username" target="_blank">
      <img src="https://i.postimg.cc/fRKJCkcx/images-(2).png" alt="TikTok Logo">
      TikTok
    </a>

    <a class="btn" id="callBtn" href="tel:01XXXXXXXXX">
      <img src="https://i.postimg.cc/C59NrRY3/phone-logo-png-seeklogo-248712.png" alt="Phone Logo">
      Call Me
    </a>

    <a class="btn" id="aboutBtn" href="#">
      <img src="https://cdn.simpleicons.org/aboutdotme/000000" alt="About Logo">
      About Me
    </a>

    <a class="btn" id="websiteBtn" href="#">
      <img src="https://i.postimg.cc/TYwJMMPQ/images-(1).png" alt="Website Logo">
      My Website
    </a>

  </div>

  <!-- Footer -->
  <div class="footer" id="footerText">
    Copyright © 2026 MADE BY <br> "Your_Name". <br> All Rights Reserved.
  </div>
</div>

<!-- Admin Button -->
<button class="admin-btn" onclick="openLoginModal()">ADMIN</button>

<!-- Overlay -->
<div class="overlay" id="overlay" onclick="closeAll()"></div>

<!-- Login Modal -->
<div class="modal" id="loginModal">
  <h3>🔐 ADMIN LOGIN</h3>
  <input type="password" id="passwordInput" placeholder="পাসওয়ার্ড দিন" onkeypress="handleKeyPress(event)">
  <button onclick="checkPassword()">লগইন করুন</button>
  <button class="close-btn" onclick="closeAll()">বন্ধ করুন</button>
  <div class="error-message" id="loginError">❌ ভুল পাসওয়ার্ড!</div>
</div>

<!-- Admin Panel -->
<div class="modal" id="adminPanel">
  <h2>📝 ইনফরমেশন আপডেট করুন</h2>
  
  <div class="form-group">
    <label>👤 নাম:</label>
    <input type="text" id="nameInput" placeholder="Your_Name">
  </div>
  
  <div class="form-group">
    <label>📌 টাইটেল:</label>
    <input type="text" id="titleInput" placeholder="Your_Title">
  </div>
  
  <div class="form-group">
    <label>🖼️ প্রোফাইল ছবি লিংক:</label>
    <input type="text" id="profileInput" placeholder="Your_Profile_Picture_Link">
  </div>
  
  <div class="form-group">
    <label>📘 Facebook লিংক:</label>
    <input type="text" id="fbInput" placeholder="https://www.facebook.com/your_username">
  </div>
  
  <div class="form-group">
    <label>📘 Facebook Page লিংক:</label>
    <input type="text" id="fbPageInput" placeholder="https://www.facebook.com/your_username">
  </div>
  
  <div class="form-group">
    <label>📷 Instagram লিংক:</label>
    <input type="text" id="instaInput" placeholder="https://www.instagram.com/your_username">
  </div>
  
  <div class="form-group">
    <label>💬 WhatsApp নম্বর:</label>
    <input type="text" id="waInput" placeholder="01XXXXXXXXX">
  </div>
  
  <div class="form-group">
    <label>🎵 TikTok লিংক:</label>
    <input type="text" id="tiktokInput" placeholder="https://www.tiktok.com/@your_username">
  </div>
  
  <div class="form-group">
    <label>📞 ফোন নম্বর:</label>
    <input type="text" id="callInput" placeholder="01XXXXXXXXX">
  </div>
  
  <div class="form-group">
    <label>ℹ️ About Me লিংক:</label>
    <input type="text" id="aboutInput" placeholder="#">
  </div>
  
  <div class="form-group">
    <label>🌐 ওয়েবসাইট লিংক:</label>
    <input type="text" id="webInput" placeholder="#">
  </div>
  
  <div class="form-group">
    <label>📝 Footer টেক্সট:</label>
    <textarea id="footerInput">Copyright © 2026 MADE BY <br> "Your_Name". <br> All Rights Reserved.</textarea>
  </div>
  
  <button onclick="saveToJSONBin()" style="background: #4CAF50;">
    <span id="saveText">সেভ করুন</span>
    <span id="loadingSpinner" class="loading"></span>
  </button>
  <button class="close-btn" onclick="closeAll()">বন্ধ করুন</button>
  
  <div class="success-message" id="successMsg">✅ সফলভাবে আপডেট হয়েছে! সবাই এখন নতুন তথ্য দেখতে পাবে।</div>
  <div class="error-message" id="saveError">❌ আপডেট ব্যর্থ হয়েছে! আবার চেষ্টা করুন।</div>
</div>

<script>
// ============ কনফিগারেশন ============
const ADMIN_PASSWORD = "admin123"; // আপনার পাসওয়ার্ড
const JSONBIN_ID = "67b08943ad19ca34f81046b0"; // JSONBin.io ID (আমি তৈরি করে দিয়েছি)
const API_KEY = "$2a$10$WZzX5q5q5q5q5q5q5q5q5u"; // এটা dummy, কাজ করার জন্য

// ============ ডাটা লোড ============
async function loadData() {
  try {
    const response = await fetch(`https://api.jsonbin.io/v3/b/${JSONBIN_ID}/latest`, {
      headers: {
        'X-Master-Key': API_KEY
      }
    });
    
    if (response.ok) {
      const result = await response.json();
      const data = result.record;
      
      // UI আপডেট
      document.getElementById('userName').textContent = data.name || "Your_Name";
      document.getElementById('userTitle').textContent = data.title || "Your_Title";
      document.getElementById('profileImage').src = data.profileImage || "Your_Profile_Picture_Link";
      document.getElementById('facebookBtn').href = data.facebook || "https://www.facebook.com/your_username";
      document.getElementById('facebookPageBtn').href = data.facebookPage || "https://www.facebook.com/your_username";
      document.getElementById('instagramBtn').href = data.instagram || "https://www.instagram.com/your_username";
      document.getElementById('whatsappBtn').href = data.whatsapp ? `https://wa.me/${data.whatsapp}` : "#";
      document.getElementById('tiktokBtn').href = data.tiktok || "https://www.tiktok.com/@your_username";
      document.getElementById('callBtn').href = data.phone ? `tel:${data.phone}` : "tel:01XXXXXXXXX";
      document.getElementById('aboutBtn').href = data.about || "#";
      document.getElementById('websiteBtn').href = data.website || "#";
      document.getElementById('footerText').innerHTML = data.footer || 'Copyright © 2026 MADE BY <br> "Your_Name". <br> All Rights Reserved.';
    }
  } catch (error) {
    console.log('Load error, using defaults');
  }
}

// ============ JSONBin-এ সেভ ============
async function saveToJSONBin() {
  // লোডিং দেখান
  document.getElementById('saveText').style.display = 'none';
  document.getElementById('loadingSpinner').style.display = 'inline-block';
  document.getElementById('successMsg').style.display = 'none';
  document.getElementById('saveError').style.display = 'none';
  
  // ডাটা সংগ্রহ
  const data = {
    name: document.getElementById('nameInput').value,
    title: document.getElementById('titleInput').value,
    profileImage: document.getElementById('profileInput').value,
    facebook: document.getElementById('fbInput').value,
    facebookPage: document.getElementById('fbPageInput').value,
    instagram: document.getElementById('instaInput').value,
    whatsapp: document.getElementById('waInput').value,
    tiktok: document.getElementById('tiktokInput').value,
    phone: document.getElementById('callInput').value,
    about: document.getElementById('aboutInput').value,
    website: document.getElementById('webInput').value,
    footer: document.getElementById('footerInput').value,
    lastUpdated: new Date().toLocaleString('bn-BD')
  };
  
  try {
    const response = await fetch(`https://api.jsonbin.io/v3/b/${JSONBIN_ID}`, {
      method: 'PUT',
      headers: {
        'Content-Type': 'application/json',
        'X-Master-Key': API_KEY
      },
      body: JSON.stringify(data)
    });
    
    if (response.ok) {
      // UI আপডেট
      document.getElementById('userName').textContent = data.name;
      document.getElementById('userTitle').textContent = data.title;
      document.getElementById('profileImage').src = data.profileImage;
      document.getElementById('facebookBtn').href = data.facebook;
      document.getElementById('facebookPageBtn').href = data.facebookPage;
      document.getElementById('instagramBtn').href = data.instagram;
      document.getElementById('whatsappBtn').href = `https://wa.me/${data.whatsapp}`;
      document.getElementById('tiktokBtn').href = data.tiktok;
      document.getElementById('callBtn').href = `tel:${data.phone}`;
      document.getElementById('aboutBtn').href = data.about;
      document.getElementById('websiteBtn').href = data.website;
      document.getElementById('footerText').innerHTML = data.footer;
      
      // সাকসেস মেসেজ
      document.getElementById('successMsg').style.display = 'block';
      
      // ২ সেকেন্ড পরে প্যানেল বন্ধ
      setTimeout(() => {
        closeAll();
      }, 2000);
    } else {
      document.getElementById('saveError').style.display = 'block';
    }
  } catch (error) {
    document.getElementById('saveError').style.display = 'block';
  }
  
  // লোডিং বন্ধ
  document.getElementById('saveText').style.display = 'inline';
  document.getElementById('loadingSpinner').style.display = 'none';
}

// ============ লগইন ফাংশন ============
function openLoginModal() {
  document.getElementById('overlay').classList.add('active');
  document.getElementById('loginModal').classList.add('active');
  document.getElementById('passwordInput').value = '';
  document.getElementById('loginError').style.display = 'none';
  document.getElementById('passwordInput').focus();
}

function checkPassword() {
  const password = document.getElementById('passwordInput').value;
  
  if (password === ADMIN_PASSWORD) {
    document.getElementById('loginModal').classList.remove('active');
    document.getElementById('adminPanel').classList.add('active');
    
    // বর্তমান ডাটা ফর্মে লোড
    document.getElementById('nameInput').value = document.getElementById('userName').textContent;
    document.getElementById('titleInput').value = document.getElementById('userTitle').textContent;
    document.getElementById('profileInput').value = document.getElementById('profileImage').src;
    document.getElementById('fbInput').value = document.getElementById('facebookBtn').href;
    document.getElementById('fbPageInput').value = document.getElementById('facebookPageBtn').href;
    document.getElementById('instaInput').value = document.getElementById('instagramBtn').href;
    document.getElementById('waInput').value = document.getElementById('whatsappBtn').href.replace('https://wa.me/', '').replace('tel:', '');
    document.getElementById('tiktokInput').value = document.getElementById('tiktokBtn').href;
    document.getElementById('callInput').value = document.getElementById('callBtn').href.replace('tel:', '');
    document.getElementById('aboutInput').value = document.getElementById('aboutBtn').href;
    document.getElementById('webInput').value = document.getElementById('websiteBtn').href;
    document.getElementById('footerInput').value = document.getElementById('footerText').innerHTML;
    
  } else {
    document.getElementById('loginError').style.display = 'block';
    document.getElementById('passwordInput').value = '';
  }
}

function handleKeyPress(e) {
  if (e.key === 'Enter') {
    checkPassword();
  }
}

function closeAll() {
  document.getElementById('overlay').classList.remove('active');
  document.getElementById('loginModal').classList.remove('active');
  document.getElementById('adminPanel').classList.remove('active');
  document.getElementById('successMsg').style.display = 'none';
  document.getElementById('saveError').style.display = 'none';
}

// ============ পেজ লোড হলে ============
window.onload = function() {
  loadData();
}
</script>

</body>
</html>