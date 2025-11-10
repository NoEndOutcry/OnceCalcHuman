<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Once Human — Калькулятор слияния девиантов</title>
  <meta name="description" content="Точный калькулятор вероятностей слияния девиантов в игре Once Human с детальным анализом типа, рейтинга и черт">
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap" rel="stylesheet">
  <style>
    :root { --c1: #1e213a; --c2: #232646; --c3: #3641a9; --c4: #198cff; --c5: #3de9c3; --accent: #ffc94a; --bg: linear-gradient(120deg, #232646 0%, #3641a9 55%, #3de9c3 100%); --card-bg: #232646d9; --text: #f6f7fa; --border: #444a8a44; --error: #ff5151; }
    * { box-sizing: border-box; }
    body { margin: 0; font-family: 'Inter', Arial, sans-serif; background: var(--bg); color: var(--text); min-height: 100vh; padding-bottom: 50px; }
    .container { max-width: 700px; margin: 32px auto 0 auto; background: var(--card-bg); border-radius: 22px; box-shadow: 0 8px 32px rgba(30, 33, 58, 0.12); padding: 2.3rem 2.1rem 2.1rem 2.1rem; border: 1.3px solid var(--border); }
    h1 span { color: var(--accent); }
    h1 { font-size: 2rem; font-weight: 700; margin-bottom: 0.45em; letter-spacing: -0.5px; text-align: center; }
    .intro { color: #c8c9ee; font-size: 1.1rem; text-align: center; margin-bottom: 1.6em; }
    .section { background: rgba(36,38,70,0.98); border-radius: 14px; padding: 1.05em 1em 0.9em 1em; margin-bottom: 22px; border: 1.2px solid var(--border); }
    .section-title { color: var(--c5); font-size: 1.12rem; font-weight: 600; margin-bottom: .95em; text-shadow: 0 3px 16px #1e213a30; letter-spacing: 0.02em; display: flex; align-items: center; gap: 10px; }
    .info-icon { display: inline-flex; align-items: center; justify-content: center; width: 20px; height: 20px; background: linear-gradient(135deg, #198cff, #3de9c3); border-radius: 50%; font-size: 12px; font-weight: 700; color: white; cursor: help; position: relative; flex-shrink: 0; outline: none; }
    .info-icon:hover, .info-icon:focus { transform: scale(1.1); box-shadow: 0 0 12px #3de9c3; }
    .info-icon:focus { outline: 2px solid #3de9c3; outline-offset: 2px; }
    .tooltip { position: absolute; top: 30px; left: 50%; transform: translateX(-50%); background: linear-gradient(135deg, #1e213a 0%, #2a355f 100%); border: 2px solid #3de9c3; border-radius: 10px; padding: 15px; width: 320px; max-width: 90vw; z-index: 1000; box-shadow: 0 8px 24px rgba(0,0,0,0.4); display: none; font-size: 0.85rem; line-height: 1.5; }
    .info-icon:hover .tooltip, .info-icon:focus .tooltip, .info-icon.active .tooltip { display: block; }
    .tooltip h4 { color: var(--accent); font-size: 0.95rem; margin: 0 0 10px 0; font-weight: 700; }
    .tooltip .formula { background: #242646; padding: 8px 10px; border-radius: 6px; margin: 8px 0; font-family: 'Courier New', monospace; color: #3de9c3; font-size: 0.8rem; border-left: 3px solid var(--accent); }
    .tooltip .description { color: #c8c9ee; margin: 8px 0; }
    .tooltip .legend { margin-top: 10px; padding-top: 10px; border-top: 1px solid #3843b544; }
    .tooltip .legend-title { color: var(--accent); font-weight: 600; font-size: 0.8rem; margin-bottom: 5px; }
    .tooltip .legend-item { color: #a7ecfb; font-size: 0.75rem; margin: 3px 0; padding-left: 10px; }
    @media (max-width: 650px) { .tooltip { left: auto; right: 0; transform: none; width: 280px; } }
    label { font-weight: 600; color: var(--accent); font-size: 0.98rem; margin-bottom: 0.23em; display: block; }
    select, input[type="number"], input[type="text"] { outline: none; border: 1.5px solid #3843b55c; background: #242646f9; color: #f6f7fa; font-size: 1rem; border-radius: 7px; padding: 9px 13px; margin-bottom: 0.8em; transition: border 0.2s, box-shadow 0.2s; width: 100%; }
    select:focus, input:focus { border: 1.5px solid var(--c5); box-shadow: 0 0 8px #3de9c390; }
    input.error, select.error { border-color: var(--error); box-shadow: 0 0 8px rgba(255, 81, 81, 0.3); }
    .error-message { color: var(--error); font-size: 0.85rem; margin-top: -0.5em; margin-bottom: 0.8em; display: none; }
    .error-message.show { display: block; }
    .inline-group { display: flex; gap: 18px; }
    @media (max-width: 650px) { .inline-group, .traits-group { flex-direction: column; } .container { padding: 10vw 3vw; } }
    .traits-group { display: flex; gap: 15px; }
    .trait-config { background: #1e213a88; border-radius: 8px; padding: 12px; margin-bottom: 12px; border: 1px solid #3843b544; }
    .trait-config label { font-size: 0.9rem; color: #b7cbf7; font-weight: 400; }
    .trait-config input[type="text"] { font-weight: 600; color: var(--accent); }
    .calculate-btn { width: 100%; padding: 0.98em; font-size: 1.17rem; font-weight: 700; border-radius: 9px; border: none; background: linear-gradient(120deg, #198cff 40%, #3de9c3 100%); color: white; box-shadow: 0 2px 12px #198cff22; cursor: pointer; transition: 0.18s transform, 0.18s box-shadow; margin-top: 7px; }
    .calculate-btn:hover { transform: translateY(-2px) scale(1.03); box-shadow: 0 8px 18px #21dce599; background: linear-gradient(120deg, #21dce5 0%, #3de9c3 100%); }
    .calculate-btn:disabled { opacity: 0.5; cursor: not-allowed; transform: none; }
    .results { margin-top: 19px; background: linear-gradient(120deg, #2a355fdd 0%, #3641a9dc 100%); border-radius: 16px; border: 1.5px solid var(--border); box-shadow: 0 2px 8px #1e213a44; display: none; padding: 1.45em 1.3em; }
    .results.show { display: block; }
    .result-item { display: flex; justify-content: space-between; align-items: center; background: #242646b6; border-left: 5px solid var(--c5); border-radius: 6px; padding: 9px 15px; margin-bottom: 9px; font-size: 1.08rem; color: #e9f5fb; }
    .result-label { color: #a7ecfb; font-weight: 400; }
    .result-value, .big-number { font-size: 1.15em; font-weight: 700; letter-spacing: .01em; }
    .result-value.high, .big-number.high { color: #13ec8d; }
    .result-value.medium, .big-number.medium { color: #f6c23e; }
    .result-value.low, .big-number.low { color: var(--error); }
    .rating-breakdown, .traits-breakdown { background: #1e213add; border-radius: 10px; padding: 15px; margin: 15px 0; border: 1.5px solid #3de9c355; }
    .rating-breakdown h4, .traits-breakdown h4 { color: var(--accent); font-size: 1.05rem; margin-bottom: 12px; text-align: center; }
    .rating-option, .trait-option { display: flex; justify-content: space-between; align-items: center; padding: 8px 12px; margin-bottom: 6px; background: #242646cc; border-radius: 6px; border-left: 3px solid transparent; transition: all 0.2s; }
    .rating-option.target, .trait-option.guaranteed { border-left-color: #13ec8d; background: #24264699; box-shadow: 0 0 8px #13ec8d33; }
    .rating-option.upgrade { border-left-color: #ffc94a; }
    .rating-option.downgrade { border-left-color: #ff5151; }
    .rating-option.same { border-left-color: #198cff; }
    .trait-option.high-prob { border-left-color: #ffc94a; }
    .trait-option.medium-prob { border-left-color: #198cff; }
    .trait-option.low-prob { border-left-color: #ff5151; }
    .rating-name, .trait-name { font-weight: 600; color: #e9f5fb; font-size: 0.95rem; }
    .rating-name .badge, .trait-name .badge { display: inline-block; padding: 2px 8px; border-radius: 4px; font-size: 0.75rem; margin-left: 8px; font-weight: 700; }
    .badge.target-badge { background: #13ec8d; color: #1e213a; }
    .badge.guaranteed-badge { background: #13ec8d; color: #1e213a; }
    .rating-prob, .trait-prob { font-weight: 700; font-size: 1.05rem; }
    .rating-bar, .trait-bar { width: 100%; height: 4px; background: #1e213a; border-radius: 2px; margin-top: 4px; overflow: hidden; }
    .rating-bar-fill, .trait-bar-fill { height: 100%; background: linear-gradient(90deg, #198cff, #3de9c3); transition: width 0.5s ease; }
    .rating-option.upgrade .rating-bar-fill { background: linear-gradient(90deg, #ffc94a, #ffdd88); }
    .rating-option.downgrade .rating-bar-fill { background: linear-gradient(90deg, #ff5151, #ff8888); }
    .rating-option.target .rating-bar-fill, .trait-option.guaranteed .trait-bar-fill { background: linear-gradient(90deg, #13ec8d, #5fffc0); }
    .trait-option.high-prob .trait-bar-fill { background: linear-gradient(90deg, #ffc94a, #ffdd88); }
    .trait-option.medium-prob .trait-bar-fill { background: linear-gradient(90deg, #198cff, #5fc3ff); }
    .trait-option.low-prob .trait-bar-fill { background: linear-gradient(90deg, #ff5151, #ff8888); }
    .trait-combinations { margin-top: 10px; padding-top: 10px; border-top: 1px solid #3843b544; }
    .trait-combinations-title { font-size: 0.9rem; color: #a7ecfb; margin-bottom: 8px; font-weight: 600; }
    .combo-item { background: #1e213a99; padding: 6px 10px; border-radius: 5px; margin-bottom: 5px; font-size: 0.85rem; display: flex; justify-content: space-between; }
    .combo-traits { color: #c8c9ee; }
    .combo-prob { color: var(--accent); font-weight: 700; }
    .no-traits-message { text-align: center; color: #a7ecfb; padding: 20px; font-style: italic; }
    .final-result { margin-top: 14px; padding: 23px 8px 13px 8px; background: var(--c1); border-radius: 10px; text-align: center; border: 2.3px solid var(--c5); box-shadow: 0 2px 12px #3de9c364; }
    .final-result h3 { font-size: 1.27rem; color: var(--accent); margin-bottom: 13px; letter-spacing: 0.01em; }
    .final-result .big-number { font-size: 2.5rem; font-weight: 700; margin: 10px 0 6px 0; letter-spacing: 0.01em; }
    .final-result .attempts { font-size: 1.1rem; color: #aad6e6; }
    .info-box { background: #232646e0; border-left: 3px solid var(--accent); padding: 10px 17px; border-radius: 7px; margin-top: 13px; font-size: 0.99em; color: #fbf6e9; }
    .info-box strong { color: var(--accent); }
    @media (max-width: 440px){ h1 {font-size: 1.18rem;} .container {max-width: 98vw; padding:6vw 2vw} }
  </style>
</head>
<body>
  <div class="container">
    <h1>Once Human: <span>Deviant Fusion Calc</span></h1>
    <p class="intro">Современный калькулятор — на основе анализа синергии материалов, рейтинга и черт. Быстрый расчёт шанса успеха!</p>

    <div class="section">
      <div class="section-title"> Тип девианта
        <div class="info-icon" tabindex="0" role="button" aria-label="Справка по типу девианта" onkeydown="toggleTooltip(event, this)"> i
          <div class="tooltip" role="tooltip">
            <h4>Методика расчёта типа</h4>
            <div class="formula">P(тип) = базовый_шанс + модификатор</div>
            <div class="description">Вероятность получения нужного типа девианта зависит от родителей и материалов слияния.</div>
            <div class="legend">
              <div class="legend-title">Легенда:</div>
              <div class="legend-item">• Одинаковые родители: 100%</div>
              <div class="legend-item">• Разные родители: 50% / 50%</div>
              <div class="legend-item">• +1 материал типа A: ~65%</div>
              <div class="legend-item">• +2 материала типа A: ~75%</div>
              <div class="legend-item">• +3 материала типа A: ~80%</div>
            </div>
          </div>
        </div>
      </div>
      <label for="sameType">Родители одного типа?</label>
      <select id="sameType" aria-label="Выбор типа родителей">
        <option value="yes">Да (одинаковые)</option>
        <option value="no">Нет (разные)</option>
      </select>
      <div id="materialsGroup" style="display: none;">
        <label for="typeMaterials">Количество материалов целевого типа (0–3):</label>
        <input type="number" id="typeMaterials" min="0" max="3" value="0" aria-label="Количество материалов">
        <div class="error-message" id="typeMaterialsError">Значение должно быть от 0 до 3</div>
      </div>
    </div>

    <div class="section">
      <div class="section-title"> Рейтинг
        <div class="info-icon" tabindex="0" role="button" aria-label="Справка по рейтингу" onkeydown="toggleTooltip(event, this)"> i
          <div class="tooltip" role="tooltip">
            <h4>Методика расчёта рейтинга</h4>
            <div class="formula">P(рейтинг) ≈ распределение_изменений</div>
            <div class="description">Рейтинг результата (формат X/Y) определяется случайным образом на основе статистического распределения из 150+ слияний игроков.</div>
            <div class="legend">
              <div class="legend-title">Распределение вероятностей:</div>
              <div class="legend-item">• Без изменений: ~44%</div>
              <div class="legend-item">• Апгрейд (+1): ~33%</div>
              <div class="legend-item">• Даунгрейд (-1): ~18%</div>
              <div class="legend-item">• Экстремальные (±2): ~5%</div>
              <div class="legend-item" style="margin-top:5px; color:#ff5151;">Даже 5/5 + 5/5 может дать 5/4!</div>
            </div>
          </div>
        </div>
      </div>
      <div class="inline-group">
        <div style="flex:1;">
          <label for="rating1">Рейтинг Родителя 1 (например, 5/4)</label>
          <input type="text" id="rating1" placeholder="5/4" value="5/4" aria-label="Рейтинг первого родителя">
          <div class="error-message" id="rating1Error">Формат: X/Y, где X и Y от 1 до 5</div>
        </div>
        <div style="flex:1;">
          <label for="rating2">Рейтинг Родителя 2</label>
          <input type="text" id="rating2" placeholder="4/5" value="4/5" aria-label="Рейтинг второго родителя">
          <div class="error-message" id="rating2Error">Формат: X/Y, где X и Y от 1 до 5</div>
        </div>
      </div>
      <label for="targetRating">Целевой рейтинг:</label>
      <select id="targetRating" aria-label="Выбор целевого рейтинга">
        <option value="5/5">5/5 (максимум)</option>
        <option value="5/4">5/4</option>
        <option value="4/5">4/5</option>
        <option value="4/4">4/4</option>
        <option value="upgrade">Любой апгрейд (+1)</option>
        <option value="same">Без изменений</option>
      </select>
    </div>

    <div class="section">
      <div class="section-title"> Наследование черт
        <div class="info-icon" tabindex="0" role="button" aria-label="Справка по чертам" onkeydown="toggleTooltip(event, this)"> i
          <div class="tooltip" role="tooltip">
            <h4>Методика расчёта черт</h4>
            <div class="formula">P(черта) = базовый_шанс + (n × бонус)</div>
            <div class="description">Вероятность наследования черты зависит от количества родителей с этой чертой и количества материалов слияния.</div>
            <div class="legend">
              <div class="legend-title">Легенда (где n = материалы):</div>
              <div class="legend-item">• 2 родителя с чертой: 100%</div>
              <div class="legend-item">• 1 родитель + 0 материалов: 50%</div>
              <div class="legend-item">• 1 родитель + 1 чистый: 60%</div>
              <div class="legend-item">• 1 родитель + 2 чистых: 70%</div>
              <div class="legend-item">• 1 родитель + 3 чистых: 80%</div>
              <div class="legend-item" style="margin-top:5px; color:#3de9c3;">Чистый = девиант без черт</div>
            </div>
          </div>
        </div>
      </div>
      <label for="numTraits">Количество желаемых черт (0–4):</label>
      <input type="number" id="numTraits" min="0" max="4" value="0" aria-label="Количество черт">
      <div class="error-message" id="numTraitsError">Значение должно быть от 0 до 4</div>
      <div id="traitsContainer"></div>
      <div class="info-box"><strong>Справка:</strong> Укажите название черты, количество родителей с ней (0–2) и количество материалов (0–3). Если черты не нужны, укажите 0.</div>
    </div>

    <div class="section">
      <div class="section-title"> Девиантные черты (морфы/мебель/животные)
        <div class="info-icon" tabindex="0" role="button" aria-label="Справка по девиантным чертам" onkeydown="toggleTooltip(event, this)"> i
          <div class="tooltip" role="tooltip">
            <h4>Методика расчёта девиантных черт</h4>
            <div class="formula">P(морф) = 1 - (0.75)^n</div>
            <div class="description">Девиантные черты (морфы внешности) получаются при использовании животных или мебели как материалов слияния. Вероятность рассчитывается мультипликативно.</div>
            <div class="legend">
              <div class="legend-title">Легенда (где n = материалы):</div>
              <div class="legend-item">• 1 материал: 25.0%</div>
              <div class="legend-item">• 2 материала: 43.75%</div>
              <div class="legend-item">• 3 материала: 57.8%</div>
              <div class="legend-item" style="margin-top:5px; color:#3de9c3;">Пример: 3 леопарда → 58% морф</div>
            </div>
          </div>
        </div>
      </div>
      <label for="wantDeviantTrait">Нужна девиантная черта?</label>
      <select id="wantDeviantTrait" aria-label="Выбор девиантной черты">
        <option value="no">Нет</option>
        <option value="yes">Да</option>
      </select>
      <div id="deviantMaterialsGroup" style="display: none;">
        <label for="deviantMaterials">Количество материалов животных/мебели (1–3):</label>
        <input type="number" id="deviantMaterials" min="1" max="3" value="1" aria-label="Количество девиантных материалов">
        <div class="error-message" id="deviantMaterialsError">Значение должно быть от 1 до 3</div>
      </div>
    </div>

    <button class="calculate-btn" onclick="calculateFusion()" aria-label="Рассчитать вероятность">Посчитать</button>

    <div class="results" id="results" role="region" aria-label="Результаты расчёта">
      <h2 style="color:#27ffe3; margin-bottom: 13px; text-align:center;">Результаты расчёта</h2>
      <div class="result-item"><span class="result-label">Вероятность типа</span><span class="result-value" id="typeProb">—</span></div>
      <div class="rating-breakdown" id="ratingBreakdown">
        <h4>Распределение вероятностей рейтинга</h4>
        <div id="ratingOptions"></div>
      </div>
      <div class="traits-breakdown" id="traitsBreakdown">
        <h4>Вероятности наследования черт</h4>
        <div id="traitsOptions"></div>
        <div class="trait-combinations" id="traitCombinations">
          <div class="trait-combinations-title">Возможные комбинации черт:</div>
          <div id="combinationsList"></div>
        </div>
      </div>
      <div class="result-item" id="deviantProbItem" style="display: none;"><span class="result-label">Девиантная черта</span><span class="result-value" id="deviantProb">—</span></div>
      <div class="final-result">
        <h3>Финальный шанс успеха</h3><div class="big-number" id="totalProb">—</div><div class="attempts">Ожидаемое количество попыток: <strong id="expectedAttempts">—</strong></div>
      </div>
      <div class="info-box" style="margin-bottom:5px;">
        <strong>Интерпретация:</strong> <br>• <span style="color:#13ec8d;">≥50%</span> — Высокий шанс (1–2 попытки) <br>• <span style="color:#f6c23e;">20–49%</span> — Средний (2–5 попыток) <br>• <span style="color:#ff5151">&lt;20%</span> — Низкий (5+ попыток)
      </div>
    </div>
  </div>

  <script>
    // Глобальное управление тултипами
    function toggleTooltip(event, element) {
      if (event.key === 'Enter' || event.key === ' ') {
        event.preventDefault();
        element.classList.toggle('active');
      }
      if (event.key === 'Escape') {
        document.querySelectorAll('.info-icon.active').forEach(icon => icon.classList.remove('active'));
      }
    }
    document.addEventListener('click', function(e) {
      if (!e.target.closest('.info-icon')) {
        document.querySelectorAll('.info-icon.active').forEach(icon => icon.classList.remove('active'));
      }
    });

    // Санитизация
    function sanitizeString(str) {
      const div = document.createElement('div');
      div.textContent = str;
      return div.innerHTML;
    }

    // Валидация
    function validateNumberInput(inputId, min, max, errorId) {
      const input = document.getElementById(inputId);
      const error = document.getElementById(errorId);
      const value = parseInt(input.value);
      if (isNaN(value) || value < min || value > max) {
        input.classList.add('error');
        error.classList.add('show');
        return false;
      } else {
        input.classList.remove('error');
        error.classList.remove('show');
        return true;
      }
    }

    function validateRating(inputId, errorId) {
      const input = document.getElementById(inputId);
      const error = document.getElementById(errorId);
      const value = input.value.trim();
      const ratingRegex = /^[1-5]\/[1-5]$/;
      if (!ratingRegex.test(value)) {
        input.classList.add('error');
        error.classList.add('show');
        return false;
      } else {
        input.classList.remove('error');
        error.classList.remove('show');
        return true;
      }
    }

    // Автокоррекция рейтинга
    function autocorrectRating(input) {
      let val = input.value.trim();
      if (/^[1-5]{2}$/.test(val)) {
        input.value = val[0] + '/' + val[1];
      } else {
        const match = val.match(/^([1-5])[\s\-:]+([1-5])$/);
        if (match) input.value = match[1] + '/' + match[2];
      }
    }

    // Сохранение данных черт
    let traitsDataCache = [];

    function handleNumTraits() {
      const n = parseInt(document.getElementById('numTraits').value) || 0;
      const c = document.getElementById('traitsContainer');
      c.innerHTML = '';
      validateNumberInput('numTraits', 0, 4, 'numTraitsError');

      if (n === 0) {
        c.innerHTML = '<div class="info-box" style="margin-top:10px;"><strong>Информация:</strong> Вы выбрали 0 черт. Калькулятор не будет учитывать черты в расчётах.</div>';
        traitsDataCache = [];
        return;
      }

      for (let i = 1; i <= n; i++) {
        const cached = traitsDataCache[i - 1] || { name: `Черта ${i}`, parents: 1, materials: 3 };
        let d = document.createElement('div');
        d.className = 'trait-config';
        d.innerHTML = `
          <label for="traitName${i}">Название черты ${i}:</label>
          <input type='text' id='traitName${i}' class='trait-name-input' placeholder='Например: Cheer Up 3' value='${sanitizeString(cached.name)}' maxlength="100" aria-label="Название черты ${i}">
          <div class='traits-group'>
            <div style='flex:1;'>
              <label for="traitParents${i}">Родителей с чертой (0-2)</label>
              <input type='number' id='traitParents${i}' class='trait-parents' min='0' max='2' value='${cached.parents}' aria-label="Количество родителей с чертой ${i}">
              <div class="error-message" id="traitParents${i}Error">Значение от 0 до 2</div>
            </div>
            <div style='flex:1;'>
              <label for="traitMaterials${i}">Материалов (0–3)</label>
              <input type='number' id='traitMaterials${i}' class='trait-materials' min='0' max='3' value='${cached.materials}' aria-label="Количество материалов для черты ${i}">
              <div class="error-message" id="traitMaterials${i}Error">Значение от 0 до 3</div>
            </div>
          </div>
        `;
        c.appendChild(d);

        // Валидация в реальном времени
        document.getElementById(`traitParents${i}`).addEventListener('input', () => validateNumberInput(`traitParents${i}`, 0, 2, `traitParents${i}Error`));
        document.getElementById(`traitMaterials${i}`).addEventListener('input', () => validateNumberInput(`traitMaterials${i}`, 0, 3, `traitMaterials${i}Error`));
      }
    }

    // Инициализация
    document.getElementById('sameType').addEventListener('change', function(){
      document.getElementById('materialsGroup').style.display = (this.value === 'no') ? 'block' : 'none';
    });
    document.getElementById('wantDeviantTrait').addEventListener('change', function(){
      document.getElementById('deviantMaterialsGroup').style.display = (this.value === 'yes') ? 'block' : 'none';
    });
    document.getElementById('rating1').addEventListener('input', function() { autocorrectRating(this); });
    document.getElementById('rating2').addEventListener('input', function() { autocorrectRating(this); });
    document.getElementById('rating1').addEventListener('blur', () => validateRating('rating1', 'rating1Error'));
    document.getElementById('rating2').addEventListener('blur', () => validateRating('rating2', 'rating2Error'));
    document.getElementById('numTraits').addEventListener('input', handleNumTraits);

    // Запуск при загрузке
    window.addEventListener('load', () => {
      handleNumTraits();
    });

    function calculateFusion() {
      let isValid = true;
      isValid = validateRating('rating1', 'rating1Error') && isValid;
      isValid = validateRating('rating2', 'rating2Error') && isValid;
      isValid = validateNumberInput('numTraits', 0, 4, 'numTraitsError') && isValid;

      const sT = document.getElementById('sameType').value;
      if (sT === 'no') isValid = validateNumberInput('typeMaterials', 0, 3, 'typeMaterialsError') && isValid;

      const wD = document.getElementById('wantDeviantTrait').value;
      if (wD === 'yes') isValid = validateNumberInput('deviantMaterials', 1, 3, 'deviantMaterialsError') && isValid;

      const numTraits = parseInt(document.getElementById('numTraits').value) || 0;
      traitsDataCache = [];
      for (let i = 1; i <= numTraits; i++) {
        isValid = validateNumberInput(`traitParents${i}`, 0, 2, `traitParents${i}Error`) && isValid;
        isValid = validateNumberInput(`traitMaterials${i}`, 0, 3, `traitMaterials${i}Error`) && isValid;
        const name = document.getElementById(`traitName${i}`).value || `Черта ${i}`;
        const p = parseInt(document.getElementById(`traitParents${i}`).value) || 0;
        const m = parseInt(document.getElementById(`traitMaterials${i}`).value) || 0;
        traitsDataCache.push({ name, parents: p, materials: m });
      }

      if (!isValid) {
        const firstError = document.querySelector('.error');
        if (firstError) firstError.scrollIntoView({ behavior: 'smooth', block: 'center' });
        return;
      }

      // Тип
      let tM = parseInt(document.getElementById('typeMaterials')?.value) || 0;
      tM = Math.max(0, Math.min(3, tM));
      let typeProb = sT === 'no' ? (tM === 0 ? 50 : tM === 1 ? 65 : tM === 2 ? 75 : 80) : 100;

      // Рейтинг
      let r1 = document.getElementById('rating1').value.trim();
      let r2 = document.getElementById('rating2').value.trim();
      let tR = document.getElementById('targetRating').value;
      let ratingResult = calculateRatingDistribution(r1, r2, tR);

      // Черты
      let traitsProb = 1;
      let traitsList = [];
      if (numTraits > 0) {
        for (let i = 1; i <= numTraits; i++) {
          let name = sanitizeString(document.getElementById(`traitName${i}`).value || `Черта ${i}`);
          let p = Math.max(0, Math.min(2, parseInt(document.getElementById(`traitParents${i}`).value) || 0));
          let m = Math.max(0, Math.min(3, parseInt(document.getElementById(`traitMaterials${i}`).value) || 0));
          let prb = p === 2 ? 1 : p === 1 ? 0.5 + m * 0.1 : 0;
          traitsList.push({ name, parents: p, materials: m, prob: prb });
          traitsProb *= prb;
        }
        traitsProb *= 100;
      } else {
        traitsProb = 100;
      }

      // Девиант
      let deviantProb = 1;
      let showDev = document.getElementById('deviantProbItem');
      if (wD === 'yes') {
        let dM = Math.max(1, Math.min(3, parseInt(document.getElementById('deviantMaterials').value) || 1));
        deviantProb = (1 - Math.pow(0.75, dM)) * 100;
        showDev.style.display = 'flex';
      } else {
        showDev.style.display = 'none';
      }

      // Финал
      let total = typeProb / 100 * ratingResult.targetProb / 100 * traitsProb / 100 * (wD === 'yes' ? deviantProb / 100 : 1) * 100;

      // Отображение
      document.getElementById('typeProb').textContent = typeProb.toFixed(1) + '%';
      displayRatingBreakdown(ratingResult);
      document.getElementById('traitsBreakdown').style.display = numTraits > 0 ? 'block' : 'none';
      if (numTraits > 0) displayTraitsBreakdown(traitsList);
      if (wD === 'yes') document.getElementById('deviantProb').textContent = deviantProb.toFixed(1) + '%';

      let tPE = document.getElementById('totalProb');
      tPE.textContent = total.toFixed(2) + '%';
      let exp = total > 0 ? (100 / total).toFixed(1) : '∞';
      document.getElementById('expectedAttempts').textContent = exp;
      tPE.className = 'big-number';
      if (total >= 50) tPE.classList.add('high');
      else if (total >= 20) tPE.classList.add('medium');
      else tPE.classList.add('low');

      document.getElementById('results').classList.add('show');
      document.getElementById('results').scrollIntoView({ behavior: 'smooth', block: 'nearest' });
    }

    function calculateRatingDistribution(r1s, r2s, targetSelection) {
      const parse = s => { let p = s.split('/'); return { m: parseInt(p[0]) || 0, pw: parseInt(p[1]) || 0 }; };
      let r1 = parse(r1s), r2 = parse(r2s);
      let avgM = (r1.m + r2.m) / 2, avgP = (r1.pw + r2.pw) / 2;
      let currentM = Math.round(avgM), currentP = Math.round(avgP);
      let sameKey = `${currentM}/${currentP}`;

      let distribution = {};
      let totalProb = 0;

      // Базовые вероятности (до нормализации)
      let sameProb = 44, upProb = 33, downProb = 18, extProb = 5;

      // Same
      distribution[sameKey] = { prob: sameProb, type: 'same', rating: { m: currentM, pw: currentP } };
      totalProb += sameProb;

      // Upgrades
      let upgrades = [
        { m: Math.min(5, currentM + 1), pw: currentP },
        { m: currentM, pw: Math.min(5, currentP + 1) },
        { m: Math.min(5, currentM + 1), pw: Math.min(5, currentP + 1) }
      ];
      let uniqueUp = [...new Set(upgrades.map(u => `${u.m}/${u.pw}`))].filter(k => k !== sameKey);
      let upEach = upProb / uniqueUp.length;
      uniqueUp.forEach(k => {
        let [m, pw] = k.split('/').map(Number);
        distribution[k] = { prob: upEach, type: 'upgrade', rating: { m, pw } };
        totalProb += upEach;
      });

      // Downgrades
      let downgrades = [
        { m: Math.max(1, currentM - 1), pw: currentP },
        { m: currentM, pw: Math.max(1, currentP - 1) }
      ];
      let uniqueDown = [...new Set(downgrades.map(d => `${d.m}/${d.pw}`))].filter(k => !distribution[k]);
      let downEach = downProb / uniqueDown.length;
      uniqueDown.forEach(k => {
        let [m, pw] = k.split('/').map(Number);
        distribution[k] = { prob: downEach, type: 'downgrade', rating: { m, pw } };
        totalProb += downEach;
      });

      // Extremes (±2)
      let extremes = [
        { m: Math.min(5, currentM + 2), pw: currentP },
        { m: Math.max(1, currentM - 2), pw: currentP },
        { m: currentM, pw: Math.min(5, currentP + 2) },
        { m: currentM, pw: Math.max(1, currentP - 2) }
      ];
      extremes.forEach(e => {
        let key = `${e.m}/${e.pw}`;
        if (!distribution[key]) {
          distribution[key] = { prob: extProb / 4, type: 'extreme', rating: e };
          totalProb += extProb / 4;
        }
      });

      // Нормализация
      Object.keys(distribution).forEach(k => distribution[k].prob = distribution[k].prob * 100 / totalProb);

      // Цель
      let targetProb = 0;
      let targetKey = '';
      if (targetSelection === 'same') {
        targetProb = distribution[sameKey]?.prob || 0;
        targetKey = sameKey;
      } else if (targetSelection === 'upgrade') {
        targetProb = Object.values(distribution).filter(d => d.type === 'upgrade').reduce((s, d) => s + d.prob, 0);
      } else {
        targetKey = targetSelection;
        targetProb = distribution[targetKey]?.prob || 0;
      }

      return { distribution, targetProb, targetKey };
    }

    function displayRatingBreakdown(data) {
      let container = document.getElementById('ratingOptions');
      container.innerHTML = '';
      let sorted = Object.entries(data.distribution).sort((a, b) => b[1].prob - a[1].prob);
      for (let [key, info] of sorted) {
        let isTarget = key === data.targetKey;
        let typeClass = isTarget ? 'target' : info.type;
        let div = document.createElement('div');
        div.className = `rating-option ${typeClass}`;
        let name = document.createElement('span');
        name.className = 'rating-name';
        name.textContent = key;
        if (isTarget) {
          let badge = document.createElement('span');
          badge.className = 'badge target-badge';
          badge.textContent = 'ЦЕЛЬ';
          name.appendChild(badge);
        }
        let prob = document.createElement('span');
        prob.className = 'rating-prob';
        prob.textContent = info.prob.toFixed(1) + '%';
        div.appendChild(name);
        div.appendChild(prob);
        let bar = document.createElement('div');
        bar.className = 'rating-bar';
        let fill = document.createElement('div');
        fill.className = 'rating-bar-fill';
        fill.style.width = Math.min(100, info.prob * 2) + '%';
        bar.appendChild(fill);
        let wrapper = document.createElement('div');
        wrapper.appendChild(div);
        wrapper.appendChild(bar);
        container.appendChild(wrapper);
      }
    }

    function displayTraitsBreakdown(traitsData) {
      let container = document.getElementById('traitsOptions');
      container.innerHTML = '';
      if (!traitsData.length) {
        container.innerHTML = '<div class="no-traits-message">Черты не указаны</div>';
        document.getElementById('traitCombinations').style.display = 'none';
        return;
      }
      for (let t of traitsData) {
        let p = t.prob * 100;
        let cls = p >= 80 ? 'guaranteed' : p >= 60 ? 'high-prob' : p >= 40 ? 'medium-prob' : 'low-prob';
        let div = document.createElement('div');
        div.className = `trait-option ${cls}`;
        let name = document.createElement('span');
        name.className = 'trait-name';
        name.textContent = t.name;
        if (p === 100) {
          let badge = document.createElement('span');
          badge.className = 'badge guaranteed-badge';
          badge.textContent = '100%';
          name.appendChild(badge);
        }
        let prob = document.createElement('span');
        prob.className = 'trait-prob';
        prob.textContent = p.toFixed(1) + '%';
        div.appendChild(name);
        div.appendChild(prob);
        let bar = document.createElement('div');
        bar.className = 'trait-bar';
        let fill = document.createElement('div');
        fill.className = 'trait-bar-fill';
        fill.style.width = p + '%';
        bar.appendChild(fill);
        let wrapper = document.createElement('div');
        wrapper.appendChild(div);
        wrapper.appendChild(bar);
        container.appendChild(wrapper);
      }
      document.getElementById('traitCombinations').style.display = 'block';
      displayTraitCombinations(traitsData);
    }

    function displayTraitCombinations(traitsData) {
      let container = document.getElementById('combinationsList');
      container.innerHTML = '';
      let allProb = traitsData.reduce((p, t) => p * t.prob, 1) * 100;
      let div = document.createElement('div');
      div.className = 'combo-item';
      div.innerHTML = `<span class="combo-traits">Все ${traitsData.length} черты</span><span class="combo-prob">${allProb.toFixed(1)}%</span>`;
      container.appendChild(div);

      if (traitsData.length > 1) {
        for (let i = 0; i < traitsData.length; i++) {
          let prob = 1;
          let names = [];
          for (let j = 0; j < traitsData.length; j++) {
            if (i === j) prob *= (1 - traitsData[j].prob);
            else { prob *= traitsData[j].prob; names.push(traitsData[j].name); }
          }
          if (prob > 0.001) {
            let d = document.createElement('div');
            d.className = 'combo-item';
            d.innerHTML = `<span class="combo-traits">${names.join(', ')}</span><span class="combo-prob">${(prob * 100).toFixed(1)}%</span>`;
            container.appendChild(d);
          }
        }
      }

      let noProb = traitsData.reduce((p, t) => p * (1 - t.prob), 1) * 100;
      if (noProb > 0.001) {
        let d = document.createElement('div');
        d.className = 'combo-item';
        d.innerHTML = `<span class="combo-traits">Без черт</span><span class="combo-prob">${noProb.toFixed(1)}%</span>`;
        container.appendChild(d);
      }
    }
  </script>
</body>
</html>
