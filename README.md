<!DOCTYPE html><html lang="es" class="h-full">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Battlezone Ofertas</title>
  <meta name="description" content="Ofertas curadas de Amazon, AliExpress, Mercado Libre y más. Actualizado al día.">
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700;800&display=swap" rel="stylesheet">
  <!-- Tailwind via CDN (ideal para prototipo). Para prod, usa build propio. -->
  <script src="https://cdn.tailwindcss.com"></script>
  <script>
    tailwind.config = {
      theme: {
        extend: {
          colors: {
            bzPurple: '#5D2F91',
            bzYellow: '#FFDB00',
            bzOrange: '#ED7E0B',
            bzRed: '#C3262F',
            ink: '#101010'
          },
          boxShadow: {
            soft: '0 10px 25px rgba(0,0,0,0.08)'
          },
        }
      }
    }
  </script>
  <style>
    :root{color-scheme: dark light}
    body{font-family: Inter, system-ui, -apple-system, Segoe UI, Roboto, 'Helvetica Neue', Arial}
    .line-clamp-2{display:-webkit-box;-webkit-line-clamp:2;-webkit-box-orient:vertical;overflow:hidden}
  </style>
</head>
<body class="min-h-full bg-neutral-50 text-ink dark:bg-ink dark:text-white">
  <!-- Top bar -->
  <header class="sticky top-0 z-40 bg-white/90 dark:bg-ink/90 backdrop-blur shadow-sm">
    <div class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8 py-3 flex items-center gap-3">
      <div class="h-10 w-10 rounded-2xl bg-bzPurple flex items-center justify-center shadow-soft">
        <span class="text-white font-extrabold">BZ</span>
      </div>
      <div class="flex-1">
        <h1 class="text-lg sm:text-xl font-extrabold tracking-tight">Battlezone Ofertas</h1>
        <p class="text-xs text-neutral-500 dark:text-neutral-400">Curadas para LATAM • Enlaces de afiliado</p>
      </div>
      <a id="submit-deal" href="#" class="hidden sm:inline-flex items-center gap-2 rounded-xl px-3 py-2 text-sm font-semibold bg-bzPurple text-white hover:opacity-90 shadow-soft">
        <!-- plus icon -->
        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" class="h-4 w-4"><path fill="currentColor" d="M11 11V5h2v6h6v2h-6v6h-2v-6H5v-2z"/></svg>
        Sugerir oferta
      </a>
    </div>
  </header>  <!-- Filters/Search -->  <section class="border-b border-neutral-200/70 dark:border-white/10 bg-white dark:bg-ink">
    <div class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8 py-4 grid grid-cols-1 md:grid-cols-4 gap-3">
      <div class="md:col-span-2 relative">
        <input id="search" type="search" placeholder="Buscar: Lego, Funko, audífonos…" class="w-full rounded-2xl border border-neutral-300 dark:border-white/10 bg-white/70 dark:bg-neutral-900/60 px-4 py-3 pr-10 outline-none focus:ring-4 focus:ring-bzPurple/20" />
        <svg class="absolute right-3 top-1/2 -translate-y-1/2 h-5 w-5 text-neutral-400" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path fill="currentColor" d="M15.5 14h-.79l-.28-.27A6.471 6.471 0 0016 9.5 6.5 6.5 0 109.5 16c1.61 0 3.09-.59 4.23-1.57l.27.28v.79l5 4.99L20.49 19l-4.99-5zm-6 0C7.01 14 5 11.99 5 9.5S7.01 5 9.5 5 14 7.01 14 9.5 11.99 14 9.5 14z"/></svg>
      </div>
      <select id="storeFilter" class="rounded-2xl border border-neutral-300 dark:border-white/10 bg-white/70 dark:bg-neutral-900/60 px-4 py-3 focus:ring-4 focus:ring-bzPurple/20">
        <option value="">Todas las tiendas</option>
        <option>Amazon</option>
        <option>AliExpress</option>
        <option>Mercado Libre</option>
        <option>Otros</option>
      </select>
      <select id="sortBy" class="rounded-2xl border border-neutral-300 dark:border-white/10 bg-white/70 dark:bg-neutral-900/60 px-4 py-3 focus:ring-4 focus:ring-bzPurple/20">
        <option value="new">Más recientes</option>
        <option value="discount">Mayor descuento</option>
        <option value="price-asc">Precio: bajo a alto</option>
        <option value="price-desc">Precio: alto a bajo</option>
      </select>
    </div>
  </section>  <!-- Main grid -->  <main class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8 py-6">
    <div id="grid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-5"></div>
    <div id="empty" class="hidden text-center text-neutral-500 dark:text-neutral-400 py-16">Sin resultados. Ajusta filtros o busca otra palabra.</div>
  </main>  <!-- Footer -->  <footer class="border-t border-neutral-200/70 dark:border-white/10 py-10 text-sm">
    <div class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8 flex flex-col md:flex-row items-center justify-between gap-4">
      <p>&copy; <span id="year"></span> Battlezone LATAM. Algunos enlaces generan comisión (afiliados).</p>
      <nav class="flex items-center gap-4 text-neutral-500">
        <a href="#" class="hover:text-bzPurple">Aviso de privacidad</a>
        <a href="#" class="hover:text-bzPurple">Términos</a>
        <a href="#" class="hover:text-bzPurple">Contacto</a>
      </nav>
    </div>
  </footer>  <!-- Datos de ejemplo embebidos para que funcione sin backend -->  <script id="offers-data" type="application/json">{
    "affiliate": {
      "amazon_tag": "battlezone-20",  
      "aliexpress_tag": "?aff_fcid=YOUR_CODE",
      "ml_tag": "?matt_id=YOUR_CODE"
    },
    "offers": [
      {
        "id": "lego-groot",
        "title": "LEGO Marvel Groot 76217 (476 pzas)",
        "img": "https://images.unsplash.com/photo-1605649487211-9b231f5a4d58?q=80&w=800&auto=format&fit=crop",
        "price": 1399.00,
        "oldPrice": 1999.00,
        "store": "Amazon",
        "currency": "MXN",
        "category": "Juguetes",
        "url": "https://www.amazon.com.mx/dp/B09QGZ5V7F",
        "createdAt": "2025-08-12T16:00:00Z"
      },
      {
        "id": "headset-sony",
        "title": "Audífonos Sony WH-CH520 BT",
        "img": "https://images.unsplash.com/photo-1518441902110-574a93ff6d57?q=80&w=800&auto=format&fit=crop",
        "price": 649.00,
        "oldPrice": 999.00,
        "store": "Amazon",
        "currency": "MXN",
        "category": "Audio",
        "url": "https://www.amazon.com.mx/dp/B0BXMJ2M6V",
        "createdAt": "2025-08-13T01:00:00Z"
      },
      {
        "id": "funko-gojo",
        "title": "Funko Pop! Satoru Gojo (Jujutsu Kaisen)",
        "img": "https://images.unsplash.com/photo-1612387090619-96c1f0aaae06?q=80&w=800&auto=format&fit=crop",
        "price": 259.00,
        "oldPrice": 389.00,
        "store": "AliExpress",
        "currency": "MXN",
        "category": "Coleccionables",
        "url": "https://www.aliexpress.com/item/1005001234567890.html",
        "createdAt": "2025-08-10T18:30:00Z"
      },
      {
        "id": "switch-controller",
        "title": "Control Wireless para Nintendo Switch",
        "img": "https://images.unsplash.com/photo-1603484477859-abe6a73f9369?q=80&w=800&auto=format&fit=crop",
        "price": 399.00,
        "oldPrice": 699.00,
        "store": "Mercado Libre",
        "currency": "MXN",
        "category": "Gaming",
        "url": "https://articulo.mercadolibre.com.mx/MLM-1234567890",
        "createdAt": "2025-08-11T12:00:00Z"
      }
    ]
  }</script>  <!-- App JS -->  <script>
    const $grid = document.getElementById('grid');
    const $empty = document.getElementById('empty');
    const $search = document.getElementById('search');
    const $store = document.getElementById('storeFilter');
    const $sort = document.getElementById('sortBy');
    document.getElementById('year').textContent = new Date().getFullYear();

    /** Helpers **/
    const fmtMoney = (v, c='MXN') => new Intl.NumberFormat('es-MX', { style:'currency', currency:c, maximumFractionDigits:0 }).format(v);
    const discountPct = (price, oldPrice) => oldPrice && price < oldPrice ? Math.round((1 - (price/oldPrice))*100) : 0;
    const relativeDate = (iso) => {
      const rtf = new Intl.RelativeTimeFormat('es', {numeric:'auto'});
      const d = new Date(iso); const now = new Date();
      const diff = Math.floor((d - now)/ (1000*60*60));
      const units = [ ['year',24*365], ['month',24*30], ['week',24*7], ['day',24], ['hour',1] ];
      for(const [unit, size] of units){
        const v = Math.round(diff/size); if(Math.abs(v) >=1) return rtf.format(v, unit);
      }
      return 'hoy';
    }

    /** Carga data embebida **/
    const raw = document.getElementById('offers-data').textContent;
    const data = JSON.parse(raw);
    const AFF = data.affiliate || {};

    function withAffiliate(url, store){
      try {
        const u = new URL(url);
        if(store === 'Amazon' && AFF.amazon_tag){ u.searchParams.set('tag', AFF.amazon_tag); }
        if(store === 'AliExpress' && AFF.aliexpress_tag){
          // Mantén parámetros existentes y añade tu código
          const extra = new URLSearchParams(AFF.aliexpress_tag.replace(/^\?/, ''));
          for (const [k,v] of extra) u.searchParams.set(k,v);
        }
        if(store === 'Mercado Libre' && AFF.ml_tag){
          const extra = new URLSearchParams(AFF.ml_tag.replace(/^\?/, ''));
          for (const [k,v] of extra) u.searchParams.set(k,v);
        }
        return u.toString();
      } catch { return url }
    }

    function storeBadge(store){
      const map = {Amazon:'bg-[#232F3E]', AliExpress:'bg-[#FF4747]', 'Mercado Libre':'bg-[#FFE600] text-ink', Otros:'bg-neutral-700'};
      return map[store] || 'bg-neutral-700';
    }

    function card(o){
      const pct = discountPct(o.price, o.oldPrice);
      return `
        <article class="group rounded-2xl border border-neutral-200/70 dark:border-white/10 bg-white dark:bg-neutral-900 overflow-hidden shadow-soft flex flex-col">
          <div class="relative aspect-[4/3] overflow-hidden">
            <img loading="lazy" src="${o.img}" alt="${o.title}" class="h-full w-full object-cover transition-transform duration-300 group-hover:scale-105"/>
            ${pct>0?`<div class="absolute left-3 top-3 rounded-xl bg-bzRed text-white px-2 py-1 text-xs font-bold shadow-soft">-${pct}%</div>`:''}
            <div class="absolute right-3 top-3 rounded-xl px-2 py-1 text-xs font-bold shadow-soft ${storeBadge(o.store)} text-white">${o.store}</div>
          </div>
          <div class="p-4 flex-1 flex flex-col gap-3">
            <h3 class="font-bold text-sm line-clamp-2">${o.title}</h3>
            <div class="flex items-baseline gap-2">
              <span class="text-lg font-extrabold text-bzPurple">${fmtMoney(o.price, o.currency)}</span>
              ${o.oldPrice?`<span class="text-xs line-through text-neutral-400">${fmtMoney(o.oldPrice, o.currency)}</span>`:''}
            </div>
            <div class="mt-auto flex items-center justify-between">
              <span class="text-xs text-neutral-500">${relativeDate(o.createdAt)}</span>
              <a target="_blank" rel="nofollow sponsored noopener" href="${withAffiliate(o.url, o.store)}" class="inline-flex items-center gap-2 rounded-xl bg-bzYellow text-ink font-semibold text-sm px-3 py-2 hover:opacity-90">
                Ver oferta
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" class="h-4 w-4"><path fill="currentColor" d="M13 5.828V15h-2V5.828L7.414 9.414 6 8l6-6 6 6-1.414 1.414zM5 18h14v2H5z"/></svg>
              </a>
            </div>
          </div>
        </article>`
    }

    function applyFilters(list){
      const q = ($search.value||'').toLowerCase().trim();
      const s = $store.value;
      let out = list.filter(o => (!s || o.store===s) && (!q || o.title.toLowerCase().includes(q)));
      switch($sort.value){
        case 'discount': out.sort((a,b)=> (discountPct(b.price,b.oldPrice) - discountPct(a.price,a.oldPrice))); break;
        case 'price-asc': out.sort((a,b)=> a.price - b.price); break;
        case 'price-desc': out.sort((a,b)=> b.price - a.price); break;
        default: out.sort((a,b)=> new Date(b.createdAt)-new Date(a.createdAt));
      }
      return out;
    }

    function render(){
      const list = applyFilters(data.offers||[]);
      $grid.innerHTML = list.map(card).join('');
      $empty.classList.toggle('hidden', list.length>0);
    }

    $search.addEventListener('input',()=>{render()});
    $store.addEventListener('change',()=>{render()});
    $sort.addEventListener('change',()=>{render()});

    render();
  </script></body>
</html>
