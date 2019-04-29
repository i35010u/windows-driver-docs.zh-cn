---
title: 框架对象简介
description: 框架对象简介
ms.assetid: 1314501a-bff1-4aac-a391-a72acca9cc26
keywords:
- framework 对象 WDK KMDF 关于 framework 对象
- 引用计数 WDK KMDF
- 删除回调函数 WDK KMDF
- 回调函数 WDK KMDF
- 父对象 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30820eddd3ea14defa66c337c291ae044f8c3c34
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378153"
---
# <a name="introduction-to-framework-objects"></a>框架对象简介





Windows 驱动程序框架 (WDF) 提供了驱动程序的接口是基于对象的。 该框架定义了多个对象。 这些对象导出[方法](framework-object-methods.md)（函数） 和[属性](framework-object-properties.md)（数据） 的驱动程序可以访问。 Framework 对象也会启动[事件](framework-object-events.md)，可以通过提供事件的回调函数来支持哪些驱动程序。

基于框架的驱动程序永远不会直接访问 framework 对象。 相反，驱动程序引用的对象*句柄*，该驱动程序通过了作为对象方法的输入。

Framework 的所有对象都具有以下特征：

<a href="" id="reference-count"></a>*引用计数*  
框架维护对每个对象的引用数的计数。 当 framework 创建一个对象时，该对象的引用计数设置为 1。 当 framework 完成使用对象，它递减引用计数。 框架不能删除该对象，直到引用计数递减到零，因此驱动程序可以通过递增其引用计数阻止删除的对象。

<a href="" id="context-space"></a>*上下文空间*  
基于框架的驱动程序可创建用于驱动程序接收或创建的每个框架对象的特定于对象上下文空间。 驱动程序应将所有特定于对象的数据存储在对象上下文空间。 有关上下文空间的详细信息，请参阅[框架对象上下文空间](framework-object-context-space.md)。

<a href="" id="deletion-callback-functions"></a>*删除回调函数*  
驱动程序可以注册回叫函数，它删除对象时，框架调用。 回调函数可以删除驱动程序分配的资源，例如特定于对象的内存分配。 有关这些回调函数的详细信息，请参阅[Framework 对象生命周期](framework-object-life-cycle.md)。

<a href="" id="parent-object"></a>*父对象*  
Framework 的所有对象可以都有一个父对象。 该框架将指定的大多数对象的默认父对象。 当驱动程序创建一个对象时，它可以指定重写对象的默认父对象的父对象。 若要将指定对象的父对象、 驱动程序组**ParentObject**的对象的成员[ **WDF\_对象\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff552400)结构。 （对于几个对象类型，驱动程序不能重写默认的父对象。）当框架或驱动程序中删除父对象时，该框架还会删除父对象的子级。

所有由 WDF 定义的对象的概述，请参阅[Framework 对象摘要](summary-of-framework-objects.md)。

 

 





