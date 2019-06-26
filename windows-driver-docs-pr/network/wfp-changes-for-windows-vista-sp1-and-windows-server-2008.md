---
title: Windows Vista SP1 和 Windows Server 2008 的 WFP 更改
description: Windows Vista SP1 和 Windows Server 2008 的 WFP 更改
ms.assetid: c901dbed-639d-473b-aaf0-8470e9c04009
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c032d9458e1998905a38c9856fa515456c335af
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67357010"
---
# <a name="wfp-changes-for-windows-vista-sp1-and-windows-server-2008"></a>Windows Vista SP1 和 Windows Server 2008 的 WFP 更改


可用的函数和行为的 Windows 筛选平台以开始使用 Windows Vista Service Pack 1 (SP1) 和 Windows Server 2008 中进行多项更改。 通常情况下，若要充分利用新功能，您必须编译或重新编译的标注驱动程序，具有 NTDDI\_版本宏设置为 NTDDI\_WIN6SP1。

-   新函数：[**FwpsConstructIpHeaderForTransportPacket0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpsconstructipheaderfortransportpacket0)
    [**FwpsReassembleForwardFragmentGroup0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpsreassembleforwardfragmentgroup0)
-   新 FWPS\_流\_标志\_接收\_中的描述的推送的标志选项[ **FwpsStreamInjectAsync0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpsstreaminjectasync0)

-   更新和重命名中列出的筛选条件[筛选可在筛选的每个层的条件](https://docs.microsoft.com/windows-hardware/drivers/network/filtering-conditions-available-at-each-filtering-layer)

-   更新和重命名数据字段标识符已添加到 FWPS\_层\_ALE\_身份验证\_收到\_接受\_*XXX*和 FWPS\_层\_入站\_ICMP\_错误\_*XXX*中列出的各层[数据的字段标识符](https://docs.microsoft.com/windows-hardware/drivers/network/data-field-identifiers)一起行为更改

-   中列出的其他元数据字段标识符[元数据字段](https://docs.microsoft.com/windows-hardware/drivers/network/metadata-fields)和[元数据字段在每个筛选层](https://docs.microsoft.com/windows-hardware/drivers/network/metadata-fields-at-each-filtering-layer)

-   以下文档主题是新增功能：
    -   [开发 IPsec 兼容标注驱动程序](developing-ipsec-compatible-callout-drivers.md)
    -   [处理对以异步方式进行分类的标注](processing-classify-callouts-asynchronously.md)
-   以下主题包含更多的更新：[处理通知标注](processing-notify-callouts.md)
    [Stream 检查](stream-inspection.md)
    [**FwpsFlowAssociateContext0** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpsflowassociatecontext0) 
     [**FwpsFlowRemoveContext0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpsflowremovecontext0)
    [*classifyFn* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nc-fwpsk-fwps_callout_classify_fn0) 
     [ *notifyFn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nc-fwpsk-fwps_callout_notify_fn0)
    [**FWPS\_CALLOUT0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/ns-fwpsk-fwps_callout0_)
    [**FWPS\_传入\_元数据\_VALUES0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/ns-fwpsk-fwps_incoming_metadata_values0_)

 

 





