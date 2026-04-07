<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>My Website</title>
  <style>
    body {
      margin: 0;
      font-family: Arial, sans-serif;
      line-height: 1.6;
      background: #f4f4f4;
    }
    header {
      background: #333;
      color: #fff;
      padding: 1rem 0;
      text-align: center;
    }
    nav {
      display: flex;
      justify-content: center;
      background: #555;
    }
    nav a {
      color: white;
      padding: 14px 20px;
      text-decoration: none;
    }
    nav a:hover {
      background: #333;
    }
    .container {
      padding: 20px;
    }
    .card {
      background: white;
      padding: 20px;
      margin: 20px 0;
      border-radius: 10px;
      box-shadow: 0 2px 5px rgba(0,0,0,0.1);
    }
    footer {
      text-align: center;
      padding: 1rem;
      background: #333;
      color: white;
      margin-top: 20px;
    }
    button {
      padding: 10px 15px;
      border: none;
      background: #333;
      color: white;
      border-radius: 5px;
      cursor: pointer;
    }
    button:hover {
      background: #555;
    }
  </style>
</head>
<body>

<header>
  <h1>My GitHub Pages Website</h1>
  <p>Welcome to my site 🚀</p>
</header>

<nav>
  <a href="#home">Home</a>
  <a href="#about">About</a>
  <a href="#contact">Contact</a>
</nav>

<div class="container">
  <section id="home" class="card">
    <h2>Home</h2>
    <p>This is my homepage. I built this using HTML, CSS, and JavaScript.</p>
    <button onclick="showMessage()">Click Me</button>
  </section>

  <section id="about" class="card">
    <h2>About</h2>
    <p>I am learning web development and hosting with GitHub Pages.</p>
  </section>

  <section id="contact" class="card">
    <h2>Contact</h2>
    <p>Email: example@email.com</p>
  </section>
</div>

<footer>
  <p>© 2026 My Website</p>
</footer>

<script>
  function showMessage() {
    alert("Thanks for clicking! 🎉");
  }
</script>

</body>
</html>
