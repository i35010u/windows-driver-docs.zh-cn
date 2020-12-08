---
title: KS 时钟
description: KS 时钟
keywords:
- 内核流 WDK，时钟
- KS WDK，时钟
- 时钟 WDK 内核流式处理
- 时间 WDK 内核流式处理
- 时间戳 WDK 内核流式处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e83949368beda815cb2b182315ae0f347fe4c443
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792521"
---
# <a name="ks-clocks"></a>KS 时钟





如果要编写 AVStream 微型驱动程序，请参阅 [AVStream 时钟](avstream-clocks.md)。

内核流式处理微型驱动程序通过为 set [KSPROPSETID \_ 时钟](./kspropsetid-clock.md)中的属性提供回调支持时钟操作。 若要了解如何执行此操作，请参阅 [KS 属性](ks-properties.md)。

用户模式客户端可以请求在时钟到达某个时间戳时收到通知，或在时钟上收到固定时间段的定期通知。 为此，客户端 [**将注册 KSEVENT \_ 时钟 \_ 位置 \_ 标记**](./ksevent-clock-position-mark.md) 和 [**KSEVENT \_ 时钟 \_ 间隔 \_ 标记**](./ksevent-clock-interval-mark.md)。

本部分包含有关以下主题的信息：

[主时钟](master-clocks.md)

[默认时钟](default-clocks.md)

 

