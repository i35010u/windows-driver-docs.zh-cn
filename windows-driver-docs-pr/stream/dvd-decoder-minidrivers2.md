---
title: DVD 解码器微型驱动程序
description: DVD 解码器微型驱动程序
keywords:
- Windows 2000 内核流式处理模型 WDK，DVD 解码器微型驱动程序
- 流式处理模型 WDK Windows 2000 内核，DVD 解码器微型驱动程序
- 内核流式处理模型 WDK，DVD 解码器微型驱动程序
- DVD 解码器微型驱动程序 WDK
- 解码器微型驱动程序 WDK DVD
- 电影播放 WDK DVD 解码器
- 音频播放 WDK DVD 解码器
- 视频播放 WDK DVD 解码器
- 播放 WDK DVD 解码器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 00a3bc8dac47c36989a2584e00abde826d7808f9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783753"
---
# <a name="dvd-decoder-minidrivers"></a>DVD 解码器微型驱动程序





DVD 提供了包含音频、视频和其他数字数据的数字数据存储。 本文档讨论了用于电影播放的 DVD 解码器微型驱动程序的设计， (视频和音频) 从 DVD 播放。 这些微型驱动程序控制 DVD 解码器适配器卡，用于读取和解码 DVD 数据流格式，如 MPEG-2 (视频和音频) 、AC-3 和 DTS。

带有 stream 类驱动程序的 DVD 解码器微型驱动程序接口。 这允许开发人员创建用于多功能设备的驱动程序，以使用适用于所有数据类型 (MPEG-2、AC-3、DTS 等) 的单个驱动程序模型在 stream 类上生成。

DVD 解码器微型驱动程序是可移植的，如果使用流类驱动程序提供了同步，则不会出现多处理器问题。 以前，开发人员必须使用 MPEG-2、音频、MIDI 和子画面的各种驱动程序模型创建单独的驱动程序。 有关详细信息，请参阅 [流式处理微型驱动程序](streaming-minidrivers2.md)。

本文讨论了以下主题：

[Windows 中的 DVD 解码器支持](dvd-decoder-support-in-windows.md)

[DVD 数据流](dvd-data-streams.md)

[DVD 版权保护](dvd-copyright-protection.md)

[DVD 区域化](dvd-regionalization.md)

[主时钟](master-clock.md)

 

 




