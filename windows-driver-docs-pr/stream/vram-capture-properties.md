---
title: VRAM 捕获属性
description: VRAM 捕获属性
keywords:
- VRAM 捕获 WDK AVStream，属性
- 捕获到系统内存 WDK AVStream
- 固定 VRAM 处理 WDK AVStream
- VRAM 捕获 WDK AVStream，请求序列
ms.date: 06/19/2020
ms.localizationpriority: medium
ms.openlocfilehash: 0bde46be75b8b5a15e25d3d0bfb25107771c60f1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791070"
---
# <a name="vram-capture-properties"></a>VRAM 捕获属性

以 pin 为中心的 AVStream 微型驱动程序必须支持多个属性才能捕获到 VRAM。 本部分介绍微型驱动程序在 VRAM 处理前后接收的请求序列。

在启动捕获之前，KS 代理会发送 [**KSPROPERTY \_ 首选 \_ 捕获 \_ SURFACE**](./ksproperty-preferred-capture-surface.md) get 属性请求。 微型驱动程序应返回不同的值，具体取决于驱动程序是否正在捕获到系统内存或 VRAM。

## <a name="capturing-to-system-memory"></a>捕获到系统内存

若要捕获到系统内存，请返回 KS \_ 捕获 \_ 分配 \_ 系统 \_ AGP。

捕获驱动程序随后接收具有系统内存值类型的 [**KSPROPERTY \_ 当前 \_ 捕获 \_ SURFACE**](./ksproperty-current-capture-surface.md) set 属性请求。 捕获驱动程序现在充当主线主机 DMA 设备，并将数据直接放入系统内存。

在此模式下，捕获驱动程序接收输出插针的 [*AVStrMiniPinProcess*](/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspin) 回调函数中的系统内存缓冲区。

有关如何在 pin 进程回拨中实现 DMA 的信息，请参阅 [AVStream 中的基于数据包的 DMA](packet-based-dma-in-avstream.md)。

若要捕获多个输出插针 (例如，单独的视频、音频和 VBI 针) ，每个 pin 应支持 VRAM 属性和处理，如前文所述。 代理为每个 pin 生成一个单独的线程。

## <a name="capturing-to-vram"></a>捕获到 VRAM

如果驱动程序支持 VRAM 捕获，请返回 **KS \_ 捕获 \_ 分配 \_ VRAM** 以响应 KSPROPERTY \_ 首选 \_ 捕获 \_ 面。

接下来，微型驱动程序将收到 [**KSPROPERTY \_ 显示 \_ 适配器 \_ guid**](./ksproperty-display-adapter-guid.md) get 属性请求，并查询显示适配器的 GUID。

从供应商提供的图形微型端口驱动程序获取适配器 GUID。 [**DXGK \_ INTERFACESPECIFICDATA**](../display/dxgk-interfacespecificdata.md)结构包含要在属性请求中返回的适配器 GUID。 此结构由 DirectX 图形内核 (DXGK) 子系统生成，在适配器初始化时传递给微型端口驱动程序。

如果 pin 支持 VRAM 传输以及显示适配器和下游筛选器匹配的 Guid，则选择 "KS 代理" 模块作为分配器。 代理通过使用所选的 "捕获" 表面类型设置 " [**KSPROPERTY \_ 当前 \_ 捕获 \_ 面**](./ksproperty-current-capture-surface.md) " 属性，在 pin 之间通知捕获插针选择 VRAM surface transport。

如果 pin 接收到 KS \_ 捕获 \_ 分配 \_ VRAM，它将接收 VRAM 处理请求。

VRAM 处理请求由两部分组成。 首先，捕获驱动程序接收 [**KSPROPERTY \_ 映射 \_ 捕获 \_ 句柄 \_ 到 \_ VRAM \_ 地址**](./ksproperty-map-capture-handle-to-vram-address.md)的 get 请求。 Get 处理程序接收 IRP，其中包含内核模式 VRAM surface 控点。

捕获驱动程序或显示微型端口驱动程序应将 VRAM surface 控点映射到实际的 VRAM 物理地址。 VRAM surface 控点 *不能保持有效; 请勿* 将其缓存供以后使用。

返回在属性请求中提供的 [**VRAM \_ SURFACE \_ INFO \_ 属性 \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-vram_surface_info_property_s) 中的映射地址。 捕获驱动程序可以发出 IOCTL，请求从显示微型端口驱动程序中进行映射。

其次，当 pin 包含要处理的数据时，将调用捕获筛选器的 *AVStrMiniPinProcess* 。

微型驱动程序现在应调用 [**KsPinGetLeadingEdgeStreamPointer**](/windows-hardware/drivers/ddi/ks/nf-ks-kspingetleadingedgestreampointer) 来获取和锁定此 pin 的主要边缘流指针。 此函数返回指向 [**KSSTREAM \_ 指针**](/windows-hardware/drivers/ddi/ks/ns-ks-_ksstream_pointer) 结构的指针。

此流指针结构包含指向 [**KSSTREAM \_ 标头**](/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_header)的指针。

在流标头的 **数据** 成员中，查找指向 [**VRAM \_ SURFACE \_ INFO**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-vram_surface_info) 结构的指针。

此结构包含为响应 \_ VRAM 地址的 KSPROPERTY 映射 \_ 捕获 \_ 句柄而 \_ \_ 返回的 \_ 物理地址。 表示句柄的 **hSurface** 成员为 **NULL**。

捕获驱动程序应：

- 用 VRAM 物理地址对捕获硬件进行编程。

- 处理视频帧完成。

- **cbCaptured** \_ \_ 用复制到 VRAM 图面中的字节数填写 VRAM SURFACE INFO 的 cbCaptured 成员。 不要将 KSSTREAM 标头的 **DataUsed** 成员设置为已 \_ 捕获的字节数。 相反，请将 **DataUsed** 设置为 SIZEOF (VRAM \_ SURFACE \_ INFO) 。

- 如果捕获驱动程序执行了时间戳，请在 KSSTREAM 标头中设置 **PresentationTime**、 **Duration** 和（如果相关） **OptionsFlags** \_ 。

- 调用 [**KsStreamPointerAdvanceOffsets**](/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointeradvanceoffsets) 以继续处理或删除所有克隆，并通过调用 [**KsStreamPointerDelete**](/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerdelete)来完成请求。

Windows 驱动程序工具包 (WDK) 示例 *中的 rocessd3dsurface 文件中* 的 **CCapturePin：:P** 方法在 Windows 驱动程序工具包中的 [AVStream 模拟硬件示例驱动程序 (AVSHwS)](/samples/microsoft/windows-driver-samples/avstream-simulated-hardware-sample-driver-avshws)显示了实现此回调以实现 VRAM 支持的一种方法。
