---
title: 框架对象简介
description: 框架对象简介
ms.assetid: 1314501a-bff1-4aac-a391-a72acca9cc26
keywords:
- framework 对象 WDK KMDF，关于框架对象
- 引用计数 WDK KMDF
- 删除回调函数 WDK KMDF
- 回调函数 WDK KMDF
- 父对象 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 721caf6d87bedbeafd48df16e82f174ba73ae1d2
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89183807"
---
# <a name="introduction-to-framework-objects"></a>框架对象简介





Windows 驱动程序框架 (WDF) 提供给驱动程序的接口是基于对象的接口。 框架定义了多个对象。 这些对象 (函数导出 [方法](framework-object-methods.md)) 和 [属性](framework-object-properties.md) (驱动程序可以访问的数据) 。 框架对象还可通过提供事件回调函数来启动事件，这些 [事件](framework-object-events.md)由驱动程序支持。

基于框架的驱动程序绝不会直接访问框架对象。 相反，驱动程序通过 *句柄*来引用对象，驱动程序将该对象作为输入传递给对象方法。

所有框架对象具有以下特征：

<a href="" id="reference-count"></a>*引用计数*  
框架维护对每个对象的引用数的计数。 当框架创建对象时，它会将对象的引用计数设置为1。 当框架完成使用对象时，它会递减引用计数。 在引用计数递减为零时，框架无法删除对象，因此，驱动程序可以通过增加对象的引用计数来阻止删除该对象。

<a href="" id="context-space"></a>*上下文空间*  
基于框架的驱动程序可以为驱动程序接收或创建的每个框架对象创建特定于对象的上下文空间。 驱动程序应将所有特定于对象的数据存储在对象的上下文空间中。 有关上下文空间的详细信息，请参阅 [框架对象上下文空间](framework-object-context-space.md)。

<a href="" id="deletion-callback-functions"></a>*删除回调函数*  
驱动程序可以注册框架在删除对象时调用的回调函数。 回调函数可以删除驱动程序分配的资源，例如对象特定的内存分配。 有关这些回调函数的详细信息，请参阅 [框架对象生命周期](framework-object-life-cycle.md)。

<a href="" id="parent-object"></a>*父对象*  
所有框架对象都可以有一个父对象。 框架为大多数对象指定默认的父对象。 当驱动程序创建对象时，它可以指定重写对象的默认父对象的父对象。 为了指定对象的父对象，驱动程序将设置对象的[**WDF \_ 对象 \_ 属性**](/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes)结构的**ParentObject**成员。 对于少量对象类型 (，驱动程序不能覆盖默认父对象 ) 。在框架或驱动程序删除父对象时，框架还会删除父对象的子对象。

有关 WDF 定义的所有对象的概述，请参阅 [框架对象的摘要](summary-of-framework-objects.md)。

 

