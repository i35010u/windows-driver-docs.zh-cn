---
title: AVStream 调度表
description: AVStream 调度表
ms.assetid: 974ea9ee-bb59-4973-83ef-c61f0240a555
keywords:
- 调度表 WDK AVStream
- AVStream 调度表 WDK
- KSDEVICE_DISPATCH
- 调度函数 WDK AVStream
- 调度函数 WDK AVStream
- 处理调度 WDK AVStream
- 筛选器为中心的筛选器 WDK AVStream
- pin 为中心的筛选器 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d9649b34cd78430ff640216fbc3ec16f6090f1e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386695"
---
# <a name="avstream-dispatch-tables"></a>AVStream 调度表





AVStream 调度表[ **KSDEVICE\_调度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksdevice_dispatch)，是一组要调度的函数的函数指针。 微型驱动程序可以扩展 AVStream 驱动程序特定的任务执行的回调例程，从而提供的行为。

这些微型驱动程序提供的例程接收通知的特定事件和可能扩展或修改由 AVStream 提供的默认事件处理。

这两[ **KSFILTER\_调度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksfilter_dispatch)并[ **KSPIN\_调度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_kspin_dispatch)结构都可提供名为调度*进程*。 使用此调度来区分[筛选器以中心](filter-centric-processing.md)从筛选[pin 构建以](pin-centric-processing.md)筛选器。若要指定筛选器为中心的筛选器，提供指向筛选器调度表中的过程调度回调例程的指针。 Pin 为中心的筛选器提供了在每个 pin 描述符表过程调度。

你可以注册筛选器，以获得有关创建、 删除操作，需要处理数据和重置的通知。 你可以注册插针，以接收事件通知的作品，如闭包，需要处理数据，重置，设置数据格式和状态更改。 若要注册通知的对象，提供指向相关调度结构中的供应商提供的调度例程的指针。

调度函数的详细信息，请参阅[ **KSFILTER\_调度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksfilter_dispatch)， [ **KSPIN\_调度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_kspin_dispatch)，并[ **KSALLOCATOR\_调度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksallocator_dispatch)。

 

 




