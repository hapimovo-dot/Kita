[index.html](https://github.com/user-attachments/files/28649686/index.html)
<!DOCTYPE html>
<html lang="de">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="default">
<meta name="apple-mobile-web-app-title" content="Kita Beobachtung">
<title>Kita Beobachtungssystem</title>
<style>
*{box-sizing:border-box;margin:0;padding:0}
body{font-family:-apple-system,BlinkMacSystemFont,'Segoe UI',sans-serif;background:#F5F5F7;color:#1D1D1F;min-height:100vh}
.app{max-width:680px;margin:0 auto;padding:1rem}
.topbar{display:flex;align-items:center;justify-content:space-between;padding:0.75rem 1rem;background:#fff;border:1px solid #E5E5EA;border-radius:14px;margin-bottom:1rem;box-shadow:0 1px 3px rgba(0,0,0,0.06)}
.appname{font-size:15px;font-weight:600;color:#1D1D1F}
.lang-toggle{display:flex;gap:4px}
.lang-btn{padding:4px 10px;font-size:12px;border:1px solid #C7C7CC;border-radius:8px;cursor:pointer;background:transparent;color:#6E6E73}
.lang-btn.active{background:#F2F2F7;color:#1D1D1F;font-weight:500}
.tabs{display:flex;gap:6px;margin-bottom:1rem;flex-wrap:wrap}
.tab{padding:7px 16px;font-size:13px;border:1px solid #E5E5EA;border-radius:10px;cursor:pointer;background:#fff;color:#6E6E73}
.tab.active{background:#fff;border-color:#1D1D1F;color:#1D1D1F;font-weight:500}
.panel{display:none}.panel.active{display:block}
.child-selector{display:flex;gap:8px;margin-bottom:1rem;align-items:center;flex-wrap:wrap}
.child-selector select{flex:1;min-width:160px;padding:8px 10px;border:1px solid #E5E5EA;border-radius:10px;background:#fff;font-size:14px;color:#1D1D1F}
.btn{padding:8px 16px;font-size:13px;font-weight:500;border:1px solid #E5E5EA;border-radius:10px;cursor:pointer;background:#fff;color:#1D1D1F;white-space:nowrap}
.btn:active{background:#F2F2F7}
.btn-primary{background:#1D1D1F;color:#fff;border-color:#1D1D1F}
.btn-primary:active{background:#3A3A3C}
.stats-row{display:grid;grid-template-columns:repeat(3,1fr);gap:8px;margin-bottom:1rem}
.stat-card{background:#fff;border-radius:12px;padding:0.75rem;text-align:center;border:1px solid #E5E5EA}
.stat-num{font-size:22px;font-weight:600;color:#1D1D1F}
.stat-label{font-size:11px;color:#6E6E73;margin-top:2px}
.section-card{background:#fff;border:1px solid #E5E5EA;border-radius:14px;margin-bottom:0.75rem;overflow:hidden}
.section-header{display:flex;align-items:center;justify-content:space-between;padding:0.85rem 1rem;cursor:pointer;user-select:none}
.section-title{font-size:14px;font-weight:500;display:flex;align-items:center;gap:8px;flex:1}
.section-badge{font-size:11px;padding:2px 8px;border-radius:20px;background:#F2F2F7;color:#6E6E73}
.section-badge.done{background:#D1F2D9;color:#1A7F3C}
.chevron{font-size:14px;color:#6E6E73;transition:transform 0.2s;flex-shrink:0}
.section-body{display:none;padding:0 1rem 0.75rem;border-top:1px solid #F2F2F7}
.section-body.open{display:block}
.item-row{padding:8px 0;border-bottom:1px solid #F2F2F7}
.item-row:last-child{border-bottom:none}
.item-row.observed .item-text{color:#AEAEB2}
.item-top{display:flex;align-items:flex-start;gap:10px}
.item-text{flex:1;font-size:13px;line-height:1.5;color:#1D1D1F}
.item-controls{display:flex;gap:4px;flex-shrink:0;margin-top:1px}
.status-btn{padding:3px 9px;font-size:11px;border:1px solid #E5E5EA;border-radius:8px;cursor:pointer;background:#fff;color:#6E6E73;font-weight:500}
.status-btn.ja{background:#D1F2D9;color:#1A7F3C;border-color:#A8E6B8}
.status-btn.manchmal{background:#FFF3D6;color:#7D4E00;border-color:#FFD97A}
.status-btn.nein{background:#FFE5E5;color:#A32D2D;border-color:#FFBEBE}
.note-area{width:100%;margin-top:6px;font-size:12px;padding:7px 9px;border:1px solid #E5E5EA;border-radius:8px;background:#F9F9F9;color:#1D1D1F;resize:vertical;min-height:40px;font-family:inherit}
.filter-bar{display:flex;gap:6px;margin-bottom:0.75rem;flex-wrap:wrap;align-items:center}
.filter-lbl{font-size:12px;color:#6E6E73}
.filter-btn{padding:4px 12px;font-size:12px;border:1px solid #E5E5EA;border-radius:20px;cursor:pointer;background:#fff;color:#6E6E73}
.filter-btn.active{background:#F2F2F7;color:#1D1D1F;font-weight:500}
.ai-panel{background:#fff;border:1px solid #E5E5EA;border-radius:14px;padding:1rem}
.ai-input{width:100%;font-size:14px;padding:10px;border:1px solid #E5E5EA;border-radius:10px;background:#F9F9F9;color:#1D1D1F;resize:vertical;min-height:90px;margin-bottom:10px;font-family:inherit}
.ai-btns{display:flex;gap:8px;flex-wrap:wrap}
.ai-result{background:#F9F9F9;border-radius:10px;padding:0.85rem;font-size:13px;line-height:1.65;margin-top:0.85rem;white-space:pre-wrap;color:#1D1D1F;border:1px solid #E5E5EA}
.report-out{background:#F9F9F9;border-radius:10px;padding:1rem;font-size:13px;line-height:1.8;white-space:pre-wrap;margin-top:0.85rem;color:#1D1D1F;border:1px solid #E5E5EA}
.info-box{padding:0.6rem 0.85rem;background:#F2F2F7;border-left:3px solid #C7C7CC;border-radius:0 8px 8px 0;font-size:12px;color:#6E6E73;margin-bottom:0.85rem;line-height:1.5}
.report-btns{display:flex;gap:8px;margin-bottom:0.75rem;flex-wrap:wrap}
.modal-bg{display:none;position:fixed;inset:0;background:rgba(0,0,0,0.4);z-index:100;align-items:flex-end;justify-content:center;padding:0}
.modal-bg.open{display:flex}
.modal{background:#fff;border-radius:20px 20px 0 0;padding:1.5rem 1.25rem 2rem;width:100%;max-width:680px;border:1px solid #E5E5EA}
@media(min-width:500px){.modal-bg{align-items:center}.modal{border-radius:20px;max-width:360px}}
.modal h3{font-size:16px;font-weight:600;margin-bottom:1rem}
.modal-field{margin-bottom:12px}
.modal-field label{display:block;font-size:12px;color:#6E6E73;margin-bottom:5px;font-weight:500}
.modal-field input,.modal-field select{width:100%;padding:9px 11px;border:1px solid #E5E5EA;border-radius:10px;font-size:14px;background:#fff;color:#1D1D1F;font-family:inherit}
.dob-row{display:flex;gap:8px}
.dob-row select{flex:1}
.modal-btns{display:flex;gap:8px;justify-content:flex-end;margin-top:1rem}
.loading-spinner{display:inline-block;width:14px;height:14px;border:2px solid #E5E5EA;border-top-color:#1D1D1F;border-radius:50%;animation:spin 0.7s linear infinite;vertical-align:-2px;margin-right:6px}
@keyframes spin{to{transform:rotate(360deg)}}
.missing-body{padding:0.85rem 0;font-size:13px;color:#6E6E73;line-height:1.5}
</style>
</head>
<body>
<div class="app">
  <div class="topbar">
    <span class="appname" id="appname">🌱 Kita Beobachtung</span>
    <div class="lang-toggle">
      <button class="lang-btn active" onclick="setLang('de')">DE</button>
      <button class="lang-btn" onclick="setLang('zh')">中文</button>
    </div>
  </div>

  <div class="child-selector">
    <select id="childSelect" onchange="loadChild()"></select>
    <button class="btn btn-primary" onclick="openAddChild()" id="btn-add-child">+ Kind</button>
  </div>

  <div class="stats-row">
    <div class="stat-card"><div class="stat-num" id="stat-total">0</div><div class="stat-label" id="stat-total-lbl">Kompetenzen</div></div>
    <div class="stat-card"><div class="stat-num" id="stat-done">0</div><div class="stat-label" id="stat-done-lbl">Beobachtet</div></div>
    <div class="stat-card"><div class="stat-num" id="stat-pct">0%</div><div class="stat-label" id="stat-pct-lbl">Fortschritt</div></div>
  </div>

  <div class="tabs">
    <button class="tab active" onclick="switchTab('observe')" id="tab-observe">Beobachtung</button>
    <button class="tab" onclick="switchTab('ai')" id="tab-ai">KI-Assistent</button>
    <button class="tab" onclick="switchTab('report')" id="tab-report">Bericht</button>
  </div>

  <div class="panel active" id="panel-observe">
    <div class="filter-bar">
      <span class="filter-lbl" id="filter-lbl">Anzeigen:</span>
      <button class="filter-btn active" onclick="setFilter('all')" id="f-all">Alle</button>
      <button class="filter-btn" onclick="setFilter('pending')" id="f-pending">Noch nicht</button>
      <button class="filter-btn" onclick="setFilter('done')" id="f-done">Beobachtet</button>
    </div>
    <div id="sections-container"></div>
  </div>

  <div class="panel" id="panel-ai">
    <div class="ai-panel">
      <div class="info-box" id="ai-info">Beschreiben Sie eine Beobachtung – die KI findet passende Kompetenzen und formuliert professionellen Text.</div>
      <textarea class="ai-input" id="ai-input" placeholder="z.B. heute hat sie anderen Kindern beim Aufräumen geholfen..."></textarea>
      <div class="ai-btns">
        <button class="btn btn-primary" onclick="aiMatch()" id="btn-ai-match">Kompetenz zuordnen ↗</button>
        <button class="btn" onclick="aiProfessionalize()" id="btn-ai-prof">Professionalisieren ↗</button>
      </div>
      <div class="ai-result" id="ai-result" style="display:none"></div>
    </div>
  </div>

  <div class="panel" id="panel-report">
    <div class="report-btns">
      <button class="btn btn-primary" onclick="generateReport('de')" id="btn-rep-de">Bericht DE ↗</button>
      <button class="btn" onclick="generateReport('zh')" id="btn-rep-zh">中文報告 ↗</button>
      <button class="btn" onclick="copyReport()" id="btn-copy">Kopieren</button>
    </div>
    <div class="report-out" id="report-out" style="display:none"></div>
  </div>
</div>

<!-- MODAL -->
<div class="modal-bg" id="modal-bg">
  <div class="modal">
    <h3 id="modal-title">Neues Kind hinzufügen</h3>
    <div class="modal-field">
      <label id="lbl-name">Name</label>
      <input type="text" id="child-name-input" placeholder="z.B. Lena M." />
    </div>
    <div class="modal-field">
      <label id="lbl-dob">Geburtsdatum (Monat / Jahr)</label>
      <div class="dob-row">
        <select id="dob-month"><option value="">Monat</option></select>
        <select id="dob-year"><option value="">Jahr</option></select>
      </div>
    </div>
    <div class="modal-btns">
      <button class="btn" onclick="closeModal()" id="btn-cancel">Abbrechen</button>
      <button class="btn btn-primary" onclick="addChild()" id="btn-save">Speichern</button>
    </div>
  </div>
</div>

<script>
const TR={
  de:{appname:"🌱 Kita Beobachtung",addChild:"+ Kind",observe:"Beobachtung",ai:"KI-Assistent",report:"Bericht",filterAll:"Alle",filterPending:"Noch nicht",filterDone:"Beobachtet",filterLbl:"Anzeigen:",statTotal:"Kompetenzen",statDone:"Beobachtet",statPct:"Fortschritt",aiInfo:"Beschreiben Sie eine Beobachtung – die KI findet passende Kompetenzen und formuliert professionellen Text.",aiPlaceholder:"z.B. heute hat sie anderen Kindern beim Aufräumen geholfen...",aiMatch:"Kompetenz zuordnen ↗",aiProf:"Professionalisieren ↗",repDe:"Bericht DE ↗",repZh:"中文報告 ↗",copy:"Kopieren",modalTitle:"Neues Kind hinzufügen",lblName:"Name",lblDob:"Geburtsdatum (Monat / Jahr)",cancel:"Abbrechen",save:"Speichern",selectChild:"Kind auswählen...",noChild:"Kein Kind ausgewählt",notePlaceholder:"Bemerkung...",months:["Januar","Februar","März","April","Mai","Juni","Juli","August","September","Oktober","November","Dezember"]},
  zh:{appname:"🌱 幼兒園觀察系統",addChild:"+ 新增",observe:"觀察記錄",ai:"AI 助理",report:"報告",filterAll:"全部",filterPending:"未觀察",filterDone:"已觀察",filterLbl:"顯示：",statTotal:"能力項目",statDone:"已觀察",statPct:"進度",aiInfo:"輸入觀察描述，AI 會找出對應能力項目並改寫成專業教師文字。",aiPlaceholder:"例如：今天她主動幫其他小朋友整理玩具…",aiMatch:"比對能力項目 ↗",aiProf:"專業化改寫 ↗",repDe:"德文報告 ↗",repZh:"中文報告 ↗",copy:"複製",modalTitle:"新增兒童",lblName:"姓名",lblDob:"出生年月",cancel:"取消",save:"儲存",selectChild:"選擇兒童...",noChild:"尚未選擇兒童",notePlaceholder:"備注...",months:["1月","2月","3月","4月","5月","6月","7月","8月","9月","10月","11月","12月"]}
};

const DOMAINS=[
  {id:"NUT",de:"Natur · Umwelt · Technik",zh:"自然・環境・技術",items:[
    {id:"NUT01",de:"Neugierig und aufmerksam sein, Interesse an seiner Umwelt zeigen",zh:"對環境充滿好奇心，對動植物、科技、自然現象感興趣"},
    {id:"NUT02",de:"Dazu Fragen stellen",zh:"主動提問"},
    {id:"NUT03",de:"Mit Freude und Ausdauer Dinge untersuchen – allein oder in der Gruppe",zh:"獨自或與他人一起持續探索事物"},
    {id:"NUT04",de:"Naturbegriffe kennen (Tiere, Pflanzen)",zh:"認識自然相關詞彙（動植物）"},
    {id:"NUT05",de:"Dinge aus der Natur nach Kategorien ordnen",zh:"對自然物品進行分類整理"},
    {id:"NUT06",de:"Fundstücke aus der Natur sammeln",zh:"收集自然物品"},
    {id:"NUT07",de:"Naturereignisse kennen (Wetter, Jahreszeiten)",zh:"認識天氣與四季等自然現象"},
    {id:"NUT08",de:"Technische Einrichtungen kennen (Ampeln, Verkehrsmittel, Haushaltsgeräte)",zh:"認識生活中的技術設施"},
    {id:"NUT09",de:"Technische Geräte bedienen können",zh:"能操作技術設備"},
    {id:"NUT10",de:"Bauwerke oder Maschinen konstruieren",zh:"能建造或組裝結構與機器"},
    {id:"NUT11",de:"Lust am Forschen und Experimentieren",zh:"喜歡探究和實驗"},
    {id:"NUT12",de:"Erklärungsversuche machen, Vermutungen anstellen, eigene Antworten finden",zh:"嘗試解釋現象、提出假設、找到自己的答案"},
    {id:"NUT13",de:"Eigene Experimente entwerfen",zh:"能自行設計實驗"},
    {id:"NUT14",de:"Erfahrungen aufzeichnen und dokumentieren",zh:"記錄觀察經驗"},
    {id:"NUT15",de:"Einfache Ursache-Wirkungszusammenhänge kennen",zh:"理解簡單的因果關係"},
    {id:"NUT16",de:"Ökologisches Grundverständnis entwickeln",zh:"建立基本的生態概念"},
    {id:"NUT17",de:"Verantwortung für Pflanzen und Tiere übernehmen",zh:"對植物和動物負責任"},
    {id:"NUT18",de:"Verantwortung für die Natur übernehmen (z.B. Müll)",zh:"對自然環境負責（如垃圾處理）"},
    {id:"NUT19",de:"Ursachen und Folgen für Umweltverschmutzung kennen",zh:"了解環境污染的原因與後果"},
    {id:"NUT20",de:"Gefahren beim Umgang mit Natur und Technik kennen",zh:"認識接觸自然和技術時的安全危險"}
  ]},
  {id:"SOZ",de:"Soziales · Kulturelles Leben · Emotionales Verhalten",zh:"社會文化生活與情緒行為",items:[
    {id:"SOZ01",de:"Lachen, lautieren, Blickkontakt halten, freudige Bewegungen zeigen",zh:"微笑、發聲、保持眼神接觸、表現愉快的動作"},
    {id:"SOZ02",de:"Neugierig und offen sein",zh:"好奇心強、開放"},
    {id:"SOZ03",de:"Bring- und Abholsituation bewältigen",zh:"能適應接送情況"},
    {id:"SOZ04",de:"Begrüßung und Verabschiedung verstehen, winken",zh:"理解問候和道別，會揮手"},
    {id:"SOZ05",de:"Die Bedeutung von 'nein' verstehen",zh:"理解「不」的含義"},
    {id:"SOZ06",de:"Mit anderen am Tisch sitzen",zh:"能與他人同坐一桌"},
    {id:"SOZ07",de:"An Kinderreimen, Fingerspielen, rhythmischen Spielen teilnehmen",zh:"參與童謠、手指遊戲、節奏遊戲"},
    {id:"SOZ08",de:"An von Erwachsenen geleiteten Spielen teilnehmen",zh:"參與由成人引導的遊戲"},
    {id:"SOZ09",de:"Parallel spielen (neben anderen Kindern)",zh:"平行遊戲"},
    {id:"SOZ10",de:"Miteinander spielen: sozialen Kontakt beginnen, fortführen und beenden",zh:"能主動開始、維持和結束社交互動"},
    {id:"SOZ11",de:"Kompromisse mit Hilfe von Erwachsenen schließen",zh:"在成人協助下達成妥協"},
    {id:"SOZ12",de:"Spielsachen mit anderen teilen",zh:"能與他人分享玩具"},
    {id:"SOZ13",de:"Warten können bis es dran ist",zh:"能等待輪到自己"},
    {id:"SOZ14",de:"Sich alleine beschäftigen können",zh:"能獨立自娛"},
    {id:"SOZ15",de:"Rollenspiele planen und durchführen",zh:"計劃並執行角色扮演遊戲"},
    {id:"SOZ16",de:"Bei häuslichen Tätigkeiten mithelfen, Tätigkeiten Erwachsener nachmachen",zh:"協助家務、模仿成人行為"},
    {id:"SOZ17",de:"Um Hilfe bitten können",zh:"能開口求助"},
    {id:"SOZ18",de:"Verantwortungsgefühl für sich selbst und seine Sachen haben",zh:"對自己和自己物品有責任感"},
    {id:"SOZ19",de:"Sich bei täglichen Ärgernissen beruhigen lassen",zh:"在日常小困擾後能被安撫"},
    {id:"SOZ20",de:"Emotionen selbst regulieren können",zh:"能自我調節情緒"},
    {id:"SOZ21",de:"Bedürfnisse, Interessen und Gefühle ausdrücken",zh:"能表達自己的需求、興趣和感受"},
    {id:"SOZ22",de:"Selbstvertrauen haben, Vertrauen in eigene Kräfte entwickeln",zh:"有自信，相信自己的能力"},
    {id:"SOZ23",de:"Stolz auf sich sein",zh:"對自己感到驕傲"},
    {id:"SOZ24",de:"Wissen, dass es richtig ist 'nein' zu sagen",zh:"知道說「不」來保護自己是正確的"},
    {id:"SOZ25",de:"Ein 'nein' akzeptieren",zh:"能接受他人說「不」"},
    {id:"SOZ26",de:"Erwartungen und Gefühle anderer wahrnehmen und achten",zh:"能察覺並尊重他人的期望和感受"},
    {id:"SOZ27",de:"Eigene Familie und Familienkultur kennen",zh:"了解自己的家庭和家庭文化"},
    {id:"SOZ28",de:"Eigene Adresse kennen",zh:"知道自己的住址"},
    {id:"SOZ29",de:"Sich zur Kitagruppe zugehörig fühlen",zh:"對幼兒園團體有歸屬感"},
    {id:"SOZ30",de:"Gemeinsamkeiten und Unterschiede wahrnehmen",zh:"能察覺自己與他人的異同"},
    {id:"SOZ31",de:"Zusammenarbeiten können, von anderen lernen",zh:"能合作，向他人學習"},
    {id:"SOZ32",de:"Regeln des Zusammenlebens kennen und anerkennen",zh:"了解並遵守共同生活規則"},
    {id:"SOZ33",de:"Sicheres Verhalten im Straßenverkehr",zh:"交通安全行為"},
    {id:"SOZ34",de:"Gefühle mit Worten beschreiben können",zh:"能用語言描述感受"},
    {id:"SOZ35",de:"Sich an Regelspielen beteiligen",zh:"參與規則遊戲"},
    {id:"SOZ36",de:"Im Spiel verlieren können",zh:"能接受在遊戲中輸"},
    {id:"SOZ37",de:"Über unerfreuliche Ereignisse berichten können",zh:"能談論不愉快的經歷"},
    {id:"SOZ38",de:"Eigene Fehler zugeben können",zh:"能承認自己的錯誤"},
    {id:"SOZ39",de:"Einfühlungsvermögen – 'Entschuldigung' verstehen und meinen",zh:"培養同理心，真正理解「對不起」"},
    {id:"SOZ40",de:"Sympathie und Mitgefühl mit traurigen Kindern zeigen",zh:"對難過的孩子表現同情與安慰"},
    {id:"SOZ41",de:"Konflikte aushandeln und Kompromisse schließen",zh:"能協商衝突並達成妥協"},
    {id:"SOZ42",de:"Empathisches Verhalten: anderen zuhören, sich einfühlen",zh:"有同理行為：傾聽他人、設身處地"},
    {id:"SOZ43",de:"Verschiedenheit von Menschen anerkennen",zh:"接受人與人之間的差異"},
    {id:"SOZ44",de:"Kinderrechte kennen und für sich eintreten",zh:"了解兒童權利並敢於維護"},
    {id:"SOZ45",de:"Eingreifen, wenn jemand geärgert wird",zh:"當有人受欺負時敢於介入"}
  ]},
  {id:"MAT",de:"Mathematik",zh:"數學",items:[
    {id:"MAT01",de:"Objektpermanenz verstehen",zh:"理解物體恆存"},
    {id:"MAT02",de:"Freude am Sortieren, Muster legen",zh:"喜歡排序和製作圖案"},
    {id:"MAT03",de:"Groß/Klein, keine/viele verstehen",zh:"理解大/小、沒有/很多"},
    {id:"MAT04",de:"Interesse an Zahlen zeigen",zh:"對數字感興趣"},
    {id:"MAT05",de:"Sein Alter kennen",zh:"知道自己的年齡"},
    {id:"MAT06",de:"Mathematik zur Strukturierung sozialer Situationen nutzen",zh:"用數學概念處理社交情境（分享、輪流）"},
    {id:"MAT07",de:"Größen- und Mengenvergleich",zh:"比較大小與數量"},
    {id:"MAT08",de:"Anzahl der Körperteile kennen",zh:"知道身體各部位的數量"},
    {id:"MAT09",de:"Zählen können (in verschiedenen Sprachen)",zh:"能數數（不同語言）"},
    {id:"MAT10",de:"Stück-für-Stück Zuordnung beim Zählen",zh:"一對一對應點數"},
    {id:"MAT11",de:"Mengenverständnis (z.B. beim Tischdecken)",zh:"理解數量概念"},
    {id:"MAT12",de:"Mengen vergleichen (mehr, weniger, gleich viel)",zh:"比較數量（多、少、一樣多）"},
    {id:"MAT13",de:"Addieren können",zh:"能做加法"},
    {id:"MAT14",de:"Kardinal- und Ordinalzahlen kennen",zh:"認識基數和序數"},
    {id:"MAT15",de:"Eigene Hausnummer kennen",zh:"知道自己的門牌號碼"},
    {id:"MAT16",de:"Dinge nach Form, Größe, Gewicht, Farbe vergleichen und ordnen",zh:"按形狀、大小、重量、顏色分類排序"},
    {id:"MAT17",de:"Zeit- und Maßeinheiten kennen",zh:"認識時間和量度單位"},
    {id:"MAT18",de:"Messgeräte kennen (Uhr, Waage, Kalender)",zh:"認識測量工具"},
    {id:"MAT19",de:"Den eigenen Geburtstag kennen",zh:"知道自己的生日"},
    {id:"MAT20",de:"Geometrische Formen kennen",zh:"認識幾何圖形"},
    {id:"MAT21",de:"Zeitverständnis entwickeln (heute/morgen/gestern, Uhrzeit)",zh:"建立時間概念"},
    {id:"MAT22",de:"Verständnis von Gewicht entwickeln",zh:"建立重量概念"},
    {id:"MAT23",de:"Verständnis im Umgang mit Geld entwickeln",zh:"建立金錢使用概念"},
    {id:"MAT24",de:"Grundlegende Kenntnisse über Gebrauch eines Computers",zh:"具備基本電腦使用知識"},
    {id:"MAT25",de:"Interesse an Rätseln und Denkaufgaben",zh:"喜歡謎題和思考任務"},
    {id:"MAT26",de:"Zahlensymbole kennen (verschiedener Kulturen)",zh:"認識數字符號（不同文化）"},
    {id:"MAT27",de:"Subtrahieren können",zh:"能做減法"}
  ]},
  {id:"GES",de:"Gesundheit · Motorik · Wahrnehmung",zh:"健康・動作・感知",items:[
    {id:"GES01",de:"Frei sitzen mit sicherer Gleichgewichtskontrolle",zh:"能安全地自行坐立並保持平衡"},
    {id:"GES02",de:"Kriechen, robben oder krabbeln",zh:"能爬行"},
    {id:"GES03",de:"Frei gehen und Gleichgewicht kontrollieren",zh:"能自由行走並控制平衡"},
    {id:"GES04",de:"Dinge vom Boden aufheben ohne Gleichgewicht zu verlieren",zh:"能從地上撿物品而不失去平衡"},
    {id:"GES05",de:"Sicher laufen und dabei etwas tragen",zh:"能安全跑動並同時攜帶物品"},
    {id:"GES06",de:"Treppen auf- und absteigen",zh:"能上下樓梯"},
    {id:"GES07",de:"Einen Ball mit dem Fuß schießen",zh:"能用腳踢球"},
    {id:"GES08",de:"Beidbeinig hüpfen und springen",zh:"能雙腳跳躍"},
    {id:"GES09",de:"Über ein Hindernis springen",zh:"能跳過障礙物"},
    {id:"GES10",de:"Rückwärts laufen",zh:"能向後跑"},
    {id:"GES11",de:"Fahrzeuge sicher bewegen",zh:"能安全操控騎乘玩具"},
    {id:"GES12",de:"Auf einem Bein stehen und hüpfen",zh:"能單腳站立和跳躍"},
    {id:"GES13",de:"Auf Gerüste klettern",zh:"能攀爬架構"},
    {id:"GES14",de:"Ball fangen",zh:"能接球"},
    {id:"GES15",de:"Purzelbaum, Hampelmann, Schaukeln",zh:"能做前滾翻、跳躍操、盪鞦韆"},
    {id:"GES16",de:"Bewegungssicherheit und Koordinationsvermögen entwickeln",zh:"發展動作安全感和協調能力"},
    {id:"GES17",de:"Selbstständig mit Löffel essen, aus Tasse trinken",zh:"能獨立用湯匙吃飯、用杯子喝水"},
    {id:"GES18",de:"Turm mit Klötzen bauen",zh:"能用積木堆塔"},
    {id:"GES19",de:"Zeichnen und Schreibmaterial nutzen",zh:"使用繪畫和書寫工具"},
    {id:"GES20",de:"Zähne putzen",zh:"刷牙"},
    {id:"GES21",de:"Sich allein an- und ausziehen",zh:"能獨立穿脫衣物"},
    {id:"GES22",de:"Mit Gabel essen, Knöpfe öffnen",zh:"能用叉子吃飯、打開鈕扣"},
    {id:"GES23",de:"Beim Kneten Kugeln und Rollen formen",zh:"捏黏土時能塑形"},
    {id:"GES24",de:"Mit Schere schneiden",zh:"能使用剪刀"},
    {id:"GES25",de:"Stift mit Erwachsenengriff halten",zh:"能用成人握筆方式持筆"},
    {id:"GES26",de:"Schleife binden, Knoten machen",zh:"能打結和綁蝴蝶結"},
    {id:"GES27",de:"Akustische Reize erkennen und unterscheiden",zh:"能識別和區分聽覺刺激"},
    {id:"GES28",de:"Visuelle Reize erkennen (Helligkeit, Formen, Farben)",zh:"能識別視覺刺激"},
    {id:"GES29",de:"Gegenstände durch Fühlen identifizieren",zh:"能透過觸覺識別物品"},
    {id:"GES30",de:"Gerüche und Geschmacksrichtungen erkennen",zh:"能識別氣味和味道"},
    {id:"GES31",de:"Gleichgewicht, Raum- und Richtungsverständnis",zh:"平衡感、空間和方向理解"},
    {id:"GES32",de:"Eigenen Körper kennen, Körperteile und Organe benennen",zh:"認識自己的身體，能說出身體部位和器官"},
    {id:"GES33",de:"Körpergrenzen vertreten, Grenzen anderer wahrnehmen",zh:"能表達身體界限，尊重他人界限"},
    {id:"GES34",de:"Positive Geschlechtsidentität, Bewusstsein für Intimsphäre",zh:"正向性別認同，有隱私意識"},
    {id:"GES35",de:"Grundwissen über Sexualität und Körperfunktionen",zh:"基本的性知識和身體功能認識"},
    {id:"GES36",de:"Grundverständnis über Gesundheit und Krankheit",zh:"對健康與疾病有基本認識"},
    {id:"GES37",de:"Grundverständnis für Hygiene entwickeln",zh:"建立基本衛生習慣"},
    {id:"GES38",de:"Toilettenbesuch selbst bewältigen",zh:"能獨立上廁所"},
    {id:"GES39",de:"Hunger, Durst und Sättigung einschätzen und ausdrücken",zh:"能感知並表達飢餓、口渴和飽足感"},
    {id:"GES40",de:"Gemeinsame Mahlzeiten genießen, Speisen auswählen",zh:"享受共同用餐，能選擇食物"},
    {id:"GES41",de:"Vielfältige Nahrungsmittel kennen, gesunde von ungesunden unterscheiden",zh:"認識各種食物，區分健康與不健康食品"}
  ]},
  {id:"KUN",de:"Kunst · Musik · Theaterspiel",zh:"藝術・音樂・戲劇遊戲",items:[
    {id:"KUN01",de:"Freude am künstlerischen Gestalten",zh:"喜歡藝術創作"},
    {id:"KUN02",de:"Befindet sich in der Kritzelphase",zh:"處於塗鴉階段"},
    {id:"KUN03",de:"Malt Menschen als Kopffüßler",zh:"畫蝌蚪人（頭腳人）"},
    {id:"KUN04",de:"Malt ganzen Menschen",zh:"能畫完整的人物"},
    {id:"KUN05",de:"Malt einzelne Elemente / Darstellungen",zh:"能畫單一元素或表現"},
    {id:"KUN06",de:"Malt Kombinationen und Kompositionen",zh:"能畫組合和構圖"},
    {id:"KUN07",de:"Malt Erzählbilder aus Realität oder Fantasie",zh:"能畫有故事性的圖畫"},
    {id:"KUN08",de:"Erklärt seine Zeichnungen mündlich",zh:"能口頭說明自己的畫作"},
    {id:"KUN09",de:"Farben und Farbnuancen kennen",zh:"認識顏色和色調深淺"},
    {id:"KUN10",de:"Techniken zur Gestaltung kennen und nutzen",zh:"認識並使用各種創作技法"},
    {id:"KUN11",de:"Werkzeuge sachgerecht handhaben",zh:"能正確使用工具"},
    {id:"KUN12",de:"Die eigenen Werke schätzen",zh:"重視自己的作品"},
    {id:"KUN13",de:"Die Werke anderer schätzen und beschreiben",zh:"欣賞並描述他人的作品"},
    {id:"KUN14",de:"Ästhetische Empfindungen ausdrücken",zh:"能表達審美感受"},
    {id:"KUN15",de:"Interesse an Kunst und Kunstwerken",zh:"對藝術作品感興趣"},
    {id:"KUN16",de:"Freude an Musik und Singen",zh:"喜歡音樂和歌唱"},
    {id:"KUN17",de:"Freude an Bewegung zu Musik und Tanzen",zh:"喜歡隨音樂動作和跳舞"},
    {id:"KUN18",de:"Freude dran, Töne produzieren",zh:"喜歡製造聲音"},
    {id:"KUN19",de:"Stille und Lautstärken bewusst erleben und unterscheiden",zh:"能有意識地體驗並區分靜默與音量"},
    {id:"KUN20",de:"Texte und Melodien einiger Lieder kennen",zh:"知道一些歌曲的歌詞和旋律"},
    {id:"KUN21",de:"Beim Singen Melodie und Rhythmus halten",zh:"唱歌時能保持旋律和節奏"},
    {id:"KUN22",de:"Rhythmus halten (Klatschen, Trommeln)",zh:"能保持節拍"},
    {id:"KUN23",de:"Instrumente am Klang erkennen",zh:"能靠聲音辨認樂器"},
    {id:"KUN24",de:"Freude am Sich-Verwandeln und Theaterspiel",zh:"喜歡扮演和戲劇遊戲"},
    {id:"KUN25",de:"Eigene Geschichten szenisch darstellen",zh:"能將故事或經歷戲劇化表演"},
    {id:"KUN26",de:"Als-Ob-Spiel: neue Welten mit Fantasie entwickeln",zh:"能用想像力創造「假裝世界」"},
    {id:"KUN27",de:"Gemeinsam Szenen und Geschichten darstellen, kooperieren",zh:"能共同表演場景，合作配合"}
  ]},
  {id:"SPR",de:"Sprache · Kommunikation",zh:"語言・溝通",missing:true,items:[],
    missingNote:{de:"⚠️ Dieser Bereich fehlt in der PDF – wird ergänzt sobald verfügbar.",zh:"⚠️ 此領域在 PDF 中缺失，待補充。"}},
  {id:"KOG",de:"Kognitive Entwicklung",zh:"認知發展",missing:true,items:[],
    missingNote:{de:"⚠️ Dieser Bereich fehlt in der PDF – wird ergänzt sobald verfügbar.",zh:"⚠️ 此領域在 PDF 中缺失，待補充。"}}
];

let lang='de';
let children=JSON.parse(localStorage.getItem('kita_children')||'[]');
let observations=JSON.parse(localStorage.getItem('kita_obs')||'{}');
let currentChild=null;
let filter='all';
let openSections={};

function t(k){return TR[lang][k]||k}

(function initYears(){
  const sel=document.getElementById('dob-year');
  const cur=new Date().getFullYear();
  for(let y=cur;y>=cur-8;y--){const o=document.createElement('option');o.value=y;o.textContent=y;sel.appendChild(o);}
})();

function buildMonths(){
  const sel=document.getElementById('dob-month');
  const cur=sel.value;
  sel.innerHTML='<option value="">'+t('filterAll').replace('Alle','Monat').replace('全部','月份')+'</option>';
  TR[lang].months.forEach((m,i)=>{const o=document.createElement('option');o.value=String(i+1).padStart(2,'0');o.textContent=m;sel.appendChild(o);});
  sel.value=cur;
}

function formatDob(m,y){
  if(!m&&!y) return '';
  const mname=m?TR[lang].months[parseInt(m)-1]:'';
  return [mname,y].filter(Boolean).join(' ');
}

function setLang(l){
  lang=l;
  document.querySelectorAll('.lang-btn').forEach(b=>b.classList.toggle('active',(l==='de'&&b.textContent==='DE')||(l==='zh'&&b.textContent==='中文')));
  buildMonths();applyLang();renderSections();
}

function applyLang(){
  document.getElementById('appname').textContent=t('appname');
  document.getElementById('btn-add-child').textContent=t('addChild');
  document.getElementById('tab-observe').textContent=t('observe');
  document.getElementById('tab-ai').textContent=t('ai');
  document.getElementById('tab-report').textContent=t('report');
  document.getElementById('filter-lbl').textContent=t('filterLbl');
  document.getElementById('f-all').textContent=t('filterAll');
  document.getElementById('f-pending').textContent=t('filterPending');
  document.getElementById('f-done').textContent=t('filterDone');
  document.getElementById('stat-total-lbl').textContent=t('statTotal');
  document.getElementById('stat-done-lbl').textContent=t('statDone');
  document.getElementById('stat-pct-lbl').textContent=t('statPct');
  document.getElementById('ai-info').textContent=t('aiInfo');
  document.getElementById('ai-input').placeholder=t('aiPlaceholder');
  document.getElementById('btn-ai-match').textContent=t('aiMatch');
  document.getElementById('btn-ai-prof').textContent=t('aiProf');
  document.getElementById('btn-rep-de').textContent=t('repDe');
  document.getElementById('btn-rep-zh').textContent=t('repZh');
  document.getElementById('btn-copy').textContent=t('copy');
  document.getElementById('modal-title').textContent=t('modalTitle');
  document.getElementById('lbl-name').textContent=t('lblName');
  document.getElementById('lbl-dob').textContent=t('lblDob');
  document.getElementById('btn-cancel').textContent=t('cancel');
  document.getElementById('btn-save').textContent=t('save');
  renderChildSelect();
}

function renderChildSelect(){
  const sel=document.getElementById('childSelect');
  sel.innerHTML='<option value="">'+t('selectChild')+'</option>';
  children.forEach(c=>{
    const opt=document.createElement('option');opt.value=c.id;
    opt.textContent=c.name+(formatDob(c.dobMonth,c.dobYear)?' ('+formatDob(c.dobMonth,c.dobYear)+')':'');
    if(currentChild&&currentChild.id===c.id) opt.selected=true;
    sel.appendChild(opt);
  });
}

function loadChild(){
  const id=document.getElementById('childSelect').value;
  currentChild=children.find(c=>c.id===id)||null;
  renderSections();updateStats();
}

function getObs(cid,iid){return observations[cid]&&observations[cid][iid]||null;}
function saveStorage(){localStorage.setItem('kita_obs',JSON.stringify(observations));}

function toggleStatus(itemId,status){
  if(!currentChild) return;
  const ex=getObs(currentChild.id,itemId);
  const noteEl=document.getElementById('note-'+itemId);
  const note=noteEl?noteEl.value:'';
  if(!observations[currentChild.id]) observations[currentChild.id]={};
  if(ex&&ex.status===status) delete observations[currentChild.id][itemId];
  else observations[currentChild.id][itemId]={status,note,ts:Date.now()};
  saveStorage();renderSections();updateStats();
}

function saveNote(itemId){
  if(!currentChild) return;
  const ex=getObs(currentChild.id,itemId);
  const noteEl=document.getElementById('note-'+itemId);
  if(ex&&noteEl){observations[currentChild.id][itemId].note=noteEl.value;saveStorage();}
}

function updateStats(){
  let total=0,done=0;
  DOMAINS.forEach(d=>{if(!d.missing) total+=d.items.length;});
  if(currentChild&&observations[currentChild.id])
    Object.values(observations[currentChild.id]).forEach(o=>{if(o.status==='ja'||o.status==='manchmal') done++;});
  document.getElementById('stat-total').textContent=total;
  document.getElementById('stat-done').textContent=done;
  document.getElementById('stat-pct').textContent=total>0?Math.round(done/total*100)+'%':'0%';
}

function setFilter(f){
  filter=f;
  document.querySelectorAll('.filter-btn').forEach(b=>b.classList.remove('active'));
  document.getElementById('f-'+f).classList.add('active');
  renderSections();
}

function toggleSection(id){openSections[id]=!openSections[id];renderSections();}

function renderSections(){
  const container=document.getElementById('sections-container');
  container.innerHTML='';
  DOMAINS.forEach(domain=>{
    const card=document.createElement('div');card.className='section-card';
    let dc=0;
    if(currentChild&&observations[currentChild.id])
      domain.items.forEach(item=>{const o=getObs(currentChild.id,item.id);if(o&&(o.status==='ja'||o.status==='manchmal')) dc++;});
    const isOpen=openSections[domain.id];
    const header=document.createElement('div');header.className='section-header';
    header.onclick=()=>toggleSection(domain.id);
    const bc=dc>0&&dc===domain.items.length&&!domain.missing?'section-badge done':'section-badge';
    header.innerHTML=`<span class="section-title">${domain[lang]}${domain.missing?' ⚠️':''}
      <span class="${bc}">${domain.missing?'待補充':dc+'/'+domain.items.length}</span></span>
      <span class="chevron" style="transform:${isOpen?'rotate(180deg)':''}">⌄</span>`;
    card.appendChild(header);
    const body=document.createElement('div');body.className='section-body'+(isOpen?' open':'');
    if(domain.missing){
      const n=document.createElement('div');n.className='missing-body';n.textContent=domain.missingNote[lang];body.appendChild(n);
    } else {
      let vis=0;
      domain.items.forEach(item=>{
        const obs=currentChild?getObs(currentChild.id,item.id):null;
        const isObs=obs&&(obs.status==='ja'||obs.status==='manchmal'||obs.status==='nein');
        if(filter==='pending'&&isObs) return;
        if(filter==='done'&&!isObs) return;
        vis++;
        const row=document.createElement('div');row.className='item-row'+(isObs?' observed':'');
        const top=document.createElement('div');top.className='item-top';
        top.innerHTML=`<div class="item-text">${item[lang]}</div>
          <div class="item-controls">
            <button class="status-btn${obs&&obs.status==='ja'?' ja':''}" onclick="toggleStatus('${item.id}','ja')">✓</button>
            <button class="status-btn${obs&&obs.status==='manchmal'?' manchmal':''}" onclick="toggleStatus('${item.id}','manchmal')">~</button>
            <button class="status-btn${obs&&obs.status==='nein'?' nein':''}" onclick="toggleStatus('${item.id}','nein')">✗</button>
          </div>`;
        row.appendChild(top);
        if(obs){
          const nw=document.createElement('div');
          nw.innerHTML=`<textarea class="note-area" id="note-${item.id}" onblur="saveNote('${item.id}')" placeholder="${t('notePlaceholder')}">${obs.note||''}</textarea>`;
          row.appendChild(nw);
        }
        body.appendChild(row);
      });
      if(vis===0){
        const e=document.createElement('div');e.className='missing-body';
        e.textContent=filter==='pending'?(lang==='de'?'Alle Kompetenzen bereits beobachtet ✓':'所有能力已觀察完畢 ✓'):(lang==='de'?'Noch keine Beobachtungen.':'尚無觀察記錄。');
        body.appendChild(e);
      }
    }
    card.appendChild(body);container.appendChild(card);
  });
}

function switchTab(tab){
  document.querySelectorAll('.tab').forEach(b=>b.classList.remove('active'));
  document.querySelectorAll('.panel').forEach(p=>p.classList.remove('active'));
  document.getElementById('tab-'+tab).classList.add('active');
  document.getElementById('panel-'+tab).classList.add('active');
}

function openAddChild(){document.getElementById('modal-bg').classList.add('open');}
function closeModal(){
  document.getElementById('modal-bg').classList.remove('open');
  document.getElementById('child-name-input').value='';
  document.getElementById('dob-month').value='';
  document.getElementById('dob-year').value='';
}
function addChild(){
  const name=document.getElementById('child-name-input').value.trim();
  if(!name) return;
  const child={id:'c'+Date.now(),name,dobMonth:document.getElementById('dob-month').value,dobYear:document.getElementById('dob-year').value};
  children.push(child);localStorage.setItem('kita_children',JSON.stringify(children));
  currentChild=child;renderChildSelect();renderSections();updateStats();closeModal();
}

async function aiCall(prompt){
  const r=await fetch('https://api.anthropic.com/v1/messages',{
    method:'POST',headers:{'Content-Type':'application/json'},
    body:JSON.stringify({model:'claude-sonnet-4-20250514',max_tokens:1000,messages:[{role:'user',content:prompt}]})
  });
  const d=await r.json();
  return d.content.map(c=>c.text||'').join('');
}

async function aiMatch(){
  const input=document.getElementById('ai-input').value.trim();if(!input) return;
  const el=document.getElementById('ai-result');el.style.display='block';
  el.innerHTML='<span class="loading-spinner"></span>'+(lang==='de'?'Analysiere...':'分析中...');
  const items=DOMAINS.flatMap(d=>d.items.map(i=>i.id+': '+i[lang]));
  const p=lang==='de'
    ?`Du bist Experte für frühkindliche Bildung. Ordne folgende Beobachtung passenden Kompetenzen zu:\n\n${items.join('\n')}\n\nBeobachtung: "${input}"\n\nAntworte: 1) Passende Kompetenz-IDs und Namen 2) Professioneller Beobachtungstext 2-3 Sätze Deutsch.`
    :`你是幼兒教育專家。將觀察與能力對應：\n\n${items.join('\n')}\n\n觀察：「${input}」\n\n回答：1) 對應能力ID和名稱 2) 2-3句專業教師觀察文字（繁體中文）。`;
  try{el.textContent=await aiCall(p);}catch(e){el.textContent=lang==='de'?'Fehler.':'失敗。';}
}

async function aiProfessionalize(){
  const input=document.getElementById('ai-input').value.trim();if(!input) return;
  const el=document.getElementById('ai-result');el.style.display='block';
  el.innerHTML='<span class="loading-spinner"></span>'+(lang==='de'?'Formuliere um...':'改寫中...');
  const p=lang==='de'
    ?`Formuliere in professionellen pädagogischen Beobachtungstext um. Fachsprache, objektiv, 3-4 Sätze Deutsch.\n\nNotiz: "${input}"`
    :`改寫成專業教師觀察文字。幼兒教育術語，客觀，繁體中文3-4句。\n\n筆記：「${input}」`;
  try{el.textContent=await aiCall(p);}catch(e){el.textContent=lang==='de'?'Fehler.':'失敗。';}
}

async function generateReport(rl){
  if(!currentChild){alert(t('noChild'));return;}
  const out=document.getElementById('report-out');out.style.display='block';
  out.innerHTML='<span class="loading-spinner"></span>'+(lang==='de'?'Generiere...':'生成中...');
  const obs=observations[currentChild.id]||{};
  const observed=[];
  DOMAINS.forEach(d=>d.items.forEach(item=>{
    const o=obs[item.id];
    if(o&&o.status==='ja') observed.push({area:d[rl==='zh'?'zh':'de'],item:item[rl==='zh'?'zh':'de'],note:o.note});
  }));
  if(!observed.length){out.textContent=rl==='de'?'Noch keine Beobachtungen.':'尚無觀察記錄。';return;}
  const grp={};observed.forEach(o=>{if(!grp[o.area]) grp[o.area]=[];grp[o.area].push(o);});
  const sum=Object.entries(grp).map(([a,its])=>a+':\n'+its.map(i=>'- '+i.item+(i.note?' ('+i.note+')':'')).join('\n')).join('\n\n');
  const dob=formatDob(currentChild.dobMonth,currentChild.dobYear);
  const ci=currentChild.name+(dob?' (geb. '+dob+')':'');
  const p=rl==='de'
    ?`Du bist Erzieherin in einer deutschen Kita. Erstelle professionellen Elterngespräch-Bericht für ${ci}. Fließende Absätze, Fachsprache, wertschätzend. Einleitung + Entwicklungsbereiche.\n\n${sum}`
    :`你是德國幼兒園教師。為兒童 ${ci} 撰寫專業家長面談報告（繁體中文）。流暢段落，專業，正面具體。引言＋發展領域。\n\n${sum}`;
  try{out.textContent=await aiCall(p);}catch(e){out.textContent=rl==='de'?'Fehler.':'失敗。';}
}

function copyReport(){
  navigator.clipboard.writeText(document.getElementById('report-out').textContent).then(()=>{
    const b=document.getElementById('btn-copy');const o=b.textContent;b.textContent='✓';setTimeout(()=>b.textContent=o,1500);
  });
}

buildMonths();renderChildSelect();renderSections();updateStats();applyLang();
</script>
</body>
</html>
