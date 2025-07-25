<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>🔥 Horror Feed Indonesia - Live Cerita Horor</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=Creepster&display=swap" rel="stylesheet">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background: linear-gradient(135deg, #000000 0%, #0d0d0d 50%, #1a0000 100%);
            color: #ffffff;
            font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
            min-height: 100vh;
            overflow-x: hidden;
        }

        .header {
            background: rgba(0, 0, 0, 0.95);
            backdrop-filter: blur(20px) saturate(180%);
            -webkit-backdrop-filter: blur(20px) saturate(180%);
            padding: 24px 20px;
            text-align: center;
            border-bottom: 1px solid rgba(255, 0, 0, 0.1);
            position: sticky;
            top: 0;
            z-index: 100;
        }

        .logo {
            font-family: 'Creepster', cursive;
            font-size: 2.2em;
            color: #ff3b30;
            text-shadow: 0 0 30px rgba(255, 59, 48, 0.3);
            animation: subtleFlicker 4s infinite ease-in-out;
            margin-bottom: 8px;
            font-weight: 400;
        }

        .subtitle {
            font-size: 0.85em;
            color: #8e8e93;
            letter-spacing: 1px;
            opacity: 0.9;
            font-weight: 400;
        }

        .status {
            margin: 16px 0 0 0;
            padding: 6px 16px;
            background: rgba(48, 209, 88, 0.1);
            border: 1px solid rgba(48, 209, 88, 0.2);
            border-radius: 20px;
            display: inline-flex;
            align-items: center;
            font-size: 0.75em;
            font-weight: 500;
        }

        .status::before {
            content: "●";
            color: #30d158;
            margin-right: 6px;
            animation: gentlePulse 2s infinite ease-in-out;
        }

        @keyframes subtleFlicker {
            0%, 100% { opacity: 1; text-shadow: 0 0 30px rgba(255, 59, 48, 0.3); }
            50% { opacity: 0.95; text-shadow: 0 0 25px rgba(255, 59, 48, 0.2); }
        }

        @keyframes gentlePulse {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.6; }
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 32px 20px;
        }

        .stats {
            background: rgba(28, 28, 30, 0.8);
            backdrop-filter: blur(20px);
            -webkit-backdrop-filter: blur(20px);
            padding: 20px 24px;
            border-radius: 16px;
            margin-bottom: 32px;
            text-align: center;
            border: 1px solid rgba(255, 255, 255, 0.05);
            display: block !important;
            visibility: visible !important;
        }

        .stats span {
            margin: 0 20px;
            font-size: 0.85em;
            font-weight: 500;
            color: #f2f2f7;
        }

        .last-update {
            color: #30d158;
            font-weight: 600;
        }

        .search-container {
            margin-bottom: 24px;
            text-align: center;
        }

        .search-input {
            padding: 14px 20px;
            width: 320px;
            max-width: 100%;
            background: rgba(28, 28, 30, 0.8);
            backdrop-filter: blur(20px);
            -webkit-backdrop-filter: blur(20px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            border-radius: 25px;
            color: #ffffff;
            font-family: inherit;
            font-size: 0.9em;
            font-weight: 400;
            outline: none;
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
        }

        .search-input::placeholder {
            color: #8e8e93;
        }

        .search-input:focus {
            border-color: rgba(255, 59, 48, 0.6);
            box-shadow: 0 0 0 4px rgba(255, 59, 48, 0.1);
            background: rgba(28, 28, 30, 0.95);
        }

        .filters {
            display: flex;
            justify-content: center;
            gap: 12px;
            margin-bottom: 40px;
            flex-wrap: wrap;
        }

        .filter-btn {
            padding: 10px 20px;
            background: rgba(28, 28, 30, 0.6);
            backdrop-filter: blur(20px);
            -webkit-backdrop-filter: blur(20px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            color: #f2f2f7;
            border-radius: 22px;
            cursor: pointer;
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
            font-family: inherit;
            font-size: 0.85em;
            font-weight: 500;
        }

        .filter-btn:hover {
            background: rgba(255, 59, 48, 0.1);
            border-color: rgba(255, 59, 48, 0.3);
            transform: translateY(-1px);
        }

        .filter-btn.active {
            background: rgba(255, 59, 48, 0.15);
            border-color: rgba(255, 59, 48, 0.4);
            color: #ff453a;
            box-shadow: 0 4px 12px rgba(255, 59, 48, 0.15);
        }

        .feed {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(360px, 1fr));
            gap: 24px;
            margin-bottom: 40px;
        }

        .horror-post {
            background: rgba(28, 28, 30, 0.8);
            backdrop-filter: blur(20px) saturate(180%);
            -webkit-backdrop-filter: blur(20px) saturate(180%);
            border: 1px solid rgba(255, 255, 255, 0.08);
            border-radius: 20px;
            overflow: hidden;
            transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
            position: relative;
        }

        .horror-post:hover {
            transform: translateY(-8px) scale(1.02);
            box-shadow: 0 20px 40px rgba(255, 59, 48, 0.15);
            border-color: rgba(255, 59, 48, 0.2);
        }

        .platform-badge {
            position: absolute;
            top: 16px;
            right: 16px;
            padding: 6px 12px;
            border-radius: 14px;
            font-size: 0.7em;
            font-weight: 600;
            z-index: 2;
            backdrop-filter: blur(10px);
            -webkit-backdrop-filter: blur(10px);
        }

        .platform-badge.tiktok { background: rgba(255, 0, 80, 0.9); color: white; }
        .platform-badge.youtube { background: rgba(255, 0, 0, 0.9); color: white; }
        .platform-badge.instagram { background: rgba(228, 64, 95, 0.9); color: white; }
        .platform-badge.twitter { background: rgba(29, 161, 242, 0.9); color: white; }

        .thumbnail {
            width: 100%;
            height: 220px;
            object-fit: cover;
            cursor: pointer;
            transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
        }

        .thumbnail:hover {
            transform: scale(1.05);
        }

        .post-content {
            padding: 24px;
        }

        .post-title {
            color: #f2f2f7;
            font-size: 1.1em;
            font-weight: 600;
            margin-bottom: 12px;
            line-height: 1.4;
            letter-spacing: -0.02em;
        }

        .post-description {
            font-size: 0.85em;
            line-height: 1.5;
            margin-bottom: 16px;
            color: #8e8e93;
            font-weight: 400;
        }

        .post-meta {
            display: flex;
            justify-content: space-between;
            align-items: center;
            font-size: 0.75em;
            color: #636366;
            margin-bottom: 20px;
            font-weight: 500;
        }

        .hashtags {
            color: #30d158;
            font-weight: 500;
        }

        .watch-btn {
            width: 100%;
            padding: 14px;
            background: linear-gradient(135deg, #ff453a 0%, #ff3b30 100%);
            color: white;
            text-decoration: none;
            border-radius: 12px;
            text-align: center;
            font-weight: 600;
            font-size: 0.9em;
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
            display: block;
            letter-spacing: -0.01em;
        }

        .watch-btn:hover {
            background: linear-gradient(135deg, #ff3b30 0%, #d70015 100%);
            box-shadow: 0 8px 25px rgba(255, 59, 48, 0.3);
            transform: translateY(-2px);
        }

        .watch-btn:active {
            transform: translateY(0);
        }

        .loading {
            text-align: center;
            padding: 60px 20px;
            font-size: 1.1em;
            color: #8e8e93;
            font-weight: 500;
        }

        .loading::after {
            content: "...";
            animation: loadingDots 1.5s infinite;
        }

        @keyframes loadingDots {
            0%, 20% { content: "..."; }
            40% { content: ".."; }
            60% { content: "."; }
            80%, 100% { content: ""; }
        }

        /* Dark mode glass effect */
        .glass-effect {
            background: rgba(28, 28, 30, 0.7);
            backdrop-filter: blur(20px) saturate(180%);
            -webkit-backdrop-filter: blur(20px) saturate(180%);
            border: 1px solid rgba(255, 255, 255, 0.1);
        }

        /* Smooth scrolling */
        html {
            scroll-behavior: smooth;
        }

        @media (max-width: 768px) {
            .feed {
                grid-template-columns: 1fr;
                gap: 20px;
            }
            
            .logo {
                font-size: 1.8em;
            }
            
            .container {
                padding: 24px 16px;
            }
            
            .search-input {
                width: 100%;
                max-width: 300px;
            }
            
            .filters {
                gap: 8px;
            }
            
            .filter-btn {
                font-size: 0.8em;
                padding: 8px 16px;
            }

            .stats {
                padding: 16px 20px;
            }

            .stats span {
                margin: 0 12px;
                font-size: 0.8em;
            }
        }

        @media (max-width: 480px) {
            .stats {
                font-size: 0.85em;
            }
            
            .stats span {
                display: block;
                margin: 4px 0;
            }
        }
    </style>
</head>
<body>
    <div class="header">
        <h1 class="logo">🔥 HORROR FEED INDONESIA</h1>
        <p class="subtitle">LIVE CERITA HOROR & MISTERI</p>
        <div class="status">SEDANG MENGUMPULKAN KONTEN</div>
    </div>

    <div class="container">
        <div class="stats glass-effect">
            <span>📊 Total Posts: <strong id="total-posts">6</strong></span>
            <span>⏰ Update Terakhir: <span class="last-update" id="last-update">Memuat...</span></span>
            <span>🔄 Next Update: <strong id="next-update">2:00</strong></span>
        </div>

        <div class="search-container">
            <input type="text" id="search-input" class="search-input" placeholder="🔍 Cari cerita horor...">
        </div>

        <div class="filters">
            <button class="filter-btn active" data-filter="all">Semua</button>
            <button class="filter-btn" data-filter="tiktok">TikTok</button>
            <button class="filter-btn" data-filter="youtube">YouTube</button>
            <button class="filter-btn" data-filter="instagram">Instagram</button>
            <button class="filter-btn" data-filter="twitter">Twitter</button>
        </div>

        <div class="feed" id="horror-feed">
            <div class="loading">Memuat konten horor terbaru</div>
        </div>
    </div>

    <script>
        // Sample horror content data with working links
        const sampleHorrorPosts = [
            {
                platform: 'tiktok',
                title: 'Penampakan Misterius di Kos Mahasiswa',
                description: 'Kejadian aneh yang dialami mahasiswa di kos dekat kampus. Suara langkah kaki di malam hari padahal tidak ada yang lewat...',
                url: 'https://www.tiktok.com/search?q=%23ceritahoror',
                thumbnail: 'https://images.unsplash.com/photo-1520637836862-4d197d17c87a?w=400&h=220&fit=crop',
                hashtags: '#ceritahoror #penampakan #kos',
                timestamp: '5 menit lalu'
            },
            {
                platform: 'youtube',
                title: 'Ritual Santet di Desa Terpencil - Kisah Nyata',
                description: 'Dokumenter tentang praktik santet yang masih berlangsung di desa terpencil di Jawa Tengah. Video ini berisi rekaman asli...',
                url: 'https://www.youtube.com/results?search_query=cerita+horor+indonesia+santet',
                thumbnail: 'https://images.unsplash.com/photo-1518709268805-4e9042af2176?w=400&h=220&fit=crop',
                hashtags: '#santet #ritual #kisahnyata',
                timestamp: '12 menit lalu'
            },
            {
                platform: 'instagram',
                title: 'Foto Pocong di Kuburan Tua',
                description: 'Foto yang diambil saat ziarah kubur menunjukkan sosok putih yang mencurigakan di belakang makam...',
                url: 'https://www.instagram.com/explore/tags/ceritahoror/',
                thumbnail: 'https://images.unsplash.com/photo-1509909756405-be0199881695?w=400&h=220&fit=crop',
                hashtags: '#pocong #kuburan #foto',
                timestamp: '18 menit lalu'
            },
            {
                platform: 'twitter',
                title: 'Thread: Pengalaman Kesurupan Massal',
                description: 'Thread panjang tentang kejadian kesurupan massal di sebuah sekolah di Bekasi. Saksi mata menceritakan kronologi...',
                url: 'https://twitter.com/search?q=%23ceritahoror%20lang%3Aid',
                thumbnail: 'https://images.unsplash.com/photo-1551803091-e20673f15770?w=400&h=220&fit=crop',
                hashtags: '#kesurupan #thread #bekasi',
                timestamp: '25 menit lalu'
            },
            {
                platform: 'tiktok',
                title: 'Suara Tangisan dari Rumah Kosong',
                description: 'Video TikTok yang merekam suara tangisan misterius dari rumah yang sudah lama ditinggalkan...',
                url: 'https://www.tiktok.com/search?q=%23rumahberhantu',
                thumbnail: 'https://images.unsplash.com/photo-1520637736862-4d197d17c87a?w=400&h=220&fit=crop',
                hashtags: '#rumahkosong #suaratangisan #horor',
                timestamp: '32 menit lalu'
            },
            {
                platform: 'youtube',
                title: 'Eksplorasi Rumah Berhantu di Bandung',
                description: 'Tim explorer Indonesia menjelajahi rumah berhantu terkenal di Bandung. Berbagai fenomena paranormal tertangkap kamera...',
                url: 'https://www.youtube.com/results?search_query=eksplorasi+rumah+berhantu+indonesia',
                thumbnail: 'https://images.unsplash.com/photo-1520637736862-4d197d17c87a?w=400&h=220&fit=crop',
                hashtags: '#eksplorasi #rumahberhantu #bandung',
                timestamp: '45 menit lalu'
            }
        ];

        let currentPosts = [...sampleHorrorPosts];
        let currentFilter = 'all';
        let searchQuery = '';

        function renderPosts(posts) {
            const feed = document.getElementById('horror-feed');
            
            if (posts.length === 0) {
                feed.innerHTML = '<div class="loading">Tidak ada konten untuk filter ini</div>';
                return;
            }

            feed.innerHTML = posts.map(post => `
                <div class="horror-post">
                    <div class="platform-badge ${post.platform}">${post.platform.toUpperCase()}</div>
                    <img src="${post.thumbnail}" alt="${post.title}" class="thumbnail" onclick="highlightThumbnail(this)">
                    <div class="post-content">
                        <h3 class="post-title">${post.title}</h3>
                        <p class="post-description">${post.description}</p>
                        <div class="post-meta">
                            <span class="timestamp">${post.timestamp}</span>
                            <span class="hashtags">${post.hashtags}</span>
                        </div>
                        <a href="${post.url}" class="watch-btn" target="_blank" onclick="trackClick('${post.platform}', '${post.title}', this)">👁️ Lihat Sekarang</a>
                    </div>
                </div>
            `).join('');

            document.getElementById('total-posts').textContent = posts.length;
        }

        function trackClick(platform, title, button) {
            console.log(`Clicked: ${platform} - ${title}`);
            
            // Show loading state
            const originalText = button.textContent;
            button.textContent = '🔄 Memuat...';
            
            setTimeout(() => {
                button.textContent = originalText;
            }, 1000);
        }

        function highlightThumbnail(img) {
            img.style.filter = 'brightness(1.2) contrast(1.1)';
            setTimeout(() => {
                img.style.filter = 'brightness(1) contrast(1)';
            }, 300);
        }

        function filterPosts(platform) {
            currentFilter = platform;
            const filtered = platform === 'all' 
                ? currentPosts 
                : currentPosts.filter(post => post.platform === platform);
            
            // Apply search if there's a query
            const finalPosts = searchQuery 
                ? filtered.filter(post => 
                    post.title.toLowerCase().includes(searchQuery.toLowerCase()) ||
                    post.description.toLowerCase().includes(searchQuery.toLowerCase()) ||
                    post.hashtags.toLowerCase().includes(searchQuery.toLowerCase())
                  )
                : filtered;
            
            renderPosts(finalPosts);

            // Update filter buttons
            document.querySelectorAll('.filter-btn').forEach(btn => {
                btn.classList.toggle('active', btn.dataset.filter === platform);
            });
        }

        function searchPosts(query) {
            searchQuery = query;
            const filtered = currentFilter === 'all' 
                ? currentPosts 
                : currentPosts.filter(post => post.platform === currentFilter);
            
            const searchResults = query 
                ? filtered.filter(post => 
                    post.title.toLowerCase().includes(query.toLowerCase()) ||
                    post.description.toLowerCase().includes(query.toLowerCase()) ||
                    post.hashtags.toLowerCase().includes(query.toLowerCase())
                  )
                : filtered;
            
            renderPosts(searchResults);
        }

        function updateLastUpdateTime() {
            const now = new Date();
            document.getElementById('last-update').textContent = now.toLocaleTimeString('id-ID');
        }

        function startUpdateTimer() {
            let seconds = 120; // 2 minutes
            
            function updateTimer() {
                const minutes = Math.floor(seconds / 60);
                const secs = seconds % 60;
                document.getElementById('next-update').textContent = 
                    `${minutes}:${secs.toString().padStart(2, '0')}`;
                
                if (seconds <= 0) {
                    seconds = 120;
                    updateLastUpdateTime();
                    // Simulate adding new content
                    addNewPost();
                }
                
                seconds--;
            }
            
            updateTimer();
            setInterval(updateTimer, 1000);
        }

        function addNewPost() {
            const platforms = ['tiktok', 'youtube', 'instagram', 'twitter'];
            const horrorTitles = [
                'Penampakan Aneh di Rumah Tua',
                'Suara Misterius di Tengah Malam',
                'Foto Hantu yang Tertangkap Kamera',
                'Kejadian Supernatural di Kampus',
                'Ritual Mistis di Hutan Angker'
            ];
            
            const randomPlatform = platforms[Math.floor(Math.random() * platforms.length)];
            const randomTitle = horrorTitles[Math.floor(Math.random() * horrorTitles.length)];
            
            const newPost = {
                platform: randomPlatform,
                title: randomTitle + ' - ' + new Date().toLocaleTimeString(),
                description: 'Konten horor baru yang baru saja ditemukan oleh sistem otomatis...',
                url: getURLForPlatform(randomPlatform),
                thumbnail: 'https://images.unsplash.com/photo-1520637736862-4d197d17c87a?w=400&h=220&fit=crop',
                hashtags: '#horor #baru #otomatis',
                timestamp: 'Baru saja'
            };
            
            currentPosts.unshift(newPost);
            
            // Re-render with current filter and search
            if (currentFilter === 'all' || currentFilter === newPost.platform) {
                filterPosts(currentFilter);
            }
            
            console.log('New horror content added!');
        }

        function getURLForPlatform(platform) {
            const urls = {
                'tiktok': 'https://www.tiktok.com/search?q=%23ceritahoror',
                'youtube': 'https://www.youtube.com/results?search_query=cerita+horor+indonesia',
                'instagram': 'https://www.instagram.com/explore/tags/ceritahoror/',
                'twitter': 'https://twitter.com/search?q=%23ceritahoror%20lang%3Aid'
            };
            return urls[platform] || '#';
        }

        // Initialize everything when page loads
        document.addEventListener('DOMContentLoaded', function() {
            // Make sure stats are visible first
            const statsElement = document.querySelector('.stats');
            if (statsElement) {
                statsElement.style.display = 'block';
                statsElement.style.visibility = 'visible';
            }
            
            renderPosts(currentPosts);
            updateLastUpdateTime();
            startUpdateTimer();

            // Add search functionality
            const searchInput = document.getElementById('search-input');
            searchInput.addEventListener('input', function(e) {
                searchPosts(e.target.value);
            });

            // Add filter event listeners
            document.querySelectorAll('.filter-btn').forEach(btn => {
                btn.addEventListener('click', () => {
                    filterPosts(btn.dataset.filter);
                });
            });
        });
    </script>
</body>
</html>
