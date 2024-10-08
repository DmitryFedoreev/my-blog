---
title: Сокращение ссылок
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

<div class="url-generator">  
  <p>Этот инструмент позволяет вам быстро генерировать краткие ссылки на основе длинных URL. Просто введите длинный URL ниже, и вы получите его краткую версию.</p>  
  <form id="short-url-form">  
    <div class="input-group">  
      <label for="url">Введите длинный URL:<span class="tooltip" title="Введите полный адрес, который нужно сократить.">?</span></label>  
      <input type="text" id="url" placeholder="https://example.com" required>  
    </div>  
    <button type="submit" class="btn">Сгенерировать</button>  
  </form>  
  <div id="generated-link"></div>  
</div> 
 
<script>  
  document.getElementById('short-url-form').addEventListener('submit', function(event) {  
    event.preventDefault(); // Предотвращаем отправку формы  
 
    const urlInput = document.getElementById('url').value; // Получаем значение из поля ввода  
    const shortUrl = generateShortUrl(urlInput); // Генерируем краткую ссылку  
 
    document.getElementById('generated-link').innerHTML = `  
      <p>Ваша краткая ссылка: <a href="${shortUrl}" target="_blank">${shortUrl}</a>  
        <span class="copy-icon" title="Скопировать" onclick="copyToClipboard('${shortUrl}')">📋</span> 
      </p>  
    `;  
  });  
 
  function generateShortUrl(longUrl) {  
    const baseUrl = 'https://short.url/';  
    const randomString = Math.random().toString(36).substring(2, 8); // Генерируем случайную строку  
    return baseUrl + randomString;  
  }  
 
  function copyToClipboard(url) { 
    navigator.clipboard.writeText(url).then(() => { 
      alert('Ссылка скопирована в буфер обмена!'); 
    }, (err) => { 
      console.error('Ошибка копирования: ', err); 
    }); 
  } 
</script>