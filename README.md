<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Rainbow Gradient - RainbowFX</title>
<!-- Import Poppins Font (ExtraBold 800) -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@800&display=swap" rel="stylesheet">

<style>
body {
margin: 0;
padding: 20px;
font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
background: #1a1a1a;
color: white;
min-height: 100vh;
display: flex;
flex-direction: column;
align-items: center;
justify-content: center;
}

/* --- UPDATED STYLES FOR ANIMATED TEXT --- */

@keyframes gradient-pan {
    0% { background-position: 0% 50%; }
    50% { background-position: 100% 50%; }
    100% { background-position: 0% 50%; }
}

/* 1. Shared class for the animated gradient effect */
.animated-gradient-text {
    font-family: 'Poppins', sans-serif;
    font-weight: 800; /* Poppins ExtraBold */
    
    /* The animated gradient background */
    background: linear-gradient(90deg,
        rgb(255, 89, 89),
        rgb(255, 192, 84),
        rgb(255, 255, 88),
        rgb(112, 255, 102),
        rgb(96, 255, 255),
        rgb(187, 93, 255),
        rgb(255, 89, 89)
    );
    background-size: 300% 300%;
    animation: gradient-pan 2s linear infinite;

    -webkit-background-clip: text;
    background-clip: text;
    -webkit-text-fill-color: transparent;
    
    /* Updated stroke color to rgb(76, 76, 76) */
    -webkit-text-stroke-color: rgb(76, 76, 76);
}

/* 2. Specific styles for the main title */
h1.animated-gradient-text {
    text-align: center;
    margin-bottom: 15px;
    font-size: 2.8em;
    -webkit-text-stroke-width: 1.849px;
}

/* 3. Specific styles for the credits text */
.header-comment {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 0.25em;
    text-align: center;
    margin-top: 15px;
    margin-bottom: 30px;
}
.header-comment .animated-gradient-text {
    font-size: 1.2em; /* Smaller font size for credits */
    -webkit-text-stroke-width: 1px; /* Thinner stroke for readability */
}

/* --- END UPDATED STYLES --- */


.gradient-container {
        width: 420px;
        height: 420px;
        border-radius: 15px;
        position: relative;
        overflow: hidden;
        box-shadow: 0 20px 40px rgba(0, 0, 0, 0.3);
        margin-bottom: 30px;
        transition: all 0.3s ease;
        background-color: #111;
    }

    .gradient-container.with-border {
        border: 10px solid black;
        border-radius: 0;
    }
    
    #imageCanvas {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        z-index: 2;
        cursor: grab;
    }
    
    #imageCanvas:active {
        cursor: grabbing;
    }

    .gradient-layer {
        position: absolute;
        width: 100%;
        height: 100%;
        background: linear-gradient(
            0deg,
            rgb(255, 0, 0) 0%,
            rgb(255, 127, 0) 16.66%,
            rgb(255, 255, 0) 33.33%,
            rgb(0, 255, 0) 50%,
            rgb(0, 255, 255) 66.66%,
            rgb(0, 0, 255) 83.33%,
            rgb(255, 0, 255) 100%
        );
        opacity: 0.25;
        z-index: 3;
        pointer-events: none;
        transition: transform 0.1s ease-out, width 0.1s ease-out, height 0.1s ease-out;
    }

    .upload-overlay {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        display: flex;
        align-items: center;
        justify-content: center;
        background: rgba(0, 0, 0, 0.8);
        border: 2px dashed #667eea;
        border-radius: 15px;
        z-index: 10;
        transition: all 0.3s ease;
        cursor: pointer;
    }

    .gradient-container.with-border .upload-overlay {
        border-radius: 0;
    }

    .upload-overlay.dragover {
        background: rgba(102, 126, 234, 0.2);
        border-color: #4ecdc4;
    }

    .upload-overlay.hidden {
        opacity: 0;
        pointer-events: none;
    }

    .upload-text {
        text-align: center;
        color: white;
        font-size: 18px;
        font-weight: 600;
    }

    .upload-subtext {
        color: #888;
        font-size: 14px;
        margin-top: 10px;
    }

    .controls {
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
        gap: 15px;
        margin-bottom: 30px;
    }

    .rainbow-btn {
        background: linear-gradient(45deg, #667eea, #764ba2);
        border: none;
        color: white;
        padding: 12px 25px;
        border-radius: 8px;
        cursor: pointer;
        font-weight: 600;
        transition: all 0.3s ease;
        font-size: 16px;
    }

    .rainbow-btn:hover {
        transform: translateY(-2px);
        box-shadow: 0 10px 20px rgba(0, 0, 0, 0.3);
    }

    .rainbow-btn.active {
        background: linear-gradient(45deg, #27ae60, #2ecc71);
    }

    .rainbow-btn.disabled, .rainbow-btn:disabled {
        background: #555;
        cursor: not-allowed;
        transform: none;
        box-shadow: none;
        opacity: 0.7;
    }

    .rainbow-btn.recording {
        background: linear-gradient(45deg, #e74c3c, #c0392b);
    }

    .info-panel {
        background: rgba(255, 255, 255, 0.1);
        backdrop-filter: blur(10px);
        border-radius: 12px;
        padding: 25px;
        border: 1px solid rgba(255, 255, 255, 0.2);
        max-width: 600px;
        width: 100%;
    }

    .title-line {
        border: 0;
        height: 1px;
        background-color: #fff;
        opacity: 0.7;
        width: 90%;
        max-width: 600px;
        margin: 0 auto;
    }

    .property { display: flex; justify-content: space-between; margin: 10px 0; padding: 8px 12px; background: rgba(255, 255, 255, 0.05); border-radius: 6px; }
    .property-label { font-weight: 600; color: #ff6b6b; }
    .speed-control { margin-top: 20px; text-align: center; }
    .speed-slider { width: 100%; height: 8px; border-radius: 4px; background: linear-gradient(to right, #3498db, #e74c3c); outline: none; margin: 15px 0; cursor: pointer; }
</style>
</head>
<body>

<!-- Apply the shared class to both elements -->
<h1 class="animated-gradient-text">RainbowFX Gradient</h1>
<hr class="title-line">
<div class="header-comment">
  <span class="animated-gradient-text">Made with love by: @AngelGamingBTW</span>
  <span>🐱❤️</span>
</div>

<div class="gradient-container" id="gradientContainer">
    <canvas id="imageCanvas" width="420" height="420"></canvas>
    <div class="gradient-layer" id="gradientLayer"></div>
    <div class="upload-overlay" id="uploadOverlay">
        <div>
            <div class="upload-text">📸 Upload Image</div>
            <div class="upload-subtext">Drag & drop or click to select<br>Scroll to zoom, drag to pan</div>
        </div>
    </div>
    <input type="file" id="fileInput" accept="image/*" style="display: none;">
</div>

<div class="controls">
    <button class="rainbow-btn" id="toggleBtn" onclick="toggleRainbow()">Start Rainbow FX</button>
    <button class="rainbow-btn" id="saveBtn" onclick="saveImage()">Save Photo</button>
    <button class="rainbow-btn" onclick="clearImage()">Clear Image</button>
    <button class="rainbow-btn" id="toggleBorderBtn" onclick="toggleBorder()">Add Border</button>
</div>

<div class="info-panel">
    <h3>Gradient Properties</h3>
    <div class="property">
        <span class="property-label">Rotation:</span>
        <span id="rotationDisplay">0°</span>
    </div>
    <div class="property">
        <span class="property-label">Size:</span>
        <span>420x420px</span>
    </div>
    <div class="property">
        <span class="property-label">Transparency:</span>
        <span>0.25 (Gradient Overlay)</span>
    </div>
    <div class="property">
        <span class="property-label">Animation:</span>
        <span id="animationStatus">Disabled</span>
    </div>
    
    <div class="speed-control">
        <h4>Animation Speed</h4>
        <input type="range" class="speed-slider" id="speedSlider" min="10" max="200" value="100">
        <p>Speed: <span id="speedValue">1.00</span></p>
    </div>

    <div class="speed-control">
        <h4>Rotation Angle</h4>
        <input type="range" class="speed-slider" id="rotationSlider" min="-180" max="180" value="0">
        <p>Angle: <span id="rotationValue">0</span>°</p>
    </div>
    
</div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/gif.js/0.2.0/gif.js"></script>

<script>
    let rainbowActive = false;
    let animationFrame;
    let speed = 1.0;
    let rotation = 0;

    let originalImage = null;
    let zoom = 1.0;
    let initialZoom = 1.0;
    let offsetX = 0;
    let offsetY = 0;
    let isDragging = false;
    let lastX, lastY;

    const gradientContainer = document.getElementById('gradientContainer');
    const gradientLayer = document.getElementById('gradientLayer');
    const uploadOverlay = document.getElementById('uploadOverlay');
    const fileInput = document.getElementById('fileInput');
    const toggleBtn = document.getElementById('toggleBtn');
    const saveBtn = document.getElementById('saveBtn'); 
    const speedSlider = document.getElementById('speedSlider');
    const speedValue = document.getElementById('speedValue');
    const rotationSlider = document.getElementById('rotationSlider');
    const rotationValue = document.getElementById('rotationValue');
    const rotationDisplay = document.getElementById('rotationDisplay');
    const animationStatus = document.getElementById('animationStatus');
    const toggleBorderBtn = document.getElementById('toggleBorderBtn');

    const imageCanvas = document.getElementById('imageCanvas');
    const ctx = imageCanvas.getContext('2d');

    const colors = [ {r: 255, g: 0, b: 0}, {r: 255, g: 127, b: 0}, {r: 255, g: 255, b: 0}, {r: 0, g: 255, b: 0}, {r: 0, g: 255, b: 255}, {r: 0, g: 0, b: 255}, {r: 255, g: 0, b: 255} ];
    
    function updateGradient(time) {
        const tick = (time * speed * 0.001 % 3) / 3;
        let gradientStops = [];
        for (let i = 0; i < colors.length; i++) {
            let stopTime = tick + i / colors.length;
            if (stopTime > 1) stopTime -= 1;
            gradientStops.push({ time: stopTime, color: `rgb(${colors[i].r}, ${colors[i].g}, ${colors[i].b})` });
        }
        gradientStops.sort((a, b) => a.time - b.time);
        const gradientString = gradientStops.map(stop => `${stop.color} ${(stop.time * 100).toFixed(1)}%`).join(', ');
        gradientLayer.style.background = `linear-gradient(${rotation}deg, ${gradientString})`;
    }
    
    function animateRainbow() {
        updateGradient(Date.now());
        if (rainbowActive) {
            animationFrame = requestAnimationFrame(animateRainbow);
        }
    }
    
    uploadOverlay.addEventListener('click', () => fileInput.click());
    uploadOverlay.addEventListener('dragover', (e) => { e.preventDefault(); uploadOverlay.classList.add('dragover'); });
    uploadOverlay.addEventListener('dragleave', () => uploadOverlay.classList.remove('dragover'));
    uploadOverlay.addEventListener('drop', (e) => {
        e.preventDefault();
        uploadOverlay.classList.remove('dragover');
        if (e.dataTransfer.files.length > 0) handleImageUpload(e.dataTransfer.files[0]);
    });
    fileInput.addEventListener('change', (e) => {
        if (e.target.files.length > 0) handleImageUpload(e.target.files[0]);
    });

    function handleImageUpload(file) {
        if (!file.type.startsWith('image/')) {
            alert('Please upload an image file');
            return;
        }
        const reader = new FileReader();
        reader.onload = (e) => {
            const img = new Image();
            img.onload = () => {
                originalImage = img;
                const canvasAspect = imageCanvas.width / imageCanvas.height;
                const imageAspect = img.width / img.height;
                
                if (imageAspect > canvasAspect) {
                    initialZoom = imageCanvas.width / img.width;
                } else {
                    initialZoom = imageCanvas.height / img.height;
                }
                zoom = initialZoom;
                
                offsetX = (imageCanvas.width - img.width * zoom) / 2;
                offsetY = (imageCanvas.height - img.height * zoom) / 2;

                drawImageWithTransform();
                uploadOverlay.classList.add('hidden');
            };
            img.src = e.target.result;
        };
        reader.readAsDataURL(file);
    }

    function drawImageWithTransform() {
        if (!originalImage) return;
        ctx.clearRect(0, 0, imageCanvas.width, imageCanvas.height);
        ctx.save();
        ctx.drawImage(
            originalImage, 
            offsetX, 
            offsetY, 
            originalImage.width * zoom, 
            originalImage.height * zoom
        );
        ctx.restore();

        const gradientWidth = originalImage.width * zoom;
        const gradientHeight = originalImage.height * zoom;

        gradientLayer.style.width = `${gradientWidth}px`;
        gradientLayer.style.height = `${gradientHeight}px`;
        gradientLayer.style.transform = `translate(${offsetX}px, ${offsetY}px)`;
    }

    function clearImage() {
        originalImage = null;
        ctx.clearRect(0, 0, imageCanvas.width, imageCanvas.height);
        uploadOverlay.classList.remove('hidden');
        fileInput.value = '';

        gradientLayer.style.width = '100%';
        gradientLayer.style.height = '100%';
        gradientLayer.style.transform = 'translate(0, 0)';
    }

    imageCanvas.addEventListener('wheel', (e) => {
        e.preventDefault();
        if (!originalImage) return;

        const rect = imageCanvas.getBoundingClientRect();
        const x = e.clientX - rect.left;
        const y = e.clientY - rect.top;

        const zoomFactor = 1.1;
        let newZoom;

        if (e.deltaY < 0) {
            newZoom = zoom * zoomFactor;
        } else {
            newZoom = zoom / zoomFactor;
        }
        
        if (newZoom < initialZoom) {
            newZoom = initialZoom;
        }

        offsetX = x - (x - offsetX) * (newZoom / zoom);
        offsetY = y - (y - offsetY) * (newZoom / zoom);

        zoom = newZoom;
        drawImageWithTransform();
    });

    imageCanvas.addEventListener('pointerdown', (e) => {
        if (!originalImage) return;
        isDragging = true;
        lastX = e.clientX;
        lastY = e.clientY;
        imageCanvas.setPointerCapture(e.pointerId);
    });
    
    imageCanvas.addEventListener('pointermove', (e) => {
        if (!isDragging || !originalImage) return;
        const dx = e.clientX - lastX;
        const dy = e.clientY - lastY;
        offsetX += dx;
        offsetY += dy;
        lastX = e.clientX;
        lastY = e.clientY;
        drawImageWithTransform();
    });

    imageCanvas.addEventListener('pointerup', (e) => {
        isDragging = false;
        imageCanvas.releasePointerCapture(e.pointerId);
    });

    imageCanvas.addEventListener('pointerleave', (e) => {
        isDragging = false;
    });

    function toggleBorder() {
        gradientContainer.classList.toggle('with-border');
        const isBorderActive = gradientContainer.classList.contains('with-border');
        toggleBorderBtn.textContent = isBorderActive ? 'Remove Border' : 'Add Border';
    }

    function toggleRainbow() {
        rainbowActive = !rainbowActive;
        if (rainbowActive) {
            toggleBtn.textContent = 'Stop Rainbow FX';
            toggleBtn.classList.add('active');
            animationStatus.textContent = 'Active';
            animateRainbow();
        } else {
            toggleBtn.textContent = 'Start Rainbow FX';
            toggleBtn.classList.remove('active');
            if (animationFrame) cancelAnimationFrame(animationFrame);
            gradientLayer.style.background = `linear-gradient(${rotation}deg, rgb(255, 0, 0) 0%, rgb(255, 127, 0) 16.66%, rgb(255, 255, 0) 33.33%, rgb(0, 255, 0) 50%, rgb(0, 255, 255) 66.66%, rgb(0, 0, 255) 83.33%, rgb(255, 0, 255) 100%)`;
            animationStatus.textContent = 'Disabled';
        }
    }

    speedSlider.addEventListener('input', function() { speed = parseInt(this.value) / 100; speedValue.textContent = speed.toFixed(2); });
    rotationSlider.addEventListener('input', function() {
        rotation = parseInt(this.value);
        rotationValue.textContent = rotation;
        rotationDisplay.textContent = rotation + '°';
        if (!rainbowActive) {
            gradientLayer.style.background = `linear-gradient(${rotation}deg, rgb(255, 0, 0) 0%, rgb(255, 127, 0) 16.66%, rgb(255, 255, 0) 33.33%, rgb(0, 255, 0) 50%, rgb(0, 255, 255) 66.66%, rgb(0, 0, 255) 83.33%, rgb(255, 0, 255) 100%)`;
        }
    });

    function saveImage() {
        if (!originalImage) {
            alert("Please upload an image first!");
            return;
        }
        if (rainbowActive) {
            saveAsGIF();
        } else {
            saveAsPNG();
        }
    }

    async function renderCurrentFrame() {
        const compositeCanvas = document.createElement('canvas');
        compositeCanvas.width = 420;
        compositeCanvas.height = 420;
        const compositeCtx = compositeCanvas.getContext('2d');
        compositeCtx.drawImage(imageCanvas, 0, 0);

        const gradientCanvas = await html2canvas(gradientLayer, {
            backgroundColor: null,
            useCORS: true,
            width: gradientLayer.offsetWidth,
            height: gradientLayer.offsetHeight
        });

        compositeCtx.globalCompositeOperation = 'source-atop';
        compositeCtx.drawImage(gradientCanvas, offsetX, offsetY, gradientLayer.offsetWidth, gradientLayer.offsetHeight);
        compositeCtx.globalCompositeOperation = 'source-over';
        
        const isBorderActive = gradientContainer.classList.contains('with-border');
        const borderWidth = isBorderActive ? 10 : 0;
        const finalWidth = 420 + (borderWidth * 2);
        const finalHeight = 420 + (borderWidth * 2);

        const finalCanvas = document.createElement('canvas');
        finalCanvas.width = finalWidth;
        finalCanvas.height = finalHeight;
        const finalCtx = finalCanvas.getContext('2d');

        if (isBorderActive) {
            finalCtx.fillStyle = 'black';
            finalCtx.fillRect(0, 0, finalWidth, finalHeight);
        }
        
        finalCtx.drawImage(compositeCanvas, borderWidth, borderWidth);
        
        return finalCanvas;
    }

    async function saveAsPNG() {
        saveBtn.textContent = 'Saving...';
        saveBtn.disabled = true;
        try {
            const finalCanvas = await renderCurrentFrame();
            const link = document.createElement('a');
            link.download = 'rainbowfx-static.png';
            link.href = finalCanvas.toDataURL('image/png');
            link.click();
        } catch(err) {
            console.error("Error saving PNG:", err);
            alert("Sorry, an error occurred while saving the image.");
        } finally {
            saveBtn.textContent = 'Save Photo';
            saveBtn.disabled = false;
        }
    }

    async function saveAsGIF() {
        const workerResponse = await fetch('https://cdnjs.cloudflare.com/ajax/libs/gif.js/0.2.0/gif.worker.js');
        const workerScript = await workerResponse.text();
        const workerBlob = new Blob([workerScript], { type: 'application/javascript' });
        const workerUrl = URL.createObjectURL(workerBlob);

        saveBtn.textContent = '🔴 Recording...';
        saveBtn.classList.add('recording');
        saveBtn.disabled = true;
        if (animationFrame) cancelAnimationFrame(animationFrame);

        try {
            const isBorderActive = gradientContainer.classList.contains('with-border');
            const borderWidth = isBorderActive ? 10 : 0;
            const gifWidth = 420 + (borderWidth * 2);
            const gifHeight = 420 + (borderWidth * 2);

            const gif = new GIF({
                workers: 2,
                quality: 20,
                width: gifWidth,
                height: gifHeight,
                workerScript: workerUrl
            });
            
            const onFinished = new Promise(resolve => {
                gif.on('finished', blob => resolve(blob));
            });

            const frameRate = 30;
            const duration = 3000;
            const totalFrames = frameRate * (duration / 1000);
            const delay = 1000 / frameRate;
            const startTime = Date.now();

            for (let i = 0; i < totalFrames; i++) {
                const currentTime = startTime + (i * delay);
                updateGradient(currentTime);
                const frameCanvas = await renderCurrentFrame();
                gif.addFrame(frameCanvas, { delay: delay });
            }

            gif.render();
            saveBtn.textContent = '💾 Compiling GIF...';
            
            const blob = await onFinished;
            
            const link = document.createElement('a');
            link.download = 'rainbowfx-animated.gif';
            link.href = URL.createObjectURL(blob);
            link.click();
            URL.revokeObjectURL(link.href);

        } catch (error) {
            console.error("Failed to create GIF:", error);
            alert("Sorry, an error occurred while recording the GIF. Please try again.");
        } finally {
            URL.revokeObjectURL(workerUrl);
            saveBtn.textContent = 'Save Photo';
            saveBtn.classList.remove('recording');
            saveBtn.disabled = false;
            if (rainbowActive) animateRainbow();
        }
    }

    speedValue.textContent = speed.toFixed(2);
    rotationValue.textContent = rotation;
    rotationDisplay.textContent = rotation + '°';
  </script>
</body>
</html>
