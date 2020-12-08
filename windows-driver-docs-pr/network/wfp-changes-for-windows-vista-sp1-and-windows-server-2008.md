---
title: Windows Vista SP1 和 Windows Server 2008 的 WFP 更改
description: Windows Vista SP1 和 Windows Server 2008 的 WFP 更改
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1394040abd9d85ee70b420ad61d4054ad429b305
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821871"
---
# <a name="wfp-changes-for-windows-vista-sp1-and-windows-server-2008"></a>Windows Vista SP1 和 Windows Server 2008 的 WFP 更改


在 Windows 筛选平台的可用功能和行为中进行了多项更改，该平台以带 Service Pack 1 的 Windows Vista (SP1) 和 Windows Server 2008 开始。 通常，若要充分利用新功能，必须编译或重新编译具有 NTDDI 版本宏的标注驱动程序， \_ 将其设置为 NTDDI \_ WIN6SP1。

-   新函数： [**FwpsConstructIpHeaderForTransportPacket0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsconstructipheaderfortransportpacket0) 
     [**FwpsReassembleForwardFragmentGroup0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsreassembleforwardfragmentgroup0)
-   \_ \_ \_ \_ FwpsStreamInjectAsync0 中描述的新的 FWPS 流标志接收推送标志 [ **FwpsStreamInjectAsync0** 选项](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsstreaminjectasync0)

-   更新和重命名了筛选条件，[这些条件在每个筛选层提供的筛选条件](./filtering-conditions-available-at-each-filtering-layer.md)中列出

-   已更新和重命名已添加到 FWPS 层 ALE 身份验证接收的数据字段标识符。 " \_ \_ \_ \_ \_ \_ *XXX* \_ \_ \_ \_ \_ *XXX* [数据字段标识符](./data-field-identifiers.md)" 中列出了 "接受 XXX" 和 "FWPS"，并与行为更改一起列出

-   在[每个筛选层](./metadata-fields-at-each-filtering-layer.md)的 "[元数据字段](./metadata-field-identifiers.md)" 和 "元数据" 字段中列出的其他元数据字段标识符

-   以下文档主题是新的：
    -   [开发 IPsec 兼容的标注驱动程序](developing-ipsec-compatible-callout-drivers.md)
    -   [以异步方式处理分类标注](processing-classify-callouts-asynchronously.md)
-   以下主题包含其他更新：[处理通知标注](processing-notify-callouts.md) 
     [流检查](stream-inspection.md) 
     [**FwpsFlowAssociateContext0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsflowassociatecontext0) 
     [**FwpsFlowRemoveContext0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsflowremovecontext0) 
     [*classifyFn*](/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_classify_fn0) 
     [*notifyFn*](/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_notify_fn0) 
     [**FWPS \_ CALLOUT0**](/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-fwps_callout0_) 
     [**FWPS \_ 传入 \_ 元数据 \_ VALUES0**](/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-fwps_incoming_metadata_values0_)

