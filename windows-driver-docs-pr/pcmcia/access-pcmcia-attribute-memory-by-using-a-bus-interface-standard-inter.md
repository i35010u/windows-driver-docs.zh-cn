---
title: 通过使用 BUS_INTERFACE_STANDARD 访问内存
description: 通过使用 BUS_INTERFACE_STANDARD 接口访问 PCMCIA 属性内存
ms.assetid: 2696a9ca-38b5-47f2-9639-029bba1173b5
keywords:
- 属性内存 WDK PCMCIA 总线，BUS_INTERFACE_STANDARD 接口
- BUS_INTERFACE_STANDARD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c89c86a41547e892e94ec5452fa7be9ad7a60cd6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391585"
---
# <a name="access-pcmcia-attribute-memory-by-using-a-businterfacestandard-interface"></a>通过使用总线访问 PCMCIA 属性内存\_接口\_标准接口





本部分介绍如何通过 PC 卡或 CardBus 卡驱动程序使用总线\_接口\_访问属性内存的标准接口。

驱动程序应使用 BUS\_接口\_标准接口，如果是不可接受的 I/O 请求的开销。 此方法的 I/O 请求方法，正如在于它将传递的缓冲区指针。 但是，此方法调用的接口例程，消除了 I/O 请求的开销。 驱动程序必须使用此方法，如果它在 IRQL 调度运行时访问属性内存\_级别 − 例如，在延缓过程调用 (DPC)。

驱动程序可以使用此方法，同时运行在 IRQL &lt;= DISPTACH\_级别。

驱动程序通常将获取总线\_接口\_在初始化期间及其的标准接口。 驱动程序使用[ **IRP\_MN\_查询\_接口**](https://msdn.microsoft.com/library/windows/hardware/ff551687)请求以获取从 PCMCIA 总线驱动程序接口。 必须在 IRQL 被动发送查询接口请求\_级别。

驱动程序将获取标准总线接口后，该驱动程序可以调用接口例程**GetBusData**或**SetBusData**访问属性内存。

 

 





