<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title id="page-title">Surya.PromptGeneratorPRO</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;700;900&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Inter', sans-serif;
        }
        .form-input, .form-select, .form-textarea {
            background-color: #1F2937; /* bg-gray-800 */
            border: 1px solid #4B5563; /* border-gray-600 */
            color: #F9FAFB; /* text-gray-50 */
            border-radius: 0.5rem; /* rounded-lg */
            padding: 0.75rem;
            width: 100%;
            transition: all 0.2s ease-in-out;
        }
        .form-input:focus, .form-select:focus, .form-textarea:focus {
            outline: none;
            border-color: #3B82F6; /* border-blue-500 */
            box-shadow: 0 0 0 2px rgba(59, 130, 246, 0.4);
        }
        .card {
            background-color: #374151; /* bg-gray-700 */
            border-radius: 0.75rem; /* rounded-xl */
            padding: 1.5rem; /* p-6 */
            box-shadow: 0 10px 15px -3px rgba(0,0,0,0.1), 0 4px 6px -2px rgba(0,0,0,0.05);
        }
        .btn {
            padding: 0.75rem 1.5rem;
            border-radius: 0.5rem;
            font-weight: 700;
            text-align: center;
            transition: all 0.2s ease-in-out;
            cursor: pointer;
            display: inline-flex;
            align-items: center;
            justify-content: center;
        }
        .btn-green {
            background-color: #10B981; /* bg-emerald-500 */
            color: white;
        }
        .btn-green:hover {
            background-color: #059669; /* bg-emerald-600 */
        }
        .btn-blue {
            background-color: #3B82F6; /* bg-blue-500 */
            color: white;
        }
        .btn-blue:hover {
            background-color: #2563EB; /* bg-blue-600 */
        }
        .btn-gray {
             background-color: #4B5563; /* bg-gray-600 */
             color: white;
        }
        .btn-gray:hover {
             background-color: #6B7280; /* bg-gray-500 */
        }
        .hidden {
            display: none;
        }
        .sub-card {
            border: 1px solid #4B5563; /* border-gray-600 */
            padding: 1rem; /* p-4 */
            border-radius: 0.5rem; /* rounded-lg */
        }
        /* Styles for Modals (Info & Language) */
        .modal-container {
            position: fixed;
            inset: 0;
            background-color: rgba(0,0,0,0.75);
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 1rem;
            z-index: 50;
        }
        .modal-content {
            background-color: #1F2937; /* bg-gray-800 */
            border-radius: 0.5rem; /* rounded-lg */
            padding: 2rem;
            max-width: 24rem; /* max-w-sm */
            width: 100%;
            text-align: center;
            position: relative;
        }
        .modal-close-btn {
            position: absolute;
            top: 0.75rem; /* top-3 */
            right: 0.75rem; /* right-3 */
            color: #9CA3AF; /* text-gray-400 */
        }
        .modal-close-btn:hover {
             color: #FFFFFF; /* hover:text-white */
        }
    </style>
</head>
<body class="bg-gray-900 text-white">

    <!-- Landing Screen -->
    <div id="landing-screen" class="min-h-screen flex flex-col items-center justify-center text-center p-4">
        <p id="landing-subtitle" class="text-xl md:text-2xl text-gray-300 mb-2">Kreasikan imajinasi dan idemu</p>
        <h1 id="landing-title" class="text-4xl md:text-6xl font-black mb-8 bg-clip-text text-transparent bg-gradient-to-r from-green-400 to-blue-500">Surya.PromptGeneratorPRO</h1>
        <button id="start-btn" class="btn btn-green text-2xl shadow-lg transform hover:scale-105">
            <span id="start-btn-text">Mulai</span>
            <svg xmlns="http://www.w3.org/2000/svg" width="28" height="28" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="ml-3"><path d="M21 18V6a2 2 0 0 0-2-2H5a2 2 0 0 0-2 2v12a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2z"></path><path d="M9 10a2 2 0 1 1-4 0 2 2 0 0 1 4 0z"></path><path d="m21 14-4.2-4.2a2 2 0 0 0-2.82 0L8 16"></path></svg>
        </button>
        <!-- Language button on landing is now hidden -->
        <button id="lang-btn-landing" class="btn btn-gray mt-6 hidden">
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="mr-2"><path d="m5 8 6 6"></path><path d="m4 14 6-6 2-3"></path><path d="M2 5h12"></path><path d="M7 2h1"></path><path d="m22 22-5-10-5 10"></path><path d="M14 18h6"></path></svg>
            <span id="lang-btn-landing-text">Bahasa</span>
        </button>
    </div>

    <!-- Main App Screen -->
    <div id="app-screen" class="hidden p-4 md:p-8 max-w-7xl mx-auto">
        <header class="flex justify-between items-center mb-8">
            <h2 id="app-title" class="text-3xl font-bold">Prompt Generator</h2>
            <div class="flex items-center space-x-2">
                <button id="lang-btn-app" class="btn btn-gray">
                    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="mr-2"><path d="m5 8 6 6"></path><path d="m4 14 6-6 2-3"></path><path d="M2 5h12"></path><path d="M7 2h1"></path><path d="m22 22-5-10-5 10"></path><path d="M14 18h6"></path></svg>
                    <span id="lang-btn-app-text">Bahasa</span>
                </button>
                <button id="info-btn" class="btn btn-gray">
                    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="mr-2"><circle cx="12" cy="12" r="10"></circle><line x1="12" y1="16" x2="12" y2="12"></line><line x1="12" y1="8" x2="12.01" y2="8"></line></svg>
                    <span id="info-btn-text">Info</span>
                </button>
            </div>
        </header>

        <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
            <!-- Kolom Input -->
            <div class="space-y-6">
                <!-- Karakter -->
                <div class="card">
                    <h3 id="card-title-character" class="text-xl font-bold mb-4">Karakter</h3>
                    <div id="character-container" class="space-y-4">
                        <div class="character-card sub-card">
                            <h4 class="font-semibold mb-2 text-lg" data-lang-key="character_card_title" data-lang-val="1">Karakter 1</h4>
                            <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                                <input type="text" data-lang-placeholder="placeholder_char_name" placeholder="Nama" class="form-input char-name">
                                <input type="number" data-lang-placeholder="placeholder_char_age" placeholder="Umur" class="form-input">
                                <input type="text" data-lang-placeholder="placeholder_char_height" placeholder="Tinggi (cth: 175cm)" class="form-input">
                                <input type="text" data-lang-placeholder="placeholder_char_weight" placeholder="Berat Badan (cth: 70kg)" class="form-input">
                                <input type="text" data-lang-placeholder="placeholder_char_hair" placeholder="Style & Warna Rambut" class="form-input">
                                <input type="text" data-lang-placeholder="placeholder_char_skin" placeholder="Warna Kulit (Rekomendasi Gemini)" class="form-input">
                                <input type="text" data-lang-placeholder="placeholder_char_eyes" placeholder="Warna Mata" class="form-input">
                                <input type="text" data-lang-placeholder="placeholder_char_trait" placeholder="Sifat (Opsional)" class="form-input">
                            </div>
                        </div>
                    </div>
                    <button id="add-character-btn" class="btn btn-blue mt-4">+ Tambah Karakter</button>
                </div>

                <!-- Lokasi -->
                <div class="card">
                    <h3 id="card-title-location" class="text-xl font-bold mb-4">Lokasi</h3>
                    <div class="space-y-4">
                        <textarea id="location-desc" class="form-textarea" rows="3" data-lang-placeholder="placeholder_location_desc" placeholder="Deskripsikan detail tempat..."></textarea>
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                             <select id="weather-select" class="form-select">
                                <option value="" data-lang-key="select_weather">-- Pilih Cuaca --</option>
                                <option value="Cerah" data-lang-key="weather_sunny">Cerah</option>
                                <option value="Berawan" data-lang-key="weather_cloudy">Berawan</option>
                                <option value="Hujan" data-lang-key="weather_rainy">Hujan</option>
                                <option value="Badai" data-lang-key="weather_stormy">Badai</option>
                                <option value="Berkabut" data-lang-key="weather_foggy">Berkabut</option>
                                <option value="manual" data-lang-key="manual_option">Manual...</option>
                            </select>
                             <select id="situation-select" class="form-select">
                                <option value="" data-lang-key="select_situation">-- Pilih Situasi Lokasi --</option>
                                <option value="Ramai" data-lang-key="situation_crowded">Ramai</option>
                                <option value="Sepi" data-lang-key="situation_quiet">Sepi</option>
                                <option value="Normal" data-lang-key="situation_normal">Normal</option>
                                <option value="Kacau" data-lang-key="situation_chaotic">Kacau</option>
                                <option value="manual" data-lang-key="manual_option">Manual...</option>
                            </select>
                        </div>
                        <select id="mood-select" class="form-select">
                            <option value="" data-lang-key="select_mood">-- Pilih Nuansa --</option>
                            <option value="Harmonis" data-lang-key="mood_harmonious">Harmonis</option>
                            <option value="Tegang" data-lang-key="mood_tense">Tegang</option>
                            <option value="Mencekam" data-lang-key="mood_gripping">Mencekam</option>
                            <option value="Misterius" data-lang-key="mood_mysterious">Misterius</option>
                            <option value="Romantis" data-lang-key="mood_romantic">Romantis</option>
                            <option value="Bahagia" data-lang-key="mood_happy">Bahagia</option>
                            <option value="manual" data-lang-key="manual_option">Manual...</option>
                        </select>
                    </div>
                </div>
                
                <!-- Adegan -->
                <div class="card">
                    <h3 id="card-title-scene" class="text-xl font-bold mb-4">Adegan</h3>
                    <div id="scene-container" class="space-y-4">
                        <div class="scene-card sub-card">
                             <h4 class="font-semibold mb-2 text-lg" data-lang-key="scene_card_title" data-lang-val="1">Adegan 1</h4>
                             <div class="space-y-4">
                                <textarea class="form-textarea" rows="3" data-lang-placeholder="placeholder_scene_desc" placeholder="Deskripsikan adegan..."></textarea>
                                <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                                    <input type="number" data-lang-placeholder="placeholder_scene_start" placeholder="Detik Mulai Adegan" class="form-input">
                                    <input type="number" data-lang-placeholder="placeholder_scene_end" placeholder="Detik Akhir Adegan" class="form-input">
                                </div>
                                <select class="form-select">
                                    <option value="" data-lang-key="select_camera_angle">-- Pilih Angle Kamera --</option>
                                    <option value="Eye Level">Eye Level</option>
                                    <option value="High Angle">High Angle</option>
                                    <option value="Low Angle">Low Angle</option>
                                    <option value="Dutch Angle">Dutch Angle</option>
                                    <option value="Over the Shoulder">Over the Shoulder</option>
                                    <option value="Point of View (POV)">Point of View (POV)</option>
                                    <option value="Wide Shot">Wide Shot</option>
                                    <option value="Medium Shot">Medium Shot</option>
                                    <option value="Close Up">Close Up</option>
                                    <option value="Extreme Close Up">Extreme Close Up</option>
                                    <option value="rekomendasi" data-lang-key="recommendation_option">Rekomendasi Sesuai Adegan</option>
                                </select>
                                 <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                                    <input type="number" data-lang-placeholder="placeholder_angle_start" placeholder="Detik Mulai Angle" class="form-input">
                                    <input type="number" data-lang-placeholder="placeholder_angle_end" placeholder="Detik Akhir Angle" class="form-input">
                                </div>
                            </div>
                        </div>
                    </div>
                     <button id="add-scene-btn" class="btn btn-blue mt-4">+ Tambah Adegan</button>
                </div>

                <!-- Detail Tambahan -->
                 <div class="card">
                    <h3 id="card-title-details" class="text-xl font-bold mb-4">Detail Tambahan</h3>
                    <div class="space-y-4">
                        <div class="p-2 border border-dashed border-gray-500 rounded-lg">
                            <label id="label-expression" class="font-semibold">Ekspresi</label>
                            <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mt-2">
                                <input type="text" data-lang-placeholder="placeholder_expression_desc" placeholder="Deskripsi Ekspresi (cth: tersenyum tipis)" class="form-input">
                                <select class="form-select expression-char-select"><option value="" data-lang-key="select_character">-- Pilih Karakter --</option></select>
                            </div>
                            <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mt-2">
                                <input type="number" data-lang-placeholder="placeholder_detail_start" placeholder="Detik Mulai" class="form-input">
                                <input type="number" data-lang-placeholder="placeholder_detail_end" placeholder="Detik Akhir" class="form-input">
                            </div>
                        </div>
                        <div class="p-2 border border-dashed border-gray-500 rounded-lg">
                            <label id="label-gesture" class="font-semibold">Gestur</label>
                            <input type="text" data-lang-placeholder="placeholder_gesture_desc" placeholder="Deskripsi Gestur (cth: mengangkat tangan)" class="form-input mt-2">
                            <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mt-2">
                                <input type="number" data-lang-placeholder="placeholder_detail_start" placeholder="Detik Mulai" class="form-input">
                                <input type="number" data-lang-placeholder="placeholder_detail_end" placeholder="Detik Akhir" class="form-input">
                            </div>
                        </div>
                        <div class="p-2 border border-dashed border-gray-500 rounded-lg">
                            <label id="label-dialogue" class="font-semibold">Dialog</label>
                            <textarea class="form-textarea mt-2" rows="2" data-lang-placeholder="placeholder_dialogue_text" placeholder="Isi dialog..."></textarea>
                            <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mt-2">
                                <select class="form-select">
                                    <option value="Indonesia" data-lang-key="lang_indonesian">Bahasa Indonesia</option>
                                    <option value="Inggris" data-lang-key="lang_english">Bahasa Inggris</option>
                                </select>
                                <select class="form-select dialog-char-select"><option value="" data-lang-key="select_character">-- Pilih Karakter --</option></select>
                            </div>
                             <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mt-2">
                                <input type="number" data-lang-placeholder="placeholder_detail_start" placeholder="Detik Mulai" class="form-input">
                                <input type="number" data-lang-placeholder="placeholder_detail_end" placeholder="Detik Akhir" class="form-input">
                            </div>
                        </div>
                        <div class="flex items-center justify-between p-2">
                            <label id="label-subtitle" class="font-semibold">Subtitle</label>
                            <div class="flex items-center space-x-4">
                                <span data-lang-key="lang_indonesian">Indonesia</span>
                                <label class="relative inline-flex items-center cursor-pointer">
                                  <input type="checkbox" value="sub-id" class="sr-only peer" checked>
                                  <div class="w-11 h-6 bg-gray-600 peer-focus:outline-none rounded-full peer peer-checked:after:translate-x-full peer-checked:after:border-white after:content-[''] after:absolute after:top-[2px] after:left-[2px] after:bg-white after:border-gray-300 after:border after:rounded-full after:h-5 after:w-5 after:transition-all peer-checked:bg-blue-600"></div>
                                </label>
                                <span data-lang-key="lang_english">Inggris</span>
                                 <label class="relative inline-flex items-center cursor-pointer">
                                  <input type="checkbox" value="sub-en" class="sr-only peer">
                                  <div class="w-11 h-6 bg-gray-600 peer-focus:outline-none rounded-full peer peer-checked:after:translate-x-full peer-checked:after:border-white after:content-[''] after:absolute after:top-[2px] after:left-[2px] after:bg-white after:border-gray-300 after:border after:rounded-full after:h-5 after:w-5 after:transition-all peer-checked:bg-blue-600"></div>
                                </label>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Kolom Output -->
            <div class="space-y-6">
                <div class="card sticky top-8">
                    <button id="generate-btn" class="btn btn-green w-full text-lg mb-4">
                        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="mr-2"><path d="M12 2a10 10 0 1 0 10 10A10 10 0 0 0 12 2v0a10 10 0 0 0-1.08 3.9M12 2a10 10 0 0 1 10 10M12 2v10m0 0a10 10 0 0 1-10 10m10-10a10 10 0 0 0 10 10m-10-10L2 12m10 10 10-10"></path></svg>
                        <span id="generate-btn-text">Generate Prompt</span>
                    </button>
                    <h3 id="output-title" class="text-xl font-bold mb-4">Hasil Prompt</h3>
                    <div class="relative">
                        <textarea id="output-prompt" class="form-textarea h-96" rows="20" readonly data-lang-placeholder="placeholder_output" placeholder="Hasil prompt akan muncul di sini..."></textarea>
                        <button id="copy-btn" class="btn btn-blue absolute top-3 right-3 px-3 py-2">
                             <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect x="9" y="9" width="13" height="13" rx="2" ry="2"></rect><path d="M5 15H4a2 2 0 0 1-2-2V4a2 2 0 0 1 2-2h9a2 2 0 0 1 2 2v1"></path></svg>
                        </button>
                    </div>
                    <div id="copy-feedback" class="hidden mt-2 text-center text-green-400 font-semibold flex items-center justify-center">
                        <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="3" stroke-linecap="round" stroke-linejoin="round" class="mr-2"><polyline points="20 6 9 17 4 12"></polyline></svg>
                        <span id="copy-feedback-text">Copy sukses!</span>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Info Modal -->
    <div id="info-modal" class="hidden modal-container">
        <div class="modal-content">
            <button id="close-info-modal-btn" class="modal-close-btn">
                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><line x1="18" y1="6" x2="6" y2="18"></line><line x1="6" y1="6" x2="18" y2="18"></line></svg>
            </button>
            <h3 id="info-modal-title" class="text-2xl font-bold mb-4">Info Pembuat</h3>
            <p id="info-modal-body" class="text-gray-300 mb-4">Aplikasi ini dibuat oleh Surya Ishwara.</p>
            <a id="info-modal-link" href="https://www.tiktok.com/@surya.ishwara" target="_blank" class="btn btn-blue w-full">
                Kunjungi TikTok @surya.ishwara
            </a>
        </div>
    </div>

    <!-- Language Modal -->
    <div id="lang-modal" class="hidden modal-container">
        <div class="modal-content">
             <button id="close-lang-modal-btn" class="modal-close-btn">
                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><line x1="18" y1="6" x2="6" y2="18"></line><line x1="6" y1="6" x2="18" y2="18"></line></svg>
            </button>
            <h3 id="lang-modal-title" class="text-2xl font-bold mb-4">Pilih Bahasa / Select Language</h3>
            <div class="flex justify-center space-x-4">
                <button id="set-lang-id" class="btn btn-gray">Bahasa Indonesia</button>
                <button id="set-lang-en" class="btn btn-blue">English</button>
            </div>
        </div>
    </div>

<script>
document.addEventListener('DOMContentLoaded', () => {

    // --- TRANSLATION DATA ---
    const translations = {
        'id': {
            // General
            page_title: 'Surya.PromptGeneratorPRO',
            lang_btn_text: 'Bahasa',
            info_btn_text: 'Info',
            // Landing
            landing_subtitle: 'Kreasikan imajinasi dan idemu',
            landing_title: 'Surya.PromptGeneratorPRO',
            start_btn_text: 'Mulai',
            // App
            app_title: 'Prompt Generator',
            // Card Titles
            card_title_character: 'Karakter',
            card_title_location: 'Lokasi',
            card_title_scene: 'Adegan',
            card_title_details: 'Detail Tambahan',
            // Character Card
            character_card_title: 'Karakter',
            add_character_btn: '+ Tambah Karakter',
            max_char_alert: 'Maksimal 3 karakter.',
            unnamed_char: 'Karakter Tanpa Nama',
            // Scene Card
            scene_card_title: 'Adegan',
            add_scene_btn: '+ Tambah Adegan',
            max_scene_alert: 'Maksimal 5 adegan.',
            // Detail Card Labels
            label_expression: 'Ekspresi',
            label_gesture: 'Gestur',
            label_dialogue: 'Dialog',
            label_subtitle: 'Subtitle',
            // Output Card
            generate_btn_text: 'Generate Prompt',
            output_title: 'Hasil Prompt',
            copy_feedback_text: 'Copy sukses!',
            copy_fail_alert: 'Gagal menyalin teks.',
            // Placeholders
            placeholder_char_name: 'Nama',
            placeholder_char_age: 'Umur',
            placeholder_char_height: 'Tinggi (cth: 175cm)',
            placeholder_char_weight: 'Berat Badan (cth: 70kg)',
            placeholder_char_hair: 'Style & Warna Rambut',
            placeholder_char_skin: 'Warna Kulit (Rekomendasi Gemini)',
            placeholder_char_eyes: 'Warna Mata',
            placeholder_char_trait: 'Sifat (Opsional)',
            placeholder_location_desc: 'Deskripsikan detail tempat...',
            placeholder_scene_desc: 'Deskripsikan adegan...',
            placeholder_scene_start: 'Detik Mulai Adegan',
            placeholder_scene_end: 'Detik Akhir Adegan',
            placeholder_angle_start: 'Detik Mulai Angle',
            placeholder_angle_end: 'Detik Akhir Angle',
            placeholder_expression_desc: 'Deskripsi Ekspresi (cth: tersenyum tipis)',
            placeholder_gesture_desc: 'Deskripsi Gestur (cth: mengangkat tangan)',
            placeholder_dialogue_text: 'Isi dialog...',
            placeholder_detail_start: 'Detik Mulai',
            placeholder_detail_end: 'Detik Akhir',
            placeholder_output: 'Hasil prompt akan muncul di sini...',
            // Select Options
            select_weather: '-- Pilih Cuaca --',
            weather_sunny: 'Cerah',
            weather_cloudy: 'Berawan',
            weather_rainy: 'Hujan',
            weather_stormy: 'Badai',
            weather_foggy: 'Berkabut',
            manual_option: 'Manual...',
            select_situation: '-- Pilih Situasi Lokasi --',
            situation_crowded: 'Ramai',
            situation_quiet: 'Sepi',
            situation_normal: 'Normal',
            situation_chaotic: 'Kacau',
            select_mood: '-- Pilih Nuansa --',
            mood_harmonious: 'Harmonis',
            mood_tense: 'Tegang',
            mood_gripping: 'Mencekam',
            mood_mysterious: 'Misterius',
            mood_romantic: 'Romantis',
            mood_happy: 'Bahagia',
            select_camera_angle: '-- Pilih Angle Kamera --',
            recommendation_option: 'Rekomendasi Sesuai Adegan',
            select_character: '-- Pilih Karakter --',
            lang_indonesian: 'Bahasa Indonesia',
            lang_english: 'Bahasa Inggris',
            // Info Modal
            info_modal_title: 'Info Pembuat',
            info_modal_body: 'Aplikasi ini dibuat oleh Surya Ishwara.',
            info_modal_link: 'Kunjungi TikTok @surya.ishwara',
            // Prompt Section Titles
            prompt_section_character: 'KARAKTER',
            prompt_section_location: 'LOKASI',
            prompt_section_scene: 'ADEGAN',
            prompt_section_details: 'DETAIL TAMBAHAN',
        },
        'en': {
            // General
            page_title: 'Surya.PromptGeneratorPRO',
            lang_btn_text: 'Language',
            info_btn_text: 'Info',
            // Landing
            landing_subtitle: 'Create your imagination and ideas',
            landing_title: 'Surya.PromptGeneratorPRO',
            start_btn_text: 'Start',
            // App
            app_title: 'Prompt Generator',
            // Card Titles
            card_title_character: 'Character',
            card_title_location: 'Location',
            card_title_scene: 'Scene',
            card_title_details: 'Additional Details',
            // Character Card
            character_card_title: 'Character',
            add_character_btn: '+ Add Character',
            max_char_alert: 'Maximum of 3 characters.',
            unnamed_char: 'Unnamed Character',
            // Scene Card
            scene_card_title: 'Scene',
            add_scene_btn: '+ Add Scene',
            max_scene_alert: 'Maximum of 5 scenes.',
            // Detail Card Labels
            label_expression: 'Expression',
            label_gesture: 'Gesture',
            label_dialogue: 'Dialogue',
            label_subtitle: 'Subtitle',
            // Output Card
            generate_btn_text: 'Generate Prompt',
            output_title: 'Prompt Result',
            copy_feedback_text: 'Copied successfully!',
            copy_fail_alert: 'Failed to copy text.',
            // Placeholders
            placeholder_char_name: 'Name',
            placeholder_char_age: 'Age',
            placeholder_char_height: 'Height (e.g., 175cm)',
            placeholder_char_weight: 'Weight (e.g., 70kg)',
            placeholder_char_hair: 'Hair Style & Color',
            placeholder_char_skin: 'Skin Color (Gemini Recommendation)',
            placeholder_char_eyes: 'Eye Color',
            placeholder_char_trait: 'Traits (Optional)',
            placeholder_location_desc: 'Describe the place details...',
            placeholder_scene_desc: 'Describe the scene...',
            placeholder_scene_start: 'Scene Start (sec)',
            placeholder_scene_end: 'Scene End (sec)',
            placeholder_angle_start: 'Angle Start (sec)',
            placeholder_angle_end: 'Angle End (sec)',
            placeholder_expression_desc: 'Expression desc (e.g., a faint smile)',
            placeholder_gesture_desc: 'Gesture desc (e.g., raising a hand)',
            placeholder_dialogue_text: 'Dialogue text...',
            placeholder_detail_start: 'Start (sec)',
            placeholder_detail_end: 'End (sec)',
            placeholder_output: 'The generated prompt will appear here...',
            // Select Options
            select_weather: '-- Select Weather --',
            weather_sunny: 'Sunny',
            weather_cloudy: 'Cloudy',
            weather_rainy: 'Rainy',
            weather_stormy: 'Stormy',
            weather_foggy: 'Foggy',
            manual_option: 'Manual...',
            select_situation: '-- Select Location Situation --',
            situation_crowded: 'Crowded',
            situation_quiet: 'Quiet',
            situation_normal: 'Normal',
            situation_chaotic: 'Chaotic',
            select_mood: '-- Select Mood --',
            mood_harmonious: 'Harmonious',
            mood_tense: 'Tense',
            mood_gripping: 'Gripping',
            mood_mysterious: 'Mysterious',
            mood_romantic: 'Romantic',
            mood_happy: 'Happy',
            select_camera_angle: '-- Select Camera Angle --',
            recommendation_option: 'Recommendation based on Scene',
            select_character: '-- Select Character --',
            lang_indonesian: 'Indonesian',
            lang_english: 'English',
            // Info Modal
            info_modal_title: 'Creator Info',
            info_modal_body: 'This app was created by Surya Ishwara.',
            info_modal_link: 'Visit TikTok @surya.ishwara',
            // Prompt Section Titles
            prompt_section_character: 'CHARACTER',
            prompt_section_location: 'LOCATION',
            prompt_section_scene: 'SCENE',
            prompt_section_details: 'ADDITIONAL DETAILS',
        }
    };
    
    // --- STATE ---
    let currentLang = 'id';
    
    // --- ELEMENT SELECTIONS ---
    const landingScreen = document.getElementById('landing-screen');
    const appScreen = document.getElementById('app-screen');
    const startBtn = document.getElementById('start-btn');
    const characterContainer = document.getElementById('character-container');
    const characterCardTemplate = characterContainer.querySelector('.character-card').cloneNode(true);
    let characterCount = 1;
    const sceneContainer = document.getElementById('scene-container');
    const sceneCardTemplate = sceneContainer.querySelector('.scene-card').cloneNode(true);
    let sceneCount = 1;
    const generateBtn = document.getElementById('generate-btn');
    const outputPrompt = document.getElementById('output-prompt');
    const copyBtn = document.getElementById('copy-btn');
    const copyFeedback = document.getElementById('copy-feedback');

    // Button elements
    const addCharacterBtn = document.getElementById('add-character-btn');
    const addSceneBtn = document.getElementById('add-scene-btn');
    
    // Info Modal elements
    const infoBtn = document.getElementById('info-btn');
    const infoModal = document.getElementById('info-modal');
    const closeInfoModalBtn = document.getElementById('close-info-modal-btn');
    
    // Lang Modal elements
    const langBtnLanding = document.getElementById('lang-btn-landing');
    const langBtnApp = document.getElementById('lang-btn-app');
    const langModal = document.getElementById('lang-modal');
    const closeLangModalBtn = document.getElementById('close-lang-modal-btn');
    const setLangIdBtn = document.getElementById('set-lang-id');
    const setLangEnBtn = document.getElementById('set-lang-en');

    // --- FUNCTIONS ---
    
    const applyTranslations = (lang) => {
        currentLang = lang;
        const t = translations[lang];

        // Translate by ID
        document.getElementById('page-title').textContent = t.page_title;
        document.getElementById('lang-btn-landing-text').textContent = t.lang_btn_text;
        document.getElementById('landing-subtitle').textContent = t.landing_subtitle;
        document.getElementById('landing-title').textContent = t.landing_title;
        document.getElementById('start-btn-text').textContent = t.start_btn_text;
        document.getElementById('app-title').textContent = t.app_title;
        document.getElementById('lang-btn-app-text').textContent = t.lang_btn_text;
        document.getElementById('info-btn-text').textContent = t.info_btn_text;
        document.getElementById('card-title-character').textContent = t.card_title_character;
        document.getElementById('add-character-btn').textContent = t.add_character_btn;
        document.getElementById('card-title-location').textContent = t.card_title_location;
        document.getElementById('card-title-scene').textContent = t.card_title_scene;
        document.getElementById('add-scene-btn').textContent = t.add_scene_btn;
        document.getElementById('card-title-details').textContent = t.card_title_details;
        document.getElementById('label-expression').textContent = t.label_expression;
        document.getElementById('label-gesture').textContent = t.label_gesture;
        document.getElementById('label-dialogue').textContent = t.label_dialogue;
        document.getElementById('label-subtitle').textContent = t.label_subtitle;
        document.getElementById('generate-btn-text').textContent = t.generate_btn_text;
        document.getElementById('output-title').textContent = t.output_title;
        document.getElementById('copy-feedback-text').textContent = t.copy_feedback_text;
        document.getElementById('info-modal-title').textContent = t.info_modal_title;
        document.getElementById('info-modal-body').textContent = t.info_modal_body;
        document.getElementById('info-modal-link').textContent = t.info_modal_link;
        
        // Translate by data-lang-key attribute (for elements without ID)
        document.querySelectorAll('[data-lang-key]').forEach(el => {
            const key = el.getAttribute('data-lang-key');
            if (t[key]) {
                if(el.hasAttribute('data-lang-val')){
                    // For dynamic text like "Character 1", "Scene 2"
                    el.textContent = `${t[key]} ${el.getAttribute('data-lang-val')}`;
                } else {
                    el.textContent = t[key];
                }
            }
        });

        // Translate placeholders
        document.querySelectorAll('[data-lang-placeholder]').forEach(el => {
            const key = el.getAttribute('data-lang-placeholder');
            if (t[key]) {
                el.placeholder = t[key];
            }
        });

        updateCharacterDropdowns(); // Re-translate character dropdowns
    };

    const setLanguage = (lang) => {
        localStorage.setItem('surya-prompt-lang', lang);
        applyTranslations(lang);
        closeLangModal();
    };
    
    // Modal controls
    const openInfoModal = () => infoModal.classList.remove('hidden');
    const closeInfoModal = () => infoModal.classList.add('hidden');
    const openLangModal = () => langModal.classList.remove('hidden');
    const closeLangModal = () => langModal.classList.add('hidden');
    
    // Character and Scene logic
    const updateCharacterDropdowns = () => {
        const charNames = Array.from(document.querySelectorAll('.char-name'))
                               .map((input, index) => {
                                   const name = input.value.trim();
                                   const unnamedText = translations[currentLang].unnamed_char;
                                   return name || `${unnamedText} ${index + 1}`;
                               });

        const expressionSelects = document.querySelectorAll('.expression-char-select');
        const dialogSelects = document.querySelectorAll('.dialog-char-select');

        [...expressionSelects, ...dialogSelects].forEach(select => {
            const currentVal = select.value;
            const placeholderText = translations[currentLang].select_character;
            select.innerHTML = `<option value="">${placeholderText}</option>`; // Clear existing
            charNames.forEach(name => {
                const option = document.createElement('option');
                option.value = name;
                option.textContent = name;
                select.appendChild(option);
            });
            // Try to restore previous selection
            if (charNames.includes(currentVal)) {
                 select.value = currentVal;
            }
        });
    }
    
    const generatePrompt = () => {
        let promptLines = [];
        const t = translations[currentLang]; // Get current language translations

        // KARAKTER
        const characterCards = document.querySelectorAll('.character-card');
        if (characterCards.length > 0 && characterCards[0].querySelector('.char-name').value.trim()) {
            promptLines.push(`${t.prompt_section_character}:`);
            characterCards.forEach((card, index) => {
                const fields = card.querySelectorAll('input');
                const titleKey = card.querySelector('h4').getAttribute('data-lang-key');
                const titleIndex = card.querySelector('h4').getAttribute('data-lang-val');
                let charDetails = `- ${t[titleKey]} ${titleIndex}:`;

                const details = [
                    fields[0].value.trim() ? `${t.placeholder_char_name}: ${fields[0].value.trim()}` : null,
                    fields[1].value.trim() ? `${t.placeholder_char_age}: ${fields[1].value.trim()}` : null,
                    fields[2].value.trim() ? `${t.placeholder_char_height.split(' ')[0]}: ${fields[2].value.trim()}` : null,
                    fields[3].value.trim() ? `${t.placeholder_char_weight.split(' ')[0]}: ${fields[3].value.trim()}` : null,
                    fields[4].value.trim() ? `${t.placeholder_char_hair.split(' ')[0]}: ${fields[4].value.trim()}` : null,
                    fields[5].value.trim() ? `${t.placeholder_char_skin.split(' ')[0]}: ${fields[5].value.trim()}` : null,
                    fields[6].value.trim() ? `${t.placeholder_char_eyes.split(' ')[0]}: ${fields[6].value.trim()}` : null,
                    fields[7].value.trim() ? `${t.placeholder_char_trait.split(' ')[0]}: ${fields[7].value.trim()}` : null,
                ].filter(Boolean);
                
                if (details.length > 0) {
                     promptLines.push(`${charDetails} ${details.join(', ')}.`);
                }
            });
        }

        // LOKASI
        const locCard = document.querySelector('.card:nth-child(2)');
        const locDesc = locCard.querySelector('textarea').value.trim();
        const locSelects = locCard.querySelectorAll('select');
        const cuaca = locSelects[0].value;
        const situasi = locSelects[1].value;
        const nuansa = locSelects[2].value;

        if (locDesc || cuaca || situasi || nuansa) {
            promptLines.push(`\n${t.prompt_section_location}:`);
            if (locDesc) promptLines.push(`- ${t.placeholder_location_desc.split('...')[0]}: ${locDesc}.`);
            let locDetails = [];
            if(cuaca && cuaca !== 'manual') locDetails.push(`${t.select_weather.split(' ')[2]} ${cuaca}`);
            if(situasi && situasi !== 'manual') locDetails.push(`situasi ${situasi}`);
            if(nuansa && nuansa !== 'manual') locDetails.push(`dengan nuansa ${nuansa}`);
            if (locDetails.length > 0) promptLines.push(`- ${locDetails.join(', ')}.`);
        }

        // ADEGAN
        const sceneCards = document.querySelectorAll('.scene-card');
        const scenePromptLines = [];
        sceneCards.forEach((card, index) => {
            const sceneDesc = card.querySelector('textarea').value.trim();
            if (!sceneDesc) return;

            const sceneInputs = card.querySelectorAll('input');
            const sceneStart = sceneInputs[0].value;
            const sceneEnd = sceneInputs[1].value;
            const cameraAngle = card.querySelector('select').value;
            const angleStart = sceneInputs[2].value;
            const angleEnd = sceneInputs[3].value;
            
            const titleKey = card.querySelector('h4').getAttribute('data-lang-key');
            const titleIndex = card.querySelector('h4').getAttribute('data-lang-val');
            let sceneLine = `- ${t[titleKey]} ${titleIndex}: ${sceneDesc}`;

            if(sceneStart && sceneEnd) sceneLine += ` [${sceneStart}s-${sceneEnd}s]`;
            scenePromptLines.push(sceneLine + ".");

            let angleLineParts = [];
            if(cameraAngle) angleLineParts.push(`Camera Angle: ${cameraAngle}`);
            if(angleStart && angleEnd) angleLineParts.push(`[${angleStart}s-${angleEnd}s]`);
            if (angleLineParts.length > 0) scenePromptLines.push(`  - ${angleLineParts.join(' ')}.`);
        });

        if (scenePromptLines.length > 0) {
            promptLines.push(`\n${t.prompt_section_scene}:`);
            promptLines.push(...scenePromptLines);
        }
        
        // DETAIL TAMBAHAN
        const detailCard = document.querySelector('.card:nth-child(4)');
        const ekspresiDesc = detailCard.querySelector('div:nth-child(1) input[type="text"]').value.trim();
        const ekspresiChar = detailCard.querySelector('div:nth-child(1) select').value;
        const gesturDesc = detailCard.querySelector('div:nth-child(2) input[type="text"]').value.trim();
        const dialogText = detailCard.querySelector('div:nth-child(3) textarea').value.trim();
        const dialogLang = detailCard.querySelector('div:nth-child(3) select:nth-of-type(1)').value;
        const dialogChar = detailCard.querySelector('div:nth-child(3) select:nth-of-type(2)').value;
        const subId = detailCard.querySelector('input[value="sub-id"]').checked;
        const subEn = detailCard.querySelector('input[value="sub-en"]').checked;
        const hasDetails = ekspresiDesc || gesturDesc || dialogText || subId || subEn;

        if (hasDetails) {
            promptLines.push(`\n${t.prompt_section_details}:`);
        }

        if (ekspresiDesc && ekspresiChar) {
            promptLines.push(`- ${t.label_expression}: ${ekspresiChar} ${ekspresiDesc}.`);
        }
        if (gesturDesc) {
            promptLines.push(`- ${t.label_gesture}: ${gesturDesc}.`);
        }
        if (dialogText && dialogChar) {
            promptLines.push(`- ${t.label_dialogue} (${dialogLang}): ${dialogChar} says, "${dialogText}".`);
        }
        if (subId || subEn) {
            let subLangs = [];
            if(subId) subLangs.push(t.lang_indonesian);
            if(subEn) subLangs.push(t.lang_english);
            if(subLangs.length > 0) promptLines.push(`- ${t.label_subtitle}: Active (${subLangs.join(" & ")}).`);
        }

        outputPrompt.value = promptLines.join('\n');
    }

    // --- EVENT LISTENERS ---
    
    startBtn.addEventListener('click', () => {
        landingScreen.classList.add('hidden');
        appScreen.classList.remove('hidden');
    });

    addCharacterBtn.addEventListener('click', () => {
        if (characterCount >= 3) {
            alert(translations[currentLang].max_char_alert);
            return;
        }
        characterCount++;
        
        const newCharacterCard = characterCardTemplate.cloneNode(true);
        const titleEl = newCharacterCard.querySelector('h4');
        titleEl.textContent = `${translations[currentLang].character_card_title} ${characterCount}`;
        titleEl.setAttribute('data-lang-val', characterCount);
        
        newCharacterCard.querySelectorAll('input').forEach(input => input.value = '');
        characterContainer.appendChild(newCharacterCard);
        
        if (characterCount === 3) {
            addCharacterBtn.disabled = true;
            addCharacterBtn.classList.add('opacity-50', 'cursor-not-allowed');
        }
        applyTranslations(currentLang); // Re-apply translations for new placeholders
        updateCharacterDropdowns();
    });

    addSceneBtn.addEventListener('click', () => {
        if (sceneCount >= 5) {
            alert(translations[currentLang].max_scene_alert);
            return;
        }
        sceneCount++;
        
        const newSceneCard = sceneCardTemplate.cloneNode(true);
        const titleEl = newSceneCard.querySelector('h4');
        titleEl.textContent = `${translations[currentLang].scene_card_title} ${sceneCount}`;
        titleEl.setAttribute('data-lang-val', sceneCount);

        newSceneCard.querySelectorAll('input, textarea, select').forEach(el => {
            if (el.tagName === 'SELECT') el.selectedIndex = 0;
            else el.value = '';
        });
        sceneContainer.appendChild(newSceneCard);
        
        if (sceneCount === 5) {
            addSceneBtn.disabled = true;
            addSceneBtn.classList.add('opacity-50', 'cursor-not-allowed');
        }
        applyTranslations(currentLang);
    });
    
    characterContainer.addEventListener('keyup', (e) => {
        if (e.target.classList.contains('char-name')) {
            updateCharacterDropdowns();
        }
    });

    generateBtn.addEventListener('click', generatePrompt);

    copyBtn.addEventListener('click', () => {
        if (!outputPrompt.value) return;
        outputPrompt.select();
        try {
            document.execCommand('copy');
            copyFeedback.classList.remove('hidden');
            setTimeout(() => {
                copyFeedback.classList.add('hidden');
            }, 2000);
        } catch (err) {
            console.error('Failed to copy: ', err);
            alert(translations[currentLang].copy_fail_alert);
        }
        window.getSelection().removeAllRanges();
    });

    infoBtn.addEventListener('click', openInfoModal);
    closeInfoModalBtn.addEventListener('click', closeInfoModal);
    infoModal.addEventListener('click', (e) => {
        if (e.target === infoModal) closeInfoModal();
    });
    
    // Language modal listeners
    langBtnLanding.addEventListener('click', openLangModal); // This listener remains but button is hidden
    langBtnApp.addEventListener('click', openLangModal);
    closeLangModalBtn.addEventListener('click', closeLangModal);
    langModal.addEventListener('click', (e) => {
        if (e.target === langModal) closeLangModal();
    });
    setLangIdBtn.addEventListener('click', () => setLanguage('id'));
    setLangEnBtn.addEventListener('click', () => setLanguage('en'));

    // --- INITIALIZATION ---
    const savedLang = localStorage.getItem('surya-prompt-lang') || 'id';
    applyTranslations(savedLang);
    updateCharacterDropdowns();
});
</script>

</body>
</html>

