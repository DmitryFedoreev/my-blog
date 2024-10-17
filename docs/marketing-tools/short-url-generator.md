---
title: Сокращение ссылок
---

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
    const domain = new URL(longUrl).origin; // Получаем основной домен  
    const uniqueId = Math.random().toString(36).substring(2, 8); // Генерируем случайный идентификатор  
    return `${domain}/${uniqueId}`;  
  }  

  function copyToClipboard(url) {  
    navigator.clipboard.writeText(url).then(() => {  
      alert('Ссылка скопирована в буфер обмена!');  
    }, (err) => {  
      console.error('Ошибка копирования: ', err);  
    });  
  }  
</script>