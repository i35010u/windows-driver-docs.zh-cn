---
title: 来自视频捕获设备的流式处理数据
description: 来自视频捕获设备的流式处理数据
ms.assetid: c83aae8e-70a7-4d65-a888-00a7c21eebdd
keywords:
- 视频捕获 WDK AVStream，流式传输数据
- 捕获视频 WDK AVStream，从流式传输数据
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7227a9863360683a709cc3bf664e40b197ffcbb
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185531"
---
# <a name="streaming-data-from-a-video-capture-device"></a>来自视频捕获设备的流式处理数据


视频流由带时间戳的数字视频和相关信息组成，如垂直消隐间隔 (VBI) 数据和时间码。 流可以暂停、启动和彼此独立地停止。 流示例采用100毫微秒分辨率时钟的时间戳。

视频捕获微型驱动程序可以支持多个同时流的压缩和未压缩视频、时间码、隐藏式字幕、原始和解码的 VBI 数据以及自定义数据格式。 对于可以同时与其他数据类型一起生成的每个数据类型，微型驱动程序应创建一个新的流。 AVStream 或 Stream 类接口为每个新流公开单独的 pin。 这些 pin 由 KsProxy 镜像，以用户模式显示为 Microsoft DirectShow 筛选器。 DirectShow 筛选器不是 WDM 筛选器驱动程序。 有关 pin 和流式处理的详细信息，请参阅 [内核流式处理](kernel-streaming.md)。

每个视频流式处理 pin 都可以支持多种不同的数据格式。 例如，单个 pin 可支持 RGB16、RGB24、YUV9 和 JPEG 数字视频。 大多数设备仅支持其中几种格式。 有关流格式和指定一系列受支持格式的详细信息，请参阅 [指定流格式](specifying-stream-formats.md)。

### <a name="vertical-blanking-interval-vbi-data"></a>垂直消隐间隔 (VBI) 数据

捕获垂直消隐间隔 (VBI) 流时，捕获设备应提供 raw、undecoded VBI 示例，以便下游筛选器和编解码器可以从原始示例中 (CC) 、北美广播 Teletext Standard (NABTS) 、Teletext 和其他专有数据提取隐藏式字幕。

必须立即向 VBI 解码器通知优化更改。 例如，当调谐器从一个通道切换到另一个通道时，必须在优化操作开始时通知 VBI 解码器，以便在信号不稳定期间暂时停止解码。 优化操作完成后，必须向 VBI 解码器通知新通道，以及可能已发生的任何视频标准或国家/地区代码更改。

微型驱动程序必须在其调谐器筛选器中传播调谐包，通过纵横比筛选器，然后再传播到捕获筛选器上的模拟视频输入插针。 此数据包仅在用户模式下可用，直到达到捕获筛选器。 微型驱动程序在微型驱动程序的捕获筛选器的模拟视频输入插针上收到此优化数据包作为 [**KS \_ TVTUNER \_ 更改 \_ 信息**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_tvtuner_change_info) 结构。

微型驱动程序还必须使用 [视频流扩展标头](video-stream-extended-headers.md)将优化数据包传播到其捕获筛选器的 VBI 输出插针。 作为链操作的 VBI 解码器必须同样将扩展标头信息从其输入插针传播到其输出插针。

 

