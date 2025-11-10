<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Once Human — Прокачанный калькулятор слияния девиантов</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --c1: #1e213a;
            --c2: #232646;
            --c3: #3641a9;
            --c4: #198cff;
            --c5: #3de9c3;
            --accent: #ffc94a;
            --bg: linear-gradient(120deg, #232646 0%, #3641a9 55%, #3de9c3 100%);
            --card-bg: #232646d9;
            --text: #f6f7fa;
            --border: #444a8a44;
            --error: #ff5151;
        }
        *, *::before, *::after { box-sizing: border-box; }
        body {
            margin: 0;
            font-family: 'Inter', Arial, sans-serif;
            background: var(--bg);
            color: var(--text);
            min-height: 100vh;
        }
        .container {
            max-width: 700px;
            margin: 32px auto 0 auto;
            background: var(--card-bg);
            border-radius: 22px;
            box-shadow: 0 8px 32px rgba(30, 33, 58, 0.12);
            padding: 2.3rem 2.1rem 2.1rem 2.1rem;
            border: 1.3px solid var(--border);
        }
        h1 span { color: var(--accent); }
        h1 {
            font-size: 2rem;
            font-weight: 700;
            margin-bottom: .45em;
            letter-spacing: -0.5px;
            text-align: center;
        }
        .intro {
            color: #c8c9ee;
            font-size: 1.1rem;
            text-align: center;
            margin-bottom: 1.6em;
        }
        .section {
            background: rgba(36,38,70,.98);
            border-radius: 14px;
            padding: 1.05em 1em .9em 1em;
            margin-bottom: 22px;
            border: 1.2px solid var(--border);
        }
        .section-title {
            color: var(--c5);
            font-size: 1.12rem;
            font-weight: 600;
            margin-bottom: .95em;
            text-shadow: 0 3px 16px #1e213a30;
            letter-spacing: .02em;
        }
        label {
            font-weight: 600;
            color: var(--accent);
            font-size: .98rem;
            margin-bottom: .23em;
            display: block;
        }
        select, input[type=number], input[type=text] {
            outline: none;
            border: 1.5px solid #3843b55c;
            background: #242646f9;
            color: #f6f7fa;
            font-size: 1rem;
            border-radius: 7px;
            padding: 9px 13px;
            margin-bottom: .8em;
            transition: border .2s, box-shadow .2s;
            width: 100%;
        }
        select:focus, input:focus {
            border: 1.5px solid var(--c5);
            box-shadow: 0 0 8px #3de9c390;
        }
        .inline-group { display: flex; gap: 18px; }
        @media (max-width: 650px) {
            .inline-group, .traits-group { flex-direction: column; }
            .container { padding: 10vw 3vw; }
        }
        .traits-group { display: flex; gap: 15px; }
        .calculate-btn {
            width: 100%;
            padding: .98em;
            font-size: 1.17rem;
            font-weight: 700;
            border-radius: 9px;
            border: none;
            background: linear-gradient(120deg, #198cff 40%, #3de9c3 100%);
            color: #fff;
            box-shadow: 0 2px 12px #198cff22;
            cursor: pointer;
            transition: transform .18s, box-shadow .18s;
            margin-top: 7px;
        }
        .calculate-btn:hover {
            transform: translateY(-2px) scale(1.03);
            box-shadow: 0 8px 18px #21dce599;
            background: linear-gradient(120deg, #21dce5 0%, #3de9c3 100%);
        }
        .results {
            margin-top: 19px;
            background: linear-gradient(120deg, #2a355fdd 0%, #3641a9dc 100%);
            border-radius: 16px;
            border: 1.5px solid var(--border);
            box-shadow: 0 2px 8px #1e213a44;
            display: none;
            padding: 1.45em 1.3em;
        }
        .results.show { display: block; }
        .result-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            background: #242646b6;
            border-left: 5px solid var(--c5);
            border-radius: 6px;
            padding: 9px 15px;
            margin-bottom: 9px;
            font-size: 1.08rem;
            color: #e9f5fb;
        }
        .result-label { color: #a7ecfb; font-weight: 400; }
        .result-value, .big-number {
            font-size: 1.15em;
            font-weight: 700;
            letter-spacing: .01em;
        }
        .result-value.high, .big-number.high { color: #13ec8d; }
        .result-value.medium, .big-number.medium { color: #f6c23e; }
        .result-value.low, .big-number.low { color: var(--error); }

        /* ---- Детализация рейтинга и черт ---- */
        .breakdown {
            background: #1e213add;
            border-radius: 10px;
            padding: 15, 15px;
            margin: 15px 0;
            border: 1.5px solid #3de9c355;
        }
        .breakdown h4 {
            color: var(--accent);
            font-size: 1.05rem;
            margin-bottom: 12px;
            text-align: center;
        }
        .option {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 8px 12px;
            margin-bottom: 6px;
            background: #242646cc;
            border-radius: 6px;
            border-left: 3px solid transparent;
            transition: all .2s;
        }
        .option.target   { border-left-color: #13ec8d; background:#24264699; box-shadow:0 0 8px #13ec8d33; }
        .option.high     { border-left-color: #13ec8d; }
        .option.medium   { border-left-color: #f6c23e; }
        .option.low      { border-left-color: #ff5151; }

        .option-name { font-weight:600; color:#e9f5fb; font-size:.95rem; }
        .option-name .badge {
            display:inline-block; padding:2px 8px; border-radius:4px;
            font-size:.75rem; margin-left:8px; font-weight:700;
        }
        .option-name .badge.target-badge { background:#13ec8d; color:#1e213a; }

        .option-prob { font-weight:700; font-size:1.05rem; }

        .option-bar { width:100%; height:4px; background:#1e213a; border-radius:2px; margin-top:4px; overflow:hidden; }
        .option-bar-fill { height:100%; background:linear-gradient(90deg,#198cff,#3de9c3); transition:width .5s ease; }
        .option.high   .option-bar-fill { background:linear-gradient(90deg,#13ec8d,#5fffc0); }
        .option.medium .option-bar-fill { background:linear-gradient(90deg,#f6c23e,#ffdd88); }
        .option.low    .option-bar-fill { background:linear-gradient(90deg,#ff5151,#ff8888); }

        .final-result {
            margin-top:14px; padding:23px 8px 13px 8px;
            background:var(--c1); border-radius:10px; text-align:center;
            border:2.3px solid var(--c5); box-shadow:0 2px 12px #3de9c364;
        }
        .final-result h3 { font-size:1.27rem; color:var(--accent); margin-bottom:13px; letter-spacing:.01em; }
        .final-result .big-number { font-size:2.5rem; font-weight:700; margin:10px 0 6px 0; letter-spacing:.01em; }
        .final-result .attempts { font-size:1.1rem; color:#aad6e6; }

        .info-box {
            background:#232646e0; border-left:3px solid var(--accent);
            padding:10px 17px; border-radius:7px; margin-top:13px;
            font-size:.99em; color:#fbf6e9;
        }
        .info-box strong { color:var(--accent); }

        @media (max-width:440px){
            h1{font-size:1.18rem;}
            .container{max-width:98vw;padding:6vw 2vw}
        }
    </style>
</head>
<body>
<div class="container">
    <h1>Once Human: <span>Deviant Fusion Calc</span></h1>
    <p class="intro">Современный калькулятор — на основе анализа синергии материалов, рейтинга и черт. Быстрый расчёт шанса успеха!</p>

    <!-- Тип девианта -->
    <div class="section">
        <div class="section-title">Тип девианта</div>
        <label>Родители одного типа?</label>
        <select id="sameType">
            <option value="yes">Да (одинаковые)</option>
            <option value="no">Нет (разные)</option>
        </select>
        <div id="materialsGroup" style="display:none;">
            <label>Количество материалов целевого типа (0–3):</label>
            <input type="number" id="typeMaterials" min="0" max="3" value="0">
        </div>
    </div>

    <!-- Рейтинг -->
    <div class="section">
        <div class="section-title">Рейтинг</div>
        <div class="inline-group">
            <div style="flex:1;">
                <label>Рейтинг Родителя 1 (например, 5/4)</label>
                <input type="text" id="rating1" placeholder="5/4" value="5/4">
            </div>
            <div style="flex:1;">
                <label>Рейтинг Родителя 2</label>
                <input type="text" id="rating2" placeholder="4/5" value="4/5">
            </div>
        </div>
        <label>Целевой рейтинг:</label>
        <select id="targetRating">
            <option value="5/5">5/5 (максимум)</option>
            <option value="5/4">5/4</option>
            <option value="4/5">4/5</option>
            <option value="4/4">4/4</option>
            <option value="upgrade">Любой апгрейд (+1)</option>
            <option value="same">Без изменений</option>
        </select>
    </div>

    <!-- Наследование черт -->
    <div class="section">
        <div class="section-title">Наследование черт</div>
        <label>Количество желаемых черт (1–4):</label>
        <input type="number" id="numTraits" min="1" max="4" value="3">
        <div id="traitsContainer"></div>
        <div class="info-box">
            <strong>Справка:</strong> Укажите, сколько родителей имеют черту (0–2) и какое количество материалов "чисто" или "с чертой" (0–3) для каждой.
        </div>
    </div>

    <!-- Девиантные черты -->
    <div class="section">
        <div class="section-title">Девиантные черты (морфы/мебели/животные)</div>
        <label>Нужна девиантная черта?</label>
        <select id="wantDeviantTrait">
            <option value="no">Нет</option>
            <option value="yes">Да</option>
        </select>
        <div id="deviantMaterialsGroup" style="display:none;">
            <label>Количество материалов животных/мебели (0–3):</label>
            <input type="number" id="deviantMaterials" min="0" max="3" value="0">
        </div>
    </div>

    <button class="calculate-btn" onclick="calculateFusion()">Посчитать</button>

    <!-- Результаты -->
    <div class="results" id="results">
        <h2 style="color:#27ffe3;margin-bottom:13px;text-align:center;">Результаты расчёта</h2>

        <div class="result-item"><span class="result-label">Вероятность типа</span><span class="result-value" id="typeProb">—</span></div>

        <!-- Детализация рейтинга -->
        <div class="breakdown" id="ratingBreakdown">
            <h4>Распределение вероятностей рейтинга</h4>
            <div id="ratingOptions"></div>
        </div>

        <!-- Детализация черт -->
        <div class="breakdown" id="traitsBreakdown">
            <h4>Вероятность получения каждой черты</h4>
            <div id="traitsOptions"></div>
        </div>

        <div class="result-item"><span class="result-label">Все черты</span><span class="result-value" id="traitsProb">—</span></div>
        <div class="result-item" id="deviantProbItem" style="display:none;">
            <span class="result-label">Девиантная черта</span><span class="result-value" id="deviantProb">—</span>
        </div>

        <div class="final-result">
            <h3>Финальный шанс успеха</h3>
            <div class="big-number" id="totalProb">—</div>
            <div class="attempts">Ожидаемое количество попыток: <strong id="expectedAttempts">—</strong></div>
        </div>

        <div class="info-box" style="margin-bottom:5px;">
            <strong>Интерпретация:</strong><br>
            • <span style="color:#13ec8d;">≥50%</span> — Высокий шанс (1–2 попытки)<br>
            • <span style="color:#f6c23e;">20–49%</span> — Средний (2–5 попыток)<br>
            • <span style="color:#ff5151;"><20%</span> — Низкий (5+ попыток)
        </div>
    </div>
</div>

<script>
/* ---------- UI helpers ---------- */
document.getElementById('sameType').addEventListener('change', function () {
    document.getElementById('materialsGroup').style.display = (this.value === 'no') ? 'block' : 'none';
});
document.getElementById('wantDeviantTrait').addEventListener('change', function () {
    document.getElementById('deviantMaterialsGroup').style.display = (this.value === 'yes') ? 'block' : 'none';
});

/* ---------- Динамическое создание полей черт ---------- */
document.getElementById('numTraits').addEventListener('input', function () {
    const n = Math.max(1, Math.min(4, parseInt(this.value) || 1));
    const container = document.getElementById('traitsContainer');
    container.innerHTML = '';
    for (let i = 0; i < n; i++) {
        const div = document.createElement('div');
        div.className = 'traits-group';
        div.innerHTML = `
            <div style="flex:1;">
                <label>Родителей с чертой (0-2)</label>
                <input type="number" class="trait-parents" min="0" max="2" value="1">
            </div>
            <div style="flex:1;">
                <label>Материалов (0–3)</label>
                <input type="number" class="trait-materials" min="0" max="3" value="3">
            </div>`;
        container.appendChild(div);
    }
});
document.getElementById('numTraits').dispatchEvent(new Event('input'));

/* ---------- Основная функция расчёта ---------- */
function calculateFusion() {
    /* ---- 1. Тип ---- */
    const sameType = document.getElementById('sameType').value;
    const typeMat = parseInt(document.getElementById('typeMaterials').value) || 0;
    let typeProb = 100;
    if (sameType === 'no') {
        typeProb = typeMat === 0 ? 50 : typeMat === 1 ? 65 : typeMat === 2 ? 75 : 80;
    }

    /* ---- 2. Рейтинг ---- */
    const r1 = document.getElementById('rating1').value.trim();
    const r2 = document.getElementById('rating2').value.trim();
    const targetSel = document.getElementById('targetRating').value;
    const ratingDist = calculateRatingDistribution(r1, r2, targetSel);

    /* ---- 3. Черты ---- */
    const parents = document.querySelectorAll('.trait-parents');
    const mats    = document.querySelectorAll('.trait-materials');
    let traitsProb = 1;
    const traitProbs = []; // для детализации

    for (let i = 0; i < parents.length; i++) {
        const p = parseInt(parents[i].value) || 0;
        const m = parseInt(mats[i].value) || 0;
        let prb = 0;
        if (p === 2) prb = 1;
        else if (p === 1) prb = 0.5 + m * 0.1;
        // p===0 → prb=0
        traitProbs.push({ index: i + 1, prob: prb * 100 });
        traitsProb *= prb;
    }
    traitsProb *= 100;

    /* ---- 4. Девиантная черта ---- */
    const wantDev = document.getElementById('wantDeviantTrait').value;
    const devMat = parseInt(document.getElementById('deviantMaterials').value) || 0;
    let deviantProb = 100;
    const devItem = document.getElementById('deviantProbItem');
    if (wantDev === 'yes') {
        deviantProb = (1 - Math.pow(0.75, devMat)) * 100;
        devItem.style.display = 'flex';
    } else {
        devItem.style.display = 'none';
    }

    /* ---- 5. Финальный шанс ---- */
    const ratingProb = ratingDist.targetProb;
    const total = (typeProb / 100) *
                  (ratingProb / 100) *
                  (traitsProb / 100) *
                  (wantDev === 'yes' ? deviantProb / 100 : 1) * 100;

    /* ---- 6. Вывод ---- */
    document.getElementById('typeProb').textContent = typeProb.toFixed(1) + '%';
    displayRatingBreakdown(ratingDist);
    displayTraitsBreakdown(traitProbs); // НОВОЕ
    document.getElementById('traitsProb').textContent = traitsProb.toFixed(1) + '%';
    if (wantDev === 'yes') document.getElementById('deviantProb').textContent = deviantProb.toFixed(1) + '%';

    const totalEl = document.getElementById('totalProb');
    totalEl.textContent = total.toFixed(2) + '%';
    const exp = total > 0 ? (100 / total).toFixed(1) : '∞';
    document.getElementById('expectedAttempts').textContent = exp;

    totalEl.className = 'big-number';
    if (total >= 50) totalEl.classList.add('high');
    else if (total >= 20) totalEl.classList.add('medium');
    else totalEl.classList.add('low');

    const results = document.getElementById('results');
    results.classList.add('show');
    results.scrollIntoView({behavior: 'smooth', block: 'nearest'});
}

/* ---------- Детализация черт ---------- */
function displayTraitsBreakdown(traits) {
    const container = document.getElementById('traitsOptions');
    container.innerHTML = '';
    if (traits.length === 0) {
        container.innerHTML = '<div style="text-align:center;color:#a7ecfb;font-style:italic;">Нет черт для анализа</div>';
        return;
    }

    traits.forEach(t => {
        const prob = t.prob;
        const level = prob >= 70 ? 'high' : prob >= 40 ? 'medium' : 'low';

        const opt = document.createElement('div');
        opt.className = `option ${level}`;

        const name = document.createElement('span');
        name.className = 'option-name';
        name.textContent = `Черта ${t.index}`;
        opt.appendChild(name);

        const probSpan = document.createElement('span');
        probSpan.className = 'option-prob';
        probSpan.textContent = prob.toFixed(1) + '%';
        opt.appendChild(probSpan);

        const bar = document.createElement('div');
        bar.className = 'option-bar';
        const fill = document.createElement('div');
        fill.className = 'option-bar-fill';
        fill.style.width = `${Math.min(100, prob * 1.43)}%`; // 70% → 100%
        bar.appendChild(fill);

        const wrapper = document.createElement('div');
        wrapper.appendChild.Opt;
        wrapper.appendChild(bar);
        container.appendChild(wrapper);
    });
}

/* ---------- Остальные функции (рейтинг) — без изменений ---------- */
function calculateRatingDistribution(r1s, r2s, targetSelection) {
    const parse = s => {
        const [m, p] = s.split('/').map(Number);
        return {m: m||0, pw: p||0};
    };
    const r1 = parse(r1s), r2 = parse(r2s);
    const avgM = (r1.m + r2.m) / 2;
    const avgP = (r1.pw + r2.pw) / 2;

    const curM = Math.round(avgM);
    const curP = Math.round(avgP);
    const sameKey = `${curM}/${curP}`;

    const sameProb      = 45;
    const upgradeProb   = 32;
    const downgradeProb = 17;
    const extremeProb   = 6;

    const distribution = {};

    distribution[sameKey] = {prob: sameProb, type: 'same', rating: {m: curM, pw: curP}};

    const upgrades = [
        {m: Math.min(5, curM + 1), pw: curP},
        {m: curM, pw: Math.min(5, curP + 1)},
        {m: Math.min(5, curM + 1), pw: Math.min(5, curP + 1)}
    ];
    const uniqUp = [...new Set(upgrades.map(o=>`${o.m}/${o.pw}`))].filter(k=>k!==sameKey);
    const upEach = upgradeProb / (uniqUp.length || 1);
    uniqUp.forEach(k => {
        const [m,pw] = k.split('/').map(Number);
        distribution[k] = {prob: upEach, type: 'upgrade', rating: {m, pw}};
    });

    const downgrades = [
        {m: Math.max(1, curM - 1), pw: curP},
        {m: curM, pw: Math.max(1, curP - 1)}
    ];
    const uniqDown = [...new Set(downgrades.map(o=>`${o.m}/${o.pw}`))].filter(k=>!distribution[k]);
    const downEach = downgradeProb / (uniqDown.length || 1);
    uniqDown.forEach(k => {
        const [m,pw] = k.split('/').map(Number);
        distribution[k] = {prob: downEach, type: 'downgrade', rating: {m, pw}};
    });

    const extremes = [
        {m: Math.min(5, curM + 2), pw: curP},
        {m: Math.max(1, curM - 2), pw: curP}
    ];
    extremes.forEach(e => {
        const k = `${e.m}/${e.pw}`;
        if (!distribution[k]) distribution[k] = {prob: extremeProb/2, type: 'extreme', rating: e};
    });

    let targetProb = 0, targetKey = '';
    if (targetSelection === 'same') {
        targetProb = sameProb; targetKey = sameKey;
    } else if (targetSelection === 'upgrade') {
        targetProb = upgradeProb;
    } else {
        targetKey = targetSelection;
        if (distribution[targetKey]) {
            targetProb = distribution[targetKey].prob;
        } else {
            const tgt = parse(targetSelection);
            const dM = Math.abs(tgt.m - curM);
            const dP = Math.abs(tgt.pw - curP);
            const diff = dM + dP;
            if (diff === 0) targetProb = sameProb;
            else if (diff === 1) targetProb = upEach;
            else if (diff === 2) targetProb = extremeProb/2;
            else targetProb = 0;
            distribution[targetKey] = {prob: targetProb, type: 'target', rating: tgt};
        }
    }

    return {distribution, targetProb, targetKey};
}

function displayRatingBreakdown(data) {
    const container = document.getElementById('ratingOptions');
    container.innerHTML = '';
    const sorted = Object.entries(data.distribution).sort((a,b)=>b[1].prob - a[1].prob);
    for (const [key, info] of sorted) {
        const isTarget = key === data.targetKey;
        const typeClass = isTarget ? 'target' : info.type === 'upgrade' ? 'high' : info.type === 'downgrade' ? 'low' : 'medium';

        const opt = document.createElement('div');
        opt.className = `option ${typeClass}`;

        const name = document.createElement('span');
        name.className = 'option-name';
        name.textContent = key;
        if (isTarget) {
            const badge = document.createElement('span');
            badge.className = 'badge target-badge';
            badge.textContent = 'ЦЕЛЬ';
            name.appendChild(badge);
        }
        opt.appendChild(name);

        const prob = document.createElement('span');
        prob.className = 'option-prob';
        prob.textContent = info.prob.toFixed(1) + '%';
        opt.appendChild(prob);

        const bar = document.createElement('div');
        bar.className = 'option-bar';
        const fill = document.createElement('div');
        fill.className = 'option-bar-fill';
        fill.style.width = `${Math.min(100, info.prob * 2)}%`;
        bar.appendChild(fill);

        const wrapper = document.createElement('div');
        wrapper.appendChild(opt);
        wrapper.appendChild(bar);
        container.appendChild(wrapper);
    }
}
</script>
</body>
</html>
