---
title: 流式处理微型驱动程序中的数据格式和数据范围
description: 流式处理微型驱动程序中的数据格式和数据范围
ms.assetid: ea3aa4af-0c8c-429e-b399-0a196eadc5ef
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
ms.openlocfilehash: 6001b982453ede293b8f729475a3f70541df2891
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190593"
---
# <a name="data-formats-and-data-ranges-in-streaming-minidrivers"></a>流式处理微型驱动程序中的数据格式和数据范围





每个流详细说明了它在其[**HW \_ 流 \_ 信息**](/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_information)结构的**StreamFormatsArray**成员中所支持的数据区域。

有关格式和范围交集的详细信息，请参阅 [AVStream 中的数据范围交集](data-range-intersections-in-avstream.md)。

 

