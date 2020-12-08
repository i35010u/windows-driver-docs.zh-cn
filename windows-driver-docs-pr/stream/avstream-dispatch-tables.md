---
title: AVStream 调度表
description: AVStream 调度表
keywords:
- 调度表 WDK AVStream
- AVStream 调度表 WDK
- KSDEVICE_DISPATCH
- 调度函数 WDK AVStream
- 调度函数 WDK AVStream
- 处理调度 WDK AVStream
- 以筛选为中心的筛选器 WDK AVStream
- pin 中心筛选器 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1279d5238b5c3f25c3223ded4a5e065c29f0d40b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806705"
---
# <a name="avstream-dispatch-tables"></a>AVStream 调度表





AVStream 调度表 [**KSDEVICE \_ 调度**](/windows-hardware/drivers/ddi/ks/ns-ks-_ksdevice_dispatch)是一组用于调度函数的函数指针。 微型驱动程序可以通过提供执行特定于驱动程序的任务的回调例程来扩展 AVStream 提供的行为。

这些微型驱动程序提供的例程接收特定事件的通知，并可能扩展或修改 AVStream 提供的默认事件处理。

[**KSFILTER \_ 调度**](/windows-hardware/drivers/ddi/ks/ns-ks-_ksfilter_dispatch)和 [**KSPIN \_ 调度**](/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_dispatch)结构都提供名为 *Process* 的调度。 使用此调度来区分以[pin 为中心](pin-centric-processing.md)的筛选器的以[筛选为中心](filter-centric-processing.md)的筛选器。若要指定以筛选为中心的筛选器，请在筛选器调度表中提供一个指向进程调度回调例程的指针。 以 pin 为中心的筛选器提供每个 pin 描述符表中的进程调度。

你可以注册筛选器，以获得有关创建、删除、需要处理数据和重置的通知。 你可以注册要通知哪些事件，如创建、关闭、处理数据、重置、设置数据格式和状态更改等事件。 若要为通知注册对象，请提供一个指向相关调度结构中供应商提供的调度例程的指针。

有关调度函数的详细信息，请参阅 [**KSFILTER \_ 调度**](/windows-hardware/drivers/ddi/ks/ns-ks-_ksfilter_dispatch)、 [**KSPIN \_ 调度**](/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_dispatch)和 [**KSALLOCATOR \_ 调度**](/windows-hardware/drivers/ddi/ks/ns-ks-_ksallocator_dispatch)。

 

