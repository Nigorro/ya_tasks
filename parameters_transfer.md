Передача параметров на сервер
==========
Способы передачи:
* XMLHttpRequest,
* JSONP,
* Iframe.

**XMLHttpRequest**
Используя запросы `HTTP` или `HTTPS` повзляет напрямую к веб-серверу загружать данные и загружает данные
ответа сервера напрямую в вызывающий скрипт. Достаточно кроссбраузерный способ, со стандартным объектом `XMLHttpRequest`.

`XMLHttpRequest` может работать с данными в любом текстовом формате (`XML`, `HTML`, `JSON`).

Функция создания `XMLHttpRequest`:
``` js
function getXmlHttp(){
  var xmlhttp;
  try {
    xmlhttp = new ActiveXObject("Msxml2.XMLHTTP");
  } catch (e) {
    try {
      xmlhttp = new ActiveXObject("Microsoft.XMLHTTP");
    } catch (E) {
      xmlhttp = false;
    }
  }
  if (!xmlhttp && typeof XMLHttpRequest!='undefined') {
    xmlhttp = new XMLHttpRequest();
  }
  return xmlhttp;
}
```

***JSONP***
«JSON with padding» дополнение к JSON. Особенностью способа является то, что позвляет запросить данные с сервера находящегося на другом домене,  операцию, запрещённую в большинстве браузеров из-за политики ограничения домена. 
Формат больше ориентирован не на передачу данных, а на получение данных с сервера.  Типиченое применение JSONP предоставляет междоменный доступ к существующему JSON API путем оборачивания начинки JSON в вызов функции к неким JSON-данным.

типичное применение JSONP предоставляет междоменный доступ к существующему JSON API путём оборачивания начинки JSON в вызов функции.


***IFRAME***
Универсальный инструмент, подерживаемый всеми браузерами.
Для общения с сервером создается невидимый `iframe`. Простая смена URL этого iframe - запрос к серверу за данными. Кроме того, в iframe можно отправлять post-запросы.

``` js
    var frameName = 'name',
    form = document.createElement('form');
    form.action = url;
    form.method = 'POST';
    form.target = frameName;
    var iframe = document.createElement('iframe');
    iframe.src = 'javascript:false';
    iframe.name = frameName;
    
    document.body.appendChild(form);
    document.body.appendChild(iframe);
    form.submit();
```
В этом случае обработчик url должен сообщить вызывающей странице об успехе или ошибке обработки отправленных данных. Есть несколько способов сделать это:

Вызвать обработчик, установленный на вызывающей странице: window.parent.callback(data). Наиболее кроссбраузерный способ.
Отправить вызывающему окну сообщение: window.parent.postMessage(message, '*'). Поддерживается всеми современными браузерами (IE8+).
Изменить хеш родительского окна через window.parent.location. Хак, использующийся для старых браузеров, в основном для кросс-доменных запросов.
Вызвать событие через dispatchEvent/fireEvent родительского окна.
С помощью iframe можно отправзять GET запросы. GET-запрос - всего лишь перевод iframe на новый URL. Его лучше всего осуществлять вызовом iframeDocument.location.src.replace(newURL).
Такой синтаксис в отличие от сабмита GET-формы в iframe или iframeDocument.location.src=..., оставляет history чистой в ряде браузеров. Так что переходы между адресами внутри iframe не отразятся на
кнопках back-forward и списке посещенных страниц.
Для POST запросов Ддостаточно задать форме form атрибут form.target='имя ифрейма' и вызвать form.submit(). 

***Кроссбраузерный способ***
Одноим из наимболее кросбраузерных способов является XMLHttpRequest, в случаее если запросы осуществляются на домен с которого загружена страница. Данный способ поддерживается всеми соверменными браузерами и с частью старыми.
