---
title: 编写 AVStream 微型驱动程序硬件
description: 编写 AVStream 微型驱动程序硬件
ms.assetid: d7dc42d7-efd0-41ff-abab-d97c508a41e6
keywords:
- AVStream WDK 硬件
- 硬件 WDK AVStream
- AVStrMiniDeviceStart
- 筛选器关系图中会 WDK AVStream
- 关系图 WDK AVStream
- 关系图 WDK AVStream 之间产生干扰
- 编码 WDK AVStream
- 解码 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c9b539cd100ecdc94ec320bff8f103d74638ef0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543577"
---
# <a name="writing-avstream-minidrivers-for-hardware"></a>编写 AVStream 微型驱动程序硬件





中的供应商提供[ *AVStrMiniDeviceStart*](https://msdn.microsoft.com/library/windows/hardware/ff556297)，支持的硬件的 AVStream 微型驱动程序应首先分析资源列表，然后调用[ **IoConnectInterrupt** ](https://msdn.microsoft.com/library/windows/hardware/ff548371)注册中断服务例程 (ISR)。

如果您的驱动程序支持直接内存访问 (DMA)，则需要其他步骤。 如果您的驱动程序实现 DMA，请参阅[AVStream DMA 服务](avstream-dma-services.md)。

如果同时使用你的设备筛选器图形可能生成多个应用程序，您必须采取措施以防止之间的关系图的干扰。 具体而言，如果构造的图表中使用设备的应用程序，您必须不会干扰正在不间断状态在使用该设备的应用程序。

可以通过图形转换到 KSSTATE 后加载微代码，避免干扰\_ACQUIRE。 这将保护当前正在运行的关系图，因为新的关系图将不会转换成**KSSTATE\_ACQUIRE**当前正在运行另一个关系图时。 若要接收的 pin 状态更改通知，请提供[ *AVStrMiniPinSetDeviceState* ](https://msdn.microsoft.com/library/windows/hardware/ff556359)中的回调例程[ **KSPIN\_调度**](https://msdn.microsoft.com/library/windows/hardware/ff563535)结构。

为了尽量减少图形启动时间，但是，你可能想要在关系图到达 KSSTATE 之前加载了微代码\_ACQUIRE。 在这种情况下，请考虑在启动过程中加载微代码，在低优先级后台线程中。 此解决方案不会影响其他应用程序，可减少图形开始时间，并应不延长启动时间，如果以异步方式执行此操作。

在启动之后，但是，请勿重新加载了微代码或操作硬件寄存器图形直到 KSSTATE\_ACQUIRE。

若要查看如何连接的新的关系图可能会影响正在运行的图形，请考虑支持编码和解码，但仅一次执行一个这些任务的视频捕获设备。 微型驱动程序公开一个编码筛选器和解码筛选器。

应用程序生成筛选器关系图包含编码筛选器。 微型驱动程序将加载微代码，编码在 pin 连接时。 筛选器关系图启动并在硬件开始编码。

编码硬件，而另一个应用程序将筛选器关系图中放置解码筛选器。 解码插针连接时，*球瓶到 KSSTATE 更改状态之前\_ACQUIRE*，微型驱动程序尝试配置用于解码的硬件。 此重新配置会影响当前处于活动状态的编码图形并可能会导致驱动程序不稳定。

 

 




