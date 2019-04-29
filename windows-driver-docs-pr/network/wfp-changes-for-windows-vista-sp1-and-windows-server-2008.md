---
title: Windows Vista SP1 和 Windows Server 2008 的 WFP 更改
description: Windows Vista SP1 和 Windows Server 2008 的 WFP 更改
ms.assetid: c901dbed-639d-473b-aaf0-8470e9c04009
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 209bab48526a194e9c2a57143a461939bb83b6ac
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365701"
---
# <a name="wfp-changes-for-windows-vista-sp1-and-windows-server-2008"></a>Windows Vista SP1 和 Windows Server 2008 的 WFP 更改


可用的函数和行为的 Windows 筛选平台以开始使用 Windows Vista Service Pack 1 (SP1) 和 Windows Server 2008 中进行多项更改。 通常情况下，若要充分利用新功能，您必须编译或重新编译的标注驱动程序，具有 NTDDI\_版本宏设置为 NTDDI\_WIN6SP1。

-   新函数：[**FwpsConstructIpHeaderForTransportPacket0**](https://msdn.microsoft.com/library/windows/hardware/ff551154)
    [**FwpsReassembleForwardFragmentGroup0**](https://msdn.microsoft.com/library/windows/hardware/ff551205)
-   新 FWPS\_流\_标志\_接收\_中的描述的推送的标志选项[ **FwpsStreamInjectAsync0**](https://msdn.microsoft.com/library/windows/hardware/ff551213)

-   更新和重命名中列出的筛选条件[筛选可在筛选的每个层的条件](https://msdn.microsoft.com/library/windows/hardware/ff549939)

-   更新和重命名数据字段标识符已添加到 FWPS\_层\_ALE\_身份验证\_收到\_接受\_*XXX*和 FWPS\_层\_入站\_ICMP\_错误\_*XXX*中列出的各层[数据的字段标识符](https://msdn.microsoft.com/library/windows/hardware/ff546312)一起行为更改

-   中列出的其他元数据字段标识符[元数据字段](https://msdn.microsoft.com/library/windows/hardware/ff559174)和[元数据字段在每个筛选层](https://msdn.microsoft.com/library/windows/hardware/ff559179)

-   以下文档主题是新增功能：
    -   [开发 IPsec 兼容标注驱动程序](developing-ipsec-compatible-callout-drivers.md)
    -   [处理对以异步方式进行分类的标注](processing-classify-callouts-asynchronously.md)
-   以下主题包含更多的更新：[处理通知标注](processing-notify-callouts.md)
    [Stream 检查](stream-inspection.md)
    [**FwpsFlowAssociateContext0** ](https://msdn.microsoft.com/library/windows/hardware/ff551165) 
     [**FwpsFlowRemoveContext0**](https://msdn.microsoft.com/library/windows/hardware/ff551169)
    [*classifyFn* ](https://msdn.microsoft.com/library/windows/hardware/ff544890) 
     [ *notifyFn*](https://msdn.microsoft.com/library/windows/hardware/ff568803)
    [**FWPS\_CALLOUT0**](https://msdn.microsoft.com/library/windows/hardware/ff551224)
    [**FWPS\_传入\_元数据\_VALUES0**](https://msdn.microsoft.com/library/windows/hardware/ff552397)

 

 





