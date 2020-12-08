---
title: 流式处理微型驱动程序中的数据格式和数据范围
description: 流式处理微型驱动程序中的数据格式和数据范围
keywords:
- Stream.sys 类驱动程序 WDK Windows 2000 内核、数据格式和范围
- 流式传输微型驱动程序 WDK Windows 2000 内核，数据格式和范围
- 微型驱动程序 WDK Windows 2000 内核流式处理，数据格式和范围
- 数据格式 WDK 流式处理微型驱动程序
- 数据范围 WDK 流式处理微型驱动程序
- 范围 WDK 流式处理微型驱动程序
- 格式化 WDK 流式处理微型驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 293b8b0f4bf08b9549385e609ff556979a008807
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817961"
---
# <a name="data-formats-and-data-ranges-in-streaming-minidrivers"></a>流式处理微型驱动程序中的数据格式和数据范围





每个流详细说明了它在其 [**HW \_ 流 \_ 信息**](/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_information)结构的 **StreamFormatsArray** 成员中所支持的数据区域。

有关格式和范围交集的详细信息，请参阅 [AVStream 中的数据范围交集](data-range-intersections-in-avstream.md)。

 

