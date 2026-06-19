<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Crowne Plaza Greater Noida – Luxury 5-Star Hotel | IHG Hotels</title>
    <meta name="description" content="Experience luxury at Crowne Plaza Greater Noida – a 5-star IHG hotel offering premium rooms, fine dining, spa, and world-class event venues near India Expo Mart." />
    <link rel="canonical" href="https://www.crowneplazagreaternoida.com/" />

    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,600;0,700;1,400&family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet" />

    <!-- Font Awesome -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" />

    <!-- Structured Data (JSON-LD) -->
    <script type="application/ld+json">
        {
            "@context": "https://schema.org",
            "@type": "Hotel",
            "name": "Crowne Plaza Greater Noida",
            "brand": "IHG Hotels & Resorts",
            "description": "Crowne Plaza Greater Noida is a luxury 5-star hotel offering premium accommodation, fine dining, wellness facilities, and world-class event venues.",
            "address": {
                "@type": "PostalAddress",
                "addressLocality": "Greater Noida",
                "addressRegion": "Uttar Pradesh",
                "addressCountry": "India"
            },
            "starRating": {
                "@type": "Rating",
                "ratingValue": "5"
            },
            "aggregateRating": {
                "@type": "AggregateRating",
                "ratingValue": "4.6",
                "reviewCount": "1200"
            },
            "telephone": "+91-XXXXXXXXXX",
            "priceRange": "₹8,000 - ₹18,000",
            "amenities": [
                "Free Wi-Fi",
                "Outdoor Pool",
                "Spa",
                "Fitness Centre",
                "Business Centre",
                "Airport Transfer",
                "Pet Friendly",
                "Room Service"
            ]
        }
    </script>

    <style>
        /* ===== CSS VARIABLES ===== */
        :root {
            --gold: #C9A96E;
            --gold-light: #E8D5A3;
            --gold-dark: #A8894A;
            --navy: #1A2634;
            --navy-light: #2C3E4E;
            --cream: #F8F5F0;
            --white: #FFFFFF;
            --black: #0A0A0A;
            --glass-bg: rgba(255, 255, 255, 0.12);
            --glass-border: rgba(255, 255, 255, 0.25);
            --glass-shadow: 0 8px 32px rgba(0, 0, 0, 0.15);
            --transition: 0.4s cubic-bezier(0.25, 0.46, 0.45, 0.94);
            --font-serif: 'Playfair Display', serif;
            --font-sans: 'Inter', sans-serif;
        }

        /* ===== RESET ===== */
        *,
        *::before,
        *::after {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        html {
            scroll-behavior: smooth;
            -webkit-font-smoothing: antialiased;
        }

        body {
            font-family: var(--font-sans);
            background: var(--cream);
            color: var(--navy);
            line-height: 1.6;
            overflow-x: hidden;
        }

        a {
            text-decoration: none;
            color: inherit;
        }
        img {
            max-width: 100%;
            display: block;
        }
        ul {
            list-style: none;
        }

        .container {
            max-width: 1280px;
            margin: 0 auto;
            padding: 0 24px;
        }

        /* ===== GLASSMORPHISM UTILITY ===== */
        .glass {
            background: var(--glass-bg);
            backdrop-filter: blur(16px) saturate(180%);
            -webkit-backdrop-filter: blur(16px) saturate(180%);
            border: 1px solid var(--glass-border);
            box-shadow: var(--glass-shadow);
        }

        .glass-dark {
            background: rgba(26, 38, 52, 0.55);
            backdrop-filter: blur(16px) saturate(180%);
            -webkit-backdrop-filter: blur(16px) saturate(180%);
            border: 1px solid rgba(255, 255, 255, 0.08);
        }

        /* ===== BUTTONS ===== */
        .btn {
            display: inline-flex;
            align-items: center;
            gap: 10px;
            padding: 14px 36px;
            font-family: var(--font-sans);
            font-weight: 600;
            font-size: 0.95rem;
            letter-spacing: 0.03em;
            border: none;
            border-radius: 50px;
            cursor: pointer;
            transition: var(--transition);
            text-transform: uppercase;
        }

        .btn-primary {
            background: var(--gold);
            color: var(--white);
        }
        .btn-primary:hover {
            background: var(--gold-dark);
            transform: translateY(-2px);
            box-shadow: 0 12px 28px rgba(201, 169, 110, 0.35);
        }

        .btn-outline {
            background: transparent;
            color: var(--white);
            border: 2px solid var(--gold);
        }
        .btn-outline:hover {
            background: var(--gold);
            color: var(--white);
            transform: translateY(-2px);
        }

        .btn-outline-dark {
            background: transparent;
            color: var(--navy);
            border: 2px solid var(--gold);
        }
        .btn-outline-dark:hover {
            background: var(--gold);
            color: var(--white);
            transform: translateY(-2px);
        }

        /* ===== SECTION HEADERS ===== */
        .section-header {
            text-align: center;
            margin-bottom: 56px;
        }

        .section-header .subtitle {
            font-family: var(--font-serif);
            font-style: italic;
            color: var(--gold);
            font-size: 1.1rem;
            letter-spacing: 0.1em;
            text-transform: uppercase;
            margin-bottom: 8px;
        }

        .section-header h2 {
            font-family: var(--font-serif);
            font-size: clamp(2.2rem, 5vw, 3.4rem);
            font-weight: 700;
            color: var(--navy);
            line-height: 1.2;
        }

        .section-header .line {
            width: 70px;
            height: 3px;
            background: var(--gold);
            margin: 16px auto 0;
            border-radius: 4px;
        }

        /* ===== NAVIGATION ===== */
        .navbar {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            z-index: 999;
            padding: 16px 0;
            transition: var(--transition);
        }

        .navbar.scrolled {
            background: rgba(26, 38, 52, 0.92);
            backdrop-filter: blur(20px) saturate(180%);
            -webkit-backdrop-filter: blur(20px) saturate(180%);
            padding: 10px 0;
            box-shadow: 0 4px 30px rgba(0, 0, 0, 0.2);
            border-bottom: 1px solid rgba(255, 255, 255, 0.06);
        }

        .navbar .container {
            display: flex;
            align-items: center;
            justify-content: space-between;
        }

        .navbar .logo {
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .navbar .logo-icon {
            width: 44px;
            height: 44px;
            background: var(--gold);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-family: var(--font-serif);
            font-weight: 700;
            font-size: 1.2rem;
            color: var(--white);
        }

        .navbar .logo-text {
            font-family: var(--font-serif);
            font-weight: 700;
            font-size: 1.3rem;
            color: var(--white);
            letter-spacing: 0.02em;
        }
        .navbar .logo-text span {
            color: var(--gold);
        }

        .navbar .logo-sub {
            font-size: 0.6rem;
            font-weight: 400;
            letter-spacing: 0.15em;
            text-transform: uppercase;
            opacity: 0.7;
            display: block;
            margin-top: -2px;
        }

        .nav-links {
            display: flex;
            align-items: center;
            gap: 28px;
        }

        .nav-links a {
            color: rgba(255, 255, 255, 0.85);
            font-size: 0.85rem;
            font-weight: 500;
            letter-spacing: 0.04em;
            text-transform: uppercase;
            transition: var(--transition);
            position: relative;
        }

        .nav-links a::after {
            content: '';
            position: absolute;
            bottom: -4px;
            left: 0;
            width: 0;
            height: 2px;
            background: var(--gold);
            transition: var(--transition);
        }

        .nav-links a:hover::after,
        .nav-links a.active::after {
            width: 100%;
        }
        .nav-links a:hover {
            color: var(--white);
        }

        .nav-cta {
            background: var(--gold);
            color: var(--white) !important;
            padding: 8px 22px;
            border-radius: 50px;
            font-weight: 600 !important;
        }
        .nav-cta:hover {
            background: var(--gold-dark) !important;
            transform: translateY(-1px);
        }
        .nav-cta::after {
            display: none !important;
        }

        /* Hamburger */
        .hamburger {
            display: none;
            flex-direction: column;
            gap: 5px;
            cursor: pointer;
            padding: 4px;
            background: none;
            border: none;
        }

        .hamburger span {
            display: block;
            width: 28px;
            height: 2px;
            background: var(--white);
            border-radius: 4px;
            transition: var(--transition);
        }

        .hamburger.active span:nth-child(1) {
            transform: rotate(45deg) translate(5px, 5px);
        }
        .hamburger.active span:nth-child(2) {
            opacity: 0;
        }
        .hamburger.active span:nth-child(3) {
            transform: rotate(-45deg) translate(5px, -5px);
        }

        /* ===== HERO ===== */
        .hero {
            position: relative;
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            text-align: center;
            padding: 120px 24px 80px;
            background: var(--navy);
            overflow: hidden;
        }

        .hero-bg {
            position: absolute;
            inset: 0;
            background:
                linear-gradient(135deg, rgba(26, 38, 52, 0.75) 0%, rgba(10, 10, 10, 0.55) 100%),
                url('https://images.unsplash.com/photo-1566073771259-6a8506099945?w=1600&q=80') center/cover no-repeat;
            animation: heroZoom 20s ease-in-out infinite alternate;
            z-index: 1;
        }

        @keyframes heroZoom {
            0% {
                transform: scale(1);
            }
            100% {
                transform: scale(1.06);
            }
        }

        .hero .container {
            position: relative;
            z-index: 2;
            max-width: 900px;
        }

        .hero-badge {
            display: inline-block;
            background: rgba(201, 169, 110, 0.2);
            border: 1px solid rgba(201, 169, 110, 0.3);
            padding: 6px 24px;
            border-radius: 50px;
            font-size: 0.75rem;
            font-weight: 600;
            letter-spacing: 0.15em;
            text-transform: uppercase;
            color: var(--gold-light);
            margin-bottom: 24px;
            backdrop-filter: blur(8px);
        }

        .hero h1 {
            font-family: var(--font-serif);
            font-size: clamp(2.8rem, 8vw, 5.2rem);
            font-weight: 700;
            color: var(--white);
            line-height: 1.08;
            margin-bottom: 16px;
            text-shadow: 0 4px 40px rgba(0, 0, 0, 0.3);
        }

        .hero h1 .highlight {
            color: var(--gold);
            position: relative;
        }

        .hero p {
            font-size: clamp(1rem, 1.4vw, 1.25rem);
            color: rgba(255, 255, 255, 0.8);
            max-width: 640px;
            margin: 0 auto 36px;
            font-weight: 300;
            line-height: 1.8;
        }

        .hero-actions {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            gap: 16px;
        }

        .hero-stats {
            display: flex;
            justify-content: center;
            gap: 48px;
            margin-top: 56px;
            padding-top: 40px;
            border-top: 1px solid rgba(255, 255, 255, 0.08);
        }

        .hero-stats .stat {
            text-align: center;
        }

        .hero-stats .stat-number {
            font-family: var(--font-serif);
            font-size: 2rem;
            font-weight: 700;
            color: var(--gold);
            display: block;
        }

        .hero-stats .stat-label {
            font-size: 0.75rem;
            text-transform: uppercase;
            letter-spacing: 0.08em;
            color: rgba(255, 255, 255, 0.6);
            margin-top: 4px;
        }

        /* floating glass cards */
        .hero-floating {
            position: absolute;
            z-index: 3;
            background: rgba(255, 255, 255, 0.06);
            backdrop-filter: blur(12px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            border-radius: 16px;
            padding: 16px 22px;
            color: var(--white);
            font-size: 0.8rem;
            box-shadow: 0 12px 40px rgba(0, 0, 0, 0.2);
            animation: float 6s ease-in-out infinite;
            pointer-events: none;
        }

        .hero-floating i {
            color: var(--gold);
            margin-right: 8px;
        }

        .hero-floating.f1 {
            top: 15%;
            left: 5%;
            animation-delay: 0s;
        }
        .hero-floating.f2 {
            bottom: 20%;
            right: 5%;
            animation-delay: 2s;
        }
        .hero-floating.f3 {
            top: 50%;
            right: 3%;
            animation-delay: 4s;
        }

        @keyframes float {
            0%,
            100% {
                transform: translateY(0);
            }
            50% {
                transform: translateY(-14px);
            }
        }

        /* ===== INTRO ===== */
        .intro {
            padding: 80px 0 60px;
            background: var(--white);
        }

        .intro-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 60px;
            align-items: center;
        }

        .intro-image {
            border-radius: 16px;
            overflow: hidden;
            position: relative;
            min-height: 380px;
            background: url('https://images.unsplash.com/photo-1582719508461-905c673771fd?w=800&q=80') center/cover no-repeat;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.12);
        }

        .intro-image .badge {
            position: absolute;
            bottom: 24px;
            left: 24px;
            background: rgba(0, 0, 0, 0.7);
            backdrop-filter: blur(8px);
            padding: 12px 20px;
            border-radius: 12px;
            color: var(--white);
            font-size: 0.8rem;
            border-left: 3px solid var(--gold);
        }

        .intro-content h3 {
            font-family: var(--font-serif);
            font-size: 2.2rem;
            font-weight: 700;
            color: var(--navy);
            margin-bottom: 12px;
        }

        .intro-content .gold-line {
            width: 60px;
            height: 3px;
            background: var(--gold);
            margin-bottom: 20px;
        }

        .intro-content p {
            color: #4a5a6a;
            font-size: 1.05rem;
            line-height: 1.8;
            margin-bottom: 16px;
        }

        .intro-features {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 12px 24px;
            margin-top: 24px;
        }

        .intro-features li {
            display: flex;
            align-items: center;
            gap: 10px;
            font-size: 0.95rem;
            color: var(--navy);
        }

        .intro-features li i {
            color: var(--gold);
            font-size: 1rem;
        }

        /* ===== ROOMS ===== */
        .rooms {
            padding: 80px 0;
            background: var(--cream);
        }

        .rooms-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
            gap: 32px;
        }

        .room-card {
            background: var(--white);
            border-radius: 20px;
            overflow: hidden;
            box-shadow: 0 8px 40px rgba(0, 0, 0, 0.06);
            transition: var(--transition);
            border: 1px solid rgba(201, 169, 110, 0.1);
        }

        .room-card:hover {
            transform: translateY(-8px);
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.1);
            border-color: var(--gold-light);
        }

        .room-card .image {
            height: 220px;
            background-size: cover;
            background-position: center;
            position: relative;
        }

        .room-card .image .tag {
            position: absolute;
            top: 16px;
            right: 16px;
            background: var(--gold);
            color: var(--white);
            padding: 4px 16px;
            border-radius: 50px;
            font-size: 0.7rem;
            font-weight: 600;
            text-transform: uppercase;
            letter-spacing: 0.06em;
        }

        .room-card .body {
            padding: 28px 28px 32px;
        }

        .room-card .body h3 {
            font-family: var(--font-serif);
            font-size: 1.4rem;
            font-weight: 700;
            color: var(--navy);
            margin-bottom: 4px;
        }

        .room-card .body .price {
            font-size: 1.2rem;
            font-weight: 700;
            color: var(--gold);
            margin-bottom: 12px;
        }
        .room-card .body .price small {
            font-weight: 400;
            font-size: 0.75rem;
            color: #6a7a8a;
        }

        .room-card .body .features {
            display: flex;
            flex-wrap: wrap;
            gap: 8px 14px;
            margin: 14px 0 20px;
        }

        .room-card .body .features li {
            font-size: 0.8rem;
            color: #4a5a6a;
            display: flex;
            align-items: center;
            gap: 6px;
        }

        .room-card .body .features li i {
            color: var(--gold);
            font-size: 0.75rem;
        }

        .room-card .body .btn {
            width: 100%;
            justify-content: center;
            padding: 12px;
        }

        /* ===== DINING ===== */
        .dining {
            padding: 80px 0;
            background: var(--white);
        }

        .dining-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 32px;
        }

        .dining-card {
            background: var(--cream);
            border-radius: 20px;
            padding: 36px 28px 32px;
            text-align: center;
            transition: var(--transition);
            border: 1px solid transparent;
            position: relative;
            overflow: hidden;
        }

        .dining-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 4px;
            background: linear-gradient(90deg, var(--gold), var(--gold-light));
            transform: scaleX(0);
            transition: var(--transition);
        }

        .dining-card:hover::before {
            transform: scaleX(1);
        }
        .dining-card:hover {
            border-color: rgba(201, 169, 110, 0.2);
            transform: translateY(-4px);
            box-shadow: 0 12px 40px rgba(0, 0, 0, 0.06);
        }

        .dining-card .icon {
            font-size: 2.8rem;
            color: var(--gold);
            margin-bottom: 16px;
        }

        .dining-card h3 {
            font-family: var(--font-serif);
            font-size: 1.5rem;
            font-weight: 700;
            color: var(--navy);
            margin-bottom: 4px;
        }

        .dining-card .cuisine {
            color: var(--gold);
            font-size: 0.85rem;
            font-weight: 500;
            letter-spacing: 0.04em;
            text-transform: uppercase;
            margin-bottom: 12px;
        }

        .dining-card p {
            color: #4a5a6a;
            font-size: 0.95rem;
            line-height: 1.7;
        }

        .dining-card .hours {
            margin-top: 16px;
            font-size: 0.8rem;
            color: var(--navy-light);
            font-weight: 500;
        }

        .dining-card .hours i {
            color: var(--gold);
            margin-right: 6px;
        }

        /* ===== AMENITIES ===== */
        .amenities {
            padding: 80px 0;
            background: var(--navy);
            color: var(--white);
        }

        .amenities .section-header h2 {
            color: var(--white);
        }
        .amenities .section-header .subtitle {
            color: var(--gold-light);
        }

        .amenities-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 32px;
        }

        .amenity-item {
            text-align: center;
            padding: 32px 16px;
            background: rgba(255, 255, 255, 0.04);
            border-radius: 16px;
            border: 1px solid rgba(255, 255, 255, 0.06);
            transition: var(--transition);
        }

        .amenity-item:hover {
            background: rgba(255, 255, 255, 0.08);
            transform: translateY(-4px);
            border-color: rgba(201, 169, 110, 0.2);
        }

        .amenity-item .icon {
            font-size: 2.4rem;
            color: var(--gold);
            margin-bottom: 12px;
        }

        .amenity-item h4 {
            font-family: var(--font-serif);
            font-size: 1.1rem;
            font-weight: 600;
            margin-bottom: 4px;
        }

        .amenity-item p {
            font-size: 0.85rem;
            opacity: 0.7;
        }

        /* ===== REVIEWS ===== */
        .reviews {
            padding: 80px 0;
            background: var(--white);
        }

        .reviews-top {
            display: flex;
            flex-wrap: wrap;
            justify-content: space-between;
            align-items: center;
            gap: 32px;
            margin-bottom: 48px;
        }

        .reviews-rating {
            display: flex;
            align-items: center;
            gap: 32px;
        }

        .reviews-rating .big-number {
            font-family: var(--font-serif);
            font-size: 3.6rem;
            font-weight: 700;
            color: var(--navy);
            line-height: 1;
        }

        .reviews-rating .big-number .stars {
            font-size: 1.2rem;
            color: var(--gold);
            display: block;
            margin-top: 4px;
        }

        .reviews-rating .detail {
            font-size: 0.9rem;
            color: #4a5a6a;
        }
        .reviews-rating .detail strong {
            color: var(--navy);
        }

        .reviews-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
            gap: 24px;
        }

        .review-card {
            background: var(--cream);
            padding: 28px;
            border-radius: 16px;
            border: 1px solid rgba(201, 169, 110, 0.1);
            transition: var(--transition);
        }

        .review-card:hover {
            border-color: var(--gold-light);
            transform: translateY(-2px);
        }

        .review-card .stars {
            color: var(--gold);
            font-size: 0.9rem;
            letter-spacing: 2px;
            margin-bottom: 8px;
        }

        .review-card blockquote {
            font-style: italic;
            color: #2a3a4a;
            font-size: 0.95rem;
            line-height: 1.7;
            margin-bottom: 12px;
        }

        .review-card .author {
            font-weight: 600;
            font-size: 0.85rem;
            color: var(--navy);
        }
        .review-card .author span {
            font-weight: 400;
            color: #6a7a8a;
            font-size: 0.8rem;
        }

        /* ===== GALLERY ===== */
        .gallery {
            padding: 80px 0;
            background: var(--cream);
        }

        .gallery-grid {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 16px;
        }

        .gallery-grid .item {
            border-radius: 16px;
            overflow: hidden;
            position: relative;
            aspect-ratio: 1/1;
            background-size: cover;
            background-position: center;
            cursor: pointer;
            transition: var(--transition);
        }

        .gallery-grid .item:hover {
            transform: scale(1.02);
            box-shadow: 0 12px 40px rgba(0, 0, 0, 0.15);
        }

        .gallery-grid .item .overlay {
            position: absolute;
            inset: 0;
            background: rgba(0, 0, 0, 0.3);
            display: flex;
            align-items: center;
            justify-content: center;
            opacity: 0;
            transition: var(--transition);
            color: var(--white);
            font-size: 1.6rem;
        }

        .gallery-grid .item:hover .overlay {
            opacity: 1;
        }

        .gallery-grid .item:nth-child(1) {
            grid-column: span 2;
            grid-row: span 2;
            aspect-ratio: auto;
        }

        /* ===== FAQ ===== */
        .faq {
            padding: 80px 0;
            background: var(--white);
        }

        .faq-list {
            max-width: 820px;
            margin: 0 auto;
        }

        .faq-item {
            border-bottom: 1px solid rgba(0, 0, 0, 0.06);
            padding: 20px 0;
        }

        .faq-item:last-child {
            border-bottom: none;
        }

        .faq-question {
            display: flex;
            justify-content: space-between;
            align-items: center;
            cursor: pointer;
            font-weight: 600;
            font-size: 1.05rem;
            color: var(--navy);
            gap: 16px;
            user-select: none;
        }

        .faq-question i {
            color: var(--gold);
            transition: var(--transition);
            font-size: 1.2rem;
        }

        .faq-item.open .faq-question i {
            transform: rotate(180deg);
        }

        .faq-answer {
            max-height: 0;
            overflow: hidden;
            transition: var(--transition);
            color: #4a5a6a;
            font-size: 0.95rem;
            line-height: 1.8;
        }

        .faq-item.open .faq-answer {
            max-height: 240px;
            padding-top: 14px;
        }

        /* ===== CONTACT / MAP ===== */
        .contact {
            padding: 80px 0;
            background: var(--cream);
        }

        .contact-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 48px;
        }

        .contact-info h3 {
            font-family: var(--font-serif);
            font-size: 2rem;
            font-weight: 700;
            margin-bottom: 8px;
        }

        .contact-info .gold-line {
            width: 50px;
            height: 3px;
            background: var(--gold);
            margin-bottom: 20px;
        }

        .contact-info p {
            color: #4a5a6a;
            margin-bottom: 24px;
            line-height: 1.8;
        }

        .contact-details {
            display: flex;
            flex-direction: column;
            gap: 14px;
        }

        .contact-details li {
            display: flex;
            align-items: center;
            gap: 14px;
            font-size: 0.95rem;
            color: var(--navy);
        }

        .contact-details li i {
            width: 36px;
            height: 36px;
            background: var(--gold);
            color: var(--white);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 0.9rem;
            flex-shrink: 0;
        }

        .contact-form {
            background: var(--white);
            padding: 36px 32px;
            border-radius: 20px;
            box-shadow: 0 8px 40px rgba(0, 0, 0, 0.06);
        }

        .contact-form h4 {
            font-family: var(--font-serif);
            font-size: 1.4rem;
            font-weight: 700;
            margin-bottom: 20px;
        }

        .form-group {
            margin-bottom: 18px;
        }

        .form-group label {
            display: block;
            font-size: 0.8rem;
            font-weight: 600;
            text-transform: uppercase;
            letter-spacing: 0.04em;
            color: var(--navy-light);
            margin-bottom: 4px;
        }

        .form-group input,
        .form-group select,
        .form-group textarea {
            width: 100%;
            padding: 12px 16px;
            border: 1px solid #e2e8f0;
            border-radius: 12px;
            font-family: var(--font-sans);
            font-size: 0.95rem;
            transition: var(--transition);
            background: var(--cream);
        }

        .form-group input:focus,
        .form-group select:focus,
        .form-group textarea:focus {
            outline: none;
            border-color: var(--gold);
            box-shadow: 0 0 0 4px rgba(201, 169, 110, 0.12);
            background: var(--white);
        }

        .form-group textarea {
            min-height: 110px;
            resize: vertical;
        }

        .form-row {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 16px;
        }

        .contact-form .btn {
            width: 100%;
            justify-content: center;
        }

        /* ===== MAP ===== */
        .map-section {
            padding: 0 0 80px;
            background: var(--cream);
        }

        .map-wrapper {
            border-radius: 20px;
            overflow: hidden;
            box-shadow: 0 8px 40px rgba(0, 0, 0, 0.06);
            border: 1px solid rgba(201, 169, 110, 0.1);
        }

        .map-wrapper iframe {
            width: 100%;
            height: 400px;
            border: none;
            display: block;
        }

        /* ===== FOOTER ===== */
        .footer {
            background: var(--navy);
            color: rgba(255, 255, 255, 0.7);
            padding: 60px 0 24px;
        }

        .footer-grid {
            display: grid;
            grid-template-columns: 2fr 1fr 1fr 1fr;
            gap: 40px;
            margin-bottom: 48px;
        }

        .footer-brand .logo-text {
            font-family: var(--font-serif);
            font-weight: 700;
            font-size: 1.6rem;
            color: var(--white);
        }
        .footer-brand .logo-text span {
            color: var(--gold);
        }

        .footer-brand p {
            margin-top: 12px;
            font-size: 0.9rem;
            line-height: 1.8;
            max-width: 320px;
        }

        .footer h4 {
            color: var(--white);
            font-weight: 600;
            font-size: 1rem;
            margin-bottom: 16px;
            letter-spacing: 0.04em;
        }

        .footer ul li {
            margin-bottom: 10px;
        }

        .footer ul li a {
            font-size: 0.9rem;
            transition: var(--transition);
        }

        .footer ul li a:hover {
            color: var(--gold);
            padding-left: 4px;
        }

        .footer-social {
            display: flex;
            gap: 12px;
            margin-top: 16px;
        }

        .footer-social a {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background: rgba(255, 255, 255, 0.06);
            display: flex;
            align-items: center;
            justify-content: center;
            color: var(--white);
            transition: var(--transition);
            border: 1px solid rgba(255, 255, 255, 0.06);
        }

        .footer-social a:hover {
            background: var(--gold);
            color: var(--white);
            transform: translateY(-3px);
            border-color: var(--gold);
        }

        .footer-bottom {
            border-top: 1px solid rgba(255, 255, 255, 0.06);
            padding-top: 24px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            gap: 12px;
            font-size: 0.8rem;
        }

        .footer-bottom a {
            transition: var(--transition);
        }
        .footer-bottom a:hover {
            color: var(--gold);
        }

        /* ===== WHATSAPP FLOAT ===== */
        .whatsapp-float {
            position: fixed;
            bottom: 28px;
            right: 28px;
            z-index: 999;
            width: 60px;
            height: 60px;
            background: #25D366;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            color: var(--white);
            font-size: 2rem;
            box-shadow: 0 8px 32px rgba(37, 211, 102, 0.4);
            transition: var(--transition);
            text-decoration: none;
        }

        .whatsapp-float:hover {
            transform: scale(1.1);
            box-shadow: 0 12px 48px rgba(37, 211, 102, 0.5);
        }

        /* ===== RESPONSIVE ===== */
        @media (max-width: 1024px) {
            .gallery-grid {
                grid-template-columns: repeat(3, 1fr);
            }
            .gallery-grid .item:nth-child(1) {
                grid-column: span 2;
                grid-row: span 2;
            }
            .footer-grid {
                grid-template-columns: 1fr 1fr;
            }
        }

        @media (max-width: 900px) {
            .intro-grid {
                grid-template-columns: 1fr;
                gap: 32px;
            }
            .intro-image {
                min-height: 280px;
            }
            .contact-grid {
                grid-template-columns: 1fr;
            }
            .hero-stats {
                gap: 28px;
                flex-wrap: wrap;
            }
            .hero-floating {
                display: none;
            }
        }

        @media (max-width: 768px) {
            .nav-links {
                position: fixed;
                top: 0;
                right: -100%;
                width: 80%;
                max-width: 340px;
                height: 100vh;
                background: rgba(26, 38, 52, 0.97);
                backdrop-filter: blur(24px);
                flex-direction: column;
                justify-content: center;
                padding: 40px;
                gap: 20px;
                transition: var(--transition);
                border-left: 1px solid rgba(255, 255, 255, 0.06);
            }

            .nav-links.open {
                right: 0;
            }

            .hamburger {
                display: flex;
                z-index: 1000;
            }

            .hero h1 {
                font-size: 2.6rem;
            }

            .rooms-grid {
                grid-template-columns: 1fr;
            }
            .dining-grid {
                grid-template-columns: 1fr;
            }
            .gallery-grid {
                grid-template-columns: 1fr 1fr;
            }
            .gallery-grid .item:nth-child(1) {
                grid-column: span 2;
                grid-row: span 1;
                aspect-ratio: 1/1;
            }

            .footer-grid {
                grid-template-columns: 1fr;
                gap: 32px;
            }
            .footer-bottom {
                flex-direction: column;
                text-align: center;
            }

            .form-row {
                grid-template-columns: 1fr;
            }

            .reviews-top {
                flex-direction: column;
                align-items: flex-start;
            }
            .reviews-rating {
                flex-wrap: wrap;
                gap: 12px;
            }

            .map-wrapper iframe {
                height: 280px;
            }

            .whatsapp-float {
                width: 52px;
                height: 52px;
                font-size: 1.6rem;
                bottom: 20px;
                right: 20px;
            }
        }

        @media (max-width: 480px) {
            .hero h1 {
                font-size: 2rem;
            }
            .hero-actions {
                flex-direction: column;
                align-items: center;
            }
            .hero-actions .btn {
                width: 100%;
                justify-content: center;
            }
            .hero-stats .stat-number {
                font-size: 1.5rem;
            }
            .section-header h2 {
                font-size: 1.8rem;
            }
            .intro-content h3 {
                font-size: 1.6rem;
            }
            .intro-features {
                grid-template-columns: 1fr;
            }
            .room-card .body {
                padding: 20px;
            }
            .contact-form {
                padding: 24px 18px;
            }
            .gallery-grid {
                gap: 8px;
            }
            .navbar .logo-text {
                font-size: 1rem;
            }
            .navbar .logo-sub {
                font-size: 0.5rem;
            }
        }
    </style>
</head>
<body>

    <!-- ===== NAVIGATION ===== -->
    <nav class="navbar" id="navbar" role="navigation" aria-label="Main navigation">
        <div class="container">
            <a href="#" class="logo" aria-label="Crowne Plaza Greater Noida Home">
                <div class="logo-icon">CP</div>
                <div>
                    <span class="logo-text">Crowne<span>Plaza</span></span>
                    <span class="logo-sub">Greater Noida</span>
                </div>
            </a>

            <ul class="nav-links" id="navLinks">
                <li><a href="#rooms">Rooms</a></li>
                <li><a href="#dining">Dining</a></li>
                <li><a href="#amenities">Amenities</a></li>
                <li><a href="#reviews">Reviews</a></li>
                <li><a href="#gallery">Gallery</a></li>
                <li><a href="#contact">Contact</a></li>
                <li><a href="#booking" class="nav-cta">Book Now</a></li>
            </ul>

            <button class="hamburger" id="hamburger" aria-label="Toggle menu" aria-expanded="false">
                <span></span><span></span><span></span>
            </button>
        </div>
    </nav>

    <!-- ===== HERO ===== -->
    <section class="hero" id="home" aria-label="Hero banner">
        <div class="hero-bg"></div>

        <!-- floating glass elements -->
        <div class="hero-floating f1"><i class="fas fa-star"></i> 4.6 / 5 · 1,200+ Reviews</div>
        <div class="hero-floating f2"><i class="fas fa-wifi"></i> Complimentary Wi-Fi</div>
        <div class="hero-floating f3"><i class="fas fa-swimmer"></i> Outdoor Pool &amp; Spa</div>

        <div class="container">
            <div class="hero-badge">✦ IHG Hotels &amp; Resorts</div>
            <h1>
                Luxury Redefined<br />
                <span class="highlight">in Greater Noida</span>
            </h1>
            <p>
                Experience world-class hospitality at Crowne Plaza Greater Noida —
                a 5-star sanctuary for business, leisure, and celebrations.
            </p>
            <div class="hero-actions">
                <a href="#booking" class="btn btn-primary">
                    <i class="fas fa-calendar-check"></i> Book Your Stay
                </a>
                <a href="#contact" class="btn btn-outline">
                    <i class="fas fa-phone-alt"></i> Contact Us
                </a>
            </div>
            <div class="hero-stats">
                <div class="stat">
                    <span class="stat-number">5★</span>
                    <span class="stat-label">Luxury Rating</span>
                </div>
                <div class="stat">
                    <span class="stat-number">4.6</span>
                    <span class="stat-label">Guest Score</span>
                </div>
                <div class="stat">
                    <span class="stat-number">12+</span>
                    <span class="stat-label">Dining &amp; Venues</span>
                </div>
                <div class="stat">
                    <span class="stat-number">24/7</span>
                    <span class="stat-label">Concierge Service</span>
                </div>
            </div>
        </div>
    </section>

    <!-- ===== INTRO ===== -->
    <section class="intro" aria-label="Hotel introduction">
        <div class="container">
            <div class="intro-grid">
                <div class="intro-image" role="img" aria-label="Luxury hotel interior">
                    <div class="badge">
                        <i class="fas fa-award" style="color:var(--gold);margin-right:6px;"></i>
                        IHG Premium Collection
                    </div>
                </div>
                <div class="intro-content">
                    <span class="subtitle" style="font-family:var(--font-serif);font-style:italic;color:var(--gold);font-size:1rem;letter-spacing:0.1em;text-transform:uppercase;">Welcome to</span>
                    <h3>Crowne Plaza Greater Noida</h3>
                    <div class="gold-line"></div>
                    <p>
                        Nestled in the heart of Greater Noida, our luxury hotel offers a seamless blend of
                        contemporary elegance and warm Indian hospitality. Designed for the modern traveler,
                        we provide premium accommodation, world-class dining, and state-of-the-art event spaces.
                    </p>
                    <p>
                        Whether you're here for business at the India Expo Mart, a weekend getaway, or a
                        grand wedding celebration, our dedicated team ensures every moment is extraordinary.
                    </p>
                    <ul class="intro-features">
                        <li><i class="fas fa-check-circle"></i> 5-Star Luxury</li>
                        <li><i class="fas fa-check-circle"></i> Business &amp; Leisure</li>
                        <li><i class="fas fa-check-circle"></i> Fine Dining</li>
                        <li><i class="fas fa-check-circle"></i> Wellness &amp; Spa</li>
                        <li><i class="fas fa-check-circle"></i> Event Venues</li>
                        <li><i class="fas fa-check-circle"></i> IHG Rewards</li>
                    </ul>
                </div>
            </div>
        </div>
    </section>

    <!-- ===== ROOMS ===== -->
    <section class="rooms" id="rooms" aria-label="Rooms and suites">
        <div class="container">
            <div class="section-header">
                <span class="subtitle">Luxurious Accommodations</span>
                <h2>Rooms &amp; Suites</h2>
                <div class="line"></div>
            </div>

            <div class="rooms-grid">
                <!-- Deluxe -->
                <div class="room-card">
                    <div class="image" style="background-image:url('https://images.unsplash.com/photo-1618773928121-c32242e63f39?w=800&q=80');">
                        <span class="tag">Most Popular</span>
                    </div>
                    <div class="body">
                        <h3>Deluxe Room</h3>
                        <div class="price">₹8,000 <small>/ night</small></div>
                        <ul class="features">
                            <li><i class="fas fa-wifi"></i> Free Wi-Fi</li>
                            <li><i class="fas fa-snowflake"></i> Air Conditioning</li>
                            <li><i class="fas fa-wine-bottle"></i> Mini Bar</li>
                            <li><i class="fas fa-city"></i> City View</li>
                            <li><i class="fas fa-bed"></i> Premium Bedding</li>
                        </ul>
                        <a href="#booking" class="btn btn-primary">Book Now</a>
                    </div>
                </div>

                <!-- Premium -->
                <div class="room-card">
                    <div class="image" style="background-image:url('https://images.unsplash.com/photo-1631049307264-da0ec9d70304?w=800&q=80');">
                        <span class="tag">Executive</span>
                    </div>
                    <div class="body">
                        <h3>Premium Room</h3>
                        <div class="price">₹12,000 <small>/ night</small></div>
                        <ul class="features">
                            <li><i class="fas fa-wifi"></i> Free Wi-Fi</li>
                            <li><i class="fas fa-crown"></i> Executive Lounge</li>
                            <li><i class="fas fa-tree"></i> Garden View</li>
                            <li><i class="fas fa-coffee"></i> Enhanced Amenities</li>
                            <li><i class="fas fa-concierge-bell"></i> Premium Comfort</li>
                        </ul>
                        <a href="#booking" class="btn btn-primary">Book Now</a>
                    </div>
                </div>

                <!-- Executive Suite -->
                <div class="room-card">
                    <div class="image" style="background-image:url('https://images.unsplash.com/photo-1582719508461-905c673771fd?w=800&q=80');">
                        <span class="tag">Signature</span>
                    </div>
                    <div class="body">
                        <h3>Executive Suite</h3>
                        <div class="price">₹18,000 <small>/ night</small></div>
                        <ul class="features">
                            <li><i class="fas fa-wifi"></i> Free Wi-Fi</li>
                            <li><i class="fas fa-vector-square"></i> Living Space</li>
                            <li><i class="fas fa-mountain"></i> Panoramic Views</li>
                            <li><i class="fas fa-gem"></i> Premium Amenities</li>
                            <li><i class="fas fa-star"></i> High-End Experience</li>
                        </ul>
                        <a href="#booking" class="btn btn-primary">Book Now</a>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- ===== DINING ===== -->
    <section class="dining" id="dining" aria-label="Dining experiences">
        <div class="container">
            <div class="section-header">
                <span class="subtitle">Culinary Excellence</span>
                <h2>Dining Experiences</h2>
                <div class="line"></div>
            </div>

            <div class="dining-grid">
                <!-- Mosaic -->
                <div class="dining-card">
                    <div class="icon"><i class="fas fa-utensils"></i></div>
                    <h3>Mosaic</h3>
                    <div class="cuisine">Global Cuisine</div>
                    <p>
                        A vibrant multi-cuisine restaurant offering breakfast buffets, lunch,
                        and dinner in a family-friendly setting. Savor the finest global flavors.
                    </p>
                    <div class="hours"><i class="far fa-clock"></i> Open daily until 11:00 PM</div>
                </div>

                <!-- ChaoBella -->
                <div class="dining-card">
                    <div class="icon"><i class="fas fa-wine-glass-alt"></i></div>
                    <h3>ChaoBella</h3>
                    <div class="cuisine">Italian Fine Dining</div>
                    <p>
                        Authentic Italian cuisine in an elegant setting. Perfect for romantic
                        dinners and special occasions with premium service.
                    </p>
                    <div class="hours"><i class="far fa-clock"></i> Open daily until 11:00 PM</div>
                </div>

                <!-- Belgian Beer Cafe -->
                <div class="dining-card">
                    <div class="icon"><i class="fas fa-beer"></i></div>
                    <h3>Belgian Beer Cafe</h3>
                    <div class="cuisine">Premium Lounge &amp; Bar</div>
                    <p>
                        Unwind with craft beers, casual dining, and evening entertainment
                        in a relaxed social atmosphere.
                    </p>
                    <div class="hours"><i class="far fa-clock"></i> Open daily until 12:00 AM</div>
                </div>
            </div>
        </div>
    </section>

    <!-- ===== AMENITIES ===== -->
    <section class="amenities" id="amenities" aria-label="Amenities and facilities">
        <div class="container">
            <div class="section-header">
                <span class="subtitle">World-Class Facilities</span>
                <h2>Premium Amenities</h2>
                <div class="line" style="background:var(--gold-light);"></div>
            </div>

            <div class="amenities-grid">
                <div class="amenity-item">
                    <div class="icon"><i class="fas fa-swimmer"></i></div>
                    <h4>Outdoor Pool</h4>
                    <p>Luxury pool for relaxation</p>
                </div>
                <div class="amenity-item">
                    <div class="icon"><i class="fas fa-spa"></i></div>
                    <h4>Spa &amp; Wellness</h4>
                    <p>Premium rejuvenation services</p>
                </div>
                <div class="amenity-item">
                    <div class="icon"><i class="fas fa-dumbbell"></i></div>
                    <h4>Fitness Centre</h4>
                    <p>Modern gym equipment</p>
                </div>
                <div class="amenity-item">
                    <div class="icon"><i class="fas fa-wifi"></i></div>
                    <h4>Free Wi-Fi</h4>
                    <p>High-speed internet access</p>
                </div>
                <div class="amenity-item">
                    <div class="icon"><i class="fas fa-parking"></i></div>
                    <h4>Complimentary Parking</h4>
                    <p>Secure parking area</p>
                </div>
                <div class="amenity-item">
                    <div class="icon"><i class="fas fa-concierge-bell"></i></div>
                    <h4>24/7 Room Service</h4>
                    <p>Around-the-clock dining</p>
                </div>
                <div class="amenity-item">
                    <div class="icon"><i class="fas fa-briefcase"></i></div>
                    <h4>Business Centre</h4>
                    <p>Meeting &amp; conference facilities</p>
                </div>
                <div class="amenity-item">
                    <div class="icon"><i class="fas fa-paw"></i></div>
                    <h4>Pet Friendly</h4>
                    <p>Welcome your furry friends</p>
                </div>
            </div>
        </div>
    </section>

    <!-- ===== REVIEWS ===== -->
    <section class="reviews" id="reviews" aria-label="Guest reviews">
        <div class="container">
            <div class="section-header">
                <span class="subtitle">Guest Feedback</span>
                <h2>What Our Guests Say</h2>
                <div class="line"></div>
            </div>

            <div class="reviews-top">
                <div class="reviews-rating">
                    <div class="big-number">
                        4.6
                        <span class="stars">★★★★★</span>
                    </div>
                    <div class="detail">
                        <strong>Excellent</strong> · 1,200+ verified reviews<br />
                        <span style="font-size:0.85rem;color:#6a7a8a;">
                            Google 4.5 · TripAdvisor 4.7 · Booking.com 4.4
                        </span>
                    </div>
                </div>
                <div style="display:flex;gap:8px;flex-wrap:wrap;">
                    <span style="background:var(--gold);color:var(--white);padding:4px 14px;border-radius:50px;font-size:0.75rem;font-weight:600;">Staff 94%</span>
                    <span style="background:var(--gold);color:var(--white);padding:4px 14px;border-radius:50px;font-size:0.75rem;font-weight:600;">Cleanliness 92%</span>
                    <span style="background:var(--gold);color:var(--white);padding:4px 14px;border-radius:50px;font-size:0.75rem;font-weight:600;">Comfort 89%</span>
                </div>
            </div>

            <div class="reviews-grid">
                <div class="review-card">
                    <div class="stars">★★★★★</div>
                    <blockquote>
                        “Exceptional hospitality from the moment we arrived. The staff went above and beyond.
                        The rooms are immaculate and the food at Mosaic was outstanding.”
                    </blockquote>
                    <div class="author">Amit S. <span>· Business Traveler</span></div>
                </div>
                <div class="review-card">
                    <div class="stars">★★★★★</div>
                    <blockquote>
                        “One of the finest luxury hotels in Greater Noida. The Belgian Beer Cafe is a must-visit.
                        Perfect for both work and leisure.”
                    </blockquote>
                    <div class="author">Priya R. <span>· Corporate Executive</span></div>
                </div>
                <div class="review-card">
                    <div class="stars">★★★★½</div>
                    <blockquote>
                        “We hosted our wedding here and it was magical. The team handled everything with
                        perfection. Highly recommended for events.”
                    </blockquote>
                    <div class="author">Vikram &amp; Neha <span>· Wedding Guests</span></div>
                </div>
            </div>
        </div>
    </section>

    <!-- ===== GALLERY ===== -->
    <section class="gallery" id="gallery" aria-label="Hotel gallery">
        <div class="container">
            <div class="section-header">
                <span class="subtitle">Visual Tour</span>
                <h2>Gallery</h2>
                <div class="line"></div>
            </div>

            <div class="gallery-grid">
                <div class="item" style="background-image:url('https://images.unsplash.com/photo-1566073771259-6a8506099945?w=800&q=80');">
                    <div class="overlay"><i class="fas fa-expand"></i></div>
                </div>
                <div class="item" style="background-image:url('https://images.unsplash.com/photo-1582719508461-905c673771fd?w=800&q=80');">
                    <div class="overlay"><i class="fas fa-expand"></i></div>
                </div>
                <div class="item" style="background-image:url('https://images.unsplash.com/photo-1618773928121-c32242e63f39?w=800&q=80');">
                    <div class="overlay"><i class="fas fa-expand"></i></div>
                </div>
                <div class="item" style="background-image:url('https://images.unsplash.com/photo-1631049307264-da0ec9d70304?w=800&q=80');">
                    <div class="overlay"><i class="fas fa-expand"></i></div>
                </div>
                <div class="item" style="background-image:url('https://images.unsplash.com/photo-1571896349842-33c89424de2d?w=800&q=80');">
                    <div class="overlay"><i class="fas fa-expand"></i></div>
                </div>
                <div class="item" style="background-image:url('https://images.unsplash.com/photo-1540541338287-41700207dee6?w=800&q=80');">
                    <div class="overlay"><i class="fas fa-expand"></i></div>
                </div>
            </div>
        </div>
    </section>

    <!-- ===== FAQ ===== -->
    <section class="faq" id="faq" aria-label="Frequently asked questions">
        <div class="container">
            <div class="section-header">
                <span class="subtitle">Have Questions?</span>
                <h2>Frequently Asked Questions</h2>
                <div class="line"></div>
            </div>

            <div class="faq-list">
                <div class="faq-item open">
                    <div class="faq-question">
                        <span>What are the check-in and check-out times?</span>
                        <i class="fas fa-chevron-down"></i>
                    </div>
                    <div class="faq-answer">
                        Check-in begins at 3:00 PM and check-out is at 12:00 PM. Early check-in and late check-out
                        are subject to availability and may incur additional charges.
                    </div>
                </div>
                <div class="faq-item">
                    <div class="faq-question">
                        <span>Does the hotel offer airport transfers?</span>
                        <i class="fas fa-chevron-down"></i>
                    </div>
                    <div class="faq-answer">
                        Yes, we provide airport transfer services for our guests. Please contact our concierge
                        team at least 24 hours in advance to arrange your transportation.
                    </div>
                </div>
                <div class="faq-item">
                    <div class="faq-question">
                        <span>Is the hotel pet-friendly?</span>
                        <i class="fas fa-chevron-down"></i>
                    </div>
                    <div class="faq-answer">
                        Yes, Crowne Plaza Greater Noida welcomes pets. Please inform us at the time of booking
                        so we can make appropriate arrangements for your furry companion.
                    </div>
                </div>
                <div class="faq-item">
                    <div class="faq-question">
                        <span>What dining options are available?</span>
                        <i class="fas fa-chevron-down"></i>
                    </div>
                    <div class="faq-answer">
                        We offer three distinct dining venues: Mosaic (global cuisine), ChaoBella (Italian fine dining),
                        and Belgian Beer Cafe (premium lounge &amp; bar). Room service is available 24/7.
                    </div>
                </div>
                <div class="faq-item">
                    <div class="faq-question">
                        <span>Does the hotel have a swimming pool and spa?</span>
                        <i class="fas fa-chevron-down"></i>
                    </div>
                    <div class="faq-answer">
                        Absolutely! Our luxury outdoor swimming pool and full-service spa &amp; wellness centre
                        are available for all guests to enjoy and rejuvenate.
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- ===== CONTACT + BOOKING ===== -->
    <section class="contact" id="contact" aria-label="Contact and booking">
        <div class="container">
            <div class="section-header">
                <span class="subtitle">Get in Touch</span>
                <h2>Contact &amp; Bookings</h2>
                <div class="line"></div>
            </div>

            <div class="contact-grid">
                <div class="contact-info">
                    <h3>We're Here to Help</h3>
                    <div class="gold-line"></div>
                    <p>
                        For reservations, event inquiries, or any assistance, our dedicated team is
                        available 24/7. Reach out to us and experience the Crowne Plaza hospitality.
                    </p>
                    <ul class="contact-details">
                        <li><i class="fas fa-map-marker-alt"></i> Greater Noida, Uttar Pradesh, India</li>
                        <li><i class="fas fa-phone"></i> +91-XXXXXXXXXX</li>
                        <li><i class="fas fa-envelope"></i> reservations@crowneplazagn.com</li>
                        <li><i class="fas fa-clock"></i> 24/7 Guest Services</li>
                        <li><i class="fab fa-whatsapp"></i> WhatsApp: +91-XXXXXXXXXX</li>
                    </ul>
                </div>

                <div class="contact-form" id="booking">
                    <h4>Book Your Stay</h4>
                    <form id="bookingForm" novalidate>
                        <div class="form-row">
                            <div class="form-group">
                                <label for="fullName">Full Name</label>
                                <input type="text" id="fullName" placeholder="John Doe" required />
                            </div>
                            <div class="form-group">
                                <label for="email">Email Address</label>
                                <input type="email" id="email" placeholder="john@example.com" required />
                            </div>
                        </div>
                        <div class="form-row">
                            <div class="form-group">
                                <label for="phone">Phone Number</label>
                                <input type="tel" id="phone" placeholder="+91 98765 43210" required />
                            </div>
                            <div class="form-group">
                                <label for="roomType">Room Type</label>
                                <select id="roomType">
                                    <option value="deluxe">Deluxe Room – ₹8,000/night</option>
                                    <option value="premium">Premium Room – ₹12,000/night</option>
                                    <option value="executive">Executive Suite – ₹18,000/night</option>
                                </select>
                            </div>
                        </div>
                        <div class="form-row">
                            <div class="form-group">
                                <label for="checkin">Check-In Date</label>
                                <input type="date" id="checkin" required />
                            </div>
                            <div class="form-group">
                                <label for="checkout">Check-Out Date</label>
                                <input type="date" id="checkout" required />
                            </div>
                        </div>
                        <div class="form-group">
                            <label for="message">Special Requests</label>
                            <textarea id="message" placeholder="Any special requests or additional information..."></textarea>
                        </div>
                        <button type="submit" class="btn btn-primary">
                            <i class="fas fa-calendar-check"></i> Check Availability
                        </button>
                    </form>
                </div>
            </div>
        </div>
    </section>

    <!-- ===== MAP ===== -->
    <section class="map-section" aria-label="Hotel location map">
        <div class="container">
            <div class="map-wrapper">
                <iframe
                src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d112345.67890123456!2d77.3456789!3d28.456789!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x390cfa9d0c1a2b3f%3A0x1234567890abcdef!2sGreater%20Noida%2C%20Uttar%20Pradesh!5e0!3m2!1sen!2sin!4v1700000000000"
                allowfullscreen=""
                loading="lazy"
                referrerpolicy="no-referrer-when-downgrade"
                title="Google Maps location of Crowne Plaza Greater Noida"
            ></iframe>
        </div>
    </div>
</section>

<!-- ===== FOOTER ===== -->
<footer class="footer" role="contentinfo">
    <div class="container">
        <div class="footer-grid">
            <div class="footer-brand">
                <div class="logo-text">Crowne<span>Plaza</span></div>
                <p style="font-size:0.85rem;opacity:0.7;margin-top:4px;">Greater Noida · An IHG Hotel</p>
                <p>
                    Luxury 5-star hospitality in Greater Noida. Premium rooms, fine dining,
                    wellness, and world-class event venues.
                </p>
                <div class="footer-social">
                    <a href="#" aria-label="Facebook"><i class="fab fa-facebook-f"></i></a>
                    <a href="#" aria-label="Instagram"><i class="fab fa-instagram"></i></a>
                    <a href="#" aria-label="Twitter"><i class="fab fa-twitter"></i></a>
                    <a href="#" aria-label="YouTube"><i class="fab fa-youtube"></i></a>
                    <a href="#" aria-label="LinkedIn"><i class="fab fa-linkedin-in"></i></a>
                </div>
            </div>
            <div>
                <h4>Quick Links</h4>
                <ul>
                    <li><a href="#rooms">Rooms &amp; Suites</a></li>
                    <li><a href="#dining">Dining</a></li>
                    <li><a href="#amenities">Amenities</a></li>
                    <li><a href="#gallery">Gallery</a></li>
                    <li><a href="#contact">Contact</a></li>
                </ul>
            </div>
            <div>
                <h4>Services</h4>
                <ul>
                    <li><a href="#">Business Centre</a></li>
                    <li><a href="#">Spa &amp; Wellness</a></li>
                    <li><a href="#">Event Venues</a></li>
                    <li><a href="#">Airport Transfer</a></li>
                    <li><a href="#">Concierge</a></li>
                </ul>
            </div>
            <div>
                <h4>Support</h4>
                <ul>
                    <li><a href="#faq">FAQ</a></li>
                    <li><a href="#contact">Contact Us</a></li>
                    <li><a href="#">Privacy Policy</a></li>
                    <li><a href="#">Terms &amp; Conditions</a></li>
                    <li><a href="#">IHG Rewards</a></li>
                </ul>
            </div>
        </div>
        <div class="footer-bottom">
            <span>&copy; 2026 Crowne Plaza Greater Noida. All rights reserved.</span>
            <span>
                <i class="fas fa-star" style="color:var(--gold);"></i>
                IHG Hotels &amp; Resorts · Luxury 5-Star
            </span>
        </div>
    </div>
</footer>

<!-- ===== WHATSAPP FLOAT ===== -->
<a href="https://wa.me/91XXXXXXXXXX?text=Hello%20Crowne%20Plaza%2C%20I%27d%20like%20to%20make%20a%20booking%20inquiry."
class="whatsapp-float"
target="_blank"
rel="noopener noreferrer"
aria-label="Contact us on WhatsApp">
<i class="fab fa-whatsapp"></i>
</a>

<!-- ===== JAVASCRIPT ===== -->
<script>
    (function() {
        'use strict';

        // ---- Navbar scroll ----
        const navbar = document.getElementById('navbar');
        let lastScroll = 0;

        window.addEventListener('scroll', function() {
            const currentScroll = window.pageYOffset || document.documentElement.scrollTop;
            if (currentScroll > 60) {
                navbar.classList.add('scrolled');
            } else {
                navbar.classList.remove('scrolled');
            }
            lastScroll = currentScroll;
        });

        // ---- Hamburger toggle ----
        const hamburger = document.getElementById('hamburger');
        const navLinks = document.getElementById('navLinks');

        hamburger.addEventListener('click', function() {
            const isOpen = navLinks.classList.toggle('open');
            hamburger.classList.toggle('active');
            hamburger.setAttribute('aria-expanded', isOpen);
        });

        // Close menu on link click (mobile)
        document.querySelectorAll('.nav-links a').forEach(function(link) {
            link.addEventListener('click', function() {
                navLinks.classList.remove('open');
                hamburger.classList.remove('active');
                hamburger.setAttribute('aria-expanded', 'false');
            });
        });

        // ---- FAQ accordion ----
        const faqItems = document.querySelectorAll('.faq-item');

        faqItems.forEach(function(item) {
            const question = item.querySelector('.faq-question');
            question.addEventListener('click', function() {
                const isOpen = item.classList.contains('open');

                // Close all others
                faqItems.forEach(function(other) {
                    other.classList.remove('open');
                });

                if (!isOpen) {
                    item.classList.add('open');
                }
            });
        });

        // ---- Booking form ----
        const bookingForm = document.getElementById('bookingForm');

        bookingForm.addEventListener('submit', function(e) {
            e.preventDefault();

            // Simple validation
            const name = document.getElementById('fullName').value.trim();
            const email = document.getElementById('email').value.trim();
            const phone = document.getElementById('phone').value.trim();
            const checkin = document.getElementById('checkin').value;
            const checkout = document.getElementById('checkout').value;

            if (!name || !email || !phone || !checkin || !checkout) {
                alert('Please fill in all required fields.');
                return;
            }

            if (!email.includes('@') || !email.includes('.')) {
                alert('Please enter a valid email address.');
                return;
            }

            // Simulate submission
            alert(
                'Thank you, ' + name +
                '! Your booking inquiry has been received. Our team will contact you shortly to confirm availability.'
                );
            bookingForm.reset();
        });

        // ---- Smooth anchor scroll ----
        document.querySelectorAll('a[href^="#"]').forEach(function(anchor) {
            anchor.addEventListener('click', function(e) {
                const targetId = this.getAttribute('href');
                if (targetId === '#') return;
                const targetElement = document.querySelector(targetId);
                if (targetElement) {
                    e.preventDefault();
                    const offsetTop = targetElement.getBoundingClientRect().top + window.pageYOffset -
                        80;
                    window.scrollTo({
                        top: offsetTop,
                        behavior: 'smooth'
                    });
                }
            });
        });

        // ---- Set min date on date inputs ----
        const today = new Date().toISOString().split('T')[0];
        const checkinInput = document.getElementById('checkin');
        const checkoutInput = document.getElementById('checkout');

        if (checkinInput) {
            checkinInput.setAttribute('min', today);
            checkinInput.addEventListener('change', function() {
                if (checkoutInput) {
                    checkoutInput.setAttribute('min', this.value);
                    if (checkoutInput.value && checkoutInput.value < this.value) {
                        checkoutInput.value = this.value;
                    }
                }
            });
        }

        if (checkoutInput) {
            checkoutInput.setAttribute('min', today);
        }

        // ---- Gallery lightbox (simple) ----
        const galleryItems = document.querySelectorAll('.gallery-grid .item');
        galleryItems.forEach(function(item) {
            item.addEventListener('click', function() {
                const bgImage = this.style.backgroundImage;
                if (bgImage) {
                    const url = bgImage.replace(/url\(["']?/, '').replace(/["']?\)/, '');
                    const overlay = document.createElement('div');
                    overlay.style.cssText = `
                                position: fixed; inset: 0; z-index: 9999;
                                background: rgba(0,0,0,0.88);
                                display: flex; align-items: center; justify-content: center;
                                cursor: pointer;
                                padding: 24px;
                                animation: fadeIn 0.3s ease;
                            `;
                    const img = document.createElement('img');
                    img.src = url;
                    img.style.cssText = `
                                max-width: 90vw; max-height: 85vh;
                                border-radius: 16px;
                                box-shadow: 0 24px 80px rgba(0,0,0,0.6);
                                object-fit: contain;
                            `;
                    overlay.appendChild(img);
                    document.body.appendChild(overlay);
                    overlay.addEventListener('click', function() {
                        this.remove();
                    });
                    // Close on escape
                    document.addEventListener('keydown', function handler(e) {
                        if (e.key === 'Escape') {
                            if (document.body.contains(overlay)) {
                                overlay.remove();
                            }
                            document.removeEventListener('keydown', handler);
                        }
                    });
                }
            });
        });

        // Add fadeIn keyframe dynamically
        const styleSheet = document.createElement('style');
        styleSheet.textContent = `
                    @keyframes fadeIn {
                        from { opacity: 0; transform: scale(0.96); }
                        to { opacity: 1; transform: scale(1); }
                    }
                `;
        document.head.appendChild(styleSheet);

        // ---- Active nav link on scroll ----
        const sections = document.querySelectorAll('section[id]');
        const navLinksAll = document.querySelectorAll('.nav-links a:not(.nav-cta)');

        window.addEventListener('scroll', function() {
            let current = '';
            sections.forEach(function(section) {
                const sectionTop = section.offsetTop - 120;
                if (window.pageYOffset >= sectionTop) {
                    current = section.getAttribute('id');
                }
            });

            navLinksAll.forEach(function(link) {
                link.classList.remove('active');
                if (link.getAttribute('href') === '#' + current) {
                    link.classList.add('active');
                }
            });
        });

        // ---- Performance: lazy load images (optional enhancement) ----
        // All images are already using background-image with URLs, fine.

        console.log('Crowne Plaza Greater Noida — Website loaded successfully.');
    })();
</script>

</body>
</html>
