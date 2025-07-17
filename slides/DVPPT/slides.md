---
title: DVPPT
background: https://cover.sli.dev
date: 2022-06-19 23:37:33
layout: center
theme: seriph
transition: fade-out
lineNumbers: true
---

# 大数据可视化

### Yuumi 吴元昊 沈溢鼎

#### 按姓名首字母排序（假装严谨）

---
transition: slide-up
---

## 数据介绍

- **内容**：

  ​		葡萄牙波尔图出租车运营数据

  ​		https://www.kaggle.com/crailtap/taxi-trajectory

- **数据时间跨度**：

  ​		2016.7.1 —— 2017.6.30

- **数据大小**：

  ​		2.03GB

---
transition: slide-up
---

## 数据信息介绍

每个数据样本对应一个已完成的行程。

它总共包含9个属性，描述如下：

```
TRIP_ID：（字符串）每一次行程都有唯一的TRIP_ID标号，以用来区分。
CALL_TYPE：（字符）由A、B、C三类标识来区分打车形式。A: 由中心调度；B: 在特定站点直接打车；C: 其他类型。
ORIGIN_CALL：（整型）用来唯一标识此次行程消费者的电话号码。
ORIGIN_STAND：（整型）唯一标识出租车站点。
TAXI_ID：（整型）每一次行程中出租车司机的唯一标识。
TIMESTAMP：（整型）Unix 时间戳，标识行程的开始。
DAYTYPE：（字符）由A、B、C三类标识区别出租车行程的日期类型。A: 其他；B: 假期；C: 假期前一天。
MISSING_DATA：（布尔值）当POLYLINE中有一个或多个坐标丢失时，值为true，否则为false。
POLYLINE：（字符串）由坐标序列组成，起始坐标为出发点，结尾坐标为目的地。行程中每隔15秒记录一次坐标信息。
```

---
transition: fade-out
layout: center
---

## 可视化形式

1. 综合分析

2. 路线图

3. 热力图

---
transition: fade-out
layout: center
---

# 综合分析

---
transition: slide-up
layout: center
---

## 数据概览

1. 数据年份统计

2. 每月行程数统计

3. 每小时行程数统计

4. 行程类型占比统计

---
transition: slide-up
---

<iframe 
    id="graph1"
    title="graph1"
    src="/DVPPT/html/Analysis/1year.html"
	height="500px"
    width="100%" 
    frameborder="0" 
    style="box-shadow: 0px 0px 20px -10px #888;"
    scrolling="no"
></iframe>

---
transition: slide-up
---

<iframe id="graph2"
	title="graph2"
	src="/DVPPT/html/Analysis/2month.html" 
	height="500px" 
	width="100%" 
	scrolling="no"
	frameborder="0" 
	style="box-shadow: 0px 0px 20px -10px #888;">
</iframe>

---
transition: slide-up
---

<iframe id="graph3"
	title="graph3"
	src="/DVPPT/html/Analysis/3hour1.html" 
	height="500px" 
	width="100%" 
	scrolling="no"
	frameborder="0" 
	style="box-shadow: 0px 0px 20px -10px #888;">
</iframe>

---
transition: slide-up
---

<iframe id="graph4"
	title="graph4"
	src="/DVPPT/html/Analysis/4hour2.html" 
	height="500px" 
	width="100%" 
	scrolling="no" 
	frameborder="0" 
	style="box-shadow: 0px 0px 20px -10px #888;">
</iframe>

---
transition: slide-left
---

<iframe id="graph5"
	title="graph5"
	src="/DVPPT/html/Analysis/5type.html" 
	height="500px" 
	width="100%" 
	scrolling="no" 
	frameborder="0" 
	style="box-shadow: 0px 0px 20px -10px #888;">
</iframe>

---
transition: slide-up
layout: center
---

## 行程数-时间 数据分析

1. 一周内平均每日行程数比较

2. 不同类型行程数比较

---
transition: slide-up
---

<iframe id="graph6"
	title="graph6"
	src="/DVPPT/html/Analysis/6average_week_day.html" 
	height="500px" 
	width="100%" 
	scrolling="no" 
	frameborder="0" 
	style="box-shadow: 0px 0px 20px -10px #888;">
</iframe>

---
transition: slide-up
---

<iframe id="graph7"
	title="graph7"
	src="/DVPPT/html/Analysis/7type_week_day1.html" 
	height="500px" 
	width="100%" 
	scrolling="no" 
	frameborder="0" 
	style="box-shadow: 0px 0px 20px -10px #888;">
</iframe>

---
transition: slide-left
---

<iframe id="graph8"
	title="graph8"
	src="/DVPPT/html/Analysis/8type_week_day2.html" 
	height="500px" 
	width="100%" 
	scrolling="no" 
	frameborder="0" 
	style="box-shadow: 0px 0px 20px -10px #888;">
</iframe>

---
transition: slide-up
layout: center
---

## 行驶路线-行程时长 数据分析

1. 行程时长统计

2. 行程时长区间统计

3. 行程时长区间占比

4. 工作日与休息日比较

---
transition: slide-up
---

### 行程时长统计

![9trip_len](/images/Analysis/9trip_len.png)

---
transition: slide-up
---

<iframe id="graph9"
	title="graph9"
	src="/DVPPT/html/Analysis/10trip_interval1.html" 
	height="500px" 
	width="100%" 
	scrolling="no" 
	frameborder="0" 
	style="box-shadow: 0px 0px 20px -10px #888;">
</iframe>

---
transition: slide-up
---

<iframe id="graph10"
	title="graph10"
	src="/DVPPT/html/Analysis/11trip_interval2.html" 
	height="500px" 
	width="100%" 
	scrolling="no" 
	frameborder="0" 
	style="box-shadow: 0px 0px 20px -10px #888;">
</iframe>

---
transition: fade-out
---

<iframe id="graph11"
	title="graph11"
	src="/DVPPT/html/Analysis/12trip_comp.html" 
	height="500px" 
	width="100%" 
	scrolling="no" 
	frameborder="0" 
	style="box-shadow: 0px 0px 20px -10px #888;">
</iframe>

---
src: ./pages/DVPPT1.md
hide: false
---

---
src: ./pages/DVPPT2.md
hide: false
---

---
src: ./pages/DVPPT3.md
hide: false
---