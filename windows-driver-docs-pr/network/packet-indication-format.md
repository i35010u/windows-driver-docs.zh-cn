---
title: 数据包指示格式
description: 数据包指示格式
keywords:
- 数据包指示 WDK Windows 筛选平台
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 61ec13eca4747ecaa6b83451039d579d34edeb45
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248423"
---
# <a name="packet-indication-format"></a>数据包指示格式


网络数据在 WFP 中以 NDIS 网络缓冲区列表的形式指示 ([**net \_ buffer \_ LIST**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_list)) 。 **网络 \_ 缓冲区 \_ 列表** 结构的 **下一个** 成员可用于描述网络缓冲区列表的 *链*。 WFP 仅指示单个网络缓冲区列表， (即，netBufferList &gt; = = **NULL**) ，但以下情况除外：

-   WFP 可以指示从流层到标注的网络缓冲区列表链。

-   当向标注的正向路径中的 IP 数据包片段组分类时，WFP 指示将网络缓冲区列表链接到标注。 链中的每个网络缓冲区列表都描述了一个片段。

尽管网络缓冲区列表可以描述一个完整的数据包，但对于不同的层类型，WFP 会以不同于 IP 标头开头的偏移量指示网络缓冲区列表。 例如，在传入网络层，net buffer 列表在 IP 标头后开始，而在传入传输层，net buffer 列表在传输标头之后启动。 IP 和传输标头始终由网络缓冲区列表内的第一个 [**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer) 结构描述。

通过使用 [**FWPS \_ 传入的 \_ 元数据 \_ VALUES0**](/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-fwps_incoming_metadata_values0_)结构的 **ipHeaderSize** 和 **transportHeaderSize** 成员，可向网络缓冲区列表中的偏移量指示标注。 标注可以使用 NDIS 函数 [**NdisRetreatNetBufferDataStart**](/windows-hardware/drivers/ddi/nblapi/nf-nblapi-ndisretreatnetbufferdatastart) 和 [**NdisAdvanceNetBufferDataStart**](/windows-hardware/drivers/ddi/nblapi/nf-nblapi-ndisadvancenetbufferdatastart) 调整所指示的网络缓冲区列表的偏移量。 但在这种情况下，标注必须先撤消偏移调整，然后才能从 [*classifyFn*](/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_classify_fn0) 函数返回。

在对传出数据的 *classifyFn* 函数的调用中， [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_list) 可以包含多个 [**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer) 结构，其中每个结构都描述了一个 IP 数据包。 例如，如果某些数据包 (例如，网络缓冲区列表中) 的网络缓冲区是可接受的，但其他一些则不是，则标注驱动程序必须执行以下操作：

1.  克隆并阻止整个网络缓冲区列表。

2.  构建一个新的网络缓冲区列表，用于描述网络缓冲区的可接受子集。

3.  将新的 net buffer 列表注入回发送路径。

或者，标注可以取消链接网络缓冲区列表中不需要的网络缓冲区，并将已更改的网络缓冲区列表重新注入发送路径。 但是，在这种情况下，在调用 [**FwpsFreeCloneNetBufferList0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsfreeclonenetbufferlist0) 函数之前，标注驱动程序必须撤消对克隆的网络缓冲区列表所做的修改。 标注驱动程序还必须将原始网络缓冲区链接信息保存为其状态数据的一部分。

有关 WFP 使用的数据偏移量的详细信息，请参阅 [数据偏移位置](./data-offset-positions.md)。

**注意**  使用已解密 IPSec ESP 数据包的标注必须使用 [**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer) 的数据长度（而不是 MDL 数据）来确定数据包长度。 若要获取数据长度，请使用 [**NET \_ BUFFER \_ 数据 \_ 长度**](/windows-hardware/drivers/ddi/nblaccessors/nf-nblaccessors-net_buffer_data_length) 宏。 有关详细信息，请参阅 [开发 IPsec-Compatible 标注驱动程序](developing-ipsec-compatible-callout-drivers.md)。

 

 

