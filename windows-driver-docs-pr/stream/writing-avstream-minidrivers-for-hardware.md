---
title: 为硬件编写 AVStream 微型驱动程序
description: 为硬件编写 AVStream 微型驱动程序
ms.assetid: d7dc42d7-efd0-41ff-abab-d97c508a41e6
keywords:
- AVStream WDK，硬件
- 硬件 WDK AVStream
- AVStrMiniDeviceStart
- 筛选器图形 WDK AVStream
- 曲线图 WDK AVStream
- 关系图 WDK AVStream 之间的干扰
- 编码 WDK AVStream
- 解码 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ae2411831b164d1a137e9496724f2186dc2b4ae2
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192763"
---
# <a name="writing-avstream-minidrivers-for-hardware"></a>为硬件编写 AVStream 微型驱动程序





在供应商提供的 [*AVStrMiniDeviceStart*](/windows-hardware/drivers/ddi/ks/nc-ks-pfnksdevicepnpstart)中，支持硬件的 AVStream 微型驱动程序应该首先分析资源列表，然后调用 [**IOCONNECTINTERRUPT**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterrupt))  (ISR 注册中断服务例程。

如果驱动程序支持 (DMA) 的直接内存访问，则需要执行其他步骤。 如果驱动程序实现 DMA，请参阅 [AVSTREAM DMA Services](avstream-dma-services.md)。

如果有多个应用程序可能使用您的设备同时生成筛选器关系图，则必须小心阻止关系图之间的干扰。 具体而言，如果使用设备在应用程序中构造图形，则不能干扰使用处于非停止状态的设备的应用程序。

可以通过在图形转换到 KSSTATE 获取后加载微代码来避免干扰 \_ 。 这将保护当前正在运行的关系图，因为在另一个关系图当前正在运行时，新的关系图不会转换为 **KSSTATE \_ 获取** 。 若要接收有关 pin 状态更改的通知，请在[**KSPIN \_ 调度**](/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_dispatch)结构中提供一个[*AVStrMiniPinSetDeviceState*](/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspinsetdevicestate)回调例程。

不过，为了最大限度地减少图形启动时间，你可能希望在图形进入 KSSTATE 获取之前加载微代码 \_ 。 在这种情况下，请考虑在启动过程中在低优先级后台线程中加载微代码。 此解决方案不会干扰其他应用程序，减少图形启动时间，而且不应在异步完成时加长启动时间。

但在启动后，请不要重新加载微码或操作硬件寄存器，直到图形进入 KSSTATE \_ 获取。

若要查看新图形连接如何干扰正在运行的图形，请考虑支持编码和解码的视频捕获设备，但是一次只执行其中一项任务。 微型驱动程序公开编码筛选器和解码筛选器。

应用程序生成包含编码筛选器的筛选器图。 微型驱动程序加载微代码，以便在连接时进行编码。 筛选器图开始，硬件开始编码。

当硬件编码时，其他应用程序将解码筛选器放在筛选器图中。 如果已连接了解码 pin，则在将 *状态更改为 KSSTATE \_ 获取之前*，微型驱动程序会尝试配置要解码的硬件。 此重新配置与当前处于活动状态的编码图形冲突，并可能导致驱动程序不稳定。

 

