---
title: 编码器设备
description: 编码器设备
ms.assetid: 156b1d6d-c6f6-4ab3-a91e-3124351c6ae5
keywords:
- 编码器设备 WDK AVStream
- AVStream WDK，编码器设备
- 未压缩的数据流 WDK AVStream
- 编码流 WDK AVStream
- 音频编码器设备 WDK AVStream
- 视频编码器设备 WDK AVStream
- 基于软件的编码器 WDK AVStream
- 基于硬件的编码器 WDK AVStream
- 集成编码器 WDK AVStream
- 独立编码器 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1dd748cf3209d28a4e23c072d46720ab058d1be3
ms.sourcegitcommit: ba3199328ea5d80119eafc399dc989e11e7ae1d6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2019
ms.locfileid: "74861839"
---
# <a name="encoder-devices"></a>编码器设备

编码器是接收到作为输入的未压缩数据流（视频和/或音频）的设备，将流编码为特定格式（例如 MPEG2），然后输出编码流。 编码器设备可能是其他设备（如组合电视调谐器/捕获适配器）的一部分，也可能是独立的。 例如，集成编码器接收来自捕获设备（例如模拟电视调谐器/解码器）的数据流，然后生成编码流。 独立编码器可能会从未压缩的文件接收输入数据、处理数据，然后输出编码数据。

Microsoft 对 DirectX 9.0 和更高版本中基于硬件的音频/视频编码器设备提供支持。

若要支持音频/视频编码器设备，你必须在内核流式处理筛选器微型驱动程序中实现对 Microsoft 定义的编码器属性的支持。 可以通过实现编码器属性，将支持添加到现有 stream 类或 AVStream 微型驱动程序。 或者，如果你正在编写一个新的微型驱动程序（适用于独立编码器或集成的编码器），Microsoft 建议遵循 AVStream 体系结构，因为 stream 类已过时且不再受支持。 你可以使用[AVStream 模拟硬件示例驱动程序（Avshws）](https://go.microsoft.com/fwlink/p/?LinkId=618052)作为起点。 Avshws 驱动程序是实现 DMA 传输支持的以 pin 为中心的 AVStream 示例。

> [!NOTE]
> 如果要编写软件实现的编码器，则不应将其作为内核流式处理筛选器来写入。 相反，此类筛选器应编写为 Microsoft DirectShow 筛选器或 DirectX 媒体对象。 有关基于软件的编码器的详细信息，请参阅 DirectShow SDK 主题 "编码器 API"。

客户端通过[**ICodecAPI**](https://docs.microsoft.com/previous-versions/ms784893(v%3dvs.85)) COM 接口访问编码器功能。 根据微型驱动程序实现的属性，指定 KsProxy 在驱动程序的 INF 文件中公开的接口。 有关 Microsoft 定义的内核流式处理属性和事件的信息，请参阅[编码器实现和支持](encoder-implementation-and-support.md)。 有关如何实现它们的示例，请参阅[编码器代码示例](encoder-code-examples.md)。 有关如何安装编码器筛选器的信息，请参阅[编码器安装和注册](encoder-installation-and-registration.md)，其中包括如何指定 KsProxy 应公开的 COM 接口。

编码器设备必须遵守 Windows 认证计划中所述的流媒体和广播要求，以及涵盖所有设备的一般徽标要求。
