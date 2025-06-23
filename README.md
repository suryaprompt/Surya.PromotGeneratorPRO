<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Surya.PromptGeneratorPRO</title>
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
        /* Style for sub-cards like character and scene cards */
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
            Mulai
            <svg xmlns="http://www.w3.org/2000/svg" width="28" height="28" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="ml-3"><path d="M21 18V6a2 2 0 0 0-2-2H5a2 2 0 0 0-2 2v12a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2z"></path><path d="M9 10a2 2 0 1 1-4 0 2 2 0 0 1 4 0z"></path><path d="m21 14-4.2-4.2a2 2 0 0 0-2.82 0L8 16"></path></svg>
        </button>
    </div>

    <!-- Main App Screen -->
    <div id="app-screen" class="hidden p-4 md:p-8 max-w-7xl mx-auto">
        <header class="flex justify-between items-center mb-8">
            <h2 class="text-3xl font-bold">Prompt Generator</h2>
            <button id="info-btn" class="btn btn-gray">
                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="mr-2"><circle cx="12" cy="12" r="10"></circle><line x1="12" y1="16" x2="12" y2="12"></line><line x1="12" y1="8" x2="12.01" y2="8"></line></svg>
                Info
            </button>
        </header>

        <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
            <!-- Kolom Input -->
            <div class="space-y-6">
                <!-- Karakter -->
                <div class="card">
                    <h3 class="text-xl font-bold mb-4">Karakter</h3>
                    <div id="character-container" class="space-y-4">
                        <!-- Character 1 is here by default -->
                        <div class="character-card sub-card">
                            <h4 class="font-semibold mb-2 text-lg">Karakter 1</h4>
                            <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                                <input type="text" placeholder="Nama" class="form-input char-name">
                                <input type="number" placeholder="Umur" class="form-input">
                                <input type="text" placeholder="Tinggi (cth: 175cm)" class="form-input">
                                <input type="text" placeholder="Berat Badan (cth: 70kg)" class="form-input">
                                <input type="text" placeholder="Style & Warna Rambut" class="form-input">
                                <input type="text" placeholder="Warna Kulit (Rekomendasi Gemini)" class="form-input">
                                <input type="text" placeholder="Warna Mata" class="form-input">
                                <input type="text" placeholder="Sifat (Opsional)" class="form-input">
                            </div>
                        </div>
                    </div>
                    <button id="add-character-btn" class="btn btn-blue mt-4">+ Tambah Karakter</button>
                </div>

                <!-- Lokasi -->
                <div class="card">
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
                
                <!-- Adegan -->
                <div class="card">
                    <h3 class="text-xl font-bold mb-4">Adegan</h3>
                    <div id="scene-container" class="space-y-4">
                        <!-- Scene 1 is here by default -->
                        <div class="scene-card sub-card">
                             <h4 class="font-semibold mb-2 text-lg">Adegan 1</h4>
                             <div class="space-y-4">
                                <textarea class="form-textarea" rows="3" placeholder="Deskripsikan adegan..."></textarea>
                                <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                                    <input type="number" placeholder="Detik Mulai Adegan" class="form-input">
                                    <input type="number" placeholder="Detik Akhir Adegan" class="form-input">
                                </div>
                                <select class="form-select">
                                    <option value="">-- Pilih Angle Kamera --</option>
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
                                    <option value="rekomendasi">Rekomendasi Sesuai Adegan</option>
                                </select>
                                 <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                                    <input type="number" placeholder="Detik Mulai Angle" class="form-input">
                                    <input type="number" placeholder="Detik Akhir Angle" class="form-input">
                                </div>
                            </div>
                        </div>
                    </div>
                     <button id="add-scene-btn" class="btn btn-blue mt-4">+ Tambah Adegan</button>
                </div>

                <!-- Ekspresi, Gestur, Dialog & Subtitle -->
                 <div class="card">
                    <h3 class="text-xl font-bold mb-4">Detail Tambahan</h3>
                    <div class="space-y-4">
                        <!-- Ekspresi -->
                        <div class="p-2 border border-dashed border-gray-500 rounded-lg">
                            <label class="font-semibold">Ekspresi</label>
                            <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mt-2">
                                <input type="text" placeholder="Deskripsi Ekspresi (cth: tersenyum tipis)" class="form-input">
                                <select class="form-select expression-char-select"></select>
                            </div>
                            <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mt-2">
                                <input type="number" placeholder="Detik Mulai" class="form-input">
                                <input type="number" placeholder="Detik Akhir" class="form-input">
                            </div>
                        </div>
                        <!-- Gestur -->
                        <div class="p-2 border border-dashed border-gray-500 rounded-lg">
                            <label class="font-semibold">Gestur</label>
                            <input type="text" placeholder="Deskripsi Gestur (cth: mengangkat tangan)" class="form-input mt-2">
                            <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mt-2">
                                <input type="number" placeholder="Detik Mulai" class="form-input">
                                <input type="number" placeholder="Detik Akhir" class="form-input">
                            </div>
                        </div>
                        <!-- Dialog -->
                        <div class="p-2 border border-dashed border-gray-500 rounded-lg">
                            <label class="font-semibold">Dialog</label>
                            <textarea class="form-textarea mt-2" rows="2" placeholder="Isi dialog..."></textarea>
                            <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mt-2">
                                <select class="form-select">
                                    <option value="Indonesia">Bahasa Indonesia</option>
                                    <option value="Inggris">Bahasa Inggris</option>
                                </select>
                                <select class="form-select dialog-char-select"></select>
                            </div>
                             <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mt-2">
                                <input type="number" placeholder="Detik Mulai" class="form-input">
                                <input type="number" placeholder="Detik Akhir" class="form-input">
                            </div>
                        </div>
                        <!-- Subtitle -->
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
            </div>

            <!-- Kolom Output -->
            <div class="space-y-6">
                <div class="card sticky top-8">
                    <button id="generate-btn" class="btn btn-green w-full text-lg mb-4">
                        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="mr-2"><path d="M12 2a10 10 0 1 0 10 10A10 10 0 0 0 12 2v0a10 10 0 0 0-1.08 3.9M12 2a10 10 0 0 1 10 10M12 2v10m0 0a10 10 0 0 1-10 10m10-10a10 10 0 0 0 10 10m-10-10L2 12m10 10 10-10"></path></svg>
                        Generate Prompt
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
                        Copy sukses!
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Info Modal -->
    <div id="info-modal" class="hidden fixed inset-0 bg-black bg-opacity-75 flex items-center justify-center p-4 z-50">
        <div class="bg-gray-800 rounded-lg p-8 max-w-sm w-full text-center relative">
            <button id="close-modal-btn" class="absolute top-3 right-3 text-gray-400 hover:text-white">
                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><line x1="18" y1="6" x2="6" y2="18"></line><line x1="6" y1="6" x2="18" y2="18"></line></svg>
            </button>
            <h3 class="text-2xl font-bold mb-4">Info Pembuat</h3>
            <p class="text-gray-300 mb-4">Aplikasi ini dibuat oleh Surya Ishwara.</p>
            <a href="https://www.tiktok.com/@surya.ishwara" target="_blank" class="btn btn-blue w-full">
                Kunjungi TikTok @surya.ishwara
            </a>
        </div>
    </div>


<script>
document.addEventListener('DOMContentLoaded', () => {
    // --- Element Selections ---
    const landingScreen = document.getElementById('landing-screen');
    const appScreen = document.getElementById('app-screen');
    const startBtn = document.getElementById('start-btn');

    // Character elements
    const addCharacterBtn = document.getElementById('add-character-btn');
    const characterContainer = document.getElementById('character-container');
    const characterCardTemplate = characterContainer.querySelector('.character-card').cloneNode(true);
    let characterCount = 1;

    // Scene elements
    const addSceneBtn = document.getElementById('add-scene-btn');
    const sceneContainer = document.getElementById('scene-container');
    const sceneCardTemplate = sceneContainer.querySelector('.scene-card').cloneNode(true);
    let sceneCount = 1;
    
    // Output elements
    const generateBtn = document.getElementById('generate-btn');
    const outputPrompt = document.getElementById('output-prompt');
    const copyBtn = document.getElementById('copy-btn');
    const copyFeedback = document.getElementById('copy-feedback');

    // Modal elements
    const infoBtn = document.getElementById('info-btn');
    const infoModal = document.getElementById('info-modal');
    const closeModalBtn = document.getElementById('close-modal-btn');

    // --- Event Listeners ---
    
    // Switch from landing to main app
    startBtn.addEventListener('click', () => {
        landingScreen.classList.add('hidden');
        appScreen.classList.remove('hidden');
    });

    // Add new character
    addCharacterBtn.addEventListener('click', () => {
        if (characterCount >= 3) {
            alert("Maksimal 3 karakter.");
            return;
        }
        characterCount++;
        
        const newCharacterCard = characterCardTemplate.cloneNode(true);
        newCharacterCard.querySelector('h4').textContent = `Karakter ${characterCount}`;
        newCharacterCard.querySelectorAll('input').forEach(input => input.value = ''); // Clear fields
        characterContainer.appendChild(newCharacterCard);
        
        if (characterCount === 3) {
            addCharacterBtn.disabled = true;
            addCharacterBtn.classList.add('opacity-50', 'cursor-not-allowed');
        }
        updateCharacterDropdowns();
    });

    // Add new scene
    addSceneBtn.addEventListener('click', () => {
        if (sceneCount >= 5) { // Set max scenes to 5
            alert("Maksimal 5 adegan.");
            return;
        }
        sceneCount++;
        
        const newSceneCard = sceneCardTemplate.cloneNode(true);
        newSceneCard.querySelector('h4').textContent = `Adegan ${sceneCount}`;
        newSceneCard.querySelectorAll('input, textarea, select').forEach(el => {
            if (el.tagName === 'SELECT') el.selectedIndex = 0;
            else el.value = '';
        });
        sceneContainer.appendChild(newSceneCard);
        
        if (sceneCount === 5) {
            addSceneBtn.disabled = true;
            addSceneBtn.classList.add('opacity-50', 'cursor-not-allowed');
        }
    });
    
    // Listen for character name changes to update dropdowns
    characterContainer.addEventListener('keyup', (e) => {
        if (e.target.classList.contains('char-name')) {
            updateCharacterDropdowns();
        }
    });

    // Generate Prompt
    generateBtn.addEventListener('click', generatePrompt);

    // Copy to clipboard
    copyBtn.addEventListener('click', () => {
        if (!outputPrompt.value) return;
        // Using document.execCommand for better iframe compatibility
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
        // Deselect text
        window.getSelection().removeAllRanges();
    });

    // Modal controls
    infoBtn.addEventListener('click', () => infoModal.classList.remove('hidden'));
    closeModalBtn.addEventListener('click', () => infoModal.classList.add('hidden'));
    infoModal.addEventListener('click', (e) => {
        if (e.target === infoModal) {
            infoModal.classList.add('hidden');
        }
    });

    // --- Functions ---
    
    function updateCharacterDropdowns() {
        const charNames = Array.from(document.querySelectorAll('.char-name'))
                               .map((input, index) => input.value.trim() || `Karakter Tanpa Nama ${index + 1}`);

        const expressionSelects = document.querySelectorAll('.expression-char-select');
        const dialogSelects = document.querySelectorAll('.dialog-char-select');

        [...expressionSelects, ...dialogSelects].forEach(select => {
            const currentVal = select.value;
            select.innerHTML = '<option value="">-- Pilih Karakter --</option>'; // Clear existing
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
        
        // --- KARAKTER ---
        const characterCards = document.querySelectorAll('.character-card');
        if (characterCards.length > 0 && characterCards[0].querySelector('.char-name').value.trim()) {
            promptLines.push("KARAKTER:");
            characterCards.forEach((card, index) => {
                const fields = card.querySelectorAll('input');
                let charDetails = `- Karakter ${index + 1}:`;
                const details = [
                    fields[0].value.trim() ? `Nama: ${fields[0].value.trim()}` : null,
                    fields[1].value.trim() ? `Umur: ${fields[1].value.trim()}` : null,
                    fields[2].value.trim() ? `Tinggi: ${fields[2].value.trim()}` : null,
                    fields[3].value.trim() ? `Berat: ${fields[3].value.trim()}` : null,
                    fields[4].value.trim() ? `Rambut: ${fields[4].value.trim()}` : null,
                    fields[5].value.trim() ? `Kulit: ${fields[5].value.trim()}` : null,
                    fields[6].value.trim() ? `Mata: ${fields[6].value.trim()}` : null,
                    fields[7].value.trim() ? `Sifat: ${fields[7].value.trim()}` : null,
                ].filter(Boolean); // Filter out empty details
                
                if (details.length > 0) {
                     promptLines.push(`${charDetails} ${details.join(', ')}.`);
                }
            });
        }

        // --- LOKASI ---
        const locCard = document.querySelector('.card:nth-child(2)');
        const locDesc = locCard.querySelector('textarea').value.trim();
        const locSelects = locCard.querySelectorAll('select');
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

        // --- ADEGAN ---
        const sceneCards = document.querySelectorAll('.scene-card');
        const scenePromptLines = [];
        sceneCards.forEach((card, index) => {
            const sceneDesc = card.querySelector('textarea').value.trim();
            if (!sceneDesc) return; // Skip empty scenes

            const sceneInputs = card.querySelectorAll('input');
            const sceneStart = sceneInputs[0].value;
            const sceneEnd = sceneInputs[1].value;
            const cameraAngle = card.querySelector('select').value;
            const angleStart = sceneInputs[2].value;
            const angleEnd = sceneInputs[3].value;
            
            let sceneLine = `- Adegan ${index + 1}: ${sceneDesc}`;
            if(sceneStart && sceneEnd) sceneLine += ` [${sceneStart}s-${sceneEnd}s]`;
            scenePromptLines.push(sceneLine + ".");

            let angleLineParts = [];
            if(cameraAngle) angleLineParts.push(`Angle kamera: ${cameraAngle}`);
            if(angleStart && angleEnd) angleLineParts.push(`[${angleStart}s-${angleEnd}s]`);
            if (angleLineParts.length > 0) scenePromptLines.push(`  - ${angleLineParts.join(' ')}.`);
        });

        if (scenePromptLines.length > 0) {
            promptLines.push("\nADEGAN:");
            promptLines.push(...scenePromptLines);
        }
        
        // --- DETAIL TAMBAHAN ---
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
            promptLines.push("\nDETAIL TAMBAHAN:");
        }

        if (ekspresiDesc && ekspresiChar) {
            promptLines.push(`- Ekspresi: ${ekspresiChar} ${ekspresiDesc}.`);
        }
        if (gesturDesc) {
            promptLines.push(`- Gestur: ${gesturDesc}.`);
        }
        if (dialogText && dialogChar) {
            promptLines.push(`- Dialog (${dialogLang}): ${dialogChar} berkata, "${dialogText}".`);
        }
        if (subId || subEn) {
            let subLangs = [];
            if(subId) subLangs.push("Indonesia");
            if(subEn) subLangs.push("Inggris");
            if(subLangs.length > 0) promptLines.push(`- Subtitle: Aktif (${subLangs.join(" & ")}).`);
        }

        outputPrompt.value = promptLines.join('\n');
    }
    
    // Initial call to populate dropdowns for the first character
    updateCharacterDropdowns();
});
</script>

</body>
</html>

