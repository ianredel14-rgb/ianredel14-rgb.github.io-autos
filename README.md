<!DOCTYPE html>
<html lang="es"><head><meta charset="UTF-8"><meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>AVELLANEDA AUTOMOTORES | DEMO LUXURY</title>
<script src="https://cdn.tailwindcss.com"></script>
<link href="https://fonts.googleapis.com/css2?family=Anton&family=Space+Grotesk:wght@300;500;700&display=swap" rel="stylesheet">
<style>body{background:#050505;color:#F2F0E9;font-family:'Space Grotesk'} .font-anton{font-family:'Anton'} .card-img{transition:transform .8s} .card:hover .card-img{transform:scale(1.06)} .glass{backdrop-filter:blur(20px);background:rgba(5,5,5,.85)}</style>
</head><body>
<header class="fixed top-0 w-full z-50 flex justify-between items-center px-6 md:px-12 py-5 glass border-b border-white/10">
<div class="font-anton text-xl tracking-widest leading-none">AVELLANEDA<br><span class="font-light text-sm tracking-[0.3em]">AUTOMOTORES</span></div>
<a href="https://wa.me/5493482640000" class="border border-white/20 px-5 py-2 text-[10px] tracking-widest hover:bg-white hover:text-black transition">WHATSAPP</a>
</header>
<section class="relative h-[92vh] w-full overflow-hidden pt-[72px]">
<img src="https://images.unsplash.com/photo-1552519507-da3b142c6e3d?q=80&w=2070" class="absolute inset-0 w-full h-full object-cover brightness-[0.55]">
<div class="relative z-10 h-full flex flex-col justify-end px-6 md:px-12 pb-16">
<p class="text-[10px] tracking-[0.4em] text-white/60 mb-3">AVELLANEDA - SANTA FE - ARGENTINA</p>
<h1 class="font-anton text-[12vw] md:text-[8vw] leading-[0.85]">USADOS<br>SELECCIONADOS</h1>
<button onclick="document.getElementById('grid').scrollIntoView({behavior:'smooth'})" class="mt-8 w-fit bg-white text-black px-8 py-4 text-xs tracking-widest">VER STOCK →</button>
</div></section>
<div id="filtros" class="sticky top-[72px] z-40 glass border-b border-white/10 px-6 md:px-12 py-4 flex flex-wrap gap-2">
<input id="search" placeholder="BUSCAR: HILUX, AMAROK, CRONOS..." class="bg-transparent border-b border-white/20 py-2 w-full lg:w-[300px] text-xs tracking-widest outline-none">
<select id="fMarca" class="bg-[#0F0F0F] border border-white/10 px-3 py-2 text-[11px]"><option value="">MARCA</option><option>TOYOTA</option><option>FORD</option><option>VOLKSWAGEN</option><option>FIAT</option><option>PEUGEOT</option></select>
<select id="fTrans" class="bg-[#0F0F0F] border border-white/10 px-3 py-2 text-[11px]"><option value="">CAJA</option><option>AUTOMÁTICO</option><option>MANUAL</option></select>
<select id="fAnio" class="bg-[#0F0F0F] border border-white/10 px-3 py-2 text-[11px]"><option value="">AÑO</option><option>2024</option><option>2023</option><option>2022</option><option>2021</option></select>
</div>
<div id="grid" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-[1px] bg-white/10 p-[1px]"></div>
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
document.getElementById('grid').innerHTML=list.map(a=>`
<div class="bg-[#050505] group">
<div class="overflow-hidden aspect-[4/3]"><img src="${a.img}" class="card-img w-full h-full object-cover"></div>
<div class="p-5"><p class="text-[9px] tracking-[0.3em] text-white/40">${a.marca} • ${a.trans} • ${a.anio}</p><h3 class="font-bold text-[13px] tracking-widest mt-2">${a.marca} ${a.modelo}</h3><div class="flex justify-between items-center mt-3"><span class="text-[11px] text-white/50">${a.km} KM</span><span class="font-anton text-lg">${a.precio}</span></div></div>
</div>`).join('');}
function filterAll(){
const q=document.getElementById('search').value.toUpperCase();
const m=document.getElementById('fMarca').value;
const t=document.getElementById('fTrans').value;
const an=document.getElementById('fAnio').value;
let f=autos.filter(a=>(a.marca+a.modelo).includes(q)&&(m==''||a.marca==m)&&(t==''||a.trans==t)&&(an==''||a.anio==an));
render(f);
}
['search','fMarca','fTrans','fAnio'].forEach(id=>document.getElementById(id).addEventListener('input',filterAll));
render(autos);
</script>
</body></html>
