---
title: 建造者模式 
tags: 设计模式
---


1. 本质
   * 分离了对象子组件的单独构造（由Builder来负责）和装配（由Director负责），从而可以构造出复杂的对象

2. 应用场景
   * StringBuilder类的append方法
   * SQL中的PrepareStatement
   * JDOM中的DomBuilder、SAXBuilder