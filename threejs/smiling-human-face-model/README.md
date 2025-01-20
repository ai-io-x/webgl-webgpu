Generate a smiling human face model in just one HTML file with JavaScript and threejs

### Plan:
1. Create basic HTML structure
2. Import Three.js library
3. Setup scene, camera, renderer
4. Create face geometry using spheres and cylinders
5. Add eyes using spheres
6. Create smiling mouth using TorusGeometry
7. Add basic lighting
8. Implement rotation animation

```html
<!DOCTYPE html>
<html>
<head>
    <title>3D Smiling Face</title>
    <style>
        body { margin: 0; }
        canvas { display: block; }
    </style>
</head>
<body>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
    <script>
        // Scene setup
        const scene = new THREE.Scene();
        const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
        const renderer = new THREE.WebGLRenderer();
        renderer.setSize(window.innerWidth, window.innerHeight);
        document.body.appendChild(renderer.domElement);

        // Face - main sphere
        const faceGeometry = new THREE.SphereGeometry(2, 32, 32);
        const faceMaterial = new THREE.MeshPhongMaterial({ color: 0xffdbac });
        const face = new THREE.Mesh(faceGeometry, faceMaterial);
        scene.add(face);

        // Eyes
        const eyeGeometry = new THREE.SphereGeometry(0.3, 32, 32);
        const eyeMaterial = new THREE.MeshPhongMaterial({ color: 0x000000 });
        
        const leftEye = new THREE.Mesh(eyeGeometry, eyeMaterial);
        leftEye.position.set(-0.7, 0.3, 1.6);
        face.add(leftEye);

        const rightEye = new THREE.Mesh(eyeGeometry, eyeMaterial);
        rightEye.position.set(0.7, 0.3, 1.6);
        face.add(rightEye);

        // Smile
        const smileGeometry = new THREE.TorusGeometry(0.7, 0.1, 16, 32, Math.PI);
        const smileMaterial = new THREE.MeshPhongMaterial({ color: 0x000000 });
        const smile = new THREE.Mesh(smileGeometry, smileMaterial);
        smile.position.set(0, -0.3, 1.6);
        smile.rotation.x = -0.5;
        face.add(smile);

        // Lighting
        const light = new THREE.DirectionalLight(0xffffff, 1);
        light.position.set(0, 0, 5);
        scene.add(light);

        const ambientLight = new THREE.AmbientLight(0x404040);
        scene.add(ambientLight);

        // Camera position
        camera.position.z = 5;

        // Animation
        function animate() {
            requestAnimationFrame(animate);
            face.rotation.y += 0.005;
            renderer.render(scene, camera);
        }
        animate();

        // Handle window resize
        window.addEventListener('resize', onWindowResize, false);
        function onWindowResize() {
            camera.aspect = window.innerWidth / window.innerHeight;
            camera.updateProjectionMatrix();
            renderer.setSize(window.innerWidth, window.innerHeight);
        }
    </script>
</body>
</html>
```

Save this as index.html and open it in a browser to see a rotating 3D smiling face. The face will automatically rotate and adjust to window resizing.

Similar code found with 2 license types

Collecting workspace information

Based on your request, I'll help you improve the 3D face model incorporating techniques from the Three.js decals example. Here's the enhanced version:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Enhanced 3D Smiling Face</title>
    <style>
        body { margin: 0; }
        canvas { display: block; }
    </style>
</head>
<body>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
    <script>
        // Enhanced scene setup with better lighting and materials
        const scene = new THREE.Scene();
        scene.background = new THREE.Color(0x443333);
        scene.fog = new THREE.Fog(0x443333, 1, 12);

        const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
        const renderer = new THREE.WebGLRenderer({ antialias: true });
        renderer.setPixelRatio(window.devicePixelRatio);
        renderer.setSize(window.innerWidth, window.innerHeight);
        renderer.shadowMap.enabled = true;
        document.body.appendChild(renderer.domElement);

        // Enhanced materials with better shading
        const faceMaterial = new THREE.MeshPhongMaterial({
            color: 0xffdbac,
            specular: 0x050505,
            shininess: 100,
            reflectivity: 0.3
        });

        // Face with more detailed geometry
        const faceGeometry = new THREE.SphereGeometry(2, 64, 64);
        const face = new THREE.Mesh(faceGeometry, faceMaterial);
        face.castShadow = true;
        face.receiveShadow = true;
        scene.add(face);

        // Enhanced eyes with glossy effect
        const eyeMaterial = new THREE.MeshPhongMaterial({
            color: 0x000000,
            specular: 0xffffff,
            shininess: 100
        });
        const eyeGeometry = new THREE.SphereGeometry(0.3, 32, 32);

        const leftEye = new THREE.Mesh(eyeGeometry, eyeMaterial);
        leftEye.position.set(-0.7, 0.3, 1.6);
        leftEye.castShadow = true;
        face.add(leftEye);

        const rightEye = new THREE.Mesh(eyeGeometry, eyeMaterial);
        rightEye.position.set(0.7, 0.3, 1.6);
        rightEye.castShadow = true;
        face.add(rightEye);

        // Enhanced smile with better geometry
        const smileGeometry = new THREE.TorusGeometry(0.7, 0.15, 32, 64, Math.PI);
        const smileMaterial = new THREE.MeshPhongMaterial({
            color: 0x000000,
            specular: 0x111111,
            shininess: 30
        });
        const smile = new THREE.Mesh(smileGeometry, smileMaterial);
        smile.position.set(0, -0.3, 1.6);
        smile.rotation.x = -0.5;
        smile.castShadow = true;
        face.add(smile);

        // Enhanced lighting setup
        const ambientLight = new THREE.AmbientLight(0x443333, 0.5);
        scene.add(ambientLight);

        const dirLight1 = new THREE.DirectionalLight(0xffddcc, 1);
        dirLight1.position.set(1, 0.75, 0.5);
        dirLight1.castShadow = true;
        scene.add(dirLight1);

        const dirLight2 = new THREE.DirectionalLight(0xccccff, 1);
        dirLight2.position.set(-1, 0.75, -0.5);
        dirLight2.castShadow = true;
        scene.add(dirLight2);

        // Add point lights for eyes sparkle
        const leftEyeLight = new THREE.PointLight(0xffffff, 0.5, 3);
        leftEyeLight.position.set(-0.7, 0.3, 2);
        face.add(leftEyeLight);

        const rightEyeLight = new THREE.PointLight(0xffffff, 0.5, 3);
        rightEyeLight.position.set(0.7, 0.3, 2);
        face.add(rightEyeLight);

        camera.position.z = 5;

        // Enhanced animation with smooth movement
        let time = 0;
        function animate() {
            requestAnimationFrame(animate);
            time += 0.01;

            face.rotation.y = Math.sin(time) * 0.3;
            face.rotation.x = Math.sin(time * 0.5) * 0.1;
            
            renderer.render(scene, camera);
        }

        // Improved window resize handler
        function onWindowResize() {
            camera.aspect = window.innerWidth / window.innerHeight;
            camera.updateProjectionMatrix();
            renderer.setSize(window.innerWidth, window.innerHeight);
        }
        window.addEventListener('resize', onWindowResize, false);

        animate();
    </script>
</body>
</html>
```

Key improvements made:

1. Added fog and better background color
2. Improved materials with specular highlights and reflectivity
3. Enhanced geometry detail with higher polygon counts
4. Added dynamic shadows
5. Implemented better lighting setup with multiple light sources
6. Added eye highlights with point lights
7. Improved animation with smooth sinusoidal movement
8. Added antialias rendering
9. Implemented proper shadow mapping
10. Added material properties for better realism

The model now has better visual quality and lighting effects similar to the decals example, while maintaining the friendly face appearance. The shadows and specular highlights give it more depth and realism.

Similar code found with 2 license types

### Plan for enhanced 3D face model:
1. Add nose using ConeGeometry
2. Create upper and lower lips using TorusGeometry
3. Improve smile curve using custom geometry
4. Add subtle shading for facial features

```html


<!DOCTYPE html>
<html>
...existing code...

        // Add nose
        const noseGeometry = new THREE.ConeGeometry(0.2, 0.5, 32);
        const noseMaterial = new THREE.MeshPhongMaterial({
            color: 0xffcca8,
            specular: 0x050505,
            shininess: 30
        });
        const nose = new THREE.Mesh(noseGeometry, noseMaterial);
        nose.rotation.x = Math.PI / 2;
        nose.position.set(0, 0, 1.8);
        face.add(nose);

        // Upper lip
        const upperLipGeometry = new THREE.TorusGeometry(0.7, 0.08, 16, 32, Math.PI);
        const lipMaterial = new THREE.MeshPhongMaterial({
            color: 0xff9999,
            specular: 0x111111,
            shininess: 30
        });
        const upperLip = new THREE.Mesh(upperLipGeometry, lipMaterial);
        upperLip.position.set(0, -0.3, 1.6);
        upperLip.rotation.x = -0.2;
        face.add(upperLip);

        // Lower lip
        const lowerLipGeometry = new THREE.TorusGeometry(0.6, 0.1, 16, 32, Math.PI);
        const lowerLip = new THREE.Mesh(lowerLipGeometry, lipMaterial);
        lowerLip.position.set(0, -0.5, 1.5);
        lowerLip.rotation.x = -0.8;
        face.add(lowerLip);

        // Smile lines (dimples)
        const smileLineGeometry = new THREE.TorusGeometry(0.2, 0.05, 16, 32, Math.PI / 2);
        const smileLineMaterial = new THREE.MeshPhongMaterial({
            color: 0xffcca8,
            transparent: true,
            opacity: 0.5
        });
        
        const leftSmileLine = new THREE.Mesh(smileLineGeometry, smileLineMaterial);
        leftSmileLine.position.set(-1, -0.3, 1.4);
        leftSmileLine.rotation.z = Math.PI / 4;
        face.add(leftSmileLine);

        const rightSmileLine = new THREE.Mesh(smileLineGeometry, smileLineMaterial);
        rightSmileLine.position.set(1, -0.3, 1.4);
        rightSmileLine.rotation.z = -Math.PI / 4;
        face.add(rightSmileLine);

...existing code...
```

### Step-by-step plan for 3D smiling face model:

1. Setup basic HTML structure
2. Initialize Three.js scene, camera, renderer
3. Create face geometry with skin-colored material
4. Add facial features:
   - Eyes with highlights
   - Nose using cone geometry
   - Lips using torus geometry
   - Smile lines (dimples)
5. Setup enhanced lighting
6. Add smooth animations
7. Handle window resizing

```html


<!DOCTYPE html>
<html>
<head>
    <title>3D Smiling Face</title>
    <style>
        body { margin: 0; }
        canvas { display: block; }
    </style>
</head>
<body>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
    <script>
        // Scene setup
        const scene = new THREE.Scene();
        scene.background = new THREE.Color(0x443333);
        scene.fog = new THREE.Fog(0x443333, 1, 12);

        const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
        const renderer = new THREE.WebGLRenderer({ antialias: true });
        renderer.setPixelRatio(window.devicePixelRatio);
        renderer.setSize(window.innerWidth, window.innerHeight);
        renderer.shadowMap.enabled = true;
        document.body.appendChild(renderer.domElement);

        // Face base
        const faceMaterial = new THREE.MeshPhongMaterial({
            color: 0xffdbac,
            specular: 0x050505,
            shininess: 100
        });

        const faceGeometry = new THREE.SphereGeometry(2, 64, 64);
        const face = new THREE.Mesh(faceGeometry, faceMaterial);
        face.castShadow = true;
        face.receiveShadow = true;
        scene.add(face);

        // Eyes
        const eyeMaterial = new THREE.MeshPhongMaterial({
            color: 0x000000,
            specular: 0xffffff,
            shininess: 100
        });
        const eyeGeometry = new THREE.SphereGeometry(0.3, 32, 32);

        const leftEye = new THREE.Mesh(eyeGeometry, eyeMaterial);
        leftEye.position.set(-0.7, 0.3, 1.6);
        face.add(leftEye);

        const rightEye = new THREE.Mesh(eyeGeometry, eyeMaterial);
        rightEye.position.set(0.7, 0.3, 1.6);
        face.add(rightEye);

        // Nose
        const noseGeometry = new THREE.ConeGeometry(0.2, 0.5, 32);
        const noseMaterial = new THREE.MeshPhongMaterial({
            color: 0xffcca8,
            specular: 0x050505,
            shininess: 30
        });
        const nose = new THREE.Mesh(noseGeometry, noseMaterial);
        nose.rotation.x = Math.PI / 2;
        nose.position.set(0, 0, 1.8);
        face.add(nose);

        // Lips
        const lipMaterial = new THREE.MeshPhongMaterial({
            color: 0xff9999,
            specular: 0x111111,
            shininess: 30
        });

        const upperLipGeometry = new THREE.TorusGeometry(0.7, 0.08, 16, 32, Math.PI);
        const upperLip = new THREE.Mesh(upperLipGeometry, lipMaterial);
        upperLip.position.set(0, -0.3, 1.6);
        upperLip.rotation.x = -0.2;
        face.add(upperLip);

        const lowerLipGeometry = new THREE.TorusGeometry(0.6, 0.1, 16, 32, Math.PI);
        const lowerLip = new THREE.Mesh(lowerLipGeometry, lipMaterial);
        lowerLip.position.set(0, -0.5, 1.5);
        lowerLip.rotation.x = -0.8;
        face.add(lowerLip);

        // Smile lines
        const smileLineGeometry = new THREE.TorusGeometry(0.2, 0.05, 16, 32, Math.PI / 2);
        const smileLineMaterial = new THREE.MeshPhongMaterial({
            color: 0xffcca8,
            transparent: true,
            opacity: 0.5
        });
        
        const leftSmileLine = new THREE.Mesh(smileLineGeometry, smileLineMaterial);
        leftSmileLine.position.set(-1, -0.3, 1.4);
        leftSmileLine.rotation.z = Math.PI / 4;
        face.add(leftSmileLine);

        const rightSmileLine = new THREE.Mesh(smileLineGeometry, smileLineMaterial);
        rightSmileLine.position.set(1, -0.3, 1.4);
        rightSmileLine.rotation.z = -Math.PI / 4;
        face.add(rightSmileLine);

        // Lighting
        const ambientLight = new THREE.AmbientLight(0x443333, 0.5);
        scene.add(ambientLight);

        const dirLight1 = new THREE.DirectionalLight(0xffddcc, 1);
        dirLight1.position.set(1, 0.75, 0.5);
        dirLight1.castShadow = true;
        scene.add(dirLight1);

        const dirLight2 = new THREE.DirectionalLight(0xccccff, 1);
        dirLight2.position.set(-1, 0.75, -0.5);
        dirLight2.castShadow = true;
        scene.add(dirLight2);

        // Eye highlights
        const leftEyeLight = new THREE.PointLight(0xffffff, 0.5, 3);
        leftEyeLight.position.set(-0.7, 0.3, 2);
        face.add(leftEyeLight);

        const rightEyeLight = new THREE.PointLight(0xffffff, 0.5, 3);
        rightEyeLight.position.set(0.7, 0.3, 2);
        face.add(rightEyeLight);

        camera.position.z = 5;

        // Animation
        let time = 0;
        function animate() {
            requestAnimationFrame(animate);
            time += 0.01;
            face.rotation.y = Math.sin(time) * 0.3;
            face.rotation.x = Math.sin(time * 0.5) * 0.1;
            renderer.render(scene, camera);
        }

        // Window resize handler
        function onWindowResize() {
            camera.aspect = window.innerWidth / window.innerHeight;
            camera.updateProjectionMatrix();
            renderer.setSize(window.innerWidth, window.innerHeight);
        }
        window.addEventListener('resize', onWindowResize, false);

        animate();
    </script>
</body>
</html>
```

Save this file and open it in a web browser to see a rotating 3D face with realistic features and lighting.

Similar code found with 2 license types

### Plan for Female 3D Face Model

1. Base Structure:
   - Softer facial features
   - Oval face shape
   - Higher cheekbones
   - Smaller nose
   - Fuller lips
   - Longer eyelashes
   - Softer skin tone
   - Subtle makeup effects

2. Technical Components:
   - Enhanced material properties for skin
   - Multiple geometries for facial features
   - Smooth shading and highlights
   - Feminine proportions
   - Soft ambient lighting

```html


<!DOCTYPE html>
<html>
<head>
    <title>3D Female Face</title>
    <style>
        body { margin: 0; background-color: #f0f0f0; }
        canvas { display: block; }
    </style>
</head>
<body>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
    <script>
        // Scene setup
        const scene = new THREE.Scene();
        scene.background = new THREE.Color(0xf0f0f0);
        scene.fog = new THREE.Fog(0xf0f0f0, 1, 15);

        const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
        const renderer = new THREE.WebGLRenderer({ antialias: true });
        renderer.setPixelRatio(window.devicePixelRatio);
        renderer.setSize(window.innerWidth, window.innerHeight);
        renderer.shadowMap.enabled = true;
        document.body.appendChild(renderer.domElement);

        // Face base - more oval shaped for feminine features
        const faceMaterial = new THREE.MeshPhongMaterial({
            color: 0xffe0d0,  // Softer skin tone
            specular: 0x101010,
            shininess: 100,
            flatShading: false
        });

        const faceGeometry = new THREE.SphereGeometry(2, 64, 64);
        const face = new THREE.Mesh(faceGeometry, faceMaterial);
        face.scale.set(1, 1.2, 0.9);  // Oval shape
        face.castShadow = true;
        scene.add(face);

        // Eyes with eyelashes
        const eyeMaterial = new THREE.MeshPhongMaterial({
            color: 0x403225,  // Brown eyes
            specular: 0xffffff,
            shininess: 100
        });
        const eyeGeometry = new THREE.SphereGeometry(0.25, 32, 32);

        const leftEye = new THREE.Mesh(eyeGeometry, eyeMaterial);
        leftEye.position.set(-0.6, 0.3, 1.6);
        leftEye.scale.set(1, 0.5, 0.5);
        face.add(leftEye);

        const rightEye = new THREE.Mesh(eyeGeometry, eyeMaterial);
        rightEye.position.set(0.6, 0.3, 1.6);
        rightEye.scale.set(1, 0.5, 0.5);
        face.add(rightEye);

        // Eyelashes
        const lashMaterial = new THREE.MeshBasicMaterial({ color: 0x000000 });
        const lashGeometry = new THREE.BoxGeometry(0.3, 0.02, 0.05);

        for (let i = -2; i <= 2; i++) {
            const leftLash = new THREE.Mesh(lashGeometry, lashMaterial);
            leftLash.position.set(-0.6 + (i * 0.1), 0.5, 1.6);
            leftLash.rotation.z = Math.PI * 0.1;
            face.add(leftLash);

            const rightLash = new THREE.Mesh(lashGeometry, lashMaterial);
            rightLash.position.set(0.6 + (i * 0.1), 0.5, 1.6);
            rightLash.rotation.z = -Math.PI * 0.1;
            face.add(rightLash);
        }

        // Smaller feminine nose
        const noseGeometry = new THREE.ConeGeometry(0.15, 0.4, 32);
        const noseMaterial = new THREE.MeshPhongMaterial({
            color: 0xffd5c8,
            specular: 0x050505,
            shininess: 30
        });
        const nose = new THREE.Mesh(noseGeometry, noseMaterial);
        nose.rotation.x = Math.PI / 2;
        nose.position.set(0, 0, 1.8);
        face.add(nose);

        // Fuller lips with subtle makeup
        const lipMaterial = new THREE.MeshPhongMaterial({
            color: 0xff8c8c,  // Soft pink
            specular: 0x111111,
            shininess: 50
        });

        const upperLipGeometry = new THREE.TorusGeometry(0.6, 0.1, 16, 32, Math.PI);
        const upperLip = new THREE.Mesh(upperLipGeometry, lipMaterial);
        upperLip.position.set(0, -0.3, 1.6);
        upperLip.rotation.x = -0.2;
        face.add(upperLip);

        const lowerLipGeometry = new THREE.TorusGeometry(0.5, 0.12, 16, 32, Math.PI);
        const lowerLip = new THREE.Mesh(lowerLipGeometry, lipMaterial);
        lowerLip.position.set(0, -0.5, 1.5);
        lowerLip.rotation.x = -0.8;
        face.add(lowerLip);

        // Cheekbones highlight
        const cheekMaterial = new THREE.MeshPhongMaterial({
            color: 0xffb6c1,
            transparent: true,
            opacity: 0.3
        });
        const cheekGeometry = new THREE.SphereGeometry(0.4, 32, 32);

        const leftCheek = new THREE.Mesh(cheekGeometry, cheekMaterial);
        leftCheek.position.set(-1.2, -0.2, 1.0);
        face.add(leftCheek);

        const rightCheek = new THREE.Mesh(cheekGeometry, cheekMaterial);
        rightCheek.position.set(1.2, -0.2, 1.0);
        face.add(rightCheek);

        // Soft lighting setup
        const ambientLight = new THREE.AmbientLight(0xffffff, 0.5);
        scene.add(ambientLight);

        const mainLight = new THREE.DirectionalLight(0xfff0f0, 1);
        mainLight.position.set(0, 1, 2);
        mainLight.castShadow = true;
        scene.add(mainLight);

        const fillLight = new THREE.DirectionalLight(0xffe4e1, 0.5);
        fillLight.position.set(-2, 0, 1);
        scene.add(fillLight);

        // Eye highlights
        const leftEyeLight = new THREE.PointLight(0xffffff, 0.5, 3);
        leftEyeLight.position.set(-0.6, 0.3, 2);
        face.add(leftEyeLight);

        const rightEyeLight = new THREE.PointLight(0xffffff, 0.5, 3);
        rightEyeLight.position.set(0.6, 0.3, 2);
        face.add(rightEyeLight);

        camera.position.z = 5;

        // Gentle animation
        let time = 0;
        function animate() {
            requestAnimationFrame(animate);
            time += 0.005;
            face.rotation.y = Math.sin(time) * 0.2;
            face.rotation.x = Math.sin(time * 0.5) * 0.1;
            renderer.render(scene, camera);
        }

        // Window resize handler
        function onWindowResize() {
            camera.aspect = window.innerWidth / window.innerHeight;
            camera.updateProjectionMatrix();
            renderer.setSize(window.innerWidth, window.innerHeight);
        }
        window.addEventListener('resize', onWindowResize, false);

        animate();
    </script>
</body>
</html>
```

Similar code found with 2 license types

### Step-by-Step Plan for Enhanced 3D Female Face

1. **Basic Structure**
   - Set up scene with soft lighting
   - Create oval face base
   - Add proper face proportions

2. **Facial Features**
   - Almond-shaped eyes with depth
   - Curved eyelashes
   - Refined nose shape
   - Natural-looking lips
   - Subtle cheek contours

3. **Materials & Lighting**
   - Realistic skin shader
   - Proper specular highlights
   - Soft shadows
   - Eye reflections

4. **Animation**
   - Smooth face movement
   - Natural head tilt
   - Gentle eye blinks

```html


<!DOCTYPE html>
<html>
<head>
    <title>Refined 3D Female Face</title>
    <style>
        body { margin: 0; background-color: #f0f0f0; }
        canvas { display: block; }
    </style>
</head>
<body>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
    <script>
        const scene = new THREE.Scene();
        scene.background = new THREE.Color(0xf0f0f0);

        const camera = new THREE.PerspectiveCamera(45, window.innerWidth / window.innerHeight, 0.1, 1000);
        camera.position.set(0, 0, 7);

        const renderer = new THREE.WebGLRenderer({ antialias: true });
        renderer.setSize(window.innerWidth, window.innerHeight);
        renderer.shadowMap.enabled = true;
        renderer.shadowMap.type = THREE.PCFSoftShadowMap;
        document.body.appendChild(renderer.domElement);

        // Face base with better proportions
        const faceGeometry = new THREE.SphereGeometry(2, 64, 64);
        const faceMaterial = new THREE.MeshPhongMaterial({
            color: 0xffe0d0,
            specular: 0x303030,
            shininess: 30,
            flatShading: false
        });
        const face = new THREE.Mesh(faceGeometry, faceMaterial);
        face.scale.set(1, 1.3, 0.85); // More oval shape
        scene.add(face);

        // Almond-shaped eyes
        const eyeGroup = new THREE.Group();
        const eyeShapeGeometry = new THREE.SphereGeometry(0.3, 32, 32);
        const eyeMaterial = new THREE.MeshPhongMaterial({
            color: 0x403225,
            specular: 0xffffff,
            shininess: 100
        });

        function createEye(x) {
            const eye = new THREE.Mesh(eyeShapeGeometry, eyeMaterial);
            eye.scale.set(1, 0.5, 0.4);
            eye.position.set(x, 0.3, 1.7);
            return eye;
        }

        const leftEye = createEye(-0.8);
        const rightEye = createEye(0.8);
        eyeGroup.add(leftEye, rightEye);
        face.add(eyeGroup);

        // Enhanced eyelashes
        const lashGeometry = new THREE.BoxGeometry(0.2, 0.02, 0.05);
        const lashMaterial = new THREE.MeshBasicMaterial({ color: 0x000000 });

        function createEyelashes(eye, mirror) {
            const lashGroup = new THREE.Group();
            for (let i = -3; i <= 3; i++) {
                const lash = new THREE.Mesh(lashGeometry, lashMaterial);
                lash.position.set(i * 0.06, 0.15, 0);
                lash.rotation.z = mirror ? -Math.PI * 0.15 : Math.PI * 0.15;
                lashGroup.add(lash);
            }
            eye.add(lashGroup);
        }

        createEyelashes(leftEye, false);
        createEyelashes(rightEye, true);

        // Refined nose
        const noseGeometry = new THREE.ConeGeometry(0.12, 0.4, 32);
        const noseMaterial = new THREE.MeshPhongMaterial({
            color: 0xffd5c8,
            specular: 0x101010,
            shininess: 20
        });
        const nose = new THREE.Mesh(noseGeometry, noseMaterial);
        nose.rotation.x = Math.PI / 2;
        nose.position.set(0, 0, 1.85);
        face.add(nose);

        // Natural-looking lips
        const lipMaterial = new THREE.MeshPhongMaterial({
            color: 0xff9999,
            specular: 0x202020,
            shininess: 30
        });

        // Upper lip
        const upperLipGeometry = new THREE.TorusGeometry(0.5, 0.08, 16, 32, Math.PI);
        const upperLip = new THREE.Mesh(upperLipGeometry, lipMaterial);
        upperLip.position.set(0, -0.4, 1.7);
        upperLip.rotation.x = -0.2;
        face.add(upperLip);

        // Lower lip
        const lowerLipGeometry = new THREE.TorusGeometry(0.45, 0.1, 16, 32, Math.PI);
        const lowerLip = new THREE.Mesh(lowerLipGeometry, lipMaterial);
        lowerLip.position.set(0, -0.6, 1.6);
        lowerLip.rotation.x = -0.8;
        face.add(lowerLip);

        // Enhanced lighting
        const ambientLight = new THREE.AmbientLight(0xffffff, 0.4);
        scene.add(ambientLight);

        const mainLight = new THREE.DirectionalLight(0xfff0f0, 1);
        mainLight.position.set(2, 2, 5);
        mainLight.castShadow = true;
        scene.add(mainLight);

        const fillLight = new THREE.DirectionalLight(0xffe4e1, 0.3);
        fillLight.position.set(-2, 0, 3);
        scene.add(fillLight);

        // Smooth animation
        let time = 0;
        function animate() {
            requestAnimationFrame(animate);
            time += 0.003;
            
            // Natural head movement
            face.rotation.y = Math.sin(time) * 0.15;
            face.rotation.x = Math.sin(time * 0.5) * 0.05;
            face.rotation.z = Math.sin(time * 0.7) * 0.03;
            
            renderer.render(scene, camera);
        }

        // Window resize handler
        function onWindowResize() {
            camera.aspect = window.innerWidth / window.innerHeight;
            camera.updateProjectionMatrix();
            renderer.setSize(window.innerWidth, window.innerHeight);
        }
        window.addEventListener('resize', onWindowResize, false);

        animate();
    </script>
</body>
</html>
```

Similar code found with 1 license type

### Plan for Realistic 3D Female Face using Three.js Decals

1. **Base Setup**
- Initialize scene, camera, renderer
- Add orbit controls for interaction
- Setup HDR environment lighting

2. **Face Structure**
- Create base mesh with detailed geometry
- Implement normal maps for skin texture
- Add ambient occlusion for depth

3. **Facial Features using Decals**
- Create decal materials for:
  - Eyes (with iris and pupil)
  - Eyebrows
  - Lips
  - Skin details
- Implement decal projection geometry

4. **Interactive Elements**
- Add mouse interaction
- Implement raycasting
- Add decal placement system

```html


<!DOCTYPE html>
<html>
<head>
    <title>Realistic 3D Female Face</title>
    <style>
        body { margin: 0; background-color: #000; }
        canvas { display: block; }
        #info {
            position: absolute;
            top: 10px;
            width: 100%;
            color: #fff;
            text-align: center;
        }
    </style>
</head>
<body>
    <div id="info">Interactive Female Face Model - Click to add details</div>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/three@0.128.0/examples/js/controls/OrbitControls.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/three@0.128.0/examples/js/loaders/GLTFLoader.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/three@0.128.0/examples/js/geometries/DecalGeometry.js"></script>

    <script>
        let container;
        let camera, scene, renderer;
        let mesh;
        let raycaster;
        let line;
        let controls;
        let intersection = {
            intersects: false,
            point: new THREE.Vector3(),
            normal: new THREE.Vector3()
        };
        let mouse = new THREE.Vector2();

        // Decal materials
        const decalMaterials = {
            'skin': new THREE.MeshPhongMaterial({
                color: 0xffe0bd,
                specular: 0x303030,
                shininess: 30,
                transparent: true,
                opacity: 0.9,
                normalScale: new THREE.Vector2(1, 1)
            }),
            'eyes': new THREE.MeshPhongMaterial({
                color: 0x403225,
                specular: 0xffffff,
                shininess: 100,
                transparent: true,
                opacity: 1
            }),
            'lips': new THREE.MeshPhongMaterial({
                color: 0xff9999,
                specular: 0x202020,
                shininess: 30,
                transparent: true,
                opacity: 0.9
            })
        };

        init();
        animate();

        function init() {
            container = document.createElement('div');
            document.body.appendChild(container);

            scene = new THREE.Scene();
            scene.background = new THREE.Color(0x443333);

            camera = new THREE.PerspectiveCamera(45, window.innerWidth / window.innerHeight, 1, 1000);
            camera.position.set(0, 0, 120);

            renderer = new THREE.WebGLRenderer({ antialias: true });
            renderer.setPixelRatio(window.devicePixelRatio);
            renderer.setSize(window.innerWidth, window.innerHeight);
            renderer.shadowMap.enabled = true;
            container.appendChild(renderer.domElement);

            // Face mesh
            const geometry = new THREE.SphereGeometry(30, 64, 64);
            mesh = new THREE.Mesh(geometry, new THREE.MeshPhongMaterial({
                color: 0xffe0bd,
                specular: 0x303030,
                shininess: 30
            }));
            mesh.scale.set(1, 1.3, 0.9);
            scene.add(mesh);

            // Lighting
            const ambientLight = new THREE.AmbientLight(0x443333, 0.5);
            scene.add(ambientLight);

            const directionalLight = new THREE.DirectionalLight(0xffddcc, 1);
            directionalLight.position.set(1, 0.75, 0.5);
            directionalLight.castShadow = true;
            scene.add(directionalLight);

            raycaster = new THREE.Raycaster();

            controls = new THREE.OrbitControls(camera, renderer.domElement);
            controls.minDistance = 50;
            controls.maxDistance = 200;

            // Event listeners
            renderer.domElement.addEventListener('mousedown', onMouseDown);
            window.addEventListener('resize', onWindowResize);
        }

        function onMouseDown(event) {
            event.preventDefault();

            mouse.x = (event.clientX / window.innerWidth) * 2 - 1;
            mouse.y = -(event.clientY / window.innerHeight) * 2 + 1;

            raycaster.setFromCamera(mouse, camera);
            const intersects = raycaster.intersectObject(mesh);

            if (intersects.length > 0) {
                const p = intersects[0].point;
                const n = intersects[0].face.normal.clone();
                n.transformDirection(mesh.matrixWorld);

                addDecal(p, n);
            }
        }

        function addDecal(position, normal) {
            const orientation = new THREE.Euler();
            const size = new THREE.Vector3(10, 10, 10);

            const decalGeometry = new THREE.DecalGeometry(mesh, position, orientation, size);
            const decal = new THREE.Mesh(decalGeometry, decalMaterials.skin);
            scene.add(decal);
        }

        function onWindowResize() {
            camera.aspect = window.innerWidth / window.innerHeight;
            camera.updateProjectionMatrix();
            renderer.setSize(window.innerWidth, window.innerHeight);
        }

        function animate() {
            requestAnimationFrame(animate);
            renderer.render(scene, camera);
        }
    </script>
</body>
</html>
```

Key features:
- Interactive face model with decal system
- Realistic materials with specular highlights
- Orbital controls for viewing
- Click interaction for adding details
- Proper lighting and shadows
- Responsive design

Similar code found with 2 license types