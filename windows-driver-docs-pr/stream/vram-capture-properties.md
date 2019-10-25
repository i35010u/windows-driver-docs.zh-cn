---
title: VRAM 捕获属性
description: VRAM 捕获属性
ms.assetid: e3ab3a10-42af-488f-9b13-d2c6d5aac615
keywords:
- VRAM 捕获 WDK AVStream，属性
- 捕获到系统内存 WDK AVStream
- 固定 VRAM 处理 WDK AVStream
- VRAM 捕获 WDK AVStream，请求序列
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4ec43e1ea3bf5a577fc0d6906b085011c6cc9798
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845276"
---
# <a name="vram-capture-properties"></a>VRAM 捕获属性


以 pin 为中心的 AVStream 微型驱动程序必须支持多个属性才能捕获到 VRAM。 本部分介绍微型驱动程序在 VRAM 处理前后接收的请求序列。

在启动捕获之前，KS 代理会发送[**KSPROPERTY\_首选\_捕获\_SURFACE**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-preferred-capture-surface) get 属性请求。 微型驱动程序应返回不同的值，具体取决于驱动程序是否正在捕获到系统内存或 VRAM。

### <a name="capturing-to-system-memory"></a>捕获到系统内存

若要捕获到系统内存，请返回 KS\_捕获\_分配\_系统\_AGP。

然后，捕获驱动程序使用系统内存值类型接收[ **\_当前\_捕获\_面**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-current-capture-surface)集属性请求。 捕获驱动程序现在充当主线主机 DMA 设备，并将数据直接放入系统内存。

在此模式下，捕获驱动程序接收输出插针的[*AVStrMiniPinProcess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspin)回调函数中的系统内存缓冲区。

有关如何在 pin 进程回拨中实现 DMA 的信息，请参阅[AVStream 中的基于数据包的 DMA](packet-based-dma-in-avstream.md)。

若要捕获多个输出插针（例如，单独的视频、音频和 VBI 的 pin），每个 pin 应支持 VRAM 属性和处理（如前文所述）。 代理为每个 pin 生成一个单独的线程。

### <a name="capturing-to-vram"></a>捕获到 VRAM

如果驱动程序支持 VRAM 捕获，请返回**KS\_捕获\_分配\_VRAM**以响应 KSPROPERTY\_首选\_捕获\_图面。

接下来，微型驱动程序将收到[**KSPROPERTY\_显示\_适配器\_guid**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-display-adapter-guid)请求，并查询显示适配器的 GUID。

从供应商提供的图形微型端口驱动程序获取适配器 GUID。 [**DXGK\_INTERFACESPECIFICDATA**](https://docs.microsoft.com/windows-hardware/drivers/display/dxgk-interfacespecificdata)结构包含要在属性请求中返回的适配器 GUID。 此结构由 DirectX 图形内核（DXGK）子系统生成，在适配器初始化时传递给微型端口驱动程序。

如果 pin 支持 VRAM 传输以及显示适配器和下游筛选器匹配的 Guid，则选择 "KS 代理" 模块作为分配器。 代理通过将[**KSPROPERTY\_当前\_捕获\_surface**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-current-capture-surface)属性设置为捕获的所选表面类型，来通知捕获插针选择了 pin 间的 VRAM surface 传输。

如果 pin 接收到 KS\_捕获\_分配\_VRAM，则它将接收 VRAM 处理请求。

VRAM 处理请求由两部分组成。 首先，捕获驱动程序接收[**KSPROPERTY\_MAP 的 get 请求\_捕获\_处理\_到\_VRAM\_ADDRESS**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-map-capture-handle-to-vram-address)。 Get 处理程序接收 IRP，其中包含内核模式 VRAM surface 控点。

捕获驱动程序或显示微型端口驱动程序应将 VRAM surface 控点映射到实际的 VRAM 物理地址。 VRAM surface 控点*不能保持有效; 请勿*将其缓存供以后使用。

返回在属性请求中提供的[**VRAM\_SURFACE\_INFO\_属性\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-vram_surface_info_property_s)中的映射地址。 捕获驱动程序可以发出 IOCTL，请求从显示微型端口驱动程序中进行映射。

其次，当 pin 包含要处理的数据时，将调用捕获筛选器的*AVStrMiniPinProcess* 。

微型驱动程序现在应调用[**KsPinGetLeadingEdgeStreamPointer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kspingetleadingedgestreampointer)来获取和锁定此 pin 的主要边缘流指针。 此函数返回指向[**KSSTREAM\_指针**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksstream_pointer)结构的指针。

此流指针结构包含指向[**KSSTREAM\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_header)的指针。

在流标头的**数据**成员中，查找指向[**VRAM\_SURFACE\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-vram_surface_info)结构的指针。

此结构包含为响应 KSPROPERTY\_映射而返回的物理地址\_捕获\_处理\_到\_VRAM\_地址。 表示句柄的**hSurface**成员为**NULL**。

捕获驱动程序应：

-   用 VRAM 物理地址对捕获硬件进行编程。

-   处理视频帧完成。

-   用复制到 VRAM 图面中的字节数填写 VRAM\_SURFACE\_信息的**cbCaptured**成员。 不要将\_KSSTREAM 的**DataUsed**成员设置为已捕获的字节数。 相反，请将**DataUsed**设置为 SIZEOF （VRAM\_SURFACE\_INFO）。

-   如果捕获驱动程序执行时间戳，请设置**PresentationTime**、 **Duration**，如果相关，请在 KSSTREAM 中的**OptionsFlags**\_标头。

-   调用[**KsStreamPointerAdvanceOffsets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointeradvanceoffsets)以继续处理或删除所有克隆，并通过调用[**KsStreamPointerDelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerdelete)来完成请求。

Windows 驱动程序工具包（WDK）*示例中* [AVStream 模拟硬件示例驱动程序（AVSHwS）](https://go.microsoft.com/fwlink/p/?linkid=256083)的 rocessd3dsurface 中的**CCapturePin：:P**方法显示了实现此回调以实现 VRAM 支持的一种方法。

 

 




