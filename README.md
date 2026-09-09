# AndrewSamekh.io
<!DOCTYPE html>
<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>3D Portfolio - Developer & Creator</title>
    <!-- Google Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Kanit:wght@300;400;600&family=Poppins:wght@300;500;700&display=swap" rel="stylesheet">
    
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Poppins', 'Kanit', sans-serif;
        }

        body {
            background-color: #0b0c10;
            color: #ffffff;
            overflow-x: hidden;
        }

        /* Canvas สำหรับ Three.js พื้นหลัง */
        #webgl-bg {
            position: fixed;
            top: 0;
            left: 0;
            width: 100vw;
            height: 100vh;
            z-index: -1;
            pointer-events: none;
        }

        /* Navbar */
        nav {
            position: fixed;
            top: 0;
            width: 100%;
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 20px 8%;
            background: rgba(11, 12, 16, 0.6);
            backdrop-filter: blur(10px);
            z-index: 100;
            border-bottom: 1px solid rgba(255, 255, 255, 0.05);
        }

        .logo {
            font-size: 1.5rem;
            font-weight: 700;
            letter-spacing: 1px;
            color: #4e54c8;
            background: linear-gradient(45deg, #00f2fe, #4e54c8);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        nav ul {
            display: flex;
            list-style: none;
            gap: 30px;
        }

        nav a {
            color: #c5c6c7;
            text-decoration: none;
            font-size: 0.95rem;
            transition: 0.3s;
        }

        nav a:hover {
            color: #66fcf1;
        }

        /* Section Layouts */
        section {
            min-height: 100vh;
            padding: 100px 8% 60px 8%;
            display: flex;
            flex-direction: column;
            justify-content: center;
        }

        /* Hero Section */
        .hero {
            align-items: flex-start;
        }

        .hero h1 {
            font-size: 4rem;
            line-height: 1.1;
            margin-bottom: 15px;
            background: linear-gradient(to right, #fff, #c5c6c7);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .hero h1 span {
            background: linear-gradient(45deg, #00f2fe, #4e54c8);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .hero p {
            font-size: 1.2rem;
            color: #a0a5b5;
            max-width: 550px;
            margin-bottom: 30px;
            font-weight: 300;
        }

        .btn {
            display: inline-block;
            padding: 12px 32px;
            background: linear-gradient(45deg, #00f2fe, #4e54c8);
            color: #fff;
            text-decoration: none;
            border-radius: 30px;
            font-weight: 500;
            box-shadow: 0 10px 20px rgba(0, 242, 254, 0.2);
            transition: transform 0.3s, box-shadow 0.3s;
        }

        .btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 15px 25px rgba(0, 242, 254, 0.3);
        }

        /* Work / Projects Section */
        .section-title {
            font-size: 2.5rem;
            margin-bottom: 40px;
            text-align: center;
            position: relative;
        }

        .projects-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 30px;
            margin-top: 20px;
        }

        .project-card {
            background: rgba(255, 255, 255, 0.03);
            border: 1px solid rgba(255, 255, 255, 0.08);
            border-radius: 16px;
            padding: 30px;
            backdrop-filter: blur(5px);
            transition: transform 0.3s, border-color 0.3s;
        }

        .project-card:hover {
            transform: translateY(-10px);
            border-color: rgba(0, 242, 254, 0.4);
        }

        .project-card h3 {
            font-size: 1.4rem;
            margin-bottom: 12px;
            color: #66fcf1;
        }

        .project-card p {
            color: #a0a5b5;
            font-size: 0.95rem;
            line-height: 1.6;
        }

        /* About & Skills */
        .skills-container {
            display: flex;
            flex-wrap: wrap;
            gap: 15px;
            justify-content: center;
            margin-top: 20px;
        }

        .skill-tag {
            background: rgba(78, 84, 200, 0.15);
            border: 1px solid rgba(78, 84, 200, 0.3);
            padding: 8px 20px;
            border-radius: 20px;
            font-size: 0.9rem;
            color: #45f3ff;
        }

        /* Footer */
        footer {
            text-align: center;
            padding: 30px;
            color: #666;
            font-size: 0.85rem;
            border-top: 1px solid rgba(255, 255, 255, 0.05);
        }

        /* Responsive */
        @media (max-width: 768px) {
            .hero h1 { font-size: 2.8rem; }
            nav ul { display: none; } /* ซ่อนเมนูสำหรับหน้าจอเล็ก (ทำเพิ่มเติมได้ตามต้องการ) */
        }
    </style>

    <!-- Import Three.js Library จาก CDN -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
</head>
<body>

    <!-- 3D Canvas Background -->
    <canvas id="webgl-bg"></canvas>

    <!-- Navigation -->
    <nav>
        <div class="logo">PORTFOLIO.3D</div>
        <ul>
            <li><a href="#hero">Home</a></li>
            <li><a href="#projects">Projects</a></li>
            <li><a href="#about">About</a></li>
            <li><a href="#contact">Contact</a></li>
        </ul>
    </nav>

    <!-- Hero Section -->
    <section id="hero" class="hero">
        <h1>Creative <span>3D & Interactive</span> Developer</h1>
        <p>ยินดีต้อนรับสู่พื้นที่รวบรวมผลงาน 3D Web Experience, Interactive Design และ Web Development</p>
        <a href="#projects" class="btn">รับชมผลงาน</a>
    </section>

    <!-- Projects Section -->
    <section id="projects">
        <h2 class="section-title">Featured Projects</h2>
        <div class="projects-grid">
            <div class="project-card">
                <h3>01. Interactive 3D Web</h3>
                <p>การพัฒนาเว็บไซต์ตอบสนองแบบ 3 มิติโดยใช้ Three.js และ WebGL เพื่อสร้างประสบการณ์ใหม่ๆ ให้ผู้ใช้งาน</p>
            </div>
            <div class="project-card">
                <h3>02. Shader & VFX Effects</h3>
                <p>การใช้ Custom GLSL Shaders สร้างเอฟเฟกต์แสง สี และ Particle visual ที่ปรับแต่งเองได้ตามต้องการ</p>
            </div>
            <div class="project-card">
                <h3>03. Game & Simulation</h3>
                <p>การพัฒนาต้นแบบระบบฟิสิกส์และการเคลื่อนที่วัตถุบนเบราว์เซอร์ รวมถึงการนำเสนอโมเดล 3D แบบเรียลไทม์</p>
            </div>
        </div>
    </section>

    <!-- About & Skills Section -->
    <section id="about">
        <h2 class="section-title">Skills & Tech Stack</h2>
        <div class="skills-container">
            <span class="skill-tag">Three.js</span>
            <span class="skill-tag">WebGL</span>
            <span class="skill-tag">JavaScript / ES6</span>
            <span class="skill-tag">GLSL Shaders</span>
            <span class="skill-tag">HTML5 / CSS3</span>
            <span class="skill-tag">Blender / 3D Modeling</span>
            <span class="skill-tag">Git</span>
        </div>
    </section>

    <!-- Contact Section -->
    <section id="contact" style="text-align: center;">
        <h2 class="section-title">Get In Touch</h2>
        <p style="color: #a0a5b5; margin-bottom: 30px;">สนใจร่วมงาน หรือสอบถามรายละเอียดเพิ่มเติม สามารถติดต่อได้ที่</p>
        <div>
            <a href="mailto:your.email@example.com" class="btn">ส่งข้อความหาเรา</a>
        </div>
    </section>

    <footer>
        <p>© 2026 3D Portfolio. Powered by Three.js</p>
    </footer>

    <!-- Three.js Logic Script -->
    <script>
        // 1. Scene, Camera, Renderer Setup
        const scene = new THREE.Scene();
        
        // เพิ่ม Fog ให้ฉากลึกขึ้นและกลมกลืนกับพื้นหลัง
        scene.fog = new THREE.FogExp2(0x0b0c10, 0.05);

        const camera = new THREE.PerspectiveCamera(
            75, 
            window.innerWidth / window.innerHeight, 
            0.1, 
            1000
        );
        camera.position.z = 5;

        const canvas = document.querySelector('#webgl-bg');
        const renderer = new THREE.WebGLRenderer({
            canvas: canvas,
            antialias: true,
            alpha: true
        });
        renderer.setSize(window.innerWidth, window.innerHeight);
        renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));

        // 2. Add 3D Object (Main Interactive Mesh - Torus Knot)
        const geometry = new THREE.TorusKnotGeometry(1, 0.3, 128, 32);
        const material = new THREE.MeshStandardMaterial({
            color: 0x4e54c8,
            roughness: 0.2,
            metalness: 0.8,
            wireframe: false
        });
        const mainMesh = new THREE.Mesh(geometry, material);
        scene.add(mainMesh);

        // 3. Add Background Particles (ละอองดาวรอบๆ)
        const particlesCount = 700;
        const particlesGeometry = new THREE.BufferGeometry();
        const positions = new Float32Array(particlesCount * 3);

        for (let i = 0; i < particlesCount * 3; i++) {
            positions[i] = (Math.random() - 0.5) * 15;
        }

        particlesGeometry.setAttribute('position', new THREE.BufferAttribute(positions, 3));

        const particlesMaterial = new THREE.PointsMaterial({
            size: 0.02,
            color: 0x66fcf1,
            transparent: true,
            opacity: 0.7
        });

        const particlesMesh = new THREE.Points(particlesGeometry, particlesMaterial);
        scene.add(particlesMesh);

        // 4. Lighting Setup
        const ambientLight = new THREE.AmbientLight(0xffffff, 0.5);
        scene.add(ambientLight);

        const pointLight1 = new THREE.PointLight(0x00f2fe, 2);
        pointLight1.position.set(5, 5, 5);
        scene.add(pointLight1);

        const pointLight2 = new THREE.PointLight(0x4e54c8, 2);
        pointLight2.position.set(-5, -5, -2);
        scene.add(pointLight2);

        // 5. Mouse Interactivity (ขยับวัตถุตามเมาส์)
        let mouseX = 0;
        let mouseY = 0;

        window.addEventListener('mousemove', (event) => {
            mouseX = (event.clientX / window.innerWidth - 0.5) * 2;
            mouseY = -(event.clientY / window.innerHeight - 0.5) * 2;
        });

        // 6. Scroll Animation (ขยับกล้องเมื่อ Scroll หน้าเว็บ)
        let scrollY = 0;
        window.addEventListener('scroll', () => {
            scrollY = window.scrollY;
        });

        // 7. Window Resize Handler
        window.addEventListener('resize', () => {
            camera.aspect = window.innerWidth / window.innerHeight;
            camera.updateProjectionMatrix();
            renderer.setSize(window.innerWidth, window.innerHeight);
            renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
        });

        // 8. Animation Loop
        const clock = new THREE.Clock();

        const animate = () => {
            const elapsedTime = clock.getElapsedTime();

            // หมุนโมเดลหลัก
            mainMesh.rotation.x = elapsedTime * 0.3;
            mainMesh.rotation.y = elapsedTime * 0.2;

            // หมุน Particle
            particlesMesh.rotation.y = elapsedTime * 0.05;

            // ตอบสนองการเลื่อนเมาส์ (Smooth Interpolation / Lerp)
            mainMesh.rotation.x += mouseY * 0.05;
            mainMesh.rotation.y += mouseX * 0.05;

            // เลื่อนกล้องตามการ Scroll หน้าเว็บ
            camera.position.y = -scrollY * 0.003;
            camera.position.z = 5 + (scrollY * 0.001);

            // Render
            renderer.render(scene, camera);
            requestAnimationFrame(animate);
        };

        animate();
    </script>
</body>
</html>
