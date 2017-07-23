# MJSArrayStrategies

## 小可作为纯正iOS开发出身，内心也曾暗下决心，非iOS不做，现实是老板一声令下，移动组全线转战移动棋牌手游，淫威之下，小子屈服了。小组决定使用cocos 引擎，JavaScript开发，这意味着小组必须以最快的速度，转到JavaScript开发上面来，小子只能说“过程是非常有压力和艰苦的”，好在，产品最终顺利上架，大家可在AppStore搜索【VS竞技跑得快】、【VS竞技跑胡子】。现在得空，整理下关于JS的基础知识，留作记录。

“c、oc、swift、java、JS等...只是工具！”。

# JavaScript数组使用大全
### 一、数组的方法，数组的方法有数组原型方法，也有从object对象继承来的方法，这里我们只介绍数组的原型方法，数组原型方法主要有以下这些：
		1.join()
		2.push()和pop()
		3.shift() 和 unshift()
		4.sort()
		5.reverse()
		6.concat()
		7.slice()
		8.splice()
		9.indexOf()和 lastIndexOf()	ES5新增
		10.forEach()			ES5新增
		11.map()			 ES5新增
		12.filter()			ES5新增
		13.every()			ES5新增
		14.some()			ES5新增
		15.reduce()和 reduceRight()	ES5新增

### 二、针对ES5新增的方法浏览器支持情况：
	1.Opera 11+ 
	2.Firefox 3.6+ 
	3.Safari 5+ 
	4.Chrome 8+ 
	5.Internet Explorer 9+

对于支持的浏览器版本，可以通过Array原型扩展来实现。下面详细介绍一下各个方法的基本功能。


## 1、join()
标准：join(separator)。

参数：separator（接收一个参数，即分隔符）

返回：字符串。

解释：将数组以separator为分隔符，组成一个字符串；separator省略则默认逗号为分隔符。

sample code:
	
	var arr = [1,2,3];
	
	console.log(arr.join()); // 1,2,3
	
	console.log(arr.join("-")); // 1-2-3
	
	console.log(arr); // [1, 2, 3]（原数组不变）
	
应用场景：

	通过join()方法可以实现重复字符串，只需传入字符串以及重复的次数，就能返回重复后的字符串，函数如下：
			
	function repeatString(str, n) {
	return new Array(n + 1).join(str);
	}
	console.log(repeatString("abc", 3)); // abcabcabc
	console.log(repeatString("Hi", 5)); // HiHiHiHiHi
## 2、push()和pop()
标准：

push(): 将任意数量的参数逐个添加到数组末尾，并返回修改后数组的长度；

pop()：数组末尾移除最后一项，减少数组的 length 值，然后返回移除的项。

参数：任意数量的参数。

返回：数组。

解释：

sample code:
	
	var arr = ["Lily","lucy","Tom"];
	
	var count = arr.push("Jack","Sean");
	
	console.log(count); // 5
	
	console.log(arr); // ["Lily", "lucy", "Tom", "Jack", "Sean"]
	
	var item = arr.pop();
	
	console.log(item); // Sean
	
	console.log(arr); // ["Lily", "lucy", "Tom", "Jack"]


## 3、shift() 和 unshift()


标准：

shift()：删除原数组第一项，并返回删除元素的值；如果数组为空则返回undefined 。 

unshift:将参数添加到原数组开头，并返回数组的长度 。

参数：

返回：

解释：这组方法和上面的push()和pop()方法正好对应，一个是操作数组的开头，一个是操作数组的结尾。

	var arr = ["Lily","lucy","Tom"];
	
	var count = arr.unshift("Jack","Sean");
	
	console.log(count); // 5
	
	console.log(arr); //["Jack", "Sean", "Lily", "lucy", "Tom"]
	
	var item = arr.shift();
	
	console.log(item); // Jack
	
	console.log(arr); // ["Sean", "Lily", "lucy", "Tom"]
	
## 4、sort()
标准：

sort()：按升序排列数组项——即最小的值位于最前面，最大的值排在最后面。

参数：

返回：

解释：在排序时，sort()方法会调用每个数组项的 toString()转型方法，然后比较得到的字符串，以确定如何排序。即使数组中的每一项都是数值， sort()方法比较的也是字符串，因此会出现以下的这种情况：


	var arr1 = ["a", "d", "c", "b"];
	
	console.log(arr1.sort()); // ["a", "b", "c", "d"]
	
	arr2 = [13, 24, 51, 3];
	
	console.log(arr2.sort()); // [13, 24, 3, 51]
	
	console.log(arr2); // [13, 24, 3, 51](元数组被改变)
	
为了解决上述问题，sort()方法可以接收一个比较函数作为参数，以便我们指定哪个值位于哪个值的前面。比较函数接收两个参数，如果第一个参数应该位于第二个之前则返回一个负数，如果两个参数相等则返回 0，如果第一个参数应该位于第二个之后则返回一个正数。以下就是一个简单的比较函数：

	function compare(value1, value2) {
	
	if (value1 < value2) {
	
	return -1;
	
	} else if (value1 > value2) {
	
	return 1;
	
	} else {
	
	return 0;
	
	}
	
	}
	arr2 = [13, 24, 51, 3];
	
	console.log(arr2.sort(compare)); // [3, 13, 24, 51]
	
如果需要通过比较函数产生降序排序的结果，只要交换比较函数返回的值即可：

	function compare(value1, value2) {
	
	if (value1 < value2) {
	
	return 1;
	
	} else if (value1 > value2) {
	
	return -1;
	
	} else {
	
	return 0;
	
	}
	
	}
	
	arr2 = [13, 24, 51, 3];
	
	console.log(arr2.sort(compare)); // [51, 24, 13, 3]
	
## 5、reverse()

标准：

reverse()：反转数组项的顺序。

参数：

返回：

解释：

	var arr = [13, 24, 51, 3];
	console.log(arr.reverse()); //[3, 51, 24, 13]
	console.log(arr); //[3, 51, 24, 13](原数组改变)
	
## 6、concat()
标准：

concat() ：将参数添加到原数组中。这个方法会先创建当前数组一个副本，然后将接收到的参数添加到这个副本的末尾，最后返回新构建的数组。在没有给 concat()方法传递参数的情况下，它只是复制当前数组并返回副本。

参数：

返回：

解释：

	var arr = [1,3,5,7];
	
	var arrCopy = arr.concat(9,[11,13]);
	
	console.log(arrCopy); //[1, 3, 5, 7, 9, 11, 13]
	
	console.log(arr); // [1, 3, 5, 7](原数组未被修改)
	
从上面测试结果可以发现：传入的不是数组，则直接把参数添加到数组后面，如果传入的是数组，则将数组中的各个项添加到数组中。但是如果传入的是一个二维数组呢？

	var arrCopy2 = arr.concat([9,[11,13]]);
	
	console.log(arrCopy2); //[1, 3, 5, 7, 9, Array[2]]
	
	console.log(arrCopy2[5]); //[11, 13]
	
上述代码中，arrCopy2数组的第五项是一个包含两项的数组，也就是说concat方法只能将传入数组中的每一项添加到数组中，如果传入数组中有些项是数组，那么也会把这一数组项当作一项添加到arrCopy2中。

## 7、slice()

标准：

slice()：返回从原数组中指定开始下标到结束下标之间的项组成的新数组。slice()方法可以接受一或两个参数，即要返回项的起始和结束位置。在只有一个参数的情况下， slice()方法返回从该参数指定位置开始到当前数组末尾的所有项。如果有两个参数，该方法返回起始和结束位置之间的项——但不包括结束位置的项。

参数：

返回：

解释：

	var arr = [1,3,5,7,9,11];
	
	var arrCopy = arr.slice(1);
	
	var arrCopy2 = arr.slice(1,4);
	
	var arrCopy3 = arr.slice(1,-2);
	
	var arrCopy4 = arr.slice(-4,-1);
	
	console.log(arr); //[1, 3, 5, 7, 9, 11](原数组没变)
	
	console.log(arrCopy); //[3, 5, 7, 9, 11]
	
	console.log(arrCopy2); //[3, 5, 7]
	
	console.log(arrCopy3); //[3, 5, 7]
	
	console.log(arrCopy4); //[5, 7, 9]
	
arrCopy只设置了一个参数，也就是起始下标为1，所以返回的数组为下标1（包括下标1）开始到数组最后。 
arrCopy2设置了两个参数，返回起始下标（包括1）开始到终止下标（不包括4）的子数组。 
arrCopy3设置了两个参数，终止下标为负数，当出现负数时，将负数加上数组长度的值（6）来替换该位置的数，因此就是从1开始到4（不包括）的子数组。 
arrCopy4中两个参数都是负数，所以都加上数组长度6转换成正数，因此相当于slice(2,5)。

## 8、splice()
标准：

参数：

返回：

解释：
splice()：很强大的数组方法，它有很多种用法，可以实现删除、插入和替换。
删除：可以删除任意数量的项，只需指定 2 个参数：要删除的第一项的位置和要删除的项数。例如， splice(0,2)会删除数组中的前两项。
插入：可以向指定位置插入任意数量的项，只需提供 3 个参数：起始位置、 0（要删除的项数）和要插入的项。例如，splice(2,0,4,6)会从当前数组的位置 2 开始插入4和6。
替换：可以向指定位置插入任意数量的项，且同时删除任意数量的项，只需指定 3 个参数：起始位置、要删除的项数和要插入的任意数量的项。插入的项数不必与删除的项数相等。例如，splice (2,1,4,6)会删除当前数组位置 2 的项，然后再从位置 2 开始插入4和6。
splice()方法始终都会返回一个数组，该数组中包含从原始数组中删除的项，如果没有删除任何项，则返回一个空数组。

	var arr = [1,3,5,7,9,11];
	
	var arrRemoved = arr.splice(0,2);
	
	console.log(arr); //[5, 7, 9, 11]
	
	console.log(arrRemoved); //[1, 3]
	
	var arrRemoved2 = arr.splice(2,0,4,6);
	
	console.log(arr); // [5, 7, 4, 6, 9, 11]
	
	console.log(arrRemoved2); // []
	
	var arrRemoved3 = arr.splice(1,1,2,4);
	
	console.log(arr); // [5, 2, 4, 4, 6, 9, 11]
	
	console.log(arrRemoved3); //[7]

## 9、indexOf()和 lastIndexOf()
标准：

参数：

返回：

解释：
indexOf()：接收两个参数：要查找的项和（可选的）表示查找起点位置的索引。其中， 从数组的开头（位置 0）开始向后查找。 
lastIndexOf：接收两个参数：要查找的项和（可选的）表示查找起点位置的索引。其中， 从数组的末尾开始向前查找。
这两个方法都返回要查找的项在数组中的位置，或者在没找到的情况下返回1。在比较第一个参数与数组中的每一项时，会使用全等操作符。

	var arr = [1,3,5,7,7,5,3,1];
	
	console.log(arr.indexOf(5)); //2
	
	console.log(arr.lastIndexOf(5)); //5
	
	console.log(arr.indexOf(5,2)); //2
	
	console.log(arr.lastIndexOf(5,4)); //2
	
	console.log(arr.indexOf("5")); //-1
	
## 10、forEach()
标准：

参数：

返回：

解释：
forEach()：对数组进行遍历循环，对数组中的每一项运行给定函数。这个方法没有返回值。参数都是function类型，默认有传参，参数分别为：遍历的数组内容；第对应的数组索引，数组本身。

	var arr = [1, 2, 3, 4, 5];
	
	arr.forEach(function(x, index, a){
	
	console.log(x + '|' + index + '|' + (a === arr));
	
	});
	
	// 输出为：
	
	// 1|0|true
	// 2|1|true
	// 3|2|true
	// 4|3|true
	// 5|4|true
	
## 11、map()
标准：

参数：

返回：

解释：
map()：指“映射”，对数组中的每一项运行给定函数，返回每次函数调用的结果组成的数组。
下面代码利用map方法实现数组中每个数求平方。

	var arr = [1, 2, 3, 4, 5];
	
	var arr2 = arr.map(function(item){
	
	return item*item;
	
	});
	
	console.log(arr2); //[1, 4, 9, 16, 25]
	
## 12、filter()
标准：

参数：

返回：

解释：
filter()：“过滤”功能，数组中的每一项运行给定函数，返回满足过滤条件组成的数组。

	var arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
	
	var arr2 = arr.filter(function(x, index) {
	
	return index % 3 === 0 || x >= 8;
	
	}); 
	
	console.log(arr2); //[1, 4, 7, 8, 9, 10]
	
## 13、every()
标准：

参数：

返回：

解释：
every()：判断数组中每一项都是否满足条件，只有所有项都满足条件，才会返回true。

	var arr = [1, 2, 3, 4, 5];
	
	var arr2 = arr.every(function(x) {
	
	return x < 10;
	
	}); 

	console.log(arr2); //true
	
	var arr3 = arr.every(function(x) {
	
	return x < 3;
	
	}); 
	
	console.log(arr3); // false
	
## 14、some()
标准：

参数：

返回：

解释：
some()：判断数组中是否存在满足条件的项，只要有一项满足条件，就会返回true。

	var arr = [1, 2, 3, 4, 5];
	
	var arr2 = arr.some(function(x) {
	
	return x < 3;
	
	}); 
	
	console.log(arr2); //true
	
	var arr3 = arr.some(function(x) {
	
	return x < 1;
	
	}); 
	
	console.log(arr3); // false
	
## 15、reduce()和 reduceRight()
标准：

参数：

返回：

解释：
这两个方法都会实现迭代数组的所有项，然后构建一个最终返回的值。reduce()方法从数组的第一项开始，逐个遍历到最后。而 reduceRight()则从数组的最后一项开始，向前遍历到第一项。
这两个方法都接收两个参数：一个在每一项上调用的函数和（可选的）作为归并基础的初始值。
传给 reduce()和 reduceRight()的函数接收 4 个参数：前一个值、当前值、项的索引和数组对象。这个函数返回的任何值都会作为第一个参数自动传给下一项。第一次迭代发生在数组的第二项上，因此第一个参数是数组的第一项，第二个参数就是数组的第二项。
下面代码用reduce()实现数组求和，数组一开始加了一个初始值10。

	var values = [1,2,3,4,5];
	
	var sum = values.reduceRight(function(prev, cur, 
	index, array){
	
	return prev + cur;
	
	},10);
	
	console.log(sum); //25

