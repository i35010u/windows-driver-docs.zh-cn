---
title: Windows Vista SP1 和 Windows Server 2008 的 WFP 更改
description: Windows Vista SP1 和 Windows Server 2008 的 WFP 更改
ms.assetid: c901dbed-639d-473b-aaf0-8470e9c04009
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c91c52c7d9b8acf0cf695be38e811e25d96c1ae
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841701"
---
# <a name="wfp-changes-for-windows-vista-sp1-and-windows-server-2008"></a>Windows Vista SP1 和 Windows Server 2008 的 WFP 更改


在 Windows 筛选平台（windows Vista Service Pack 1 （SP1）和 Windows Server 2008）的可用功能和行为中进行了一些更改。 通常，若要充分利用新功能，必须编译或重新编译将 NTDDI\_VERSION 宏设置为 NTDDI\_WIN6SP1 的标注驱动程序。

-   新函数： [**FwpsConstructIpHeaderForTransportPacket0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsconstructipheaderfortransportpacket0)
    [**FwpsReassembleForwardFragmentGroup0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsreassembleforwardfragmentgroup0)
-   新的 FWPS\_STREAM\_标志\_接收\_推送标志选项，如 FwpsStreamInjectAsync0 中所述。 [](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsstreaminjectasync0)

-   更新和重命名了筛选条件，[这些条件在每个筛选层提供的筛选条件](https://docs.microsoft.com/windows-hardware/drivers/network/filtering-conditions-available-at-each-filtering-layer)中列出

-   已更新和重命名数据字段标识符，这些标识符已添加到 FWPS\_层\_ALE\_身份验证\_接收\_ *\_\_\_\_* \_\_*XXX*层，列在[数据字段标识符](https://docs.microsoft.com/windows-hardware/drivers/network/data-field-identifiers)中，以及行为更改

-   在[每个筛选层](https://docs.microsoft.com/windows-hardware/drivers/network/metadata-fields-at-each-filtering-layer)的 "[元数据字段](https://docs.microsoft.com/windows-hardware/drivers/network/metadata-fields)" 和 "元数据" 字段中列出的其他元数据字段标识符

-   以下文档主题是新的：
    -   [开发与 IPsec 兼容的标注驱动程序](developing-ipsec-compatible-callout-drivers.md)
    -   [异步处理分类标注](processing-classify-callouts-asynchronously.md)
-   以下主题包含其他更新：[处理通知标注](processing-notify-callouts.md)
    [流检查](stream-inspection.md)
    [**FwpsFlowAssociateContext0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsflowassociatecontext0)
    [**FwpsFlowRemoveContext0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsflowremovecontext0)
    [*classifyFn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_classify_fn0)
    [*notifyFn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_notify_fn0)
    [**FWPS\_CALLOUT0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-fwps_callout0_)
    [**FWPS\_传入\_元数据\_VALUES0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-fwps_incoming_metadata_values0_)

 

 





