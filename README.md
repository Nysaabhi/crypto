# crypto
<head>
    <title>Exclusive NFT Gallery</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css" rel="stylesheet">
    <style>
        :root {
            --primary-color: #A67C00;
            --primary-hover: #8B6914;
            --accent-gold: #FFD700;
            --background-dark: #0A0B0E;
            --card-bg: #141519;
            --text-light: #FFFFFF;
            --text-gold: #D4AF37;
            --premium-gradient: linear-gradient(135deg, #B8860B, #FFD700);
            --card-shadow: 0 8px 32px rgba(0, 0, 0, 0.4);
            --glass-effect: rgba(255, 255, 255, 0.05);
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            min-height: 100vh;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: var(--background-dark);
            color: var(--text-light);
            background-image: 
                radial-gradient(circle at 20% 20%, rgba(255, 215, 0, 0.05) 0%, transparent 40%),
                radial-gradient(circle at 80% 80%, rgba(255, 215, 0, 0.05) 0%, transparent 40%);
        }

        .header {
            padding: 20px;
            background: rgba(0, 0, 0, 0.8);
            backdrop-filter: blur(20px);
            position: fixed;
            width: 100%;
            top: 0;
            z-index: 1000;
            border-bottom: 1px solid rgba(255, 215, 0, 0.1);
        }

        .header-content {
            max-width: 1400px;
            margin: 0 auto;
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 0 20px;
        }

        .logo {
            font-size: 1.8em;
            font-weight: 800;
            background: var(--premium-gradient);
            -webkit-background-clip: text;
            color: transparent;
            letter-spacing: 1px;
        }

        .connect-wallet {
            padding: 10px 20px;
            background: var(--premium-gradient);
            border: none;
            border-radius: 25px;
            color: var(--background-dark);
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .main-container {
            max-width: 1400px;
            margin: 100px auto 40px;
            padding: 20px;
            position: relative;
        }

        .carousel-container {
            position: relative;
            padding: 40px 60px;
            background: var(--card-bg);
            border-radius: 30px;
            box-shadow: var(--card-shadow);
            border: 1px solid rgba(255, 215, 0, 0.1);
            overflow: hidden;
        }

        .carousel {
            display: flex;
            transition: transform 0.5s ease;
            gap: 20px;
            padding: 20px 0;
        }

        .artwork-card {
            flex: 0 0 300px;
            background: rgba(20, 21, 25, 0.8);
            border-radius: 20px;
            overflow: hidden;
            box-shadow: var(--card-shadow);
            transition: all 0.4s ease;
            border: 1px solid rgba(255, 215, 0, 0.1);
            cursor: pointer;
            transform: scale(0.98);
            opacity: 0.8;
        }

        .artwork-card.active {
            transform: scale(1);
            opacity: 1;
        }

        .artwork-card:hover {
            transform: translateY(-5px) scale(1.02);
            box-shadow: 0 15px 40px rgba(255, 215, 0, 0.1);
        }

        .artwork-image {
            position: relative;
            width: 100%;
            height: 300px;
            overflow: hidden;
        }

        .artwork-image img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            transition: transform 0.5s ease;
        }

        .artwork-info {
            padding: 20px;
            background: linear-gradient(to top, rgba(0,0,0,0.8), transparent);
        }

        .artwork-title {
            font-size: 1.2em;
            color: var(--text-gold);
            margin-bottom: 8px;
            font-weight: bold;
        }

        .artwork-collection {
            color: rgba(255, 255, 255, 0.7);
            font-size: 0.9em;
            margin-bottom: 12px;
        }

        .artwork-price {
            font-size: 1.1em;
            color: var(--text-gold);
            font-weight: bold;
        }

        .carousel-button {
            position: absolute;
            top: 50%;
            transform: translateY(-50%);
            background: var(--premium-gradient);
            border: none;
            width: 40px;
            height: 40px;
            border-radius: 50%;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            color: var(--background-dark);
            font-size: 1.2em;
            z-index: 10;
            transition: all 0.3s ease;
        }

        .carousel-button:hover {
            transform: translateY(-50%) scale(1.1);
        }

        .carousel-button.prev {
            left: 20px;
        }

        .carousel-button.next {
            right: 20px;
        }

        .carousel-dots {
            display: flex;
            justify-content: center;
            gap: 10px;
            margin-top: 20px;
        }

        .dot {
            width: 8px;
            height: 8px;
            border-radius: 50%;
            background: rgba(255, 215, 0, 0.3);
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .dot.active {
            background: var(--text-gold);
            transform: scale(1.2);
        }

        @media (max-width: 768px) {
            .carousel-container {
                padding: 20px;
            }

            .artwork-card {
                flex: 0 0 280px;
            }

            .artwork-image {
                height: 250px;
            }

            .carousel-button {
                width: 35px;
                height: 35px;
                font-size: 1em;
            }
        }

        @media (max-width: 480px) {
            .artwork-card {
                flex: 0 0 260px;
            }

            .artwork-image {
                height: 220px;
            }
        }

        .modal-content {
            background: var(--card-bg);
            border-radius: 30px;
            padding: 40px;
            max-width: 1000px;
            margin: 40px auto;
            position: relative;
        }

        .nft-details {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
        }

        @media (max-width: 768px) {
            .nft-details {
                grid-template-columns: 1fr;
            }

            .modal-content {
                margin: 20px;
                padding: 20px;
            }
        }
    </style>
</head>
<body>
    <header class="header">
        <div class="header-content">
            <div class="logo">GENESIS NFT</div>
            <button class="connect-wallet">
                <i class="fas fa-wallet"></i>
                Connect
            </button>
        </div>
    </header>

    <div class="main-container">
        <div class="carousel-container">
            <button class="carousel-button prev">
                <i class="fas fa-chevron-left"></i>
            </button>
            <button class="carousel-button next">
                <i class="fas fa-chevron-right"></i>
            </button>
            <div class="carousel"></div>
            <div class="carousel-dots"></div>
        </div>
    </div>

    <div class="modal" id="nftModal">
        <div class="modal-content">
            <div class="modal-close">&times;</div>
            <div class="nft-details">
                <!-- NFT details will be dynamically inserted here -->
            </div>
        </div>
    </div>

    <script>
        const nftData = [
            {
                id: 1,
                title: "Divine Harmony #001",
                collection: "Genesis Collection",
                price: "12.5 ETH",
                image: "https://i.ibb.co/yFNbRqF/Whats-App-Image-2024-10-20-at-09-16-07-510389dd.jpg",
                badge: "Genesis Edition",
                artist: "CryptoMaster",
                description: "A masterpiece that blends digital art with traditional aesthetics, representing the harmony between past and future.",
                attributes: [
                    { trait: "Rarity", value: "Legendary" },
                    { trait: "Edition", value: "1 of 1" },
                    { trait: "Blockchain", value: "Ethereum" }
                ]
            },
            {
                id: 2,
                title: "Ethereal Dreams #002",
                collection: "Platinum Series",
                price: "8.8 ETH",
                image: "https://i.ibb.co/7vkRDZv/Whats-App-Image-2024-10-20-at-09-16-08-0798f91f.jpg",
                badge: "Platinum",
                artist: "DigitalDreamer",
                description: "An ethereal masterpiece capturing the essence of dreams in the digital age.",
                attributes: [
                    { trait: "Rarity", value: "Ultra Rare" },
                    { trait: "Edition", value: "2 of 5" },
                    { trait: "Blockchain", value: "Ethereum" }
                ]
            },
            {
                id: 3,
                title: "Quantum Legacy #003",
                collection: "Elite Collection",
                price: "15.2 ETH",
                image: "https://i.ibb.co/k8zNj9j/a-captivating-and-dreamlike-scene-of-a-dali-esque-swof-qz-GQu-Ks-Sj-h-EVGflw-q-Em-M-hmr-Rcm-FUZb-GUc.jpg",
                badge: "Ultra Rare",
                artist: "QuantumArtist",
                description: "A visionary piece that explores the intersection of quantum mechanics and digital art.",
                attributes: [
                    { trait: "Rarity", value: "Mythical" },
                    { trait: "Edition", value: "3 of 3" },
                    { trait: "Blockchain", value: "Ethereum" }
                ]
            },
            {
                id: 4,
                title: "Celestial Vision #004",
                collection: "Masterpiece Series",
                price: "18.5 ETH",
                image: "https://i.ibb.co/k51wwwg/an-awe-inspiring-scene-of-mythical-beasts-roaming-E6-Ugt4-g-TAO4r-Pl-Gpra-e-Q-t0tr-Egk6-Sf2r8k-Tr2-I.jpg",
                badge: "Masterpiece",
                artist: "StardustCreator",
                description: "A celestial journey through digital realms, capturing the essence of cosmic beauty.",
                attributes: [
                    { trait: "Rarity", value: "Divine" },
                    { trait: "Edition", value: "4 of 4" },
                    { trait: "Blockchain", value: "Ethereum" }
                ]
            },
            {
                id: 5,
                title: "Digital Royalty #005",
                collection: "Crown Collection",
                price: "21.0 ETH",
                image: "https://i.ibb.co/YBXK5Mg/a-striking-3d-illustration-of-a-t-shirt-hanging-on-h1-AIHpnz-TRK-8e-SADc-LFJw-l-Hs-Od-YYj-Sp-Wg6xv-U.jpg",
                badge: "Royal Edition",
                artist: "CrownMaster",
                description: "A royal masterpiece that sets new standards in digital art collecting.",
                attributes: [
                    { trait: "Rarity", value: "Royal" },
                    { trait: "Edition", value: "5 of 5" },
                    { trait: "Blockchain", value: "Ethereum" }
                ]
            }
        ];

        function createNFTCard(nft) {
            return `
                <div class="artwork-card" onclick="showNFTDetails(${nft.id})">
                    <div class="artwork-image">
                        <img src="${nft.image}" alt="${nft.title}">
                    </div>
                    <div class="artwork-info">
                        <h3 class="artwork-title">${nft.title}</h3>
                        <p class="artwork-collection">${nft.collection}</p>
                        <p class="artwork-price"><i class="fab fa-ethereum"></i> ${nft.price}</p>
                    </div>
                </div>
            `;
        }

        function createNFTDetails(nft) {
            return `
                <div class="nft-image-large">
                    <img src="${nft.image}" alt="${nft.title}">
                </div>
                <div class="nft-info">
                    <div class="info-section">
                        <h2 class="artwork-title">${nft.title}</h2>
                        <p class="artwork-collection">${nft.collection}</p>
                        <p class="artist">By ${nft.artist}</p>
                    </div>
                    <div class="info-section">
                        <div class="info-title">Description</div>
                        <div class="info-content">${nft.description}</div>
                    </div>
                    <div class="info-section">
                        <div class="info-title">Attributes</div>
                        <div class="info-content">
                            ${nft.attributes.map(attr => `
                                <div class="attribute">
                                    <span>${attr.trait}:</span> ${attr.value} 
                                    </div>
                            `).join('')}
                        </div>
                    </div>
                    <div class="info-section">
                        <div class="price-section">
                            <i class="fab fa-ethereum"></i>
                            <span>${nft.price}</span>
                        </div>
                    </div>
                    <div class="action-buttons">
                        <button class="action-btn buy-btn" onclick="purchaseNFT(${nft.id})">
                            Purchase Now
                        </button>
                        <button class="action-btn view-btn" onclick="viewOnMarket(${nft.id})">
                            View on Market
                        </button>
                    </div>
                </div>
            `;
        }

        class Carousel {
            constructor() {
                this.currentIndex = 0;
                this.carousel = document.querySelector('.carousel');
                this.prevButton = document.querySelector('.carousel-button.prev');
                this.nextButton = document.querySelector('.carousel-button.next');
                this.dotsContainer = document.querySelector('.carousel-dots');
                this.cards = [];
                this.touchStartX = 0;
                this.touchEndX = 0;

                this.initialize();
                this.setupEventListeners();
            }

            initialize() {
                // Create carousel items
                this.carousel.innerHTML = nftData.map(nft => createNFTCard(nft)).join('');
                this.cards = Array.from(document.querySelectorAll('.artwork-card'));
                
                // Create dots
                this.dotsContainer.innerHTML = nftData.map((_, index) => 
                    `<div class="dot ${index === 0 ? 'active' : ''}" data-index="${index}"></div>`
                ).join('');

                this.dots = Array.from(document.querySelectorAll('.dot'));
                this.updateCarousel();
            }

            setupEventListeners() {
                this.prevButton.addEventListener('click', () => this.slide('prev'));
                this.nextButton.addEventListener('click', () => this.slide('next'));
                
                // Dot navigation
                this.dots.forEach((dot, index) => {
                    dot.addEventListener('click', () => {
                        this.currentIndex = index;
                        this.updateCarousel();
                    });
                });

                // Touch events for mobile
                this.carousel.addEventListener('touchstart', (e) => {
                    this.touchStartX = e.touches[0].clientX;
                });

                this.carousel.addEventListener('touchend', (e) => {
                    this.touchEndX = e.changedTouches[0].clientX;
                    this.handleSwipe();
                });

                // Auto-advance carousel
                setInterval(() => this.slide('next'), 5000);

                // Pause auto-advance on hover
                this.carousel.addEventListener('mouseenter', () => this.pauseAutoAdvance());
                this.carousel.addEventListener('mouseleave', () => this.resumeAutoAdvance());

                // Handle window resize
                window.addEventListener('resize', () => this.updateCarousel());
            }

            handleSwipe() {
                const swipeDistance = this.touchEndX - this.touchStartX;
                const threshold = 50; // minimum distance for swipe

                if (Math.abs(swipeDistance) > threshold) {
                    if (swipeDistance > 0) {
                        this.slide('prev');
                    } else {
                        this.slide('next');
                    }
                }
            }

            slide(direction) {
                if (direction === 'next') {
                    this.currentIndex = (this.currentIndex + 1) % this.cards.length;
                } else {
                    this.currentIndex = (this.currentIndex - 1 + this.cards.length) % this.cards.length;
                }
                this.updateCarousel();
            }

            updateCarousel() {
                const cardWidth = this.cards[0].offsetWidth;
                const gap = 20; // matches CSS gap
                const offset = -(cardWidth + gap) * this.currentIndex;
                
                this.carousel.style.transform = `translateX(${offset}px)`;

                // Update active states
                this.cards.forEach((card, index) => {
                    card.classList.toggle('active', index === this.currentIndex);
                });

                this.dots.forEach((dot, index) => {
                    dot.classList.toggle('active', index === this.currentIndex);
                });

                // Show/hide navigation buttons
                this.prevButton.style.opacity = this.currentIndex === 0 ? '0.5' : '1';
                this.nextButton.style.opacity = this.currentIndex === this.cards.length - 1 ? '0.5' : '1';
            }

            pauseAutoAdvance() {
                clearInterval(this.autoAdvanceInterval);
            }

            resumeAutoAdvance() {
                this.autoAdvanceInterval = setInterval(() => this.slide('next'), 5000);
            }
        }

        // Modal functionality
        function showNFTDetails(id) {
            const modal = document.getElementById('nftModal');
            const nft = nftData.find(item => item.id === id);
            
            if (nft) {
                const detailsContainer = modal.querySelector('.nft-details');
                detailsContainer.innerHTML = createNFTDetails(nft);
                modal.style.display = 'block';
                document.body.style.overflow = 'hidden';
            }
        }

        document.querySelector('.modal-close').addEventListener('click', () => {
            const modal = document.getElementById('nftModal');
            modal.style.display = 'none';
            document.body.style.overflow = 'auto';
        });

        window.addEventListener('click', (event) => {
            const modal = document.getElementById('nftModal');
            if (event.target === modal) {
                modal.style.display = 'none';
                document.body.style.overflow = 'auto';
            }
        });

        function purchaseNFT(id) {
            alert(`Connecting wallet to purchase NFT #${id}...`);
        }

        function viewOnMarket(id) {
            alert(`Redirecting to marketplace for NFT #${id}...`);
        }

        // Initialize carousel when page loads
        window.onload = () => {
            new Carousel();
        };
    </script>
</body>
