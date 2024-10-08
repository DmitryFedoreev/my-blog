---
title: Генератор UTM-меток
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

<div class="utm-generator">
  <form id="utm-generator">
    <div class="input-group">
      <label for="url">Введите URL: 
        <span class="tooltip" title="Полный адрес страницы, на которую будет вести ссылка.">?</span>
      </label>
      <input type="text" id="url" placeholder="https://example.com" required>
    </div>
    <div class="input-group">
      <label for="utm_source">utm_source: 
        <span class="tooltip" title="Источник трафика (например, google, newsletter).">?</span>
      </label>
      <input type="text" id="utm_source" placeholder="source" required>
    </div>
    <div class="input-group">
      <label for="utm_medium">utm_medium: 
        <span class="tooltip" title="Тип трафика (например, cpc, email).">?</span>
      </label>
      <input type="text" id="utm_medium" placeholder="medium" required>
    </div>
    <div class="input-group">
      <label for="utm_campaign">utm_campaign: 
        <span class="tooltip" title="Название кампании для отслеживания.">?</span>
      </label>
      <input type="text" id="utm_campaign" placeholder="campaign" required>
    </div>
    <div class="input-group">
      <label for="utm_term">utm_term: 
        <span class="tooltip" title="Ключевые слова для платных поисковых объявлений.">?</span>
      </label>
      <input type="text" id="utm_term" placeholder="term">
    </div>
    <div class="input-group">
      <label for="utm_content">utm_content: 
        <span class="tooltip" title="Используется для различия похожих объявлений.">?</span>
      </label>
      <input type="text" id="utm_content" placeholder="content">
    </div>
    <button type="submit">Сгенерировать UTM-ссылку</button>
  </form>
  
  <!-- Блок для вывода сгенерированной ссылки -->
  <div id="generated-link" style="margin-top: 20px; padding: 10px; border: 1px solid #ccc; border-radius: 5px; background-color: #f9f9f9;">
    <strong>Сгенерированная ссылка появится здесь</strong>
  </div>
</div>


<script>
  document.getElementById('utm-generator').addEventListener('submit', function(e) {
    e.preventDefault(); // Предотвращаем стандартное поведение формы
    
    // Получаем значения из полей
    const url = document.getElementById('url').value;
    const utmSource = document.getElementById('utm_source').value;
    const utmMedium = document.getElementById('utm_medium').value;
    const utmCampaign = document.getElementById('utm_campaign').value;
    const utmTerm = document.getElementById('utm_term').value;
    const utmContent = document.getElementById('utm_content').value;


    // Проверяем, что обязательные поля заполнены
    if (!url || !utmSource || !utmMedium || !utmCampaign) {
      alert('Пожалуйста, заполните все обязательные поля!');
      return;
    }


    // Формируем UTM-ссылку
    let utmLink = `${url}?utm_source=${encodeURIComponent(utmSource)}&utm_medium=${encodeURIComponent(utmMedium)}&utm_campaign=${encodeURIComponent(utmCampaign)}`;
    
    if (utmTerm) {
      utmLink += `&utm_term=${encodeURIComponent(utmTerm)}`;
    }
    
    if (utmContent) {
      utmLink += `&utm_content=${encodeURIComponent(utmContent)}`;
    }


    // Выводим сгенерированную ссылку в блок #generated-link
    document.getElementById('generated-link').innerHTML = `<strong>Сгенерированная ссылка:</strong><br><textarea id="generated-link-text" style="width: 100%; height: 100px; padding: 10px; border: 1px solid #ccc; border-radius: 5px;" readonly>${utmLink}</textarea>`;
  });
</script>