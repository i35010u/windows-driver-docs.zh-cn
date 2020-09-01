---
title: KS 时钟
description: KS 时钟
ms.assetid: e3ffc7ca-f3cd-4989-af40-78b6a2438f95
keywords:
- 内核流 WDK，时钟
- KS WDK，时钟
- 时钟 WDK 内核流式处理
- 时间 WDK 内核流式处理
- 时间戳 WDK 内核流式处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 89554b34f9dd21ca80c11f7125f7ee8353829e1b
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190003"
---
# <a name="ks-clocks"></a>KS 时钟





如果要编写 AVStream 微型驱动程序，请参阅 [AVStream 时钟](avstream-clocks.md)。

内核流式处理微型驱动程序通过为 set [KSPROPSETID \_ 时钟](./kspropsetid-clock.md)中的属性提供回调支持时钟操作。 若要了解如何执行此操作，请参阅 [KS 属性](ks-properties.md)。

用户模式客户端可以请求在时钟到达某个时间戳时收到通知，或在时钟上收到固定时间段的定期通知。 为此，客户端 [**将注册 KSEVENT \_ 时钟 \_ 位置 \_ 标记**](./ksevent-clock-position-mark.md) 和 [**KSEVENT \_ 时钟 \_ 间隔 \_ 标记**](./ksevent-clock-interval-mark.md)。

本部分包含有关以下主题的信息：

[主时钟](master-clocks.md)

[默认时钟](default-clocks.md)

 

