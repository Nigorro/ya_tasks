Ответы на вопросы
==========
**Вопрос 1**
> Необходимо передать на сервер набор параметров, не перезагружая при этом страницу браузера. Расскажите, как это сделать: перечислите все возможные способы и назовите самый кроссбраузерный.

**Вопрос 2**
> Мы уделяем большое внимание производительности наших приложений. Нередко случается, что отдельно взятая функция (например, обработчик события) работает достаточно долго, а вызывается часто, что сильно ухудшает отзывчивость интерфейса.
Предложите общее решение, позволяющее вызывать любую функцию не чаще N раз в секунду, даже если её вызов происходит чаще.

**Вопрос 3**
> Напишите функцию, которая из произвольного входящего массива выберет все комбинации чисел, сумма которых будет равняться 10.

**Вопрос 4**
> Приведите примеры вашего кода. Это могут быть:ссылка на открытый репозиторий, например GitHub; ссылка на сам проект (укажите, какую его часть вы написали); несколько файлов с кодом (укажите, частью какого проекта он является)

В качестве примера приведу два своих проекта из песочницы где я игрался с JS, а в частности с AngularJS
* [toDoList](https://github.com/Nigorro/ToDoList ) Простой ToDoList. Реализованая возможность добавлять, редактировать, удалять записи. Так же для каждой записи в листе можно выставить рейтинг, путем нажатия на звездочку ( от 1 до 5 ). Все данные в листе первончально хранились в Cookes, но потом в качестве эксперимент подключил [http://deployd.com/](http://deployd.com/), было интерестно поиграться в данной штукой. При разработке использовалось: Yeoman, Grunt.js, Angular.js, Bootstrap. 
* [showCases](https://github.com/Nigorro/showcases). Витрина в выполнеными проектами компании, реализована для  быстрого поиска необходимой информации по прошедшим проектам. Так же как и  в [toDoList](https://github.com/Nigorro/ToDoList ) для хранения данных выбран [http://deployd.com/](http://deployd.com/), по причиние простоты и быстроты написание простенького  хранилища  данных. Все проекты представленные на странице, были сверстаны мною.
*[Avantum.ru](http://avantum.ru/) Сверстанный мною сайт компании.
* Обработчик форм запроса вывода средств
``` js
$(function() {
			$('.head .radio').click(function(){
			    if($("#content .spoiler-body:hidden").length>0){
					$(".spoiler-body:not(:hidden)").slideUp(600);}
					var t = $( "input:checked" ).data('target')	
					$('#'+t).slideToggle(600);
			});

			$('.yamoney').click(function(){
				$('.yamoney').prop('checked', true);
				$('.yamoney-form').slideToggle(600)
				$('.bank-form').slideUp(600)

			});
			$('.bank').click(function(){
				$('.bank').prop('checked', true);
				$('.yamoney-form').slideUp(600)
				$('.bank-form').slideToggle(600)
			});

			$('.numbers').bind("change keyup input click", function() {
			    if (this.value.match(/[^0-9]/g)) {
			        this.value = this.value.replace(/[^0-9]/g, '');
			    }
			});
			$("#parnterMoney #money").change(function(){ 
			   	if( parseInt($(this).val()) > parseInt($('#profit').text())){
			   		$(this).val($('#profit').text())
			   	}
			});
			$("#moneyСourse #money").change(function(){ 
			   	if( parseInt($(this).val()) > parseInt($('#all_profit').text())){
			   		$(this).val($('#all_profit').text())
			   	}
			});
			function getCookie(name) {
			    var cookieValue = null;
			    if (document.cookie && document.cookie != '') {
			        var cookies = document.cookie.split(';');
			        for (var i = 0; i < cookies.length; i++) {
			            var cookie = jQuery.trim(cookies[i]);
			            if (cookie.substring(0, name.length + 1) == (name + '=')) {
			                cookieValue = decodeURIComponent(cookie.substring(name.length + 1));
			                break;
			            }
			        }
			    }
			    return cookieValue;
			};
			var csrftoken = getCookie('csrftoken');
			$( "input[name='csrfmiddlewaretoken']" ).val(csrftoken);
			if($('.nav-header').text().length>0){
				$('.userLogin').val($('.nav-header').text())
			};

			$('.btn_submit').click(function(event){
				var emailReg = /^([\w-\.]+@([\w-]+\.)+[\w-]{2,4})?$/;
				var email = $(this).parent().parent().parent().find('#inputEmail').val()

				if( !emailReg.test(email) ) {
					event.preventDefault();
					$(this).parent().parent().parent().find('#inputEmail').popover('show')
				}
				var additional_field = '.rfield,.' + $(this).parent().parent().parent().find('input:checked').data('type');
				$(this).parent().parent().parent().find(additional_field).each(function(){
					if($(this).val() == ''){
						event.preventDefault();
						$(this).addClass('empty_field')
					}else{
						$(this).removeClass('empty_field');
					}
				});
			})

			$('#agree').change(function(){
				if($(this).prop('checked')==true){
					$('#agree_btn').removeAttr("disabled")
				}
				else($('#agree_btn').attr("disabled", "disabled"))
			})
         });
```

``` js
<% if @id == '0': %>
	<script type="text/javascript" id='jscript'>
		$(function() { 
				$('#bgimage').css('background', '<%= @url %>   no-repeat fixed');
				$('#bgimage').css('background-position', '50%');
				$('#bgimage').css('background-size', '100%');

				$('.layout').css( '-webkit-box-shadow', '<%= @sh_opacity %>');
                $('.layout').css( '-moz-box-shadow', '<%= @sh_opacity %>');
                $('.layout').css( 'box-shadow', '<%= @sh_opacity %>');
                $('.layout').css( 'background-color', '<%= @l_opacity %>');               
		 });
	</script>
<% else if @id == '1': %>
 	<script type="text/javascript" id='jscript'>
		$(function() {
				$('#bgimage').css('background', '<%= @url %> ');
				$('.layout').css( '-webkit-box-shadow', '<%= @sh_opacity %>');
                $('.layout').css( '-moz-box-shadow', '<%= @sh_opacity %>');
                $('.layout').css( 'box-shadow', '<%= @sh_opacity %>');
                $('.layout').css( 'background-color', '<%= @l_opacity %>');
		 });
	</script>
<% else if @id >= '2': %>
 	<script type="text/javascript" id='jscript'>
		$(function() {
				$('#bgimage').css('background', 'url(/static/img/onepage/background/<%= @id %>.png )');
				$('.layout').css( '-webkit-box-shadow', '<%= @sh_opacity %>');
                $('.layout').css( '-moz-box-shadow', '<%= @sh_opacity %>');
                $('.layout').css( 'box-shadow', '<%= @sh_opacity %>');
                $('.layout').css( 'background-color', '<%= @l_opacity %>'); 
		 });
	</script>
<% end %>

```

``` js 
$(function() {
                $('.imgbox img').css('border','solid 2px #fff');   
                $('.controls').css('margin-left','0');
                $('.imgbox').css('height', '65px');
                $('.imgbox').css('padding-bottom', '15px');
                $('#layout_opacity').change( function() {
                   
                    var op ='rgba(255, 255, 255,' + this.value/100 +')';
                    $('#layout').css( 'background-color', op);
                    $('#value').text(this.value+'%');
                });

                $('#shadow_opacity').change( function() {
                    var op ='0px 4px 5px rgba(0, 0, 0,' + this.value/100 +')';
                    $('#layout').css( '-webkit-box-shadow', op);
                    $('#layout').css( '-moz-box-shadow', op);
                    $('#layout').css( 'box-shadow', op);
                    $('#value_shadow').text(this.value+'%');
                });
                $('#bgimage').change(function(){
                    $('.imgbox img').css('border','solid 2px #fff');
                    var url = 'url(' + $('#bgimage').val() + ')';
                    if ($('#bgimage').val()[0] == '#'){
                        $(box).css('backgroundImage', 'none');
                        $(box).css('background-color', $('#bgimage').val());
                    }
                    else {
                        $(box).css('backgroundImage', url);
                    };
                });
                $('.imgbox img').on("click", function(){
                        $('.imgbox img').css('border','solid 2px #fff');    
                        $(this).css('border','solid 2px #00A75D');
                        var id = $(this).attr("id");
                        var url = '/static/img/onepage/background/' + id + '.png';
                        $('#bgimage').val(url);
                        $("input:radio[value='1']").attr('checked', true);
                        $(box).css('backgroundImage', 'url(/static/img/onepage/background/' + id + '.png)');
                });               
         });
```
