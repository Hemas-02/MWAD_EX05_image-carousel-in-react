# MWAD_EX05_image-carousel-in-react
## Date: 28-11-2025

## AIM
To create a Image Carousel using React 

## ALGORITHM
### STEP 1 Initial Setup:
Input: A list of images to display in the carousel.

Output: A component displaying the images with navigation controls (e.g., next/previous buttons).

### Step 2 State Management:
Use a state variable (currentIndex) to track the index of the current image displayed.

The carousel starts with the first image, so initialize currentIndex to 0.

### Step 3 Navigation Controls:
Next Image: When the "Next" button is clicked, increment currentIndex.

If currentIndex is at the end of the image list (last image), loop back to the first image using modulo:
currentIndex = (currentIndex + 1) % images.length;

Previous Image: When the "Previous" button is clicked, decrement currentIndex.

If currentIndex is at the beginning (first image), loop back to the last image:
currentIndex = (currentIndex - 1 + images.length) % images.length;

### Step 4 Displaying the Image:
The currentIndex determines which image is displayed.

Using the currentIndex, display the corresponding image from the images list.

### Step 5 Auto-Rotation:
Set an interval to automatically change the image after a set amount of time (e.g., 3 seconds).

Use setInterval to call the nextImage() function at regular intervals.

Clean up the interval when the component unmounts using clearInterval to prevent memory leaks.

PROGRAM
App.js

```
import React from 'react';
import './App.css';
import ImageCarousel from './imagecarousel';
import img1 from './dog01.jpg';
import img2 from './dog02.jpg';
import img3 from './dog03.jpg';

function App() {
  const images = [img1, img2, img3];

  return (
    <div>
      <h2 style={{ textAlign: 'center' }}>React Image Carousel</h2>
      <ImageCarousel images={images} autoPlayInterval={3000} />
    </div>
  );
}

export default App;
```
ImageCarousel.js
```
import React, { useEffect, useState } from 'react';
import './imagecarousel.css';

function ImageCarousel({ images, autoPlayInterval }) {
  const [currentIndex, setCurrentIndex] = useState(0);

  useEffect(() => {
    const timer = setInterval(() => {
      goToNext();
    }, autoPlayInterval);

    return () => clearInterval(timer);
  }, [currentIndex]);

  const goToPrevious = () => {
    setCurrentIndex((prevIndex) =>
      prevIndex === 0 ? images.length - 1 : prevIndex - 1
    );
  };

  const goToNext = () => {
    setCurrentIndex((prevIndex) =>
      (prevIndex + 1) % images.length
    );
  };

  return (
    <div className="carousel">
      <button className="nav-button prev" onClick={goToPrevious}>❮</button>
      <img
        src={images[currentIndex]}
        alt={`Slide ${currentIndex + 1}`}
        className="carousel-image"
      />
      <button className="nav-button next" onClick={goToNext}>❯</button>
    </div>
  );
}

export default ImageCarousel;
```

ImageCarousel.css
```
.carousel {
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  height: 400px;
  background-color: #f0f0f0;
  overflow: hidden;
  border-radius: 10px;
  margin: 20px auto;
  width: 80%;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
}

.carousel-image {
  max-width: 100%;
  max-height: 100%;
  object-fit: cover;
  border-radius: 10px;
}

.nav-button {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background-color: rgba(0, 0, 0, 0.4);
  color: white;
  border: none;
  padding: 10px;
  cursor: pointer;
  z-index: 1;
  font-size: 24px;
  border-radius: 50%;
}

.nav-button:hover {
  background-color: rgba(0, 0, 0, 0.6);
}

.prev {
  left: 10px;
}

.next {
  right: 10px;
}
```

# OUTPUT

<img width="1763" height="889" alt="image" src="https://github.com/user-attachments/assets/6ab3603d-2991-4b1f-99e9-4f542a4978f9" />

<img width="1757" height="900" alt="image" src="https://github.com/user-attachments/assets/7fbf5281-618a-4e45-b2be-acf617207944" />

<img width="1758" height="907" alt="image" src="https://github.com/user-attachments/assets/9ebfe518-bcc3-477f-be45-db1523794d63" />

# RESULT
The program for creating Image Carousel using React is executed successfully.
