<!DOCTYPE html>
<html lang="bn">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Your Name</title>

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

/* Profile Picture */
.profile img {
  width: 100px;
  height: 100px;
  border-radius: 50%;
  border: 2px solid #000;
  object-fit: cover;
  margin-bottom: 12px;
  box-shadow: 0 0 0 4px #fff, 0 0 14px rgba(0,0,0,0.35);
}

/* Name */
.name {
  font-size: 18px;
  font-weight: 700;
  margin-bottom: 4px;
}

/* Title */
.title {
  font-size: 12px;
  color: #555;
  margin-bottom: 14px;
}

/* Buttons */
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

/* Footer */
.footer {
  margin-top: 16px;
  font-size: 12px;
  color: #555;
  text-align: center;
}
</style>
</head>

<body>

<div class="wrapper">
  <div class="container">

    <!-- Profile Picture -->
    <div class="profile">
      <img src="Your_Profile_Picture_Link" alt="Profile Picture">
    </div>

    <!-- Name & Title -->
    <div class="name">Your_Name</div>
    <div class="title">Your_Title</div>

    <!-- Buttons -->

    <!-- Facebook -->
    <a class="btn" href="https://www.facebook.com/your_username">
      <img src="https://cdn.simpleicons.org/facebook/000000" alt="Facebook Logo">
      Facebook
    </a>

    <!-- New Button: Facebook Page -->
    <a class="btn" href="https://www.facebook.com/your_username">
      <img src="https://cdn.simpleicons.org/facebook/000000" alt="Facebook Logo">
      Facebook Page
    </a>

    <!-- Instagram -->
    <a class="btn" href="https://www.instagram.com/your_username">
      <img src="https://cdn.simpleicons.org/instagram/000000" alt="Instagram Logo">
      Instagram
    </a>

    <!-- WhatsApp -->
    <a class="btn" href="#">
      <img src="https://cdn.simpleicons.org/whatsapp/000000" alt="WhatsApp Logo">
      WhatsApp
    </a>

    <!-- TikTok -->
    <a class="btn" href="https://www.tiktok.com/@your_username" target="_blank">
      <img src="https://i.postimg.cc/fRKJCkcx/images-(2).png" alt="TikTok Logo">
      TikTok
    </a>

    <!-- Call Me -->
    <a class="btn" href="tel:01XXXXXXXXX">
      <img src="https://i.postimg.cc/C59NrRY3/phone-logo-png-seeklogo-248712.png" alt="Phone Logo">
      Call Me
    </a>

    <!-- About Me -->
    <a class="btn" href="#">
      <img src="https://cdn.simpleicons.org/aboutdotme/000000" alt="About Logo">
      About Me
    </a>

    <!-- My Website -->
    <a class="btn" href="#">
      <img src="https://i.postimg.cc/TYwJMMPQ/images-(1).png" alt="Website Logo">
      My Website
    </a>

  </div>

  <!-- Footer -->
  <div class="footer">
    Copyright © 2026 MADE BY <br> "Your_Name". <br> All Rights Reserved.
  </div>
</div>

</body>
</html>