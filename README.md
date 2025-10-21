<html lang="de">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>Einkaufs-Shop</title>

<!-- Favicon: Einkaufszettel -->
<link rel="icon" type="image/svg+xml"
      href='data:image/svg+xml,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><rect x="3" y="2" width="18" height="20" rx="2" fill="white" stroke="black" stroke-width="2"/><line x1="7" y1="7" x2="17" y2="7" stroke="black" stroke-width="2"/><line x1="7" y1="11" x2="17" y2="11" stroke="black" stroke-width="2"/><line x1="7" y1="15" x2="17" y2="15" stroke="black" stroke-width="2"/></svg>'>

<style>
  :root{
    --bg:#f0f3f8;
    --ribbon1:#2c3e50;
    --ribbon2:#34495e;
    --accent:#1abc9c;
    --accent2:#27ae60;
    --btn:#007bff;
    --btnh:#0056b3;
    --warn:#ff9800;
    --danger:#e74c3c;
    --card:#ffffff;
    --muted:#6b7280;
  }
  *{box-sizing:border-box}
  body{font-family:Arial,Helvetica,sans-serif;background:var(--bg);margin:0;color:#111}
  .ribbon{background:linear-gradient(90deg,var(--ribbon1),var(--ribbon2));color:#fff;position:sticky;top:0;z-index:40;box-shadow:0 2px 6px rgba(0,0,0,.25)}
  .main-menu{display:flex;align-items:center;gap:8px;padding:8px}
  .main-menu button{flex:1;padding:12px 10px;background:transparent;color:#fff;font-size:16px;font-weight:700;border:none;cursor:pointer;border-radius:8px;transition:.18s}
  .main-menu button:hover{background:var(--accent)}
  .main-menu .cart{display:flex;align-items:center;gap:8px;justify-content:center}
  #save-button{position:absolute;right:10px;top:8px;width:36px;height:36px;border-radius:50%;background:#f39c12;color:#fff;display:flex;align-items:center;justify-content:center;font-size:16px;cursor:pointer;box-shadow:0 2px 5px rgba(0,0,0,.2);transition:.12s}
  #save-button:hover{background:#e67e22;transform:scale(1.04)}
  .sub-menu{display:flex;justify-content:center;gap:8px;background:#16a085;padding:8px}
  .sub-menu button{padding:8px 14px;background:#1abc9c;color:#fff;border:none;border-radius:8px;font-size:14px;cursor:pointer}
  .content{padding:18px}
  h2{color:var(--ribbon2);margin:8px 0 12px}
  .filter-row{display:flex;gap:10px;align-items:center;flex-wrap:wrap;margin-bottom:12px}
  input,select{padding:10px;border-radius:8px;border:1px solid #cbd5e1;font-size:14px;background:#fff}
  button.primary{background:var(--btn);color:#fff;border:none;padding:10px 14px;border-radius:10px;cursor:pointer}
  button.primary:hover{background:var(--btnh)}
  button.green{background:var(--accent2);color:#fff;border:none;padding:10px 12px;border-radius:10px;cursor:pointer}
  .toast-area{position:fixed;right:18px;bottom:18px;display:flex;flex-direction:column;gap:8px;z-index:60}
  .toast{background:var(--warn);color:#fff;padding:10px 14px;border-radius:10px;box-shadow:0 2px 8px rgba(0,0,0,.22)}
  .card{background:var(--card);border-radius:12px;padding:12px;box-shadow:0 6px 18px rgba(0,0,0,.08);text-align:center}
  .card img{width:100px;height:100px;object-fit:contain;margin-bottom:8px}
  .card-grid{display:grid;grid-template-columns:repeat(6,minmax(0,1fr));gap:12px}
  .group-title{font-size:18px;font-weight:700;margin:18px 0 8px;color:var(--ribbon2);border-bottom:2px solid #e6e9ee;padding-bottom:6px}
  /* Buchstaben-Ansicht: left letter + 6-column grid */
  .letter-section{display:grid;grid-template-columns:80px 1fr;gap:12px;align-items:start;margin:6px 0}
  .letter-aside{position:sticky;top:84px;align-self:start;font-size:28px;font-weight:900;color:var(--ribbon1);display:flex;align-items:center;justify-content:center}
  .letter-grid{display:grid;grid-template-columns:repeat(6,minmax(0,1fr));gap:12px}
  .muted{color:var(--muted)}
  .small-btn{padding:6px 8px;border-radius:8px;font-size:13px}
  #gesamtpreis{font-weight:800;color:var(--danger);margin-top:10px}
  .controls-wrap{display:flex;gap:8px;flex-wrap:wrap}
  /* Upload list should be vertical (fixes display errors) */
  #produkte-liste-hochladen { display:flex; flex-direction:column; gap:12px; }
  /* Responsive adjustments */
  @media (max-width:1100px){.card-grid,.letter-grid{grid-template-columns:repeat(4,minmax(0,1fr))}}
  @media (max-width:800px){.card-grid,.letter-grid{grid-template-columns:repeat(2,minmax(0,1fr))}; .letter-aside{display:none}}
  @media (max-width:420px){.card-grid,.letter-grid{grid-template-columns:1fr}}
</style>
</head>
<body>

<!-- Ribbon -->
<div class="ribbon">
  <div class="main-menu">
    <button onclick="showRibbon('produkte')">Produkte</button>
    <button class="cart" onclick="showRibbon('warenkorb')">
      <svg viewBox="0 0 24 24" width="18" height="18" style="vertical-align:middle;margin-right:6px"><circle cx="8.5" cy="20" r="1.5"/><circle cx="17.5" cy="20" r="1.5"/><path d="M2 2h2l3.6 7.59A2 2 0 0 0 9 11h7a2 2 0 0 0 1.98-1.69L19.5 1.54A1 1 0 0 0 18 0H6" fill="none" stroke="white" stroke-width="2"/></svg>
      Einkaufswagen
    </button>
    <button onclick="showRibbon('einstellungen')">⚙️ Einstellungen</button>
    <div id="save-button" title="Shop speichern" onclick="saveAll()">💾</div>
  </div>

  <div class="sub-menu" id="submenu-produkte">
    <button onclick="showSection('produkte-alle')">Alle Produkte</button>
  </div>
  <div class="sub-menu" id="submenu-warenkorb" style="display:none">
    <button onclick="showSection('warenkorb-uebersicht')">Übersicht</button>
  </div>
  <div class="sub-menu" id="submenu-einstellungen" style="display:none">
    <button onclick="showSection('settings-allgemein')">Allgemein</button>
    <button onclick="showSection('produktgruppen')">Produktgruppen</button>
    <button onclick="showSection('produkte-hochladen')">Produkte hochladen</button>
    <button onclick="showSection('settings-speichern')">Speichern/Laden</button>
  </div>
</div>

<!-- Content -->
<div class="content">
  <!-- PRODUKTE -->
  <div id="produkte-alle">
    <h2>Alle Produkte</h2>
    <div class="filter-row">
      <input id="such-produkte" type="search" placeholder="🔎 Produkt suchen..." oninput="anzeigenProdukte()" />
      <label>
        Filter:
        <select id="filter-mode" onchange="anzeigenProdukte()">
          <option value="none">Kein Filter</option>
          <option value="buchstabe">Sortieren nach Buchstaben A–Z</option>
        </select>
      </label>
      <div style="flex:1"></div>
    </div>
    <div id="produkte-liste"></div>
  </div>

  <!-- EINKAUFSWAGEN -->
  <div id="warenkorb-uebersicht" style="display:none">
    <h2>Einkaufswagen</h2>
    <div style="display:flex;gap:8px;align-items:center;flex-wrap:wrap;margin-bottom:8px">
      <input id="such-warenkorb" type="search" placeholder="🔎 Im Warenkorb suchen..." oninput="anzeigenEinkaufswagen()" />
      <div style="flex:1"></div>
      <button class="green" onclick="exportWarenkorbXLS()">📄 Export (.xls)</button>
      <button class="green" onclick="exportWarenkorbPDF()">📝 Export (PDF)</button>
    </div>
    <div id="einkaufswagen-liste"></div>
    <div id="gesamtpreis">Gesamt: 0.00 CHF</div>
  </div>

  <!-- EINSTELLUNGEN / GRUPPEN / UPLOAD -->
  <div id="settings-allgemein" style="display:none">
    <h2>Allgemeine Einstellungen</h2>
    <p class="muted">Optionen wie Darkmode könnten hier kommen.</p>
  </div>

  <div id="produktgruppen" style="display:none">
    <h2>Produktgruppen verwalten</h2>
    <div style="display:flex;gap:8px;flex-wrap:wrap">
      <input id="gruppe-input" placeholder="Neue Gruppe" />
      <button class="primary" onclick="hinzufuegenGruppe()">➕ Speichern</button>
      <button class="primary" onclick="resetGruppeForm()">Abbrechen</button>
    </div>
    <div id="gruppen-liste" style="margin-top:12px"></div>
  </div>

  <div id="produkte-hochladen" style="display:none">
    <h2>Produkt hochladen / bearbeiten</h2>
    <div style="display:grid;grid-template-columns:1fr 1fr;gap:14px;align-items:start">
      <div class="card" style="text-align:left">
        <label>Bild<br><input id="bild-input" type="file" accept="image/*" /></label><br><br>
        <label>Produktname<br><input id="name-input" type="text" placeholder="Produktname" /></label><br><br>
        <label>Preis (CHF)<br><input id="preis-input" type="number" step="0.01" placeholder="0.00" /></label><br><br>
        <label>Gruppe<br>
          <select id="gruppe-select"><option value="">-- keine Gruppe --</option></select>
        </label>
        <div style="display:flex;gap:8px;margin-top:10px">
          <button class="primary" onclick="hinzufuegenProdukt()">Speichern</button>
          <button class="primary" onclick="resetInputs()">Zurücksetzen</button>
        </div>
      </div>
      <div>
        <h3>Produkte (bearbeiten / löschen)</h3>
        <div id="produkte-liste-hochladen" style="margin-top:8px"></div>
      </div>
    </div>
  </div>

  <div id="settings-speichern" style="display:none">
    <h2>Speichern & Laden</h2>
    <div style="display:flex;gap:8px;flex-wrap:wrap">
      <button class="primary" onclick="saveAll()">💾 Speichern</button>
      <button class="primary" onclick="loadAll()">📂 Laden</button>
      <button class="primary" onclick="clearAll()">🗑️ Alles löschen</button>
    </div>
  </div>
</div>

<!-- Toast -->
<div class="toast-area" id="toast"></div>

<!-- jsPDF für PDF-Export -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>

<script>
/* ---------------- state ---------------- */
let produkte = [];            // {id,name,preis,bild,gruppe}
let einkaufswagen = [];      // {produkt, menge}
let produktgruppen = [];     // [ "Obst", "Gemüse", ... ]
let editIndex = null;
let editGruppeIndex = null;
let saved = true;

/* ---------------- utilities ---------------- */
function notify(msg){
  const t = document.getElementById("toast");
  const el = document.createElement("div");
  el.className = "toast";
  el.textContent = msg;
  t.appendChild(el);
  setTimeout(()=>el.remove(), 3000);
}
function markDirty(){ saved = false; }
function replaceUmlautsForXLS(s){
  return String(s).replace(/ä/g,"ae").replace(/ö/g,"oe").replace(/ü/g,"ue")
                  .replace(/Ä/g,"Ae").replace(/Ö/g,"Oe").replace(/Ü/g,"Ue").replace(/ß/g,"ss");
}
function uid(){ return Date.now() + Math.floor(Math.random()*1000); }

/* ---------------- navigation ---------------- */
function showRibbon(name){
  document.getElementById("submenu-produkte").style.display = (name==='produkte') ? 'flex' : 'none';
  document.getElementById("submenu-warenkorb").style.display = (name==='warenkorb') ? 'flex' : 'none';
  document.getElementById("submenu-einstellungen").style.display = (name==='einstellungen') ? 'flex' : 'none';
  if(name==='produkte') showSection('produkte-alle');
  if(name==='warenkorb') showSection('warenkorb-uebersicht');
  if(name==='einstellungen') showSection('settings-allgemein');
}
function showSection(id){
  const sections = ['produkte-alle','warenkorb-uebersicht','settings-allgemein','produktgruppen','produkte-hochladen','settings-speichern'];
  sections.forEach(s => {
    const el = document.getElementById(s);
    if(el) el.style.display = (s===id) ? 'block' : 'none';
  });
  if(id==='produkte-alle') anzeigenProdukte();
  if(id==='warenkorb-uebersicht') anzeigenEinkaufswagen();
  if(id==='produktgruppen') anzeigenGruppen();
  if(id==='produkte-hochladen'){ anzeigenProdukteHochladen(); updateGruppeSelect(); }
}

/* ---------------- gruppen ---------------- */
function sortGroups(){ produktgruppen.sort((a,b)=>a.localeCompare(b,'de')); }
function updateGruppeSelect(){
  const sel = document.getElementById("gruppe-select");
  sel.innerHTML = '<option value="">-- keine Gruppe --</option>';
  sortGroups();
  produktgruppen.forEach(g=>{
    const opt = document.createElement("option");
    opt.value = g; opt.textContent = g;
    sel.appendChild(opt);
  });
}
function updateGruppenListe(){
  const list = document.getElementById("gruppen-liste");
  list.innerHTML = '';
  sortGroups();
  produktgruppen.forEach((g,i)=>{
    const card = document.createElement("div");
    card.className = "card";
    card.style.display = "flex"; card.style.justifyContent = "space-between"; card.style.alignItems = "center";
    card.style.marginBottom = "8px";
    card.innerHTML = `<strong>${g}</strong>`;
    const actions = document.createElement("div");
    const editBtn = document.createElement("button");
    editBtn.textContent = "✏️";
    editBtn.className = "small-btn";
    editBtn.onclick = ()=>bearbeiteGruppe(i);
    const delBtn = document.createElement("button");
    delBtn.textContent = "❌";
    delBtn.className = "small-btn";
    delBtn.onclick = ()=>entferneGruppe(i);
    actions.appendChild(editBtn); actions.appendChild(delBtn);
    card.appendChild(actions);
    list.appendChild(card);
  });
}
function hinzufuegenGruppe(){
  const input = document.getElementById("gruppe-input");
  const name = input.value.trim();
  if(!name){ notify("Gruppenname erforderlich"); return; }
  if(editGruppeIndex!==null){
    produktgruppen[editGruppeIndex] = name;
    editGruppeIndex = null;
    notify("Gruppe bearbeitet");
  } else {
    if(!produktgruppen.includes(name)) produktgruppen.push(name);
    notify("Gruppe hinzugefügt");
  }
  input.value = '';
  markDirty();
  updateGruppeSelect();
  updateGruppenListe();
  anzeigenProdukte();
}
function bearbeiteGruppe(i){
  editGruppeIndex = i;
  document.getElementById("gruppe-input").value = produktgruppen[i];
  notify("Bearbeite Gruppe");
}
function entferneGruppe(i){
  if(!confirm("Gruppe wirklich löschen?")) return;
  const name = produktgruppen[i];
  // entferne Gruppenzuordnung aus Produkten
  produkte.forEach(p => { if(p.gruppe === name) p.gruppe = ""; });
  produktgruppen.splice(i,1);
  markDirty();
  updateGruppeSelect();
  updateGruppenListe();
  anzeigenProdukte();
  anzeigenProdukteHochladen();
}
function resetGruppeForm(){ editGruppeIndex = null; document.getElementById("gruppe-input").value = ""; }

/* ---------------- produkte ---------------- */
function anzeigenProdukte(){
  const container = document.getElementById("produkte-liste");
  container.innerHTML = "";
  const search = (document.getElementById("such-produkte").value || "").toLowerCase();
  const mode = document.getElementById("filter-mode").value; // 'none' or 'buchstabe'

  // Base list filtered by search
  let list = produkte.slice();
  if(search) list = list.filter(p => p.name.toLowerCase().includes(search));

  if(mode === "buchstabe"){
    // Group by starting letter, show letter aside on left and 6-column grid
    const map = {};
    list.forEach(p => {
      const letter = (p.name && p.name.trim()[0]) ? p.name.trim()[0].toUpperCase() : "#";
      (map[letter] ||= []).push(p);
    });
    Object.keys(map).sort((a,b)=>a.localeCompare(b,'de')).forEach(letter => {
      const section = document.createElement("div");
      section.className = "letter-section";
      const aside = document.createElement("div");
      aside.className = "letter-aside";
      aside.textContent = letter;
      const grid = document.createElement("div");
      grid.className = "letter-grid";
      const arr = map[letter].slice().sort((a,b)=>a.name.localeCompare(b.name,'de'));
      arr.forEach(p => {
        const card = document.createElement("div");
        card.className = "card";
        card.innerHTML = `
          <img src="${p.bild || ''}" alt="${p.name}" />
          <div style="font-weight:700;margin:6px 0">${p.name}</div>
          <div class="muted" style="font-size:13px;margin-bottom:8px">${p.gruppe || 'Keine Gruppe'}</div>
          <div style="font-weight:700">${p.preis.toFixed(2)} CHF</div>
          <div style="margin-top:8px"><button class="small-btn" onclick="produktZumEinkaufswagenID('${p.id}')">🛒</button></div>
        `;
        grid.appendChild(card);
      });
      section.appendChild(aside);
      section.appendChild(grid);
      container.appendChild(section);
    });
    return;
  }

  // mode === none: Show products grouped by productgruppe (groups are headers A–Z)
  const groups = {};
  produkte.forEach(p => {
    const g = p.gruppe || "Andere";
    (groups[g] ||= []).push(p);
  });
  const groupNames = Object.keys(groups).sort((a,b)=>a.localeCompare(b,'de'));
  groupNames.forEach(g => {
    const title = document.createElement("div");
    title.className = "group-title";
    title.textContent = g;
    container.appendChild(title);

    const grid = document.createElement("div");
    grid.className = "card-grid";
    groups[g].sort((a,b)=>a.name.localeCompare(b.name,'de')).forEach(p => {
      const card = document.createElement("div");
      card.className = "card";
      card.innerHTML = `
        <img src="${p.bild || ''}" alt="${p.name}" />
        <div style="font-weight:700;margin:6px 0">${p.name}</div>
        <div class="muted" style="font-size:13px;margin-bottom:8px">${p.gruppe || 'Keine Gruppe'}</div>
        <div style="font-weight:700">${p.preis.toFixed(2)} CHF</div>
        <div style="margin-top:8px"><button class="small-btn" onclick="produktZumEinkaufswagenID('${p.id}')">🛒</button></div>
      `;
      grid.appendChild(card);
    });
    container.appendChild(grid);
  });
}

function anzeigenProdukteHochladen(){
  const container = document.getElementById("produkte-liste-hochladen");
  container.innerHTML = "";
  // Show products sorted by name; ensure callbacks get original indices
  const sorted = produkte.slice().sort((a,b)=>a.name.localeCompare(b.name,'de'));
  sorted.forEach(p => {
    const originalIndex = produkte.findIndex(x => x.id === p.id);
    const card = document.createElement("div");
    card.className = "card";
    card.style.textAlign = "left";
    card.style.marginBottom = "10px";
    card.innerHTML = `
      <div style="display:flex;gap:12px;align-items:center">
        <img src="${p.bild || ''}" alt="${p.name}" style="width:72px;height:72px;object-fit:contain;border-radius:8px"/>
        <div style="flex:1">
          <div style="font-weight:700">${p.name}</div>
          <div class="muted">${p.preis.toFixed(2)} CHF • ${p.gruppe || 'Keine Gruppe'}</div>
        </div>
        <div style="display:flex;flex-direction:column;gap:8px">
          <button class="small-btn" onclick="bearbeiteProdukt(${originalIndex})">✏️</button>
          <button class="small-btn" onclick="produktEntfernen(${originalIndex})">❌</button>
        </div>
      </div>
    `;
    container.appendChild(card);
  });
}

function hinzufuegenProdukt(){
  const name = (document.getElementById("name-input").value || "").trim();
  const preis = parseFloat(document.getElementById("preis-input").value);
  const gruppe = document.getElementById("gruppe-select").value || "";
  const file = document.getElementById("bild-input").files[0];

  if(!name || isNaN(preis)){ notify("Name & Preis erforderlich"); return; }

  const finishAdd = (imgData) => {
    if(editIndex !== null){
      const p = produkte[editIndex];
      p.name = name; p.preis = preis; p.gruppe = gruppe; if(imgData !== null) p.bild = imgData;
      editIndex = null;
      notify("Produkt aktualisiert");
    } else {
      produkte.push({ id: String(uid()), name, preis, bild: imgData || "", gruppe });
      notify("Produkt hinzugefügt");
    }
    markDirty();
    resetInputs();
    anzeigenProdukteHochladen();
    anzeigenProdukte();
  };

  if(file){
    const reader = new FileReader();
    reader.onload = e => finishAdd(e.target.result);
    reader.readAsDataURL(file);
  } else {
    // No file chosen: allow update without new image, or new product without image
    finishAdd(null);
  }
}

function bearbeiteProdukt(i){
  if(i < 0 || i >= produkte.length) return;
  editIndex = i;
  const p = produkte[i];
  document.getElementById("name-input").value = p.name;
  document.getElementById("preis-input").value = p.preis;
  document.getElementById("gruppe-select").value = p.gruppe || "";
  showSection('produkte-hochladen');
  notify("Produkt bearbeiten");
}

function produktEntfernen(i){
  if(!confirm("Produkt wirklich löschen?")) return;
  produkte.splice(i,1);
  markDirty();
  anzeigenProdukteHochladen();
  anzeigenProdukte();
}

/* ---------------- Einkaufswagen ---------------- */
function produktZumEinkaufswagenID(id){
  const p = produkte.find(x => x.id === id);
  if(!p){ notify("Produkt nicht gefunden"); return; }
  const existing = einkaufswagen.find(it => it.produkt.id === id);
  if(existing){ existing.menge += 1; } else { einkaufswagen.push({ produkt: p, menge: 1 }); }
  markDirty();
  notify("Produkt in Warenkorb");
  anzeigenEinkaufswagen();
}

function anzeigenEinkaufswagen(){
  const c = document.getElementById("einkaufswagen-liste");
  c.innerHTML = "";
  const search = (document.getElementById("such-warenkorb").value || "").toLowerCase();

  // groups in cart
  const groups = {};
  einkaufswagen.forEach((it, idx) => {
    if(search && !it.produkt.name.toLowerCase().includes(search)) return;
    const g = it.produkt.gruppe || "Andere";
    (groups[g] ||= []).push({ item: it, idx });
  });

  const groupNames = Object.keys(groups).sort((a,b)=>a.localeCompare(b,'de'));
  let gesamt = 0;
  groupNames.forEach(g => {
    const title = document.createElement("div");
    title.className = "group-title";
    title.textContent = g;
    c.appendChild(title);
    const grid = document.createElement("div");
    grid.className = "card-grid";
    groups[g].forEach(({ item, idx }) => {
      gesamt += item.produkt.preis * item.menge;
      const card = document.createElement("div");
      card.className = "card";
      card.innerHTML = `
        <img src="${item.produkt.bild || ''}" alt="${item.produkt.name}" />
        <div style="font-weight:700;margin:6px 0">${item.produkt.name}</div>
        <div class="muted">${item.produkt.preis.toFixed(2)} CHF × ${item.menge}</div>
        <div style="margin-top:8px">
          <button class="small-btn" onclick="mengeAendern(${idx},-1)">➖</button>
          <button class="small-btn" onclick="mengeAendern(${idx},1)">➕</button>
          <button class="small-btn" onclick="entferneAusWarenkorb(${idx})">❌</button>
        </div>
      `;
      grid.appendChild(card);
    });
    c.appendChild(grid);
  });
  document.getElementById("gesamtpreis").textContent = "Gesamt: " + gesamt.toFixed(2) + " CHF";
}

function mengeAendern(idx, delta){
  if(!einkaufswagen[idx]) return;
  einkaufswagen[idx].menge += delta;
  if(einkaufswagen[idx].menge <= 0) einkaufswagen.splice(idx,1);
  markDirty();
  anzeigenEinkaufswagen();
}
function entferneAusWarenkorb(idx){
  einkaufswagen.splice(idx,1);
  markDirty();
  anzeigenEinkaufswagen();
}

/* ---------------- Export XLS (TSV) ---------------- */
function exportWarenkorbXLS(){
  if(einkaufswagen.length === 0){ notify("Warenkorb leer"); return; }
  const groups = {};
  einkaufswagen.forEach(it => {
    const g = it.produkt.gruppe || "Andere";
    (groups[g] ||= []).push(it);
  });
  const groupNames = Object.keys(groups).sort((a,b)=>a.localeCompare(b,'de'));
  const lines = [];
  lines.push("EINKAUFSZETTEL");
  lines.push("");
  lines.push("Gruppe\tProdukt\tMenge\tEinzelpreis (CHF)\tGesamt (CHF)");
  groupNames.forEach(g => {
    lines.push(`${replaceUmlautsForXLS(g)}\t\t\t\t`);
    groups[g].forEach(it => {
      const total = (it.produkt.preis * it.menge).toFixed(2);
      lines.push(`\t${replaceUmlautsForXLS(it.produkt.name)}\t${it.menge}\t${it.produkt.preis.toFixed(2)}\t${total}`);
    });
    lines.push("");
  });
  const blob = new Blob([lines.join("\n")], { type: "application/vnd.ms-excel" });
  const a = document.createElement("a");
  a.href = URL.createObjectURL(blob);
  a.download = "Einkaufszettel.xls";
  a.click();
  URL.revokeObjectURL(a.href);
  notify("XLS exportiert");
}

/* ---------------- Export PDF (no prices) ---------------- */
function exportWarenkorbPDF(){
  if(einkaufswagen.length === 0){ notify("Warenkorb leer"); return; }
  const { jsPDF } = window.jspdf;
  const doc = new jsPDF({ unit: "pt", format: "a4" });
  const left = 40, top = 50, line = 18;
  let y = top;
  doc.setFontSize(16);
  doc.text("Einkaufszettel", left, y);
  y += 26;
  doc.setFontSize(12);
  doc.text("Produkt", left, y);
  doc.text("Gruppe", left + 260, y);
  doc.text("Menge", left + 460, y);
  y += 10;
  doc.setLineWidth(0.5);
  doc.line(left, y, left + 520, y);
  y += 16;

  const groups = {};
  einkaufswagen.forEach(it => {
    const g = it.produkt.gruppe || "Andere";
    (groups[g] ||= []).push(it);
  });
  const groupNames = Object.keys(groups).sort((a,b)=>a.localeCompare(b,'de'));
  groupNames.forEach(g => {
    const items = groups[g].slice().sort((a,b)=>a.produkt.name.localeCompare(b.produkt.name,'de'));
    items.forEach(it => {
      if(y > 800){ doc.addPage(); y = top; }
      doc.text(it.produkt.name, left, y);
      doc.text(g, left + 260, y);
      doc.text(String(it.menge), left + 460, y);
      y += line;
    });
    y += 6;
  });

  doc.save("Einkaufszettel.pdf");
  notify("PDF exportiert");
}

/* ---------------- Speichern / Laden / Clear ---------------- */
function saveAll(){
  localStorage.setItem("produkte", JSON.stringify(produkte));
  localStorage.setItem("einkaufswagen", JSON.stringify(einkaufswagen));
  localStorage.setItem("produktgruppen", JSON.stringify(produktgruppen));
  saved = true;
  notify("Daten gespeichert");
}
function loadAll(){
  try{
    produkte = JSON.parse(localStorage.getItem("produkte") || "[]");
    einkaufswagen = JSON.parse(localStorage.getItem("einkaufswagen") || "[]");
    produktgruppen = JSON.parse(localStorage.getItem("produktgruppen") || "[]");
  }catch(e){
    produkte = []; einkaufswagen = []; produktgruppen = [];
  }
  sortGroups();
  updateGruppeSelect();
  updateGruppenListe();
  anzeigenProdukte();
  anzeigenProdukteHochladen();
  anzeigenEinkaufswagen();
  saved = true;
  notify("Daten geladen");
}
function clearAll(){
  if(!confirm("Wirklich alles löschen?")) return;
  localStorage.clear();
  produkte = []; einkaufswagen = []; produktgruppen = [];
  saved = false;
  updateGruppeSelect();
  updateGruppenListe();
  anzeigenProdukte();
  anzeigenProdukteHochladen();
  anzeigenEinkaufswagen();
  notify("Alles gelöscht");
}

/* ---------------- Close prompt ---------------- */
window.onbeforeunload = function(e){
  if(!saved){
    e.preventDefault();
    e.returnValue = "";
    return "";
  }
};

/* ---------------- helper ---------------- */
function resetInputs(){
  document.getElementById("bild-input").value = "";
  document.getElementById("name-input").value = "";
  document.getElementById("preis-input").value = "";
  document.getElementById("gruppe-select").value = "";
  editIndex = null;
}

/* ---------------- init ---------------- */
window.onload = function(){
  loadAll();
  showRibbon('produkte');
  // ensure selects and lists are up to date
  updateGruppeSelect();
  updateGruppenListe();
  anzeigenProdukte();
  anzeigenProdukteHochladen();
  anzeigenEinkaufswagen();
};

</script>
</body>
</html>




