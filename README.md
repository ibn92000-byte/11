<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    
    <link rel="icon" type="image/png" href="Image/favicon.png">
    
    <title>Walid Market | واجهتك للتسوق الذكي</title>
    <script src="https://cdn.tailwindcss.com"></script>
    
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700;900&display=swap" rel="stylesheet">
    
    <style>
        body { font-family: 'Cairo', sans-serif; }
        .gradient-bg {
            background: linear-gradient(135deg, #1e3a8a 0%, #064e3b 100%);
        }
    </style>
</head>
<body class="bg-gray-50/50 text-gray-800 min-h-screen flex flex-col justify-between">

    <header class="bg-white/80 backdrop-blur-md shadow-sm sticky top-0 z-50 border-b border-gray-100 transition-all duration-300">
        <div class="container mx-auto px-4 py-3 flex flex-col sm:flex-row justify-between items-center gap-3 sm:gap-4">
            
            <div class="flex justify-between items-center w-full sm:w-auto gap-4">
                <a href="index.html" class="flex items-center h-12 sm:h-14 group">
                    <div id="logoContainer" class="h-full flex items-center">
                        <img src="Image/logo.png" alt="Walid Market" class="h-full w-auto object-contain transition-transform group-hover:scale-105" 
                             onerror="window.showTextLogo()">
                    </div>
                </a>
                
                <a href="login.html" class="sm:hidden px-4 py-2 rounded-xl font-bold text-xs bg-blue-50 text-blue-900 hover:bg-blue-100 transition-all duration-300">
                    تسجيل دخول
                </a>
            </div>
            
            <div class="w-full sm:flex-grow sm:max-w-md relative">
                <input type="text" id="searchInput" placeholder="ابحث عن منتجك المفضل الآن..." 
                       class="w-full pl-4 pr-11 py-2.5 sm:py-3 rounded-2xl border border-gray-200 outline-none focus:border-green-600 focus:ring-4 focus:ring-green-500/10 bg-gray-50/80 transition-all text-xs sm:text-sm font-semibold">
                <span class="absolute right-4 top-1/2 -translate-y-1/2 text-lg sm:text-xl text-gray-400">🔍</span>
            </div>

            <div class="hidden sm:flex items-center gap-3">
                <a href="login.html" class="px-5 py-2.5 rounded-2xl font-bold text-sm bg-blue-50 text-blue-900 hover:bg-blue-100 transition-all duration-300">
                    تسجيل دخول
                </a>
            </div>
        </div> 
    </header>

    <section class="gradient-bg text-white py-8 sm:py-14 px-4 text-center relative overflow-hidden shadow-inner">
        <div class="absolute inset-0 opacity-10 bg-[radial-gradient(#fff_1px,transparent_1px)] [background-size:20px_20px]"></div>
        <div class="max-w-3xl mx-auto relative z-10 space-y-3 sm:space-y-4">
            <span class="bg-green-500/20 text-green-300 border border-green-500/30 px-3 py-1 sm:px-4 sm:py-1.5 rounded-full text-[10px] sm:text-xs font-bold tracking-wide animate-pulse inline-block">
                ✨ منصة وليد ماركت المعتمدة
            </span>
            <h1 class="text-2xl sm:text-4xl md:text-5xl font-black leading-tight">تسوق بأمان والدفع عند <span class="text-green-400">الاستلام</span></h1>
            <p class="text-blue-100/80 text-xs sm:text-base max-w-lg mx-auto font-medium">
                اكتشف تشكيلتنا الحصرية المميزة. جودة عالية، أسعار تنافسية، وتوصيل سريع مباشرة إلى باب منزلك.
            </p>
        </div>
    </section>

    <main class="container mx-auto px-3 sm:px-4 py-6 sm:py-10 flex-grow">
        
        <div class="mb-6 sm:mb-10 bg-white p-3 sm:p-4 rounded-2xl sm:rounded-3xl shadow-sm border border-gray-100/80 flex flex-row items-center justify-between gap-4">
            <div class="flex items-center gap-2 sm:gap-3">
                <span class="p-1.5 sm:p-2 bg-green-50 text-green-600 rounded-xl text-lg sm:text-xl">🎯</span>
                <div>
                    <h2 class="font-bold text-gray-800 text-xs sm:text-base">التصنيفات</h2>
                    <p class="text-[10px] text-gray-400 hidden sm:block">فلترة سريعة للوصول لطلبك</p>
                </div>
            </div>
            <select id="categoryFilter" class="p-2 sm:p-3 rounded-xl sm:rounded-2xl border border-gray-200 outline-none w-40 sm:w-56 text-xs sm:text-sm font-semibold bg-gray-50/50 focus:border-green-600 cursor-pointer">
                <option value="all">كل التصنيفات</option>
            </select>
        </div>

        <div id="productsGrid" class="grid grid-cols-2 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 xl:grid-cols-5 gap-3 sm:gap-6">
            </div>
    </main>

    <footer class="bg-white border-t border-gray-100 py-4 sm:py-6 text-center text-[10px] sm:text-xs font-semibold text-gray-400">
        <p>&copy; 2026 <span class="text-blue-900 font-bold">Walid Market</span>. جميع الحقوق محفوظة.</p>
    </footer>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
        import { getFirestore, collection, getDocs, query, where } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-firestore.js";

        // 🔥 إعدادات الفايربيز الخاصة بك
        const firebaseConfig = {
            apiKey: "AIzaSyAIfkBI0WhxZr1hCyiuYcbVYAy3wXAJxCU",
            authDomain: "walid-shop.firebaseapp.com",
            projectId: "walid-shop",
            storageBucket: "walid-shop.firebasestorage.app",
            messagingSenderId: "3705207162",
            appId: "1:3705207162:web:7b3a80ba4acea3e29c3ec3",
            measurementId: "G-YX3PT078PG"
        };

        // تهيئة الفايربيز وقاعدة البيانات
        const app = initializeApp(firebaseConfig);
        const db = getFirestore(app);
        
        let allProducts = [];

        // تعريف دالة اللوجو النصي احتياطياً في النطاق العالمي
        window.showTextLogo = () => {
            const container = document.getElementById('logoContainer');
            if (container) {
                container.innerHTML = `
                    <div class="flex items-center gap-1.5 sm:gap-2 bg-gradient-to-r from-blue-900 to-blue-800 text-white px-3 py-1.5 sm:px-4 sm:py-2 rounded-xl sm:rounded-2xl shadow-md shadow-blue-900/10">
                        <span class="text-base sm:text-xl">🛒</span>
                        <span class="font-black tracking-wide text-xs sm:text-lg">Walid<span class="text-green-400">Market</span></span>
                    </div>
                `;
            }
        };

        // دالة عرض المنتجات في الصفحة
        function renderProducts(products) {
            const grid = document.getElementById('productsGrid');
            if (!grid) return;
            
            if (products.length === 0) {
                grid.innerHTML = `
                    <div class="col-span-full text-center py-12 bg-white rounded-2xl border border-dashed border-gray-200">
                        <span class="text-3xl block mb-2">📦</span>
                        <p class="text-gray-400 font-bold text-xs">لا توجد منتجات حالياً.</p>
                    </div>`;
                return;
            }

            grid.innerHTML = products.map(p => {
                const productImg = p.image ? (Array.isArray(p.image) ? p.image[0] : p.image) : 'https://placehold.co/400x400?text=لا+صورة';
                const formattedPrice = p.price ? Number(p.price).toLocaleString() : "0";

                return `
                <div class="bg-white rounded-2xl sm:rounded-3xl shadow-sm border border-gray-100/70 overflow-hidden hover:shadow-xl hover:-translate-y-1 transition-all duration-300 flex flex-col justify-between group relative">
                    
                    <a href="product-details.html?id=${p.id}" class="block flex-grow">
                        <div class="h-36 sm:h-52 overflow-hidden bg-gray-50 relative border-b border-gray-100/50">
                            <img src="${productImg}" class="w-full h-full object-cover group-hover:scale-105 transition-transform duration-500" alt="${p.name || ''}">
                            <span class="absolute top-2 right-2 bg-white/90 backdrop-blur-sm text-green-600 text-[9px] sm:text-[10px] font-black px-2 py-0.5 sm:px-2.5 sm:py-1 rounded-full shadow-sm">
                                متوفر ⚡
                            </span>
                        </div>
                        
                        <div class="p-3 sm:p-5">
                            <h3 class="font-bold text-gray-800 text-xs sm:text-base truncate group-hover:text-green-600 transition-colors duration-300">${p.name || 'منتج بدون اسم'}</h3>
                            <div class="flex items-baseline gap-0.5 sm:gap-1 mt-1 sm:mt-2">
                                <span class="text-base sm:text-2xl font-black text-green-600">${formattedPrice}</span>
                                <span class="text-[10px] sm:text-xs font-bold text-green-700">د.ج</span>
                            </div>
                        </div>
                    </a>
                    
                    <div class="p-3 sm:p-5 pt-0 space-y-1.5 sm:space-y-2.5">
                        <a href="product-details.html?id=${p.id}" class="w-full bg-gray-50 text-gray-600 py-2 sm:py-3 rounded-xl sm:rounded-2xl font-bold text-[10px] sm:text-xs hover:bg-gray-100 text-center transition-colors duration-300 block">
                            🔎 التفاصيل
                        </a>
                        <a href="checkout.html?productId=${p.id}" class="w-full bg-gradient-to-r from-green-600 to-emerald-600 text-white py-2 sm:py-3 rounded-xl sm:rounded-2xl font-bold text-[10px] sm:text-xs hover:from-green-700 hover:to-emerald-700 text-center transition-all duration-300 block shadow-md shadow-green-600/20">
                            ⚡ شراء الآن
                        </a>
                    </div>
                </div>
                `;
            }).join('');
        }

        // دالة الفلترة والبحث المشترك
        function filterProducts() {
            const queryVal = document.getElementById('searchInput').value.toLowerCase().trim();
            const catId = document.getElementById('categoryFilter').value;
            
            const filtered = allProducts.filter(p => {
                const matchName = p.name ? p.name.toLowerCase().includes(queryVal) : false;
                const matchCat = (catId === 'all' || p.category === catId);
                return matchName && matchCat;
            });
            
            renderProducts(filtered);
        }

        // ربط أحداث البحث والفلترة بالعناصر مباشرة لمنع مشاكل النطاق (Scope) في الموديولات
        document.getElementById('searchInput').addEventListener('input', filterProducts);
        document.getElementById('categoryFilter').addEventListener('change', filterProducts);

        // الدالة الأساسية لتشغيل الصفحة وجلب البيانات
        async function init() {
            try {
                // 1. جلب التصنيفات من كولكشن categories
                const categoriesSnapshot = await getDocs(collection(db, 'categories'));
                const catFilter = document.getElementById('categoryFilter');
                
                categoriesSnapshot.forEach(docSnap => {
                    const catData = docSnap.data();
                    const option = document.createElement('option');
                    option.value = docSnap.id;
                    option.textContent = catData.name;
                    catFilter.appendChild(option);
                });

                // 2. جلب المنتجات النشطة فقط من كولكشن products
                const q = query(collection(db, 'products'), where('is_active', '==', true));
                const productsSnapshot = await getDocs(q);
                
                allProducts = productsSnapshot.docs.map(docSnap => ({ id: docSnap.id, ...docSnap.data() }));
                
                // ترتيب المنتجات برمجياً من الأحدث للأقدم
                allProducts.sort((a, b) => new Date(b.created || 0) - new Date(a.created || 0));
                
                // عرض المنتجات فوراً
                renderProducts(allProducts);
            } catch (err) {
                console.error("خطأ أثناء الاتصال بقاعدة بيانات الفايربيز:", err);
            }
        }

        // تشغيل التطبيق عند تحميل الصفحة
        init();
    </script>
</body>
</html>
