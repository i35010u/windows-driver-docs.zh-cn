---
title: VRAM 捕获属性
description: VRAM 捕获属性
ms.assetid: e3ab3a10-42af-488f-9b13-d2c6d5aac615
keywords:
- Vram 能够捕获 WDK AVStream，属性
- 捕获到系统内存 WDK AVStream
- pin vram 能够处理 WDK AVStream
- Vram 能够捕获 WDK AVStream，请求序列
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: edffc83e3dcc43882a60b55b1bcd4bfc183a89ac
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385360"
---
# <a name="vram-capture-properties"></a>VRAM 捕获属性


Pin 为中心的 AVStream 微型驱动程序必须以使其捕获到 vram 能够支持多个属性。 本部分介绍微型驱动程序接收之前和过程 vram 能够处理的请求的序列。

启动捕获之前，KS 代理将发送[ **KSPROPERTY\_PREFERRED\_捕获\_图面**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-preferred-capture-surface) get 属性请求。 微型驱动程序应返回不同的值，具体取决于是否为系统内存或 vram 能够捕获驱动程序。

### <a name="capturing-to-system-memory"></a>捕获到系统内存

若要捕获到系统内存，请返回 KS\_捕获\_ALLOC\_系统\_AGP。

捕获驱动程序然后接收[ **KSPROPERTY\_当前\_捕获\_图面**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-current-capture-surface)设置属性使用系统内存值类型的请求。 捕获驱动程序现在充当主总线 DMA 设备并直接将数据置于系统内存。

在此模式下，捕获驱动程序收到系统中的内存缓冲区[ *AVStrMiniPinProcess* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnkspin)回调函数的输出插针。

有关如何在您的 pin 进程回调中实现 DMA 的信息，请参阅[AVStream 中基于数据包的 DMA](packet-based-dma-in-avstream.md)。

若要捕获与多个输出插针 （例如，单独的视频、 音频和 VBI pin），每个 pin 应支持的 vram 能够属性和处理如前面所述。 代理生成一个单独的线程，对于每个插针。

### <a name="capturing-to-vram"></a>向 vram 能够捕获

如果您的驱动程序支持 vram 能够捕获，则返回**KS\_捕获\_ALLOC\_vram 能够**响应 KSPROPERTY\_首选\_捕获\_图面。

接下来，微型驱动程序收到[ **KSPROPERTY\_显示\_适配器\_GUID** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-display-adapter-guid)属性 get 请求，查询显示适配器的 GUID。

获取从供应商提供图形微型端口驱动程序的适配器 GUID。 [ **DXGK\_INTERFACESPECIFICDATA** ](https://docs.microsoft.com/windows-hardware/drivers/display/dxgk-interfacespecificdata)结构包含适配器属性请求中返回的 GUID。 此结构生成的 DirectX 图形内核 (DXGK) 子系统，该适配器初始化时传递给微型端口驱动程序。

如果 pin 支持 vram 能够传输和显示适配器和下游的筛选器匹配的 Guid，KS 代理模块被选作分配器。 代理通知有关的 vram 能够通过设置 pin 之间的图面上传输选择捕获 pin [ **KSPROPERTY\_当前\_捕获\_图面**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-current-capture-surface)具有用于捕获图面上选定类型的属性。

如果 pin 收到 KS\_捕获\_ALLOC\_vram 能够，它随后会收到 vram 能够处理请求。

Vram 能够处理请求由两个部分组成。 首先，捕获驱动程序收到的 get 请求[ **KSPROPERTY\_地图\_捕获\_处理\_TO\_vram 能够\_地址**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-map-capture-handle-to-vram-address). Get 处理程序接收 IRP，包含内核模式 vram 能够图面上句柄。

捕获驱动程序或显示微型端口驱动程序应映射到实际的 vram 能够物理地址的 vram 能够图面上的句柄。 Vram 能够图面上的句柄*does 不保持有效; 不这样做*缓存以供将来使用。

返回在映射的地址[ **vram 能够\_面\_信息\_属性\_S** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-vram_surface_info_property_s)属性请求中提供。 捕获驱动程序可以发出 IOCTL 显示微型端口驱动程序从请求该映射。

第二个，捕获筛选器*AVStrMiniPinProcess* pin 必须要处理的数据时调用。

应立即调用微型驱动程序[ **KsPinGetLeadingEdgeStreamPointer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-kspingetleadingedgestreampointer)来获取和锁定此 pin 的前边缘流指针。 此函数返回一个指向[ **KSSTREAM\_指针**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksstream_pointer)结构。

此流指针结构包含一个指向[ **KSSTREAM\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksstream_header)。

在中**数据**流标头的成员查找指向的指针[ **vram 能够\_图面\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-vram_surface_info)结构。

此结构包含 KSPROPERTY 响应中返回的物理地址\_地图\_捕获\_处理\_TO\_vram 能够\_地址。 **HSurface**表示句柄的成员是**NULL**。

应该捕获驱动程序：

-   编程捕获硬件的 vram 能够物理地址。

-   处理视频帧完成。

-   填写**cbCaptured**成员的 vram 能够\_面\_字节数的信息复制到的 vram 能够图面。 未设置**DataUsed** KSSTREAM 成员\_标头以及捕获的字节数。 与此相反，设置**DataUsed**到 sizeof (vram 能够\_面\_信息)。

-   如果您捕获的驱动程序执行时间戳，设置**PresentationTime**，**持续时间**，并且，如果相关， **OptionsFlags**中 KSSTREAM\_标头。

-   调用[ **KsStreamPointerAdvanceOffsets** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointeradvanceoffsets)若要继续处理，或删除所有克隆，完成请求，通过调用[ **KsStreamPointerDelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerdelete).

**CCapturePin::ProcessD3DSurface**中的方法*Capture.cpp*的[AVStream 模拟硬件示例驱动程序 (AVSHwS)](https://go.microsoft.com/fwlink/p/?linkid=256083)中的 Windows Driver Kit (WDK) 示例演示一种方式实现 vram 能够支持此回调。

 

 




