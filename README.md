<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Horror Feed Indonesia</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background: #0a0a0a;
            color: #ffffff;
            font-family: 'Inter', sans-serif;
            min-height: 100vh;
            overflow-x: hidden;
        }

        .navbar {
            position: fixed;
            top: 0;
            width: 100%;
            background: rgba(10, 10, 10, 0.95);
            backdrop-filter: blur(20px);
            z-index: 1000;
            padding: 15px 40px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            transition: all 0.3s ease;
        }

        .logo {
            font-size: 2rem;
            font-weight: 800;
            background: linear-gradient(135deg, #ff0000, #cc0000);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .nav-links {
            display: flex;
            gap: 30px;
        }

        .nav-link {
            color: #cccccc;
            text-decoration: none;
            font-weight: 500;
            padding: 8px 16px;
            border-radius: 20px;
            transition: all 0.3s ease;
            cursor: pointer;
        }

        .nav-link:hover, .nav-link.active {
            color: #ffffff;
            background: rgba(255, 0, 0, 0.2);
        }

        .hero {
            height: 100vh;
            background: linear-gradient(rgba(0,0,0,0.7), rgba(0,0,0,0.7)), 
                        linear-gradient(45deg, #1a0000, #330000);
            display: flex;
            align-items: center;
            padding: 0 40px;
            position: relative;
        }

        .hero::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: radial-gradient(circle at 20% 50%, rgba(255,0,0,0.1) 0%, transparent 50%),
                        radial-gradient(circle at 80% 20%, rgba(255,0,0,0.1) 0%, transparent 50%);
            pointer-events: none;
        }

        .hero-content {
            max-width: 600px;
            position: relative;
            z-index: 2;
        }

        .hero-title {
            font-size: 4rem;
            font-weight: 800;
            margin-bottom: 20px;
            background: linear-gradient(135deg, #ffffff, #ff6b6b);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .hero-subtitle {
            font-size: 1.3rem;
            color: #e0e0e0;
            margin-bottom: 30px;
            line-height: 1.5;
        }

        .hero-buttons {
            display: flex;
            gap: 20px;
        }

        .btn-primary {
            background: linear-gradient(135deg, #ffffff, #f0f0f0);
            color: #000000;
            padding: 15px 30px;
            border: none;
            border-radius: 8px;
            font-weight: 700;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .btn-primary:hover {
            transform: translateY(-3px);
            box-shadow: 0 10px 30px rgba(255,255,255,0.2);
        }

        .btn-secondary {
            background: rgba(255,255,255,0.1);
            color: #ffffff;
            padding: 15px 30px;
            border: 2px solid rgba(255,255,255,0.3);
            border-radius: 8px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .btn-secondary:hover {
            background: rgba(255,255,255,0.2);
        }

        .content {
            padding: 80px 40px;
            background: #111111;
        }

        .content-row {
            margin-bottom: 60px;
        }

        .section-title {
            font-size: 2rem;
            font-weight: 700;
            margin-bottom: 30px;
            color: #ffffff;
            position: relative;
            padding-left: 20px;
        }

        .section-title::before {
            content: '';
            position: absolute;
            left: 0;
            top: 50%;
            transform: translateY(-50%);
            width: 4px;
            height: 30px;
            background: linear-gradient(135deg, #ff0000, #cc0000);
            border-radius: 2px;
        }

        .carousel {
            display: flex;
            gap: 20px;
            overflow-x: auto;
            padding: 20px 0;
            scroll-behavior: smooth;
        }

        .carousel::-webkit-scrollbar {
            height: 6px;
        }

        .carousel::-webkit-scrollbar-track {
            background: rgba(255,255,255,0.1);
            border-radius: 3px;
        }

        .carousel::-webkit-scrollbar-thumb {
            background: #ff0000;
            border-radius: 3px;
        }

        .horror-card {
            min-width: 300px;
            background: linear-gradient(145deg, #1a1a1a, #0f0f0f);
            border-radius: 12px;
            overflow: hidden;
            transition: all 0.3s ease;
            cursor: pointer;
            position: relative;
            border: 1px solid rgba(255,255,255,0.1);
        }

        .horror-card:hover {
            transform: scale(1.05) translateY(-5px);
            box-shadow: 0 15px 40px rgba(255,0,0,0.2);
        }

        .card-image {
            width: 100%;
            height: 180px;
            background: linear-gradient(45deg, #2a0000, #4a0000);
            display: flex;
            align-items: center;
            justify-content: center;
            color: #666;
            font-size: 3rem;
        }

        .card-content {
            padding: 20px;
        }

        .card-title {
            font-size: 1.1rem;
            font-weight: 700;
            margin-bottom: 10px;
            color: #ffffff;
        }

        .card-description {
            font-size: 0.9rem;
            color: #cccccc;
            line-height: 1.4;
            margin-bottom: 15px;
        }

        .card-meta {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .platform-tag {
            background: linear-gradient(135deg, #ff0000, #cc0000);
            color: #ffffff;
            padding: 4px 12px;
            border-radius: 15px;
            font-size: 0.7rem;
            font-weight: 600;
            text-transform: uppercase;
        }

        .timestamp {
            color: #aaaaaa;
            font-size: 0.8rem;
        }

        .generator-section {
            margin-top: 60px;
            background: linear-gradient(145deg, #1a1a1a, #111111);
            border-radius: 16px;
            padding: 40px;
            border: 2px solid rgba(255,0,0,0.2);
        }

        .generator-header {
            text-align: center;
            margin-bottom: 30px;
        }

        .generator-title {
            font-size: 1.8rem;
            font-weight: 700;
            margin-bottom: 10px;
            background: linear-gradient(135deg, #ff6b6b, #ff0000);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .generator-subtitle {
            color: #cccccc;
            font-size: 1rem;
        }

        .form-group {
            margin-bottom: 25px;
        }

        .form-label {
            display: block;
            color: #ffffff;
            font-weight: 600;
            margin-bottom: 10px;
        }

        .form-textarea {
            width: 100%;
            height: 100px;
            background: rgba(30,30,30,0.8);
            border: 2px solid rgba(255,255,255,0.2);
            border-radius: 8px;
            color: #ffffff;
            padding: 15px;
            font-family: inherit;
            resize: vertical;
            outline: none;
        }

        .form-textarea:focus {
            border-color: rgba(255,0,0,0.5);
        }

        .button-group {
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
            margin-bottom: 25px;
        }

        .option-btn {
            background: rgba(40,40,40,0.8);
            color: #cccccc;
            border: 1px solid rgba(255,255,255,0.2);
            border-radius: 20px;
            padding: 8px 16px;
            font-size: 0.9rem;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .option-btn:hover {
            background: rgba(255,255,255,0.1);
        }

        .option-btn.active {
            background: linear-gradient(135deg, #ff0000, #cc0000);
            color: #ffffff;
            border-color: #ff0000;
        }

        .generate-btn {
            width: 100%;
            background: linear-gradient(135deg, #ff0000, #cc0000);
            color: #ffffff;
            border: none;
            border-radius: 8px;
            padding: 18px;
            font-size: 1.1rem;
            font-weight: 700;
            cursor: pointer;
            transition: all 0.3s ease;
            margin-bottom: 30px;
        }

        .generate-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 30px rgba(255,0,0,0.3);
        }

        .generate-btn:disabled {
            opacity: 0.6;
            cursor: not-allowed;
            transform: none;
        }

        .images-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin-top: 20px;
        }

        .image-item {
            background: #222222;
            border-radius: 8px;
            overflow: hidden;
            border: 1px solid rgba(255,255,255,0.1);
        }

        .generated-image {
            width: 100%;
            height: 200px;
            background: linear-gradient(45deg, #2a0000, #4a0000);
            display: flex;
            align-items: center;
            justify-content: center;
            color: #666;
            font-size: 2rem;
        }

        .image-actions {
            padding: 15px;
            display: flex;
            gap: 10px;
        }

        .download-btn {
            flex: 1;
            background: #00aa00;
            color: #ffffff;
            border: none;
            border-radius: 6px;
            padding: 10px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .download-btn:hover {
            background: #00cc00;
        }

        .alert {
            padding: 15px;
            border-radius: 8px;
            margin: 15px 0;
            text-align: center;
            font-weight: 600;
        }

        .alert-success {
            background: rgba(0,255,0,0.1);
            border: 1px solid rgba(0,255,0,0.3);
            color: #00ff00;
        }

        .alert-error {
            background: rgba(255,0,0,0.1);
            border: 1px solid rgba(255,0,0,0.3);
            color: #ff6b6b;
        }

        .loading-spinner {
            display: inline-block;
            width: 20px;
            height: 20px;
            border: 2px solid rgba(255,255,255,0.3);
            border-top: 2px solid #ffffff;
            border-radius: 50%;
            animation: spin 1s linear infinite;
            margin-right: 10px;
        }

        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        @media (max-width: 768px) {
            .navbar {
                padding: 15px 20px;
            }

            .nav-links {
                gap: 15px;
            }

            .hero {
                padding: 0 20px;
                text-align: center;
            }

            .hero-title {
                font-size: 2.5rem;
            }

            .content {
                padding: 60px 20px;
            }

            .horror-card {
                min-width: 250px;
            }

            .generator-section {
                padding: 25px;
            }
        }
    </style>
</head>
<body>
    <nav class="navbar">
        <div class="logo">HORROR FEED</div>
        <div class="nav-links">
            <div class="nav-link active">Beranda</div>
            <div class="nav-link">TikTok</div>
            <div class="nav-link">YouTube</div>
            <div class="nav-link">Instagram</div>
        </div>
    </nav>

    <section class="hero">
        <div class="hero-content">
            <h1 class="hero-title">Cerita Horor<br>Indonesia</h1>
            <p class="hero-subtitle">Temukan kisah-kisah menyeramkan dari seluruh nusantara. Dari penampakan mistis hingga ritual kuno yang mengerikan.</p>
            <div class="hero-buttons">
                <button class="btn-primary" onclick="scrollToContent()">
                    ▶ Mulai Menonton
                </button>
                <button class="btn-secondary">
                    ℹ Info Selengkapnya
                </button>
            </div>
        </div>
    </section>

    <section class="content" id="content">
        <div class="content-row">
            <h2 class="section-title">🔥 Trending Hari Ini</h2>
            <div class="carousel" id="trending-carousel">
                <!-- Content will be loaded here -->
            </div>
        </div>

        <div class="content-row">
            <h2 class="section-title">📱 Cerita TikTok Viral</h2>
            <div class="carousel" id="tiktok-carousel">
                <!-- Content will be loaded here -->
            </div>
        </div>

        <div class="generator-section">
            <div class="generator-header">
                <h3 class="generator-title">🎨 Generator Gambar Horor AI</h3>
                <p class="generator-subtitle">Buat gambar horor mengerikan dengan teknologi AI</p>
            </div>

            <div class="form-group">
                <label class="form-label">Deskripsi Gambar Horror:</label>
                <textarea class="form-textarea" id="image-prompt" placeholder="Contoh: Hantu pocong putih di kuburan tua dengan kabut tebal, suasana malam yang mengerikan..."></textarea>
            </div>

            <div class="form-group">
                <label class="form-label">Gaya Horror:</label>
                <div class="button-group">
                    <button class="option-btn active" data-style="realistic">📸 Realistis</button>
                    <button class="option-btn" data-style="gothic">🏰 Gothic</button>
                    <button class="option-btn" data-style="dark">🌙 Dark</button>
                    <button class="option-btn" data-style="vintage">📰 Vintage</button>
                </div>
            </div>

            <div class="form-group">
                <label class="form-label">Tema Horror Indonesia:</label>
                <div class="button-group">
                    <button class="option-btn" data-theme="pocong">👻 Pocong</button>
                    <button class="option-btn" data-theme="kuntilanak">👤 Kuntilanak</button>
                    <button class="option-btn" data-theme="tuyul">👹 Tuyul</button>
                    <button class="option-btn" data-theme="santet">🔮 Santet</button>
                </div>
            </div>

            <button class="generate-btn" id="generate-btn">
                🎨 Generate Gambar Horror
            </button>

            <div id="alert-container"></div>
            <div class="images-grid" id="images-grid"></div>
        </div>
    </section>

    <script>
        // Horror content data
        const horrorContent = [
            {
                platform: 'tiktok',
                title: 'Penampakan Misterius di Kos Jakarta',
                description: 'Mahasiswa mengalami kejadian aneh di kos. Suara langkah kaki malam hari dan pintu terbuka sendiri.',
                icon: '👻',
                timestamp: '5 menit lalu'
            },
            {
                platform: 'youtube',
                title: 'Ritual Santet di Desa Terpencil',
                description: 'Dokumenter tentang praktik santet di Jawa Tengah dengan kesaksian korban.',
                icon: '🔮',
                timestamp: '12 menit lalu'
            },
            {
                platform: 'instagram',
                title: 'Foto Pocong di Kuburan Tua',
                description: 'Foto ziarah kubur menunjukkan sosok putih mencurigakan di belakang makam.',
                icon: '⚰️',
                timestamp: '18 menit lalu'
            },
            {
                platform: 'tiktok',
                title: 'Suara Tangisan dari Rumah Kosong',
                description: 'Video viral merekam tangisan misterius dari rumah kosong 10 tahun.',
                icon: '🏚️',
                timestamp: '25 menit lalu'
            },
            {
                platform: 'youtube',
                title: 'Misteri Boneka Haunted',
                description: 'Koleksi boneka antik yang bergerak sendiri di malam hari.',
                icon: '🪆',
                timestamp: '30 menit lalu'
            },
            {
                platform: 'instagram',
                title: 'Kuntilanak di Hutan Jati',
                description: 'Pendaki gunung mengabadikan sosok perempuan berambut panjang.',
                icon: '🌲',
                timestamp: '45 menit lalu'
            }
        ];

        // Initialize page
        document.addEventListener('DOMContentLoaded', function() {
            loadContent();
            setupEventListeners();
            loadSampleImages();
        });

        // Load content into carousels
        function loadContent() {
            const trendingCarousel = document.getElementById('trending-carousel');
            const tiktokCarousel = document.getElementById('tiktok-carousel');

            // Load trending content
            trendingCarousel.innerHTML = generateCarouselHTML(horrorContent);
            
            // Load TikTok content
            const tiktokContent = horrorContent.filter(item => item.platform === 'tiktok');
            tiktokCarousel.innerHTML = generateCarouselHTML(tiktokContent.concat(tiktokContent)); // Duplicate for more content
        }

        // Generate carousel HTML
        function generateCarouselHTML(items) {
            return items.map(item => `
                <div class="horror-card">
                    <div class="card-image">${item.icon}</div>
                    <div class="card-content">
                        <h3 class="card-title">${item.title}</h3>
                        <p class="card-description">${item.description}</p>
                        <div class="card-meta">
                            <span class="platform-tag">${item.platform}</span>
                            <span class="timestamp">${item.timestamp}</span>
                        </div>
                    </div>
                </div>
            `).join('');
        }

        // Setup event listeners
        function setupEventListeners() {
            // Style buttons
            document.querySelectorAll('.option-btn[data-style]').forEach(btn => {
                btn.addEventListener('click', function() {
                    document.querySelectorAll('.option-btn[data-style]').forEach(b => b.classList.remove('active'));
                    this.classList.add('active');
                });
            });

            // Theme buttons (multiple selection)
            document.querySelectorAll('.option-btn[data-theme]').forEach(btn => {
                btn.addEventListener('click', function() {
                    this.classList.toggle('active');
                });
            });

            // Generate button
            document.getElementById('generate-btn').addEventListener('click', generateImages);
        }

        // Generate horror images
        async function generateImages() {
            const generateBtn = document.getElementById('generate-btn');
            const prompt = document.getElementById('image-prompt').value.trim();
            const alertContainer = document.getElementById('alert-container');
            const imagesGrid = document.getElementById('images-grid');

            if (!prompt) {
                showAlert('Mohon masukkan deskripsi gambar!', 'error');
                return;
            }

            // Show loading
            generateBtn.disabled = true;
            generateBtn.innerHTML = '<span class="loading-spinner"></span>Generating...';

            try {
                // Simulate API call
                await new Promise(resolve => setTimeout(resolve, 2000));

                // Generate placeholder images
                const numImages = Math.floor(Math.random() * 3) + 2; // 2-4 images
                const selectedImages = [];
                const icons = ['👻', '🔮', '⚰️', '🏚️', '🪆', '🌲', '🎭', '🕷️'];
                
                for (let i = 0; i < numImages; i++) {
                    const randomIcon = icons[Math.floor(Math.random() * icons.length)];
                    selectedImages.push({
                        icon: randomIcon,
                        id: Date.now() + i
                    });
                }

                // Display images
                displayImages(selectedImages);
                showAlert('✅ Gambar berhasil dibuat!', 'success');

            } catch (error) {
                showAlert('❌ Gagal membuat gambar. Coba lagi.', 'error');
            } finally {
                // Reset button
                generateBtn.disabled = false;
                generateBtn.innerHTML = '🎨 Generate Gambar Horror';
            }
        }

        // Display generated images
        function displayImages(images) {
            const imagesGrid = document.getElementById('images-grid');
            
            const imagesHTML = images.map(image => `
                <div class="image-item">
                    <div class="generated-image">${image.icon}</div>
                    <div class="image-actions">
                        <button class="download-btn" onclick="downloadImage('${image.id}')">
                            📥 Download
                        </button>
                    </div>
                </div>
            `).join('');

            imagesGrid.innerHTML = imagesHTML;
        }

        // Download image (placeholder)
        function downloadImage(imageId) {
            showAlert('✅ Download berhasil! (Demo mode)', 'success');
        }

        // Show alert
        function showAlert(message, type) {
            const alertContainer = document.getElementById('alert-container');
            const alertDiv = document.createElement('div');
            alertDiv.className = `alert alert-${type}`;
            alertDiv.innerHTML = message;
            
            alertContainer.innerHTML = '';
            alertContainer.appendChild(alertDiv);
            
            setTimeout(() => {
                if (alertDiv.parentNode) {
                    alertDiv.remove();
                }
            }, 4000);
        }

        // Scroll to content
        function scrollToContent() {
            document.getElementById('content').scrollIntoView({ 
                behavior: 'smooth' 
            });
        }

        // Load sample images on page load
        function loadSampleImages() {
            setTimeout(() => {
                const sampleImages = [
                    { icon: '👻', id: 'sample-1' },
                    { icon: '🔮', id: 'sample-2' },
                    { icon: '⚰️', id: 'sample-3' }
                ];
                displayImages(sampleImages);
            }, 1000);
        }
    </script>
</body>
</html>
