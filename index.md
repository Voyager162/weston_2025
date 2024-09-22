---
layout: base
title: Student Home 
description: Home Page
author: Weston Gardner
hide: true
---
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Cool Dropdown Menu</title>
  <style>
    .button-custom {
      background-color: #2b669a; /* Main theme color, adjust to match theme */
      color: white;
      border: none;
      border-radius: 5px;
      padding: 10px 20px;
      font-size: 16px;
      cursor: pointer;
      transition: background-color 0.3s ease, transform 0.3s ease;
    }
    .button-custom:hover {
      background-color: #1d4f73; /* Darker shade for hover */
      transform: scale(1.05);    /* Slightly enlarges button on hover */
    }
    .button-custom:active {
      background-color: #163d59; /* Even darker on click */
      transform: scale(0.98);    /* Shrinks button slightly on click */
    }
    .button-custom:focus {
      outline: none;
      box-shadow: 0 0 5px #2b669a; /* Adds a shadow on focus */
    }
    .dropdown {
      position: relative;
      display: inline-block;
    }
    .dropdown button {
      background-color: #3498db;
      color: white;
      padding: 14px 20px;
      font-size: 18px;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      transition: background-color 0.3s ease;
    }
    .dropdown button:hover {
      background-color: #2980b9;
    }
    .dropdown-content {
      display: none;
      position: absolute;
      background-color: #34495e;
      min-width: 160px;
      box-shadow: 0px 8px 16px rgba(0, 0, 0, 0.2);
      border-radius: 8px;
      z-index: 1;
      opacity: 0;
      transform: translateY(10px);
      transition: opacity 0.3s ease, transform 0.3s ease;
    }
    .dropdown-content a {
      color: white;
      padding: 12px 16px;
      text-decoration: none;
      display: block;
      border-radius: 8px;
      transition: background-color 0.3s ease;
    }
    .dropdown-content a:hover {
      background-color: #1abc9c;
    }
    .dropdown:hover .dropdown-content {
      display: block;
      opacity: 1;
      transform: translateY(0);
    }
  </style>
</head>
  <body>
    <div class="dropdown">
      <button>Jupyter Notebooks</button>
      <div class="dropdown-content">
        <a href="/weston_2025/posts/myproblems">My Problems</a>
        <a href="/weston_2025/posts/mario">Mario</a>
        <a href="/weston_2025/posts/aboutcoding">About Coding</a>
      </div>
    </div>
    <p>Fractals are interesting, here is a button that you can click that says fractals on it</p>
    <button class="button-custom">FRACTALS</button>
    <div style="height: 50px;"></div>
    <a href="https://en.wikipedia.org/wiki/Fractal" style="display: block;">
      <button class="button-custom">Wiki Page</button>
    </a>
    <div style="height: 5px;"></div>
    <a href="https://math.hws.edu/eck/js/mandelbrot/MB.html" style="display: block;">
      <button class="button-custom">Try Fractals</button>
    </a>
    <p>Here is a link to a wiki page that you can learn about fractals on. And another will bring you to a simulation of a fractal for you to play with</p>
  </body>
  <head>
    <link rel="stylesheet" href="/weston_2025/_sass/nighthawk/hacks.css">
  </head>
  <body>
    <div class="dropdown">
      <button>Games</button>
      <div class="dropdown-content">
        <a href="/weston_2025/javascriptCalculator">Regular Calculator</a>
        <a href="/weston_2025/javascript/project/binary-calculator">Binary Calculator</a>
        <a href="/weston_2025/clicker">Clicker Game</a>
        <a href="/weston_2025/TickTackToe">Tick Tack Toe</a>
        <a href="https://voyager162.github.io/RunAway">RunAwayGame</a>
      </div>
    </div>
  </body>
</html>


<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Loading Spinner Example</title>
  <style>
    /* Overlay and loader styles */
    .loader-overlay {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background-color: rgba(0, 0, 0, 0.7);
      display: flex;
      justify-content: center;
      align-items: center;
      z-index: 9999;
    }
    .loader {
      border: 8px solid rgba(255, 255, 255, 0.3);
      border-top: 8px solid #2b669a;
      border-radius: 50%;
      width: 100px;
      height: 100px;
      animation: spin 1s linear infinite, colorchange 3s ease-in-out infinite;
    }
    @keyframes spin {
      0% {
        transform: rotate(0deg);
      }
      100% {
        transform: rotate(360deg);
      }
    }
    @keyframes colorchange {
      0% {
        border-top-color: #2b669a;
      }
      50% {
        border-top-color: #ff6347;
      }
      100% {
        border-top-color: #4caf50;
      }
    }
    /* Page content that gets hidden initially */
    #content {
      display: none;
    }
  </style>
</head>
<body>
<!-- Loading spinner overlay -->
<div id="loading" class="loader-overlay">
  <div class="loader"></div>
</div>
<!-- Page content (hidden until the page is loaded) -->
<div id="content">
  <h1>Welcome to the Page!</h1>
  <p>This content will be shown after the loading spinner disappears.</p>
</div>
<script>
  window.addEventListener("load", function() {
    document.getElementById("loading").style.display = "none"; // Hide spinner once loaded
    document.getElementById("content").style.display = "block"; // Show content
  });
</script>
</body>
</html>