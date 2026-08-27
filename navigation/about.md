---
layout: post
title: About me! ♡
permalink: /about/
comments: true
---

## As a conversation Starter

I'm Indian American!

<style>
    /* Style looks pretty compact, 
       - grid-container and grid-item are referenced the code 
    */
    .grid-container {
        display: grid;
        grid-template-columns: repeat(auto-fill, minmax(150px, 1fr)); /* Dynamic columns */
        gap: 10px;
    }
    .grid-item {
        text-align: center;
    }
    .grid-item img {
        width: 100%;
        height: 100px; /* Fixed height for uniformity */
        object-fit: contain; /* Ensure the image fits within the fixed height */
    }
    .grid-item p {
        margin: 5px 0; /* Add some margin for spacing */
    }

    .image-gallery {
        display: flex;
        flex-wrap: nowrap;
        overflow-x: auto;
        gap: 10px;
    }

    .image-gallery img {
        max-height: 150px;
        object-fit: cover;
        border-radius: 5px;
    }
</style>

<!-- This grid_container class is used by CSS styling and the id is used by JavaScript connection -->
<div class="grid-container" id="grid_container">
    <!-- content will be added here by JavaScript -->
</div>

<script>
    var container = document.getElementById("grid_container");

    var living_in_the_world = [
        { "house": "house.jpg", "greeting": "Indian flag" },
        { "house": "house2.jpg", "greeting": "American flag" }
    ];

    for (const location of living_in_the_world) {
        var gridItem = document.createElement("div");
        gridItem.className = "grid-item";

        var img = document.createElement("img");
        img.src = "{{site.baseurl}}/images/about/" + location.house;
        img.alt = location.greeting;

        var greeting = document.createElement("p");
        greeting.textContent = location.greeting;

        gridItem.appendChild(img);
        gridItem.appendChild(greeting);
        container.appendChild(gridItem);
    }
</script>

### My journey through life

Here is what I've done in my life so far!:

- Born on August 19, 2011 ⋆.ೃ࿔*:･
- Attended Stone Ranch Elementary School from kindergarden to 5th grade ⋆.ೃ࿔*:･
- Started learning Ice Skating ⛸️
- Started learning dance 💃
- Joined Math Olympaid and Debate club 🧠📚
- Attended Oak Valley Middle School from 6th to 8th grade ⋆.ೃ࿔*:･
- Joined Sci Olympaid 🧑‍🔬
- Started tennis 🎾
- Currently in Del Norte Highschool until 2029 ⋆.ೃ࿔*:･

### Hobbies, Family, and Fun

For me, everything is all about family, sports and my hobbies.

- I do around sports 5 in total; field hockey, tennis, dance, ice skating, swimming
- My family is pretty big however most of them live in India. Me and family are the only ones who live in the US currently. Despite being the only ones, we are a small family. Me, my dad and my mom.
- The gallery of pics has some of my family, hobbies, and sports.

<comment>
Gallery of Pics, scroll to the right for more ...
</comment>
<div class="image-gallery">
  <img src="{{site.baseurl}}/images/about/hockey.jpg" alt="Image 1">
  <img src="{{site.baseurl}}/images/about/Tennis.jpg" alt="Image 2">
  <img src="{{site.baseurl}}/images/about/Dance.jpg" alt="Image 3">
  <img src="{{site.baseurl}}/images/about/1.jpg" alt="Image 4">
  <img src="{{site.baseurl}}/images/about/skating.jpg" alt="Image 5">
  <img src="{{site.baseurl}}/images/about/sci oly1.png" alt="Image 6">
  <img src="{{site.baseurl}}/images/about/2.jpg" alt="Image 7">
</div>

<div id="test">
</div>

##### My Favourite food

<div class="grid-container" id="grid_container_1">
    <!-- content will be added here by JavaScript -->
</div>

<script>
    // 1. Make a connection to the HTML container defined in the HTML div
    var container = document.getElementById("grid_container_1"); // This container connects to the HTML div

    // 2. Define a JavaScript object for our http source and our data rows for the Living in the World grid
    var http_source = "https://upload.wikimedia.org/wikipedia/commons/";
    var living_in_the_world = [
        {"house": "https://upload.wikimedia.org/wikipedia/commons/4/48/Brooklyn_Pizza-cropped.png", "greeting": "Pizza", "description": "My Favourite pizza"},
        {"house": "https://upload.wikimedia.org/wikipedia/commons/e/e1/Vegan_rhubarb-strawberry-blueberry_pie_with_caramel_oat_ice-cream_%283084610787%29.jpg", "greeting": "Icecream", "description": "icecream"},
        {"house": "https://upload.wikimedia.org/wikipedia/commons/5/50/TORTEL-DOLS.jpg", "greeting": "Pasta", "description": "Pasta"},
        {"house": "https://upload.wikimedia.org/wikipedia/commons/7/73/001_Tacos_de_carnitas%2C_carne_asada_y_al_pastor.jpg", "greeting": "Tacos", "description":"Tacos"}
    ];

    // 3a. Consider how to update style count for size of container
    // The grid-template-columns has been defined as dynamic with auto-fill and minmax

    // 3b. Build grid items inside of our container for each row of data
    for (const location of living_in_the_world) {
        // Create a "div" with "class grid-item" for each row
        var gridItem = document.createElement("div");
        gridItem.className = "grid-item"; // This class name connects the gridItem to the CSS style elements

        var img = document.createElement("img");
        img.src = location.house;
        img.alt = location.greeting;

        var description = document.createElement("p");
        description.textContent = location.description;

        var greeting = document.createElement("p");
        greeting.textContent = location.greeting;

        gridItem.appendChild(img);
        gridItem.appendChild(greeting);
        container.appendChild(gridItem);
    }
</script>