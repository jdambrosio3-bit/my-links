<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Curated Product Portal</title>
    <style>
        :root {
            --bg-primary: #0f172a;
            --bg-secondary: #1e293b;
            --bg-card: #1e293b;
            --accent: #3b82f6;
            --accent-hover: #2563eb;
            --text-primary: #f8fafc;
            --text-secondary: #94a3b8;
            --success: #10b981;
            --border: #334155;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
        }

        body {
            background-color: var(--bg-primary);
            color: var(--text-primary);
            line-height: 1.5;
            padding-bottom: 60px;
        }

        /* Header Banner Layout */
        .hero-banner {
            background: linear-gradient(135deg, #0f172a 0%, #1e1b4b 100%);
            padding: 60px 20px;
            text-align: center;
            border-bottom: 1px solid var(--border);
            position: relative;
            overflow: hidden;
        }

        .hero-banner::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: radial-gradient(circle, rgba(59,130,246,0.1) 0%, transparent 50%);
            pointer-events: none;
        }

        .profile-container {
            width: 110px;
            height: 110px;
            margin: 0 auto 20px;
            border-radius: 50%;
            border: 3px solid var(--accent);
            overflow: hidden;
            box-shadow: 0 4px 20px rgba(0,0,0,0.4);
        }

        .profile-image {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }

        .hero-title {
            font-size: 2.5rem;
            font-weight: 800;
            margin-bottom: 12px;
            letter-spacing: -0.025em;
        }

        .hero-bio {
            max-width: 600px;
            margin: 0 auto 20px;
            color: var(--text-secondary);
            font-size: 1.1rem;
        }

        .social-links {
            display: flex;
            justify-content: center;
            gap: 12px;
            flex-wrap: wrap;
        }

        .social-icon {
            background: rgba(255,255,255,0.05);
            border: 1px solid var(--border);
            color: var(--text-primary);
            padding: 8px 16px;
            border-radius: 20px;
            text-decoration: none;
            font-size: 0.9rem;
            font-weight: 600;
            transition: all 0.2s ease;
        }

        .social-icon:hover {
            background: var(--accent);
            border-color: var(--accent);
            transform: translateY(-2px);
        }

        /* Control Panel */
        .controls-container {
            max-width: 1200px;
            margin: 40px auto 20px;
            padding: 0 20px;
        }

        .search-box {
            width: 100%;
            padding: 16px 20px;
            background-color: var(--bg-secondary);
            border: 1px solid var(--border);
            border-radius: 12px;
            color: var(--text-primary);
            font-size: 1.1rem;
            margin-bottom: 24px;
            box-shadow: 0 4px 6px -1px rgba(0,0,0,0.1);
            transition: border-color 0.2s;
        }

        .search-box:focus {
            outline: none;
            border-color: var(--accent);
        }

        .filter-tabs {
            display: flex;
            gap: 10px;
            overflow-x: auto;
            padding-bottom: 10px;
            scrollbar-width: thin;
        }

        .filter-tabs::-webkit-scrollbar {
            height: 6px;
        }

        .filter-tabs::-webkit-scrollbar-thumb {
            background: var(--border);
            border-radius: 3px;
        }

        .tab-btn {
            background-color: var(--bg-secondary);
            border: 1px solid var(--border);
            color: var(--text-secondary);
            padding: 10px 20px;
            border-radius: 30px;
            cursor: pointer;
            font-weight: 600;
            font-size: 0.95rem;
            white-space: nowrap;
            transition: all 0.2s ease;
        }

        .tab-btn:hover {
            border-color: var(--text-secondary);
            color: var(--text-primary);
        }

        .tab-btn.active {
            background-color: var(--accent);
            border-color: var(--accent);
            color: white;
        }

        /* Product Grid */
        .grid-container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
            gap: 30px;
        }

        .product-card {
            background-color: var(--bg-card);
            border: 1px solid var(--border);
            border-radius: 16px;
            overflow: hidden;
            display: flex;
            flex-direction: column;
            box-shadow: 0 10px 15px -3px rgba(0,0,0,0.3);
            transition: transform 0.2s, box-shadow 0.2s;
        }

        .product-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 20px 25px -5px rgba(0,0,0,0.4);
        }

        /* Image Container Zone */
        .image-container {
            position: relative;
            height: 220px;
            overflow: hidden;
            background-color: #0f172a;
        }

        .product-image {
            width: 100%;
            height: 100%;
            object-fit: cover;
            transition: transform 0.3s ease;
        }

        .product-card:hover .product-image {
            transform: scale(1.05);
        }

        .category-badge {
            position: absolute;
            top: 12px;
            left: 12px;
            background: rgba(15, 23, 42, 0.65);
            backdrop-filter: blur(4px);
            -webkit-backdrop-filter: blur(4px);
            color: var(--text-primary);
            padding: 4px 12px;
            border-radius: 20px;
            font-size: 0.75rem;
            font-weight: 700;
            border: 1px solid rgba(255,255,255,0.1);
            letter-spacing: 0.05em;
            text-transform: uppercase;
            z-index: 2;
        }

        .card-content {
            padding: 24px;
            display: flex;
            flex-direction: column;
            flex-grow: 1;
        }

        .product-title {
            font-size: 1.25rem;
            font-weight: 700;
            margin-bottom: 8px;
            color: var(--text-primary);
        }

        .product-desc {
            color: var(--text-secondary);
            font-size: 0.95rem;
            margin-bottom: 20px;
            flex-grow: 1;
        }

        .card-footer {
            display: flex;
            flex-direction: column;
            gap: 12px;
            margin-top: auto;
        }

        .stats-row {
            display: flex;
            justify-content: space-between;
            align-items: center;
            font-size: 0.85rem;
            color: var(--text-secondary);
            border-top: 1px solid var(--border);
            padding-top: 12px;
        }

        .action-row {
            display: flex;
            gap: 8px;
        }

        .btn-main {
            flex-grow: 1;
            background-color: var(--accent);
            color: white;
            text-align: center;
            padding: 12px;
            border-radius: 8px;
            text-decoration: none;
            font-weight: 600;
            font-size: 0.95rem;
            transition: background-color 0.2s;
        }

        .btn-main:hover {
            background-color: var(--accent-hover);
        }

        .btn-copy {
            background-color: rgba(255,255,255,0.05);
            border: 1px solid var(--border);
            color: var(--text-primary);
            width: 46px;
            height: 46px;
            border-radius: 8px;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: all 0.2s;
        }

        .btn-copy:hover {
            background-color: rgba(255,255,255,0.1);
            border-color: var(--text-secondary);
        }

        .btn-copy.copied {
            background-color: var(--success);
            border-color: var(--success);
            color: white;
        }

        /* Fallback State */
        #noResults {
            grid-column: 1 / -1;
            text-align: center;
            padding: 60px 20px;
            color: var(--text-secondary);
            display: none;
        }

        #noResults svg {
            margin-bottom: 16px;
            color: var(--border);
        }
    </style>
</head>
<body>

    <!-- Header Layout Banner -->
    <header class="hero-banner">
        <div class="profile-container">
            <img src="https://images.unsplash.com/photo-1534528741775-53994a69daeb?auto=format&fit=crop&w=256&h=256&q=80" alt="Creator Profile" class="profile-image">
        </div>
        <h1 class="hero-title">My Recommended Products</h1>
        <p class="hero-bio">Welcome! Browse my hand-picked curation of favorite products, tech setups, essentials, and recommendations across my top categories.</p>
        <div class="social-links">
            <a href="#" class="social-icon">YouTube</a>
            <a href="#" class="social-icon">Instagram</a>
            <a href="#" class="social-icon">TikTok</a>
        </div>
    </header>

    <!-- Control Panel -->
    <div class="controls-container">
        <input type="text" id="searchBar" class="search-box" placeholder="Search products, brands, keywords...">
        
        <div class="filter-tabs">
            <button class="tab-btn active" data-filter="all">All Items</button>
            <button class="tab-btn" data-filter="tech-gear">Tech Gear</button>
            <button class="tab-btn" data-filter="gaming">Gaming</button>
            <button class="tab-btn" data-filter="fashion">Fashion</button>
            <button class="tab-btn" data-filter="fitness">Fitness</button>
            <button class="tab-btn" data-filter="wellness">Wellness</button>
            <button class="tab-btn" data-filter="organic-food">Organic Food</button>
            <button class="tab-btn" data-filter="appliances">Appliances</button>
            <button class="tab-btn" data-filter="beauty-care">Beauty Care</button>
            <button class="tab-btn" data-filter="music">Music</button>
            <button class="tab-btn" data-filter="life-safety">Life Safety</button>
        </div>
    </div>

    <!-- Product Grid -->
    <main class="grid-container" id="productGrid">
        
        <!-- Tech Gear Card -->
        <div class="product-card" data-category="tech-gear">
            <div class="image-container">
                <span class="category-badge">Tech Gear</span>
                <img src="https://images.unsplash.com/photo-1542751371-adc38448a05e?auto=format&fit=crop&w=600&q=80" alt="Mechanical Keyboard" class="product-image">
            </div>
            <div class="card-content">
                <h3 class="product-title">Pro Mechanical Keyboard</h3>
                <p class="product-desc">Hot-swappable mechanical switches, premium aluminum framing, and custom RGB layout configuration options.</p>
                <div class="card-footer">
                    <div class="stats-row">
                        <span class="clicks-count" id="clicks-tech-01">0 clicks</span>
                        <span>Verified Item</span>
                    </div>
                    <div class="action-row">
                        <a href="YOUR_AFFILIATE_URL_HERE" target="_blank" class="btn-main" data-id="tech-01">View Product</a>
                        <button class="btn-copy" data-url="YOUR_AFFILIATE_URL_HERE" title="Copy link">
                            <svg width="20" height="20" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M8 16H6a2 2 0 01-2-2V6a2 2 0 012-2h8a2 2 0 012 2v2m-6 12h8a2 2 0 002-2v-8a2 2 0 00-2-2h-8a2 2 0 00-2 2v8a2 2 0 002 2z"></path></svg>
                        </button>
                    </div>
                </div>
            </div>
        </div>

        <!-- Gaming Card -->
        <div class="product-card" data-category="gaming">
            <div class="image-container">
                <span class="category-badge">Gaming</span>
                <img src="https://images.unsplash.com/photo-1600861195091-690c92f1d2cc?auto=format&fit=crop&w=600&q=80" alt="Gaming Mouse" class="product-image">
            </div>
            <div class="card-content">
                <h3 class="product-title">Ultra-Light Wireless Gaming Mouse</h3>
                <p class="product-desc">Sub-60g competitive gaming mouse featuring an enterprise-grade 26K DPI sensor and near-zero latency click metrics.</p>
                <div class="card-footer">
                    <div class="stats-row">
                        <span class="clicks-count" id="clicks-game-01">0 clicks</span>
                        <span>Top Rated</span>
                    </div>
                    <div class="action-row">
                        <a href="YOUR_AFFILIATE_URL_HERE" target="_blank" class="btn-main" data-id="game-01">View Product</a>
                        <button class="btn-copy" data-url="YOUR_AFFILIATE_URL_HERE" title="Copy link">
                            <svg width="20" height="20" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M8 16H6a2 2 0 01-2-2V6a2 2 0 012-2h8a2 2 0 012 2v2m-6 12h8a2 2 0 002-2v-8a2 2 0 00-2-2h-8a2 2 0 00-2 2v8a2 2 0 002 2z"></path></svg>
                        </button>
                    </div>
                </div>
            </div>
        </div>

        <!-- Fashion Card -->
        <div class="product-card" data-category="fashion">
            <div class="image-container">
                <span class="category-badge">Fashion</span>
                <img src="https://images.unsplash.com/photo-1591047139829-d91aecb6caea?auto=format&fit=crop&w=600&q=80" alt="Minimalist Jacket" class="product-image">
            </div>
            <div class="card-content">
                <h3 class="product-title">Minimalist Bomber Jacket</h3>
                <p class="product-desc">Water-resistant, lightweight insulation material engineered for daily commuting layouts and stylish modern silhouettes.</p>
                <div class="card-footer">
                    <div class="stats-row">
                        <span class="clicks-count" id="clicks-fash-01">0 clicks</span>
                        <span>Premium Blend</span>
                    </div>
                    <div class="action-row">
                        <a href="YOUR_AFFILIATE_URL_HERE" target="_blank" class="btn-main" data-id="fash-01">View Product</a>
                        <button class="btn-copy" data-url="YOUR_AFFILIATE_URL_HERE" title="Copy link">
                            <svg width="20" height="20" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M8 16H6a2 2 0 01-2-2V6a2 2 0 012-2h8a2 2 0 012 2v2m-6 12h8a2 2 0 002-2v-8a2 2 0 00-2-2h-8a2 2 0 00-2 2v8a2 2 0 002 2z"></path></svg>
                        </button>
                    </div>
                </div>
            </div>
        </div>

        <!-- Fitness Card -->
        <div class="product-card" data-category="fitness">
            <div class="image-container">
                <span class="category-badge">Fitness</span>
                <img src="https://images.unsplash.com/photo-1517838277536-f5f99be501cd?auto=format&fit=crop&w=600&q=80" alt="Resistance Bands" class="product-image">
            </div>
            <div class="card-content">
                <h3 class="product-title">Premium Resistance Bands</h3>
                <p class="product-desc">Heavy-duty natural latex resistance loops with custom carry bags, rated across progressive tension barriers.</p>
                <div class="card-footer">
                    <div class="stats-row">
                        <span class="clicks-count" id="clicks-fit-01">0 clicks</span>
                        <span>Daily Gear</span>
                    </div>
                    <div class="action-row">
                        <a href="YOUR_AFFILIATE_URL_HERE" target="_blank" class="btn-main" data-id="fit-01">View Product</a>
                        <button class="btn-copy" data-url="YOUR_AFFILIATE_URL_HERE" title="Copy link">
                            <svg width="20" height="20" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M8 16H6a2 2 0 01-2-2V6a2 2 0 012-2h8a2 2 0 012 2v2m-6 12h8a2 2 0 002-2v-8a2 2 0 00-2-2h-8a2 2 0 00-2 2v8a2 2 0 002 2z"></path></svg>
                        </button>
                    </div>
                </div>
            </div>
        </div>

        <!-- Wellness Card -->
        <div class="product-card" data-category="wellness">
            <div class="image-container">
                <span class="category-badge">Wellness</span>
                <img src="https://images.unsplash.com/photo-1608571423902-eed4a5ad8108?auto=format&fit=crop&w=600&q=80" alt="Essential Oil Diffuser" class="product-image">
            </div>
            <div class="card-content">
                <h3 class="product-title">Ultrasonic Humidifier & Diffuser</h3>
                <p class="product-desc">Whisper-quiet ambient mist humidifier supporting therapeutic essential oil delivery with integrated auto-shutoff parameters.</p>
                <div class="card-footer">
                    <div class="stats-row">
                        <span class="clicks-count" id="clicks-well-01">0 clicks</span>
                        <span>Eco Certified</span>
                    </div>
                    <div class="action-row">
                        <a href="YOUR_AFFILIATE_URL_HERE" target="_blank" class="btn-main" data-id="well-01">View Product</a>
                        <button class="btn-copy" data-url="YOUR_AFFILIATE_URL_HERE" title="Copy link">
                            <svg width="20" height="20" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M8 16H6a2 2 0 01-2-2V6a2 2 0 012-2h8a2 2 0 012 2v2m-6 12h8a2 2 0 002-2v-8a2 2 0 00-2-2h-8a2 2 0 00-2 2v8a2 2 0 002 2z"></path></svg>
                        </button>
                    </div>
                </div>
            </div>
        </div>

        <!-- Organic Food Card -->
        <div class="product-card" data-category="organic-food">
            <div class="image-container">
                <span class="category-badge">Organic Food</span>
                <img src="https://images.unsplash.com/photo-1540420773420-3366772f4999?auto=format&fit=crop&w=600&q=80" alt="Organic Green Tea Blend" class="product-image">
            </div>
            <div class="card-content">
                <h3 class="product-title">Premium Matcha Green Tea</h3>
                <p class="product-desc">100% stone-ground ceremonial grade organic matcha. Shaded-grown without synthetic additives or artificial processing elements.</p>
                <div class="card-footer">
                    <div class="stats-row">
                        <span class="clicks-count" id="clicks-food-01">0 clicks</span>
                        <span>USDA Organic</span>
                    </div>
                    <div class="action-row">
                        <a href="YOUR_AFFILIATE_URL_HERE" target="_blank" class="btn-main" data-id="food-01">View Product</a>
                        <button class="btn-copy" data-url="YOUR_AFFILIATE_URL_HERE" title="Copy link">
                            <svg width="20" height="20" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M8 16H6a2 2 0 01-2-2V6a2 2 0 012-2h8a2 2 0 012 2v2m-6 12h8a2 2 0 002-2v-8a2 2 0 00-2-2h-8a2 2 0 00-2 2v8a2 2 0 002 2z"></path></svg>
                        </button>
                    </div>
                </div>
            </div>
        </div>

        <!-- Appliances Card -->
        <div class="product-card" data-category="appliances">
            <div class="image-container">
                <span class="category-badge">Appliances</span>
                <img src="https://images.unsplash.com/photo-1588854337236-6889d631faa8?auto=format&fit=crop&w=600&q=80" alt="Smart Air Fryer" class="product-image">
            </div>
            <div class="card-content">
                <h3 class="product-title">Smart Countertop Air Fryer</h3>
                <p class="product-desc">Multi-zone convection basket with digital app synchronization profiles for precise, rapid heat distributions.</p>
                <div class="card-footer">
                    <div class="stats-row">
                        <span class="clicks-count" id="clicks-app-01">0 clicks</span>
                        <span>Energy Saver</span>
                    </div>
                    <div class="action-row">
                        <a href="YOUR_AFFILIATE_URL_HERE" target="_blank" class="btn-main" data-id="app-01">View Product</a>
                        <button class="btn-copy" data-url="YOUR_AFFILIATE_URL_HERE" title="Copy link">
                            <svg width="20" height="20" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M8 16H6a2 2 0 01-2-2V6a2 2 0 012-2h8a2 2 0 012 2v2m-6 12h8a2 2 0 002-2v-8a2 2 0 00-2-2h-8a2 2 0 00-2 2v8a2 2 0 002 2z"></path></svg>
                        </button>
                    </div>
                </div>
            </div>
        </div>

        <!-- Beauty Care Card -->
        <div class="product-card" data-category="beauty-care">
            <div class="image-container">
                <span class="category-badge">Beauty Care</span>
                <img src="https://images.unsplash.com/photo-1601049541289-9b1b7bbbfe19?auto=format&fit=crop&w=600&q=80" alt="Hydrating Serum" class="product-image">
            </div>
            <div class="card-content">
                <h3 class="product-title">Hyaluronic Acid Hydration Serum</h3>
                <p class="product-desc">Advanced multi-molecular moisture matrix compound supporting structural skin restoration and brightening characteristics.</p>
                <div class="card-footer">
                    <div class="stats-row">
                        <span class="clicks-count" id="clicks-beau-01">0 clicks</span>
                        <span>Cruelty Free</span>
                    </div>
                    <div class="action-row">
                        <a href="YOUR_AFFILIATE_URL_HERE" target="_blank" class="btn-main" data-id="beau-01">View Product</a>
                        <button class="btn-copy" data-url="YOUR_AFFILIATE_URL_HERE" title="Copy link">
                            <svg width="20" height="20" fill="none" stroke="currentColor" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M8 16H6a2 2 0 01-2-2V6a2 2 0 012-2h8a2 2 0 012 2v2m-6 12h8a2 2 0 002-2v-8a2 2 0 00-2-2h-8a2 2 0 00-2 2v8a2 2 0 002 2z"></path></svg>
                        </button>
                    </div>
                </div>
            </div>
        </div>

        <!-- Music Card -->
        <div class="product-card" data-category="music">
            <div class="image-container">
                <span class="category-badge">Music</span>
                <img src="https://images.unsplash.com/photo-1546435770-a3e426bf472b?auto=format&fit=crop&w=600&q=80" alt="Studio Headphones" class="product-image">
            </div>
            <div class="card-content">
                <h3 class="product-title">Studio Monitor Headphones</h3>
                <p class="product-desc">Professional neutral frequency monitors engineered for precision audio mixing layouts and high fidelity isolation performance.</p>
                <div class="card-footer">
                    <div class="stats-row">
                        <span class="clicks-count" id="clicks-mus-01">0 clicks</span>
                        <span>Reference Grade</span>
                    </div>
                    <div class="action-row">
                        <a href="YOUR_AFFILIATE_URL_HERE" target="_blank" class="btn-main" data-id="mus-01">View Product</a>
                        <button class="btn-copy" data-url="YOUR_AFFILIATE_URL_HERE" title="Copy link">
                            <svg width="20" height="20" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M8 16H6a2 2 0 01-2-2V6a2 2 0 012-2h8a2 2 0 012 2v2m-6 12h8a2 2 0 002-2v-8a2 2 0 00-2-2h-8a2 2 0 00-2 2v8a2 2 0 002 2z"></path></svg>
                        </button>
                    </div>
                </div>
            </div>
        </div>

        <!-- Life Safety Card -->
        <div class="product-card" data-category="life-safety">
            <div class="image-container">
                <span class="category-badge">Life Safety</span>
                <img src="https://images.unsplash.com/photo-1584308666744-24d5c474f2ae?auto=format&fit=crop&w=600&q=80" alt="Emergency First Aid Kit" class="product-image">
            </div>
            <div class="card-content">
                <h3 class="product-title">Comprehensive Emergency First Aid Kit</h3>
                <p class="product-desc">OSHA-compliant, weather-proof medical response array structured with heavy-duty trauma care modules and wilderness safety tools.</p>
                <div class="card-footer">
                    <div class="stats-row">
                        <span class="clicks-count" id="clicks-safe-01">0 clicks</span>
                        <span>Safety Rated</span>
                    </div>
                    <div class="action-row">
                        <a href="YOUR_AFFILIATE_URL_HERE" target="_blank" class="btn-main" data-id="safe-01">View Product</a>
                        <button class="btn-copy" data-url="YOUR_AFFILIATE_URL_HERE" title="Copy link">
                            <svg width="20" height="20" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M8 16H6a2 2 0 01-2-2V6a2 2 0 012-2h8a2 2 0 012 2v2m-6 12h8a2 2 0 002-2v-8a2 2 0 00-2-2h-8a2 2 0 00-2 2v8a2 2 0 002 2z"></path></svg>
                        </button>
                    </div>
                </div>
            </div>
        </div>

        <!-- Fallback Message -->
        <div id="noResults">
            <svg width="48" height="48" fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24" style="margin: 0 auto 12px;"><path stroke-linecap="round" stroke-linejoin="round" d="M21 21l-5.197-5.197m0 0A7.5 7.5 0 105.196 5.196a7.5 7.5 0 0010.607 10.607z"></path></svg>
            <p>No products found matching your active filter criteria.</p>
        </div>

    </main>

    <script>
        // DOM Elements
        const searchBar = document.getElementById('searchBar');
        const filterButtons = document.querySelectorAll('.tab-btn');
        const productCards = document.querySelectorAll('.product-card');
        const noResults = document.getElementById('noResults');

        let activeFilter = 'all';

        // 1. Unified Filtering System (Search + Tabs)
        function filterProducts() {
            const query = searchBar.value.toLowerCase().trim();
            let visibleCount = 0;

            productCards.forEach(card => {
                const category = card.getAttribute('data-category');
                const title = card.querySelector('.product-title').textContent.toLowerCase();
                const desc = card.querySelector('.product-desc').textContent.toLowerCase();
                
                const matchesFilter = (activeFilter === 'all' || category === activeFilter);
                const matchesSearch = (title.includes(query) || desc.includes(query));

                if (matchesFilter && matchesSearch) {
                    card.style.display = 'flex';
                    visibleCount++;
                } else {
                    card.style.display = 'none';
                }
            });

            noResults.style.display = visibleCount === 0 ? 'block' : 'none';
        }

        // 2. Tab Event Listeners
        filterButtons.forEach(btn => {
            btn.addEventListener('click', () => {
                filterButtons.forEach(b => b.classList.remove('active'));
                btn.classList.add('active');
                activeFilter = btn.getAttribute('data-filter');
                filterProducts();
            });
        });

        // Search Input Listener
        searchBar.addEventListener('input', filterProducts);

        // 3. Persistent Click Tracker Mechanics
        function initClickTracker() {
            productCards.forEach(card => {
                const linkButton = card.querySelector('.btn-main');
                const id = linkButton.getAttribute('data-id');
                const statsDisplay = card.querySelector('.clicks-count');

                // Load initial count state from LocalStorage
                let currentCount = localStorage.getItem(`click_count_${id}`) || 0;
                statsDisplay.textContent = `${currentCount} click${currentCount == 1 ? '' : 's'}`;

                // Handle live tracking increments
                linkButton.addEventListener('click', () => {
                    currentCount++;
                    localStorage.setItem(`click_count_${id}`, currentCount);
                    statsDisplay.textContent = `${currentCount} click${currentCount == 1 ? '' : 's'}`;
                });
            });
        }

        // 4. Asynchronous Copy-To-Clipboard Script
        function initClipboard() {
            const copyButtons = document.querySelectorAll('.btn-copy');

            copyButtons.forEach(btn => {
                btn.addEventListener('click', async () => {
                    const urlToCopy = btn.getAttribute('data-url');
                    
                    try {
                        await navigator.clipboard.writeText(urlToCopy);
                        
                        // Active Visual Success State Transition
                        btn.classList.add('copied');
                        const originalSvg = btn.innerHTML;
                        btn.innerHTML = `<svg width="20" height="20" fill="none" stroke="currentColor" stroke-width="2.5" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M4.5 12.75l6 6 9-13.5"></path></svg>`;

                        // Auto Restorative visual reset
                        setTimeout(() => {
                            btn.classList.remove('copied');
                            btn.innerHTML = originalSvg;
                        }, 2000);

                    } catch (err) {
                        console.error('Failed to copy text string properties: ', err);
                    }
                });
            });
        }

        // Initialize script dependencies on launch
        document.addEventListener('DOMContentLoaded', () => {
            initClickTracker();
            initClipboard();
        });
    </script>
</body>
</html>
