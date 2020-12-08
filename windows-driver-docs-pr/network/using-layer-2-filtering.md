---
title: 使用第 2 层筛选
description: 使用第 2 层筛选
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b05ca707c824bea9527c0e9396f520c234822bdd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809907"
---
# <a name="using-layer-2-filtering"></a>使用第 2 层筛选

Windows 8 和更高版本的 Windows 支持第2层筛选。

此 WFP 功能允许筛选第2层 MAC 标头的字段。 对于主机发送或接收的所有数据包，将根据每个数据包调用这些层。 在入站路径上的数据包重组之前以及出站路径上的数据包碎片后，将调用这些层。 可以从 (LWF) 驱动程序的 NDIS 轻型筛选器访问这些层。

> [!NOTE]
> 如果某个图层上没有相应的筛选器，则标注不应在该层上插入数据包。 [网络 \_ 缓冲区 \_ 列表](net-buffer-list-structure.md)结构的注入应与筛选器添加和移除进行协调，以便仅当相应层中存在筛选器时才执行注入。 此外，提供程序不应删除属于其他提供程序的筛选器。 

本节包括下列主题：

-   [注入 MAC 帧](#injecting-mac-frames)
-   [对链式网络缓冲区列表分类](#classifying-chained-network-buffer-lists)
-   [WFP 第2层层和字段](#wfp-layer-2-layers-and-fields)

## <a name="injecting-mac-frames"></a>注入 MAC 帧

回调驱动程序会调用 [**FwpsInjectMacReceiveAsync0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsinjectmacreceiveasync0) 函数来 reinject 以前吸收的 MAC 帧 (或帧的克隆) 返回到它被截获的第2层入站数据路径，或在入站数据路径中注入一个发明的 mac 帧。

回调驱动程序会调用 [**FwpsInjectMacSendAsync0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsinjectmacsendasync0) 函数来 reinject 以前吸收的 MAC 帧 (或帧的克隆) 返回到它被截获的第2层出站数据路径，或在出站数据路径中注入一个发明的 mac 帧。

*NetBufferLists* 参数可以是 [网络 \_ 缓冲区 \_ 列表](net-buffer-list-structure.md)链。 不过，可以多次调用完成函数，完成段 (或单个网络 \_ 缓冲区 \_ 列表) 链。

如果数据包与最初分类的筛选器匹配，则插入的帧可能会再次分类。 因此，与 IP 层的标注一样，第2层标注还必须通过调用 [**FwpsQueryPacketInjectionState0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsquerypacketinjectionstate0)防止无限数据包检查。

此外，还必须在插入的层上安装标注。 否则，注入的 [网络 \_ 缓冲区 \_ 列表](net-buffer-list-structure.md) 将不会完成到完成函数中，并且 NET \_ buffer \_ 列表将沿堆栈进一步增加。 在这种情况下，该行为是不确定的，因为 NDIS 会尝试将注入的网络 \_ 缓冲区 \_ 列表传递到堆栈中的下一个组件。

[NET \_ BUFFER \_ LIST](net-buffer-list-structure.md)**status** 成员包含堆栈注入的状态结果。 堆栈注入的状态结果是在 \_ \_ WFP 注入函数返回 **状态 " \_ 成功**" 后堆栈置于网络缓冲区列表中的状态。 应使用 **NT \_ SUCCESS** 宏来检查 **状态** 成员中的堆栈注入状态。 如果 **status** 值为 **status \_ SUCCESS**，则注入成功，没有其他信息。 大于 **状态 \_ 成功** 的 **状态** 成员值意味着注入成功，但可能存在有关应考虑的注入的详细信息。 小于 **状态 \_ 成功** 的 **状态** 成员值意味着注入因 **状态** 成员中指定的原因而失败。

## <a name="classifying-chained-network-buffer-lists"></a>对链式网络缓冲区列表分类

默认情况下，标注驱动程序只能为网络缓冲区列表单独分类。 但是，如果执行以下两项操作，标注驱动程序可以对 [网络 \_ 缓冲区 \_ 列表](net-buffer-list-structure.md) 链进行分类以获得更好的性能：

-   指定在 [**FWPS \_ CALLOUT2**](/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-fwps_callout2_)结构的 **Flags** 成员中 **\_ \_ \_ 允许 \_ L2 \_ 批 \_ 分类标志的 .fwp 标注标志**。
-   注册可对 [网络 \_ 缓冲区 \_ 列表](net-buffer-list-structure.md)链进行分类的 [*classifyFn2*](/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_classify_fn2)函数。

> [!WARNING]
> 但是，如果标注驱动程序设置了 **FWP_CALLOUT_FLAG_ALLOW_L2_BATCH_CLASSIFY** 标志，则它不能使用以下函数来修改 NET_BUFFER_LISTs。
> 
> - [FwpsReferenceNetBufferList0](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsreferencenetbufferlist0)
> - [FwpsDereferenceNetBufferList0](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsdereferencenetbufferlist0)
> - [FwpsAllocateCloneNetBufferList0](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsallocateclonenetbufferlist0)
> - [FwpsFreeCloneNetBufferList0](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsfreeclonenetbufferlist0)
>
> 设置此标志后， **FwpsAllocateCloneNetBufferList0** 将始终返回 **INVALID_PARAMETER** 错误。 这可能会意外导致第三方标注驱动程序无法管理网络缓冲区列表的引用 \_ 计数 \_ ，从而导致发送和接收操作停止。

## <a name="wfp-layer-2-layers-and-fields"></a>WFP 第2层层和字段

虚拟交换机筛选的运行时筛选层标识符包括：

**FWPS \_ 层 \_ 入站 \_ MAC \_ 帧 \_ 以太网**

**FWPS \_ 层 \_ 出站 \_ MAC \_ 帧 \_ 以太网**

**FWPS \_ 层 \_ 入站 \_ MAC \_ 帧 \_ 本机**

**FWPS \_ 层 \_ 出站 \_ MAC \_ 帧 \_ 本机**

用于虚拟交换机筛选的数据字段标识符包括：

[**FWPS \_ 字段 \_ 入站 \_ MAC \_ 帧 \_ 以太网**](/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_inbound_mac_frame_ethernet_)

[**FWPS \_ 字段 \_ 出站 \_ MAC \_ 帧 \_ 以太网**](/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_outbound_mac_frame_ethernet_)

[**FWPS \_ 字段 \_ 入站 \_ MAC \_ 帧 \_ 本机**](/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_inbound_mac_frame_native_)

[**FWPS \_ 字段 \_ 出站 \_ MAC \_ 帧 \_ 本机**](/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_outbound_mac_frame_native_)

 

