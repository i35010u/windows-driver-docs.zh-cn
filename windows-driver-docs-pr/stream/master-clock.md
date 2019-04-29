---
title: 主时钟
description: 主时钟
ms.assetid: 87a99371-9c72-4310-bcc7-02af19207b3e
keywords:
- DVD 解码器微型驱动程序 WDK，主时钟
- 解码器微型驱动程序 WDK DVD，主时钟
- 主时钟 WDK DVD 解码器
- 时钟的 WDK DVD 解码器
- 载入时钟 WDK DVD 解码器
- 当前流时间 WDK DVD 解码器
- 时间 WDK DVD 解码器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 13d23dc4318f5cbebb44d6009b17581009cbb368
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375593"
---
# <a name="master-clock"></a>主时钟





DVD 解码器微型驱动程序可能指示给定的流是能够提供主时钟信息。 这表示该流是一个到的所有其他应进行同步。 所需的 SRB 结构只有两个成员。

*HwClockFunction*成员设置为指向处理的时钟信息调用 DVD 解码器微型驱动程序例程的指针。 例程会设置 SRB\_打开\_接收主时钟流的流调用。 这表示流能够作为主系统时钟。

*ClockSupportFlags*的成员[ **HW\_时钟\_对象**](https://msdn.microsoft.com/library/windows/hardware/ff559671)结构设置为以下值之一：

<a href="" id="clock-support-can-set-onboard-clock"></a>时钟\_支持\_可以\_设置\_载入\_时钟  
指示设备可以为任意值来更改要登记的时钟时间。

<a href="" id="clock-support-can-read-onboard-clock"></a>时钟\_支持\_可以\_读取\_载入\_时钟  
指示可以为硬件中的此流读取当前时钟时间。 此时钟不具有关联到当前流时，它只是表示该驱动程序能够返回中载入时钟的 100ns 个单位的值。

<a href="" id="clock-support-can-return-stream-time"></a>时钟\_支持\_可以\_返回\_流\_时间  
指示此流可以返回当前正在处理的硬件中的流时间。

有关详细信息，请参阅[Master 时钟](master-clocks.md)。

 

 




