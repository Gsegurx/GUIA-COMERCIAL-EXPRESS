[index.html](https://github.com/user-attachments/files/26944193/index.html)
<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>Árbol de Decisión de Venta — Claro</title>
<link href="https://fonts.googleapis.com/css2?family=Nunito:wght@400;600;700;800;900&display=swap" rel="stylesheet">
<style>
*{box-sizing:border-box;margin:0;padding:0}
body{font-family:'Nunito',sans-serif;background:#f2f2f2;min-height:100vh;display:flex;align-items:flex-start;justify-content:center;padding:20px}
.app{width:100%;max-width:480px;background:#fff;border-radius:20px;box-shadow:0 8px 40px rgba(0,0,0,.12);overflow:hidden}
.app-header{background:#E30613;padding:18px 20px 14px;display:flex;align-items:center;gap:12px}
.logo{width:40px;height:40px;border-radius:50%;background:rgba(255,255,255,.2);display:flex;align-items:center;justify-content:center;font-size:20px;flex-shrink:0}
.app-title{color:#fff;font-size:16px;font-weight:900;line-height:1.2}
.app-sub{color:rgba(255,255,255,.75);font-size:11px;font-weight:400}
.body{padding:18px}
.breadcrumb{display:flex;flex-wrap:wrap;gap:4px;margin-bottom:14px;min-height:18px}
.bc-item{font-size:11px;color:#888;display:flex;align-items:center;gap:3px}
.bc-item:not(:last-child)::after{content:"›";opacity:.5}
.bc-item.active{color:#E30613;font-weight:800}
.screen{animation:fadeIn .22s ease}
@keyframes fadeIn{from{opacity:0;transform:translateY(5px)}to{opacity:1;transform:translateY(0)}}
.qbox{background:#f8f8f8;border-radius:14px;padding:16px;margin-bottom:14px;border-left:4px solid #E30613}
.qicon{font-size:26px;margin-bottom:6px;line-height:1}
.qtext{font-size:16px;font-weight:900;color:#1a1a1a;line-height:1.3}
.qhint{font-size:12px;color:#888;margin-top:4px}
.choices{display:grid;gap:10px}
.choices.cols2{grid-template-columns:1fr 1fr}
.choice-btn{border:1.5px solid #e0e0e0;border-radius:14px;padding:14px 12px;background:#fff;cursor:pointer;text-align:left;transition:all .15s;display:flex;align-items:center;gap:10px;width:100%}
.choice-btn:hover{border-color:#E30613;background:#fff5f5;transform:translateY(-2px);box-shadow:0 4px 12px rgba(227,6,19,.1)}
.choice-icon{font-size:24px;flex-shrink:0;line-height:1}
.choice-label{font-size:14px;font-weight:800;color:#1a1a1a;line-height:1.2}
.choice-desc{font-size:11px;color:#888;margin-top:2px;font-weight:400}
.offers-grid{display:grid;gap:9px}
.offer-card{border-radius:12px;padding:12px 12px 10px 14px;border:1px solid #eee;background:#fff;position:relative;overflow:hidden}
.offer-card::before{content:'';position:absolute;left:0;top:0;bottom:0;width:4px;border-radius:4px 0 0 4px;background:#E30613}
.offer-card.gold::before{background:#F59E0B}
.offer-card.teal::before{background:#10B981}
.offer-card.blue::before{background:#3B82F6}
.offer-card.star-card{background:linear-gradient(135deg,#FFFBEB 0%,#FEF3C7 100%);border:2px solid #F59E0B}
.offer-card.star-card::before{background:linear-gradient(180deg,#F59E0B,#D97706);width:5px}
.star-badge{display:inline-flex;align-items:center;gap:4px;background:#F59E0B;color:#fff;font-size:10px;font-weight:900;padding:2px 8px;border-radius:20px;margin-bottom:6px}
.offer-top{display:flex;justify-content:space-between;align-items:flex-start;gap:8px}
.offer-name{font-size:12px;font-weight:800;color:#1a1a1a;line-height:1.3}
.offer-price{font-size:20px;font-weight:900;color:#E30613;line-height:1;white-space:nowrap}
.offer-price.star-price{color:#D97706;font-size:22px}
.offer-period{font-size:10px;color:#aaa;text-align:right}
.price-row{display:flex;gap:8px;align-items:center;margin-top:5px;flex-wrap:wrap}
.price-original{font-size:11px;color:#aaa;text-decoration:line-through}
.price-promo{font-size:13px;font-weight:800;color:#E30613}
.price-tactico{font-size:15px;font-weight:900;color:#D97706}
.price-label{font-size:9px;font-weight:800;color:#888;background:#f0f0f0;padding:1px 5px;border-radius:4px}
.tags{display:flex;flex-wrap:wrap;gap:4px;margin-top:7px}
.tag{font-size:10px;font-weight:800;padding:2.5px 7px;border-radius:20px}
.tag-green{background:#D1FAE5;color:#065F46}
.tag-red{background:#FEE2E2;color:#991B1B}
.tag-amber{background:#FEF3C7;color:#92400E}
.tag-blue{background:#DBEAFE;color:#1E40AF}
.tag-gray{background:#F3F4F6;color:#374151}
.tag-gold{background:#FEF9C3;color:#854D0E;border:1px solid #FDE047}
.warn-box{background:#FFFBEB;border:1.5px solid #F59E0B;border-radius:10px;padding:9px 11px;margin-top:8px;display:flex;gap:7px;align-items:flex-start}
.warn-icon{font-size:14px;flex-shrink:0}
.warn-text{font-size:11px;font-weight:700;color:#78350F;line-height:1.4}
.info-box{background:#EFF6FF;border:1.5px solid #93C5FD;border-radius:10px;padding:9px 11px;margin-top:8px;display:flex;gap:7px;align-items:flex-start}
.info-text{font-size:11px;font-weight:700;color:#1E40AF;line-height:1.4}
.divider{height:1px;background:#f0f0f0;margin:12px 0}
.section-label{font-size:10px;font-weight:900;color:#aaa;text-transform:uppercase;letter-spacing:.05em;margin-bottom:7px}
.section-label.red{color:#E30613}
.mini-grid{display:grid;grid-template-columns:1fr 1fr;gap:7px;margin-bottom:10px}
.mini-card{background:#f8f8f8;border-radius:10px;padding:9px 10px;border:1px solid #eee}
.mini-price{font-size:16px;font-weight:900;color:#E30613}
.mini-label{font-size:10px;color:#888;margin-top:2px}
.mini-card.green{background:#ECFDF5;border-color:#6EE7B7}
.mini-card.green .mini-price{color:#065F46}
.la-table{width:100%;border-collapse:collapse;margin-top:4px}
.la-table th{background:#1a1a1a;color:#fff;font-size:10px;font-weight:800;padding:7px 8px;text-align:center}
.la-table td{font-size:11px;padding:7px 8px;border-bottom:1px solid #f0f0f0;text-align:center;font-weight:600}
.la-table tr:nth-child(even) td{background:#f8f8f8}
.la-table td:first-child{text-align:left;font-weight:700;color:#374151}
.la-na{color:#991B1B;background:#FEE2E2;border-radius:6px;padding:1px 6px;font-size:10px}
.la-price{color:#E30613;font-size:13px;font-weight:900}
/* Price list cards */
.pl-card{border-radius:10px;padding:10px 12px;border:1px solid #eee;background:#fff;margin-bottom:7px;position:relative;overflow:hidden}
.pl-card::before{content:'';position:absolute;left:0;top:0;bottom:0;width:3px;background:#E30613}
.pl-card.star{background:#FFFBEB;border-color:#FDE68A}
.pl-card.star::before{background:#F59E0B}
.pl-header{display:flex;justify-content:space-between;align-items:flex-start;gap:6px}
.pl-name{font-size:11px;font-weight:800;color:#1a1a1a;line-height:1.3;flex:1}
.pl-marca{font-size:9px;color:#888;background:#f3f4f6;padding:1px 5px;border-radius:4px;font-weight:700;white-space:nowrap}
.pl-prices{display:flex;gap:6px;align-items:center;margin-top:5px;flex-wrap:wrap}
.pl-base{font-size:10px;color:#aaa;text-decoration:line-through}
.pl-promo{font-size:12px;font-weight:900;color:#E30613}
.pl-tac{font-size:13px;font-weight:900;color:#D97706}
.pl-lbl{font-size:9px;font-weight:800;padding:1px 5px;border-radius:4px;background:#f3f4f6;color:#374151}
.pl-lbl.tac{background:#FEF3C7;color:#92400E}
.pl-lbl.star{background:#FEF9C3;color:#854D0E}
.speed-group{background:#1a1a1a;border-radius:8px;padding:5px 10px;margin:10px 0 6px;display:flex;align-items:center;gap:6px}
.speed-label{font-size:10px;font-weight:900;color:#fff}
.speed-badge{background:#E30613;color:#fff;font-size:9px;font-weight:900;padding:2px 7px;border-radius:10px}
.nav-row{display:flex;gap:8px;margin-top:14px}
.btn-back{padding:10px 16px;border-radius:10px;border:1.5px solid #e0e0e0;background:#fff;cursor:pointer;font-size:13px;font-weight:800;color:#666;font-family:'Nunito',sans-serif;transition:all .12s}
.btn-back:hover{background:#f5f5f5}
.btn-restart{flex:1;padding:10px;border-radius:10px;border:1.5px solid #E30613;background:#fff5f5;cursor:pointer;font-size:13px;font-weight:800;color:#E30613;font-family:'Nunito',sans-serif;transition:all .12s}
.btn-restart:hover{background:#FEE2E2}
.result-header{text-align:center;padding:10px;margin-bottom:10px}
.result-icon{font-size:32px;margin-bottom:5px}
.result-title{font-size:16px;font-weight:900;color:#1a1a1a}
.result-sub{font-size:11px;color:#888}
.footer{background:#f8f8f8;padding:10px 20px;text-align:center;font-size:10px;color:#bbb;font-weight:600}
</style>
</head>
<body>
<div class="app">
  <div class="app-header">
    <div class="logo">🎯</div>
    <div>
      <div class="app-title">Árbol de Decisión de Venta</div>
      <div class="app-sub">CLAROVTR · Canales Presenciales · Vigencia 14-04-2025</div>
    </div>
  </div>
  <div class="body">
    <div class="breadcrumb" id="breadcrumb"></div>
    <div id="screen-area"></div>
  </div>
  <div class="footer">Coordinación de Gestión de Canales Presenciales · Uso interno</div>
</div>

<script>
// ── DATOS PRECIOS ────────────────────────────────────────────────────────────
const D1P = [
  {marca:'CLARO/VTR',red:'HFC',mb:null,nombre:'Fono Ilimitado 600 Móvil',precio:12990,dctoN:0,promo:0,dctoT:0,tac:0,temp:'',nota:'',star:false},
  {marca:'VTR',red:'FTTH',mb:null,nombre:'Stream TV Inicia ★',precio:20990,dctoN:0,promo:0,dctoT:0,tac:0,temp:'',nota:'* Inst. $50.000',star:false},
  {marca:'CLARO',red:'FTTH',mb:null,nombre:'Stream TV Inicia ★',precio:16990,dctoN:0,promo:0,dctoT:0,tac:0,temp:'',nota:'* Inst. $50.000',star:false},
  {marca:'CLARO/VTR',red:'FTTH',mb:null,nombre:'Stream TV Plus ★',precio:22990,dctoN:0,promo:0,dctoT:0,tac:0,temp:'',nota:'* Inst. $50.000',star:false},
  {marca:'CLARO/VTR',red:'FTTH',mb:null,nombre:'Stream TV Premium ★',precio:28990,dctoN:0,promo:0,dctoT:0,tac:0,temp:'',nota:'* Inst. $50.000',star:false},
  {marca:'CLARO/VTR',red:'HFC',mb:500,nombre:'Internet Hogar',precio:21990,dctoN:7000,promo:14990,dctoT:0,tac:0,temp:'',nota:'',star:false},
  {marca:'VTR',red:'HFC',mb:500,nombre:'Internet Hogar Stream',precio:29990,dctoN:8000,promo:21990,dctoT:0,tac:0,temp:'',nota:'',star:false},
  {marca:'CLARO',red:'HFC',mb:500,nombre:'Internet Hogar Stream',precio:29990,dctoN:9000,promo:20990,dctoT:0,tac:0,temp:'',nota:'',star:false},
  {marca:'CLARO/VTR',red:'FTTH',mb:600,nombre:'Fibra Hogar',precio:21990,dctoN:7000,promo:14990,dctoT:0,tac:0,temp:'',nota:'',star:false},
  {marca:'VTR',red:'FTTH',mb:600,nombre:'Fibra Hogar Stream',precio:29990,dctoN:8000,promo:21990,dctoT:0,tac:0,temp:'',nota:'',star:false},
  {marca:'CLARO',red:'FTTH',mb:600,nombre:'Fibra Hogar Stream',precio:29990,dctoN:9000,promo:20990,dctoT:0,tac:0,temp:'',nota:'',star:false},
  {marca:'CLARO/VTR',red:'FTTH',mb:800,nombre:'Fibra Avanzado',precio:23990,dctoN:8000,promo:15990,dctoT:11000,tac:12990,temp:'x12 meses',nota:'cuota liberada',star:true},
  {marca:'VTR',red:'FTTH',mb:800,nombre:'Fibra Avanzado Stream',precio:31990,dctoN:9000,promo:22990,dctoT:0,tac:0,temp:'',nota:'',star:false},
  {marca:'CLARO',red:'FTTH',mb:800,nombre:'Fibra Avanzado Stream',precio:31990,dctoN:10000,promo:21990,dctoT:0,tac:0,temp:'',nota:'',star:false},
  {marca:'CLARO/VTR',red:'FTTH',mb:940,nombre:'Fibra Experto',precio:29990,dctoN:10000,promo:19990,dctoT:0,tac:0,temp:'',nota:'',star:false},
  {marca:'VTR',red:'FTTH',mb:940,nombre:'Fibra Experto Stream',precio:37990,dctoN:11000,promo:26990,dctoT:0,tac:0,temp:'',nota:'',star:false},
  {marca:'CLARO',red:'FTTH',mb:940,nombre:'Fibra Experto Stream',precio:37990,dctoN:12000,promo:25990,dctoT:0,tac:0,temp:'',nota:'',star:false}
];
const D2P = [
  {marca:'VTR',red:'HFC',mb:null,nombre:'Stream TV Plus + Fono 600 Móvil',precio:28990,dctoN:0,promo:0,dctoT:0,tac:0,temp:'',nota:'',star:false},
  {marca:'VTR',red:'HFC',mb:null,nombre:'Stream TV Premium + Fono 600 Móvil',precio:35990,dctoN:0,promo:0,dctoT:0,tac:0,temp:'',nota:'',star:false},
  {marca:'VTR',red:'HFC',mb:500,nombre:'Doble Pack Plus Hogar',precio:41990,dctoN:11000,promo:30990,dctoT:0,tac:0,temp:'',nota:'',star:false},
  {marca:'VTR',red:'HFC',mb:500,nombre:'Internet Hogar + Fono 600 Móvil',precio:23990,dctoN:0,promo:0,dctoT:0,tac:0,temp:'',nota:'',star:false},
  {marca:'VTR',red:'HFC',mb:500,nombre:'Doble Pack Inicia Hogar',precio:41990,dctoN:0,promo:0,dctoT:0,tac:0,temp:'',nota:'',star:false},
  {marca:'VTR',red:'HFC',mb:500,nombre:'Doble Pack Premium Hogar',precio:46990,dctoN:15000,promo:31990,dctoT:0,tac:0,temp:'',nota:'',star:false},
  {marca:'VTR',red:'FTTH',mb:600,nombre:'Fibra Hogar + Fono 600 Móvil',precio:23990,dctoN:0,promo:0,dctoT:0,tac:0,temp:'',nota:'',star:false},
  {marca:'VTR',red:'FTTH',mb:600,nombre:'Doble Pack Premium Fibra Hogar',precio:46990,dctoN:15000,promo:31990,dctoT:0,tac:0,temp:'',nota:'',star:false},
  {marca:'VTR',red:'FTTH',mb:600,nombre:'Doble Pack Plus Fibra Hogar',precio:41990,dctoN:11000,promo:30990,dctoT:0,tac:0,temp:'',nota:'',star:false},
  {marca:'VTR',red:'FTTH',mb:600,nombre:'Doble Pack Inicia Fibra Hogar',precio:41990,dctoN:0,promo:0,dctoT:0,tac:0,temp:'',nota:'',star:false},
  {marca:'VTR',red:'FTTH',mb:800,nombre:'Fibra Avanzado + Fono 600 Móvil',precio:26990,dctoN:0,promo:0,dctoT:0,tac:0,temp:'',nota:'',star:false},
  {marca:'VTR',red:'FTTH',mb:800,nombre:'Doble Pack Premium Fibra Avanzado',precio:47990,dctoN:14000,promo:33990,dctoT:0,tac:0,temp:'',nota:'',star:false},
  {marca:'VTR',red:'FTTH',mb:800,nombre:'Doble Pack Plus Fibra Avanzado',precio:42990,dctoN:11000,promo:31990,dctoT:0,tac:0,temp:'',nota:'',star:false},
  {marca:'VTR',red:'FTTH',mb:800,nombre:'Doble Pack Inicia Fibra Avanzado',precio:42990,dctoN:0,promo:0,dctoT:17000,tac:25990,temp:'x12 meses',nota:'',star:true},
  {marca:'VTR',red:'FTTH',mb:940,nombre:'Fibra Experto + Fono 600 Móvil',precio:35990,dctoN:0,promo:0,dctoT:0,tac:0,temp:'',nota:'',star:false},
  {marca:'VTR',red:'FTTH',mb:940,nombre:'Doble Pack Premium Fibra Experto',precio:52990,dctoN:14000,promo:38990,dctoT:0,tac:0,temp:'',nota:'',star:false},
  {marca:'VTR',red:'FTTH',mb:940,nombre:'Doble Pack Plus Fibra Experto',precio:47990,dctoN:12000,promo:35990,dctoT:0,tac:0,temp:'',nota:'',star:false},
  {marca:'VTR',red:'FTTH',mb:940,nombre:'Doble Pack Inicia Fibra Experto',precio:47990,dctoN:0,promo:0,dctoT:0,tac:0,temp:'',nota:'',star:false}
];
const D3P = [
  {marca:'VTR',red:'HFC',mb:500,nombre:'Triple Pack Inicia Hogar',precio:46990,dctoN:0,promo:0,dctoT:0,tac:0,temp:'',star:false},
  {marca:'VTR',red:'HFC',mb:500,nombre:'Triple Pack Plus Hogar',precio:46990,dctoN:11000,promo:35990,dctoT:0,tac:0,temp:'',star:false},
  {marca:'VTR',red:'HFC',mb:500,nombre:'Triple Pack Premium Hogar',precio:51990,dctoN:15000,promo:36990,dctoT:0,tac:0,temp:'',star:false},
  {marca:'VTR',red:'FTTH',mb:600,nombre:'Triple Pack Plus Fibra Hogar',precio:46990,dctoN:11000,promo:35990,dctoT:0,tac:0,temp:'',star:false},
  {marca:'VTR',red:'FTTH',mb:600,nombre:'Triple Pack Premium Fibra Hogar',precio:51990,dctoN:15000,promo:36990,dctoT:0,tac:0,temp:'',star:false},
  {marca:'VTR',red:'FTTH',mb:600,nombre:'Triple Pack Inicia Fibra Hogar',precio:46990,dctoN:0,promo:0,dctoT:0,tac:0,temp:'',star:false},
  {marca:'VTR',red:'FTTH',mb:800,nombre:'Triple Pack Plus Fibra Avanzado',precio:47990,dctoN:11000,promo:36990,dctoT:0,tac:0,temp:'',star:false},
  {marca:'VTR',red:'FTTH',mb:800,nombre:'Triple Pack Premium Fibra Avanzado',precio:53990,dctoN:16000,promo:37990,dctoT:0,tac:0,temp:'',star:false},
  {marca:'VTR',red:'FTTH',mb:800,nombre:'Triple Pack Inicia Fibra Avanzado',precio:47990,dctoN:0,promo:0,dctoT:0,tac:0,temp:'',star:false},
  {marca:'VTR',red:'FTTH',mb:940,nombre:'Triple Pack Plus Fibra Experto',precio:52990,dctoN:12000,promo:40990,dctoT:0,tac:0,temp:'',star:false},
  {marca:'VTR',red:'FTTH',mb:940,nombre:'Triple Pack Premium Fibra Experto',precio:58990,dctoN:18000,promo:40990,dctoT:0,tac:0,temp:'',star:false},
  {marca:'VTR',red:'FTTH',mb:940,nombre:'Triple Pack Inicia Fibra Experto',precio:52990,dctoN:0,promo:0,dctoT:0,tac:0,temp:'',star:false}
];

// ── SCREENS ──────────────────────────────────────────────────────────────────
const SCREENS={
  start:{icon:'🏠',q:'¿Qué vas a vender hoy?',hint:'Elige tu negocio',choices:[
    {icon:'🏠',label:'Hogar',desc:'Internet / TV / Telefonía',next:'hogar_tipo'},
    {icon:'📱',label:'Móvil',desc:'Portabilidad / Terreno / Línea Adicional',next:'movil'}
  ],cols:2},

  // ── HOGAR ─────────────────────────────────────────────────────────────────
  hogar_tipo:{icon:'🏠',q:'¿Tipo de vivienda?',hint:'Define el contexto del cliente',choices:[
    {icon:'🏢',label:'Vertical',desc:'Edificios / Condominios',next:'fijo_vertical'},
    {icon:'🏡',label:'Horizontal',desc:'Casas / Villas',next:'fijo_horizontal'},
    {icon:'📋',label:'Todos los precios',desc:'Ver catálogo completo 1P / 2P / 3P',next:'precios_menu'}
  ],cols:1},

  // ── VER TODOS LOS PRECIOS ─────────────────────────────────────────────────
  precios_menu:{icon:'📋',q:'¿Qué tipo de pack necesitas ver?',hint:'Selecciona la cantidad de servicios',choices:[
    {icon:'1️⃣',label:'1 Play',desc:'Un servicio: Internet, TV o Fono',next:'precios_1p'},
    {icon:'2️⃣',label:'2 Play',desc:'Combina dos servicios',next:'precios_2p'},
    {icon:'3️⃣',label:'3 Play',desc:'Triple pack completo',next:'precios_3p'}
  ],cols:1},
  precios_1p:{type:'result',icon:'1️⃣',title:'Precios — 1 Play',sub:'Internet · TV · Telefonía',canal:'list_1p'},
  precios_2p:{type:'result',icon:'2️⃣',title:'Precios — 2 Play',sub:'Doble pack de servicios',canal:'list_2p'},
  precios_3p:{type:'result',icon:'3️⃣',title:'Precios — 3 Play',sub:'Triple pack completo',canal:'list_3p'},

  // ── RESULTADOS HOGAR ──────────────────────────────────────────────────────
  fijo_vertical:{type:'result',icon:'🏢',title:'Verticales — Edificios',sub:'Ofertas destacadas + Táctica',canal:'fijo_v'},
  fijo_horizontal:{type:'result',icon:'🏡',title:'Horizontales — Casas',sub:'Ofertas destacadas + Táctica',canal:'fijo_h'},

  // ── MÓVIL ─────────────────────────────────────────────────────────────────
  movil:{icon:'📱',q:'¿Tipo de gestión móvil?',hint:'Identifica la situación del cliente',choices:[
    {icon:'🔁',label:'Portabilidad',desc:'Pre→Post / Post→Post',next:'movil_port'},
    {icon:'📍',label:'Terreno / Especial',desc:'Venta en terreno o adulto mayor',next:'movil_terreno'},
    {icon:'➕',label:'Línea Adicional',desc:'Cliente nuevo o stock',next:'movil_la_tipo'}
  ],cols:1},
  movil_la_tipo:{icon:'➕',q:'¿Tipo de cliente para línea adicional?',hint:'Determina el perfil del cliente',choices:[
    {icon:'🆕',label:'Cliente Nuevo',desc:'Sin relación previa con Claro',next:'movil_la_nuevo'},
    {icon:'👤',label:'Cliente Stock',desc:'Antigüedad mayor a 7 días',next:'movil_la_stock'}
  ],cols:2},
  movil_la_nuevo:{icon:'🆕',q:'¿La línea adicional es portada?',hint:'Determina si el número viene de otro operador',choices:[
    {icon:'🔁',label:'Sí, portada',desc:'Ambas líneas portadas',next:'movil_la_nuevo_port'},
    {icon:'📵',label:'No portada',desc:'Número Claro o nuevo',next:'movil_la_nuevo_noport'}
  ],cols:2},
  movil_la_nuevo_port:{type:'result',icon:'🔁',title:'Móvil · Cliente Nuevo — Línea Portada',sub:'Plan base y línea adicional, ambos portados',canal:'la_n_p'},
  movil_la_nuevo_noport:{type:'result',icon:'📵',title:'Móvil · Cliente Nuevo — Línea No Portada',sub:'Línea adicional no portada',canal:'la_n_np'},
  movil_la_stock:{type:'result',icon:'👤',title:'Móvil · Cliente Stock',sub:'Antigüedad mayor a 7 días',canal:'la_s'},
  movil_port:{type:'result',icon:'🔁',title:'Portabilidad',sub:'Planes masivos disponibles',canal:'movil'},
  movil_terreno:{type:'result',icon:'📍',title:'Móvil Terreno',sub:'Ofertas tácticas y especiales',canal:'movil_t'}
};

const BREAD={
  start:'Inicio',hogar_tipo:'Hogar',movil:'Móvil',
  fijo_vertical:'Vertical',fijo_horizontal:'Horizontal',
  precios_menu:'Todos los Precios',precios_1p:'1 Play',precios_2p:'2 Play',precios_3p:'3 Play',
  movil_port:'Portabilidad',movil_terreno:'Terreno',
  movil_la_tipo:'Línea Adicional',movil_la_nuevo:'Cliente Nuevo',movil_la_stock:'Cliente Stock',
  movil_la_nuevo_port:'Portada',movil_la_nuevo_noport:'No Portada'
};

let history=[],current='start';

// ── HELPERS ───────────────────────────────────────────────────────────────────
const fmt=n=>'$'+n.toLocaleString('es-CL');
const tag=(cls,txt)=>`<span class="tag ${cls}">${txt}</span>`;

function plCard(p){
  const isStar=p.star;
  let h=`<div class="pl-card${isStar?' star':''}">`;
  if(isStar) h+=`<div style="margin-bottom:4px"><span class="tag tag-gold">⭐ Precio Estrella</span></div>`;
  h+=`<div class="pl-header"><div class="pl-name">${p.nombre}</div><span class="pl-marca">${p.marca} · ${p.red}${p.mb?' · '+p.mb+'M':''}</span></div>`;
  h+=`<div class="pl-prices">`;
  if(p.tac>0){
    h+=`<span class="pl-base">${fmt(p.precio)}</span>`;
    if(p.promo>0) h+=`<span class="pl-promo">${fmt(p.promo)}</span><span style="font-size:9px;color:#aaa">→</span>`;
    h+=`<span class="pl-tac">${fmt(p.tac)}</span><span class="pl-lbl tac">Táctico ${p.temp}</span>`;
  } else if(p.promo>0){
    h+=`<span class="pl-base">${fmt(p.precio)}</span><span class="pl-promo">${fmt(p.promo)}</span><span class="pl-lbl">Promo Nacional</span>`;
  } else {
    h+=`<span class="pl-promo">${fmt(p.precio)}</span><span class="pl-lbl">Precio base</span>`;
  }
  h+=`</div>`;
  if(p.nota) h+=`<div style="font-size:10px;color:#065F46;font-weight:700;margin-top:3px">✅ ${p.nota}</div>`;
  h+=`</div>`;
  return h;
}

function speedGroup(mb,label){
  return `<div class="speed-group"><span class="speed-label">${label||''}</span>${mb?`<span class="speed-badge">${mb} Megas</span>`:''}</div>`;
}

function renderPriceList(data){
  // Group by mb
  const groups={};
  data.forEach(p=>{
    const k=p.mb?p.mb+'M':'TV/Fono';
    if(!groups[k])groups[k]=[];
    groups[k].push(p);
  });
  let h='';
  for(const k in groups){
    const isTVF=k==='TV/Fono';
    h+=speedGroup(isTVF?null:parseInt(k),isTVF?'📺 TV / Telefonía':'📡 Internet');
    groups[k].forEach(p=>{h+=plCard(p);});
  }
  h+=`<div class="info-box" style="margin-top:10px"><div class="warn-icon">📌</div><div class="info-text">★ Planes TV solo cable: instalación tiene costo de $50.000</div></div>`;
  return h;
}

// ── RENDER RESULT ────────────────────────────────────────────────────────────
function renderResult(s){
  let h=`<div class="result-header"><div class="result-icon">${s.icon}</div><div class="result-title">${s.title}</div><div class="result-sub">${s.sub}</div></div>`;

  // ── LISTAS DE PRECIOS COMPLETAS ───────────────────────────────────────────
  if(s.canal==='list_1p') return h+renderPriceList(D1P);
  if(s.canal==='list_2p') return h+renderPriceList(D2P);
  if(s.canal==='list_3p') return h+renderPriceList(D3P);

  // ── ESTRELLA COMPARTIDA (aparece en vertical y horizontal) ────────────────
  function starCards(){
    return `
    <div class="section-label red">⭐ Precios Estrella</div>
    <div class="offers-grid">
      <div class="offer-card star-card">
        <div class="star-badge">⭐ Precio Estrella · 1 Play</div>
        <div class="offer-top">
          <div>
            <div class="offer-name">Fibra Avanzado 800 · CLARO/VTR · FTTH</div>
            <div style="font-size:10px;color:#92400E;margin-top:3px">Promo Táctica · Descuento x 12 meses</div>
          </div>
          <div>
            <div class="offer-price star-price">$12.990</div>
            <div class="offer-period">Precio Táctico</div>
          </div>
        </div>
        <div class="price-row">
          <span class="price-original">$23.990</span>
          <span style="font-size:9px;color:#aaa">→ Nacional</span>
          <span class="price-promo">$15.990</span>
          <span style="font-size:9px;color:#aaa">→ Táctico</span>
          <span class="price-tactico">$12.990</span>
        </div>
        <div class="tags" style="margin-top:6px">
          ${tag('tag-green','✅ Cuota liberada')}${tag('tag-amber','⏱ x12 meses')}${tag('tag-gold','⭐ Táctica')}
        </div>
      </div>
      <div class="offer-card star-card">
        <div class="star-badge">⭐ Precio Estrella · 2 Play</div>
        <div class="offer-top">
          <div>
            <div class="offer-name">Doble Pack Inicia Fibra Avanzado 800 · VTR · FTTH</div>
            <div style="font-size:10px;color:#92400E;margin-top:3px">Precio Táctico · Descuento x 12 meses</div>
          </div>
          <div>
            <div class="offer-price star-price">$25.990</div>
            <div class="offer-period">Precio Táctico</div>
          </div>
        </div>
        <div class="price-row">
          <span class="price-original">$42.990</span>
          <span style="font-size:9px;color:#aaa">→ Táctico</span>
          <span class="price-tactico">$25.990</span>
        </div>
        <div class="tags" style="margin-top:6px">
          ${tag('tag-amber','⏱ x12 meses')}${tag('tag-gold','⭐ Táctica')}
        </div>
      </div>
    </div>`;
  }

  // ── FIJO VERTICAL ─────────────────────────────────────────────────────────
  if(s.canal==='fijo_v'){
    h+=starCards();
    h+=`<div class="divider"></div><div class="section-label">Otras ofertas activas — Verticales</div><div class="offers-grid">`;
    [{n:'1 Play Mega 800',p:'$12.990',per:'Táctica',tags:[['tag-green','✅ Sin cuota']],cls:''},{n:'2–3 Play: dcto 1ª boleta',p:'$10.000',per:'1ª boleta',tags:[['tag-amber','🏷 Puntual']],cls:'gold'},{n:'Dcto Conserjería',p:'6 meses',per:'Beneficio adicional',tags:[['tag-blue','🏢 Solo verticales']],cls:'gold'},{n:'Deco adicional',p:'50%',per:'Descuento deco',tags:[['tag-gray','📺 Accesorio']],cls:'gold'}].forEach(o=>{h+=`<div class="offer-card ${o.cls}"><div class="offer-top"><div class="offer-name">${o.n}</div><div><div class="offer-price">${o.p}</div><div class="offer-period">${o.per}</div></div></div><div class="tags">${o.tags.map(([c,t])=>tag(c,t)).join('')}</div></div>`;});
    h+='</div>';
  }

  // ── FIJO HORIZONTAL ───────────────────────────────────────────────────────
  if(s.canal==='fijo_h'){
    h+=starCards();
    h+=`<div class="divider"></div>`;
    h+=`<div class="section-label">1 Play · Semana táctica</div><div class="offers-grid">
    <div class="offer-card"><div class="offer-top"><div><div class="offer-name">1 Play Fibra Avanzado 800</div><div style="font-size:10px;color:#aaa;margin-top:2px">⏱ 12 meses permanencia</div></div><div><div class="offer-price">$12.990</div><div class="offer-period">sem. táctica</div></div></div><div class="tags">${tag('tag-green','✅ Cuota liberada (semana táctica)')}</div></div>
    <div class="offer-card gold"><div class="offer-top"><div class="offer-name">1 Play · Desde semana 2</div></div><div class="tags">${tag('tag-amber','75% ventas → $12.990')}${tag('tag-red','25% ventas → $14.990')}${tag('tag-green','Agencias/Directa: libre')}</div></div></div>
    <div class="divider"></div><div class="section-label">2 Play</div><div class="offers-grid">
    <div class="offer-card teal"><div class="offer-top"><div class="offer-name">2 Play Premium Fibra / HFC VTR</div><div><div class="offer-price">$28.990</div><div class="offer-period">x6 meses</div></div></div><div class="tags">${tag('tag-green','✅ Cuota liberada todos los subcanales')}</div></div></div>`;
  }

  // ── MÓVIL PORTABILIDAD ────────────────────────────────────────────────────
  if(s.canal==='movil'){
    h+=`<div class="section-label">Planes masivos</div><div class="offers-grid">`;
    [{n:'Plan MAX M',p:'$9.990',per:'x6 meses',tags:[['tag-gray','POSPOS']]},{n:'Plan MAX L Libre',p:'$7.990',per:'x6 meses',tags:[['tag-blue','Libre']]},{n:'Plan MAX XL Libre',p:'$11.990',per:'x6 meses',tags:[['tag-blue','Libre']]},{n:'Plan MAX Libre Pro',p:'$14.990',per:'x6 meses',tags:[['tag-red','⭐ Pro']]}].forEach(o=>{h+=`<div class="offer-card"><div class="offer-top"><div class="offer-name">${o.n}</div><div><div class="offer-price">${o.p}</div><div class="offer-period">${o.per}</div></div></div><div class="tags">${o.tags.map(([c,t])=>tag(c,t)).join('')}</div></div>`;});
    h+='</div>';
    h+=`<div class="warn-box"><div class="warn-icon">⚠️</div><div class="warn-text">Canal <strong>Directa</strong>: solo POSPOS · Prohibido Plan S y Plan M en Directa</div></div>`;
    h+=`<div class="divider"></div><div class="section-label">Línea adicional (referencia rápida)</div><div class="mini-grid"><div class="mini-card"><div class="mini-price">$4.990</div><div class="mini-label">Nuevo o Stock portada</div></div><div class="mini-card"><div class="mini-price">$8.990</div><div class="mini-label">No portada</div></div><div class="mini-card"><div class="mini-price">$3.990</div><div class="mini-label">Stock portada (GGTT)</div></div><div class="mini-card green"><div class="mini-price">`;
  }

  // ── MÓVIL TERRENO ─────────────────────────────────────────────────────────
  if(s.canal==='movil_t'){
    h+=`<div class="section-label">Oferta táctica terreno</div><div class="offers-grid">
    <div class="offer-card"><div class="offer-top"><div><div class="offer-name">Plan MAX M · 40% Dcto</div><div style="font-size:10px;color:#aaa;margin-top:2px">x6 meses · luego precio normal</div></div><div><div class="offer-price">$7.794</div><div class="offer-period">luego $9.743</div></div></div><div class="tags">${tag('tag-amber','📍 Solo terreno')}</div></div></div>
    <div class="divider"></div><div class="section-label">Plan especial</div>
    <div class="offer-card teal"><div class="offer-top"><div class="offer-name">👵 Plan Adulto Mayor</div><div><div class="offer-price">$3.990</div><div class="offer-period">x12 meses</div></div></div><div class="tags">${tag('tag-green','✅ Aplicable todos los canales')}</div></div>`;
  }

  // ── LÍNEA ADICIONAL ───────────────────────────────────────────────────────
  if(s.canal==='la_n_p'){
    h+=`<div class="section-label">Línea Adicional — Cliente Nuevo · Ambos portados</div>
    <table class="la-table"><thead><tr><th>Plan Base</th><th>Precio Línea Adicional</th></tr></thead><tbody>
    <tr><td>Plan S</td><td><span class="la-na">NO APLICA</span></td></tr>
    <tr><td>Plan MAX M</td><td><span class="la-na">NO APLICA</span></td></tr>
    <tr><td>Plan MAX L Libre</td><td><span class="la-price">$4.990</span></td></tr>
    <tr><td>Plan MAX XL Libre</td><td><span class="la-price">$3.990</span></td></tr>
    <tr><td>Plan MAX Libre Pro</td><td><span class="la-price">$3.990</span></td></tr>
    </tbody></table>
    <div class="warn-box" style="margin-top:10px"><div class="warn-icon">📌</div>`;
  }
  if(s.canal==='la_n_np'){
    h+=`<div class="section-label">Línea Adicional — Cliente Nuevo · Línea no portada</div>
    <table class="la-table"><thead><tr><th>Plan Base</th><th>Precio Línea Adicional</th></tr></thead><tbody>
    <tr><td>Plan S</td><td><span class="la-na">NO APLICA</span></td></tr>
    <tr><td>Plan MAX M</td><td><span class="la-na">NO APLICA</span></td></tr>
    <tr><td>Plan MAX L Libre</td><td><span class="la-price">$8.990</span></td></tr>
    <tr><td>Plan MAX XL Libre</td><td><span class="la-price">$8.990</span></td></tr>
    <tr><td>Plan MAX Libre Pro</td><td><span class="la-price">$8.990</span></td></tr>
    </tbody></table>`;
  }
  if(s.canal==='la_s'){
    h+=`<div class="section-label">Cliente Stock — Antigüedad mayor a 7 días</div><div class="offers-grid">
    <div class="offer-card blue"><div class="offer-top"><div><div class="offer-name">Línea Adicional PORTADA</div><div style="font-size:10px;color:#aaa;margin-top:2px">Independiente del plan base</div></div><div><div class="offer-price" style="color:#1D4ED8">$4.990</div></div></div><div class="tags">${tag('tag-green','✅ Todos los canales')}</div></div>
    <div class="offer-card"><div class="offer-top"><div><div class="offer-name">Línea Adicional NO PORTADA</div><div style="font-size:10px;color:#aaa;margin-top:2px">Independiente del plan base</div></div><div><div class="offer-price">$8.990</div></div></div><div class="tags">${tag('tag-green','✅ Todos los canales')}</div></div>
    </div>`;
  }
  return h;
}

// ── RENDER SCREEN ─────────────────────────────────────────────────────────────
function renderScreen(id){
  const s=SCREENS[id];if(!s)return;
  const area=document.getElementById('screen-area');
  let html='<div class="screen">';
  if(s.type==='result'){
    html+=renderResult(s);
  } else {
    html+=`<div class="qbox"><div class="qicon">${s.icon}</div><div class="qtext">${s.q}</div>${s.hint?`<div class="qhint">${s.hint}</div>`:''}</div>
    <div class="choices ${s.cols===2?'cols2':''}">`;
    s.choices.forEach(c=>{html+=`<button class="choice-btn" onclick="navigate('${c.next}')"><div class="choice-icon">${c.icon}</div><div><div class="choice-label">${c.label}</div>${c.desc?`<div class="choice-desc">${c.desc}</div>`:''}</div></button>`;});
    html+='</div>';
  }
  if(history.length>0){html+=`<div class="nav-row"><button class="btn-back" onclick="goBack()">← Volver</button><button class="btn-restart" onclick="restart()">🔄 Reiniciar</button></div>`;}
  html+='</div>';
  area.innerHTML=html;
  const bc=document.getElementById('breadcrumb');
  bc.innerHTML=[...history,current].map((id2,i,arr)=>`<span class="bc-item ${i===arr.length-1?'active':''}">${BREAD[id2]||id2}</span>`).join('');
}
function navigate(id){history.push(current);current=id;renderScreen(id);}
function goBack(){if(!history.length)return;current=history.pop();renderScreen(current);}
function restart(){history=[];current='start';renderScreen('start');}
renderScreen('start');
</script>
</body>
</html>
