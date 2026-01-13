<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My English App</title>
    <style>
        :root {
            --primary: #4a90e2;
            --success: #2ecc71;
            --danger: #e74c3c;
            --glass: rgba(255, 255, 255, 0.95);
        }

        body { 
            font-family: 'Segoe UI', Roboto, sans-serif; 
            background: radial-gradient(circle at top, #2c3e50, #000000);
            display: flex; flex-direction: column; align-items: center; padding: 20px; min-height: 100vh; margin: 0;
            color: #333;
        }

        .app-header { color: #fff; text-shadow: 0 4px 10px rgba(0,0,0,0.3); font-size: 2.5rem; margin: 20px 0; font-weight: bold; }

        .menu { margin-bottom: 25px; display: flex; flex-wrap: wrap; justify-content: center; gap: 10px; }
        .menu button { 
            padding: 12px 20px; cursor: pointer; border: none; background: #007bff; 
            color: #fff; border-radius: 10px; transition: 0.3s; font-weight: bold;
            box-shadow: 0 4px 15px rgba(0,0,0,0.2);
        }
        .menu button:hover { background: #0056b3; transform: translateY(-2px); }

        .container { 
            background: var(--glass); padding: 40px; border-radius: 30px; 
            box-shadow: 0 20px 50px rgba(0,0,0,0.5); width: 100%; max-width: 700px; 
            text-align: center; box-sizing: border-box;
        }

        .section { display: none; animation: fadeIn 0.4s ease; }
        .active { display: block; }
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

        .card-box { 
            padding: 80px 20px; border: 2px dashed var(--primary); border-radius: 25px; 
            font-size: 32px; font-weight: bold; cursor: pointer; background: #fff; 
            margin-bottom: 30px; color: #2c3e50; transition: transform 0.2s;
        }

        .word-counter-badge {
            background: #e1f5fe; color: #0288d1; padding: 8px 15px; 
            border-radius: 50px; font-weight: bold; margin-bottom: 20px; display: inline-block;
        }

        /* ТЕСТОВЫЕ КНОПКИ */
        .test-block { border: 1px solid #ddd; border-radius: 15px; padding: 20px; margin-bottom: 20px; background: #fff; text-align: left; }
        .tf-btn { 
            padding: 15px; border: 2px solid #eee; border-radius: 10px; 
            cursor: pointer; font-weight: bold; background: #fff; transition: 0.2s;
            margin: 5px; min-width: 80px;
        }
        .mc-btn {
            display: block; width: 100%; padding: 15px; margin: 8px 0;
            background: #f9f9f9; border: 2px solid #eee; border-radius: 12px;
            cursor: pointer; text-align: left; transition: 0.2s;
        }

        /* Состояния выбора */
        .selected-choice { border-color: var(--primary) !important; background: #eef6ff !important; }
        .selected-true { border-color: var(--success) !important; background: #f0fff4 !important; }
        .selected-false { border-color: var(--danger) !important; background: #fff5f5 !important; }

        /* Результаты */
        .correct-ans { background: #d4edda !important; border-color: var(--success) !important; }
        .wrong-ans { background: #f8d7da !important; border-color: var(--danger) !important; }

        input, textarea { width: 100%; padding: 15px; margin: 10px 0; border: 2px solid #eee; border-radius: 12px; font-size: 16px; box-sizing: border-box; }
        .btn-main { background: var(--success); color: white; border: none; padding: 18px; border-radius: 12px; width: 100%; cursor: pointer; font-size: 18px; font-weight: bold; }
    </style>
</head>
<body>

    <div class="app-header">🚀 My English App</div>

    <div class="menu">
        <button onclick="changeTab('cardTab')">📇 Карточки</button>
        <button onclick="changeTab('testTab')">📝 Тест</button>
        <button onclick="changeTab('writeTab')">✍️ Написание</button>
        <button onclick="changeTab('smartTab')">🔄 Повторение</button>
        <button onclick="changeTab('settingTab')">⚙️ Настройки</button>
    </div>

    <div class="container">
        <div id="testTab" class="section">
            <div id="testSetupArea">
                <div class="word-counter-badge" id="testBadge">В словаре: 0 слов</div>
                <h3>Настройка теста</h3>
                <p>Количество слов:</p>
                <input type="number" id="testInputCount" style="width: 100px; text-align: center;">
                <button class="btn-main" onclick="startTest()">Начать тест</button>
            </div>
            <div id="testArea"></div>
            <div id="testResults" style="display:none">
                <h2 id="testScore"></h2>
                <button class="btn-main" style="background:#6c757d" onclick="changeTab('testTab')">Выйти</button>
            </div>
            <button id="testCheckBtn" style="display:none; margin-top:20px" class="btn-main" onclick="checkTest()">Проверить ответы</button>
        </div>

        <div id="cardTab" class="section active">
            <div class="card-box" id="cardDisplay" onclick="flipCard()">Нажми для начала</div>
            <button class="btn-main" style="background:#6c757d" onclick="initCard()">Следующее слово →</button>
        </div>

        <div id="writeTab" class="section">
            <h2 id="writeQuest">...</h2>
            <input type="text" id="writeInput" placeholder="Перевод...">
            <button class="btn-main" onclick="checkWrite()">Проверить</button>
            <div id="writeFeed"></div>
            <button id="writeNext" style="display:none; margin-top:10px;" class="btn-main" onclick="initWrite()">Дальше</button>
        </div>

        <div id="smartTab" class="section">
            <div id="smartProg"></div>
            <div class="card-box" id="smartDisplay" onclick="flipSmart()">Начать</div>
            <div id="smartControls" style="display:none; gap:10px;">
                <button class="btn-main" style="background:var(--danger)" onclick="handleSmart(false)">Не помню</button>
                <button class="btn-main" onclick="handleSmart(true)">Знаю</button>
            </div>
            <button id="smartResetBtn" style="display:none" class="btn-main" onclick="initSmart()">Заново</button>
        </div>

        <div id="settingTab" class="section">
            <div class="word-counter-badge" id="settingBadge">Всего слов: 0</div>
            <textarea id="massInput" rows="6" placeholder="слово;перевод"></textarea>
            <button class="btn-main" onclick="massAdd()">Добавить список</button>
        </div>
    </div>

<script>
    let myWords = JSON.parse(localStorage.getItem('myWords')) || [];
    let currentWord = null;
    let smartQueue = [];
    let isFlipped = false;

    function speak(text) {
        window.speechSynthesis.cancel();
        let msg = new SpeechSynthesisUtterance(text);
        msg.lang = 'en-US';
        window.speechSynthesis.speak(msg);
    }

    function updateCounters() {
        const count = myWords.length;
        document.getElementById('testBadge').innerText = `В словаре: ${count} слов`;
        document.getElementById('settingBadge').innerText = `Всего слов: ${count}`;
        document.getElementById('testInputCount').value = count;
    }

    function changeTab(tabId) {
        document.querySelectorAll('.section').forEach(s => s.classList.remove('active'));
        document.getElementById(tabId).classList.add('active');
        updateCounters();
        if(tabId === 'cardTab') initCard();
        if(tabId === 'writeTab') initWrite();
        if(tabId === 'smartTab') initSmart();
    }

    // --- ТЕСТ (ИСПРАВЛЕННЫЙ ВЫБОР) ---
    function startTest() {
        let count = parseInt(document.getElementById('testInputCount').value) || 0;
        if(count <= 0 || myWords.length < 2) return alert("Мало слов!");
        count = Math.min(count, myWords.length);
        document.getElementById('testSetupArea').style.display = "none";
        document.getElementById('testCheckBtn').style.display = "block";
        let shuffled = [...myWords].sort(() => 0.5 - Math.random()).slice(0, count);
        let html = "";

        shuffled.forEach((q, i) => {
            const isTF = Math.random() > 0.5;
            if (isTF) {
                const isCor = Math.random() > 0.5;
                const trans = isCor ? q.en : myWords[Math.floor(Math.random()*myWords.length)].en;
                html += `<div class="test-block" id="tb_${i}" data-type="tf" data-answer="${isCor}">
                    <p><b>${i+1}. ${q.ru} = ${trans}?</b></p>
                    <button class="tf-btn" id="tf_t_${i}" onclick="selectTF(${i}, true)">ВЕРНО</button>
                    <button class="tf-btn" id="tf_f_${i}" onclick="selectTF(${i}, false)">ЛОЖЬ</button>
                </div>`;
            } else {
                let opts = [q.en];
                while(opts.length < Math.min(4, myWords.length)) {
                    let r = myWords[Math.floor(Math.random()*myWords.length)].en;
                    if(!opts.includes(r)) opts.push(r);
                }
                opts.sort(() => 0.5 - Math.random());
                html += `<div class="test-block" id="tb_${i}" data-type="mc" data-answer="${q.en}">
                    <p><b>${i+1}. Перевод "${q.ru}":</b></p>
                    ${opts.map((o, optIdx) => `<button class="mc-btn" id="mc_${i}_${optIdx}" onclick="selectMC(${i}, '${o}', ${optIdx})">${o}</button>`).join('')}
                </div>`;
            }
        });
        document.getElementById('testArea').innerHTML = html;
    }

    function selectTF(i, val) {
        let b = document.getElementById(`tb_${i}`);
        b.dataset.userVal = val;
        b.querySelectorAll('.tf-btn').forEach(btn => btn.classList.remove('selected-true', 'selected-false'));
        document.getElementById(`tf_${val?'t':'f'}_${i}`).classList.add(val?'selected-true':'selected-false');
    }

    function selectMC(i, word, optIdx) {
        let b = document.getElementById(`tb_${i}`);
        b.dataset.userVal = word;
        b.querySelectorAll('.mc-btn').forEach(btn => btn.classList.remove('selected-choice'));
        document.getElementById(`mc_${i}_${optIdx}`).classList.add('selected-choice');
    }

    function checkTest() {
        let score = 0;
        document.querySelectorAll('.test-block').forEach(b => {
            let type = b.dataset.type;
            let ans = b.dataset.answer;
            let user = b.dataset.userVal;
            
            let isCorrect = (type === 'tf') ? (user === ans) : (user === ans);
            
            if(isCorrect) {
                score++;
                b.classList.add('correct-ans');
            } else {
                b.classList.add('wrong-ans');
            }
        });
        document.getElementById('testResults').style.display = "block";
        document.getElementById('testScore').innerText = `Твой счет: ${score}`;
        document.getElementById('testCheckBtn').style.display = "none";
        window.scrollTo(0,0);
    }

    // --- КАРТОЧКИ ---
    function initCard() {
        if(!myWords.length) return;
        currentWord = myWords[Math.floor(Math.random() * myWords.length)];
        isFlipped = false;
        document.getElementById('cardDisplay').innerText = currentWord.ru;
    }

    function flipCard() {
        if(!currentWord) return;
        isFlipped = !isFlipped;
        document.getElementById('cardDisplay').innerText = isFlipped ? currentWord.en : currentWord.ru;
        if(isFlipped) speak(currentWord.en);
    }

    // --- ПОВТОРЕНИЕ ---
    function initSmart() {
        if(!myWords.length) return;
        smartQueue = [...myWords].sort(() => 0.5 - Math.random());
        document.getElementById('smartControls').style.display = "flex";
        document.getElementById('smartResetBtn').style.display = "none";
        updateSmart();
    }
    function updateSmart() {
        if(!smartQueue.length) {
            document.getElementById('smartDisplay').innerText = "Готово!";
            document.getElementById('smartControls').style.display = "none";
            document.getElementById('smartResetBtn').style.display = "block";
            return;
        }
        isFlipped = false;
        document.getElementById('smartDisplay').innerText = smartQueue[0].ru;
        document.getElementById('smartProg').innerText = `Осталось: ${smartQueue.length}`;
    }
    function flipSmart() {
        if(!smartQueue.length) return;
        isFlipped = !isFlipped;
        document.getElementById('smartDisplay').innerText = isFlipped ? smartQueue[0].en : smartQueue[0].ru;
        if(isFlipped) speak(smartQueue[0].en);
    }
    function handleSmart(k) {
        let w = smartQueue.shift();
        if(!k) smartQueue.push(w);
        updateSmart();
    }

    // --- НАСТРОЙКИ ---
    function massAdd() {
        let input = document.getElementById('massInput').value.trim();
        input.split('\n').forEach(l => {
            let p = l.split(';');
            if(p.length === 2) myWords.push({ru: p[0].trim(), en: p[1].trim()});
        });
        localStorage.setItem('myWords', JSON.stringify(myWords));
        updateCounters();
        alert("ОК!");
    }

    updateCounters();
    initCard();
</script>
</body>
</html>
