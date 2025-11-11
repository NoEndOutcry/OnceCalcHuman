<!DOCTYPE html>
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
    <p class="intro">Современный калькулятор — на основе синергии материалов, рейтинга и черт. Быстрый расчёт шанса успеха в Once Human!</p>
    <div class="aria-live" id="live-region" aria-live="assertive"></div>
    <div class="section">
        <div class="section-title">Тип девианта
            <div class="info-icon" tabindex="0" aria-label="Справка по типу девианта">
                i
                <div class="tooltip" role="tooltip">
                    <h4>Методика расчёта типа</h4>
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
                    <h4>Методика расчёта рейтинга</h4>
                    <div class="formula">P(рейтинг) ≈ распределение_изменений</div>
                    <div>Распределение основано на данных в игре (~150+ слияний, player reports).</div>
                    <div class="legend">
                        <div class="legend-title">Границы вероятностей:</div>
                        <div class="legend-item">• Без изменений: ~45%</div>
                        <div class="legend-item">• Апгрейд (+1): ~32%</div>
                        <div class="legend-item">• Даунгрейд (-1): ~18%</div>
                        <div class="legend-item">• Экстремальные (±2): ~5%</div>
                        <div class="legend-item" style="color:#ff5151;">Невозможные исходы исключены!</div>
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
                    <h4>Методика расчёта черт</h4>
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
        <div class="info-box"><strong>Справка:</strong> Учтите: boost, если материал с чертой, реализуется только в игре! Здесь — только "clean" boost как приближение.</div>
    </div>
    <div class="section">
        <div class="section-title">Девиантные черты (морфы)
            <div class="info-icon" tabindex="0" aria-label="Справка по девиантным чертам">
                i
                <div class="tooltip" role="tooltip">
                    <h4>Методика морфов</h4>
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
    <button class="calculate-btn" id="calcBtn" aria-label="Посчитать">Посчитать</button>
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

function setState(partial) {
    Object.assign(state, partial);
    calculateFusionRealtime();
}

const traitsKey = i => `trait-${i}`;

function saveTraitFields() {
    const res = [];
    for (let i = 0; i < state.numTraits; ++i) {
        const name = document.getElementById(traitsKey(i)+"-name")?.value || "";
        const parents = +document.getElementById(traitsKey(i)+"-parents")?.value || 0;
        const materials = +document.getElementById(traitsKey(i)+"-materials")?.value || 0;
        res.push({name, parents, materials});
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
    val = val.replace(/\s+/g,"").toLowerCase();
    if (/^[1-5]{2}$/.test(val)) return val[0]+"/"+val[1];
    let m = val.match(/^([1-5])[\/:\-\s]+([1-5])$/);
    if (m) return m[1]+"/"+m[2];
    return val;
}

function validateForm(show = true) {
    let valid = true;
    function setErr(id, msg) {
        const el = document.getElementById(id);
        if (show && el) el.classList.add("error");
        const errDiv = document.getElementById(id+"Error") || document.getElementById(id+"Err");
        if (errDiv) { errDiv.classList.add("show"); errDiv.textContent = msg; }
    }
    function clrErr(id) {
        const el = document.getElementById(id);
        if (el) el.classList.remove("error");
        const errDiv = document.getElementById(id+"Error") || document.getElementById(id+"Err");
        if (errDiv) { errDiv.classList.remove("show"); errDiv.textContent = ""; }
    }

    // Рейтинг
    const r1Raw = document.getElementById("rating1").value;
    const r2Raw = document.getElementById("rating2").value;
    const r1 = autoparseRating(r1Raw);
    const r2 = autoparseRating(r2Raw);
    document.getElementById("rating1").value = r1;
    document.getElementById("rating2").value = r2;
    const rTest = /^[1-5]\/[1-5]$/;
    if (!rTest.test(r1)) { setErr("rating1", "Формат 1–5/1–5"); valid = false; } else clrErr("rating1");
    if (!rTest.test(r2)) { setErr("rating2", "Формат 1–5/1–5"); valid = false; } else clrErr("rating2");

    // Тип
    if (state.sameType === "no") {
        const v = +document.getElementById("typeMaterials").value;
        if (v < 0 || v > 3) { setErr("typeMaterials", "0–3"); valid = false; } else clrErr("typeMaterials");
    }

    // Девиант
    if (state.wantDeviantTrait === "yes") {
        const v = +document.getElementById("deviantMaterials").value;
        if (v < 1 || v > 3) { setErr("deviantMaterials", "1–3"); valid = false; } else clrErr("deviantMaterials");
    }

    // Черты
    const n = Math.min(4, Math.max(0, +document.getElementById("numTraits").value || 0));
    document.getElementById("numTraits").value = n;
    if (n < 0 || n > 4) { setErr("numTraits", "0–4"); valid = false; } else clrErr("numTraits");

    for (let i = 0; i < n; ++i) {
        const pval = +document.getElementById(traitsKey(i)+"-parents").value;
        if (pval < 0 || pval > 2) { setErr(traitsKey(i)+"-parents", "0–2"); valid = false; } else clrErr(traitsKey(i)+"-parents");
        const mval = +document.getElementById(traitsKey(i)+"-materials").value;
        if (mval < 0 || mval > 3) { setErr(traitsKey(i)+"-materials", "0–3"); valid = false; } else clrErr(traitsKey(i)+"-materials");
    }

    return valid;
}

function getRatingDistribution(r1s, r2s, target) {
    const parse = s => { const [m, p] = s.split('/'); return {m: +m, p: +p}; };
    const r1 = parse(r1s), r2 = parse(r2s);
    const baseM = Math.round((r1.m + r2.m) / 2);
    const baseP = Math.round((r1.p + r2.p) / 2);

    const dist = {};
    let totalWeight = 0;

    // Same
    const sameKey = `${baseM}/${baseP}`;
    dist[sameKey] = {prob: 45, type: 'same'};
    totalWeight += 45;

    // Upgrades +1
    const upgrades = [];
    if (baseM < 5) upgrades.push(`${baseM + 1}/${baseP}`);
    if (baseP < 5) upgrades.push(`${baseM}/${baseP + 1}`);
    const upWeight = upgrades.length ? 32 / upgrades.length : 0;
    upgrades.forEach(k => {
        dist[k] = {prob: (dist[k]?.prob || 0) + upWeight, type: 'upgrade'};
        totalWeight += upWeight;
    });

    // Downgrades -1
    const downgrades = [];
    if (baseM > 1) downgrades.push(`${baseM - 1}/${baseP}`);
    if (baseP > 1) downgrades.push(`${baseM}/${baseP - 1}`);
    const downWeight = downgrades.length ? 18 / downgrades.length : 0;
    downgrades.forEach(k => {
        dist[k] = {prob: (dist[k]?.prob || 0) + downWeight, type: 'downgrade'};
        totalWeight += downWeight;
    });

    // Extremes ±2
    const extremes = [];
    if (baseM <= 3) extremes.push(`${baseM + 2}/${baseP}`);
    if (baseP <= 3) extremes.push(`${baseM}/${baseP + 2}`);
    if (baseM >= 3) extremes.push(`${baseM - 2}/${baseP}`);
    if (baseP >= 3) extremes.push(`${baseM}/${baseP - 2}`);
    const uniqueExt = [...new Set(extremes.filter(k => !dist[k]))];
    const extWeight = uniqueExt.length ? 5 / uniqueExt.length : 0;
    uniqueExt.forEach(k => {
        dist[k] = {prob: extWeight, type: 'extreme'};
        totalWeight += extWeight;
    });

    // Нормализация
    let targetProb = 0;
    for (const k in dist) {
        dist[k].prob = +(dist[k].prob / totalWeight * 100).toFixed(2);
        if (target === k) targetProb = dist[k].prob;
        else if (target === 'upgrade' && dist[k].type === 'upgrade') targetProb += dist[k].prob;
        else if (target === 'same' && dist[k].type === 'same') targetProb += dist[k].prob;
    }

    return {distribution: dist, targetProb};
}

function getTypesProb(sameType, typeMaterials) {
    if (sameType === "yes") return 100;
    return [50, 65, 75, 80][typeMaterials] || 50;
}

function getTraitProb(parents, materials) {
    if (parents === 2) return 1;
    if (parents === 1) return 0.5 + materials * 0.1;
    return materials > 0 ? materials * 0.1 : 0;
}

function getDeviantProb(mats) {
    return 1 - Math.pow(0.75, Math.max(1, Math.min(3, mats)));
}

function calculateFusionRealtime() {
    if (!validateForm(false)) return;

    const rating1 = autoparseRating(document.getElementById("rating1").value);
    const rating2 = autoparseRating(document.getElementById("rating2").value);
    const targetRating = document.getElementById("targetRating").value;
    const sameType = document.getElementById("sameType").value;
    const typeMaterials = +document.getElementById("typeMaterials")?.value || 0;
    const numTraits = +document.getElementById("numTraits").value || 0;
    const wantDeviantTrait = document.getElementById("wantDeviantTrait").value;
    const deviantMaterials = +document.getElementById("deviantMaterials")?.value || 1;

    saveTraitFields();

    const typeProb = getTypesProb(sameType, typeMaterials);
    const {distribution, targetProb: ratingProb} = getRatingDistribution(rating1, rating2, targetRating);

    const traitList = state.traits.slice(0, numTraits).map((t, i) => ({
        name: t.name || `Черта ${i+1}`,
        prob: getTraitProb(t.parents, t.materials)
    }));
    const traitsProb = traitList.reduce((a, t) => a * t.prob, 1);

    const deviantProb = wantDeviantTrait === "yes" ? getDeviantProb(deviantMaterials) : 1;

    const total = (typeProb / 100) * (ratingProb / 100) * (numTraits ? traitsProb : 1) * deviantProb;

    renderResults(typeProb, distribution, targetRating, traitList, deviantProb, total, wantDeviantTrait === "yes");
    document.getElementById("live-region").textContent = `Финальный шанс: ${(total * 100).toFixed(2)}%`;
}

function renderResults(typeProb, dist, target, traits, deviantProb, total, showDeviant) {
    let html = `<div class="result-item"><span class="result-label">Вероятность типа</span><span class="result-value">${typeProb.toFixed(1)}%</span></div>`;
    
    html += `<div class="rating-breakdown"><h4>Распределение рейтинга</h4>`;
    const sorted = Object.keys(dist).sort((a, b) => dist[b].prob - dist[a].prob);
    for (const k of sorted) {
        const info = dist[k];
        const isTarget = (target === k) || (target === 'upgrade' && info.type === 'upgrade') || (target === 'same' && info.type === 'same');
        const badge = isTarget ? '<span class="badge target-badge">ЦЕЛЬ</span>' : '';
        const color = info.prob >= 30 ? '#13ec8d' : info.prob >= 12 ? '#f6c23e' : '#ff5151';
        html += `<div class="rating-option ${info.type} ${isTarget ? 'target' : ''}">
            <span class="rating-name">${k}${badge}</span>
            <span class="rating-prob" style="color:${color}">${info.prob.toFixed(1)}%</span>
            <div class="rating-bar"><div class="rating-bar-fill" style="width:${info.prob * 2}%"></div></div>
        </div>`;
    }
    html += `</div>`;

    if (traits.length > 0) {
        html += `<div class="traits-breakdown"><h4>Наследование черт</h4><div id="traitsOptions"></div>
            <div class="trait-combinations"><div class="trait-combinations-title">Комбинации:</div><div id="combinationsList"></div></div></div>`;
    }

    if (showDeviant) {
        html += `<div class="result-item"><span class="result-label">Девиантная черта</span><span class="result-value">${(deviantProb * 100).toFixed(1)}%</span></div>`;
    }

    const attempts = total > 0 ? (1 / total).toFixed(1) : "∞";
    const colorClass = total >= 0.5 ? 'high' : total >= 0.2 ? 'medium' : 'low';

    html += `<div class="final-result">
        <h3>Финальный шанс</h3>
        <div class="big-number ${colorClass}">${(total * 100).toFixed(2)}%</div>
        <div class="attempts">Попыток: <strong>${attempts}</strong></div>
    </div>
    <div class="info-box" style="margin-bottom:5px;">
        <b>Интерпретация:</b><br>
        • <span style="color:#13ec8d;">≥50%</span> — 1–2 попытки<br>
        • <span style="color:#f6c23e;">20–49%</span> — 2–5 попыток<br>
        • <span style="color:#ff5151;"><20%</span> — 5+ попыток
    </div>`;

    const results = document.getElementById("results");
    results.innerHTML = html;
    results.classList.add("show");

    if (traits.length > 0) renderTraitsDetailed(traits);
}

function renderTraitsDetailed(traits) {
    const container = document.getElementById("traitsOptions");
    const combList = document.getElementById("combinationsList");
    if (!container || !combList) return;

    container.innerHTML = "";
    traits.forEach(t => {
        const pct = t.prob * 100;
        const cls = pct >= 80 ? "guaranteed" : pct >= 60 ? "high-prob" : pct >= 40 ? "medium-prob" : "low-prob";
        const badge = pct === 100 ? '<span class="badge guaranteed-badge">100%</span>' : '';
        container.innerHTML += `<div class="trait-option ${cls}">
            <span class="trait-name">${t.name}${badge}</span>
            <span class="trait-prob">${pct.toFixed(1)}%</span>
            <div class="trait-bar"><div class="trait-bar-fill" style="width:${pct}%"></div></div>
        </div>`;
    });

    // Все комбинации
    const n = traits.length;
    for (let mask = 0; mask < (1 << n); mask++) {
        if (mask === 0) continue;
        let prob = 1;
        let names = [];
        for (let i = 0; i < n; i++) {
            if (mask & (1 << i)) {
                prob *= traits[i].prob;
                names.push(traits[i].name);
            } else {
                prob *= (1 - traits[i].prob);
            }
        }
        if (prob < 0.001) continue;
        const text = names.length === n ? `Все ${n}` : names.length === 0 ? "Без черт" : names.join(", ");
        combList.innerHTML += `<div class="combo-item"><span class="combo-traits">${text}</span><span class="combo-prob">${(prob * 100).toFixed(1)}%</span></div>`;
    }
}

// === Слушатели ===
document.querySelectorAll("input, select").forEach(el => {
    el.addEventListener("input", () => {
        if (el.id.startsWith("trait-")) saveTraitFields();
        setTimeout(calculateFusionRealtime, 10);
    });
});

document.getElementById("calcBtn").addEventListener("click", () => {
    if (validateForm(true)) {
        calculateFusionRealtime();
        focusFirstError();
    }
});

document.getElementById("numTraits").addEventListener("input", function() {
    let n = Math.min(4, Math.max(0, +this.value || 0));
    this.value = n;
    saveTraitFields();
    renderTraitFields();
    state.numTraits = n;
    state.traits = state.traits.slice(0, n);
    for (let i = state.traits.length; i < n; i++) {
        state.traits[i] = {name: "", parents: 1, materials: 3};
    }
    setTimeout(calculateFusionRealtime, 10);
});

document.getElementById('sameType').addEventListener('change', function() {
    document.getElementById('materialsGroup').style.display = this.value === 'no' ? 'block' : 'none';
    setState({sameType: this.value});
});

document.getElementById('wantDeviantTrait').addEventListener('change', function() {
    document.getElementById('deviantMaterialsGroup').style.display = this.value === 'yes' ? 'block' : 'none';
    setState({wantDeviantTrait: this.value});
});

document.querySelectorAll('.info-icon').forEach(el => {
    el.addEventListener('keydown', e => {
        if (e.key === "Enter" || e.key === " ") el.classList.toggle('active');
        if (e.key === "Escape") el.classList.remove('active');
    });
    el.addEventListener('blur', () => el.classList.remove('active'));
});

// Инициализация
renderTraitFields();
calculateFusionRealtime();
</script>
</body>
</html>
