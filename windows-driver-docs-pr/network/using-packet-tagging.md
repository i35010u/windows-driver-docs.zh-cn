---
title: 使用数据包标记
description: 使用数据包标记
ms.assetid: a151256b-d69f-4abb-bf68-644f157dfdd7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe6218d4bb52bb21a042c5a4162035482346af26
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842980"
---
# <a name="using-packet-tagging"></a>使用数据包标记


标注驱动程序可以标记感兴趣的数据包，并接收标记的数据包中发生的事件的通知。 Windows 7 和更高版本的 Windows 中支持数据包标记。

若要使用数据包标记，标注驱动程序必须实现[*FWPS\_NET\_buffer\_列表\_通知\_FN0*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_net_buffer_list_notify_fn0)或[*FWPS\_NET\_* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_net_buffer_list_notify_fn1)\_\_\_才能. 此函数将接收标记数据包的所有状态通知。 在标记各个数据包之前，标注驱动程序必须通过调用[**FwpsNetBufferListGetTagForContext0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsnetbufferlistgettagforcontext0)来获取特殊的上下文标记。 标注驱动程序可以对部分或全部标记的数据包使用相同的上下文标记。 例如，标注驱动程序可以使用不同的上下文标记来区分标记数据包的类型。

标注驱动程序使用[**NET\_BUFFER\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构来标记数据包。 标注驱动程序调用[**FwpsNetBufferListAssociateContext0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsnetbufferlistassociatecontext0)来标记各个**网络\_缓冲区\_列表**结构。 标注驱动程序与数据包关联的上下文是任意未签名的64位值。 触发事件时， [*FWPS\_NET\_buffer\_列表\_通知\_FN0*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_net_buffer_list_notify_fn0)或[*FWPS\_NET\_* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_net_buffer_list_notify_fn1)\_\_\_通知输入参数，使标注驱动程序可以识别单个标记数据包。 筛选引擎不使用或计算上下文。 它仅传递到回调以供标注驱动程序使用。

当数据包离开堆栈时，上下文会自动从标记的数据包中删除。 但是，如果数据包从不进入 TCP/IP 堆栈（例如，在使用 NDIS 筛选器驱动程序的情况下），则需要通过调用[**FwpsNetBufferListRemoveContext0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsnetbufferlistremovecontext0)并将*netBufferList*参数设置为 NULL，手动删除上下文.

如果某个标注需要提前中止标记操作，则可以通过调用[**FwpsNetBufferListRemoveContext0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsnetbufferlistremovecontext0)来删除上下文。 删除上下文通常会触发**FWPS\_NET\_缓冲器\_列表\_上下文\_删除**事件。 有关可触发的事件的详细信息，请参阅[**FWPS\_NET\_BUFFER\_LIST\_事件\_TYPE0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_net_buffer_list_event_type0_)枚举。 在某些情况下，将不会触发任何事件，例如当包从不进入 TCP/IP 堆栈进行处理时。

克隆标记的数据包时，标注驱动程序可以将上下文移动或复制到克隆包。 若要移动上下文（对于克隆），标注驱动程序必须调用[**FwpsNetBufferListRetrieveContext0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsnetbufferlistretrievecontext0) ，并将*removeContext*参数设置为**TRUE**。 然后，可以将该上下文与新的数据包相关联。 复制上下文（对于重复项）的过程相同，只不过**FwpsNetBufferListRetrieveContext0**的*removeContext*参数必须设置为**FALSE**。

可从[NDIS 筛选器驱动程序](ndis-filter-drivers2.md)检索从 tcp/ip 层标记的数据包。 反之也是如此。 不会在未指明数据包（数据段除外）的流层中提供数据包标记。

标注驱动程序可以检索[*FWPS\_NET\_BUFFER\_列表*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_net_buffer_list_notify_fn0)之外的数据包的上下文\_通知\_\_\_\_\_\_[*列表FN1*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_net_buffer_list_notify_fn1) [**函数。** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsnetbufferlistretrievecontext0) 通常，标注驱动程序会在其[classifyFn](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)回调中检索上下文。

## <a name="related-topics"></a>相关主题


[classifyFn](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

[**FWPS\_NET\_BUFFER\_列表\_事件\_TYPE0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_net_buffer_list_event_type0_)

[*FWPS\_NET\_缓冲器\_列表\_通知\_FN0*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_net_buffer_list_notify_fn0)

[*FWPS\_NET\_缓冲器\_列表\_通知\_FN1*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_net_buffer_list_notify_fn1)

[**FwpsNetBufferListAssociateContext0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsnetbufferlistassociatecontext0)

[**FwpsNetBufferListGetTagForContext0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsnetbufferlistgettagforcontext0)

[**FwpsNetBufferListRemoveContext0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsnetbufferlistremovecontext0)

[**FwpsNetBufferListRetrieveContext0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsnetbufferlistretrievecontext0)

[**NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)

[NDIS 筛选器驱动程序](ndis-filter-drivers2.md)

 

 






