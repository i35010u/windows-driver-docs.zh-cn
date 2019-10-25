---
title: 主时钟
description: 主时钟
ms.assetid: 87a99371-9c72-4310-bcc7-02af19207b3e
keywords:
- DVD 解码器微型驱动程序 WDK，主时钟
- 解码器微型驱动程序 WDK DVD，主时钟
- 主时钟 WDK DVD 解码器
- 时钟 WDK DVD 解码器
- 内置时钟 WDK DVD 解码器
- 当前流时间 WDK DVD 解码器
- 时间 WDK DVD 解码器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60f8408021acc3b5b76d6da1230ebdce60fe0607
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838042"
---
# <a name="master-clock"></a>主时钟





DVD 解码器微型驱动程序可能指示给定流能够提供主时钟信息。 这表示流是所有其他应同步到的流。 只需要 SRB 结构的两个成员。

*HwClockFunction*成员设置为指向用于处理时钟信息调用的 DVD 解码器微型驱动程序例程的指针。 当 SRB\_打开主时钟流的\_流调用时，将设置例程。 这表明流能够成为系统的主时钟。

[**HW\_时钟\_对象**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_clock_object)结构的*ClockSupportFlags*成员设置为以下值之一：

<a href="" id="clock-support-can-set-onboard-clock"></a>时钟\_支持\_可以\_\_板载\_时钟  
指示设备可将板载时钟时间更改为任意值。

<a href="" id="clock-support-can-read-onboard-clock"></a>时钟\_支持\_可以\_\_板载\_时钟  
指示可以从硬件为此流读取当前的时钟时间。 此时钟不必与当前的流时间关联，只是指示驱动程序能够以100ns 为单位的单元返回值。

<a href="" id="clock-support-can-return-stream-time"></a>时钟\_支持\_可以\_返回\_流\_时间  
指示此流可以返回硬件中正在处理的当前流时间。

有关详细信息，请参阅[主时钟](master-clocks.md)。

 

 




