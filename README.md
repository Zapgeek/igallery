# Ex.08 Design of Interactive Image Gallery
## Date:

## AIM:
To design a web application for an inteactive image gallery with minimum five images.

## DESIGN STEPS:

### Step 1:
Clone the github repository and create Django admin interface.

### Step 2:
Change settings.py file to allow request from all hosts.

### Step 3:
Use CSS for positioning and styling.

### Step 4:
Write JavaScript program for implementing interactivity.

### Step 5:
Validate the HTML and CSS code.

### Step 6:
Publish the website in the given URL.

## PROGRAM :

views.py
```
from django.shortcuts import render
def gallery (request):
    return render(request,'image_gallery.html')
```

image_gallery.html
```
{% load static %}
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Singapore</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: white;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            overflow: hidden;
        }

        .title {
            position: absolute;
            top: 20px;
            left: 50%;
            transform: translateX(-50%);
            font-size: 42px;
            color: rgb(0, 0, 0);
            z-index: 1;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.6);
        }

        .gallery-container {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(370px, 1fr));
            gap: 10px;
            padding: 20px;
            max-width: 1200px;
            width: 100%;
        }

        .gallery-item img {
            width: 100%; 
            height: 300px; 
            border-radius: 8px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            transition: transform 0.3s ease;
        }

        .gallery-item img:hover {
            transform: scale(1.30);
            cursor: pointer;
        }

        .slider {
            display: none;
            position: fixed;
            z-index: 2;
            left: 0;
            top: 50%;
            transform: translateY(-50%);
            width: 100%;
            text-align: center;
        }

        .slider img {
            width: 90%;
            max-width: 800px;
            border-radius: 10px;
            transition: opacity 0.5s ease;
        }

        .arrow {
            cursor: pointer;
            position: absolute;
            top: 50%;
            transform: translateY(-50%);
            font-size: 40px;
            color: white;
            user-select: none;
            padding: 10px;
        }

        .arrow.left {
            left: 10px;
            color: aqua;
        }

        .arrow.right {
            right: 10px;
            color: aqua;
        }

        .arrow:hover {
            color: lightgray;
        }

        .close-btn {
            position: absolute;
            top: 10px;
            right: 10px;
            background-color: rgba(0, 0, 0, 0.6);
            color: rgb(0, 255, 251);
            border: none;
            padding: 10px;
            cursor: pointer;
            font-size: 20px;
            border-radius: 5px;
            display: none;
        }

        .close-btn:hover {
            background-color: rgba(0, 0, 0, 0.8);
        }
    </style>
</head>
<body>
    <div class="title">Singapore</div> 
    
    <div class="gallery-container">
        <div class="gallery-item">
            <img src="{% static 'images/sg1.jpeg' %}" alt="Image 1">
        </div>
        <div class="gallery-item">
            <img src="{% static 'images/sg2.jpg' %}" alt="Image 2">
        </div>
        <div class="gallery-item">
            <img src="{% static 'images/sg3.avif' %}" alt="Image 3">
        </div>
        <div class="gallery-item">
            <img src="{% static 'images/sg4.jpg' %}" alt="Static Image">
        </div>
        <div class="gallery-item">
            <img src="{% static 'images/sg5.webp' %}" alt="Image 5">
        </div>
        <div class="gallery-item">
            <img src="{% static 'images/sg6.jpg' %}" alt="Image 6">
        </div>
    </div>

    <div class="slider" id="slider">
        <button class="close-btn" id="close-btn">&#10006;</button>
        <span class="arrow left" id="prev">&#10094;</span>
        <img src="" alt="Slider Image" id="slider-img">
        <span class="arrow right" id="next">&#10095;</span>
    </div>

    <script>
        const images = document.querySelectorAll('.gallery-item img');
        const slider = document.getElementById('slider');
        const sliderImg = document.getElementById('slider-img');
        const prevBtn = document.getElementById('prev');
        const nextBtn = document.getElementById('next');
        const closeBtn = document.getElementById('close-btn');

        let currentIndex = 0;
        images.forEach((image, index) => {
            image.addEventListener('click', () => {
                slider.style.display = 'block';
                sliderImg.src = image.src;
                currentIndex = index;
                closeBtn.style.display = 'block'; 
            });
        });

        prevBtn.addEventListener('click', (e) => {
            e.stopPropagation(); 
            currentIndex = (currentIndex - 1 + images.length) % images.length;
            sliderImg.src = images[currentIndex].src;
        });

        nextBtn.addEventListener('click', (e) => {
            e.stopPropagation(); 
            currentIndex = (currentIndex + 1) % images.length;
            sliderImg.src = images[currentIndex].src;
        });

        closeBtn.addEventListener('click', () => {
            slider.style.display = 'none';
            closeBtn.style.display = 'none';
        });

        slider.addEventListener('click', () => {
            slider.style.display = 'none';
            closeBtn.style.display = 'none';
        });
    </script>

</body>
</html>
```
urls.py
```
from django.contrib import admin 
from django.urls import path 
from app import views
urlpatterns = [ 
    path('admin/', admin.site.urls), 
    path('gallery/',views.gallery),
]
```
## OUTPUT:
![395654914-f31f2c10-85fd-4039-9859-50b1bc3b207d](https://github.com/user-attachments/assets/45cc97aa-5708-497a-a98f-60e5294fc4e8)

![395654985-3915d5f8-3eb0-41e0-9585-aa46d7db6003](https://github.com/user-attachments/assets/37111620-391d-419e-bbd2-88ad5afc2f5b)

![395655012-5a9c7e5a-308a-430d-802e-57143088f748](https://github.com/user-attachments/assets/2d050d9b-4cf1-4f7f-8797-d27fe5293163)

![image](https://github.com/user-attachments/assets/775f05eb-c2b4-4132-9e42-c5f007f3a10a)




## RESULT:
The program for designing an interactive image gallery using HTML, CSS and JavaScript is executed successfully.
