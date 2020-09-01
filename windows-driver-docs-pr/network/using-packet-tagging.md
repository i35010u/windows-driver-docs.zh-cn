---
title: 使用数据包标记
description: 使用数据包标记
ms.assetid: a151256b-d69f-4abb-bf68-644f157dfdd7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a5c760490902683558ceb9834a6abf3addcac6c
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211557"
---
# <a name="using-packet-tagging"></a>使用数据包标记


标注驱动程序可以标记感兴趣的数据包，并接收标记的数据包中发生的事件的通知。 Windows 7 和更高版本的 Windows 中支持数据包标记。

若要使用数据包标记，标注驱动程序必须实现 [*FWPS \_ net \_ buffer \_ List \_ notify \_ FN0*](/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_net_buffer_list_notify_fn0) 或 [*FWPS \_ net \_ buffer \_ list \_ notify \_ FN1*](/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_net_buffer_list_notify_fn1) 回调函数。 此函数将接收标记数据包的所有状态通知。 在标记各个数据包之前，标注驱动程序必须通过调用 [**FwpsNetBufferListGetTagForContext0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsnetbufferlistgettagforcontext0)来获取特殊的上下文标记。 标注驱动程序可以对部分或全部标记的数据包使用相同的上下文标记。 例如，标注驱动程序可以使用不同的上下文标记来区分标记数据包的类型。

标注驱动程序使用 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构来标记数据包。 标注驱动程序调用 [**FwpsNetBufferListAssociateContext0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsnetbufferlistassociatecontext0) 来标记各个 **网络 \_ 缓冲区 \_ 列表** 结构。 标注驱动程序与数据包关联的上下文是任意未签名的64位值。 触发事件时， [*FWPS \_ net \_ buffer \_ List \_ 通知 \_ FN0*](/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_net_buffer_list_notify_fn0) 或 [*FWPS \_ net \_ buffer \_ list \_ 通知 \_ FN1*](/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_net_buffer_list_notify_fn1) 回调将上下文作为输入参数传递，以使标注驱动程序能够识别单个标记的数据包。 筛选引擎不使用或计算上下文。 它仅传递到回调以供标注驱动程序使用。

当数据包离开堆栈时，上下文会自动从标记的数据包中删除。 但是，如果数据包从不进入 TCP/IP 堆栈（例如，在使用 NDIS 筛选器驱动程序的情况下），则需要通过调用 [**FwpsNetBufferListRemoveContext0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsnetbufferlistremovecontext0) 并将 *netBufferList* 参数设置为 **NULL**，手动删除上下文。

如果某个标注需要提前中止标记操作，则可以通过调用 [**FwpsNetBufferListRemoveContext0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsnetbufferlistremovecontext0)来删除上下文。 删除上下文通常会触发 **FWPS \_ 网络 \_ 缓冲区 \_ 列表 \_ 上下文 \_ 删除** 事件。 有关可触发的事件的详细信息，请参阅 [**FWPS \_ NET \_ BUFFER \_ LIST \_ EVENT \_ TYPE0**](/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_net_buffer_list_event_type0_) 枚举。 在某些情况下，将不会触发任何事件，例如当包从不进入 TCP/IP 堆栈进行处理时。

克隆标记的数据包时，标注驱动程序可以将上下文移动或复制到克隆包。 若要在克隆) 的情况下移动上下文 (，标注驱动程序必须调用 [**FwpsNetBufferListRetrieveContext0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsnetbufferlistretrievecontext0) ，并将 *removeContext* 参数设置为 **TRUE**。 然后，可以将该上下文与新的数据包相关联。 对于复制) ，复制上下文 (的过程是相同的，只不过**FwpsNetBufferListRetrieveContext0**的*removeContext*参数必须设置为**FALSE**。

可从 [NDIS 筛选器驱动程序](./roadmap-for-developing-ndis-filter-drivers.md)检索从 tcp/ip 层标记的数据包。 反之亦然。 不会在未指明数据包（数据段除外）的流层中提供数据包标记。

标注驱动程序可以通过调用[**FwpsNetBufferListRetrieveContext0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsnetbufferlistretrievecontext0)，为[*FWPS \_ net \_ Buffer \_ list \_ notify \_ FN0*](/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_net_buffer_list_notify_fn0)或[*FWPS \_ net \_ buffer \_ list \_ notify \_ FN1*](/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_net_buffer_list_notify_fn1)函数之外的数据包检索上下文。 通常，标注驱动程序会在其 [classifyFn](/windows-hardware/drivers/ddi/_netvista/) 回调中检索上下文。

## <a name="related-topics"></a>相关主题


[classifyFn](/windows-hardware/drivers/ddi/_netvista/)

[**FWPS \_ NET \_ BUFFER \_ LIST \_ 事件 \_ TYPE0**](/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_net_buffer_list_event_type0_)

[*FWPS \_ 网络 \_ 缓冲区 \_ 列表 \_ 通知 \_ FN0*](/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_net_buffer_list_notify_fn0)

[*FWPS \_ 网络 \_ 缓冲区 \_ 列表 \_ 通知 \_ FN1*](/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_net_buffer_list_notify_fn1)

[**FwpsNetBufferListAssociateContext0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsnetbufferlistassociatecontext0)

[**FwpsNetBufferListGetTagForContext0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsnetbufferlistgettagforcontext0)

[**FwpsNetBufferListRemoveContext0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsnetbufferlistremovecontext0)

[**FwpsNetBufferListRetrieveContext0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsnetbufferlistretrievecontext0)

[**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)

[NDIS 筛选器驱动程序](./roadmap-for-developing-ndis-filter-drivers.md)

 

