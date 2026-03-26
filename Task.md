I want you to build a premium, highly interactive single-page website for "Raw Pressery | Alphanso Mango". I will provide 200 JPG frames ([ezgif-frame-001.jpg](cci:7://file:///c:/Users/Golde/OneDrive/Documents/Personal_Projects/MangoJuice/ezgif-frame-001.jpg:0:0-0:0) through [ezgif-frame-200.jpg](cci:7://file:///c:/Users/Golde/OneDrive/Documents/Personal_Projects/MangoJuice/ezgif-frame-200.jpg:0:0-0:0)) of a 3D animated bottle scene for the background. 

Please follow these precise specifications using a single [index.html](cci:7://file:///c:/Users/Golde/OneDrive/Documents/Personal_Projects/MangoJuice/index.html:0:0-0:0) file, vanilla JavaScript, and Tailwind CSS (via CDN).

### 1. Layout & Styling
* **Background & Scrolling**: The body should have a fallback linear gradient from `#f97316` to `#ea580c`. Create a main wrapper set to `height: 500vh` to force a native vertical scrollbar that the user will use to control the animation.
* **Sticky UI Overlay**: Inside the 500vh wrapper, place a `sticky top-0 w-full h-screen` container. All text and UI elements live inside this sticky layer so they stay perfectly in place while the user scrolls.
* **Typography**:
  * Top Navbar: "RAW [light] PRESSERY [bold]" logo, and links for "Shop", "Our Story", and a white "Cart" button.
  * Hero Background Text: A massive, italicized "ALPHANSO", 20% opacity white, positioned near the top-center.
  * Foreground Product Info (Bottom center): An H2 "Alphanso Mango", a subtitle "Pure. Cold-Pressed. Golden.", a pricing block (150 kr crossed out, 120 kr), and a black "ADD TO BASKET" pill-shaped button.
  * Include a bouncing "Grab Scrollbar or Drag Screen" hint at the very bottom.
  * Use text dropshadows so the white text pops off the dynamic background.

### 2. The Fullscreen 3D Canvas
* Create a `<canvas>` element fixed to the viewport (`fixed inset-0 w-screen h-screen -z-10`). This canvas acts as the animated background of the entire website.
* Preload the 200 image frames. Display a loading percentage in the center of the screen that vanishes once `loadedImages === 200`.
* **Important Rendering Logic**: When drawing frames to the canvas (`context.drawImage`), you must calculate the aspect ratio of the image vs the aspect ratio of the window so it perfectly acts like CSS `object-fit: cover`. The image must fill the entire screen without black bars or severe distortion, regardless of the monitor size.

### 3. Interactivity & JavaScript
* **Scroll to Rotate**: Map the `window.scrollY` progression (from 0 to max scrollable height) directly to frames 1 to 200.
* **Drag to Rotate**: Add event listeners to the interactive layer allowing the user to click, hold, and drag the mouse left/right across the screen to manually shift the current frame (scrubbing 360 degrees infinitely). Wrap the frames when going below 1 or above 200.
* **Butter-Smooth Easing**: Do not instantly snap the canvas to the requested frame. Use a `requestAnimationFrame` loop with linear interpolation (Lerp), moving the current frame towards the target frame by `0.1` per tick. This makes the rotation feel incredibly premium and fluid, even with a chunky mouse scroll wheel. 
* **Mouse Parallax**: Track the `mousemove` event and apply a very slight opposite CSS `transform: translate()` to background elements (like the giant "ALPHANSO" text and other floating elements) to simulate 3D depth. 
