---
title: IEEE 1394 设备的常时等量交谈选项
description: IEEE 1394 设备的常时等量交谈选项
keywords:
- 同步 i/o WDK IEEE 1394 总线，交谈选项
- 交谈选项 WDK IEEE 1394 总线
- 标头 WDK IEEE 1394 总线
- 固定大小的数据数据包 WDK IEEE 1394 总线
- 可变大小的数据数据包 WDK IEEE 1394 总线
- 标头元素 WDK IEEE 1394 总线
- 缓冲 WDK IEEE 1394 总线
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0c19df18af018677a1364fecfabb8531847d6dc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798221"
---
# <a name="isochronous-talk-options-for-ieee-1394-devices"></a>IEEE 1394 设备的常时等量交谈选项





可以通过三种方式来组织同步对话运营中的输出数据：没有标头的数据包、带有标头的固定大小的数据包，以及带有标头的可变大小数据包。

### <a name="packets-with-no-headers"></a>无标头的数据包

默认情况下，主机控制器会按附加缓冲区的顺序在附加缓冲区中发送数据，由 [**ISOCH \_ 描述符**](/windows-hardware/drivers/ddi/1394/ns-1394-_isoch_descriptor)结构的 **Mdl** 成员指示。 在默认情况下，主机控制器会自动将缓冲区拆分为不大于在缓冲区的 ISOCH 描述符结构的 **nMaxBytesPerFrame** 成员中指定的大小的数据包 \_ 。

例如，设备的驱动程序需要在512字节数据包中接收其数据，在其缓冲区的 ISOCH 描述符声明中包括以下 \_ 内容：

```cpp
/* elsewhere, the buffer has declared: */
/*        ISOCH_DESCRIPTOR isoch_descriptor; */
isoch_descriptor->nMaxBytesPerFrame = 512;
```

### <a name="fixed-size-data-packets-with-headers"></a>固定大小的数据包和标头

某些设备要求将一些标头信息附加到设备接收的每个数据包中。  (此标头信息将插入数据之前，但在 IEEE 1394 标准同步数据包标头之后。 ) 在此实例中，驱动程序可以汇编标头的缓冲区和数据缓冲区，并让主机控制器自动为它发送到设备的数据包预置标头。 驱动程序通过 \_ \_ \_ 在该缓冲区的 ISOCH 描述符结构中指定描述符标头散播聚集标志，指示缓冲区包含一个标头列表 \_ 。 有两种类型的标头可附加到数据包：固定大小和可变大小的标头。

对于固定大小的标头，驱动程序在 ISOCH 描述符结构的 **nMaxBytesPerFrame** 成员中指定标头大小 \_ 。 宿主控制器将此缓冲区和下一个缓冲区视为成对：标头缓冲区和数据缓冲区。 当它汇编数据包时，它将从标头缓冲区和数据缓冲区中获取一个帧，并将这些数据包接合在一起以形成发送到设备的下一个数据包。

例如，假设设备需要每个512字节数据缓冲区前面带有8个字节的标头。 驱动程序可以声明一对 ISOCH \_ 描述符结构，如下所示：

```cpp
/* elsewhere, the buffer has declared: */
/*        ISOCH_DESCRIPTOR isoch_descriptor_1, isoch_descriptor_2; */
/*        #define NUM_HEADERS to be the number of headers included in  */
/*        the first buffer */
 
isoch_descriptor_1->fulFlags = DESCRIPTOR_HEADER_SCATTER_GATHER;
isoch_descriptor_1->ulLength = 8 * NUM_HEADERS;
isoch_descriptor_1->nMaxBytesPerFrame = 8;
       .
       .
       .
isoch_descriptor_2->ulLength = 512 * NUM_HEADERS;
isoch_descriptor_2->nMaxBytesPerFrame = 512;
```

并非所有主机控制器都支持描述符 \_ 标头 \_ 散播 \_ 聚集标志。 若要确定主机控制器是否支持此功能，请通过 [**请求 \_ 获取 \_ 本地 \_ 主机 \_ 信息**](https://msdn.microsoft.com/library/windows/hardware/ff537644) 请求查询总线驱动程序，同时 **nLevel** = 获取 \_ 主机 \_ 功能。 总线驱动程序将设置 "主机 \_ 信息 \_ " \_ 支持 \_ \_ 其返回的 "获取 **HostCapabilities** \_ 本地 \_ 主机 INFO2" 结构的 HostCapabilities 成员的 ISO HDR 插入标志 \_ 。

### <a name="variable-size-data-packets-with-headers"></a>带标头的可变大小数据包

这种情况类似于固定大小的数据包大小写。 与固定大小的情况一样，驱动程序必须 \_ \_ \_ 在标头缓冲区的 ISOCH 描述符结构中设置描述符标头散播聚集标志，如下所示 \_ ：

```cpp
isoch_descriptor_1->fulFlags = DESCRIPTOR_HEADER_SCATTER_GATHER;
```

但对于可变大小的情况，驱动程序还必须在 \_ \_ \_ 使用 [**请求 \_ ISOCH \_ 分配 \_ 资源**](https://msdn.microsoft.com/library/windows/hardware/ff537649)请求分配资源时，在 IRB 的 **fulFlags** 成员中设置资源变量 ISOCH 负载标志。

此外，对于可变大小的数据包，驱动程序必须将标头的缓冲区组装为固定大小的大小写。 但是，对于大小可变的数据包，与固定大小的数据包不同，驱动程序必须在每个标头前面加上一个散播/聚集 *标头元素* 中记录每个数据包的大小。

标头元素由在 *1394* 中找到的以下结构定义：

```cpp
typedef struct _IEEE1394_SCATTER_GATHER_HEADER {
  USHORT  HeaderLength;
  USHORT  DataLength;
  UCHAR  HeaderData;
} IEEE1394_SCATTER_GATHER_HEADER, *PIEEE1394_SCATTER_GATHER_HEADER;
```

标头元素指示标头的长度和数据的长度。 因此，对于可变大小的数据包，*数据* 描述符的 **nMaxSizeBytesPerFrame** 成员不再指示单个数据包的大小。 每个数据包的相应标头元素中可能有不同的大小。 *标头* 描述符的 **nMaxSizeBytesPerFrame** 成员的定义如下。

```cpp
IsochDescriptor->nMaxBytesPerFrame = MAX_HEADER_DATA_SIZE+FIELD_OFFSET(HeaderElement,HeaderData)
```

其中，最大 \_ 标头 \_ 数据 \_ 大小指示要预置到每个数据包的标头的大小，字段 \_ 偏移量 (HeaderElement，HeaderData) 指示紧靠在每个标头之前插入的标头元素的长度。

只要驱动程序在 "交谈模式" 下传输可变 **大小的数据包** ，就应该知道个很微妙的定义。 在两种情况下，驱动程序必须定义 **nMaxBytesPerFrame**，并且在这两种情况下，如果驱动程序正在传输大小可变的帧，则主机控制器驱动程序会将分配给 **nMaxBytesPerFrame** 的值解释为 *最小* 帧大小，而不是最大值。

-   在请求 \_ ISOCH \_ 分配 \_ 资源请求期间，驱动程序必须在 [**IRB**](/windows-hardware/drivers/ddi/1394/ns-1394-_irb)的 **nMaxBytesPerFrame** 成员中指定帧大小。

-   在请求 \_ ISOCH \_ 附加 \_ 缓冲区请求期间，驱动程序必须在 [**ISOCH \_ 描述符**](/windows-hardware/drivers/ddi/1394/ns-1394-_isoch_descriptor)的 **nMaxBytesPerFrame** 成员中指定帧大小。

帧越小，主机控制器驱动程序可容纳到传输缓冲区中的帧就越多。 由于每个帧都需要系统资源（例如时间戳和状态信息），因此较小的帧会更快速地消耗系统资源。 主机控制器驱动程序根据 **nMaxBytesPerFrame** 中的值，计算将适合缓冲区的帧数，以及这些帧所需的资源数。 如果帧小于 **nMaxBytesPerFrame** 中指示的大小，则需要资源的帧数将大于主机控制器驱动程序计算的值，这可能会导致错误。

当驱动程序接收数据时，仅当驱动程序在 "交谈模式" 下传输可变大小的帧时，这些注意事项才适用。 当使用 [**请求 \_ ISOCH \_ 分配 \_ 资源**](https://msdn.microsoft.com/library/windows/hardware/ff537649) 请求获取通道的资源句柄时，驱动程序指定与特定通道关联的数据传输类型。 驱动程序在 \_ 此请求过程中将资源变量 \_ ISOCH \_ 负载标记设置为 **fulFlags** ，以指示它将传输大小可变的帧。 驱动程序设置 IsochAllocateResources 中的对话中使用的资源， \_ \_ \_ 以指示它将使用通道传输而不是接收数据。 **u.IsochAllocateResources.fulFlags** 仅当驱动程序在资源分配请求期间设置这两个标志时，主机控制器驱动程序才会将 **nMaxBytesPerFrame** 解释为最小值，而不是最大值。

请注意， [**IRB**](/windows-hardware/drivers/ddi/1394/ns-1394-_irb)的 **IsochAllocateResources. nMaxBufferSize** 成员始终是最大值。

驱动程序现在只能通过将标头元素的 **DataLength** 成员设置为零来传输仅标头的数据包：

```cpp
HeaderElement->DataLength = 0
```

标头描述符缓冲区的总长度是通过描述符的 **ulLength** 成员通常的方式来表示的。 它必须是标头散点/集合元素数的整数倍：

```cpp
IsochDescriptor->ulLength = IsochDescriptor->nMaxBytesPerFrame * NUMBER_OF_PACKETS;
```

其中， \_ \_ 数据包数是要传输的数据包数目 (包括仅限标头的数据包) 。

标头元素结构 **HeaderData** 的第三个成员只是一个占位符，用于指示标头数据的开始位置。 下图演示了8字节 CIP 标头的已汇编缓冲区的示例。

![阐释8字节 cip 标头的缓冲区的关系图](images/hdrelem.png)

给定说明符中的所有标头必须具有相同的长度。 这允许 OHCI 端口驱动程序 (*ohci1394.sys*) 分析标头说明符，如固定大小元素数组。 数据包的大小可能不同，但必须是连续的，没有 "洞"。

标头和数据描述符中的数据都必须是页对齐的。 数据包的大小不受限制，但不允许标头和数据数据包跨页面边界。 *在为缓冲区设置 MDL 之前，* 驱动程序必须正确对齐描述符缓冲区。

例如，如果驱动程序汇编了包含12个字节的标头和4个字节的标头元素的标头描述符，则每个数据包将具有16字节的预置数据。 因为16个字节的页256恰好适合4096个字节，所以任何预置数据都不会跨越页面边界。

另一方面，如果驱动程序装配带有8个字节的标头和4个字节的标头元素的标头描述符，则每个数据包的预置数据将包含12个字节。 由于4096字节页不是12的整数倍数，因此标头描述符的大小必须小于4096字节，以防止标头跨越页面边界。 但是，可以通过调整缓冲区的基址（如以下伪代码中所示），将标头描述符缓冲区的大小扩展到两页。

```cpp
// First find the number of headers (together with header elements)
// that will fit in a page. Use a floor function that rounds down to 
// the nearest integer
PrependData = sizeof(header) + 8; // First two fields of header element take up 8 bytes
NumHeaders =floor(PAGE_SIZE/PrependData);
// By forcing the buffer address defined in the MDL to begin at the appropriate offset,
// the driver can guarantee that the last header in the buffer will be aligned on a page 
// boundary. That way, DMA can continue across at least one page boundary.
r = PAGE_SIZE - (NumHeaders*12).
// BufferAddress = the page-aligned address returned by a memory allocation routine
// Adjust buffer starting address
BufferAddress += r;
isochDescriptor->mdl = IoAllocateMdl(BufferAddress, ... and so on.)
```

 

