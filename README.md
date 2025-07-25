<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
    <title>Horror Feed Indonesia</title>
    <meta name="description" content="Cerita horor Indonesia dari TikTok, YouTube, dan Instagram. Plus AI gambar horor!">
    <meta name="keywords" content="horor, Indonesia, cerita, AI, TikTok, YouTube, Instagram, horror image generator">
    <meta name="author" content="Horror Feed ID">
    <link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;800&display=swap" />
    <style>
        html, body {
            margin: 0;
            font-family: 'Inter', sans-serif;
            background-color: #0a0a0a;
            color: white;
            overflow-x: hidden;
            scroll-behavior: smooth;
        }

        .navbar {
            position: fixed;
            top: 0;
            width: 100%;
            background-color: #111;
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 1rem 2rem;
            z-index: 1000;
        }

        .logo {
            font-size: 1.5rem;
            font-weight: 800;
            color: red;
        }

        .nav-links a {
            color: #ccc;
            text-decoration: none;
            margin-left: 1rem;
            font-weight: 500;
        }

        .nav-links a:hover,
        .nav-link.active {
            color: white;
        }

        .hero {
            height: 100vh;
            background: linear-gradient(to bottom, rgba(0,0,0,0.8), rgba(0,0,0,0.9)),
                url('https://images.unsplash.com/photo-1520637836862-4d197d17c87a?w=1920&fit=crop') center/cover no-repeat;
            display: flex;
            align-items: center;
            justify-content: center;
            padding-top: 70px;
            text-align: center;
        }

        .hero h1 {
            font-size: 3rem;
            background: linear-gradient(90deg, white, red);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .hero p {
            font-size: 1.2rem;
            color: #ccc;
            margin: 1rem 0;
        }

        .btn {
            padding: 0.8rem 1.5rem;
            margin: 0.5rem;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-weight: 600;
        }

        .btn-primary {
            background-color: white;
            color: black;
        }

        .btn-secondary {
            background-color: transparent;
            color: white;
            border: 1px solid white;
        }

        section.content {
            padding: 4rem 2rem;
        }

        .section-title {
            font-size: 2rem;
            margin-bottom: 1rem;
        }

        .carousel {
            display: flex;
            gap: 1rem;
            overflow-x: auto;
        }

        .horror-card {
            min-width: 300px;
            background: #1a1a1a;
            border: 1px solid #333;
            border-radius: 10px;
            overflow: hidden;
        }

        .horror-card img {
            width: 100%;
            height: 180px;
            object-fit: cover;
        }

        .horror-card .card-content {
            padding: 1rem;
        }

        .generator-section {
            margin-top: 3rem;
            background-color: #111;
            padding: 2rem;
            border-radius: 10px;
        }

        .form-textarea {
            width: 100%;
            height: 100px;
            padding: 1rem;
            background: #222;
            color: white;
            border: 1px solid #444;
            border-radius: 5px;
            resize: vertical;
        }

        .generate-btn {
            margin-top: 1rem;
            width: 100%;
            padding: 1rem;
            background: red;
            color: white;
            border: none;
            border-radius: 8px;
            font-weight: bold;
            font-size: 1rem;
            cursor: pointer;
        }

        .images-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 1rem;
            margin-top: 2rem;
        }

        .image-item img {
            width: 100%;
            height: 200px;
            object-fit: cover;
            border-radius: 8px;
        }

        footer {
            text-align: center;
            padding: 2rem;
            color: #666;
            background: #000;
        }
    </style>
</head>
<body>
    <nav class="navbar">
        <div class="logo">HORROR FEED</div>
        <div class="nav-links">
            <a href="#">Beranda</a>
            <a href="#">TikTok</a>
            <a href="#">YouTube</a>
            <a href="#">Instagram</a>
        </div>
    </nav>

    <section class="hero">
        <div>
            <h1>Cerita Horor Indonesia</h1>
            <p>Penampakan, pocong, santet dan kisah nyata dari seluruh Nusantara.</p>
            <button class="btn btn-primary" onclick="scrollToContent()">▶ Mulai</button>
            <button class="btn btn-secondary">ℹ Info</button>
        </div>
    </section>

    <section class="content" id="content">
        <h2 class="section-title">🔥 Trending Hari Ini</h2>
        <div class="carousel" id="carousel-container"></div>

        <div class="generator-section">
            <h2 class="section-title">🎨 Generator Gambar AI</h2>
            <textarea class="form-textarea" id="imagePrompt" placeholder="Contoh: pocong berdiri di tengah kuburan berkabut..."></textarea>
            <button class="generate-btn" onclick="generateImages()">🎨 Buat Gambar</button>
            <div class="images-grid" id="imagesGrid"></div>
        </div>
    </section>

    <footer>
        &copy; 2025 Horror Feed Indonesia
    </footer>

    <script>
        const horrorContent = [
            {
                title: "Penampakan di kosan",
                description: "Mahasiswa melihat bayangan misterius lewat kaca.",
                image: "https://images.unsplash.com/photo-1544207240-66d3e1c39d68?w=300&h=180&fit=crop"
            },
            {
                title: "Ritual Santet di desa",
                description: "Video menampilkan ritual kuno dan suara-suara aneh.",
                image: "https://images.unsplash.com/photo-1518709268805-4e9042af2176?w=300&h=180&fit=crop"
            },
            {
                title: "Sosok putih di pemakaman",
                description: "Foto viral menunjukkan penampakan tak dikenal.",
                image: "https://images.unsplash.com/photo-1509909756405-be0199881695?w=300&h=180&fit=crop"
            }
        ];

        const horrorImages = [
            "https://images.unsplash.com/photo-1520637836862-4d197d17c87a?w=400&h=400&fit=crop",
            "https://images.unsplash.com/photo-1518709268805-4e9042af2176?w=400&h=400&fit=crop",
            "https://images.unsplash.com/photo-1509909756405-be0199881695?w=400&h=400&fit=crop"
        ];

        function scrollToContent() {
            document.getElementById("content").scrollIntoView({ behavior: "smooth" });
        }

        function generateImages() {
            const prompt = document.getElementById("imagePrompt").value;
            const grid = document.getElementById("imagesGrid");
            if (!prompt) {
                alert("Isi deskripsi dulu, dong!");
                return;
            }

            grid.innerHTML = "";
            for (let i = 0; i < 3; i++) {
                const imgURL = horrorImages[Math.floor(Math.random() * horrorImages.length)];
                const div = document.createElement("div");
                div.className = "image-item";
                div.innerHTML = `<img src="${imgURL}" alt="Generated Horror Image">`;
                grid.appendChild(div);
            }
        }

        function loadCarousel() {
            const container = document.getElementById("carousel-container");
            horrorContent.forEach(item => {
                const card = document.createElement("div");
                card.className = "horror-card";
                card.innerHTML = `
                    <img src="${item.image}" alt="${item.title}">
                    <div class="card-content">
                        <h3>${item.title}</h3>
                        <p>${item.description}</p>
                    </div>
                `;
                container.appendChild(card);
            });
        }

        document.addEventListener("DOMContentLoaded", loadCarousel);
    </script>
</body>
</html>
