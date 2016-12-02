
# manba
<img src="http://manba.ch-un.com/images/logo.png" alt="manba" width="100"><br/>
超级简洁的日期处理Util，比moment.js小很多。  
![manba](https://img.shields.io/badge/manba-1.1.15-red.svg)

## 官方网站

[http://manba.ch-un.com](http://manba.ch-un.com)

## 安装
```
npm install manba
```
建议本地安装
```
npm install --save manba
```

## NPM

[https://www.npmjs.com/package/manba](https://www.npmjs.com/package/manba)

## 文档
### 初始化数据

初始化的时候，对月份做了修补。

`manba(String|Number|Date|Array)`

```javascript
manba(1459235037).format() //秒 2016-03-29
manba(1459235037000).format() //毫秒 2016-03-29
manba([2016,12,23,4,3,5]).format("f") 
//月份自动补充，执行：new Date(2016,11,23,4,3,5) 2016-12-23 04:03:05
manba([2015,12,3]).format("f") 
//执行：new Date(2015,11,3) 2015-12-03
manba("2014-12-03").format("f") //2014-12-03 00:00:00
manba("2014-12-03 12:34").format("f") //2014-12-03 12:34:00
manba("2014-12-03 12:34:12").format("f") //2014-12-03 12:34:34
manba("20141203").format("f") //2014-12-03 00:00:00
manba("201412031223").format("f") //2014-12-03 12:23:00
```

### format
格式化日期转换标准
- YYYY/yyyy:年份
- M:月份
- MM:月份，个位补充0
- D/d:天数
- DD/dd:天数，个位补充0
- H/h:小时
- HH/hh:小时，个位补充0
- m:分钟
- mm:分钟，个位补充0
- S/s:秒数
- SS/ss:秒数，个位补充0
- w:星期，返回中文：['日', '一', '二', '三', '四', '五', '六']
- q:上下午，返回中文：['上午', '下午']

#### 内置简洁的格式化
- "l": "YYYY-MM-DD",
- "ll": "YYYY年MM月DD日",
- "k": "YYYY-MM-DD hh:mm",
- "kk": "YYYY年MM月DD日 hh点mm分",
- "kkk": "YYYY年MM月DD日 hh点mm分 q",
- "f": "YYYY-MM-DD hh:mm:ss",
- "ff": "YYYY年MM月DD日 hh点mm分ss秒",
- "fff": "YYYY年MM月DD日 hh点mm分ss秒 星期w",
- "n": "MM-DD",
- "nn": "MM月DD日",

```javascript
//各种format
manba() // Tue Mar 29 2016 16:52:56 GMT+0800 (CST)
manba().toString() // Tue Mar 29 2016 16:52:56 GMT+0800 (CST)
manba().format() // 2016-03-29
manba().format("l") // 2016-03-29
manba().format("ll") // 2016年03月29日
manba().format("k") // 2016-03-29 16:52
manba().format("kk") // 2016年03月29日 16点52分
manba().format("kkk") // 2016年03月29日 16点52分 下午
manba().format("f") // 2016-03-29 16:52:56
manba().format("ff") // 2016年03月29日 16点52分56秒
manba().format("fff") // 2016年03月29日 16点52分56秒 星期二
manba().format("n") // 03-29
manba().format("nn") // 03月29日
manba().format("YYYY") // 2016
```
#### 定制简洁格式

```javascript
manba.config({
    formatString: {
        "r": "YYYY"
    },
    now:"2016-07-11T18:42:34.453+08:00"
}

//now参数可以设置前端与后端的时间差，这样前端也可以使用manba()获取当前时间。

manba().format("r") // 2016

```

### 获取数值函数
`month()`方法，对月份做了修补。

```javascript
manba().year() //2016
manba().year(2018).format() //2018-03-29
manba().month() //2016-03-29
manba().month(4).format() //2016-04-29
manba().minutes() //59
manba().minutes(34)
manba().time() //1459242450800
manba().time(123131312321).format() //1973-11-26
manba().date() //29
manba().date(4).format() //2016-03-04
manba().isLeapYear() //是否为闰年 true
manba().toString()
manba().toISOString() //返回带时区的格式，2016-12-02T20:58:02+08:00
```
### distance

`manba.distance(manba|String|Number|Date|Array,manba.TYPE)`

```javascript
manba("2012-09-21").distance("2012-09-20 23:59:59") 
//两个日期间相隔天数，纠正日期计算偏差 1

manba("2012-09-21").distance("2012-09-20 23:59:59",manba.DAY) 
//两个日期间相隔天数 1

manba("2012-09-21").distance("2012-08-20 23:59:59",manba.MONTH) 
//两个日期间相隔月数 1

manba("2012-09-21").distance("2011-09-20 23:59:59",manba.YEAR) 
//两个日期间相隔年数 1

```
### add
`add`方法，对日期做加减法，只有add函数，如果需要减法，则传递负数。
`manba.add(Number,manba.TYPE)`

```javascript
manba("2012-10-03 23:59:59").add(1,manba.DAY).format("fff")
//2012年10月04日 23点59分59秒 星期四

manba("2012-10-03 23:59:59").add(-1,manba.DAY).format("fff")
//2012年10月02日 23点59分59秒 星期二

manba("2012-10-03 23:59:59").add(26,manba.MONTH).format("fff")
//2014年12月03日 23点59分59秒 星期三

manba("2012-10-03 23:59:59").add(-1,manba.YEAR).format("fff")
//2011年10月03日 23点59分59秒 星期一

manba("2012-10-03 23:59:59").add(1,manba.MINUTE).format("ff")
//2012年10月04日 00点00分59秒
```

### startOf
`startOf`方法，做一定规则的时间处理，并返回结果。
注：该处理并不修改原来的对象，请使用返回的对象处理。  
`manba.startOf(manba.TYPE)`

```javascript
manba("2012-10-03 23:59:59").startOf(manba.DAY).format("fff")
//2012年10月03日 00点00分00秒 星期三

manba("2012-10-03 23:59:59").startOf(manba.YEAR).format("fff")
//2012年01月01日 00点00分00秒 星期日

manba("2012-10-03 23:59:59").startOf(manba.MONTH).format("fff")
//2012年10月01日 00点00分00秒 星期一

manba("2012-10-03 23:59:59").startOf(manba.HOUR).format("fff")
//2012年10月03日 15点00分00秒 星期三

manba("2012-10-03 23:59:59").startOf(manba.WEEK).format("fff")
//2012年09月30日 00点00分00秒 星期日

manba("2012-10-03 23:59:59").startOf(manba.WEEK,manba.MONDAY).format("fff")
//2012年10月01日 00点00分00秒 星期一
```


### endOf
`endOf`方法，做一定规则的时间处理，并返回结果。
注：该处理并不修改原来的对象，请使用返回的对象处理。  
`manba.endOf(manba.TYPE)`

```javascript
manba("2012-10-03 23:59:59").endOf(manba.DAY).format("ff")
//2012年10月03日 23点59分59秒

manba("2012-10-03 23:59:59").endOf(manba.YEAR).format()
//2012-12-31

manba("2012-10-03 23:59:59").endOf(manba.MONTH).format()
//2012-10-31

manba("2012-10-03 23:59:59").endOf(manba.WEEK).format("fff")
//2012年10月06日 23点59分59秒 星期六

manba("2012-10-03 23:59:59").endOf(manba.WEEK,manba.MONDAY).format("fff")
//2012年10月07日 23点59分59秒 星期日
```

### 星期数
```javascript
//获取当月的星期数
//manba.SUNDAY 星期日开始
//默认星期日
manba().getWeekOfMonth()
manba().getWeekOfMonth(manba.MONDAY)

//获取当年的星期数
//manba.MONDAY 星期一开始
manba().getWeekOfYear(manba.MONDAY)
```

