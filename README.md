<!DOCTYPE html>
<html lang="uz">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Qadrdon Xotiralar — Oilaviy Jonli Fotoalbom</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Google Fonts: Lora (Albom sarlavhalari uchun) va Inter (Matnlar uchun) -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Caveat:wght@600;700&family=Inter:wght@300;400;500;600;700&family=Lora:ital,wght@0,500;0,600;0,700;1,400&display=swap" rel="stylesheet">
    <!-- Font Awesome ikonkalar -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css">
    <!-- Tone.js sahifa varoqlash va yengil kuy ovozlari uchun -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/tone/14.8.49/Tone.js"></script>

    <style>
        :root {
            --bg-parchment: #FAF6F0;
            --paper-light: #FFFDF9;
            --paper-shadow: #E8DFD1;
            --wood-dark: #4A3222;
            --bronze-primary: #8B5E3C;
            --gold-accent: #C89D66;
            --ink-dark: #2C221E;
            --ink-muted: #6E5D53;
        }

        body {
            font-family: 'Inter', sans-serif;
            background-color: var(--bg-parchment);
            background-image: 
                radial-gradient(circle at 20% 20%, rgba(200, 157, 102, 0.08) 0%, transparent 50%),
                radial-gradient(circle at 80% 80%, rgba(139, 94, 60, 0.08) 0%, transparent 50%);
            color: var(--ink-dark);
            overflow-x: hidden;
        }

        .font-serif-album {
            font-family: 'Lora', serif;
        }

        .font-handwriting {
            font-family: 'Caveat', cursive;
        }

        /* 3D Albom Sahna va Varoqlash Animatsiyasi */
        .album-stage {
            perspective: 2200px;
        }

        .album-book {
            position: relative;
            background: linear-gradient(135deg, #5C3D28 0%, #3E2718 100%);
            border-radius: 20px;
            padding: 12px;
            box-shadow: 
                0 25px 50px -12px rgba(44, 34, 30, 0.35),
                0 0 0 1px rgba(200, 157, 102, 0.3),
                inset 0 2px 4px rgba(255, 255, 255, 0.15);
            transition: transform 0.4s ease;
        }

        @media (min-width: 768px) {
            .album-book {
                padding: 18px;
                border-radius: 24px;
            }
        }

        .album-paper {
            background-color: var(--paper-light);
            background-image: linear-gradient(to right, rgba(0,0,0,0.03) 0%, rgba(255,255,255,0) 6%, rgba(255,255,255,0) 94%, rgba(0,0,0,0.03) 100%);
            border-radius: 14px;
            position: relative;
            transform-style: preserve-3d;
            box-shadow: 
                inset 0 0 30px rgba(232, 223, 209, 0.6),
                0 4px 15px rgba(0,0,0,0.08);
            transition: transform 0.65s cubic-bezier(0.645, 0.045, 0.355, 1), opacity 0.4s ease;
        }

        /* Albom o'rtasidagi bukilish chizig'i (katta ekranlarda) */
        @media (min-width: 1024px) {
            .album-spine::after {
                content: '';
                position: absolute;
                top: 0;
                bottom: 0;
                left: 50%;
                width: 36px;
                transform: translateX(-50%);
                background: linear-gradient(to right, 
                    rgba(0,0,0,0) 0%, 
                    rgba(74, 50, 34, 0.08) 35%, 
                    rgba(74, 50, 34, 0.18) 50%, 
                    rgba(74, 50, 34, 0.08) 65%, 
                    rgba(0,0,0,0) 100%);
                pointer-events: none;
                z-index: 10;
            }
        }

        /* Sahifa varoqlash animatsiya klasslari */
        .flip-next-out {
            animation: pageFlipNextOut 0.45s cubic-bezier(0.4, 0, 0.2, 1) forwards;
            transform-origin: left center;
        }

        .flip-next-in {
            animation: pageFlipNextIn 0.45s cubic-bezier(0.4, 0, 0.2, 1) forwards;
            transform-origin: left center;
        }

        .flip-prev-out {
            animation: pageFlipPrevOut 0.45s cubic-bezier(0.4, 0, 0.2, 1) forwards;
            transform-origin: right center;
        }

        .flip-prev-in {
            animation: pageFlipPrevIn 0.45s cubic-bezier(0.4, 0, 0.2, 1) forwards;
            transform-origin: right center;
        }

        @keyframes pageFlipNextOut {
            0% { transform: rotateY(0deg) scale(1); opacity: 1; }
            100% { transform: rotateY(-35deg) scale(0.96); opacity: 0; }
        }

        @keyframes pageFlipNextIn {
            0% { transform: rotateY(35deg) scale(0.96); opacity: 0; }
            100% { transform: rotateY(0deg) scale(1); opacity: 1; }
        }

        @keyframes pageFlipPrevOut {
            0% { transform: rotateY(0deg) scale(1); opacity: 1; }
            100% { transform: rotateY(35deg) scale(0.96); opacity: 0; }
        }

        @keyframes pageFlipPrevIn {
            0% { transform: rotateY(-35deg) scale(0.96); opacity: 0; }
            100% { transform: rotateY(0deg) scale(1); opacity: 1; }
        }

        /* Polaroid / Klassik Albom Rasm Ramkasi va Burchak Yopishtirgichlar */
        .photo-frame {
            position: relative;
            background: #FFFFFF;
            padding: 12px 12px 18px 12px;
            border-radius: 6px;
            box-shadow: 
                0 10px 25px -5px rgba(74, 50, 34, 0.16),
                0 2px 6px rgba(0, 0, 0, 0.06),
                0 0 0 1px rgba(200, 157, 102, 0.25);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }

        .photo-frame:hover {
            transform: translateY(-3px) rotate(0.4deg);
            box-shadow: 
                0 18px 32px -8px rgba(74, 50, 34, 0.22),
                0 0 0 1px rgba(200, 157, 102, 0.45);
        }

        /* Albom burchaklari (Photo Corners) */
        .photo-corner {
            position: absolute;
            width: 24px;
            height: 24px;
            z-index: 5;
            pointer-events: none;
        }
        .corner-tl {
            top: 6px; left: 6px;
            border-top: 4px solid var(--gold-accent);
            border-left: 4px solid var(--gold-accent);
            border-top-left-radius: 4px;
        }
        .corner-tr {
            top: 6px; right: 6px;
            border-top: 4px solid var(--gold-accent);
            border-right: 4px solid var(--gold-accent);
            border-top-right-radius: 4px;
        }
        .corner-bl {
            bottom: 12px; left: 6px;
            border-bottom: 4px solid var(--gold-accent);
            border-left: 4px solid var(--gold-accent);
            border-bottom-left-radius: 4px;
        }
        .corner-br {
            bottom: 12px; right: 6px;
            border-bottom: 4px solid var(--gold-accent);
            border-right: 4px solid var(--gold-accent);
            border-bottom-right-radius: 4px;
        }

        /* Maxsus Scrollbar */
        ::-webkit-scrollbar {
            width: 6px;
            height: 6px;
        }
        ::-webkit-scrollbar-track {
            background: #F2EBE1;
        }
        ::-webkit-scrollbar-thumb {
            background: #C89D66;
            border-radius: 999px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #8B5E3C;
        }

        /* Yurakcha urish animatsiyasi */
        @keyframes heartPop {
            0% { transform: scale(1); }
            40% { transform: scale(1.35); }
            70% { transform: scale(0.9); }
            100% { transform: scale(1); }
        }
        .heart-pop {
            animation: heartPop 0.4s ease;
        }
    </style>
</head>
<body class="min-h-screen flex flex-col selection:bg-[#C89D66] selection:text-white">

    <!-- Bildirishnoma (Toast) oynasi -->
    <div id="toast-container" class="fixed top-4 right-4 z-50 flex flex-col gap-2 max-w-sm w-full pointer-events-none px-4 sm:px-0"></div>

    <!-- Yuqori Sarlavha (Header) -->
    <header class="sticky top-0 z-30 bg-[#FAF6F0]/90 backdrop-blur-md border-b border-[#E5D8C5] shadow-sm">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-3">
            <div class="flex flex-wrap items-center justify-between gap-3">
                <!-- Brend va Oila Nomi -->
                <div class="flex items-center gap-3">
                    <div class="w-11 h-11 rounded-2xl bg-gradient-to-br from-[#8B5E3C] to-[#5C3D28] text-[#FAF6F0] flex items-center justify-center shadow-md border border-[#C89D66]/40">
                        <i class="fa-solid fa-book-open text-lg"></i>
                    </div>
                    <div>
                        <div class="flex items-center gap-2">
                            <h1 class="font-serif-album text-lg sm:text-xl font-bold text-[#3E2718] tracking-tight">
                                Qadrdon Xotiralar
                            </h1>
                            <span id="live-indicator" class="inline-flex items-center gap-1 px-2 py-0.5 rounded-full text-[11px] font-medium bg-emerald-100 text-emerald-800 border border-emerald-200">
                                <span class="w-1.5 h-1.5 rounded-full bg-emerald-500 animate-pulse"></span>
                                Jonli albom
                            </span>
                        </div>
                        <p class="text-xs text-[#6E5D53] truncate max-w-[220px] sm:max-w-md">
                            Oila va qarindoshlar uchun umumiy xotira sandig'i
                        </p>
                    </div>
                </div>

                <!-- O'ng tarafdagi tezkor tugmalar -->
                <div class="flex items-center gap-2 sm:gap-3">
                    <!-- Foydalanuvchi (Qarindosh) Profili tugmasi -->
                    <button onclick="openProfileModal()" id="user-badge-btn" class="flex items-center gap-2 px-3 py-2 rounded-xl bg-[#FFFDF9] hover:bg-[#F4ECE1] text-[#4A3222] border border-[#DFD1BE] text-xs sm:text-sm font-medium transition shadow-sm">
                        <i class="fa-solid fa-user-pen text-[#8B5E3C]"></i>
                        <span id="current-user-label" class="max-w-[110px] sm:max-w-[160px] truncate">Ism kiritish</span>
                    </button>

                    <!-- Guruhga ulashish tugmasi -->
                    <button onclick="shareToGroup()" class="flex items-center gap-2 px-3.5 py-2 rounded-xl bg-[#EFE6D8] hover:bg-[#E5D7C3] text-[#4A3222] border border-[#D4C1A7] text-xs sm:text-sm font-semibold transition shadow-sm" title="Telegram va qarindoshlar guruhiga ulashish">
                        <i class="fa-solid fa-share-nodes text-[#8B5E3C]"></i>
                        <span class="hidden sm:inline">Guruhga ulashish</span>
                    </button>

                    <!-- Yangi rasm qo'shish tugmasi -->
                    <button onclick="openUploadModal()" class="flex items-center gap-2 px-4 py-2 rounded-xl bg-gradient-to-r from-[#8B5E3C] to-[#6F482B] hover:from-[#7A5132] hover:to-[#5C3B22] text-white text-xs sm:text-sm font-semibold transition shadow-md active:scale-95">
                        <i class="fa-solid fa-camera-retro"></i>
                        <span>Rasm qo'shish</span>
                    </button>
                </div>
            </div>
        </div>
    </header>

    <!-- Asosiy Kontent -->
    <main class="flex-1 max-w-7xl w-full mx-auto px-4 sm:px-6 lg:px-8 py-5 sm:py-7 flex flex-col gap-5">

        <!-- Filtrlar, Qidiruv va Slayd-shou Paneli -->
        <section class="bg-[#FFFDF9] rounded-2xl p-3.5 sm:p-4 border border-[#E5D8C5] shadow-sm flex flex-col lg:flex-row items-stretch lg:items-center justify-between gap-3">
            <!-- Kategoriyalar (Albom bo'limlari) -->
            <div class="flex items-center gap-1.5 overflow-x-auto pb-1 lg:pb-0 no-scrollbar" id="category-filters">
                <button data-cat="Barchasi" class="cat-btn active px-3.5 py-1.5 rounded-xl text-xs sm:text-sm font-semibold bg-[#8B5E3C] text-white shadow-sm whitespace-nowrap transition">
                    <i class="fa-solid fa-images mr-1"></i> Barchasi (<span id="total-count">0</span>)
                </button>
                <button data-cat="Oila davrasida" class="cat-btn px-3.5 py-1.5 rounded-xl text-xs sm:text-sm font-medium bg-[#F5EFE6] text-[#5C493E] hover:bg-[#EAE0D1] whitespace-nowrap transition">
                    🏡 Oila davrasida
                </button>
                <button data-cat="To'ylar va Marosimlar" class="cat-btn px-3.5 py-1.5 rounded-xl text-xs sm:text-sm font-medium bg-[#F5EFE6] text-[#5C493E] hover:bg-[#EAE0D1] whitespace-nowrap transition">
                    💍 To'ylar
                </button>
                <button data-cat="Bayramlar" class="cat-btn px-3.5 py-1.5 rounded-xl text-xs sm:text-sm font-medium bg-[#F5EFE6] text-[#5C493E] hover:bg-[#EAE0D1] whitespace-nowrap transition">
                    🎉 Bayramlar
                </button>
                <button data-cat="Bolalik xotiralari" class="cat-btn px-3.5 py-1.5 rounded-xl text-xs sm:text-sm font-medium bg-[#F5EFE6] text-[#5C493E] hover:bg-[#EAE0D1] whitespace-nowrap transition">
                    🧸 Bolalik
                </button>
                <button data-cat="Sayohatlar" class="cat-btn px-3.5 py-1.5 rounded-xl text-xs sm:text-sm font-medium bg-[#F5EFE6] text-[#5C493E] hover:bg-[#EAE0D1] whitespace-nowrap transition">
                    ✈️ Sayohatlar
                </button>
            </div>

            <!-- Qidiruv va Slayd-shou tugmalari -->
            <div class="flex items-center gap-2">
                <div class="relative flex-1 sm:w-56">
                    <i class="fa-solid fa-magnifying-glass absolute left-3 top-1/2 -translate-y-1/2 text-[#8E7B6E] text-xs"></i>
                    <input type="text" id="search-input" placeholder="Izoh yoki ism bo'yicha..." class="w-full pl-8 pr-3 py-1.5 rounded-xl bg-[#FAF6F0] border border-[#DFD1BE] text-xs sm:text-sm text-[#2C221E] placeholder-[#9A897D] focus:outline-none focus:border-[#8B5E3C]">
                </div>

                <!-- Slayd-shou tugmasi -->
                <button id="slideshow-btn" onclick="toggleSlideshow()" class="flex items-center gap-1.5 px-3.5 py-1.5 rounded-xl bg-[#FAF6F0] hover:bg-[#EFE6D8] text-[#8B5E3C] border border-[#C89D66]/60 text-xs sm:text-sm font-semibold whitespace-nowrap transition" title="Avtomatik xotiralar sayohati">
                    <i class="fa-solid fa-play" id="slideshow-icon"></i>
                    <span id="slideshow-text">Slayd-shou</span>
                </button>

                <!-- Ko'rinish rejimi (Albom / To'r) -->
                <button id="view-toggle-btn" onclick="toggleViewMode()" class="p-2 rounded-xl bg-[#FAF6F0] hover:bg-[#EFE6D8] text-[#6E5D53] border border-[#DFD1BE] text-xs sm:text-sm transition" title="Barcha rasmlarni ro'yxatda ko'rish">
                    <i class="fa-solid fa-table-cells-large" id="view-toggle-icon"></i>
                </button>
            </div>
        </section>

        <!-- ASOSIY 3D ALBOM SAHNASI -->
        <section id="album-view-section" class="album-stage flex-1 flex flex-col justify-center">
            <!-- Yuklanish indikatori -->
            <div id="loading-state" class="bg-[#FFFDF9] rounded-3xl p-12 border border-[#E5D8C5] text-center shadow-sm">
                <div class="inline-block w-10 h-10 border-4 border-[#C89D66] border-t-[#5C3D28] rounded-full animate-spin mb-3"></div>
                <p class="font-serif-album text-lg text-[#4A3222]">Oilaviy xotiralar albomi ochilmoqda...</p>
            </div>

            <!-- Albom Muqovasi / Ichki Sahifalar -->
            <div id="album-container" class="hidden">
                <div class="album-book">
                    <!-- Albom Ichki Qog'oz Sahifasi -->
                    <div id="album-page" class="album-paper album-spine min-h-[540px] sm:min-h-[580px] p-4 sm:p-7 lg:p-9 flex flex-col justify-between">
                        
                        <!-- Sahifa Yuqori Kolontitul (Header) -->
                        <div class="flex items-center justify-between border-b border-[#E8DFD1] pb-3 mb-4 text-xs text-[#8E7B6E]">
                            <div class="flex items-center gap-2">
                                <i class="fa-solid fa-feather-pointed text-[#C89D66]"></i>
                                <span class="font-serif-album italic font-medium text-[#5C493E]">Abduxalimovlar va Qadrdonlar Albomi</span>
                            </div>
                            <div class="flex items-center gap-3">
                                <span id="page-category-badge" class="px-2.5 py-0.5 rounded-full bg-[#F4ECE1] text-[#8B5E3C] font-medium">
                                    Xotira sahifasi
                                </span>
                                <span class="font-serif-album font-semibold text-[#4A3222]" id="page-indicator">
                                    1 / 1 - sahifa
                                </span>
                            </div>
                        </div>

                        <!-- Sahifa Markaziy Qismi: 2 ustunli (Chap: Rasm, O'ng: Xotira va Qarindoshlar izohlari) -->
                        <div id="page-content" class="grid grid-cols-1 lg:grid-cols-12 gap-6 lg:gap-10 items-center flex-1 my-auto">
                            
                            <!-- CHAP SAHIFA: Rasm va Ramka -->
                            <div class="lg:col-span-6 flex flex-col items-center justify-center">
                                <div class="photo-frame w-full max-w-md mx-auto">
                                    <!-- Albom burchaklari -->
                                    <div class="photo-corner corner-tl"></div>
                                    <div class="photo-corner corner-tr"></div>
                                    <div class="photo-corner corner-bl"></div>
                                    <div class="photo-corner corner-br"></div>

                                    <!-- Rasm konteyneri -->
                                    <div class="relative overflow-hidden rounded bg-[#F5EFE6] aspect-[4/3] group cursor-zoom-in" onclick="openLightbox()">
                                        <img id="memory-image" src="" alt="Oilaviy xotira" class="w-full h-full object-cover transition duration-500 group-hover:scale-105">
                                        
                                        <!-- Kattalashtirish va Yuklab olish tugmalari -->
                                        <div class="absolute bottom-2.5 right-2.5 flex items-center gap-1.5 opacity-90 sm:opacity-0 group-hover:opacity-100 transition">
                                            <button onclick="event.stopPropagation(); downloadCurrentPhoto()" class="w-9 h-9 rounded-full bg-black/65 hover:bg-black/85 text-white flex items-center justify-center backdrop-blur-sm transition" title="Rasmni yuklab olish">
                                                <i class="fa-solid fa-download text-xs"></i>
                                            </button>
                                            <button onclick="event.stopPropagation(); openLightbox()" class="w-9 h-9 rounded-full bg-black/65 hover:bg-black/85 text-white flex items-center justify-center backdrop-blur-sm transition" title="To'liq ekranda ko'rish">
                                                <i class="fa-solid fa-expand text-xs"></i>
                                            </button>
                                        </div>
                                    </div>

                                    <!-- Rasm ostidagi qo'lyozma uslubidagi sana va joy -->
                                    <div class="mt-3 px-1 flex items-center justify-between text-[#5C493E]">
                                        <span id="memory-date" class="font-handwriting text-xl sm:text-2xl text-[#6F482B]">
                                            12-May, 2024
                                        </span>
                                        <span id="memory-author-badge" class="inline-flex items-center gap-1.5 text-xs font-medium bg-[#FAF6F0] px-2.5 py-1 rounded-lg border border-[#E5D8C5]">
                                            <i class="fa-solid fa-user-check text-[#8B5E3C]"></i>
                                            <span id="memory-author">Otabek</span>
                                        </span>
                                    </div>
                                </div>
                            </div>

                            <!-- O'NG SAHIFA: Xotira Izohi, Yurakchalar va Qarindoshlar Fikrlari -->
                            <div class="lg:col-span-6 flex flex-col justify-between h-full bg-[#FAF6F0]/70 rounded-2xl p-4 sm:p-6 border border-[#EAE0D1]">
                                <div>
                                    <!-- Voqea sarlavhasi -->
                                    <div class="flex items-start justify-between gap-2 mb-2">
                                        <h2 id="memory-title" class="font-serif-album text-xl sm:text-2xl font-bold text-[#3E2718] leading-snug">
                                            Xotira sarlavhasi
                                        </h2>
                                        <button id="delete-photo-btn" onclick="deleteCurrentMemory()" class="hidden text-xs text-red-500 hover:text-red-700 p-1.5 rounded-lg hover:bg-red-50 transition" title="O'chirish">
                                            <i class="fa-solid fa-trash-can"></i>
                                        </button>
                                    </div>

                                    <!-- Asosiy Xotira Matni (Izoh) -->
                                    <div class="relative bg-white/80 rounded-xl p-4 border-l-4 border-[#C89D66] shadow-sm mb-4">
                                        <i class="fa-solid fa-quote-left text-[#C89D66]/40 text-xl absolute top-2 right-3"></i>
                                        <p id="memory-caption" class="text-sm sm:text-base text-[#3A2E28] leading-relaxed whitespace-pre-line">
                                            Bu yerda rasm ostiga yozilgan samimiy xotira matni turadi...
                                        </p>
                                    </div>

                                    <!-- Reaksiya (Yurakcha) va Tezkor harakatlar -->
                                    <div class="flex items-center justify-between pb-3 mb-3 border-b border-[#E5D8C5]">
                                        <button id="like-btn" onclick="toggleLikeCurrent()" class="flex items-center gap-2 px-3.5 py-1.5 rounded-xl bg-white hover:bg-rose-50 text-rose-600 border border-rose-200 shadow-sm transition active:scale-95">
                                            <i id="like-icon" class="fa-regular fa-heart text-base"></i>
                                            <span class="text-xs sm:text-sm font-semibold"><span id="like-count">0</span> ta mehr</span>
                                        </button>

                                        <span class="text-xs text-[#8E7B6E]">
                                            <i class="fa-regular fa-comments mr-1"></i>
                                            <span id="comments-count">0</span> ta qarindosh izohi
                                        </span>
                                    </div>

                                    <!-- Qarindoshlar yozgan izohlar ro'yxati -->
                                    <div class="mb-3">
                                        <h3 class="text-xs font-semibold uppercase tracking-wider text-[#8E7B6E] mb-2">
                                            Qarindoshlarning iliq fikrlari:
                                        </h3>
                                        <div id="comments-list" class="max-h-36 overflow-y-auto space-y-2 pr-1">
                                            <!-- Izohlar JS orqali yuklanadi -->
                                        </div>
                                    </div>
                                </div>

                                <!-- Yangi izoh yozish formasi -->
                                <form id="comment-form" onsubmit="submitComment(event)" class="mt-2 flex items-center gap-2">
                                    <input type="text" id="comment-input" required placeholder="Bu rasm haqida xotira yoki izoh yozing..." class="flex-1 px-3.5 py-2 rounded-xl bg-white border border-[#D8C8B4] text-xs sm:text-sm text-[#2C221E] placeholder-[#9A897D] focus:outline-none focus:border-[#8B5E3C]">
                                    <button type="submit" class="px-4 py-2 rounded-xl bg-[#8B5E3C] hover:bg-[#6F482B] text-white text-xs sm:text-sm font-semibold shadow-sm transition active:scale-95">
                                        <i class="fa-solid fa-paper-plane"></i>
                                    </button>
                                </form>
                            </div>
                        </div>

                        <!-- Sahifa Pastki Boshqaruv Paneli (Varoqlash tugmalari) -->
                        <div class="mt-5 pt-3 border-t border-[#E8DFD1] flex items-center justify-between gap-2">
                            <button id="prev-page-btn" onclick="prevPage()" class="flex items-center gap-2 px-4 py-2.5 rounded-xl bg-[#F4ECE1] hover:bg-[#E7DAC7] disabled:opacity-40 disabled:pointer-events-none text-[#4A3222] text-xs sm:text-sm font-semibold transition shadow-sm">
                                <i class="fa-solid fa-chevron-left"></i>
                                <span>Oldingi sahifa</span>
                            </button>

                            <!-- Sahifa nuqtalari / Tezkor o'tish -->
                            <div id="page-dots" class="hidden sm:flex items-center gap-1.5 max-w-xs overflow-x-auto py-1">
                                <!-- Nuqtalar JS orqali yaratiladi -->
                            </div>

                            <button id="next-page-btn" onclick="nextPage()" class="flex items-center gap-2 px-4 py-2.5 rounded-xl bg-[#8B5E3C] hover:bg-[#6F482B] disabled:opacity-40 disabled:pointer-events-none text-white text-xs sm:text-sm font-semibold transition shadow-sm">
                                <span>Keyingi sahifa</span>
                                <i class="fa-solid fa-chevron-right"></i>
                            </button>
                        </div>

                    </div>
                </div>
            </div>

            <!-- Bo'sh holat (Agar qidiruvda hech narsa topilmasa) -->
            <div id="empty-state" class="hidden bg-[#FFFDF9] rounded-3xl p-10 border border-[#E5D8C5] text-center shadow-sm">
                <div class="w-16 h-16 rounded-full bg-[#F4ECE1] text-[#8B5E3C] flex items-center justify-center mx-auto mb-3 text-2xl">
                    <i class="fa-regular fa-images"></i>
                </div>
                <h3 class="font-serif-album text-xl font-bold text-[#3E2718] mb-1">Bu bo'limda hali rasmlar yo'q</h3>
                <p class="text-sm text-[#6E5D53] mb-4">Birinchi bo'lib oilaviy xotira rasmini yuklang va qarindoshlar bilan bo'lishing!</p>
                <button onclick="openUploadModal()" class="px-5 py-2.5 rounded-xl bg-[#8B5E3C] text-white text-sm font-semibold shadow-md hover:bg-[#6F482B] transition">
                    <i class="fa-solid fa-plus mr-1.5"></i> Yangi rasm qo'shish
                </button>
            </div>
        </section>

        <!-- BARCHA RASMLAR TO'R KO'RINISHI (Grid View - ixtiyoriy) -->
        <section id="grid-view-section" class="hidden">
            <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-5" id="memories-grid">
                <!-- Kartochkalar JS orqali yaratiladi -->
            </div>
        </section>

    </main>

    <!-- Pastki Qism (Footer) -->
    <footer class="mt-auto py-4 px-4 border-t border-[#E5D8C5] bg-[#FAF6F0] text-center text-xs text-[#8E7B6E]">
        <p>✨ Oilaviy rishtalar abadiy bo'lsin! Har bir surat — bir umrlik shirin xotira.</p>
    </footer>

    <!-- ===================================================================== -->
    <!-- MODAL 1: YANGI RASM QO'SHISH OYNASI                                   -->
    <!-- ===================================================================== -->
    <div id="upload-modal" class="fixed inset-0 z-50 hidden bg-black/60 backdrop-blur-sm flex items-center justify-center p-4 overflow-y-auto">
        <div class="bg-[#FFFDF9] rounded-3xl max-w-lg w-full border border-[#DFD1BE] shadow-2xl overflow-hidden my-auto">
            <!-- Modal Sarlavha -->
            <div class="bg-gradient-to-r from-[#5C3D28] to-[#8B5E3C] px-6 py-4 text-white flex items-center justify-between">
                <div class="flex items-center gap-2.5">
                    <i class="fa-solid fa-camera-retro text-lg text-[#F3D5A5]"></i>
                    <h3 class="font-serif-album text-lg font-bold">Albomga yangi xotira qo'shish</h3>
                </div>
                <button onclick="closeUploadModal()" class="w-8 h-8 rounded-full bg-white/15 hover:bg-white/25 flex items-center justify-center transition">
                    <i class="fa-solid fa-xmark"></i>
                </button>
            </div>

            <!-- Modal Forma -->
            <form id="upload-form" onsubmit="handlePhotoUpload(event)" class="p-5 sm:p-6 space-y-4">
                <!-- Kim yuklamoqda? -->
                <div class="grid grid-cols-1 sm:grid-cols-2 gap-3">
                    <div>
                        <label class="block text-xs font-semibold text-[#5C493E] mb-1">Ismingiz *</label>
                        <input type="text" id="upload-name" required placeholder="Masalan: Otabek" class="w-full px-3.5 py-2 rounded-xl bg-[#FAF6F0] border border-[#D8C8B4] text-sm focus:outline-none focus:border-[#8B5E3C]">
                    </div>
                    <div>
                        <label class="block text-xs font-semibold text-[#5C493E] mb-1">Qarindoshlik darajangiz *</label>
                        <select id="upload-relation" class="w-full px-3.5 py-2 rounded-xl bg-[#FAF6F0] border border-[#D8C8B4] text-sm focus:outline-none focus:border-[#8B5E3C]">
                            <option value="Oila a'zosi">Oila a'zosi</option>
                            <option value="Ota / Ona">Ota / Ona</option>
                            <option value="Buvi / Bobo">Buvi / Bobo</option>
                            <option value="Aka / Uka">Aka / Uka</option>
                            <option value="Opa / Singil">Opa / Singil</option>
                            <option value="Tog'a / Amaki">Tog'a / Amaki</option>
                            <option value="Xola / Amma">Xola / Amma</option>
                            <option value="Jiyan / Qarindosh">Jiyan / Qarindosh</option>
                        </select>
                    </div>
                </div>

                <!-- Rasm tanlash maydoni -->
                <div>
                    <label class="block text-xs font-semibold text-[#5C493E] mb-1">Rasmni tanlang (Galereya yoki Kamera) *</label>
                    <label for="photo-file-input" id="drop-zone" class="flex flex-col items-center justify-center border-2 border-dashed border-[#C89D66] rounded-2xl p-4 bg-[#FAF6F0] hover:bg-[#F3ECE1] cursor-pointer transition text-center">
                        <div id="preview-wrapper" class="hidden w-full mb-2">
                            <img id="upload-preview-img" src="" alt="Tanlangan rasm" class="max-h-48 mx-auto rounded-xl shadow-sm object-contain">
                        </div>
                        <div id="upload-placeholder">
                            <i class="fa-solid fa-cloud-arrow-up text-2xl text-[#8B5E3C] mb-1.5"></i>
                            <p class="text-xs sm:text-sm font-medium text-[#4A3222]">Rasm tanlash uchun bosing</p>
                            <p class="text-[11px] text-[#8E7B6E] mt-0.5">JPG, PNG formatlar qo'llab-quvvatlanadi</p>
                        </div>
                        <input type="file" id="photo-file-input" accept="image/*" required class="hidden" onchange="previewSelectedFile(event)">
                    </label>
                </div>

                <!-- Sarlavha va Bo'lim -->
                <div class="grid grid-cols-1 sm:grid-cols-2 gap-3">
                    <div>
                        <label class="block text-xs font-semibold text-[#5C493E] mb-1">Xotira nomi (Sarlavha) *</label>
                        <input type="text" id="upload-title" required placeholder="Masalan: Navro'z dasturxoni" class="w-full px-3.5 py-2 rounded-xl bg-[#FAF6F0] border border-[#D8C8B4] text-sm focus:outline-none focus:border-[#8B5E3C]">
                    </div>
                    <div>
                        <label class="block text-xs font-semibold text-[#5C493E] mb-1">Albom bo'limi</label>
                        <select id="upload-category" class="w-full px-3.5 py-2 rounded-xl bg-[#FAF6F0] border border-[#D8C8B4] text-sm focus:outline-none focus:border-[#8B5E3C]">
                            <option value="Oila davrasida">🏡 Oila davrasida</option>
                            <option value="To'ylar va Marosimlar">💍 To'ylar va Marosimlar</option>
                            <option value="Bayramlar">🎉 Bayramlar</option>
                            <option value="Bolalik xotiralari">🧸 Bolalik xotiralari</option>
                            <option value="Sayohatlar">✈️ Sayohatlar</option>
                        </select>
                    </div>
                </div>

                <!-- Sana -->
                <div>
                    <label class="block text-xs font-semibold text-[#5C493E] mb-1">Voqea sanasi (taxminiy yil yoki kun)</label>
                    <input type="text" id="upload-date" placeholder="Masalan: 21-Mart, 2025 yoki 2018-yil yozi" class="w-full px-3.5 py-2 rounded-xl bg-[#FAF6F0] border border-[#D8C8B4] text-sm focus:outline-none focus:border-[#8B5E3C]">
                </div>

                <!-- Rasm tagiga yoziladigan izoh -->
                <div>
                    <label class="block text-xs font-semibold text-[#5C493E] mb-1">Rasm ostiga xotira izohi *</label>
                    <textarea id="upload-caption" rows="3" required placeholder="Bu rasm qachon va qayerda olingan? Kimlar bor? Shu kun haqida shirin xotirangizni yozing..." class="w-full px-3.5 py-2 rounded-xl bg-[#FAF6F0] border border-[#D8C8B4] text-sm focus:outline-none focus:border-[#8B5E3C]"></textarea>
                </div>

                <!-- Saqlash tugmasi -->
                <div class="pt-2 flex items-center justify-end gap-2">
                    <button type="button" onclick="closeUploadModal()" class="px-4 py-2.5 rounded-xl bg-[#F2EBE1] text-[#5C493E] text-sm font-medium hover:bg-[#E5DACB] transition">
                        Bekor qilish
                    </button>
                    <button type="submit" id="submit-upload-btn" class="px-6 py-2.5 rounded-xl bg-gradient-to-r from-[#8B5E3C] to-[#6F482B] text-white text-sm font-semibold shadow-md hover:opacity-95 transition flex items-center gap-2">
                        <i class="fa-solid fa-check"></i>
                        <span>Albomga joylash</span>
                    </button>
                </div>
            </form>
        </div>
    </div>

    <!-- ===================================================================== -->
    <!-- MODAL 2: QARINDOSH ISMINI KIRITISH OYNASI                             -->
    <!-- ===================================================================== -->
    <div id="profile-modal" class="fixed inset-0 z-50 hidden bg-black/60 backdrop-blur-sm flex items-center justify-center p-4">
        <div class="bg-[#FFFDF9] rounded-3xl max-w-md w-full border border-[#DFD1BE] shadow-2xl overflow-hidden">
            <div class="bg-[#5C3D28] px-6 py-4 text-white flex items-center justify-between">
                <h3 class="font-serif-album text-lg font-bold">Xush kelibsiz, Qadrdonim!</h3>
                <button onclick="closeProfileModal()" class="w-8 h-8 rounded-full bg-white/15 hover:bg-white/25 flex items-center justify-center">
                    <i class="fa-solid fa-xmark"></i>
                </button>
            </div>
            <form onsubmit="saveUserProfile(event)" class="p-6 space-y-4">
                <p class="text-xs sm:text-sm text-[#6E5D53]">
                    Qarindoshlar siz qo'shgan rasmlar va izohlarni tanishlari uchun ismingizni kiriting:
                </p>
                <div>
                    <label class="block text-xs font-semibold text-[#5C493E] mb-1">Ismingiz *</label>
                    <input type="text" id="profile-name-input" required placeholder="Masalan: Otabek" class="w-full px-3.5 py-2.5 rounded-xl bg-[#FAF6F0] border border-[#D8C8B4] text-sm focus:outline-none focus:border-[#8B5E3C]">
                </div>
                <div>
                    <label class="block text-xs font-semibold text-[#5C493E] mb-1">Qarindoshlik maqomingiz</label>
                    <select id="profile-relation-input" class="w-full px-3.5 py-2.5 rounded-xl bg-[#FAF6F0] border border-[#D8C8B4] text-sm focus:outline-none focus:border-[#8B5E3C]">
                        <option value="Oila a'zosi">Oila a'zosi</option>
                        <option value="Ota / Ona">Ota / Ona</option>
                        <option value="Buvi / Bobo">Buvi / Bobo</option>
                        <option value="Aka / Uka">Aka / Uka</option>
                        <option value="Opa / Singil">Opa / Singil</option>
                        <option value="Tog'a / Amaki">Tog'a / Amaki</option>
                        <option value="Xola / Amma">Xola / Amma</option>
                        <option value="Jiyan / Qarindosh">Jiyan / Qarindosh</option>
                    </select>
                </div>
                <button type="submit" class="w-full py-2.5 rounded-xl bg-[#8B5E3C] hover:bg-[#6F482B] text-white text-sm font-semibold shadow-md transition">
                    Saqlash va Albomni ochish
                </button>
            </form>
        </div>
    </div>

    <!-- ===================================================================== -->
    <!-- MODAL 3: TO'LIQ EKRANDA RASMNI KO'RISH (LIGHTBOX)                     -->
    <!-- ===================================================================== -->
    <div id="lightbox-modal" class="fixed inset-0 z-50 hidden bg-black/90 backdrop-blur-md flex flex-col items-center justify-center p-4" onclick="closeLightbox()">
        <button onclick="closeLightbox()" class="absolute top-4 right-4 w-10 h-10 rounded-full bg-white/15 hover:bg-white/25 text-white flex items-center justify-center text-lg">
            <i class="fa-solid fa-xmark"></i>
        </button>
        <img id="lightbox-img" src="" alt="Kattalashtirilgan rasm" class="max-h-[82vh] max-w-[94vw] rounded-xl shadow-2xl object-contain" onclick="event.stopPropagation()">
        <p id="lightbox-caption" class="mt-3 text-white/90 font-serif-album text-sm sm:text-base text-center max-w-2xl px-4"></p>
    </div>

    <!-- ===================================================================== -->
    <!-- FIREBASE VA ILOVA MANTIQI (MODULAR SCRIPT)                            -->
    <!-- ===================================================================== -->
    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";
        import { getAuth, signInAnonymously, signInWithCustomToken, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js";
        import { getFirestore, collection, doc, addDoc, updateDoc, deleteDoc, onSnapshot, arrayUnion, arrayRemove } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";

        // Muhit o'zgaruvchilarini tekshirish
        const appId = typeof __app_id !== 'undefined' ? __app_id : 'family-memory-album-uz';
        let firebaseConfig = null;
        try {
            if (typeof __firebase_config !== 'undefined' && __firebase_config) {
                firebaseConfig = JSON.parse(__firebase_config);
            }
        } catch (e) {
            console.warn("Firebase config topilmadi, avtonom rejim ishlaydi.");
        }

        // Ilova holati (State)
        let db = null;
        let auth = null;
        let currentUser = null;
        let isCloudReady = false;

        let allMemories = [];
        let filteredMemories = [];
        let currentIndex = 0;
        let selectedCategory = "Barchasi";
        let searchQuery = "";
        let isGridView = false;
        let slideshowInterval = null;
        let compressedBase64 = null;

        // Foydalanuvchi (Qarindosh) ma'lumotlari (xotirada)
        let relativeProfile = {
            name: "Otabek",
            relation: "Albom asoschisi"
        };

        // Boshlang'ich namuna rasmlar (Albom birinchi ochilganda chiroyli ko'rinishi uchun)
        const demoMemories = [
            {
                id: "demo-1",
                isDemo: true,
                title: "Katta Oilaviy Dasturxon Atrofida",
                category: "Oila davrasida",
                date: "21-Mart, 2025 — Navro'z ayyomi",
                authorName: "Otabek",
                authorRelation: "Albom asoschisi",
                imageUrl: "https://images.unsplash.com/photo-1511895426328-dc8714191300?auto=format&fit=crop&w=1000&q=80",
                caption: "Barcha qarindoshlarimiz bir dasturxon atrofida jam bo'lgan eng fayzli kun! Buvi va bobomizning duolari, bolalarning quvnoq kulgusi — barchasi shu suratda muhrlangan. Siz ham o'zingizdagi rasmlarni yuqoridagi 'Rasm qo'shish' tugmasi orqali joylang!",
                likes: ["demo_u1", "demo_u2", "demo_u3"],
                comments: [
                    { author: "Xolam (Dilnoza)", text: "Qanday ajoyib kun bo'lgan edi! Sumalak ham juda shirin chiqqan.", time: "2 kun oldin" },
                    { author: "Tog'am (Rustam)", text: "Hammamizning boshimiz doim shunday to'y-tantanalarda birga bo'lsin!", time: "Kecha" }
                ],
                createdAt: 1711000000000
            },
            {
                id: "demo-2",
                isDemo: true,
                title: "Tog' bag'ridagi unutilmas sayohat",
                category: "Sayohatlar",
                date: "15-Avgust, 2024 — Chimyon",
                authorName: "Sardor",
                authorRelation: "Aka / Uka",
                imageUrl: "https://images.unsplash.com/photo-1506744038136-46273834b3fb?auto=format&fit=crop&w=1000&q=80",
                caption: "Yozning issiq kunlarida qarindoshlar bilan toza havo va salqin sharsharalar bag'riga chiqqan edik. Kechqurun gulxan atrofida aytilgan qo'shiqlar hali ham yodimizda.",
                likes: ["demo_u1", "demo_u4"],
                comments: [
                    { author: "Otabek", text: "Bu yil yozda yana barcha qarindoshlar bilan boramiz Xudo xohlasa!", time: "3 soat oldin" }
                ],
                createdAt: 1710000000000
            },
            {
                id: "demo-3",
                isDemo: true,
                title: "Beg'ubor bolalik va ilk qadamlar",
                category: "Bolalik xotiralari",
                date: "2012-yil bahori",
                authorName: "Malika",
                authorRelation: "Opa / Singil",
                imageUrl: "https://images.unsplash.com/photo-1472162072942-cd5147eb3902?auto=format&fit=crop&w=1000&q=80",
                caption: "Eski albomlarni titkilab shu suratni topib oldim. Qaranglar, hammamiz qanchalik kichkina va beg'ubor bo'lganmiz. Vaqt naqadar tez o'tadi-ya...",
                likes: ["demo_u1", "demo_u2", "demo_u3", "demo_u5"],
                comments: [
                    { author: "Buvim", text: "Ilohim umringiz uzoq, baxtingiz butun bo'lsin bolajonlarim!", time: "1 kun oldin" }
                ],
                createdAt: 1709000000000
            }
        ];

        // Sahifa varoqlash ovozi (Tone.js)
        function playPageFlipSound() {
            try {
                if (typeof Tone !== 'undefined' && Tone.context.state === 'running') {
                    const noise = new Tone.NoiseSynth({
                        noise: { type: 'pink' },
                        envelope: { attack: 0.02, decay: 0.14, sustain: 0, release: 0.05 }
                    }).toDestination();
                    noise.volume.value = -18;
                    noise.triggerAttackRelease("16n");
                }
            } catch (e) {
                // Ovoz bloklangan bo'lsa e'tibor bermaymiz
            }
        }

        // Toast xabarnoma ko'rsatish
        window.showToast = function(message, type = "info") {
            const container = document.getElementById("toast-container");
            const toast = document.createElement("div");
            const colors = {
                success: "bg-emerald-800 text-white border-emerald-600",
                error: "bg-rose-800 text-white border-rose-600",
                info: "bg-[#4A3222] text-[#FAF6F0] border-[#C89D66]"
            };
            const icons = {
                success: "fa-circle-check",
                error: "fa-circle-exclamation",
                info: "fa-heart"
            };

            toast.className = `pointer-events-auto flex items-center gap-3 px-4 py-3 rounded-2xl border shadow-xl text-xs sm:text-sm font-medium transition-all duration-300 transform translate-y-0 ${colors[type] || colors.info}`;
            toast.innerHTML = `
                <i class="fa-solid ${icons[type] || icons.info} text-base"></i>
                <span class="flex-1">${message}</span>
            `;
            container.appendChild(toast);

            setTimeout(() => {
                toast.style.opacity = "0";
                toast.style.transform = "translateY(-10px)";
                setTimeout(() => toast.remove(), 300);
            }, 3500);
        };

        // Firebase va Autentifikatsiyani ishga tushirish
        async function initApp() {
            updateUserLabel();

            if (!firebaseConfig) {
                // Avtonom demo rejim
                allMemories = [...demoMemories];
                applyFilters();
                document.getElementById("loading-state").classList.add("hidden");
                document.getElementById("album-container").classList.remove("hidden");
                return;
            }

            try {
                const app = initializeApp(firebaseConfig);
                auth = getAuth(app);
                db = getFirestore(app);

                // QOIDA 3: Avval autentifikatsiyani kutamiz
                if (typeof __initial_auth_token !== 'undefined' && __initial_auth_token) {
                    await signInWithCustomToken(auth, __initial_auth_token);
                } else {
                    await signInAnonymously(auth);
                }

                currentUser = auth.currentUser;
                isCloudReady = true;
                subscribeToMemories();
            } catch (error) {
                console.error("Ulanish xatosi:", error);
                allMemories = [...demoMemories];
                applyFilters();
                document.getElementById("loading-state").classList.add("hidden");
                document.getElementById("album-container").classList.remove("hidden");
            }
        }

        // Firestore'dan umumiy rasmlarni real vaqtda tinglash (QOIDA 1 va 2)
        function subscribeToMemories() {
            if (!currentUser || !db) return;

            const memoriesRef = collection(db, 'artifacts', appId, 'public', 'data', 'family_memories');

            onSnapshot(memoriesRef, (snapshot) => {
                const cloudItems = [];
                snapshot.forEach((docSnap) => {
                    cloudItems.push({ id: docSnap.id, ...docSnap.data() });
                });

                // Xotirada saralash (eng yangilari birinchi)
                cloudItems.sort((a, b) => (b.createdAt || 0) - (a.createdAt || 0));

                // Bulutdagi rasmlar + namuna rasmlar (agar bulutda 3 tadan kam bo'lsa namunalarni ham ko'rsatamiz)
                if (cloudItems.length > 0) {
                    allMemories = [...cloudItems, ...demoMemories];
                } else {
                    allMemories = [...demoMemories];
                }

                document.getElementById("loading-state").classList.add("hidden");
                applyFilters(false);
            }, (error) => {
                console.error("Ma'lumotlarni olishda xato:", error);
                allMemories = [...demoMemories];
                document.getElementById("loading-state").classList.add("hidden");
                applyFilters();
            });
        }

        // Filtrlash va Qidiruvni qo'llash
        function applyFilters(resetIndex = true) {
            filteredMemories = allMemories.filter((item) => {
                const matchesCat = selectedCategory === "Barchasi" || item.category === selectedCategory;
                const q = searchQuery.toLowerCase().trim();
                const matchesSearch = !q || 
                    (item.title && item.title.toLowerCase().includes(q)) ||
                    (item.caption && item.caption.toLowerCase().includes(q)) ||
                    (item.authorName && item.authorName.toLowerCase().includes(q));
                return matchesCat && matchesSearch;
            });

            document.getElementById("total-count").textContent = allMemories.length;

            if (resetIndex) {
                currentIndex = 0;
            } else if (currentIndex >= filteredMemories.length) {
                currentIndex = Math.max(0, filteredMemories.length - 1);
            }

            renderCurrentView();
        }

        // Joriy ko'rinishni chizish (Albom yoki Grid)
        function renderCurrentView() {
            const albumContainer = document.getElementById("album-container");
            const emptyState = document.getElementById("empty-state");
            const gridSection = document.getElementById("grid-view-section");

            if (filteredMemories.length === 0) {
                albumContainer.classList.add("hidden");
                gridSection.classList.add("hidden");
                emptyState.classList.remove("hidden");
                return;
            }

            emptyState.classList.add("hidden");

            if (isGridView) {
                albumContainer.classList.add("hidden");
                gridSection.classList.remove("hidden");
                renderGridView();
            } else {
                gridSection.classList.add("hidden");
                albumContainer.classList.remove("hidden");
                renderAlbumPage();
            }
        }

        // 3D Albom sahifasini to'ldirish
        function renderAlbumPage() {
            const memory = filteredMemories[currentIndex];
            if (!memory) return;

            document.getElementById("page-category-badge").textContent = memory.category || "Xotira";
            document.getElementById("page-indicator").textContent = `${currentIndex + 1} / ${filteredMemories.length} - sahifa`;

            const imgEl = document.getElementById("memory-image");
            imgEl.src = memory.imageUrl;
            imgEl.onerror = () => {
                imgEl.src = "https://placehold.co/800x600/EFE6D8/5C3D28?text=Oilaviy+Xotira";
            };

            document.getElementById("memory-date").textContent = memory.date || "Unutilmas kun";
            document.getElementById("memory-author").textContent = `${memory.authorName} (${memory.authorRelation || "Qarindosh"})`;
            document.getElementById("memory-title").textContent = memory.title;
            document.getElementById("memory-caption").textContent = memory.caption;

            // O'chirish tugmasi (faqat o'zi yuklagan rasmlar uchun)
            const deleteBtn = document.getElementById("delete-photo-btn");
            if (!memory.isDemo && currentUser && memory.ownerUid === currentUser.uid) {
                deleteBtn.classList.remove("hidden");
            } else {
                deleteBtn.classList.add("hidden");
            }

            // Yurakchalar (Likes)
            const likes = Array.isArray(memory.likes) ? memory.likes : [];
            const uid = currentUser ? currentUser.uid : "guest_user";
            const isLiked = likes.includes(uid);

            document.getElementById("like-count").textContent = likes.length;
            const likeIcon = document.getElementById("like-icon");
            if (isLiked) {
                likeIcon.className = "fa-solid fa-heart text-rose-600 text-base";
            } else {
                likeIcon.className = "fa-regular fa-heart text-rose-600 text-base";
            }

            // Izohlar (Comments)
            const comments = Array.isArray(memory.comments) ? memory.comments : [];
            document.getElementById("comments-count").textContent = comments.length;
            const commentsList = document.getElementById("comments-list");

            if (comments.length === 0) {
                commentsList.innerHTML = `<p class="text-xs italic text-[#9A897D] py-2">Hali izoh yozilmagan. Birinchi bo'lib iliq fikr qoldiring!</p>`;
            } else {
                commentsList.innerHTML = comments.map(c => `
                    <div class="bg-white/90 rounded-xl px-3 py-2 border border-[#EAE0D1] text-xs">
                        <div class="flex items-center justify-between mb-0.5">
                            <span class="font-semibold text-[#5C3D28]">${escapeHtml(c.author)}</span>
                            <span class="text-[10px] text-[#9A897D]">${escapeHtml(c.time || "")}</span>
                        </div>
                        <p class="text-[#3A2E28] leading-snug">${escapeHtml(c.text)}</p>
                    </div>
                `).join("");
                commentsList.scrollTop = commentsList.scrollHeight;
            }

            // Oldingi / Keyingi tugmalar holati
            document.getElementById("prev-page-btn").disabled = currentIndex === 0;
            document.getElementById("next-page-btn").disabled = currentIndex === filteredMemories.length - 1;

            // Sahifa nuqtalari
            const dotsContainer = document.getElementById("page-dots");
            dotsContainer.innerHTML = filteredMemories.map((_, idx) => `
                <button onclick="goToPage(${idx})" class="h-2 rounded-full transition-all ${idx === currentIndex ? 'w-6 bg-[#8B5E3C]' : 'w-2 bg-[#D5C5B0] hover:bg-[#B39B7D]'}" title="${idx + 1}-sahifa"></button>
            `).join("");
        }

        // Barcha rasmlarni To'r (Grid) ko'rinishida chizish
        function renderGridView() {
            const grid = document.getElementById("memories-grid");
            grid.innerHTML = filteredMemories.map((m, idx) => `
                <div onclick="openFromGrid(${idx})" class="photo-frame cursor-pointer flex flex-col justify-between group">
                    <div>
                        <div class="relative overflow-hidden rounded aspect-[4/3] bg-[#F5EFE6] mb-3">
                            <img src="${m.imageUrl}" alt="${escapeHtml(m.title)}" class="w-full h-full object-cover group-hover:scale-105 transition duration-500">
                            <span class="absolute top-2 left-2 px-2.5 py-0.5 rounded-full text-[11px] font-medium bg-black/60 text-white backdrop-blur-sm">
                                ${escapeHtml(m.category)}
                            </span>
                        </div>
                        <h3 class="font-serif-album font-bold text-base text-[#3E2718] line-clamp-1">${escapeHtml(m.title)}</h3>
                        <p class="text-xs text-[#6E5D53] line-clamp-2 mt-1">${escapeHtml(m.caption)}</p>
                    </div>
                    <div class="mt-3 pt-2 border-t border-[#EFE6D8] flex items-center justify-between text-xs text-[#8E7B6E]">
                        <span><i class="fa-solid fa-user text-[#8B5E3C] mr-1"></i>${escapeHtml(m.authorName)}</span>
                        <span class="text-rose-600 font-medium"><i class="fa-solid fa-heart mr-1"></i>${(m.likes || []).length}</span>
                    </div>
                </div>
            `).join("");
        }

        // 3D Varoqlash Animatsiyasi bilan sahifa almashtirish
        function flipPageWithAnimation(newIndex, direction) {
            if (newIndex < 0 || newIndex >= filteredMemories.length || newIndex === currentIndex) return;

            const pageEl = document.getElementById("album-page");
            const outClass = direction === "next" ? "flip-next-out" : "flip-prev-out";
            const inClass = direction === "next" ? "flip-next-in" : "flip-prev-in";

            if (typeof Tone !== 'undefined' && Tone.context.state !== 'running') {
                Tone.start();
            }
            playPageFlipSound();

            pageEl.classList.remove("flip-next-out", "flip-next-in", "flip-prev-out", "flip-prev-in");
            pageEl.classList.add(outClass);

            setTimeout(() => {
                currentIndex = newIndex;
                renderAlbumPage();
                pageEl.classList.remove(outClass);
                pageEl.classList.add(inClass);

                setTimeout(() => {
                    pageEl.classList.remove(inClass);
                }, 450);
            }, 260);
        }

        window.nextPage = function() {
            if (currentIndex < filteredMemories.length - 1) {
                flipPageWithAnimation(currentIndex + 1, "next");
            }
        };

        window.prevPage = function() {
            if (currentIndex > 0) {
                flipPageWithAnimation(currentIndex - 1, "prev");
            }
        };

        window.goToPage = function(idx) {
            const dir = idx > currentIndex ? "next" : "prev";
            flipPageWithAnimation(idx, dir);
        };

        window.openFromGrid = function(idx) {
            isGridView = false;
            document.getElementById("view-toggle-icon").className = "fa-solid fa-table-cells-large";
            currentIndex = idx;
            renderCurrentView();
        };

        window.toggleViewMode = function() {
            isGridView = !isGridView;
            const icon = document.getElementById("view-toggle-icon");
            icon.className = isGridView ? "fa-solid fa-book-open" : "fa-solid fa-table-cells-large";
            renderCurrentView();
        };

        // Slayd-shou (Avtomatik varoqlash)
        window.toggleSlideshow = function() {
            const btn = document.getElementById("slideshow-btn");
            const icon = document.getElementById("slideshow-icon");
            const text = document.getElementById("slideshow-text");

            if (slideshowInterval) {
                clearInterval(slideshowInterval);
                slideshowInterval = null;
                icon.className = "fa-solid fa-play";
                text.textContent = "Slayd-shou";
                btn.classList.remove("bg-[#8B5E3C]", "text-white");
                showToast("Slayd-shou to'xtatildi", "info");
            } else {
                if (isGridView) toggleViewMode();
                icon.className = "fa-solid fa-pause";
                text.textContent = "To'xtatish";
                btn.classList.add("bg-[#8B5E3C]", "text-white");
                showToast("Xotiralar sayohati boshlandi (har 4 soniyada varoqlanadi)", "success");

                slideshowInterval = setInterval(() => {
                    if (currentIndex < filteredMemories.length - 1) {
                        flipPageWithAnimation(currentIndex + 1, "next");
                    } else {
                        flipPageWithAnimation(0, "prev");
                    }
                }, 4000);
            }
        };

        // Rasmni siqish (Canvas orqali Firestore 1MB limitiga moslash uchun)
        window.previewSelectedFile = function(event) {
            const file = event.target.files[0];
            if (!file) return;

            const reader = new FileReader();
            reader.onload = function(e) {
                const img = new Image();
                img.onload = function() {
                    const canvas = document.createElement("canvas");
                    const MAX_WIDTH = 900;
                    const MAX_HEIGHT = 900;
                    let width = img.width;
                    let height = img.height;

                    if (width > height) {
                        if (width > MAX_WIDTH) {
                            height *= MAX_WIDTH / width;
                            width = MAX_WIDTH;
                        }
                    } else {
                        if (height > MAX_HEIGHT) {
                            width *= MAX_HEIGHT / height;
                            height = MAX_HEIGHT;
                        }
                    }

                    canvas.width = width;
                    canvas.height = height;
                    const ctx = canvas.getContext("2d");
                    ctx.drawImage(img, 0, 0, width, height);

                    compressedBase64 = canvas.toDataURL("image/jpeg", 0.78);
                    document.getElementById("upload-preview-img").src = compressedBase64;
                    document.getElementById("preview-wrapper").classList.remove("hidden");
                    document.getElementById("upload-placeholder").classList.add("hidden");
                };
                img.src = e.target.result;
            };
            reader.readAsDataURL(file);
        };

        // Yangi rasm va izohni saqlash
        window.handlePhotoUpload = async function(event) {
            event.preventDefault();
            if (!compressedBase64) {
                showToast("Iltimos, avval rasm tanlang!", "error");
                return;
            }

            const submitBtn = document.getElementById("submit-upload-btn");
            submitBtn.disabled = true;
            submitBtn.innerHTML = `<i class="fa-solid fa-spinner animate-spin"></i> <span>Yuklanmoqda...</span>`;

            const name = document.getElementById("upload-name").value.trim() || "Qarindosh";
            const relation = document.getElementById("upload-relation").value;
            const title = document.getElementById("upload-title").value.trim();
            const category = document.getElementById("upload-category").value;
            const dateStr = document.getElementById("upload-date").value.trim() || new Date().toLocaleDateString("uz-UZ");
            const caption = document.getElementById("upload-caption").value.trim();

            // Foydalanuvchi profilini yangilab qo'yamiz
            relativeProfile = { name, relation };
            updateUserLabel();

            const newMemory = {
                title,
                category,
                date: dateStr,
                authorName: name,
                authorRelation: relation,
                imageUrl: compressedBase64,
                caption,
                likes: [],
                comments: [],
                ownerUid: currentUser ? currentUser.uid : "guest_user",
                createdAt: Date.now()
            };

            try {
                if (isCloudReady && currentUser && db) {
                    const memoriesRef = collection(db, 'artifacts', appId, 'public', 'data', 'family_memories');
                    await addDoc(memoriesRef, newMemory);
                } else {
                    newMemory.id = "local-" + Date.now();
                    allMemories.unshift(newMemory);
                    applyFilters(true);
                }

                closeUploadModal();
                showToast("Ajoyib! Xotira surati umumiy albomga qo'shildi ❤️", "success");
            } catch (err) {
                console.error("Yuklash xatosi:", err);
                showToast("Rasmni saqlashda xatolik yuz berdi. Qayta urinib ko'ring.", "error");
            } finally {
                submitBtn.disabled = false;
                submitBtn.innerHTML = `<i class="fa-solid fa-check"></i> <span>Albomga joylash</span>`;
            }
        };

        // Yurakcha (Like) bosish
        window.toggleLikeCurrent = async function() {
            const memory = filteredMemories[currentIndex];
            if (!memory) return;

            const likeIcon = document.getElementById("like-icon");
            likeIcon.classList.add("heart-pop");
            setTimeout(() => likeIcon.classList.remove("heart-pop"), 450);

            const uid = currentUser ? currentUser.uid : "guest_user";
            const likes = Array.isArray(memory.likes) ? memory.likes : [];
            const alreadyLiked = likes.includes(uid);

            if (memory.isDemo || !isCloudReady || !currentUser || !db) {
                if (alreadyLiked) {
                    memory.likes = likes.filter(id => id !== uid);
                } else {
                    memory.likes = [...likes, uid];
                }
                renderAlbumPage();
                return;
            }

            try {
                const docRef = doc(db, 'artifacts', appId, 'public', 'data', 'family_memories', memory.id);
                if (alreadyLiked) {
                    await updateDoc(docRef, { likes: arrayRemove(uid) });
                } else {
                    await updateDoc(docRef, { likes: arrayUnion(uid) });
                }
            } catch (e) {
                console.error("Like xatosi:", e);
            }
        };

        // Rasm ostiga qarindosh izohi qo'shish
        window.submitComment = async function(event) {
            event.preventDefault();
            const input = document.getElementById("comment-input");
            const text = input.value.trim();
            if (!text) return;

            const memory = filteredMemories[currentIndex];
            if (!memory) return;

            const commentObj = {
                author: `${relativeProfile.name} (${relativeProfile.relation})`,
                text: text,
                time: "Hozirgina"
            };

            input.value = "";

            if (memory.isDemo || !isCloudReady || !currentUser || !db) {
                memory.comments = [...(memory.comments || []), commentObj];
                renderAlbumPage();
                showToast("Izohingiz qo'shildi!", "success");
                return;
            }

            try {
                const docRef = doc(db, 'artifacts', appId, 'public', 'data', 'family_memories', memory.id);
                await updateDoc(docRef, {
                    comments: arrayUnion(commentObj)
                });
                showToast("Iliq fikringiz albomga yozildi!", "success");
            } catch (e) {
                console.error("Izoh qo'shish xatosi:", e);
                showToast("Izohni yuborishda xato yuz berdi", "error");
            }
        };

        // O'zi yuklagan rasmni o'chirish
        window.deleteCurrentMemory = async function() {
            const memory = filteredMemories[currentIndex];
            if (!memory || memory.isDemo) return;

            try {
                if (isCloudReady && currentUser && db) {
                    const docRef = doc(db, 'artifacts', appId, 'public', 'data', 'family_memories', memory.id);
                    await deleteDoc(docRef);
                } else {
                    allMemories = allMemories.filter(m => m.id !== memory.id);
                    applyFilters(true);
                }
                showToast("Surat albomdan olib tashlandi", "info");
            } catch (e) {
                console.error("O'chirish xatosi:", e);
            }
        };

        // Qarindoshlar guruhiga ulashish (Clipboardga nusxalash)
        window.shareToGroup = function() {
            const url = window.location.href;
            const shareText = `Assalomu alaykum aziz qarindoshlar! ❤️\nOilaviy umumiy xotiralar albomimizga kiring, rasmlarni varoqlab ko'ring va o'zingizdagi eng shirin rasmlarni ham qo'shib qo'ying:\n${url}`;

            // iframe ichida ishonchli nusxalash (execCommand)
            const tempInput = document.createElement("textarea");
            tempInput.value = shareText;
            document.body.appendChild(tempInput);
            tempInput.select();
            try {
                document.execCommand("copy");
                showToast("Taklif matni va havola nusxalandi! Endi Telegram guruhiga 'Joylashtirish' (Paste) qiling 📋", "success");
            } catch (err) {
                showToast("Havolani brauzer manzilidan nusxalab guruhga yuboring!", "info");
            }
            document.body.removeChild(tempInput);
        };

        // Rasmni yuklab olish
        window.downloadCurrentPhoto = function() {
            const memory = filteredMemories[currentIndex];
            if (!memory) return;
            const a = document.createElement("a");
            a.href = memory.imageUrl;
            a.download = `${(memory.title || "oilaviy-xotira").replace(/\s+/g, "_")}.jpg`;
            document.body.appendChild(a);
            a.click();
            document.body.removeChild(a);
            showToast("Rasm qurilmangizga yuklanmoqda...", "success");
        };

        // Modal oynalarni boshqarish
        window.openUploadModal = function() {
            document.getElementById("upload-name").value = relativeProfile.name;
            document.getElementById("upload-modal").classList.remove("hidden");
        };

        window.closeUploadModal = function() {
            document.getElementById("upload-modal").classList.add("hidden");
            document.getElementById("upload-form").reset();
            compressedBase64 = null;
            document.getElementById("preview-wrapper").classList.add("hidden");
            document.getElementById("upload-placeholder").classList.remove("hidden");
        };

        window.openProfileModal = function() {
            document.getElementById("profile-name-input").value = relativeProfile.name;
            document.getElementById("profile-modal").classList.remove("hidden");
        };

        window.closeProfileModal = function() {
            document.getElementById("profile-modal").classList.add("hidden");
        };

        window.saveUserProfile = function(event) {
            event.preventDefault();
            const name = document.getElementById("profile-name-input").value.trim();
            const relation = document.getElementById("profile-relation-input").value;
            if (name) {
                relativeProfile = { name, relation };
                updateUserLabel();
                closeProfileModal();
                showToast(`Xush kelibsiz, ${name} (${relation})!`, "success");
            }
        };

        function updateUserLabel() {
            document.getElementById("current-user-label").textContent = `${relativeProfile.name}`;
        }

        window.openLightbox = function() {
            const memory = filteredMemories[currentIndex];
            if (!memory) return;
            document.getElementById("lightbox-img").src = memory.imageUrl;
            document.getElementById("lightbox-caption").textContent = `${memory.title} — ${memory.caption}`;
            document.getElementById("lightbox-modal").classList.remove("hidden");
        };

        window.closeLightbox = function() {
            document.getElementById("lightbox-modal").classList.add("hidden");
        };

        // XSS himoyasi uchun matn tozalash
        function escapeHtml(text) {
            if (!text) return "";
            const div = document.createElement("div");
            div.textContent = text;
            return div.innerHTML;
        }

        // Kategoriya tugmalari hodisalari
        document.querySelectorAll(".cat-btn").forEach(btn => {
            btn.addEventListener("click", () => {
                document.querySelectorAll(".cat-btn").forEach(b => {
                    b.classList.remove("bg-[#8B5E3C]", "text-white", "shadow-sm");
                    b.classList.add("bg-[#F5EFE6]", "text-[#5C493E]");
                });
                btn.classList.remove("bg-[#F5EFE6]", "text-[#5C493E]");
                btn.classList.add("bg-[#8B5E3C]", "text-white", "shadow-sm");

                selectedCategory = btn.getAttribute("data-cat");
                applyFilters(true);
            });
        });

        // Qidiruv maydoni hodisasi
        document.getElementById("search-input").addEventListener("input", (e) => {
            searchQuery = e.target.value;
            applyFilters(true);
        });

        // Klaviatura strelkalari orqali varoqlash
        document.addEventListener("keydown", (e) => {
            if (e.target.tagName === "INPUT" || e.target.tagName === "TEXTAREA") return;
            if (e.key === "ArrowRight") nextPage();
            if (e.key === "ArrowLeft") prevPage();
            if (e.key === "Escape") {
                closeLightbox();
                closeUploadModal();
                closeProfileModal();
            }
        });

        // Mobil qurilmalarda barmoq bilan surib (Swipe) varoqlash
        let touchStartX = 0;
        const albumStage = document.getElementById("album-view-section");
        albumStage.addEventListener("touchstart", (e) => {
            touchStartX = e.changedTouches[0].screenX;
        }, { passive: true });

        albumStage.addEventListener("touchend", (e) => {
            const touchEndX = e.changedTouches[0].screenX;
            const diff = touchStartX - touchEndX;
            if (Math.abs(diff) > 55) {
                if (diff > 0) nextPage();
                else prevPage();
            }
        }, { passive: true });

        // Ilovani ishga tushirish
        window.addEventListener("load", initApp);
    </script>
</body>
</html>
