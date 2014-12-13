**Функция, ограниченная по времени**
============
Решение с использованием произвольной зарежки.
``` js 


function  funcByFrequencyCalls(func , delay, count){
	if ( !(func && func.constructor && func.call && func.apply)) {
		alert(func+' is not a function! =(');
	};

	var totalCalls = count || 3
	delayTime = delay || 1000
	timeOut = null
	callsCounter = 0
	isFuncCall = true;

	return function(){
		if (isFuncCall){
			if(callsCounter<totalCalls){
				callsCounter+=1;
				func();
			} else {
				isFuncCall = false;
				callsCounter = 0;
				timeOut = setTimeout( function(){
					isFuncCall = true;
				}, delayTime);
			}
		}
	}
}


function consoleLog(){
	consoleLog('foo poo');
}
var test = funcByFrequencyCalls(consoleLog, 10000, 4);

test();
```


