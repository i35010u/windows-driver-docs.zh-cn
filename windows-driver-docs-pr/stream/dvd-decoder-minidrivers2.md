---
title: DVD 解码器微型驱动程序
description: DVD 解码器微型驱动程序
ms.assetid: 1dec271d-47cf-4ab6-9149-7f5b9b92b189
keywords:
- Windows 2000 内核流式处理模型 WDK，DVD 解码器微型驱动程序
- 流式处理模型 WDK Windows 2000 内核，DVD 解码器微型驱动程序
- 内核流式处理模型 WDK，DVD 解码器微型驱动程序
- DVD 解码器微型驱动程序 WDK
- 解码器微型驱动程序 WDK DVD
- 电影播放 WDK DVD 解码器
- 音频播放 WDK DVD 解码器
- 视频回放 WDK DVD 解码器
- 播放 WDK DVD 解码器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 32203fa7e859a19a4056f92b1e2b386e9eda5444
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363721"
---
# <a name="dvd-decoder-minidrivers"></a>DVD 解码器微型驱动程序





DVD 提供了包含音频、 视频和其他数字数据的数字数据存储。 本文档讨论的 DVD 解码器微型驱动程序用于从 DVD 的电影播放 （视频和音频） 的设计。 这些微型驱动程序控制读取并解码如 mpeg-2 （视频和音频）、 ac-3 和 DTS DVD 数据流格式的 DVD 解码器适配器卡。

使用流类驱动程序的 DVD 解码器微型驱动程序接口。 这允许创建多功能设备的驱动程序的开发人员在使用某一单独的驱动程序模型运行的所有数据类型的流类上进行构建 (mpeg-2，ac-3、 DTS，等等)。

DVD 解码器微型驱动程序是可移植，并且如果它们使用 stream 类驱动程序提供同步具有任何多处理器问题。 以前，开发人员将不得不创建单独的驱动程序对于 MPEG 2，音频，使用各种驱动程序模型 MIDI 和子画面。 有关详细信息，请参阅[流式处理微型驱动程序](streaming-minidrivers2.md)。

论述了以下主题：

[在 Windows 中的 DVD 解码器支持](dvd-decoder-support-in-windows.md)

[DVD 数据流](dvd-data-streams.md)

[DVD 版权保护](dvd-copyright-protection.md)

[DVD 区域化](dvd-regionalization.md)

[Master 时钟](master-clock.md)

 

 




