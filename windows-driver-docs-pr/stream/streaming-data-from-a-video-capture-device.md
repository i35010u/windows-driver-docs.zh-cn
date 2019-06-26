---
title: 来自视频捕获设备的流式处理数据
description: 来自视频捕获设备的流式处理数据
ms.assetid: c83aae8e-70a7-4d65-a888-00a7c21eebdd
keywords:
- 视频捕获 WDK AVStream 中的流数据
- 捕获视频 WDK AVStream 中的流数据
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51b7590555c13416f0767a4b9a9f1e2cccfcfb14
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377786"
---
# <a name="streaming-data-from-a-video-capture-device"></a>来自视频捕获设备的流式处理数据


视频流组成加盖时间戳和数字化视频和相关信息，如垂直遮蔽的间隔 (VBI) 数据和时间码。 流可以暂停、 启动，并且独立于另一个已停止。 Stream 示例都是时间戳与 100 毫微秒解析时钟。

视频捕获微型驱动程序可以支持多个，同时发生的压缩和未压缩视频，时间码，流关闭字幕，原始并解码 VBI 数据和自定义数据格式。 微型驱动程序应使用其他数据类型同时创建可生成每个数据类型的新流。 AVStream 或 Stream 类接口公开单独为每个新的流 pin。 这些引脚 KsProxy 被镜像，并显示在用户模式下作为 Microsoft DirectShow 筛选器。 DirectShow 筛选器不 WDM 筛选器驱动程序。 有关插针和流式处理的详细信息，请参阅[内核流式处理](kernel-streaming.md)。

每个视频流式处理 pin 可以支持各种不同的数据格式。 例如，单个插针程序支持 RGB16、 RGB24、 YUV9 和 JPEG 数字视频。 大多数设备都支持只有几个这些格式。 有关详细信息流格式和指定一系列支持的格式，请参见[指定 Stream 格式](specifying-stream-formats.md)。

### <a name="vertical-blanking-interval-vbi-data"></a>垂直消隐功能数据间隔 (VBI)

捕获设备捕获垂直遮蔽的间隔 (VBI) 流时, 应提供原始的、 undecoded VBI 示例，以便下游的筛选器和编解码器可以提取隐藏字幕 (CC)、 North American 广播 Teletext 标准 (NABTS)、 Teletext，和从原始样本其他专用数据。

VBI 解码器必须立即通知的优化的更改。 例如，调谐器间切换时从一个通道，VBI 解码器必须通知优化操作的开始处以便它可以暂时停止信号不稳定的期间进行解码。 优化操作完成后，VBI 解码器必须通知新频道和视频的任何标准或可能已发生的国家/地区代码更改。

通过纵横制筛选器，然后再转换其捕获筛选器上的模拟视频输入 pin，微型驱动程序必须将传播其调谐器的筛选器，从优化数据包。 此数据包是仅在用户模式下可用，直到它达到捕获筛选器。 微型驱动程序收到与此优化数据包[ **KS\_TVTUNER\_更改\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagks_tvtuner_change_info)上的模拟视频输入插针微型驱动程序的捕获的结构筛选器。

微型驱动程序还必须将传播到 VBI 输出插针，其捕获筛选器使用的优化数据包[视频流扩展标头](video-stream-extended-headers.md)。 充当链 VBI 解码器同样必须传播到其输出插针从其输入插针扩展标头信息。

 

 




