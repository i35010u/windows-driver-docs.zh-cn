---
title: 默认时钟
description: 默认时钟
ms.assetid: 8c1a51e5-238b-446a-8f20-3fe1b82020b5
keywords:
- 默认时钟，WDK 内核流式处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 224e4847d0ed7f9026589df970e1bd91a5577e7e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837717"
---
# <a name="default-clocks"></a>默认时钟





内核流式处理微型驱动程序可以调用[**KsAllocateDefaultClockEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksallocatedefaultclockex)来分配和初始化默认时钟结构。 或者，它们可以调用[**KsAllocateDefaultClock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksallocatedefaultclock)，它是**KsAllocateDefaultClockEx**的包装器，其中包含 nonclock 成员的默认参数。 使用**KsAllocateDefaultClockEx**后调用[**KsCreateDefaultClock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kscreatedefaultclock)以初始化默认时钟。

默认时钟支持[KSPROPSETID\_时钟](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-clock)，可以像筛选器 pin 提供的任何其他时钟一样访问。 不过，基础数据结构由筛选器 pin 创建，并由该 pin 共享以及所创建时钟的任何实例。 时钟依赖于 pin 来更新共享结构中的当前状态和其他元素。 默认时钟处理通知请求和时钟查询。

当提供此时钟的筛选器上的 pin 分配有主时钟时，pin 拥有此时钟。 该 pin 应引用该时钟文件对象，就像分配了一些其他时钟实现一样。 创建实例时，默认时钟不引用 pin 的文件对象。 相反，它会基于常见时钟结构的初始分配和时钟上打开的每个文件对象保留内部引用计数。 即使时钟的所有者释放了时钟结构，它仍将保留在所有文件对象关闭的位置。 Pin 可以直接访问默认时钟对象，而不是经过标准时钟接口。

微型驱动程序可以支持[**KSPROPERTY\_时钟\_FUNCTIONTABLE**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-clock-functiontable)属性，以便为用户模式客户端提供检查引用时钟时间的机制。 此属性使用可实现此功能的函数指针填充结构，从而支持精确速率匹配。

此外，如果指定的 pin 允许速率更改，则微型驱动程序支持[**KSPROPERTY\_流\_速率**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-stream-rate)属性。

使用内核流式处理代理接口的应用程序调用[IKsClockPropertySet](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksproxy/nn-ksproxy-iksclockpropertyset)接口中的方法来获取和设置物理时钟的时间，可在其他位置使用该时间进行速率匹配。

请参阅[质量管理](quality-management.md)了解相关信息。

 

 




