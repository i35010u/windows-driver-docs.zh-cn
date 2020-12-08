---
title: 默认时钟
description: 默认时钟
keywords:
- 默认时钟，WDK 内核流式处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb7ae8d46fc282bf22ec277c973f5f6936e1cbba
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811363"
---
# <a name="default-clocks"></a>默认时钟





内核流式处理微型驱动程序可以调用 [**KsAllocateDefaultClockEx**](/windows-hardware/drivers/ddi/ks/nf-ks-ksallocatedefaultclockex) 来分配和初始化默认时钟结构。 或者，它们可以调用 [**KsAllocateDefaultClock**](/windows-hardware/drivers/ddi/ks/nf-ks-ksallocatedefaultclock)，它是 **KsAllocateDefaultClockEx** 的包装器，其中包含 nonclock 成员的默认参数。 使用 **KsAllocateDefaultClockEx** 后调用 [**KsCreateDefaultClock**](/windows-hardware/drivers/ddi/ks/nf-ks-kscreatedefaultclock)以初始化默认时钟。

默认时钟支持 [KSPROPSETID \_ 时钟](./kspropsetid-clock.md)，可以像筛选器 pin 提供的任何其他时钟一样访问。 不过，基础数据结构由筛选器 pin 创建，并由该 pin 共享以及所创建时钟的任何实例。 时钟依赖于 pin 来更新共享结构中的当前状态和其他元素。 默认时钟处理通知请求和时钟查询。

当提供此时钟的筛选器上的 pin 分配有主时钟时，pin 拥有此时钟。 该 pin 应引用该时钟文件对象，就像分配了一些其他时钟实现一样。 创建实例时，默认时钟不引用 pin 的文件对象。 相反，它会基于常见时钟结构的初始分配和时钟上打开的每个文件对象保留内部引用计数。 即使时钟的所有者释放了时钟结构，它仍将保留在所有文件对象关闭的位置。 Pin 可以直接访问默认时钟对象，而不是经过标准时钟接口。

微型驱动程序可以支持 [**KSPROPERTY \_ 时钟 \_ FUNCTIONTABLE**](./ksproperty-clock-functiontable.md) 属性，以便为用户模式客户端提供检查引用时钟时间的机制。 此属性使用可实现此功能的函数指针填充结构，从而支持精确速率匹配。

此外，如果指定的 pin 允许速率更改，则微型驱动程序支持 [**KSPROPERTY \_ 流 \_ 速率**](./ksproperty-stream-rate.md) 属性。

使用内核流式处理代理接口的应用程序调用 [IKsClockPropertySet](/windows-hardware/drivers/ddi/ksproxy/nn-ksproxy-iksclockpropertyset) 接口中的方法来获取和设置物理时钟的时间，可在其他位置使用该时间进行速率匹配。

请参阅 [质量管理](quality-management.md) 了解相关信息。

 

