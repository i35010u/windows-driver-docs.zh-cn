---
title: KS 时钟
description: KS 时钟
ms.assetid: e3ffc7ca-f3cd-4989-af40-78b6a2438f95
keywords:
- 流式处理 WDK，时钟的内核
- KS WDK 时钟
- 流式处理的时钟 WDK 内核
- 流式处理的时间 WDK 内核
- 流式处理的时间戳 WDK 内核
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b485ad341daaad779b80aba8cbc3356ba5881e5e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382549"
---
# <a name="ks-clocks"></a>KS 时钟





如果你正在编写 AVStream 微型驱动程序，请参阅[AVStream 时钟](avstream-clocks.md)。

内核流式处理的微型驱动程序支持时钟操作通过一组中的属性提供回调[KSPROPSETID\_时钟](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-clock)。 若要了解如何执行此操作，请参阅[KS 属性](ks-properties.md)。

用户模式下客户端可以请求一个时钟达到特定的时间戳时收到通知，或接收时钟上固定的时间量已过的定期通知。 若要执行此操作，客户端注册[ **KSEVENT\_时钟\_位置\_标记**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-clock-position-mark)并[ **KSEVENT\_时钟\_间隔\_标记**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-clock-interval-mark)。

本部分包含有关以下主题的信息：

[Master 时钟](master-clocks.md)

[默认时钟](default-clocks.md)

 

 




