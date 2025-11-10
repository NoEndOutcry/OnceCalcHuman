
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
        h1 span {
            color: var(--accent);
        }
        h1 {
            font-size: 2rem;
            font-weight: 700;
            margin-bottom: 0.45em;
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
            background: rgba(36,38,70,0.98);
            border-radius: 14px;
            padding: 1.05em 1em 0.9em 1em;
            margin-bottom: 22px;
            border: 1.2px solid var(--border);
        }
        .section-title {
            color: var(--c5);
            font-size: 1.12rem;
            font-weight: 600;
            margin-bottom: .95em;
            text-shadow: 0 3px 16px #1e213a30;
            letter-spacing: 0.02em;
        }
        label {
            font-weight: 600;
            color: var(--accent);
            font-size: 0.98rem;
            margin-bottom: 0.23em;
            display: block;
        }
        select, input[type="number"], input[type="text"] {
            outline: none;
            border: 1.5px solid #3843b55c;
            background: #242646f9;
            color: #f6f7fa;
            font-size: 1rem;
            border-radius: 7px;
            padding: 9px 13px;
            margin-bottom: 0.8em;
            transition: border 0.2s, box-shadow 0.2s;
        }
        select:focus, input:focus {
            border: 1.5px solid var(--c5);
            box-shadow: 0 0 8px #3de9c390;
        }
        .inline-group {
            display: flex;
            gap: 18px;
        }
        @media (max-width: 650px) {
            .inline-group, .traits-group {
                flex-direction: column;
            }
            .container {
                padding: 10vw 3vw;
            }
        }
        .traits-group {
            display: flex;
            gap: 15px;
        }
        .trait-item label {
            font-weight: 400;
            color: #b7cbf7;
            font-size: 0.98em;
        }
        .calculate-btn {
            width: 100%;
            padding: 0.98em;
            font-size: 1.17rem;
            font-weight: 700;
            border-radius: 9px;
            border: none;
            background: linear-gradient(120deg, #198cff 40%, #3de9c3 100%);
            color: white;
            box-shadow: 0 2px 12px #198cff22;
            cursor: pointer;
            transition: 0.18s transform, 0.18s box-shadow;
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
        .results.show {
            display: block;
        }
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
        .result-label {
            color: #a7ecfb;
            font-weight: 400;
        }
        .result-value, .big-number {
            font-size: 1.15em;
            font-weight: 700;
            letter-spacing: .01em;
        }
        .result-value.high, .big-number.high {
            color: #13ec8d;
        }
        .result-value.medium, .big-number.medium {
            color: #f6c23e;
        }
        .result-value.low, .big-number.low {
            color: var(--error);
        }

        /* Новые стили для детализации рейтинга */
        .rating-breakdown {
            background: #1e213add;
            border-radius: 10px;
            padding: 15px;
            margin: 15px 0;
            border: 1.5px solid #3de9c355;
        }
        .rating-breakdown h4 {
            color: var(--accent);
            font-size: 1.05rem;
            margin-bottom: 12px;
            text-align: center;
        }
        .rating-option {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 8px 12px;
            margin-bottom: 6px;
            background: #242646cc;
            border-radius: 6px;
            border-left: 3px solid transparent;
            transition: all 0.2s;
        }
        .rating-option.target {
            border-left-color: #13ec8d;
            background: #24264699;
            box-shadow: 0 0 8px #13ec8d33;
        }
        .rating-option.upgrade {
            border-left-color: #ffc94a;
        }
        .rating-option.downgrade {
            border-left-color: #ff5151;
        }
        .rating-option.same {
            border-left-color: #198cff;
        }
        .rating-name {
            font-weight: 600;
            color: #e9f5fb;
            font-size: 0.95rem;
        }
        .rating-name .badge {
            display: inline-block;
            padding: 2px 8px;
            border-radius: 4px;
            font-size: 0.75rem;
            margin-left: 8px;
            font-weight: 700;
        }
        .rating-name .badge.target-badge {
            background: #13ec8d;
            color: #1e213a;
        }
        .rating-prob {
            font-weight: 700;
            font-size: 1.05rem;
        }
        .rating-bar {
            width: 100%;
            height: 4px;
            background: #1e213a;
            border-radius: 2px;
            margin-top: 4px;
            overflow: hidden;
        }
        .rating-bar-fill {
            height: 100%;
            background: linear-gradient(90deg, #198cff, #3de9c3);
            transition: width 0.5s ease;
        }
        .rating-option.upgrade .rating-bar-fill {
            background: linear-gradient(90deg, #ffc94a, #ffdd88);
        }
        .rating-option.downgrade .rating-bar-fill {
            background: linear-gradient(90deg, #ff5151, #ff8888);
        }
        .rating-option.target .rating-bar-fill {
            background: linear-gradient(90deg, #13ec8d, #5fffc0);
        }

        .final-result {
            margin-top: 14px;
            padding: 23px 8px 13px 8px;
            background: var(--c1);
            border-radius: 10px;
            text-align: center;
            border: 2.3px solid var(--c5);
            box-shadow: 0 2px 12px #3de9c364;
        }
        .final-result h3 {
            font-size: 1.27rem;
            color: var(--accent);
            margin-bottom: 13px;
            letter-spacing: 0.01em;
        }
        .final-result .big-number {
            font-size: 2.5rem;
            font-weight: 700;
            margin: 10px 0 6px 0;
            letter-spacing: 0.01em;
        }
        .final-result .attempts {
            font-size: 1.1rem;
            color: #aad6e6;
        }
        .info-box {
            background: #232646e0;
            border-left: 3px solid var(--accent);
            padding: 10px 17px;
            border-radius: 7px;
            margin-top: 13px;
            font-size: 0.99em;
            color: #fbf6e9;
        }
        .info-box strong {
            color: var(--accent);
        }
        @media (max-width: 440px){
            h1 {font-size: 1.18rem;}
            .container {max-width: 98vw; padding:6vw 2vw}
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Once Human: <span>Deviant Fusion Calc</span></h1>
        <p class="intro">Современный калькулятор — на основе анализа синергии материалов, рейтинга и черт. Быстрый расчёт шанса успеха!</p>

        <div class="section">
            <div class="section-title">Тип девианта</div>
            <label>Родители одного типа?</label>
            <select id="sameType"><option value="yes">Да (одинаковые)</option><option value="no">Нет (разные)</option></select>
            <div id="materialsGroup" style="display: none;">
                <label>Количество материалов целевого типа (0–3):</label>
                <input type="number" id="typeMaterials" min="0" max="3" value="0">
            </div>
        </div>

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

        <div class="section">
            <div class="section-title">Наследование черт</div>
            <label>Количество желаемых черт (1–4):</label>
            <input type="number" id="numTraits" min="1" max="4" value="3">
            <div id="traitsContainer"></div>
            <div class="info-box"><strong>Справка:</strong> Укажите, сколько родителей имеют черту (0–2) и какое количество материалов "чисто" или "с чертой" (0–3) для каждой.</div>
        </div>
        <div class="section">
            <div class="section-title">Девиантные черты (морфы/мебель/животные)</div>
            <label>Нужна девиантная черта?</label>
            <select id="wantDeviantTrait"><option value="no">Нет</option><option value="yes">Да</option></select>
            <div id="deviantMaterialsGroup" style="display: none;">
                <label>Количество материалов животных/мебели (1–3):</label>
                <input type="number" id="deviantMaterials" min="0" max="3" value="0">
            </div>
        </div>
        <button class="calculate-btn" onclick="calculateFusion()">🧮 Посчитать</button>
        <div class="results" id="results">
            <h2 style="color:#27ffe3; margin-bottom: 13px; text-align:center;">Результаты расчёта</h2>
                <div class="result-item"><span class="result-label">Вероятность типа</span><span class="result-value" id="typeProb">—</span></div>

                <!-- Детализация рейтинга -->
                <div class="rating-breakdown" id="ratingBreakdown">
                    <h4>📊 Распределение вероятностей рейтинга</h4>
                    <div id="ratingOptions"></div>
                </div>

                <div class="result-item"><span class="result-label">Все черты</span><span class="result-value" id="traitsProb">—</span></div>
                <div class="result-item" id="deviantProbItem" style="display: none;"><span class="result-label">Девиантная черта</span><span class="result-value" id="deviantProb">—</span></div>
            <div class="final-result">
                <h3>Финальный шанс успеха</h3><div class="big-number" id="totalProb">—</div><div class="attempts">Ожидаемое количество попыток: <strong id="expectedAttempts">—</strong></div>
            </div>
            <div class="info-box" style="margin-bottom:5px;">
                <strong>Интерпретация:</strong>
                <br>• <span style="color:#13ec8d;">≥50%</span> — Высокий шанс (1–2 попытки)
                <br>• <span style="color:#f6c23e;">20–49%</span> — Средний (2–5 попыток)
                <br>• <span style="color:#ff5151">&lt;20%</span> — Низкий (5+ попыток)
            </div>
        </div>
    </div>
    <script>
        document.getElementById('sameType').addEventListener('change', function(){document.getElementById('materialsGroup').style.display=(this.value==='no')?'block':'none'});
        document.getElementById('wantDeviantTrait').addEventListener('change', function(){document.getElementById('deviantMaterialsGroup').style.display=(this.value==='yes')?'block':'none'});
        document.getElementById('numTraits').addEventListener('input', function(){
            const n=parseInt(this.value)||1, c=document.getElementById('traitsContainer'); c.innerHTML='';
            for(let i=1;i<=n;i++){
                let d=document.createElement('div');d.className='traits-group';
                d.innerHTML=`<div style='flex:1;'><label>Родителей с чертой (0-2)</label><input type='number' class='trait-parents' min='0' max='2' value='1'></div><div style='flex:1;'><label>Материалов (0–3)</label><input type='number' class='trait-materials' min='0' max='3' value='3'></div>`;
                c.appendChild(d)
            }});
        document.getElementById('numTraits').dispatchEvent(new Event('input'));

        function calculateFusion(){
            // Тип
            let sT = document.getElementById('sameType').value;
            let tM = parseInt(document.getElementById('typeMaterials')?.value)||0;
            let typeProb=100;if(sT==='no'){typeProb=tM===0?50:tM===1?65:tM===2?75:80;}

            // Рейтинг - получаем детальное распределение
            let r1=document.getElementById('rating1').value,r2=document.getElementById('rating2').value,tR=document.getElementById('targetRating').value;
            let ratingDistribution = calculateRatingDistribution(r1, r2, tR);

            // Черты
            let parents=document.querySelectorAll('.trait-parents'),mats=document.querySelectorAll('.trait-materials'),traitsProb=1;
            for(let i=0;i<parents.length;i++){let p=parseInt(parents[i].value)||0,m=parseInt(mats[i].value)||0,prb=0;
                if(p===2)prb=1;else if(p===1)prb=0.5+m*0.1;traitsProb*=prb}
            traitsProb*=100;

            // Девиантная черта
            let deviantProb=1,wD=document.getElementById('wantDeviantTrait').value;let showDev=document.getElementById('deviantProbItem');
            if(wD==='yes'){let dM=parseInt(document.getElementById('deviantMaterials').value)||0;
                deviantProb=(1-Math.pow(0.75,dM))*100;showDev.style.display='flex';}else showDev.style.display='none';

            // Финал
            let ratingProb = ratingDistribution.targetProb;
            let total=typeProb/100*ratingProb/100*traitsProb/100*(wD==='yes'?deviantProb/100:1)*100;

            // Отображение
            document.getElementById('typeProb').textContent=typeProb.toFixed(1)+'%';
            displayRatingBreakdown(ratingDistribution);
            document.getElementById('traitsProb').textContent=traitsProb.toFixed(1)+'%';
            if(wD==='yes')document.getElementById('deviantProb').textContent=deviantProb.toFixed(1)+'%';
            let tPE=document.getElementById('totalProb');
            tPE.textContent=total.toFixed(2)+'%';
            let exp=(total>0?(100/total).toFixed(1):'∞');
            document.getElementById('expectedAttempts').textContent=exp;
            tPE.className='big-number';if(total>=50)tPE.classList.add('high');else if(total>=20)tPE.classList.add('medium');else tPE.classList.add('low');
            document.getElementById('results').classList.add('show');document.getElementById('results').scrollIntoView({behavior:'smooth',block:'nearest'});
        }

        function calculateRatingDistribution(r1s, r2s, targetSelection) {
            const parseRating = s => {
                let p = s.split('/');
                return {m: parseInt(p[0]) || 0, pw: parseInt(p[1]) || 0};
            };

            let r1 = parseRating(r1s), r2 = parseRating(r2s);
            let avgM = (r1.m + r2.m) / 2, avgP = (r1.pw + r2.pw) / 2;

            // Генерируем возможные результаты
            let options = [];

            // Текущий средний (без изменений) - 40-50%
            let currentM = Math.round(avgM), currentP = Math.round(avgP);
            let sameProb = 45;

            // Апгрейды (+1) - 30-35%
            let upgradeProb = 32;
            let upgrades = [
                {m: Math.min(5, currentM + 1), pw: currentP},
                {m: currentM, pw: Math.min(5, currentP + 1)},
                {m: Math.min(5, currentM + 1), pw: Math.min(5, currentP + 1)}
            ];

            // Даунгрейды (-1) - 15-20%
            let downgradeProb = 17;
            let downgrades = [
                {m: Math.max(1, currentM - 1), pw: currentP},
                {m: currentM, pw: Math.max(1, currentP - 1)}
            ];

            // Экстремальные (±2) - 1-5%
            let extremeProb = 3;

            // Собираем все варианты
            let distribution = {};

            // Без изменений
            let sameKey = `${currentM}/${currentP}`;
            distribution[sameKey] = {prob: sameProb, type: 'same', rating: {m: currentM, pw: currentP}};

            // Апгрейды (распределяем вероятность между вариантами)
            let uniqueUpgrades = [];
            for(let u of upgrades) {
                let key = `${u.m}/${u.pw}`;
                if(key !== sameKey && !uniqueUpgrades.includes(key)) {
                    uniqueUpgrades.push(key);
                }
            }
            let upgradeEach = upgradeProb / uniqueUpgrades.length;
            for(let key of uniqueUpgrades) {
                let [m, pw] = key.split('/').map(Number);
                distribution[key] = {prob: upgradeEach, type: 'upgrade', rating: {m, pw}};
            }

            // Даунгрейды
            let uniqueDowngrades = [];
            for(let d of downgrades) {
                let key = `${d.m}/${d.pw}`;
                if(!distribution[key] && !uniqueDowngrades.includes(key)) {
                    uniqueDowngrades.push(key);
                }
            }
            let downgradeEach = downgradeProb / uniqueDowngrades.length;
            for(let key of uniqueDowngrades) {
                let [m, pw] = key.split('/').map(Number);
                distribution[key] = {prob: downgradeEach, type: 'downgrade', rating: {m, pw}};
            }

            // Экстремальные варианты
            let extreme = [
                {m: Math.min(5, currentM + 2), pw: currentP},
                {m: Math.max(1, currentM - 2), pw: currentP}
            ];
            for(let e of extreme) {
                let key = `${e.m}/${e.pw}`;
                if(!distribution[key]) {
                    distribution[key] = {prob: extremeProb / 2, type: 'extreme', rating: e};
                }
            }

            // Определяем целевую вероятность
            let targetProb = 0;
            let targetKey = '';

            if(targetSelection === 'same') {
                targetProb = sameProb;
                targetKey = sameKey;
            } else if(targetSelection === 'upgrade') {
                targetProb = upgradeProb;
            } else {
                // Конкретный рейтинг
                targetKey = targetSelection;
                if(distribution[targetKey]) {
                    targetProb = distribution[targetKey].prob;
                } else {
                    // Оцениваем вероятность для нестандартного целевого рейтинга
                    let target = parseRating(targetSelection);
                    let diffM = Math.abs(target.m - currentM);
                    let diffP = Math.abs(target.pw - currentP);
                    let totalDiff = diffM + diffP;

                    if(totalDiff === 0) targetProb = sameProb;
                    else if(totalDiff === 1) targetProb = upgradeEach;
                    else if(totalDiff === 2) targetProb = extremeProb;
                    else targetProb = 5;

                    distribution[targetKey] = {prob: targetProb, type: 'target', rating: target};
                }
            }

            return {
                distribution: distribution,
                targetProb: targetProb,
                targetKey: targetKey
            };
        }

        function displayRatingBreakdown(data) {
            let container = document.getElementById('ratingOptions');
            container.innerHTML = '';

            // Сортируем по вероятности (убывание)
            let sorted = Object.entries(data.distribution).sort((a, b) => b[1].prob - a[1].prob);

            for(let [key, info] of sorted) {
                let isTarget = (key === data.targetKey);
                let typeClass = isTarget ? 'target' : info.type;

                let optionDiv = document.createElement('div');
                optionDiv.className = `rating-option ${typeClass}`;

                let nameSpan = document.createElement('span');
                nameSpan.className = 'rating-name';
                nameSpan.textContent = key;

                if(isTarget) {
                    let badge = document.createElement('span');
                    badge.className = 'badge target-badge';
                    badge.textContent = 'ЦЕЛЬ';
                    nameSpan.appendChild(badge);
                }

                let probSpan = document.createElement('span');
                probSpan.className = 'rating-prob';
                probSpan.textContent = info.prob.toFixed(1) + '%';

                // Цвет вероятности
                if(info.prob >= 30) probSpan.style.color = '#13ec8d';
                else if(info.prob >= 15) probSpan.style.color = '#f6c23e';
                else probSpan.style.color = '#ff5151';

                optionDiv.appendChild(nameSpan);
                optionDiv.appendChild(probSpan);

                // Прогресс-бар
                let barDiv = document.createElement('div');
                barDiv.className = 'rating-bar';
                let fillDiv = document.createElement('div');
                fillDiv.className = 'rating-bar-fill';
                fillDiv.style.width = Math.min(100, info.prob * 2) + '%';
                barDiv.appendChild(fillDiv);

                let wrapperDiv = document.createElement('div');
                wrapperDiv.appendChild(optionDiv);
                wrapperDiv.appendChild(barDiv);

                container.appendChild(wrapperDiv);
            }
        }
    </script>
</body>
</html>
