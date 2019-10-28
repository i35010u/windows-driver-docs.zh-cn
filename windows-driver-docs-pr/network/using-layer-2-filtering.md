---
title: 使用第 2 层筛选
description: 使用第 2 层筛选
ms.assetid: 679E6DE2-4EFB-44F6-936D-2BF611BC9726
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a0ddbda562aa2979e4b5e4ce109beb38fb3af17
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842990"
---
# <a name="using-layer-2-filtering"></a>使用第 2 层筛选

Windows 8 和更高版本的 Windows 支持第2层筛选。

此 WFP 功能允许筛选第2层 MAC 标头的字段。 对于主机发送或接收的所有数据包，将根据每个数据包调用这些层。 在入站路径上的数据包重组之前以及出站路径上的数据包碎片后，将调用这些层。 可从 NDIS 轻型筛选器（LWF）驱动程序访问这些层。

> [!NOTE]
> 如果某个图层上没有相应的筛选器，则标注不应在该层上插入数据包。 [NET\_缓冲区\_列表](net-buffer-list-structure.md)结构的注入应与筛选器添加和删除操作进行协调，以便仅当相应层中存在筛选器时才执行注入。 此外，提供程序不应删除属于其他提供程序的筛选器。 

本部分包括下列主题：

-   [注入 MAC 帧](#injecting-mac-frames)
-   [对链式网络缓冲区列表分类](#classifying-chained-network-buffer-lists)
-   [WFP 第2层层和字段](#wfp-layer-2-layers-and-fields)

## <a name="injecting-mac-frames"></a>注入 MAC 帧

回调驱动程序将调用[**FwpsInjectMacReceiveAsync0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsinjectmacreceiveasync0)函数，以将以前吸收的 mac 帧（或帧的克隆） reinject 回被截获的第2层入站数据路径，或在入站数据路径中注入一个发明的 mac 帧。

回调驱动程序将调用[**FwpsInjectMacSendAsync0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsinjectmacsendasync0)函数，以将以前吸收的 mac 帧（或帧的克隆） reinject 回被截获的第2层出站数据路径，或在出站数据路径中注入一个发明的 mac 帧。

*NetBufferLists*参数可以是[网络\_缓冲区\_列表](net-buffer-list-structure.md)链。 不过，可以多次调用完成函数，完成该链的一个段（或单个网络\_缓冲区\_列表）。

如果数据包与最初分类的筛选器匹配，则插入的帧可能会再次分类。 因此，与 IP 层的标注一样，第2层标注还必须通过调用[**FwpsQueryPacketInjectionState0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsquerypacketinjectionstate0)防止无限数据包检查。

此外，还必须在插入的层上安装标注。 否则，注入的[NET\_缓冲区\_列表](net-buffer-list-structure.md)将不会完成到完成函数中，并且 NET\_缓冲区\_列表将在堆栈中向上提升。 在这种情况下，该行为是不确定的，因为 NDIS 会尝试将注入的 NET\_缓冲区\_列表传递到堆栈中的下一个组件。

[NET\_缓冲区\_列表](net-buffer-list-structure.md)**状态**成员包含堆栈注入的状态结果。 堆栈注入的状态结果是在 WFP 注入函数返回**状态\_SUCCESS**后，堆栈置于 NET\_缓冲区\_列表的状态。 应使用**NT\_SUCCESS**宏来检查**状态**成员中堆栈注入的状态。 如果**status**值为**status\_SUCCESS**，则注入成功，无需进一步的信息。 如果**状态**成员值大于**状态\_成功**意味着注入成功，但可能存在有关应考虑的注入的详细信息。 如果**状态**成员值小于**状态\_成功**，则表示由于在**状态**成员中指定的原因注入失败。

## <a name="classifying-chained-network-buffer-lists"></a>对链式网络缓冲区列表分类

默认情况下，标注驱动程序只能为网络缓冲区列表单独分类。 但是，如果执行以下两项操作，标注驱动程序可以将[NET\_缓冲器分类\_列表](net-buffer-list-structure.md)链，以获得更好的性能：

-   指定 **.fwp\_标注\_标志\_允许**在[**FWPS\_CALLOUT2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-fwps_callout2_)结构的**Flags**成员中\_L2\_BATCH\_分类标志。
-   注册一个[*classifyFn2*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_classify_fn2)函数，该函数可对[NET\_BUFFER\_列表](net-buffer-list-structure.md)链进行分类。

> [!WARNING]
> 但是，如果标注驱动程序设置了**FWP_CALLOUT_FLAG_ALLOW_L2_BATCH_CLASSIFY**标志，则它不能使用以下函数来修改 NET_BUFFER_LISTs。
> 
> - [FwpsReferenceNetBufferList0](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsreferencenetbufferlist0)
> - [FwpsDereferenceNetBufferList0](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsdereferencenetbufferlist0)
> - [FwpsAllocateCloneNetBufferList0](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsallocateclonenetbufferlist0)
> - [FwpsFreeCloneNetBufferList0](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsfreeclonenetbufferlist0)
>
> 设置此标志后， **FwpsAllocateCloneNetBufferList0**将始终返回**INVALID_PARAMETER**错误。 这可能会意外导致第三方标注驱动程序无法管理 NET\_缓冲区\_列表的引用计数，导致发送和接收操作停止。

## <a name="wfp-layer-2-layers-and-fields"></a>WFP 第2层层和字段

虚拟交换机筛选的运行时筛选层标识符包括：

**FWPS\_层\_入站\_MAC\_帧\_以太网**

**FWPS\_层\_出站\_MAC\_帧\_以太网**

**FWPS\_层\_入站\_MAC\_帧\_本机**

**FWPS\_层\_出站\_MAC\_帧\_本机**

用于虚拟交换机筛选的数据字段标识符包括：

[**FWPS\_字段\_入站\_MAC\_帧\_以太网**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_inbound_mac_frame_ethernet_)

[**FWPS\_字段\_出站\_MAC\_帧\_以太网**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_outbound_mac_frame_ethernet_)

[**FWPS\_字段\_入站\_MAC\_帧\_本机**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_inbound_mac_frame_native_)

[**FWPS\_字段\_出站\_MAC\_帧\_本机**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_outbound_mac_frame_native_)

 

 





