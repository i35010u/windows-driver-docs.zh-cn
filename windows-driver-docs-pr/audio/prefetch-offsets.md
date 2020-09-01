---
title: 预提取偏移量
description: 预提取偏移量
ms.assetid: 92a0163f-29b1-4e15-88ab-67e1097d015e
keywords:
- 硬件加速 WDK DirectSound，预提取偏移量
- 预提取偏移 WDK 音频
- 写入光标偏移 WDK 音频
- 播放光标偏移 WDK 音频
- 偏移 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ee6615fcf1a221035886da17755d2a5dd9defac
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210453"
---
# <a name="prefetch-offsets"></a>预提取偏移量


## <span id="prefetch_offsets"></span><span id="PREFETCH_OFFSETS"></span>


WavePci 微型端口驱动程序调用 [**IPreFetchOffset：： SetPreFetchOffset**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iprefetchoffset-setprefetchoffset) 方法，以指定硬件加速 DirectSound 输出流的预提取偏移量。 此偏移量是在音频设备硬件缓冲区中将写入游标与播放光标分隔的数据字节数。 写入游标指定 DirectSound 应用程序可在其中安全写入下一个声音示例的缓冲区位置。 播放光标指定音频设备当前正在播放的声音示例的缓冲区位置。

DirectSound 通过发送 [**KSPROPERTY \_ 音频 \_ 位置**](./ksproperty-audio-position.md) 属性请求，在 WavePci 端口驱动程序中查询播放和写入游标的当前位置。 为响应此请求，端口驱动程序通过调用 [**IMiniportWavePciStream：： GetPosition**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepcistream-getposition)从微型端口驱动程序获取当前播放位置。 端口驱动程序如何确定写入位置取决于是否调用了 [**SetPreFetchOffset**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iprefetchoffset-setprefetchoffset) 。

默认情况下，端口驱动程序将写入光标置于微型端口驱动程序请求的最后一个映射中。 每次调用 [**IPortWavePciStream：： GetMapping**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavepcistream-getmapping)时，默认的预提取偏移量会增大。 如果 WavePci 微型端口驱动程序获取大量映射，则默认偏移量可能会变得非常大。

调用 [**SetPreFetchOffset**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iprefetchoffset-setprefetchoffset) 将重写默认值。 在此调用之后，端口驱动程序会通过将指定的预取偏移量添加到播放位置，来计算写入位置， (会考虑 DirectSound 缓冲区末尾) 的环绕。

小型端口驱动程序可能会出于以下几个原因分配大量映射。 一种是降低系统处理器上音频操作的开销。 对于更多映射，驱动程序需要较少的中断以使音频设备持续与数据一起提供。 另一个原因是，如果在很短的时间内设备驱动程序的设备驱动程序不正常，则分配更多的映射会降低音频播放面临的难题。

较大的预提取偏移量存在一个问题，即一些 DirectSound 应用程序可能会对播放和写入游标的相对位置感到困惑。 在 Windows 95/98 中，音频 Vxd 保持相对较小的预取偏移量，如果偏移量大于预期大小，则为这些操作系统编写的 DirectSound 应用程序可能无法正常运行。

例如，应用程序可能将 DirectSound 缓冲区分为上半部分和下半部分，然后在应用程序和设备之间进行两次 "ping"。 当写入游标第一次进入缓冲区的上半或后半部分时，它会将一半缓冲区的数据写入到缓冲区的一半。 此方案假定播放光标始终定位于缓冲区的另一半（即未写入的一半）。 请注意，如果预提取偏移量超过缓冲区大小的一半，则此假设不正确。 在这种情况下，当写入光标到达 DirectSound 缓冲区的末尾并环绕缓冲区的开头时，它将与播放光标处于缓冲区的一半。 当应用程序将一半缓冲区的数据写入新的写入游标位置时，最终将覆盖播放光标位置并销毁尚未播放的数据。

尽管应用程序本身对于这种类型的故障是怪的，但 WavePci 微型端口驱动程序只需调用 [**SetPreFetchOffset**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iprefetchoffset-setprefetchoffset) 将预提取偏移设置为较小的值即可消除故障模式。

将预提取偏移量设置为较小的值会使生成的写入光标接近于播放光标。 应将预提取偏移量设置为硬件的 FIFO 大小。 典型的预提取偏移量大约为64示例，具体取决于 DMA 引擎的硬件设计。

为了保持与某些较旧的 DirectSound 应用程序的兼容性，DirectSound 当前将硬件加速 pin 的写入游标填充10毫秒。 请注意，填充量将来可能会更改。

有关在驱动程序级别管理写入游标和播放游标的其他信息，请参阅 [音频位置属性](audio-position-property.md)。

 

