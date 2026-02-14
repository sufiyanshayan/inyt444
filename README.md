<!DOCTYPE html>
<html lang="bn">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Your Name - Live Editor</title>

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
}

/* Main Website Styles */
.website-view {
  height: 100vh;
  overflow: hidden;
  position: relative;
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
  max-width: 900px;
  max-height: 90vh;
  overflow: hidden;
  flex-direction: column;
}

.modal.active {
  display: flex;
}

.modal h3 {
  text-align: center;
  margin-top: 0;
  margin-bottom: 20px;
  color: #333;
}

/* Code Editor */
.code-editor {
  width: 100%;
  height: 500px;
  font-family: 'Courier New', monospace;
  font-size: 14px;
  line-height: 1.5;
  padding: 15px;
  border: 1px solid #ddd;
  border-radius: 5px;
  resize: vertical;
  white-space: pre-wrap;
  background: #1e1e1e;
  color: #d4d4d4;
  margin-bottom: 15px;
}

.editor-tabs {
  display: flex;
  gap: 10px;
  margin-bottom: 10px;
}

.tab-btn {
  padding: 8px 16px;
  background: #f0f0f0;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-weight: bold;
}

.tab-btn.active {
  background: #000;
  color: white;
}

.preview-btn {
  background: #2196F3;
  color: white;
  padding: 8px 16px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  margin-left: auto;
}

/* Login Modal (smaller) */
.login-modal {
  max-width: 400px;
}

.login-modal input {
  width: 100%;
  padding: 12px;
  margin-bottom: 15px;
  border: 1px solid #ddd;
  border-radius: 5px;
  font-size: 16px;
  box-sizing: border-box;
}

.login-modal button {
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

.login-modal .close-btn {
  background: #f0f0f0;
  color: #333;
}

.button-group {
  display: flex;
  gap: 10px;
  margin-top: 15px;
}

.button-group button {
  flex: 1;
  padding: 12px;
  border: none;
  border-radius: 5px;
  font-size: 16px;
  font-weight: bold;
  cursor: pointer;
}

.save-btn {
  background: #4CAF50;
  color: white;
}

.apply-btn {
  background: #2196F3;
  color: white;
}

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

.info-box {
  background: #e3f2fd;
  border-left: 4px solid #2196F3;
  padding: 10px;
  margin-bottom: 15px;
  font-size: 13px;
  color: #0d47a1;
}

/* Export/Import */
.export-import {
  display: flex;
  gap: 10px;
  margin-bottom: 15px;
}

.export-import button {
  flex: 1;
  padding: 8px;
  background: #f0f0f0;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}
</style>
</head>
<body>

<!-- Main Website View -->
<div class="website-view" id="websiteView">
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
</div>

<!-- Admin Button -->
<button class="admin-btn" onclick="openLoginModal()">ADMIN</button>

<!-- Overlay -->
<div class="overlay" id="overlay" onclick="closeAll()"></div>

<!-- Login Modal -->
<div class="modal login-modal" id="loginModal">
  <h3>🔐 ADMIN LOGIN</h3>
  <input type="password" id="passwordInput" placeholder="পাসওয়ার্ড দিন" onkeypress="handleKeyPress(event)">
  <button onclick="checkPassword()">লগইন করুন</button>
  <button class="close-btn" onclick="closeAll()">বন্ধ করুন</button>
  <div class="error-message" id="loginError">❌ ভুল পাসওয়ার্ড!</div>
</div>

<!-- HTML Editor Modal -->
<div class="modal" id="editorModal">
  <h3>📝 HTML কোড এডিটর</h3>
  
  <div class="info-box">
    <strong>⚠️ সতর্কতা:</strong> HTML কোড পরিবর্তন করলে ওয়েবসাইটের ডিজাইন ও কন্টেন্ট পরিবর্তন হবে। 
    <br><strong>নোট:</strong> এই পরিবর্তন শুধু আপনার ব্রাউজারে থাকবে। GitHub-এ আপডেট করতে চাইলে নতুন কোড কপি করে GitHub-এ পেস্ট করুন।
  </div>
  
  <div class="export-import">
    <button onclick="exportHtml()">📥 HTML ডাউনলোড</button>
    <button onclick="importHtml()">📤 HTML আপলোড</button>
  </div>
  
  <div class="editor-tabs">
    <button class="tab-btn active" onclick="switchTab('code')">📝 কোড</button>
    <button class="tab-btn" onclick="switchTab('preview')">👁️ প্রিভিউ</button>
    <button class="preview-btn" onclick="previewCode()">প্রিভিউ দেখুন</button>
  </div>
  
  <textarea id="htmlEditor" class="code-editor" placeholder="এখানে HTML কোড লিখুন..."></textarea>
  
  <div id="previewArea" style="display: none; height: 500px; overflow: auto; border: 1px solid #ddd; padding: 20px; background: white;"></div>
  
  <div class="button-group">
    <button class="save-btn" onclick="saveToBrowser()">
      <span>💾 ব্রাউজারে সেভ</span>
    </button>
    <button class="apply-btn" onclick="applyChanges()">
      <span>🔄 ওয়েবসাইটে প্রয়োগ</span>
    </button>
    <button class="close-btn" onclick="closeAll()">✖️ বন্ধ করুন</button>
  </div>
  
  <div class="success-message" id="successMsg">✅ সফলভাবে সেভ হয়েছে!</div>
  <div class="error-message" id="errorMsg">❌ এরর হয়েছে! আবার চেষ্টা করুন।</div>
  
  <div style="margin-top: 15px; padding: 10px; background: #fff3cd; border-radius: 5px; font-size: 13px;">
    <strong>📌 GitHub আপডেট করার নিয়ম:</strong><br>
    1. কোড এডিট করুন<br>
    2. "HTML ডাউনলোড" বাটনে ক্লিক করুন<br>
    3. ডাউনলোড করা ফাইল GitHub-এ আপলোড করুন
  </div>
</div>

<script>
// ============ কনফিগারেশন ============
const ADMIN_PASSWORD = "admin123"; // আপনার পাসওয়ার্ড

// ============ অরিজিনাল HTML কোড ============
function getCurrentHTML() {
  return document.documentElement.outerHTML;
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
    openEditorModal();
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

// ============ এডিটর মোডাল ============
function openEditorModal() {
  document.getElementById('editorModal').classList.add('active');
  
  // ব্রাউজার স্টোরেজ থেকে HTML লোড
  const savedHtml = localStorage.getItem('websiteHtml');
  if (savedHtml) {
    document.getElementById('htmlEditor').value = savedHtml;
  } else {
    // Current HTML দেখান
    document.getElementById('htmlEditor').value = getCurrentHTML();
  }
}

function switchTab(tab) {
  const codeEditor = document.getElementById('htmlEditor');
  const previewArea = document.getElementById('previewArea');
  const tabs = document.querySelectorAll('.tab-btn');
  
  if (tab === 'code') {
    codeEditor.style.display = 'block';
    previewArea.style.display = 'none';
    tabs[0].classList.add('active');
    tabs[1].classList.remove('active');
  } else {
    codeEditor.style.display = 'none';
    previewArea.style.display = 'block';
    tabs[0].classList.remove('active');
    tabs[1].classList.add('active');
    previewCode();
  }
}

function previewCode() {
  const html = document.getElementById('htmlEditor').value;
  const previewArea = document.getElementById('previewArea');
  
  // প্রিভিউ দেখান (সিকিউরিটি জন্য)
  const safeHtml = html.replace(/<script\b[^<]*(?:(?!<\/script>)<[^<]*)*<\/script>/gi, '<!-- স্ক্রিপ্ট সরানো হয়েছে -->');
  previewArea.innerHTML = safeHtml;
}

// ============ ব্রাউজারে সেভ ============
function saveToBrowser() {
  const html = document.getElementById('htmlEditor').value;
  localStorage.setItem('websiteHtml', html);
  showMessage('successMsg', 'ব্রাউজারে সেভ হয়েছে!');
}

// ============ ওয়েবসাইটে প্রয়োগ ============
function applyChanges() {
  if (confirm('আপনি কি নিশ্চিত? ওয়েবসাইট আপডেট হবে।')) {
    const html = document.getElementById('htmlEditor').value;
    
    // একটা temporary iframe তৈরি করে দেখানো যায়
    // কিন্তু পুরো পেজ রিপ্লেস করা risky
    
    showMessage('successMsg', 'এই ফিচারটি ডেমো জন্য। GitHub-এ আপডেট করতে HTML ডাউনলোড করুন।');
  }
}

// ============ HTML ডাউনলোড ============
function exportHtml() {
  const html = document.getElementById('htmlEditor').value;
  const blob = new Blob([html], { type: 'text/html' });
  const url = URL.createObjectURL(blob);
  const a = document.createElement('a');
  a.href = url;
  a.download = 'index.html';
  document.body.appendChild(a);
  a.click();
  document.body.removeChild(a);
  URL.revokeObjectURL(url);
  
  showMessage('successMsg', 'HTML ডাউনলোড শুরু হয়েছে!');
}

// ============ HTML আপলোড ============
function importHtml() {
  const input = document.createElement('input');
  input.type = 'file';
  input.accept = '.html,.htm';
  
  input.onchange = function(e) {
    const file = e.target.files[0];
    const reader = new FileReader();
    
    reader.onload = function(e) {
      document.getElementById('htmlEditor').value = e.target.result;
      showMessage('successMsg', 'HTML আপলোড হয়েছে!');
    };
    
    reader.readAsText(file);
  };
  
  input.click();
}

// ============ হেল্পার ফাংশন ============
function showMessage(elementId, message) {
  const element = document.getElementById(elementId);
  element.textContent = message;
  element.style.display = 'block';
  
  setTimeout(() => {
    element.style.display = 'none';
  }, 3000);
}

function closeAll() {
  document.getElementById('overlay').classList.remove('active');
  document.getElementById('loginModal').classList.remove('active');
  document.getElementById('editorModal').classList.remove('active');
}

// ============ পেজ লোড হলে ============
window.onload = function() {
  // ব্রাউজার স্টোরেজ থেকে HTML লোড করে দেখানোর জন্য
  const savedHtml = localStorage.getItem('websiteHtml');
  if (savedHtml) {
    console.log('Saved HTML found in browser storage');
  }
}
</script>

</body>
</html>