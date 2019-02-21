---
title: WDF 体系结构
description: WDF 体系结构
ms.assetid: e5e2ed4a-5faf-4879-965f-7316fe64edf9
keywords:
- 内核模式驱动程序 WDK KMDF，体系结构
- KMDF WDK，体系结构
- 内核模式驱动程序框架 WDK，体系结构
- 对象方法 WDK KMDF
- WDK KMDF 体系结构
- 对象事件的回调函数 WDK KMDF
- 事件回调函数 WDK KMDF
- 对象属性 WDK KMDF
- 对象将处理 WDK KMDF
- WDK KMDF 接口
- WDK KMDF 对象
- framework 对象 WDK KMDF，体系结构
- 基于框架的驱动程序 WDK KMDF，体系结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a008ce9d6caaa072269775fbdbe638d75091abf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541344"
---
# <a name="wdf-architecture"></a>WDF 体系结构





WDF 驱动程序提供基于对象的接口。 框架定义的对象，接口包括：

<a href="" id="object-methods"></a>*对象方法*  
方法是将驱动程序可以调用以执行对象的操作或要获取或设置对象属性的函数。 方法名为 **Wdf * * * ObjectAction*，其中*对象*描述的对象并*操作*指示函数的行为。 例如， [ **WdfDeviceCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff545926)创建设备对象。

<a href="" id="object-event-callback-functions"></a>*对象事件的回调函数*  
事件回调函数是驱动程序提供的函数。 每个事件的回调函数都可以在对象中发生的特定事件相关联。 关联的事件发生时，框架将调用事件回调函数。 按照约定，事件回调函数的占位符称为 Evt*ObjectEvent*，尽管可以在您的驱动程序中选择任意命名这些回调。 例如，驱动程序注册[ *EvtDeviceD0Entry* ](https://msdn.microsoft.com/library/windows/hardware/ff540848)事件回调以在其设备将进入工作状态时得到通知。

<a href="" id="object-properties"></a>*对象属性*  
属性是的值存储在对象和一个驱动程序可以*获取*（即，获取） 和*设置*（即，更改）。 在许多情况下，属性直接映射到相应的 WDM 对象中的字段。 不能故障的属性名为 **Wdf***对象***获取 * * * 值*和 **Wdf***对象***设置 * * * 值*，并可能会失败的属性将名为 **Wdf***对象***检索 * * * 值*和 **Wdf***对象***分配 * * * 值*。 *对象*描述了对象，并*值*标识该函数设置或返回的数据。 例如， [ **WdfDeviceGetDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff545998)返回的句柄的设备对象与关联的驱动程序对象。

<a href="" id="object-handles"></a>*对象句柄*  
基于框架的驱动程序绝不会直接访问 framework 对象。 相反，驱动程序收到对象句柄，它可以传递给对象的方法。

框架定义了基于框架的驱动程序使用的几个对象类型：

-   一个*framework 驱动程序对象*表示每个驱动程序。

-   一个*framework 设备对象*表示每个驱动程序支持的设备。

-   *Framework 队列对象*表示接收设备的 I/O 请求的 I/O 队列。

-   *Framework 请求对象*表示每个 I/O 队列接收的 I/O 请求。

有关所有框架定义的对象的列表，请参阅[Framework 对象摘要](summary-of-framework-objects.md)。

 

 





