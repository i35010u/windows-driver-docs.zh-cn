---
title: 流同步
description: 流同步
ms.assetid: bbf589f1-ca4b-41a2-970d-b31c7761eb1a
keywords:
- 同步 WDK DVD 解码器
- 流同步 WDK DVD 解码器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6617b776b1e785edff086964649655817454cb33
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187653"
---
# <a name="stream-synchronization"></a>流同步





DVD 流输入可能由两个或多个流组成。 Stream 类驱动程序可以代表 DVD 解码器微型驱动程序来透明地处理同步。 有关详细信息，请参阅 [微型驱动程序同步](minidriver-synchronization.md)。 程序员仍必须知道影响 DVD 流的几个因素，包括：

-   音频流必须提供主时钟，并且在没有数据时必须合成时钟。 当音频数据停止时，音频流将根据 [**KeQueryPerformanceCounter**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-kequeryperformancecounter)返回的速率匹配和时钟频率使用系统时钟。 所有其他流必须作为音频的从属项。 也就是说，它们将其性能同步到音频流。

-   必须在用户模式下支持软件音频解码器。 时钟转发器 DirectShow 筛选器将 DirectShow 时钟转发到微型驱动程序。 这对于微型驱动程序是透明的。

-   解码器不应使用主要基本流中的时间戳 (PE) 标头。

-   系统时钟引用 (SCRs) 不用于同步。 DVD 包的 SCR 字段设置为零，因为 Microsoft 的 DVD 体系结构使用 "主时钟" 模式进行音频和视频同步。

-   微型驱动程序不会看到时间戳中断。 DVD 导航器/拆分器使所有时间戳是连续的。

如果解码器为音频和视频提供了解码功能，则解码器仅在音频流作为系统主时钟打开时才可以使用硬件同步。 如果音频流不是主时钟，视频流必须将视频解码同步到 stream 类的主时钟。

 

