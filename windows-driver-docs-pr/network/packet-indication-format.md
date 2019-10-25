---
title: 数据包指示格式
description: 数据包指示格式
ms.assetid: 37ee6db6-2f0e-4987-85e9-5362d23d7b27
keywords:
- 数据包指示 WDK Windows 筛选平台
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 25d060b728cab3c98eff66f6ab4a5f2fe5e2a8fb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843714"
---
# <a name="packet-indication-format"></a>数据包指示格式


网络数据在 WFP 中以 NDIS 网络缓冲区列表（[**net\_buffer\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)）表示。 **Net\_缓冲区**的**下一个**成员\_列表结构可用于描述网络缓冲区列表*链*。 WFP 仅指示&gt;netBufferList 的单个网络缓冲区列表（即，下一次 = = **NULL**），但以下情况除外：

-   WFP 可以指示从流层到标注的网络缓冲区列表链。

-   当向标注的正向路径中的 IP 数据包片段组分类时，WFP 指示将网络缓冲区列表链接到标注。 链中的每个网络缓冲区列表都描述了一个片段。

尽管网络缓冲区列表可以描述一个完整的数据包，但对于不同的层类型，WFP 会以不同于 IP 标头开头的偏移量指示网络缓冲区列表。 例如，在传入网络层，net buffer 列表在 IP 标头后开始，而在传入传输层，net buffer 列表在传输标头之后启动。 IP 和传输标头始终由网络缓冲区列表内的第一个[**网络\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)结构描述。

通过使用[**FWPS\_传入\_元数据\_VALUES0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-fwps_incoming_metadata_values0_)结构的的**ipHeaderSize**和**transportHeaderSize**成员，将网络缓冲区列表的偏移量指定为标注。 标注可以使用 NDIS 函数[**NdisRetreatNetBufferDataStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisretreatnetbufferdatastart)和[**NdisAdvanceNetBufferDataStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisadvancenetbufferdatastart)调整所指示的网络缓冲区列表的偏移量。 但在这种情况下，标注必须先撤消偏移调整，然后才能从[*classifyFn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_classify_fn0)函数返回。

在对传出数据的*classifyFn*函数调用中，[**网络\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)可以包含多个[**net\_缓冲**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)结构，其中每个结构都描述了一个 IP 数据包。 如果网络缓冲区列表中的某些数据包（例如，net buffer）是可接受的，但其他数据包不是，则标注驱动程序必须执行以下操作：

1.  克隆并阻止整个网络缓冲区列表。

2.  构建一个新的网络缓冲区列表，用于描述网络缓冲区的可接受子集。

3.  将新的 net buffer 列表注入回发送路径。

或者，标注可以取消链接网络缓冲区列表中不需要的网络缓冲区，并将已更改的网络缓冲区列表重新注入发送路径。 但是，在这种情况下，在调用[**FwpsFreeCloneNetBufferList0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsfreeclonenetbufferlist0)函数之前，标注驱动程序必须撤消对克隆的网络缓冲区列表所做的修改。 标注驱动程序还必须将原始网络缓冲区链接信息保存为其状态数据的一部分。

有关 WFP 使用的数据偏移量的详细信息，请参阅[数据偏移位置](https://docs.microsoft.com/windows-hardware/drivers/network/data-offset-positions)。

**请注意**，使用已解密的 IPSec ESP 数据包  的标注必须使用[**NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)结构的数据长度，而不是使用 MDL 数据来确定数据包长度。 若要获取数据长度，请使用[**NET\_BUFFER\_data\_length**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-data-length)宏。 有关详细信息，请参阅[开发与 IPsec 兼容的标注驱动程序](developing-ipsec-compatible-callout-drivers.md)。

 

 

 





