---
title: Нормализатор фраз
---

<!-- Yandex.Metrika counter --> 
<script type="text/javascript" > 
   (function(m,e,t,r,i,k,a){m[i]=m[i]||function(){(m[i].a=m[i].a||[]).push(arguments)}; 
   m[i].l=1*new Date(); 
   for (var j = 0; j < document.scripts.length; j++) {if (document.scripts[j].src === r) { return; }} 
   k=e.createElement(t),a=e.getElementsByTagName(t)[0],k.async=1,k.src=r,a.parentNode.insertBefore(k,a)}) 
   (window, document, "script", "https://mc.yandex.ru/metrika/tag.js", "ym"); 
 
   ym(98576815, "init", { 
        clickmap:true, 
        trackLinks:true, 
        accurateTrackBounce:true, 
        webvisor:true 
   }); 
</script> 
<noscript><div><img src="https://mc.yandex.ru/watch/98576815" style="position:absolute; left:-9999px;" alt="" /></div></noscript> 
<!-- /Yandex.Metrika counter -->

<p>Инструмент чистит ваше ядро от мусора, уберет дубли слов и лишние символы.</p> 
<ol> 
    <li>Вставьте фразы в окно ниже.</li> 
    <li>Нажмите кнопку нормализовать фразы.</li> 
    <li>Скопируйте фразы.</li> 
</ol> 
 
<p>Выделите чек боксы под фразами, чтобы считать перестановку фраз дублями и удалить их, удалить спец символы («+», «-», «?»), преобразовать с Ё на Е.</p> 

<details> 
    <summary style="cursor: pointer; color: blue;">Как работает инструмент</summary> 
    <p>Цель</p>  
    <p>Процесс нормализации ключевых фраз значительно повышает эффективность контекстной рекламы. Это достигается за счет систематизации и устранения дубликатов фраз, а также стандартизации формата ключевых фраз для их дальнейшей группировки. Данный инструмент позволяет экономить время маркетолога и, что более важно, снижает затраты на контекстную рекламу, исключая повторяющиеся фразы.</p>  
    <p>Преимущества нормализации ключевых фраз:</p>  
    <ul>  
        <li><strong>Удаление дубликатов:</strong> Система автоматически выявляет и устраняет повторяющиеся ключевые фразы, что предотвращает ненужные расходы на рекламу одних и тех же словосочетаний.</li>  
        <li><strong>Сортировка:</strong> Инструмент предоставляет возможность сортировки ключевых фраз по алфавиту или другим критериям, что облегчает процесс группировки.</li>  
        <li><strong>Импорт фраз:</strong> Загружайте списки фраз из различных источников в сервис, и вы получите обработанные фразы, готовые к дальнейшей работе.</li>  
        <li><strong>Обработка перестановок:</strong> Сервис также может обрабатывать фразы, которые содержат одни и те же слова, расположенные в разном порядке, рассматривая их как дубликаты. Это помогает уменьшить общий объем списка ключевых фраз и упростить управление ими.</li>  
        <li><strong>Замена символов:</strong> Система автоматически заменяет букву Ë на букву Е, устраняя потенциальные различия при поиске и отображении рекламы с использованием этих символов.</li>  
        <li><strong>Удаление специальных символов:</strong> Сервис способен исключать символы, такие как "+", "-", «?», что минимизирует вероятность ошибок при поиске и отображении рекламы.</li>  
</ul>
</details>

<textarea id="input-phrases" rows="10" cols="50"></textarea> 

<label><input type="checkbox" id="remove-permutations" checked> Считать перестановку фраз дублями</label><br> 
<label><input type="checkbox" id="remove-special-chars" checked> Удалить спецсимволы: "+", "-", "?"</label><br> 
<label><input type="checkbox" id="replace-e" checked> Преобразовать Ё в Е</label>
 
<button onclick="normalizePhrases()">Нормализовать фразы</button> 
<button onclick="copyPhrases()">Скопировать фразы</button> 

<p>Результат:</p> 
<pre id="output-phrases"></pre> 
<p>Кол-во фраз: <span id="phrase-count">0</span></p> 

<script>


function cleanPhrase(phrase) {  
    // Убираем спецсимволы  
    if (document.getElementById('remove-special-chars').checked) {  
        phrase = phrase.replace(/[+?]/g, '').replace(/-/g, '');  
    }  
    // Преобразуем Ё в Е  
    if (document.getElementById('replace-e').checked) {  
        phrase = phrase.replace(/Ё/g, 'Е');  
    }  
    return phrase.trim().toLowerCase(); // Приводим к нижнему регистру  
}  

function normalizePhrases() {  
    // Получаем введенные фразы  
    const input = document.getElementById('input-phrases').value;  
    const phrases = input.split('\n').map(phrase => phrase.trim()).filter(phrase => phrase);  
 
    // Очищаем фразы  
    const cleanedPhrases = phrases.map(cleanPhrase);  
 
    // Удаление дубликатов с учетом перестановок  
    const uniquePhrases = [];  
    const seen = new Set();  
 
    cleanedPhrases.forEach(phrase => {  
        // Генерируем отсортированную версию фразы для учета перестановок  
        const sortedPhrase = phrase.split('').sort().join('');  
        if (!seen.has(sortedPhrase)) {  
            seen.add(sortedPhrase);  
            uniquePhrases.push(phrase);  
        }  
    });  
 
    // Сортировка финального списка  
    uniquePhrases.sort();  
 
    // Обновляем вывод и количество фраз  
    document.getElementById('output-phrases').textContent = uniquePhrases.join('\n');  
    document.getElementById('phrase-count').textContent = uniquePhrases.length;  
}  
 
function copyPhrases() {  
    const output = document.getElementById('output-phrases').textContent;  
    navigator.clipboard.writeText(output).then(() => {  
        alert('Фразы скопированы в буфер обмена!');  
    }).catch(err => {  
        console.error('Ошибка при копировании:', err);  
    });  
}  
</script>