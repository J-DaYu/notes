# Javascript 位运算

> 位运算符可以直接操作二进制上的`位`
>
> JavaScript 将数字转化为二进制
>
> ```javascript
> let num = 2;
> num.toString(2); // 10
> ```



## & 与

> 比较二进制 每个 `位` 上的 1或0, 如果都为1 则保留给结果, 否则保留0给结果

```javascript
let a = 2; // 10
let b = 3; // 11
a & b // 2 => 10
```

二进制 `位` 关系

| 变量 | 值   | 二进制 |
| ---- | ---- | ------ |
| a    | 2    | 10     |
| b    | 3    | 11     |
| 结果 | 2    | 10     |



## | 或

> 比较二进制每个`位` 上的1或0, 如果有一个为1就保留给结果, 否则保留0给结果

```javascript
let a = 2; // 10
let b = 3; // 11
a | b // 3 => 11
```

二进制 `位` 关系

| 变量 | 值   | 二进制 |
| ---- | ---- | ------ |
| a    | 2    | 10     |
| b    | 3    | 11     |
| 结果 | 3    | 11     |



## << 左移

> 当前二进制 `位` 向左移

```javascript
let a = 10;			// 1010
// 二进制 1010 向左移动两位 得到101000
let b = a << 2;	// 20 => 101000
```

二进制 `位` 关系

| 变量 | 值   | 二进制 |
| ---- | ---- | ------ |
| a    | 10   | 1010   |
| b    | 20   | 101000 |



## >> 右移

> 当前二进制 `位` 向右移

```javascript
let a = 10;		// 1010
// 二进制 1010 向右移动一位 得到 101
let b = a >> 1; // 5 => 101
```

二进制`位`关系

| 变量 | 值   | 二进制 |
| ---- | ---- | ------ |
| a    | 10   | 1010   |
| b    | 5    | 101    |



## ~ Not

>  位运算 NOT 是三步的处理过程:
>
> 1. 把运算数转换成 32 位数字
> 2. 把二进制数转换成它的二进制反码
> 3. 把二进制数转换成浮点数
>
> 实际上 ~ 是对数字求负然后减1

```javascript
let a = 10; // 	10 => 00000000000000000000000000001010
let b = ~a; // -11 => 11111111111111111111111111111011
```

等同于

```javascript
let a = 10;
let b = -a-1; // -11
```

二进制 `位` 关系

| 变量 | 值   | 二进制                           |
| ---- | ---- | -------------------------------- |
| a    | 10   | 00000000000000000000000000001010 |
| b    | -11  | 11111111111111111111111111111011 |



## 奇技淫巧

###  & 奇偶数判断

> 偶数的二进制最后一位永远 0 , 奇数的二进制最后一位永远为1
>
> 1的二进制 是 01
>
> 所有 偶数 & 1 时得到 0
>
> 所有 奇数 & 1 时得到 1

```javascript
let a = 2; // 010
let b = 3; // 011
let c = 4; // 100
// 1 => 			001
a & 1 // 0
b & 1 // 1
c & 1 // 0
```



### << 获得乘以 2 的n次方的结果

> << 移动的位数 表示2 的(n)次方

```javascript
let a = 3;
a << 1; // 3 * (2) = 6
a << 2; // 3 * (2 * 2) = 12
a << 3; // 3 * (2 * 2 * 2) = 24
```

