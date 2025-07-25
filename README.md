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
            font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
            min-height: 100vh;
            overflow-x: hidden;
            line-height: 1.6;
        }

        /* Enhanced Navigation */
        .netflix-nav {
            position: fixed;
            top: 0;
            width: 100%;
            background: linear-gradient(180deg, rgba(0,0,0,0.95) 0%, rgba(0,0,0,0.8) 70%, transparent 100%);
            z-index: 1000;
            padding: 15px 40px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
            backdrop-filter: blur(20px);
        }

        .netflix-nav.scrolled {
            background: rgba(10, 10, 10, 0.98);
            backdrop-filter: blur(25px);
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
            padding: 12px 40px;
        }

        .logo {
            font-size: 2.2rem;
            font-weight: 800;
            background: linear-gradient(135deg, #ff0000 0%, #cc0000 50%, #990000 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            letter-spacing: -0.03em;
            text-shadow: 0 0 30px rgba(255, 0, 0, 0.3);
        }

        .nav-links {
            display: flex;
            gap: 35px;
            align-items: center;
        }

        .nav-link {
            color: #cccccc;
            text-decoration: none;
            font-weight: 500;
            font-size: 0.95rem;
            padding: 8px 16px;
            border-radius: 25px;
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
            cursor: pointer;
            position: relative;
            overflow: hidden;
        }

        .nav-link::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.1), transparent);
            transition: left 0.5s;
        }

        .nav-link:hover::before {
            left: 100%;
        }

        .nav-link:hover {
            color: #ffffff;
            background: rgba(255, 255, 255, 0.1);
            transform: translateY(-2px);
        }

        .nav-link.active {
            color: #ffffff;
            background: linear-gradient(135deg, #ff0000, #cc0000);
            box-shadow: 0 8px 25px rgba(255, 0, 0, 0.3);
        }

        .search-icon {
            width: 22px;
            height: 22px;
            cursor: pointer;
            fill: #cccccc;
            transition: all 0.3s ease;
            padding: 8px;
            border-radius: 50%;
        }

        .search-icon:hover {
            fill: #ffffff;
            background: rgba(255, 255, 255, 0.1);
            transform: scale(1.1);
        }

        /* Enhanced Hero Section */
        .hero-section {
            height: 100vh;
            background: 
                linear-gradient(135deg, rgba(0,0,0,0.7) 0%, rgba(20,0,0,0.6) 50%, rgba(0,0,0,0.8) 100%), 
                radial-gradient(circle at 30% 40%, rgba(255, 0, 0, 0.1) 0%, transparent 50%),
                url('https://images.unsplash.com/photo-1520637836862-4d197d17c87a?w=1920&h=1080&fit=crop') center/cover;
            display: flex;
            align-items: center;
            justify-content: flex-start;
            padding: 0 40px;
            position: relative;
            overflow: hidden;
        }

        .hero-section::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: linear-gradient(45deg, 
                transparent 0%, 
                rgba(255, 0, 0, 0.03) 25%, 
                transparent 50%, 
                rgba(255, 0, 0, 0.03) 75%, 
                transparent 100%);
            animation: shimmer 4s ease-in-out infinite;
        }

        @keyframes shimmer {
            0%, 100% { opacity: 0; }
            50% { opacity: 1; }
        }

        .hero-content {
            max-width: 650px;
            z-index: 2;
            animation: slideInUp 1s ease-out;
        }

        @keyframes slideInUp {
            from {
                opacity: 0;
                transform: translateY(50px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .hero-title {
            font-size: 4.5rem;
            font-weight: 800;
            line-height: 1.1;
            margin-bottom: 25px;
            background: linear-gradient(135deg, #ffffff 0%, #ff6b6b 50%, #ff0000 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            text-shadow: 0 0 50px rgba(255, 255, 255, 0.1);
            animation: glow 3s ease-in-out infinite alternate;
        }

        @keyframes glow {
            from { filter: drop-shadow(0 0 20px rgba(255, 107, 107, 0.3)); }
            to { filter: drop-shadow(0 0 40px rgba(255, 0, 0, 0.5)); }
        }

        .hero-subtitle {
            font-size: 1.4rem;
            color: #e0e0e0;
            margin-bottom: 35px;
            font-weight: 400;
            line-height: 1.5;
            opacity: 0.9;
        }

        .hero-buttons {
            display: flex;
            gap: 20px;
            align-items: center;
        }

        .btn-primary {
            background: linear-gradient(135deg, #ffffff 0%, #f0f0f0 100%);
            color: #000000;
            padding: 15px 35px;
            border: none;
            border-radius: 8px;
            font-weight: 700;
            font-size: 1.05rem;
            cursor: pointer;
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
            display: flex;
            align-items: center;
            gap: 10px;
            box-shadow: 0 8px 25px rgba(0, 0, 0, 0.3);
            position: relative;
            overflow: hidden;
        }

        .btn-primary::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.2), transparent);
            transition: left 0.5s;
        }

        .btn-primary:hover::before {
            left: 100%;
        }

        .btn-primary:hover {
            transform: translateY(-3px);
            box-shadow: 0 12px 35px rgba(0, 0, 0, 0.4);
        }

        .btn-secondary {
            background: rgba(255, 255, 255, 0.15);
            color: #ffffff;
            padding: 15px 35px;
            border: 2px solid rgba(255, 255, 255, 0.3);
            border-radius: 8px;
            font-weight: 600;
            font-size: 1.05rem;
            cursor: pointer;
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
            display: flex;
            align-items: center;
            gap: 10px;
            backdrop-filter: blur(10px);
        }

        .btn-secondary:hover {
            background: rgba(255, 255, 255, 0.25);
            border-color: rgba(255, 255, 255, 0.5);
            transform: translateY(-3px);
        }

        /* Enhanced Content Section */
        .content-section {
            padding: 80px 40px;
            background: linear-gradient(180deg, #0a0a0a 0%, #111111 100%);
            position: relative;
        }

        .content-section::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 100px;
            background: linear-gradient(180deg, rgba(0,0,0,0.8) 0%, transparent 100%);
        }

        .section-title {
            font-size: 2.2rem;
            font-weight: 700;
            margin-bottom: 40px;
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
            width: 6px;
            height: 40px;
            background: linear-gradient(135deg, #ff0000, #cc0000);
            border-radius: 3px;
            box-shadow: 0 0 15px rgba(255, 0, 0, 0.5);
        }

        .content-row {
            margin-bottom: 70px;
            opacity: 0;
            animation: fadeInUp 0.8s ease-out forwards;
        }

        .content-row:nth-child(1) { animation-delay: 0.1s; }
        .content-row:nth-child(2) { animation-delay: 0.2s; }
        .content-row:nth-child(3) { animation-delay: 0.3s; }
        .content-row:nth-child(4) { animation-delay: 0.4s; }

        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .netflix-carousel {
            display: flex;
            gap: 20px;
            overflow-x: auto;
            padding: 15px 0 25px 0;
            scroll-behavior: smooth;
            scroll-snap-type: x mandatory;
        }

        .netflix-carousel::-webkit-scrollbar {
            height: 8px;
        }

        .netflix-carousel::-webkit-scrollbar-track {
            background: rgba(255, 255, 255, 0.1);
            border-radius: 4px;
        }

        .netflix-carousel::-webkit-scrollbar-thumb {
            background: linear-gradient(90deg, #ff0000, #cc0000);
            border-radius: 4px;
        }

        .netflix-carousel::-webkit-scrollbar-thumb:hover {
            background: linear-gradient(90deg, #ff3333, #ff0000);
        }

        /* Enhanced Horror Cards */
        .horror-card {
            min-width: 320px;
            max-width: 320px;
            background: linear-gradient(145deg, #1a1a1a, #0f0f0f);
            border-radius: 12px;
            overflow: hidden;
            transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
            cursor: pointer;
            position: relative;
            flex-shrink: 0;
            scroll-snap-align: start;
            border: 1px solid rgba(255, 255, 255, 0.1);
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.3);
        }

        .horror-card:hover {
            transform: scale(1.08) translateY(-10px);
            z-index: 10;
            box-shadow: 0 20px 60px rgba(255, 0, 0, 0.2);
            border-color: rgba(255, 0, 0, 0.3);
        }

        .horror-card:hover .card-overlay {
            opacity: 1;
            backdrop-filter: blur(5px);
        }

        .horror-card:hover .card-image {
            transform: scale(1.1);
        }

        .card-image {
            width: 100%;
            height: 200px;
            object-fit: cover;
            transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
            display: block;
        }

        .card-overlay {
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: linear-gradient(180deg, 
                rgba(0,0,0,0.2) 0%, 
                rgba(0,0,0,0.5) 40%, 
                rgba(0,0,0,0.9) 100%);
            opacity: 0;
            transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
            display: flex;
            flex-direction: column;
            justify-content: flex-end;
            padding: 25px;
        }

        .card-title {
            color: #ffffff;
            font-size: 1.1rem;
            font-weight: 700;
            margin-bottom: 12px;
            line-height: 1.3;
            text-shadow: 0 2px 8px rgba(0, 0, 0, 0.5);
        }

        .card-description {
            color: #e0e0e0;
            font-size: 0.85rem;
            line-height: 1.5;
            margin-bottom: 15px;
            opacity: 0.9;
        }

        .card-meta {
            display: flex;
            justify-content: space-between;
            align-items: center;
            font-size: 0.75rem;
        }

        .platform-tag {
            background: linear-gradient(135deg, #ff0000, #cc0000);
            color: #ffffff;
            padding: 6px 12px;
            border-radius: 20px;
            font-weight: 600;
            font-size: 0.7rem;
            text-transform: uppercase;
            letter-spacing: 0.5px;
            box-shadow: 0 4px 15px rgba(255, 0, 0, 0.3);
        }

        .timestamp {
            color: #aaaaaa;
            font-weight: 500;
        }

        /* Enhanced Search */
        .floating-search {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: rgba(15, 15, 15, 0.98);
            backdrop-filter: blur(30px);
            padding: 50px;
            border-radius: 20px;
            border: 1px solid rgba(255, 255, 255, 0.15);
            z-index: 2000;
            width: 90%;
            max-width: 650px;
            display: none;
            box-shadow: 0 25px 80px rgba(0, 0, 0, 0.6);
        }

        .floating-search.active {
            display: block;
            animation: popIn 0.3s cubic-bezier(0.4, 0, 0.2, 1);
        }

        @keyframes popIn {
            from {
                opacity: 0;
                transform: translate(-50%, -50%) scale(0.8);
            }
            to {
                opacity: 1;
                transform: translate(-50%, -50%) scale(1);
            }
        }

        .search-input {
            width: 100%;
            padding: 20px 25px;
            background: rgba(30, 30, 30, 0.8);
            border: 2px solid rgba(255, 255, 255, 0.2);
            border-radius: 12px;
            color: #ffffff;
            font-size: 1.2rem;
            font-family: inherit;
            outline: none;
            margin-bottom: 25px;
            transition: all 0.3s ease;
        }

        .search-input:focus {
            border-color: rgba(255, 0, 0, 0.5);
            box-shadow: 0 0 25px rgba(255, 0, 0, 0.2);
        }

        .search-input::placeholder {
            color: #888888;
        }

        .search-results {
            max-height: 450px;
            overflow-y: auto;
        }

        .search-result {
            padding: 20px;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
            cursor: pointer;
            transition: all 0.3s ease;
            border-radius: 8px;
            margin-bottom: 5px;
        }

        .search-result:hover {
            background: rgba(255, 255, 255, 0.08);
            transform: translateX(5px);
        }

        .search-result:last-child {
            border-bottom: none;
        }

        .overlay {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0, 0, 0, 0.85);
            z-index: 1500;
            display: none;
            backdrop-filter: blur(5px);
        }

        .overlay.active {
            display: block;
            animation: fadeIn 0.3s ease;
        }

        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }

        /* Loading and Error States */
        .loading {
            text-align: center;
            color: #666666;
            padding: 60px 20px;
            font-size: 1.1rem;
        }

        .loading::after {
            content: '';
            display: inline-block;
            width: 20px;
            height: 20px;
            border: 2px solid #666666;
            border-radius: 50%;
            border-top-color: #ff0000;
            animation: spin 1s ease-in-out infinite;
            margin-left: 10px;
        }

        @keyframes spin {
            to { transform: rotate(360deg); }
        }

        .error-message {
            color: #ff6b6b;
            background: rgba(255, 107, 107, 0.1);
            padding: 20px;
            border-radius: 12px;
            margin: 25px 0;
            border: 1px solid rgba(255, 107, 107, 0.3);
            text-align: center;
            font-weight: 500;
        }

        /* Responsive Design */
        @media (max-width: 768px) {
            .netflix-nav {
                padding: 15px 20px;
            }

            .nav-links {
                gap: 25px;
            }

            .nav-link {
                font-size: 0.85rem;
                padding: 6px 12px;
            }

            .hero-section {
                padding: 0 20px;
                text-align: center;
                justify-content: center;
            }

            .hero-title {
                font-size: 3rem;
            }

            .hero-subtitle {
                font-size: 1.2rem;
            }

            .content-section {
                padding: 60px 20px;
            }

            .section-title {
                font-size: 1.8rem;
            }

            .horror-card {
                min-width: 280px;
                max-width: 280px;
            }

            .floating-search {
                padding: 30px;
                width: 95%;
            }
        }

        @media (max-width: 480px) {
            .logo {
                font-size: 1.8rem;
            }

            .nav-links {
                gap: 15px;
            }

            .nav-link {
                font-size: 0.8rem;
                padding: 5px 10px;
            }

            .hero-title {
                font-size: 2.2rem;
            }

            .hero-buttons {
                flex-direction: column;
                width: 100%;
                gap: 15px;
            }

            .btn-primary, .btn-secondary {
                width: 100%;
                justify-content: center;
            }

            .horror-card {
                min-width: 250px;
                max-width: 250px;
            }

            .section-title {
                font-size: 1.6rem;
            }
        }
    </style>
</head>
<body>
    <!-- Enhanced Navigation -->
    <nav class="netflix-nav" id="navbar">
        <div class="logo">HORROR FEED</div>
        <div class="nav-links">
            <a href="#" class="nav-link active" data-filter="all">Beranda</a>
            <a href="#" class="nav-link" data-filter="tiktok">TikTok</a>
            <a href="#" class="nav-link" data-filter="youtube">YouTube</a>
            <a href="#" class="nav-link" data-filter="instagram">Instagram</a>
            <a href="#" class="nav-link" data-filter="twitter">Twitter</a>
            <svg class="search-icon" id="search-toggle" viewBox="0 0 24 24">
                <path d="M15.5 14h-.79l-.28-.27A6.471 6.471 0 0 0 16 9.5 6.5 6.5 0 1 0 9.5 16c1.61 0 3.09-.59 4.23-1.57l.27.28v.79l5 4.99L20.49 19l-4.99-5zm-6 0C7.01 14 5 11.99 5 9.5S7.01 5 9.5 5 14 7.01 14 9.5 11.99 14 9.5 14z"/>
            </svg>
        </div>
    </nav>

    <!-- Enhanced Hero Section -->
    <section class="hero-section">
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

    <!-- Enhanced Content Sections -->
    <section class="content-section" id="content">
        <div class="content-row">
            <h2 class="section-title">🔥 Trending Hari Ini</h2>
            <div class="netflix-carousel" id="trending-carousel">
                <div class="loading">Memuat konten trending...</div>
            </div>
        </div>

        <div class="content-row">
            <h2 class="section-title">📱 Cerita TikTok Viral</h2>
            <div class="netflix-carousel" id="tiktok-carousel">
                <div class="loading">Memuat video TikTok...</div>
            </div>
        </div>

        <div class="content-row">
            <h2 class="section-title">🎬 Dokumenter YouTube</h2>
            <div class="netflix-carousel" id="youtube-carousel">
                <div class="loading">Memuat dokumenter...</div>
            </div>
        </div>

        <div class="content-row">
            <h2 class="section-title">📸 Instagram Stories</h2>
            <div class="netflix-carousel" id="instagram-carousel">
                <div class="loading">Memuat stories Instagram...</div>
            </div>
        </div>

        <div class="content-row">
            <h2 class="section-title">🐦 Thread Twitter</h2>
            <div class="netflix-carousel" id="twitter-carousel">
                <div class="loading">Memuat thread Twitter...</div>
            </div>
        </div>
    </section>

    <!-- Enhanced Search Modal -->
    <div class="overlay" id="search-overlay"></div>
    <div class="floating-search" id="floating-search">
        <input type="text" class="search-input" id="search-input" placeholder="Cari cerita horor yang mengerikan..." autocomplete="off">
        <div class="search-results" id="search-results"></div>
    </div>

    <script>
        // Enhanced horror content data
        const horrorContent = [
            {
                platform: 'tiktok',
                title: 'Penampakan Misterius di Kos Mahasiswa Jakarta',
                description: 'Kejadian aneh yang dialami mahasiswa di kos dekat kampus. Suara langkah kaki di malam hari padahal tidak ada yang lewat. Pintu kamar yang tiba-tiba terbuka sendiri...',
                url: 'https://www.tiktok.com/search?q=%23ceritahoror',
                thumbnail: 'https://images.unsplash.com/photo-1520637836862-4d197d17c87a?w=300&h=180&fit=crop',
                timestamp: '5 menit lalu'
            },
            {
                platform: 'youtube',
                title: 'Ritual Santet di Desa Terpencil - Kisah Nyata',
                description: 'Dokumenter mendalam tentang praktik santet yang masih berlangsung di desa terpencil Jawa Tengah. Kesaksian langsung dari korban dan dukun setempat...',
                url: 'https://www.youtube.com/results?search_query=cerita+horor+indonesia+santet',
                thumbnail: 'https://images.unsplash.com/photo-1518709268805-4e9042af2176?w=300&h=180&fit=crop',
                timestamp: '12 menit lalu'
            },
            {
                platform: 'instagram',
                title: 'Foto Pocong Tertangkap Kamera di Kuburan Tua',
                description: 'Foto yang diambil saat ziarah kubur menunjukkan sosok putih mencurigakan di belakang makam. Photographer mengaku tidak melihat apapun saat pengambilan gambar...',
                url: 'https://www.instagram.com/explore/tags/ceritahoror/',
                thumbnail: 'https://images.unsplash.com/photo-1509909756405-be0199881695?w=300&h=180&fit=crop',
                timestamp: '18 menit lalu'
            },
            {
                platform: 'twitter',
                title: 'Thread: Pengalaman Kesurupan Massal di Sekolah',
                description: 'Thread viral tentang kejadian kesurupan massal di SMA Bekasi. 15 siswa kesurupan bersamaan saat upacara bendera. Saksi mata berbagi pengalaman mengerikan...',
                url: 'https://twitter.com/search?q=%23ceritahoror%20lang%3Aid',
                thumbnail: 'https://images.unsplash.com/photo-1551803091-e20673f15770?w=300&h=180&fit=crop',
                timestamp: '25 menit lalu'
            },
            {
                platform: 'tiktok',
                title: 'Suara Tangisan Anak Kecil dari Rumah Kosong',
                description: 'Video viral TikTok yang merekam suara tangisan misterius dari rumah yang sudah 10 tahun ditinggalkan. Warga sekitar mengaku sering mendengar suara serupa...',
                url: 'https://www.tiktok.com/search?q=%23rumahberhantu',
                thumbnail: 'https://images.unsplash.com/photo-1520637736862-4d197d17c87a?w=300&h=180&fit=crop',
                timestamp: '32 menit lalu'
            },
            {
                platform: 'youtube',
                title: 'Eksplorasi Rumah Berhantu Lawang Sewu',
                description: 'Tim explorer Indonesia berani masuk ke Lawang Sewu tengah malam. Berbagai fenomena paranormal tertangkap kamera. Video ini viral dengan 2M views...',
                url: 'https://www.youtube.com/results?search_query=eksplorasi+rumah+berhantu+indonesia',
                thumbnail: 'https://images.unsplash.com/photo-1544207240-66d3e1c39d68?w=300&h=180&fit=crop',
                timestamp: '45 menit lalu'
            },
            {
                platform: 'instagram',
                title: 'Ritual Pelet Jawa yang Salah - Story Viral
