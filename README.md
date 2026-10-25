<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>AVELLANEDA AUTOMOTORES | USADOS SELECCIONADOS</title>
<script src="https://cdn.tailwindcss.com"></script>
<link href="https://fonts.googleapis.com/css2?family=Anton&family=Space+Grotesk:wght@300;500;700&display=swap" rel="stylesheet">
<style>
body{background:#050505;color:#F2F0E9;font-family:'Space Grotesk',sans-serif}
.font-anton{font-family:'Anton',sans-serif}
.card-img{transition:transform .8s cubic-bezier(.16,1,.3,1)}
.card:hover .card-img{transform:scale(1.06)}
.glass{backdrop-filter:blur(20px);background:rgba(5,5,5,.85)}
::-webkit-scrollbar{width:6px;height:6px}
::-webkit-scrollbar-thumb{background:rgba(255,255,255,0.15)}
</style>
</head>
<body>
<header class="fixed top-0 w-full z-50 flex justify-between items-center px-6 md:px-12 py-5 glass border-b border-white/10">
<div class="font-anton text-xl tracking-widest leading-none">AVELLANEDA<br><span class="font-light text-[11px] tracking-[0.3em]">AUTOMOTORES</span></div>
<a href="https://wa.me/5493482640000?text=Hola!%20Quiero%20info%20de%20un%20usado" target="_blank" class="border border-white/20 px-5 py-2 text-[10px] tracking-widest hover:bg-white hover:text-black transition">WHATSAPP</a>
</header>

<section class="relative h-[92vh] w-full overflow-hidden pt-[72px]">
<img src="https://images.unsplash.com/photo-1552519507-da3b142c6e3d?q=80&w=2070" class="absolute inset-0 w-full h-full object-cover brightness-[0.55]">
<div class="absolute inset-0 bg-gradient-to-t from-black via-black/40 to-transparent"></div>
<div class="relative z-10 h-full flex flex-col justify-end px-6 md:px-12 pb-16">
<p class="text-[10px] tracking-[0.4em] text-white/60 mb-3">AVELLANEDA - SANTA FE - ARGENTINA</p>
<h1 class="font-anton text-[12vw] md:text-[8vw] leading-[0.85]">USADOS<br>SELECCIONADOS</h1>
<button onclick="document.getElementById('grid').scrollIntoView({behavior:'smooth'})" class="mt-8 w-fit bg-white text-black px-8 py-4 text-xs tracking-[0.2em] hover:bg-[#FF3B30] hover:text-white transition">VER STOCK →</button>
</div>
</section>

<div id="filtros" class="sticky top-[72px] z-40 glass border-b border-white/10 px-6 md:px-12 py-4 flex flex-wrap gap-2">
<input id="search" placeholder="BUSCAR: HILUX, AMAROK, CRONOS..." class="bg-transparent border-b border-white/20 py-2 w-full lg:w-[320px] text-xs tracking-widest outline-none placeholder:text-white/30 focus:border-white">
<select id="fMarca" class="bg-[#0F0F0F] border border-white/10 px-3 py-2 text-[11px] outline-none"><option value="">MARCA</option><option>TOYOTA</option><option>FORD</option><option>VOLKSWAGEN</option><option>FIAT</option><option>PEUGEOT</option><option>AUDI</option></select>
<select id="fTrans" class="bg-[#0F0F0F] border border-white/10 px-3 py-2 text-[11px] outline-none"><option value="">CAJA</option><option>AUTOMÁTICO</option><option>MANUAL</option></select>
<select id="fAnio" class="bg-[#0F0F0F] border border-white/10 px-3 py-2 text-[11px] outline-none"><option value="">AÑO</option><option>2025</option><option>2024</option><option>2023</option><option>2022</option><option>2021</option></select>
<button onclick="limpiar()" class="text-[10px] tracking-widest opacity-50 hover:opacity-100 ml-2">LIMPIAR</button>
</div>

<div id="grid" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-[1px] bg-white/10 p-[1px]"></div>
<div id="empty" class="hidden py-24 text-center text-white/40 text-xs tracking-widest">NO SE ENCONTRARON VEHÍCULOS</div>

<footer class="px-6 md:px-12 py-10 border-t border-white/10 text-[10px] tracking-widest text-white/30">
AVELLANEDA AUTOMOTORES • Avellaneda, Santa Fe • WhatsApp 3482 640000
</footer>

<script>
const autos=[
{marca:'TOYOTA',modelo:'HILUX SRX 4X4',anio:'2023',trans:'AUTOMÁTICO',km:'45.000',precio:'USD 38.500',img:'https://images.unsplash.com/photo-1552519507-da3b142c6e3d?q=80&w=800'},
{marca:'VOLKSWAGEN',modelo:'AMAROK V6 EXTREME',anio:'2022',trans:'AUTOMÁTICO',km:'62.000',precio:'USD 36.900',img:'https://images.unsplash.com/photo-1494976388531-d1058494cdd8?q=80&w=800'},
{marca:'FORD',modelo:'RANGER RAPTOR',anio:'2025',trans:'AUTOMÁTICO',km:'0',precio:'USD 89.500',img:'https://images.unsplash.com/photo-1605893477799-b99e3b8b93fe?q=80&w=800'},
{marca:'AUDI',modelo:'Q8 55 TFSI',anio:'2024',trans:'AUTOMÁTICO',km:'8.500',precio:'USD 115.000',img:'https://images.unsplash.com/photo-1603584173870-7f23fdae1b7a?q=80&w=800'},
{marca:'FIAT',modelo:'CRONOS DRIVE 1.3',anio:'2023',trans:'MANUAL',km:'22.000',precio:'$ 14.900.000',img:'https://images.unsplash.com/photo-1623869675781-80b862f144a?q=80&w=800'},
{marca:'PEUGEOT',modelo:'208 FELINE 1.6',anio:'2024',trans:'AUTOMÁTICO',km:'9.000',precio:'$ 18.500.000',img:'https://images.unsplash.com/photo-1494976388531-d1058494cdd8?q=80&w=800'},
];

function render(list){
const grid=document.getElementById('grid');
const empty=document.getElementById('empty');
if(list.length===0){grid.innerHTML='';empty.classList.remove('hidden');return;}
empty.classList.add('hidden');
grid.innerHTML=list.map(a=>`
<div class="bg-[#050505] group card flex flex-col">
<div class="overflow-hidden aspect-[4/3] relative"><img src="${a.img}" class="card-img w-full h-full object-cover" loading="lazy" onerror="this.src='https://images.unsplash.com/photo-1494976388531-d1058494cdd8?q=80&w=800'"><div class="absolute top-3 left-3 bg-white text-black text-[9px] px-2 py-1 tracking-widest">${a.anio}</div></div>
<div class="p-5 flex flex-col flex-1">
<p class="text-[9px] tracking-[0.3em] text-white/40">${a.marca} • ${a.trans} • ${a.anio}</p>
<h3 class="font-bold text-[13px] tracking-widest mt-2">${a.marca} ${a.modelo}</h3>
<div class="flex justify-between items-center mt-3"><span class="text-[11px] text-white/50">${a.km} KM</span><span class="font-anton text-lg">${a.precio}</span></div>
<a href="https://wa.me/5493482640000?text=Hola!%20Me%20interesa%20${encodeURIComponent(a.marca+' '+a.modelo+' '+a.anio+' '+a.precio)}" target="_blank" class="mt-4 block text-center border border-white/10 py-3 text-[10px] tracking-[0.3em] hover:bg-white hover:text-black transition">CONSULTAR</a>
</div>
</div>`).join('');
}

function filterAll(){
const q=document.getElementById('search').value.toUpperCase().trim();
const m=document.getElementById('fMarca').value;
const t=document.getElementById('fTrans').value;
const an=document.getElementById('fAnio').value;
let f=autos.filter(a=>{
const txt=(a.marca+' '+a.modelo).toUpperCase();
return (q===''||txt.includes(q))&&(m===''||a.marca===m)&&(t===''||a.trans===t)&&(an===''||a.anio===an);
});
render(f);
}
function limpiar(){
document.getElementById('search').value='';
document.getElementById('fMarca').value='';
document.getElementById('fTrans').value='';
document.getElementById('fAnio').value='';
render(autos);
}
['search','fMarca','fTrans','fAnio'].forEach(id=>document.getElementById(id).addEventListener('input',filterAll));
render(autos);
</script>
</body>
</html>
