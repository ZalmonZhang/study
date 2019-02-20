## String字符串
### 1.语法:
`var str1 = "";`  
`var str2 = new String("hello");`  

**如:**
```js
var s1="hello";
var s2=new String("hello world");

console.log(s1,s1.length);
console.log(s2,s2.length);

for (var i = 0;i<s2.length;i++){
	
}
```

### 2.属性和方法
#### 1.属性:
`length`: 获取字符串长度(字符个数)  
遍历字符串:  
   由于字符串也是类数组结构,每个字符都会分配下标,可以按照数组访问元素的方法访问字符
```js
var str="hello";
for (var i = 0;i<s2.length;i++){
	console.log(str[i]);
	}
```
#### 2.常用方法
##### 1. 转换大小写(英文字母)
1. `toUpperCase()`  
   `str.toUpperCase.()`  
   转换为大写字母,返回新的字符串  
2. `toLowerCase()`  
   `str.toLowerCase()`  
   转换为小写字母,返回新的字符串
   
**练习**
>模拟验证码操作:  
>1. 创建数组,由数字,字母组成  
>2. 生成随机验证码  
>3. 提示用户输入验证码  
>4. 验证用户输入正确与否,返回提示信息k  
>>随机数: `Math.random()[0~1)`  
>>随机下标:  
>>1. `[0,length)`  
>>2. 取整  

```js
<script type="text/javascript">
		function createCode(){
			var str1="abcdefghijklmnopqrstuvwxyz0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ";
		var yy=""
		var a1=parseInt(Math.random()*62);
		var a2=parseInt(Math.random()*62);
		var a3=parseInt(Math.random()*62);
		var a4=parseInt(Math.random()*62);
		yy+=str1[a1]+str1[a2]+str1[a3]+str1[a4];
		console.log(yy);
		return yy;
		}
		function textCheck(){
			var code = createCode();
			var ipt = prompt("请输入右侧的验证码:"+code);
			if (ipt.toUpperCase()==code.toUpperCase()){
				alert("验证通过");
			}else{
				alert("输入错误");
			}
		}
	</script>
	<button onclick="textCheck()">点我验证</button>
```

##### 2. 获取指定字符
1. `charCodeAt(index)`: 获取指定位置字符的`Unicode`码,参数省略表时获取第一个字符  
2. ` charAt(index)`: 获取指定位置下标的字符  

##### 3.检索字符串
获取指定字符的下标  
1. `indexOf(value[])`  

##### 4. 截取字符串
`subtring(startIndex,endIndex)`  
根据指定的开始下标截取,截取至endindex  
参数:`endIndex`可以省略,省略结束下标,表示截至末尾  
返回:`[startIndex,endIdex)`之间的字符串  

**练习;**
>1. 截取邮箱中的用户名和服务商  
>   zhangsan3546@163.com  
>2. 提取身份证信息(年月日)  
>   100112197802151234  
>  



##### 5.分割字符串
`split(seperator;)`  
方法: 根据执行的符号(字符串中存在的)将字符串分割层若干小字符串  
参数: 指定字符  
返回值: 数组,数组中存放若干子字符串  
**如:**
```js
var s1 ="2018-11-11";
var res= s1.split('-');
console.log(res);
```

**练习:**
>分割URL  
>101_5&102_10&221_3  
>
```js
var ss="101_5&102_10&221_3";
var s1=ss.split('&');
console.log(s1);
for(i=0;i<s1.length;i++){
	x=s1[i].split('_');
	xx="商品id:"+x[0]+"  商品数量:"+x[1];
	console.log(xx);
}
```

##### 6. 模式匹配
1. 结合正则表达式实现查找字符串中的指定字符  
2. 正则表达式  
   `var reg1=/正则表达式/;`  
      `var reg2=/hello/;`  
   模式修饰符:  
   `i : ignore case` 忽略大小写  
   `g: global` 全局匹配  
   **如 :**
   `var reg3=/你好/ig;`  
3. 方法:
   1. `match(substr|RegExp);`  
   根据指定的字符串或正则模式,查找字符串内容,返回数组,保存匹配结果  
   
```js
//1.根据正则模式或指定字符串匹配内容
var s1="你好,小白,你好,小黑";
var arr=s1.match("你好");
var arr2=s1.match(/你好/g);
console.log(arr);
console.log(arr2);

```
   2. `replace(sunstr|RegExp,newString);`  
   根据正则模式查找内容,并且使用newString替换  

**练习:**
>Microsoft is a big company,microsoft is a big company,MicroSoft is a big company.  
>将所有的Microsoft替换为中文"微软"  
>并输出替换了多少次  
>
```js
var s1="Microsoft is a big company,microsoft is a big company,MicroSoft is a big company.";
var nn=s1.replace(/microsoft/ig,"微软");
var s2=s1.match(/microsoft/ig)
console.log(nn,"共替换了",s2.length,"次")
```

----

## 2.正则表达式
### 1.正则表达式 `Regular Expression`  
   设置模式,匹配或验证字符串格式  
### 2.创建正则
1. `var reg1=/^\d{6}/ig;`  
2. `var reg2=new RegExp("模式","修饰符");`  
   注意: 元字符中的转义`\`,在字符串表示时需要多加一个`\`  
   `var reg3=new RegExp('\\d{6}','i');`  

如:
```js
//1. 创建正则表达式
var reg1=/microsoft/ig;
var reg2=/\d{6}/g;
var reg3=new RegExp("\\d{6}","ig");
```

### 3. 属性与方法
1. 属性: `lastIndex`  
指定下一次匹配的起始索引,只有在设置了全局匹配才起作用  
原则上,同一个正则表达式,不要重复验证,`lastIndex`每次起始索引不同,影响验证结果  
但是,可以手动修改`lastIndex`为0,保证每次都从0位置查找字符  
2. 方法:  
`test(param)`  
参数为要验证的字符串  
返回值:true/false 表示字符串中是否包含满足正则模式的内容  

----
## 3. Math 数学对象
提供一系列数学方法  
### 1. 属性
#### 数学常量:  
`Math.PI` : 圆周率/180deg  
`Math.E`  : 自然对数  
### 2. 方法
1. 三角函数  
   `Math.sin(deg)`  
   `Math.cos(deg)`  
   `Math.tan(deg)`  
   注意:  
   参数为度数,可以使用`Math.PI(180deg)`进行转换  
   涉及小数,可能存在误差  
2. 计算函数  
   `Math.sqrt(x);`	对x开平方  
   `Math.pow(x,y);` 求x的y次方  
   `Math.log(x);`		求对数  
3. 数值函数(较常用)  
   `Math.abs(x);`		求x的绝对值  
   `Math.max(list);`	求一组数据的最大值  
   `Math.min(list);`	求一组数据的最小值  
   `Math.random()`  获取`[0,1)`之间的随机数  
   `Math,ceil(x)`	 对x向上取整  
   `Math.floor(x)`	对x向下取整,舍弃小数部分  
   `Math.round(x)`  对x四舍五入取整  
   
   -----
### 4.Date 日期对象
#### 1. 提供获取客户端时间与日期的方法
#### 2. 创建日期对象
`var date1=new Date();` 获取当前系统时间  
`var date2=new Date("2018-11-11 10:11:12")` 根据指定的日期时间创建对象  
#### 3. 方法
1. 设置或获取当前是间的毫秒数(了解)
   1. `getTime();  
   获取当前日期对象距离`1970-01-01 00:00:00`之间的毫秒数  
   2. `setTime(毫秒数);`  
   根据指定的毫秒数结合`1970-01-01 00:00:00`计算日期  
2. 获取时间分量(重点)  
   1. `getFullYear();`  
   获取当前日期对象中的年份信息  
   四位年份数字  
   2. `getMonth();`  
   获取日期对象中的月份信息  
   返回值 0-11 对应12个月,需要+1显示  
   3. `getDate();`  
   获取日期对象中的日子信息  
   返回值 正常号数  
   4. `getDay();`  
   获取日期对象中的星期信息  
   返回值0-6 对应周日-周六  
   5. 获取时间  
   `getHours();` 获取小时数  
   `getMinutes();`获取分钟数  
   `getSeconds();`获取秒数  
   `getMilliseconds();`获取毫秒数  
   6. 将日期对象转换为指定的字符串  
      1. `toString();`  
	  2. `toLocaleString(); `  
	以本地日期格式输出  
	2018/11/20 下午5:21:43  
	   3. `toLocaleDateString();`  
       4. `toLocaleTimeString();`  

练习:  
>获取系统日期时间  
>按照以下格式输出显示:  
>xxxx年xx月xx日 xx时xx分xx秒 星期x  
