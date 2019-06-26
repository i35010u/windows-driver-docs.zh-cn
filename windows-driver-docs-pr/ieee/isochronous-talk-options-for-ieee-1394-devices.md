---
title: IEEE 1394 设备的常时等量交谈选项
description: IEEE 1394 设备的常时等量交谈选项
ms.assetid: b3df5dd5-9903-48b4-9cb2-17b8d3a08f8f
keywords:
- 同步 I/O WDK IEEE 1394 总线，讨论选项
- 通信选项 WDK IEEE 1394 总线
- 标头 WDK IEEE 1394 总线
- 固定大小的数据数据包 WDK IEEE 1394 总线
- 大小可变的数据数据包 WDK IEEE 1394 总线
- 标头元素 WDK IEEE 1394 总线
- 缓冲区 WDK IEEE 1394 总线
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 12ac524be304111e23ac2964158d3662ed58e498
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385761"
---
# <a name="isochronous-talk-options-for-ieee-1394-devices"></a>IEEE 1394 设备的常时等量交谈选项





有三种方法的组织中等时讨论操作的输出数据： 没有标头、 固定大小的数据的数据包，其中标头和变量大小的数据的数据包，其中标头的数据包。

### <a name="packets-with-no-headers"></a>没有标头的数据包

默认情况下，主控制器发出的附加缓冲区中的数据由**Mdl**的成员[ **ISOCH\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/1394/ns-1394-_isoch_descriptor)结构，在缓冲区已附加的顺序。 默认情况下，主控制器自动拆分缓冲区大小的数据包不应超过中指定的**nMaxBytesPerFrame**成员的缓冲区的 ISOCH\_描述符结构。

例如，将要在 512 字节的数据包中接收其数据的设备的驱动程序将缓冲区的 ISOCH 其声明中包括以下\_描述符：

```cpp
/* elsewhere, the buffer has declared: */
/*        ISOCH_DESCRIPTOR isoch_descriptor; */
isoch_descriptor->nMaxBytesPerFrame = 512;
```

### <a name="fixed-size-data-packets-with-headers"></a>固定大小的数据的数据包，其中标头

某些设备需要某些标头信息将附加到每个设备接收的数据包。 （之前数据，但之后的 IEEE 1394 标准同步数据包标头，将插入此标头信息。）在此情况下，驱动程序可以组合的标头，缓冲区和缓冲区的数据，并且可以自动在前面添加的标头的数据包将发送到设备的主机控制器。 该驱动程序指示缓冲区包含标头的列表，通过指定描述符\_标头\_散点图\_收集标志中该缓冲区 ISOCH\_描述符结构。 有两种类型的可附加到一个数据包的标头： 固定大小且大小可变的。

具有固定大小标头，该驱动程序指定的标头大小**nMaxBytesPerFrame** ISOCH 成员\_描述符结构。 主控制器将作为对中处理此缓冲区的下一个缓冲区： 标头缓冲区和数据缓冲区。 当会汇集的数据包时，它从数据缓冲区将标头缓冲区中的一个框架和一个框架，并拼接它们一起以形成它向设备发送的下一个数据包。

例如，假设设备要求每个 512 字节的数据缓冲区，前面加上 8 个字节标头。 该驱动程序可以声明一对 ISOCH\_描述符结构，如下所示：

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

并非所有主机控制器都支持描述符\_标头\_散点图\_收集标志。 若要确定主机控制器支持它，请查询使用总线驱动程序[**请求\_获取\_本地\_主机\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff537644)请求，使用**nLevel** = GET\_主机\_功能。 总线驱动程序将设置主机\_INFO\_支持\_ISO\_HDR\_插入标志**HostCapabilities**的 GET 成员\_本地\_主机\_INFO2 结构，它返回。

### <a name="variable-size-data-packets-with-headers"></a>大小可变的数据的数据包，其中标头

这种情况下是类似于固定大小的数据包方案。 正如一样固定大小的情况下，该驱动程序必须设置描述符\_标头\_散点图\_中的标头缓冲区 ISOCH 收集标志\_描述符结构，如下所示：

```cpp
isoch_descriptor_1->fulFlags = DESCRIPTOR_HEADER_SCATTER_GATHER;
```

对于可变大小的情况，该驱动程序还必须设置资源，但是\_变量\_ISOCH\_中的有效负载标志**u.IsochAllocateResources.fulFlags** IRB 时它会分配的成员使用资源[**请求\_ISOCH\_分配\_资源**](https://msdn.microsoft.com/library/windows/hardware/ff537649)请求。

此外，在大小可变的数据包的情况下，驱动程序必须组合标头，如固定大小的缓冲区。 但是，与可变大小的数据包，与不同的固定大小的数据包，驱动程序必须记录每个数据包的大小中分散/聚拢*标头元素*它前添加到每个标头。

标头元素定义由以下结构中找到*1394.h*:

```cpp
typedef struct _IEEE1394_SCATTER_GATHER_HEADER {
  USHORT  HeaderLength;
  USHORT  DataLength;
  UCHAR  HeaderData;
} IEEE1394_SCATTER_GATHER_HEADER, *PIEEE1394_SCATTER_GATHER_HEADER;
```

标头元素指示标头的长度和数据的长度。 因此，与可变大小数据包**nMaxSizeBytesPerFrame**的成员*数据*描述符不再指示单个数据包的大小。 每个数据包可以具有不同的大小及其相应的标头元素中所示。 **NMaxSizeBytesPerFrame**的成员*标头*描述符定义，如下所示。

```cpp
IsochDescriptor->nMaxBytesPerFrame = MAX_HEADER_DATA_SIZE+FIELD_OFFSET(HeaderElement,HeaderData)
```

其中最大\_标头\_数据\_大小指示要附加到每个数据包和字段的标头大小\_OFFSET(HeaderElement,HeaderData) 指示插入的标头元素的长度之前每个标头。

应注意的方面的定义微妙的地方**nMaxBytesPerFrame**每当您的驱动程序正在传输"对话模式"中的大小可变的数据包。 有两种情况下，驱动程序必须在其中定义**nMaxBytesPerFrame**，并在这两种情况下主机控制器驱动程序截获的值分配给**nMaxBytesPerFrame**作为*最小值*帧大小，而不是最大值，如果该驱动程序传输大小是可变的帧。

-   在请求\_ISOCH\_分配\_资源请求，该驱动程序必须指示中的帧大小**u.IsochAllocateResources.nMaxBytesPerFrame**隶属[ **IRB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/1394/ns-1394-_irb)。

-   在请求\_ISOCH\_附加\_缓冲区请求驱动程序必须指示中的帧大小**nMaxBytesPerFrame**隶属[ **ISOCH\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/1394/ns-1394-_isoch_descriptor)。

越小框架，多个帧主机控制器驱动程序可以根据传输缓冲区。 每个帧都需要系统资源，例如时间戳和状态信息，因为较小的帧更快地消耗系统资源。 主机控制器驱动程序计算将缓冲区中容纳不下的帧数和这些帧，根据中的值所需的资源数**nMaxBytesPerFrame**。 如果小于帧大小所示**nMaxBytesPerFrame**需要资源的帧数将大于由主机控制器驱动程序计算的值，这可能会导致错误。

这些注意事项不适用于驱动程序接收数据时，仅当该驱动程序正在传输中的大小可变的帧时"通信模式"。 驱动程序指定的数据传输与某一特定通道时获取与通道的资源句柄相关联的类型[**请求\_ISOCH\_分配\_资源**](https://msdn.microsoft.com/library/windows/hardware/ff537649)请求。 该驱动程序设置的资源\_变量\_ISOCH\_中的有效负载标志**u.IsochAllocateResources.fulFlags**期间此请求，以指示它会将传输大小可变的帧。 该驱动程序设置的资源\_用\_IN\_中的活动的谈话标志**u.IsochAllocateResources.fulFlags**以指示它将使用该通道来传输，而不是接收数据。 仅当驱动程序设置这两个这些标志在资源分配请求时将主机控制器驱动程序解释**nMaxBytesPerFrame**作为最小值而不是最大值。

请注意， **u.IsochAllocateResources.nMaxBufferSize**的成员[ **IRB** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/1394/ns-1394-_irb)始终是最大值。

驱动程序现在可以通过只需设置传输纯标头的数据包**DataLength**为零的标头元素的成员：

```cpp
HeaderElement->DataLength = 0
```

标头的描述符缓冲区的总长度指示通过常规方式**ulLength**描述符的成员。 它必须是整数的标头分散/集中元素数的倍数：

```cpp
IsochDescriptor->ulLength = IsochDescriptor->nMaxBytesPerFrame * NUMBER_OF_PACKETS;
```

其中数字\_OF\_数据包是传输 （包括仅限标头的数据包） 的数据包数。

标头元素结构，第三个成员**HeaderData**，是只是一个占位符，用以指示标头数据的开始位置。 下图演示了一个已组装的缓冲区的 8 字节 CIP 标头的示例。

![说明的 8 字节 cip 标头缓冲区的关系图](images/hdrelem.png)

给定描述符中的所有标头必须是长度相同。 这允许 OHCI 端口驱动程序 (*ohci1394.sys*) 分析类似于数组的元素的固定大小的标头描述符。 数据包的大小，可能会有所不同，但是必须是连续的没有"漏洞。"

标头和数据描述符中的数据必须是页面对齐。 数据数据包的大小没有限制，但标头和数据包都不允许跨页边界。 驱动程序必须正确对齐描述符缓冲区*之前设置缓冲区 MDL*。

如果，例如，驱动程序汇编 12 字节标头和 4 字节的标头元素的标头描述符，每个数据包将具有 16 个字节的预置数据。 16 字节到 4,096 字节页适合恰好 256 次，因为任何预置数据不断跨越页边界。

如果，但是，该驱动程序汇编 8 字节标头和 4 字节的标头元素的标头描述符，每个包将具有 12 个字节的预置数据。 因为 4,096 字节页不是一个整数，多个标头描述符必须为 12，是在 4,096 字节的大小，以防止跨页边界标头。 但是，标头的描述符缓冲区的大小可以扩展最多两个页面通过调整缓冲区中遵循的伪代码所示的基址。

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

 

 




