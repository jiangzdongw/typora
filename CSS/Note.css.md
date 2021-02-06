## 样式的分类

- 布局样式
- 非布局样式。宋体，行高，背景，边框，滚动，文本折行，装饰属性

## 样式的权重

## CSS 非布局样式

### 字体

### 行高

### 背景

### 边框

### 滚动

### 装饰属性

### 文字的折行

- overflow-wrap(word-wrap) 通用换行控制，是否保留单词
- word-break 针对多字节文字，中文句子也被当作单词
- white-space 空白处是否断行

## CSS 布局样式

table 表格布局

float 浮动 + margin

inline-block 布局

flexbox 布局



## 面试题

### CSS样式（选择器）的优先级

- 计算权重的确定
- ！important
- 内联样式
- 权重相同时，后写的优先级更高

### 雪碧图的作用（背景图的定位）

- 减少HTTP的请求数，提高加载性能
- 有一些情况下可以减少图片的大小

### 自定义字体的使用场景

- 字体图标
- 特定场景使用（只使用部分字体）

### base64 的使用

- 用于减少HTTP的请求
- 适用于小图片
- base64的体积约为原图的4/3，字节增多

### 伪元素与伪类的区别

- 伪元素表一种状态
- 伪类表是真的有元素，或可以选择的部分内容
- 伪元素使用双冒号，伪类使用单冒号

### 如保美化checkbox

- label[for] 和 id
- 隐藏原生input
- :checked + label

---

### 如何用一个DIV 画图形

box-shadow 无限投影，::before ::after

### 如何产生不占空间的边框

- box-shadow
- outline

### 如何实现圆形元素

- border-radius: 50%;

### 如何实现 IOS  图标圆角

- clip-path: (svg)

### 如何实现半圆、扇形等图形

- border-radius 组合
- 有无边框
- 边框粗细
- 圆角半径

### 如何实现背景图居中显示/不重复/改变大小

- background-position
- background-repeat
- background-size: cover/contain

### 如何平移/放大一个元素

- transform: translateX(100px)
- transform: scale(2)

### 如何实现3D效果

- perspective: 500px
- transform-style: preserve-3d
- transform: translate/rotate …