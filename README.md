# zinixflix
أفلام ومسلسلات ومباريات رياضية 
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>تطبيق الأفلام والمباريات</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Tajawal:wght@400;500;700&display=swap');
        body { font-family: 'Tajawal', sans-serif; }
        .pulse { animation: pulse-animation 2s infinite; }
        @keyframes pulse-animation {
            0% { opacity: 1; transform: scale(1); }
            50% { opacity: 0.5; transform: scale(1.1); }
            100% { opacity: 1; transform: scale(1); }
        }
        .tab-content { display: none; }
        .tab-content.active { display: block; animation: fadeIn 0.3s ease-in-out; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }
    </style>
</head>
<body class="bg-gray-900 text-white min-h-screen">

    <!-- شريط التنقل العلوي -->
    <nav class="bg-gray-800 shadow-lg sticky top-0 z-50">
        <div class="max-w-7xl mx-auto px-4">
            <div class="flex justify-between items-center h-16">
                <div class="flex space-x-4 space-x-reverse items-center">
                    <span class="text-2xl font-bold text-blue-500"><i class="fas fa-play-circle ml-2"></i>شامل</span>
                    <div class="hidden md:flex space-x-2 space-x-reverse">
                        <button onclick="switchTab('movies')" class="tab-btn px-4 py-2 rounded-md hover:bg-gray-700 transition active-tab text-blue-400" data-target="movies">🎬 الأفلام</button>
                        <button onclick="switchTab('matches')" class="tab-btn px-4 py-2 rounded-md hover:bg-gray-700 transition" data-target="matches">⚽ المباريات</button>
                    </div>
                </div>
            </div>
        </div>
    </nav>

    <!-- المحتوى الرئيسي -->
    <main class="max-w-7xl mx-auto px-4 py-6">

        <!-- تبويب الأفلام -->
        <section id="movies" class="tab-content active">
            <div class="flex flex-col md:flex-row justify-between items-center mb-6 gap-4">
                <h2 class="text-3xl font-bold">الأفلام الرائجة</h2>
                <div class="relative w-full md:w-80">
                    <!-- حقل البحث المباشر -->
                    <input type="text" id="searchInput" placeholder="بحث عن فيلم أو ممثل..." class="w-full bg-gray-800 text-white rounded-full py-2 px-4 pl-10 focus:outline-none focus:ring-2 focus:ring-blue-500 transition">
                    <i class="fas fa-search absolute left-4 top-3 text-gray-400"></i>
                </div>
            </div>
            
            <!-- حاوية الأفلام (سيتم تعبئتها ديناميكياً بواسطة الجافاسكربت) -->
            <div id="moviesContainer" class="grid grid-cols-2 md:grid-cols-4 lg:grid-cols-5 gap-6">
                <!-- سيتم حقن البطاقات هنا -->
            </div>
        </section>

        <!-- تبويب المباريات -->
        <section id="matches" class="tab-content">
            <div class="bg-red-900/30 border border-red-500/50 rounded-lg p-3 mb-6 flex items-center justify-between">
                <div class="flex items-center">
                    <div class="w-3 h-3 bg-red-500 rounded-full pulse ml-3"></div>
                    <span class="font-bold text-red-400">مباشر الآن:</span>
                    <span class="ml-2 text-sm text-gray-300">يوجد 1 مباراة جارية حالياً</span>
                </div>
            </div>

            <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                <div class="bg-gray-800 rounded-lg p-4 border-l-4 border-red-500 cursor-pointer" onclick="toggleMatchDetails('match1')">
                    <div class="flex justify-between items-center mb-2">
                        <span class="text-xs text-gray-400">دوري أبطال أوروبا</span>
                        <div class="flex items-center text-red-500 font-bold text-sm">
                            <span class="pulse mr-1">🔴</span> د. 75
                        </div>
                    </div>
                    <div class="flex justify-between items-center text-xl font-bold">
                        <div class="flex items-center w-1/3"><img src="https://media.api-sports.io/football/teams/541.png" class="w-6 h-6 ml-2" alt="Real Madrid"> ريال مدريد</div>
                        <div class="bg-gray-900 px-4 py-1 rounded text-red-400 tracking-widest">2 - 1</div>
                        <div class="flex items-center justify-end w-1/3"><img src="https://media.api-sports.io/football/teams/157.png" class="w-6 h-6 mr-2" alt="Bayern"> بايرن ميونخ</div>
                    </div>
                    <div id="match1" class="hidden mt-4 pt-4 border-t border-gray-700 text-sm">
                        <div class="flex justify-between text-gray-300">
                            <div>⚽ فينيسيوس جونيور (15')</div>
                            <div class="text-left">⚽ هاري كين (42')</div>
                        </div>
                    </div>
                </div>
            </div>
        </section>

    </main>

    <script>
        // دالة التبديل بين التبويبات
        function switchTab(tabId) {
            document.querySelectorAll('.tab-content').forEach(tab => tab.classList.remove('active'));
            document.querySelectorAll('.tab-btn').forEach(btn => btn.classList.remove('text-blue-400'));
            
            document.getElementById(tabId).classList.add('active');
            document.querySelector(`[data-target="${tabId}"]`).classList.add('text-blue-400');
        }

        // دالة إظهار وإخفاء تفاصيل المباراة
        function toggleMatchDetails(matchId) {
            document.getElementById(matchId).classList.toggle('hidden');
        }

        // ==========================================
        // قسم البيانات الوهمية (Mock Data) والبحث
        // ==========================================

        // 1. مصفوفة الأفلام محاكية لبيانات TMDB
        const mockMovies = [
            {
                id: 1,
                title: "Deadpool & Wolverine",
                image: "https://image.tmdb.org/t/p/w500/8cdWjvZQUExUUTzyp4t6EDMubfO.jpg",
                rating: 8.5,
                genres: "أكشن, كوميديا",
                actors: ["Ryan Reynolds", "Hugh Jackman"]
            },
            {
                id: 2,
                title: "Dune: Part Two",
                image: "https://image.tmdb.org/t/p/w500/1pdfLvkbY9ohJlCjQH2JGqqc9bG.jpg",
                rating: 8.3,
                genres: "خيال علمي, مغامرة",
                actors: ["Timothée Chalamet", "Zendaya"]
            },
            {
                id: 3,
                title: "Oppenheimer",
                image: "https://image.tmdb.org/t/p/w500/8Gxv8gSFCU0XGDykEGv7zR1n2ua.jpg",
                rating: 8.9,
                genres: "سيرة ذاتية, دراما",
                actors: ["Cillian Murphy", "Robert Downey Jr."]
            },
            {
                id: 4,
                title: "The Batman",
                image: "https://image.tmdb.org/t/p/w500/74xTEgt7R36Fpooo50r9T25onhq.jpg",
                rating: 7.8,
                genres: "أكشن, جريمة",
                actors: ["Robert Pattinson", "Zoë Kravitz"]
            },
            {
                id: 5,
                title: "Interstellar",
                image: "https://image.tmdb.org/t/p/w500/gEU2QniE6E77NI6lCU6MxlNBvIx.jpg",
                rating: 8.6,
                genres: "خيال علمي, دراما",
                actors: ["Matthew McConaughey", "Anne Hathaway"]
            }
        ];

        // 2. العناصر من واجهة المستخدم
        const moviesContainer = document.getElementById('moviesContainer');
        const searchInput = document.getElementById('searchInput');

        // 3. دالة بناء وعرض الأفلام في الصفحة
        function renderMovies(moviesArray) {
            moviesContainer.innerHTML = ''; // تفريغ الحاوية قبل إعادة الرسم

            // في حال لم يتم العثور على نتائج
            if (moviesArray.length === 0) {
                moviesContainer.innerHTML = `
                    <div class="col-span-full text-center py-12 text-gray-500">
                        <i class="fas fa-search-minus text-4xl mb-3"></i>
                        <p class="text-lg">لم يتم العثور على أفلام أو ممثلين بهذا الاسم</p>
                    </div>
                `;
                return;
            }

            // رسم البطاقات
            moviesArray.forEach(movie => {
                const movieCard = `
                    <div class="bg-gray-800 rounded-lg overflow-hidden shadow-lg hover:scale-105 transition duration-300 flex flex-col h-full">
                        <img src="${movie.image}" alt="${movie.title}" class="w-full h-64 object-cover">
                        <div class="p-4 flex flex-col flex-grow">
                            <h3 class="font-bold text-lg mb-1 truncate" title="${movie.title}">${movie.title}</h3>
                            <p class="text-xs text-gray-400 mb-2 truncate" title="${movie.actors.join('، ')}">بطولة: ${movie.actors.join('، ')}</p>
                            
                            <div class="flex justify-between items-center text-sm text-gray-400 mt-auto pt-2">
                                <span><i class="fas fa-star text-yellow-400 mr-1"></i> ${movie.rating}</span>
                                <span class="text-xs bg-gray-700 px-2 py-1 rounded">${movie.genres.split(',')[0]}</span>
                            </div>
                            
                            <button class="mt-3 w-full bg-blue-600 hover:bg-blue-700 text-white py-1.5 rounded transition font-medium">
                                <i class="fas fa-plus ml-1"></i> قائمتي
                            </button>
                        </div>
                    </div>
                `;
                moviesContainer.innerHTML += movieCard;
            });
        }

        // 4. مستمع الأحداث (Event Listener) للبحث المباشر
        searchInput.addEventListener('input', (e) => {
            const searchTerm = e.target.value.toLowerCase().trim();
            
            const filteredMovies = mockMovies.filter(movie => {
                // البحث في اسم الفيلم
                const titleMatch = movie.title.toLowerCase().includes(searchTerm);
                // البحث في أسماء الممثلين
                const actorMatch = movie.actors.some(actor => actor.toLowerCase().includes(searchTerm));
                
                return titleMatch || actorMatch;
            });

            // إعادة رسم الأفلام بناءً على النتائج المفلترة
            renderMovies(filteredMovies);
        });

        // 5. عرض جميع الأفلام عند تحميل الصفحة لأول مرة
        renderMovies(mockMovies);

    </script>
</body>
</html>
