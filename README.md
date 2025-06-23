<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Surya.PromptGeneratorPRO</title>
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
        .form-textarea:disabled {
            background-color: #374151;
            cursor: not-allowed;
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
        .btn-red {
            background-color: #EF4444; /* bg-red-500 */
            color: white;
        }
        .btn-red:hover {
            background-color: #DC2626; /* bg-red-600 */
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
    </style>
</head>
<body class="bg-gray-900 text-white">

    <!-- Landing Screen -->
    <div id="landing-screen" class="min-h-screen flex flex-col items-center justify-center text-center p-4">
        <p class="text-xl md:text-2xl text-gray-300 mb-2">Kreasikan imajinasi dan idemu</p>
        <h1 class="text-4xl md:text-6xl font-black mb-8 bg-clip-text text-transparent bg-gradient-to-r from-green-400 to-blue-500">Surya.PromptGeneratorPRO</h1>
        <button id="start-btn" class="btn btn-green text-2xl shadow-lg transform hover:scale-105">
            <span>Mulai</span>
            <svg xmlns="http://www.w3.org/2000/svg" width="28" height="28" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="ml-3"><path d="M21 18V6a2 2 0 0 0-2-2H5a2 2 0 0 0-2 2v12a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2z"></path><path d="M9 10a2 2 0 1 1-4 0 2 2 0 0 1 4 0z"></path><path d="m21 14-4.2-4.2a2 2 0 0 0-2.82 0L8 16"></path></svg>
        </button>
    </div>

    <!-- Main App Screen (Initially Hidden) -->
    <div id="app-screen" class="hidden p-4 md:p-8 max-w-7xl mx-auto">
        <header class="flex justify-between items-center mb-8">
            <h2 class="text-3xl font-bold">Prompt Generator</h2>
        </header>

        <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
            <!-- Kolom Input -->
            <div id="input-column" class="space-y-6">
                <!-- Pengaturan Utama -->
                <div id="main-settings-card" class="card">
                    <h3 class="text-xl font-bold mb-4">Pengaturan Utama</h3>
                    <div class="space-y-4">
                        <div>
                            <label for="model-select" class="font-semibold mb-2 block">Model AI</label>
                            <select id="model-select" class="form-select">
                                <option>Gemini 1.5 Pro</option>
                                <option>Midjourney v6</option>
                                <option>DALL-E 3</option>
                                <option>Stable Diffusion XL</option>
                                <option>Google Veo</option>
                            </select>
                        </div>
                        <div>
                            <label for="style-input" class="font-semibold mb-2 block">Gaya Visual</label>
                            <input id="style-input" type="text" placeholder="Cth: Sinematik, Foto Realistis, Anime" class="form-input">
                        </div>
                    </div>
                </div>

                <!-- Karakter -->
                <div id="character-card" class="card">
                    <h3 class="text-xl font-bold mb-4">Karakter</h3>
                    <div id="character-container" class="space-y-4">
                        <div class="character-instance sub-card">
                            <h4 class="font-semibold mb-2 text-lg">Karakter 1</h4>
                            <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                                <input type="text" placeholder="Nama" class="form-input char-name">
                                <select class="form-select char-gender">
                                    <option value="">-- Pilih Gender --</option>
                                    <option>Pria</option>
                                    <option>Wanita</option>
                                </select>
                                <input type="number" placeholder="Umur" class="form-input">
                                <input type="text" placeholder="Tinggi (cth: 175cm)" class="form-input">
                                <input type="text" placeholder="Berat Badan (cth: 70kg)" class="form-input">
                                <input type="text" placeholder="Style & Warna Rambut" class="form-input">
                                <input type="text" placeholder="Warna Kulit (Rekomendasi Gemini)" class="form-input">
                                <input type="text" placeholder="Warna Mata" class="form-input">
                                <input type="text" placeholder="Sifat (Opsional)" class="form-input col-span-2">
                            </div>
                        </div>
                    </div>
                    <button id="add-character-btn" class="btn btn-blue mt-4">+ Tambah Karakter</button>
                </div>

                <!-- Lokasi -->
                <div id="location-card" class="card">
                    <h3 class="text-xl font-bold mb-4">Lokasi</h3>
                    <div class="space-y-4">
                        <textarea class="form-textarea" rows="3" placeholder="Deskripsikan detail tempat..."></textarea>
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                             <select class="form-select">
                                <option value="">-- Pilih Cuaca --</option>
                                <option>Cerah</option>
                                <option>Berawan</option>
                                <option>Hujan</option>
                                <option>Badai</option>
                                <option>Berkabut</option>
                                <option value="manual">Manual...</option>
                            </select>
                             <select class="form-select">
                                <option value="">-- Pilih Situasi Lokasi --</option>
                                <option>Ramai</option>
                                <option>Sepi</option>
                                <option>Normal</option>
                                <option>Kacau</option>
                                <option value="manual">Manual...</option>
                            </select>
                        </div>
                        <select class="form-select">
                            <option value="">-- Pilih Nuansa --</option>
                            <option>Harmonis</option>
                            <option>Tegang</option>
                            <option>Mencekam</option>
                            <option>Misterius</option>
                            <option>Romantis</option>
                            <option>Bahagia</option>
                            <option value="manual">Manual...</option>
                        </select>
                    </div>
                </div>
                
                <!-- Timeline Adegan -->
                <div id="timeline-card" class="card">
                    <h3 class="text-xl font-bold mb-4">Timeline Adegan</h3>
                    <div id="timeline-container" class="space-y-4">
                        <!-- Adegan instances will be added here -->
                    </div>
                    <button id="add-scene-btn" class="btn btn-blue mt-4">+ Tambah Adegan</button>
                </div>
                
                <!-- Dialog & Subtitle -->
                 <div id="dialogs-card" class="card">
                    <h3 class="text-xl font-bold mb-4">Dialog & Subtitle</h3>
                    <div class="space-y-4">
                        <!-- Dialog Container -->
                        <div id="dialog-section" class="p-2 border border-dashed border-gray-500 rounded-lg">
                            <label class="font-semibold">Dialog</label>
                            <div id="dialog-container" class="space-y-3 mt-2">
                                <!-- Dialog instances will be added here -->
                            </div>
                            <button id="add-dialog-btn" class="btn btn-blue mt-3 w-full text-sm">+ Tambah Dialog</button>
                        </div>
                        <!-- Subtitle Section -->
                        <div class="flex items-center justify-between p-2">
                            <label class="font-semibold">Subtitle</label>
                            <div class="flex items-center space-x-4">
                                <span>Indonesia</span>
                                <label class="relative inline-flex items-center cursor-pointer">
                                  <input type="checkbox" value="sub-id" class="sr-only peer" checked>
                                  <div class="w-11 h-6 bg-gray-600 peer-focus:outline-none rounded-full peer peer-checked:after:translate-x-full peer-checked:after:border-white after:content-[''] after:absolute after:top-[2px] after:left-[2px] after:bg-white after:border-gray-300 after:border after:rounded-full after:h-5 after:w-5 after:transition-all peer-checked:bg-blue-600"></div>
                                </label>
                                <span>Inggris</span>
                                 <label class="relative inline-flex items-center cursor-pointer">
                                  <input type="checkbox" value="sub-en" class="sr-only peer">
                                  <div class="w-11 h-6 bg-gray-600 peer-focus:outline-none rounded-full peer peer-checked:after:translate-x-full peer-checked:after:border-white after:content-[''] after:absolute after:top-[2px] after:left-[2px] after:bg-white after:border-gray-300 after:border after:rounded-full after:h-5 after:w-5 after:transition-all peer-checked:bg-blue-600"></div>
                                </label>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Audio & Backsound -->
                <div id="audio-card" class="card">
                    <h3 class="text-xl font-bold mb-4">Audio & Backsound</h3>
                    <div class="space-y-4">
                        <!-- Efek Suara (SFX) -->
                        <div class="p-2 border border-dashed border-gray-500 rounded-lg">
                            <div class="flex justify-between items-center mb-2">
                                <label class="font-semibold">Efek Suara (SFX)</label>
                                <div class="flex items-center space-x-2">
                                    <label for="sfx-auto" class="text-sm">Otomatis</label>
                                    <input type="checkbox" id="sfx-auto" class="sfx-auto-checkbox h-5 w-5 rounded bg-gray-800 border-gray-600 text-blue-500 focus:ring-blue-600">
                                </div>
                            </div>
                            <textarea class="sfx-desc-textarea form-textarea" rows="2" placeholder="Deskripsikan efek suara yang diinginkan... (Cth: suara langkah kaki, kicau burung, angin berdesir)"></textarea>
                        </div>
                        <!-- Musik Latar (Backsound) -->
                        <div class="p-2 border border-dashed border-gray-500 rounded-lg">
                            <div class="flex justify-between items-center mb-2">
                                <label class="font-semibold">Musik Latar (Backsound)</label>
                                <div class="flex items-center space-x-2">
                                    <label for="music-auto" class="text-sm">Otomatis</label>
                                    <input type="checkbox" id="music-auto" class="music-auto-checkbox h-5 w-5 rounded bg-gray-800 border-gray-600 text-blue-500 focus:ring-blue-600">
                                </div>
                            </div>
                            <textarea class="music-desc-textarea form-textarea" rows="2" placeholder="Deskripsikan genre atau nuansa musik... (Cth: musik orkestra tegang, lo-fi santai, gamelan jawa)"></textarea>
                        </div>
                    </div>
                </div>
                
                <!-- Info Card -->
                <div id="info-card" class="card">
                    <h3 class="text-xl font-bold mb-4">Info Pembuat</h3>
                    <p class="text-gray-300 mb-4">Aplikasi ini dibuat oleh Surya Ishwara.</p>
                    <div class="space-y-3">
                        <a href="https://www.tiktok.com/@surya.ishwara" target="_blank" class="btn btn-blue w-full">
                            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="mr-2"><path d="M16 8a6 6 0 0 1 6 6v7h-4v-7a2 2 0 0 0-2-2 2 2 0 0 0-2 2v7h-4v-7a6 6 0 0 1 6-6z"></path><rect x="2" y="9" width="4" height="12"></rect><circle cx="4" cy="4" r="2"></circle></svg>
                            Kunjungi TikTok
                        </a>
                         <a href="https://www.facebook.com/surya.ishwara" target="_blank" class="btn btn-blue w-full">
                            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="mr-2"><path d="M18 2h-3a5 5 0 0 0-5 5v3H7v4h3v8h4v-8h3l1-4h-4V7a1 1 0 0 1 1-1h3z"></path></svg>
                            Kunjungi Facebook
                        </a>
                         <a href="https://www.youtube.com/@surya.ishwara" target="_blank" class="btn btn-blue w-full">
                           <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="mr-2"><path d="M22.54 6.42a2.78 2.78 0 0 0-1.94-2C18.88 4 12 4 12 4s-6.88 0-8.6.46a2.78 2.78 0 0 0-1.94 2A29 29 0 0 0 1 11.75a29 29 0 0 0 .46 5.33A2.78 2.78 0 0 0 3.4 19c1.72.46 8.6.46 8.6.46s6.88 0 8.6-.46a2.78 2.78 0 0 0 1.94-2 29 29 0 0 0 .46-5.25 29 29 0 0 0-.46-5.33z"></path><polygon points="9.75 15.02 15.5 11.75 9.75 8.48 9.75 15.02"></polygon></svg>
                            Kunjungi YouTube
                        </a>
                    </div>
                </div>
            </div>

            <!-- Kolom Output -->
            <div class="space-y-6">
                <div class="card sticky top-8">
                    <button id="generate-btn" class="btn btn-green w-full text-lg mb-4">
                        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="mr-2"><path d="M12 2a10 10 0 1 0 10 10A10 10 0 0 0 12 2v0a10 10 0 0 0-1.08 3.9M12 2a10 10 0 0 1 10 10M12 2v10m0 0a10 10 0 0 1-10 10m10-10a10 10 0 0 0 10 10m-10-10L2 12m10 10 10-10"></path></svg>
                        <span>Generate Prompt</span>
                    </button>
                    <h3 class="text-xl font-bold mb-4">Hasil Prompt</h3>
                    <div class="relative">
                        <textarea id="output-prompt" class="form-textarea h-96" rows="20" readonly placeholder="Hasil prompt akan muncul di sini..."></textarea>
                        <button id="copy-btn" class="btn btn-blue absolute top-3 right-3 px-3 py-2">
                             <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect x="9" y="9" width="13" height="13" rx="2" ry="2"></rect><path d="M5 15H4a2 2 0 0 1-2-2V4a2 2 0 0 1 2-2h9a2 2 0 0 1 2 2v1"></path></svg>
                        </button>
                    </div>
                    <div id="copy-feedback" class="hidden mt-2 text-center text-green-400 font-semibold flex items-center justify-center">
                        <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="3" stroke-linecap="round" stroke-linejoin="round" class="mr-2"><polyline points="20 6 9 17 4 12"></polyline></svg>
                        <span>Copy sukses!</span>
                    </div>
                </div>
            </div>
        </div>
    </div>
    
    <!-- TEMPLATES -->
    <template id="scene-template">
        <div class="scene-instance sub-card space-y-4">
            <div class="flex justify-between items-start">
                <h4 class="font-semibold text-lg">Adegan</h4>
                <button type="button" class="remove-scene-btn btn btn-red btn-sm !p-1 !rounded-full w-6 h-6">
                    <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="3" stroke-linecap="round" stroke-linejoin="round"><line x1="18" y1="6" x2="6" y2="18"></line><line x1="6" y1="6" x2="18" y2="18"></line></svg>
                </button>
            </div>
            <textarea class="scene-desc form-textarea" rows="3" placeholder="Deskripsikan adegan utamanya di sini..."></textarea>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                <input type="number" class="scene-start form-input" placeholder="Detik Mulai Adegan">
                <input type="number" class="scene-end form-input" placeholder="Detik Akhir Adegan">
            </div>
            <div class="details-container border-t border-gray-600 pt-4 mt-4 space-y-3">
                <!-- Detail instances (camera, gesture, etc.) will be added here -->
            </div>
            <button class="add-detail-btn btn btn-gray w-full text-sm">+ Tambah Detail di Adegan</button>
        </div>
    </template>

    <template id="detail-template">
        <div class="detail-instance p-2 border border-gray-600 rounded-lg space-y-2">
             <div class="flex justify-between items-center">
                <select class="detail-type-select form-select w-2/5">
                    <option value="camera">Angle Kamera</option>
                    <option value="expression">Ekspresi</option>
                    <option value="gesture">Gestur</option>
                </select>
                <button type="button" class="remove-detail-btn btn btn-red btn-sm !p-1 !rounded-full w-6 h-6">
                    <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="3" stroke-linecap="round" stroke-linejoin="round"><line x1="18" y1="6" x2="6" y2="18"></line><line x1="6" y1="6" x2="18" y2="18"></line></svg>
                </button>
            </div>
            <div class="detail-fields">
                <!-- Contextual fields will be injected here -->
            </div>
        </div>
    </template>
    
    <template id="dialog-template">
        <div class="dialog-instance p-2 border border-gray-700 rounded-lg">
            <div class="flex justify-end mb-2">
                <button type="button" class="remove-dialog-btn btn btn-red btn-sm !p-1 !rounded-full w-6 h-6">
                    <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="3" stroke-linecap="round" stroke-linejoin="round"><line x1="18" y1="6" x2="6" y2="18"></line><line x1="6" y1="6" x2="18" y2="18"></line></svg>
                </button>
            </div>
            <textarea class="dialog-text form-textarea" rows="2" placeholder="Isi dialog..."></textarea>
            <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mt-2">
                <select class="form-select dialog-lang">
                    <option value="Indonesia">Bahasa Indonesia</option>
                    <option value="Inggris">Bahasa Inggris</option>
                </select>
                <select class="form-select dialog-char-select"><option value="">-- Pilih Karakter --</option></select>
                <select class="form-select dialog-tone">
                    <option value="">-- Nada Suara --</option>
                    <option>Biasa</option>
                    <option>Senang</option>
                    <option>Sedih</option>
                    <option>Marah</option>
                    <option>Berbisik</option>
                    <option>Tegas</option>
                    <option>Bingung</option>
                </select>
            </div>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mt-2">
                <input type="number" placeholder="Detik Mulai" class="form-input">
                <input type="number" placeholder="Detik Akhir" class="form-input">
            </div>
        </div>
    </template>

<script>
document.addEventListener('DOMContentLoaded', () => {
    // --- ELEMENT SELECTIONS ---
    const landingScreen = document.getElementById('landing-screen');
    const appScreen = document.getElementById('app-screen');
    const startBtn = document.getElementById('start-btn');

    // Character elements
    const addCharacterBtn = document.getElementById('add-character-btn');
    const characterContainer = document.getElementById('character-container');
    const characterCardTemplate = characterContainer.querySelector('.character-instance').cloneNode(true);
    let characterCount = 1;

    // Timeline/Scene elements
    const addSceneBtn = document.getElementById('add-scene-btn');
    const timelineContainer = document.getElementById('timeline-container');
    const sceneTemplate = document.getElementById('scene-template');
    const detailTemplate = document.getElementById('detail-template');
    
    // Dialog elements
    const addDialogBtn = document.getElementById('add-dialog-btn');
    const dialogContainer = document.getElementById('dialog-container');
    const dialogTemplate = document.getElementById('dialog-template');

    // Audio elements
    const audioCard = document.getElementById('audio-card');

    // Output elements
    const generateBtn = document.getElementById('generate-btn');
    const outputPrompt = document.getElementById('output-prompt');
    const copyBtn = document.getElementById('copy-btn');
    const copyFeedback = document.getElementById('copy-feedback');
    
    // Input Card Wrappers
    const mainSettingsCard = document.getElementById('main-settings-card');
    const characterCard = document.getElementById('character-card');
    const locationCard = document.getElementById('location-card');
    const dialogsCard = document.getElementById('dialogs-card');

    // --- EVENT LISTENERS ---
    
    startBtn.addEventListener('click', () => {
        landingScreen.classList.add('hidden');
        appScreen.classList.remove('hidden');
    });

    addCharacterBtn.addEventListener('click', () => {
        if (characterCount >= 3) {
            alert("Maksimal 3 karakter.");
            return;
        }
        characterCount++;
        
        const newCharacterCard = characterCardTemplate.cloneNode(true);
        newCharacterCard.querySelector('h4').textContent = `Karakter ${characterCount}`;
        newCharacterCard.querySelectorAll('input, select').forEach(el => {
            if(el.tagName === 'SELECT') el.selectedIndex = 0;
            else el.value = '';
        });
        characterContainer.appendChild(newCharacterCard);
        
        if (characterCount === 3) {
            addCharacterBtn.disabled = true;
            addCharacterBtn.classList.add('opacity-50', 'cursor-not-allowed');
        }
        updateCharacterDropdowns();
    });

    addSceneBtn.addEventListener('click', () => {
        const sceneCount = timelineContainer.children.length;
        if (sceneCount >= 10) { // Example limit
            alert("Maksimal 10 adegan.");
            return;
        }
        const newScene = sceneTemplate.content.cloneNode(true);
        newScene.querySelector('h4').textContent = `Adegan ${sceneCount + 1}`;
        timelineContainer.appendChild(newScene);
    });

    timelineContainer.addEventListener('click', e => {
        if (e.target.closest('.remove-scene-btn')) {
            e.target.closest('.scene-instance').remove();
            // Re-number scenes
            timelineContainer.querySelectorAll('h4').forEach((h4, index) => {
                h4.textContent = `Adegan ${index + 1}`;
            });
        }
        if (e.target.closest('.add-detail-btn')) {
            const detailsContainer = e.target.closest('.scene-instance').querySelector('.details-container');
            const newDetail = detailTemplate.content.cloneNode(true);
            detailsContainer.appendChild(newDetail);
            // Manually trigger change event to load initial fields
            const newSelect = detailsContainer.lastElementChild.querySelector('.detail-type-select');
            newSelect.dispatchEvent(new Event('change'));
        }
        if(e.target.closest('.remove-detail-btn')) {
            e.target.closest('.detail-instance').remove();
        }
    });

    timelineContainer.addEventListener('change', e => {
        if (e.target.classList.contains('detail-type-select')) {
            const detailFieldsContainer = e.target.closest('.detail-instance').querySelector('.detail-fields');
            const type = e.target.value;
            renderDetailFields(detailFieldsContainer, type);
        }
    });
    
    addDialogBtn.addEventListener('click', () => {
        const newDialog = dialogTemplate.content.cloneNode(true);
        dialogContainer.appendChild(newDialog);
        updateCharacterDropdowns();
    });

    dialogContainer.addEventListener('click', (e) => {
        if (e.target.closest('.remove-dialog-btn')) {
            e.target.closest('.dialog-instance').remove();
        }
    });

    characterContainer.addEventListener('keyup', (e) => {
        if (e.target.classList.contains('char-name')) {
            updateCharacterDropdowns();
        }
    });
    
    audioCard.addEventListener('change', (e) => {
        if (e.target.classList.contains('sfx-auto-checkbox')) {
            const textarea = audioCard.querySelector('.sfx-desc-textarea');
            textarea.disabled = e.target.checked;
            if (e.target.checked) textarea.value = '';
        }
        if (e.target.classList.contains('music-auto-checkbox')) {
            const textarea = audioCard.querySelector('.music-desc-textarea');
            textarea.disabled = e.target.checked;
            if (e.target.checked) textarea.value = '';
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
            console.error('Gagal menyalin: ', err);
            alert('Gagal menyalin teks.');
        }
        window.getSelection().removeAllRanges();
    });

    // --- FUNCTIONS ---

    function renderDetailFields(container, type) {
        container.innerHTML = ''; // Clear previous fields
        let fieldsHtml = `
            <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mt-2">
                <input type="number" class="detail-start form-input" placeholder="Detik Mulai">
                <input type="number" class="detail-end form-input" placeholder="Detik Akhir">
            </div>`;

        if (type === 'camera') {
            fieldsHtml = `
                <select class="detail-value form-select mt-2">
                    <option>Eye Level</option>
                    <option>High Angle</option>
                    <option>Low Angle</option>
                    <option>Dutch Angle</option>
                    <option>Over the Shoulder</option>
                    <option>Point of View (POV)</option>
                    <option>Wide Shot</option>
                    <option>Medium Shot</option>
                    <option>Close Up</option>
                    <option>Extreme Close Up</option>
                </select>
            ` + fieldsHtml;
        } else if (type === 'expression') {
            fieldsHtml = `
                <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mt-2">
                    <input type="text" class="detail-desc form-input" placeholder="Deskripsi Ekspresi">
                    <select class="detail-char-select form-select expression-char-select"></select>
                </div>
            ` + fieldsHtml;
        } else if (type === 'gesture') {
            fieldsHtml = `
                <input type="text" class="detail-desc form-input mt-2" placeholder="Deskripsi Gestur">
            ` + fieldsHtml;
        }
        container.innerHTML = fieldsHtml;
        updateCharacterDropdowns();
    }
    
    function updateCharacterDropdowns() {
        const charNames = Array.from(document.querySelectorAll('.char-name'))
                               .map((input, index) => input.value.trim() || `Karakter Tanpa Nama ${index + 1}`);

        const allCharSelects = document.querySelectorAll('.expression-char-select, .dialog-char-select');

        allCharSelects.forEach(select => {
            const currentVal = select.value;
            select.innerHTML = '<option value="">-- Pilih Karakter --</option>';
            charNames.forEach(name => {
                const option = document.createElement('option');
                option.value = name;
                option.textContent = name;
                select.appendChild(option);
            });
            select.value = currentVal;
        });
    }
    
    function generatePrompt() {
        let promptLines = [];
        
        // --- PENGATURAN UTAMA ---
        const model = mainSettingsCard.querySelector('#model-select').value;
        const style = mainSettingsCard.querySelector('#style-input').value.trim();
        promptLines.push(`Buat prompt untuk model ${model}.`);
        if (style) {
            promptLines.push(`Gaya visual: ${style}.`);
        }
        promptLines.push("---");

        // --- KARAKTER ---
        const characterInstances = characterCard.querySelectorAll('.character-instance');
        if (characterInstances.length > 0 && characterInstances[0].querySelector('.char-name').value.trim()) {
            promptLines.push("KARAKTER:");
            characterInstances.forEach((card, index) => {
                const inputs = card.querySelectorAll('input');
                const gender = card.querySelector('.char-gender').value;

                let charDetails = `- Karakter ${index + 1}:`;
                const details = [
                    inputs[0].value.trim() ? `Nama: ${inputs[0].value.trim()}` : null,
                    gender ? `Gender: ${gender}`: null,
                    inputs[1].value.trim() ? `Umur: ${inputs[1].value.trim()}` : null,
                    inputs[2].value.trim() ? `Tinggi: ${inputs[2].value.trim()}` : null,
                    inputs[3].value.trim() ? `Berat: ${inputs[3].value.trim()}` : null,
                    inputs[4].value.trim() ? `Rambut: ${inputs[4].value.trim()}` : null,
                    inputs[5].value.trim() ? `Kulit: ${inputs[5].value.trim()}` : null,
                    inputs[6].value.trim() ? `Mata: ${inputs[6].value.trim()}` : null,
                    inputs[7].value.trim() ? `Sifat: ${inputs[7].value.trim()}` : null,
                ].filter(Boolean);
                
                if (details.length > 0) {
                     promptLines.push(`${charDetails} ${details.join(', ')}.`);
                }
            });
        }

        // --- LOKASI ---
        const locDesc = locationCard.querySelector('textarea').value.trim();
        const locSelects = locationCard.querySelectorAll('select');
        const cuaca = locSelects[0].value;
        const situasi = locSelects[1].value;
        const nuansa = locSelects[2].value;

        if (locDesc || cuaca || situasi || nuansa) {
            promptLines.push("\nLOKASI:");
            if (locDesc) promptLines.push(`- Deskripsi: ${locDesc}.`);
            let details = [];
            if(cuaca && cuaca !== 'manual') details.push(`Cuaca ${cuaca}`);
            if(situasi && situasi !== 'manual') details.push(`situasi ${situasi}`);
            if(nuansa && nuansa !== 'manual') details.push(`dengan nuansa ${nuansa}`);
            if (details.length > 0) promptLines.push(`- ${details.join(', ')}.`);
        }

        // --- TIMELINE ADEGAN ---
        const sceneInstances = timelineContainer.querySelectorAll('.scene-instance');
        if (sceneInstances.length > 0) {
            promptLines.push('\nTIMELINE ADEGAN:');
            sceneInstances.forEach((scene, index) => {
                const sceneDesc = scene.querySelector('.scene-desc').value.trim();
                const sceneStart = scene.querySelector('.scene-start').value;
                const sceneEnd = scene.querySelector('.scene-end').value;
                let sceneHeader = `- Adegan ${index + 1}`;
                if (sceneStart && sceneEnd) sceneHeader += ` [${sceneStart}s-${sceneEnd}s]`;
                sceneHeader += sceneDesc ? `: ${sceneDesc}` : '';
                promptLines.push(sceneHeader);

                const detailInstances = scene.querySelectorAll('.detail-instance');
                detailInstances.forEach(detail => {
                    const type = detail.querySelector('.detail-type-select').value;
                    const start = detail.querySelector('.detail-start').value;
                    const end = detail.querySelector('.detail-end').value;
                    let detailLine = '  - ';
                    if (start && end) detailLine += `[${start}s-${end}s] `;

                    if (type === 'camera') {
                        const value = detail.querySelector('.detail-value').value;
                        detailLine += `Angle Kamera: ${value}.`;
                    } else if (type === 'expression') {
                        const desc = detail.querySelector('.detail-desc').value.trim();
                        const char = detail.querySelector('.detail-char-select').value;
                        if(desc && char) detailLine += `Ekspresi: ${char} ${desc}.`;
                    } else if (type === 'gesture') {
                        const desc = detail.querySelector('.detail-desc').value.trim();
                        if(desc) detailLine += `Gestur: ${desc}.`;
                    }
                    if(detailLine.length > 5) promptLines.push(detailLine);
                });
            });
        }
        
        // --- DIALOG & SUBTITLE ---
        const dialogLines = [];
        const dialogInstances = dialogsCard.querySelectorAll('.dialog-instance');
        dialogInstances.forEach(dialog => {
            const dialogText = dialog.querySelector('.dialog-text').value.trim();
            const dialogLang = dialog.querySelector('.dialog-lang').value;
            const dialogChar = dialog.querySelector('.dialog-char-select').value;
            const dialogTone = dialog.querySelector('.dialog-tone').value;
            
            if (dialogText && dialogChar) {
                let dialogLine = `- (${dialogLang}) ${dialogChar} berkata`;
                if (dialogTone && dialogTone !== 'Biasa') {
                    dialogLine += ` dengan nada ${dialogTone.toLowerCase()}`;
                }
                dialogLine += `, "${dialogText}".`;
                dialogLines.push(dialogLine);
            }
        });
        
        const subId = dialogsCard.querySelector('input[value="sub-id"]').checked;
        const subEn = dialogsCard.querySelector('input[value="sub-en"]').checked;
        if (subId || subEn) {
            let subLangs = [];
            if(subId) subLangs.push("Indonesia");
            if(subEn) subLangs.push("Inggris");
            if(subLangs.length > 0) dialogLines.push(`- Subtitle: Aktif (${subLangs.join(" & ")}).`);
        }
        
        if (dialogLines.length > 0) {
            promptLines.push("\nDIALOG & SUBTITLE:");
            promptLines.push(...dialogLines);
        }
        
        // --- AUDIO & BACKSOUND ---
        const sfxAuto = audioCard.querySelector('.sfx-auto-checkbox').checked;
        const sfxDesc = audioCard.querySelector('.sfx-desc-textarea').value.trim();
        const musicAuto = audioCard.querySelector('.music-auto-checkbox').checked;
        const musicDesc = audioCard.querySelector('.music-desc-textarea').value.trim();

        const audioLines = [];

        if (sfxAuto) {
            audioLines.push(`- Efek Suara (SFX): Rekomendasi otomatis sesuai adegan.`);
        } else if (sfxDesc) {
            audioLines.push(`- Efek Suara (SFX): ${sfxDesc}.`);
        }

        if (musicAuto) {
            audioLines.push(`- Musik Latar: Rekomendasi otomatis sesuai nuansa.`);
        } else if (musicDesc) {
            audioLines.push(`- Musik Latar: ${musicDesc}.`);
        }

        if (audioLines.length > 0) {
            promptLines.push("\nAUDIO & BACKSOUND:");
            promptLines.push(...audioLines);
        }

        outputPrompt.value = promptLines.join('\n');
    }
    
    // Initial call to populate dropdowns for the first character & add one dialog/scene box
    addDialogBtn.click();
    addSceneBtn.click();
    updateCharacterDropdowns();
});
</script>

</body>
</html>

