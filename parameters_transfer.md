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
`function getXmlHttp(){
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
}`
