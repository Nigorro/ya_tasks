**Поиск сочетаний, сумма которых равна 10**
=============
Алгоритм решения задачи, прост. На входе функция получает входной массив с числами и искомое число.
Обходим массив, если текущий элемент массива больше или равшен нужной сумме выходим из итериций, если равен то заносим 
во временный массив. Далее при помощи рекурсии начинается поиск комбинаций исключая текучщее значение.


``` js

function findNumbers(array, target){
	var result = [],
	arrLen = array.length,
	i = 0,
	item;
	for (i = 0; i < arrLen; i++) {
		item = array[i];
		if (item > target) continue;
		if(item == target) {
			result.push([item]);
			continue;
		}
		var temp = findNumbers(array.slice(i+1), target - item);
		if(!temp.length) continue;
		for (var j = 0, len = temp.length; j < len; j++) {
			result.push([item].concat(temp[j]));
		};
	};
	return result;
};

console.log( findNumbers([ 3,4,5,1,9,23,10,2], 10) );

/*Out 
[3,4,1,2],[3,5,2],[5,5,1],[1,9],[10] 
*/ 
```
