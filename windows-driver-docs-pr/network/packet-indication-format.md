---
title: 数据包指示格式
description: 数据包指示格式
ms.assetid: 37ee6db6-2f0e-4987-85e9-5362d23d7b27
keywords:
- 数据包指示 WDK Windows 筛选平台
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b0884caa88b401c5536c82e5266cd86bab04359c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541044"
---
# <a name="packet-indication-format"></a>数据包指示格式


网络数据作为 NDIS net 缓冲区列表所示 WFP ([**NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388))。 **下一步**的成员**NET\_缓冲区\_列表**结构可用于描述*链*的 net 缓冲区列表。 WFP 仅指示到标注的单个 net 缓冲区列表 (即，netBufferList-&gt;接下来 = = **NULL**)，但以下情况除外：

-   WFP 可以从 Stream 层到标注指示最终缓冲区列表链。

-   WFP 指示最终缓冲区列表链接至标注时将调出的前向路径中的 IP 数据包片段组分为两类。 链中的每个网络缓冲区列表描述了单个片段。

尽管 net 缓冲区列表可以描述整个数据包时，为不同类型的层，WFP net 缓冲区列表向指示标注在不同的偏移量从 IP 标头的开头。 例如，在传入的网络层，则 net 缓冲区列表开始执行后 IP 标头，在传入的传输层，net 缓冲区列表后开始传输标头。 IP 和传输标头始终由第一个描述[ **NET\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff568376) net 缓冲区列表中的结构。

Net 缓冲区列表中的偏移通过使用指定给标注**ipHeaderSize**并**transportHeaderSize**的成员[ **FWPS\_传入\_元数据\_VALUES0** ](https://msdn.microsoft.com/library/windows/hardware/ff552397)结构。 调出可以使用 NDIS 函数[ **NdisRetreatNetBufferDataStart** ](https://msdn.microsoft.com/library/windows/hardware/ff564527)并[ **NdisAdvanceNetBufferDataStart** ](https://msdn.microsoft.com/library/windows/hardware/ff560703)调整列出了指示最终缓冲区的偏移量。 但是在这种情况下，标注必须撤销的偏移量的调整之前它将返回[ *classifyFn* ](https://msdn.microsoft.com/library/windows/hardware/ff544890)函数。

在调用*classifyFn*传出数据的函数[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)可以包含多个[ **NET\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff568376)其中每个描述的 IP 数据包的结构。 如果 net 缓冲区列表中的某些数据包 （例如，网络缓冲区） 可以接受的但其他人不会标注驱动程序必须执行以下操作：

1.  克隆并阻止整个 net 缓冲区列表。

2.  生成一个新的 net 缓冲区列表描述的网络缓冲区可接受的子集。

3.  将新的 net 缓冲区列表传回发送路径。

或者，标注可以从网络缓冲区列表中不需要的网络缓冲区中取消链接并将传回发送路径更改后的净缓冲区列表。 但是，在这种情况下标注驱动程序必须撤消此修改到克隆的 net 缓冲区列表之前它将调用[ **FwpsFreeCloneNetBufferList0** ](https://msdn.microsoft.com/library/windows/hardware/ff551170)函数。 标注驱动程序还必须将原始 net 缓冲区链接信息保存其状态数据的一部分。

有关 WFP 使用的数据偏移量的详细信息，请参阅[数据的偏移量位置](https://msdn.microsoft.com/library/windows/hardware/ff546324)。

**请注意**  调出适用于已解密的 IPSec ESP 数据包必须使用的数据长度[ **NET\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff568376)而不是 MDL 数据以确定结构数据包长度。 若要获取的数据长度，请使用[ **NET\_缓冲区\_数据\_长度**](https://msdn.microsoft.com/library/windows/hardware/ff568382)宏。 有关详细信息，请参阅[开发 IPsec 兼容标注驱动程序](developing-ipsec-compatible-callout-drivers.md)。

 

 

 





