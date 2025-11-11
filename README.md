<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Once Human — Калькулятор слияния девиантов</title>
    <meta name="description" content="Точный калькулятор слияния девиантов для Once Human: вероятности типа, рейтинга, наследования черт, девиантных морфов. UX и механика близки к игре.">
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --c1: #1e213a;
            --c2: #232646;
            --c5: #3de9c3;
            --accent: #ffc94a;
            --bg: linear-gradient(120deg, #232646 0%, #3641a9 55%, #3de9c3 100%);
            --card-bg: #232646d9;
            --text: #f6f7fa;
            --border: #444a8a44;
            --error: #ff5151;
        }
        * { box-sizing: border-box; }
        body {
            margin: 0; background: var(--bg); color: var(--text);
            font-family: 'Inter', Arial, sans-serif; min-height: 100vh;
        }
        .container {
            max-width: 700px; margin: 32px auto 0 auto; background: var(--card-bg);
            border-radius: 20px; box-shadow: 0 8px 32px #23264636;
            padding: 2.2rem 2vw 2.1rem 2vw; border: 1.3px solid var(--border);
        }
        h1 span { color: var(--accent);}
        h1 { font-size: 2.3rem; font-weight: 700; margin-bottom: 0.4em; letter-spacing: -0.8px; text-align: center;}
        @media (max-width: 440px) { h1 {font-size: 1.35rem;} }
        .intro { color: #c8c9ee; font-size: 1.12rem; text-align: center; margin-bottom: 1.6em;}
        .section {background: rgba(36,38,70,0.98); border-radius: 14px; padding: 1.1em 1em;
            margin-bottom: 22px; border: 1.2px solid var(--border);}
        .section-title {color: var(--c5); font-size: 1.12rem; font-weight: 600; margin-bottom: 1em;
            letter-spacing: 0.01em; display: flex; align-items: center; gap: 10px;}
        .info-icon {display:inline-flex;align-items:center;justify-content:center;width:20px;height:20px;
            background:linear-gradient(135deg,#198cff,#3de9c3);border-radius:50%;font-size:13px;font-weight:700;
            color:white;cursor:pointer;position:relative;transition:.15s;outline:none;}
        .info-icon:hover,.info-icon:focus {transform:scale(1.13);box-shadow:0 0 12px #13ec8d80;}
        .tooltip {position:absolute;top:30px;left:50%;transform:translateX(-50%);
            background:linear-gradient(135deg,#1e213a 0%,#2a355f 100%);border:2px solid #3de9c3;
            border-radius:10px;padding:15px;width:320px;max-width:92vw;z-index:500;
            font-size: .88rem;line-height:1.4;display:none;}
        .info-icon:hover .tooltip, .info-icon:focus .tooltip, .info-icon.active .tooltip {display:block;}
        .tooltip h4 {margin:0 0 8px 0; font-size: 1.04rem; color: var(--accent);}
        .formula {background: #242646; padding:6px 10px; border-radius:5px; font-family:monospace;
            color:#3de9c3;margin: 6px 0 7px 0;}
        .legend { margin-top: 7px; border-top: 1px solid #3843b544; padding-top: 5px;}
        .legend-title {color:var(--accent);font-size:0.97em;}
        .legend-item {color: #a7ecfb; font-size: 0.97em;}
        @media (max-width:650px){ .tooltip {left:auto;right:0;transform:none;width:260px;} }
        label { font-weight: 600; color: var(--accent); font-size: .97rem; margin-bottom:0.22em; display: block;}
        select, input[type="number"], input[type="text"] {
            outline: none;border:1.5px solid #3843b55c;background: #242646fb; color: #f6f7fa;
            font-size: 1rem; border-radius: 6px; padding:9px 13px;margin-bottom:0.8em; width: 100%;
            transition:border 0.2s, box-shadow 0.2s;}
        select:focus, input:focus {border:1.5px solid var(--c5);box-shadow:0 0 8px #3de9c390;}
        input.error, select.error {border-color:var(--error);box-shadow:0 0 8px #ff515170;}
        .error-message {color:var(--error);font-size:0.89em;margin:-0.2em 0 0.7em 0;display:none;}
        .error-message.show {display:block;}
        .inline-group {display: flex; gap: 18px;}
        @media (max-width:650px){ .inline-group,.traits-group {flex-direction:column;}
            .container{padding:10vw 3vw;} }
        .traits-group {display:flex;gap:15px;}
        .trait-config {background:#1e213a88;border-radius:8px;padding:12px;margin-bottom:12px;
            border:1px solid #3843b544;}
        .trait-config label {font-size:.91em;color:#b7cbf7;font-weight:400;}
        .trait-config input[type="text"] {font-weight:600;color:var(--accent);}
        .calculate-btn {
            width:100%;padding:.98em;font-size:1.18rem;font-weight:700;border-radius:9px;
            border:none;background:linear-gradient(120deg,#198cff 40%,#3de9c3 100%);
            color:white;box-shadow:0 2px 12px #198cff22;cursor:pointer; margin-top:7px;}
        .calculate-btn:hover {transform:translateY(-2px) scale(1.03);
            box-shadow:0 8px 18px #21dce599;background:linear-gradient(120deg,#21dce5 0%,#3de9c3 100%);}
        .calculate-btn:disabled {opacity:0.5;cursor:not-allowed;}
        .results {margin-top:19px;background:linear-gradient(120deg,#2a355fdd 0%,#3641a9dc 100%);
            border-radius:16px;border:1.5px solid var(--border);box-shadow:0 2px 8px #1e213a44;display:none;
            padding:1.45em 1.3em;}
        .results.show {display:block;}
        .result-item {display:flex;justify-content:space-between;align-items:center;
            background:#242646b6;border-left:5px solid var(--c5);border-radius:6px;
            padding:9px 15px;margin-bottom:9px;font-size:1.08rem;color:#e9f5fb;}
        .result-label {color:#a7ecfb;font-weight:400;}
        .result-value,.big-number {font-size:1.15em;font-weight:700;letter-spacing:.01em;}
        .result-value.high,.big-number.high {color:#13ec8d;}
        .result-value.medium,.big-number.medium {color:#f6c23e;}
        .result-value.low,.big-number.low {color:var(--error);}
        .rating-breakdown,.traits-breakdown {background:#1e213add;border-radius:10px;padding:15px;
            margin:15px 0;border:1.5px solid #3de9c355;}
        .rating-breakdown h4,.traits-breakdown h4 {color:var(--accent);font-size:1.05rem;
            margin-bottom:12px;text-align:center;}
        .rating-option,.trait-option {display:flex;justify-content:space-between;
            align-items:center;padding:8px 12px;margin-bottom:6px;
            background:#242646cc;border-radius:6px;border-left:3px solid transparent;}
        .rating-option.target,.trait-option.guaranteed {border-left-color:#13ec8d;
            background:#24264699;box-shadow:0 0 8px #13ec8d33;}
        .rating-option.upgrade {border-left-color:#ffc94a;}
        .rating-option.downgrade {border-left-color:#ff5151;}
        .rating-option.same {border-left-color:#198cff;}
        .trait-option.high-prob {border-left-color:#ffc94a;}
        .trait-option.medium-prob {border-left-color:#198cff;}
        .trait-option.low-prob {border-left-color:#ff5151;}
        .rating-name,.trait-name {font-weight:600;color:#e9f5fb;font-size:0.98em;}
        .badge.target-badge {background:#13ec8d;color:#1e213a;}
        .badge.guaranteed-badge {background:#13ec8d;color:#1e213a;}
        .rating-prob,.trait-prob {font-weight:700;font-size:1.07em;}
        .rating-bar,.trait-bar {width:100%;height:4px;background:#1e213a;border-radius:2px;
            margin-top:4px;overflow:hidden;}
        .rating-bar-fill,.trait-bar-fill {height:100%;background:linear-gradient(90deg,#198cff,#3de9c3);
            transition:width 0.5s;}
        .rating-option.upgrade .rating-bar-fill {background:linear-gradient(90deg,#ffc94a,#ffdd88);}
        .rating-option.downgrade .rating-bar-fill {background:linear-gradient(90deg,#ff5151,#ff8888);}
        .rating-option.target .rating-bar-fill,
        .trait-option.guaranteed .trait-bar-fill {background:linear-gradient(90deg,#13ec8d,#5fffc0);}
        .trait-option.high-prob .trait-bar-fill {background:linear-gradient(90deg,#ffc94a,#ffdd88);}
        .trait-option.medium-prob .trait-bar-fill {background:linear-gradient(90deg,#198cff,#5fc3ff);}
        .trait-option.low-prob .trait-bar-fill {background:linear-gradient(90deg,#ff5151,#ff8888);}
        .trait-combinations {margin-top:10px;padding-top:10px;border-top:1px solid #3843b544;}
        .trait-combinations-title {font-size:.97em;color:#a7ecfb;margin-bottom:8px;font-weight:600;}
        .combo-item {background:#1e213a99;padding:6px 10px;border-radius:5px;margin-bottom:5px;
            font-size:.94em;display:flex;justify-content:space-between;}
        .combo-traits {color:#c8c9ee;}
        .combo-prob {color:var(--accent);font-weight:700;}
        .no-traits-message {text-align:center;color:#a7ecfb;padding:20px;font-style:italic;}
        .final-result {margin-top:14px;padding:23px 8px 13px 8px;background:var(--c1);
            border-radius:10px;text-align:center;border:2.3px solid var(--c5);
            box-shadow:0 2px 12px #3de9c364;}
        .final-result h3 {font-size:1.27rem;color:var(--accent);margin-bottom:13px;}
        .final-result .big-number {font-size:2.5rem;font-weight:700;margin:10px 0 6px 0;}
        .final-result .attempts {font-size:1.12rem;color:#aad6e6;}
        .info-box {background:#232646e0;border-left:3px solid var(--accent);
            padding:10px 17px;border-radius:7px;margin-top:13px;font-size:.99em;color:#fbf6e9;}
        .info-box strong {color:var(--accent);}
        .aria-live {position:absolute;left:-9999px;top:auto;width:1px;height:1px;overflow:hidden;}
    </style>
</head>
<body>
<div class="container" role="main">
    <h1>Once Human: <span>Deviant Fusion Calc</span></h1>
    <p class="intro">Все расчеты калькулятора основываются на статистике и опыте игроков. Было проанализировано около 150 исходов слияний, статистику продолжаю пополнять. Калькулятор работает в тестовом режиме и не гарантирует результат, так как принципы по которым считает игра - не раскрываются компанией.</p>
    <div class="aria-live" id="live-region" aria-live="assertive"></div>

    <div class="section">
        <div class="section-title">Тип девианта
            <div class="info-icon" tabindex="0" aria-label="Справка по типу девианта">
                i
                <div class="tooltip" role="tooltip">
                    <h4>📌 Методика расчёта типа</h4>
                    <div class="formula">P(тип) = базовый_шанс + модификатор</div>
                    <div>Вероятность совпадения типа слияния зависит от родителей и материалов.</div>
                    <div class="legend">
                        <div class="legend-title">Легенда:</div>
                        <div class="legend-item">• Одинаковые родители: 100%</div>
                        <div class="legend-item">• Разные родители: 50%/50%</div>
                        <div class="legend-item">• +1 материал типа: 65%</div>
                        <div class="legend-item">• +2: 75%, +3: 80%</div>
                    </div>
                </div>
            </div>
        </div>
        <label for="sameType">Родители одного типа?</label>
        <select id="sameType" aria-label="Тип родителей">
            <option value="yes">Да (одинаковые)</option>
            <option value="no">Нет (разные)</option>
        </select>
        <div id="materialsGroup" style="display: none;">
            <label for="typeMaterials">Кол-во материалов целевого типа (0–3):</label>
            <input type="number" id="typeMaterials" min="0" max="3" value="0" aria-label="Материалов типа">
            <div class="error-message" id="typeMaterialsError"></div>
        </div>
    </div>

    <div class="section">
        <div class="section-title">Рейтинг
            <div class="info-icon" tabindex="0" aria-label="Справка по рейтингу">
                i
                <div class="tooltip" role="tooltip">
                    <h4>📊 Методика расчёта рейтинга</h4>
                    <div class="formula">P(рейтинг) ≈ распределение_изменений</div>
                    <div>Распределение основано на данных в игре (~150+ слияний, player reports).</div>
                    <div class="legend">
                        <div class="legend-title">Границы вероятностей:</div>
                        <div class="legend-item">• Без изменений: ~45%</div>
                        <div class="legend-item">• Апгрейд (+1): ~32%</div>
                        <div class="legend-item">• Даунгрейд (-1): ~18%</div>
                        <div class="legend-item">• Экстремальные (±2): ~5%</div>
                        <div class="legend-item" style="color:#ff5151;">⚠️ Невозможные исходы исключены!</div>
                    </div>
                </div>
            </div>
        </div>
        <div class="inline-group">
            <div style="flex:1;">
                <label for="rating1">Рейтинг Родителя 1 (например, 5/4)</label>
                <input type="text" id="rating1" placeholder="5/4" value="5/4" aria-label="Рейтинг 1">
                <div class="error-message" id="rating1Error"></div>
            </div>
            <div style="flex:1;">
                <label for="rating2">Рейтинг Родителя 2</label>
                <input type="text" id="rating2" placeholder="4/5" value="4/5" aria-label="Рейтинг 2">
                <div class="error-message" id="rating2Error"></div>
            </div>
        </div>
        <label for="targetRating">Целевой рейтинг</label>
        <select id="targetRating">
            <option value="5/5">5/5 (макс.)</option>
            <option value="5/4">5/4</option>
            <option value="4/5">4/5</option>
            <option value="4/4">4/4</option>
            <option value="upgrade">Любой апгрейд (+1)</option>
            <option value="same">Без изменений</option>
        </select>
    </div>

    <div class="section">
        <div class="section-title">Наследование черт
            <div class="info-icon" tabindex="0" aria-label="Справка по чертам">
                i
                <div class="tooltip" role="tooltip">
                    <h4>✨ Методика расчёта черт</h4>
                    <div class="formula">P(черта) = базовый + (m × 0.1) (clean). В игре: material с чертой = boost x10!</div>
                    <div>Данная модель — аппроксимация статистики игроков (она ближе к fusion preview в Once Human, но не учтён true mat-boost).</div>
                    <div class="legend">
                        <div class="legend-title">Легенда:</div>
                        <div class="legend-item">• 2 родителя: 100%</div>
                        <div class="legend-item">• 1 parent + 0 materials: 50%</div>
                        <div class="legend-item">• 1 parent + 3 чистых: 80%</div>
                        <div class="legend-item" style="color:#ffc94a;">• Материал с чертой → шанс выше (x10 boost, вики/игра)</div>
                    </div>
                </div>
            </div>
        </div>
        <label for="numTraits">Количество желаемых черт (0–4):</label>
        <input type="number" id="numTraits" min="0" max="4" value="0" aria-label="Количество черт">
        <div class="error-message" id="numTraitsError"></div>
        <div id="traitsContainer"></div>
        <div class="info-box"><strong>Справка:</strong> Важно: В игре добавление материалов с нужной чертой сильно повышает шанс её наследования (до 10 раз!). Здесь учтён только базовый бонус от количества "чистых" материалов — как приближение.</div>
    </div>

    <div class="section">
        <div class="section-title">Девиантные черты (морфы)
            <div class="info-icon" tabindex="0" aria-label="Справка по девиантным чертам">
                i
                <div class="tooltip" role="tooltip">
                    <h4>🦎 Методика морфов</h4>
                    <div class="formula">P(morph) = 1 - (0.75)^n, где n = кол-во материалов (1–3)</div>
                    <div class="legend">
                        <div class="legend-item">• 1 мат: 25%</div>
                        <div class="legend-item">• 2: 43.75%</div>
                        <div class="legend-item">• 3: 57.8%</div>
                    </div>
                </div>
            </div>
        </div>
        <label for="wantDeviantTrait">Нужна девиантная черта?</label>
        <select id="wantDeviantTrait" aria-label="Девиантная черта">
            <option value="no">Нет</option>
            <option value="yes">Да</option>
        </select>
        <div id="deviantMaterialsGroup" style="display: none;">
            <label for="deviantMaterials">Кол-во материалов животных/мебели (1–3):</label>
            <input type="number" id="deviantMaterials" min="1" max="3" value="1" aria-label="Девиантных материалов">
            <div class="error-message" id="deviantMaterialsError"></div>
        </div>
    </div>

    <button class="calculate-btn" id="calcBtn" aria-label="Посчитать">🧮 Посчитать</button>
    <div class="results" id="results" role="region" aria-label="Результаты"></div>
</div>

<script>
let state = {
    rating1: "5/4",
    rating2: "4/5",
    targetRating: "5/5",
    sameType: "yes",
    typeMaterials: 0,
    numTraits: 0,
    traits: [],
    wantDeviantTrait: "no",
    deviantMaterials: 1
};

const traitsKey = i => `trait-${i}`;

function saveTraitFields() {
    const res = [];
    for (let i = 0; i < state.numTraits; ++i) {
        res.push({
            name: document.getElementById(traitsKey(i)+"-name")?.value || "",
            parents: +document.getElementById(traitsKey(i)+"-parents")?.value || 0,
            materials: +document.getElementById(traitsKey(i)+"-materials")?.value || 0
        });
    }
    state.traits = res;
}

function renderTraitFields() {
    let n = state.numTraits;
    let c = document.getElementById('traitsContainer');
    let prev = state.traits || [];
    c.innerHTML = "";
    for (let i = 0; i < n; ++i) {
        let t = prev[i] || {name: "", parents:1, materials:3};
        let nameHtml = `<input type="text" id="${traitsKey(i)}-name" class="trait-name-input" placeholder="Например: Cheer Up 3" maxlength="100" value="${t.name.replace(/"/g, '&quot;')}" aria-label="Название черты ${i+1}">`;
        let parHtml = `<input type="number" id="${traitsKey(i)}-parents" min="0" max="2" value="${t.parents}" aria-label="Родителей с чертой ${i+1}">`;
        let matHtml = `<input type="number" id="${traitsKey(i)}-materials" min="0" max="3" value="${t.materials}" aria-label="Материалов для черты ${i+1}">`;
        c.innerHTML += `<div class="trait-config"><label>Название черты #${i+1}</label>${nameHtml}<div class="traits-group">
            <div style="flex:1"><label>Родителей (0-2)</label>${parHtml}<div class="error-message" id="${traitsKey(i)}-parentsErr"></div></div>
            <div style="flex:1"><label>Материалов (0–3)</label>${matHtml}<div class="error-message" id="${traitsKey(i)}-materialsErr"></div></div>
        </div></div>`;
    }
}

function focusFirstError() {
    const err = document.querySelector('input.error, select.error');
    if (err) { err.focus(); err.scrollIntoView({behavior:"smooth",block:"center"}); }
}

function autoparseRating(val) {
    val = val.replace(/\s+/g,"");
    if (/^[1-5]{2}$/.test(val)) return val[0]+"/"+val[1];
    let m = val.match(/^([1-5])[\/:\-\s]+([1-5])$/);
    if (m) return m[1]+"/"+m[2];
    return val;
}

function validateRatingField(inputId, errorId) {
    let el = document.getElementById(inputId);
    let errDiv = document.getElementById(errorId);
    let val = el.value.trim();
    
    // Автокоррекция
    let corrected = autoparseRating(val);
    if (corrected !== val) {
        el.value = corrected;
        val = corrected;
    }
    
    // Валидация
    let rTest = /^[1-5]\/[1-5]$/;
    if (!rTest.test(val)) {
        el.classList.add("error");
        errDiv.classList.add("show");
        errDiv.textContent = "Формат 1–5/1–5 (например: 5/4)";
        return false;
    } else {
        el.classList.remove("error");
        errDiv.classList.remove("show");
        errDiv.textContent = "";
        return true;
    }
}

function validateForm(show=true) {
    let valid = true;
    function setErr(id,msg) {
        let el = document.getElementById(id);
        if (show) { el && (el.classList.add("error")); }
        let errDiv = document.getElementById(id+"Error")||document.getElementById(id+"Err");
        if (errDiv) { errDiv.classList.add("show"); errDiv.textContent = msg; }
    }
    function clrErr(id) {
        let el = document.getElementById(id);
        el && el.classList.remove("error");
        let errDiv = document.getElementById(id+"Error")||document.getElementById(id+"Err");
        if (errDiv) { errDiv.classList.remove("show"); errDiv.textContent = ""; }
    }
    
    // Рейтинги (с автокоррекцией)
    valid = validateRatingField("rating1", "rating1Error") && valid;
    valid = validateRatingField("rating2", "rating2Error") && valid;
    
    if (state.sameType==="no") {
        let v = +document.getElementById("typeMaterials").value;
        if (v<0||v>3) { setErr("typeMaterials","Значение от 0 до 3"); valid=false; } else clrErr("typeMaterials");
    }
    
    if (state.wantDeviantTrait==="yes") {
        let v = +document.getElementById("deviantMaterials").value;
        if (v<1||v>3) { setErr("deviantMaterials","Значение от 1 до 3"); valid=false; } else clrErr("deviantMaterials");
    }
    
    let n = +document.getElementById("numTraits").value;
    if (n<0||n>4) { setErr("numTraits","Значение от 0 до 4"); valid=false; } else clrErr("numTraits");

    for (let i = 0; i < n; ++i) {
        let pval = +document.getElementById(traitsKey(i)+"-parents").value;
        if (pval < 0 || pval > 2) { setErr(traitsKey(i)+"-parents", "0–2"); valid = false; } else clrErr(traitsKey(i)+"-parents");
        let mval = +document.getElementById(traitsKey(i)+"-materials").value;
        if (mval < 0 || mval > 3) { setErr(traitsKey(i)+"-materials", "0–3"); valid = false; } else clrErr(traitsKey(i)+"-materials");
    }
    return valid;
}

function getRatingDistribution(r1s, r2s, target) {
    let parse = s => { let p = s.split('/'); return {m:+p[0], pw:+p[1]}; };
    let r1 = parse(r1s), r2 = parse(r2s);
    let avM = Math.round((r1.m+r2.m)/2), avP = Math.round((r1.pw+r2.pw)/2);
    let dist = {};
    let total = 0;
    
    dist[`${avM}/${avP}`] = {prob:45, type:'same'};
    total+=45;
    
    let upgrades = [];
    if (avM<5) upgrades.push(`${avM+1}/${avP}`);
    if (avP<5) upgrades.push(`${avM}/${avP+1}`);
    if (avM<5&&avP<5) upgrades.push(`${avM+1}/${avP+1}`);
    upgrades = [...new Set(upgrades)];
    let uP = upgrades.length?32/upgrades.length:0;
    for (let u of upgrades) {dist[u]={prob:uP,type:'upgrade'};total+=uP;}
    
    let downs = [];
    if (avM>1) downs.push(`${avM-1}/${avP}`);
    if (avP>1) downs.push(`${avM}/${avP-1}`);
    downs = [...new Set(downs)];
    let dP = downs.length?18/downs.length:0;
    for (let d of downs) {dist[d]={prob:dP,type:'downgrade'};total+=dP;}
    
    let ex = [];
    if (avM<4) ex.push(`${avM+2}/${avP}`);
    if (avP<4) ex.push(`${avM}/${avP+2}`);
    if (avM>2) ex.push(`${avM-2}/${avP}`);
    if (avP>2) ex.push(`${avM}/${avP-2}`);
    ex = [...new Set(ex.filter(k=>!dist[k]))];
    let eP = ex.length?5/ex.length:0;
    for (let e of ex) {dist[e]={prob:eP,type:'extreme'};total+=eP;}
    
    for (let k in dist) dist[k].prob = +(dist[k].prob/total*100).toFixed(2);
    
    let tprob = dist[target]?dist[target].prob:0;
    return {distribution:dist, targetKey:target, targetProb:tprob};
}

function getTypesProb(sameType, typeMaterials) {
    if (sameType==="yes") return 100;
    if (typeMaterials===0) return 50;
    if (typeMaterials===1) return 65;
    if (typeMaterials===2) return 75;
    return 80;
}

function getTraitProb(parents, mats) {
    if (parents===2) return 1;
    if (parents===1) return 0.5+mats*0.1;
    return 0;
}

function getDeviantProb(mats) {
    return 1-Math.pow(0.75,Math.max(0,Math.min(3,mats)));
}

function calculateFusion() {
    if(!validateForm(true)) {
        focusFirstError();
        return;
    }

    let rating1 = document.getElementById("rating1").value.trim();
    let rating2 = document.getElementById("rating2").value.trim();
    let targetRating = document.getElementById("targetRating").value;
    let sameType = document.getElementById("sameType").value;
    let typeMaterials = +document.getElementById("typeMaterials")?.value || 0;
    let numTraits = +document.getElementById("numTraits").value || 0;
    let wantDeviantTrait = document.getElementById("wantDeviantTrait").value;
    let deviantMaterials = +document.getElementById("deviantMaterials")?.value || 1;

    saveTraitFields();

    let typeProb = getTypesProb(sameType, typeMaterials);
    let distObj = getRatingDistribution(rating1, rating2, targetRating);
    let ratingProb = distObj.targetProb;
    
    let traitFieldList = [];
    for(let i=0;i<numTraits;i++){
        let t = state.traits[i]||{name:`Черта ${i+1}`,parents:0,materials:0};
        let prob = getTraitProb(+t.parents,+t.materials);
        traitFieldList.push({name:t.name||`Черта ${i+1}`, parents:+t.parents, materials:+t.materials, prob});
    }
    let traitsProb = traitFieldList.reduce((a,t)=>a*t.prob,1);
    
    let deviantProb = wantDeviantTrait==="yes"?getDeviantProb(deviantMaterials):1;
    let total = 1.0*typeProb/100*ratingProb/100*(numTraits?traitsProb:1)*(wantDeviantTrait==="yes"?deviantProb:1);
    
    let html = "";
    html += `<div class="result-item"><span class="result-label">Вероятность типа</span><span class="result-value">${typeProb.toFixed(1)}%</span></div>`;
    html += `<div class="rating-breakdown"><h4>📊 Распределение вероятностей рейтинга</h4>`;
    let keys = Object.keys(distObj.distribution).sort((a,b)=>distObj.distribution[b].prob-distObj.distribution[a].prob);
    for(let k of keys){
        let info = distObj.distribution[k];
        let badge = (k===distObj.targetKey)?'<span class="badge target-badge">ЦЕЛЬ</span>':'';
        let color=(info.prob>=30)?'#13ec8d':(info.prob>=12)?'#f6c23e':'#ff5151';
        html += `<div class="rating-option${k===distObj.targetKey?' target':''}">
            <span class="rating-name">${k}${badge}</span>
            <span class="rating-prob" style="color:${color}">${info.prob.toFixed(1)}%</span>
            <div class="rating-bar"><div class="rating-bar-fill" style="width:${Math.min(info.prob*2,100)}%"></div></div>
        </div>`;
    }
    html += `</div>`;
    
    if(numTraits>0){
        html += `<div class="traits-breakdown">
            <h4>✨ Вероятности наследования черт</h4>
            <div id="traitsOptions"></div>
            <div class="trait-combinations" id="traitCombinations">
                <div class="trait-combinations-title">Возможные комбинации черт:</div>
                <div id="combinationsList"></div>
            </div>
        </div>`;
    }
    
    if(wantDeviantTrait==="yes"){
        html += `<div class="result-item"><span class="result-label">Девиантная черта</span>`;
        html += `<span class="result-value">${(deviantProb*100).toFixed(1)}%</span></div>`;
    }
    
    html += `<div class="final-result"><h3>Финальный шанс успеха</h3>
        <div class="big-number" style="${total>=.5?'color:#13ec8d;':total>=.2?'color:#f6c23e;':'color:var(--error);'}">${(total*100).toFixed(2)}%</div>
        <div class="attempts">Ожидаемо попыток: <strong>${total>0?(100/(total*100)).toFixed(1):"∞"}</strong></div></div>
        <div class="info-box" style="margin-bottom:5px;"><b>Интерпретация:</b>
        <br>• <span style="color:#13ec8d;">≥50%</span> — Высокий шанс (1–2 попытки)
        <br>• <span style="color:#f6c23e;">20–49%</span> — Средний (2–5 попыток)
        <br>• <span style="color:#ff5151">&lt;20%</span> — Низкий (5+ попыток)</div>
    `;
    
    document.getElementById("results").innerHTML = html;
    document.getElementById("results").classList.add("show");
    
    if (numTraits>0) renderTraitsDetailed(traitFieldList);
    document.getElementById("live-region").textContent = `Вероятность цели: ${(total*100).toFixed(2)}%`;
    
    document.getElementById("results").scrollIntoView({behavior:"smooth",block:"nearest"});
}

function renderTraitsDetailed(traits) {
    let c = document.getElementById("traitsOptions");
    if (!c) return;
    c.innerHTML = "";
    for (let t of traits) {
        let pct = t.prob*100;
        let typeClass = pct>=80?"guaranteed":pct>=60?"high-prob":pct>=40?"medium-prob":"low-prob";
        let badge = pct==100?'<span class="badge guaranteed-badge">100%</span>':'';
        c.innerHTML += `<div class="trait-option ${typeClass}">
            <span class="trait-name">${t.name}${badge}</span>
            <span class="trait-prob">${pct.toFixed(1)}%</span>
            <div class="trait-bar"><div class="trait-bar-fill" style="width:${pct}%"></div></div>
        </div>`;
    }
    
    let combDiv = document.getElementById("combinationsList");
    if (!combDiv) return;
    let N = traits.length;
    let probAll = traits.reduce((a,t)=>a*t.prob,1);
    combDiv.innerHTML = `<div class="combo-item"><span class="combo-traits">Все ${N} черт</span><span class="combo-prob">${(probAll*100).toFixed(1)}%</span></div>`;
    
    if (N>1) for(let i=0;i<N;++i) {
        let p=traits.reduce((a,t,j)=>a*(i==j?(1-t.prob):t.prob),1);
        if (p>0.001) combDiv.innerHTML += `<div class="combo-item"><span class="combo-traits">${traits.filter((_,j)=>i!=j).map(tt=>tt.name).join(", ")}</span><span class="combo-prob">${(p*100).toFixed(1)}%</span></div>`;
    }
    let none = traits.reduce((a,t)=>a*(1-t.prob),1);
    if (none>0.001) combDiv.innerHTML += `<div class="combo-item"><span class="combo-traits">Без черт</span><span class="combo-prob">${(none*100).toFixed(1)}%</span></div>`;
}

// Live-валидация для полей рейтинга
document.getElementById("rating1").addEventListener("input", function() {
    validateRatingField("rating1", "rating1Error");
});

document.getElementById("rating2").addEventListener("input", function() {
    validateRatingField("rating2", "rating2Error");
});

// Кнопка расчёта
document.getElementById("calcBtn").addEventListener("click", calculateFusion);

// Управление показом/скрытием дополнительных полей
document.getElementById('sameType').addEventListener('change',function(){
    state.sameType = this.value;
    document.getElementById('materialsGroup').style.display=(this.value==='no')?'block':'none';
});

document.getElementById('wantDeviantTrait').addEventListener('change',function(){
    state.wantDeviantTrait = this.value;
    document.getElementById('deviantMaterialsGroup').style.display=(this.value==='yes')?'block':'none';
});

document.getElementById("numTraits").addEventListener("input", function(){
    saveTraitFields();
    let n = +(this.value)||0;
    let prev = state.traits || [];
    state.numTraits = n;
    
    let next = [];
    for(let i=0;i<n;++i) next[i]=prev[i]||{name:"", parents:1, materials:3};
    state.traits = next;
    
    renderTraitFields();
});

// Tooltip keyboard support
document.querySelectorAll('.info-icon').forEach(el=>{
    el.addEventListener('keydown',function(e){
        if(e.key==="Enter"||e.key===" "){e.preventDefault();el.classList.toggle('active');}
        if(e.key==="Escape"){el.classList.remove('active');}
    });
    el.addEventListener('blur',function(){el.classList.remove('active');});
});

// Инициализация полей черт
renderTraitFields();
</script>
</body>
</html>
