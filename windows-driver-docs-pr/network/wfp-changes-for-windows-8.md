---
title: 适用于 Windows 8 的 WFP 更改
description: 适用于 Windows 8 的 WFP 更改
ms.assetid: B83EC5A5-6169-49AB-A7EC-F2078AA0735E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f1393411cc9f0d908d494ef03a4aee2b21297e6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545144"
---
# <a name="wfp-changes-for-windows-8"></a>适用于 Windows 8 的 WFP 更改


可用的函数和行为的 Windows 筛选平台以与 Windows 8 中进行多项更改。 通常情况下，若要充分利用新功能，您必须编译或重新编译的标注驱动程序，具有 NTDDI\_版本宏设置为 NTDDI\_WIN8。

-   新的功能：
    - [使用第 2 层筛选](using-layer-2-filtering.md)
    - [使用跟踪的代理连接](using-proxied-connections-tracking.md)
    - [使用虚拟交换机筛选](using-virtual-switch-filtering.md)
-   新函数：
    - [**FwpsCalloutRegister2**](https://msdn.microsoft.com/library/windows/hardware/hh439576)
    - [**FwpsFlowAbort0**](https://msdn.microsoft.com/library/windows/hardware/hh439582)
    - [**FwpsInjectMacReceiveAsync0**](https://msdn.microsoft.com/library/windows/hardware/hh439588)
    - [**FwpsInjectMacSendAsync0**](https://msdn.microsoft.com/library/windows/hardware/hh439593)
    - [**FwpsNetBufferListAssociateContext1**](https://msdn.microsoft.com/library/windows/hardware/hh439674)
    - [**FwpsQueryConnectionRedirectState0**](https://msdn.microsoft.com/library/windows/hardware/hh439677)
    - [**FwpsRedirectHandleCreate0**](https://msdn.microsoft.com/library/windows/hardware/hh439681)
    - [**FwpsRedirectHandleDestroy0**](https://msdn.microsoft.com/library/windows/hardware/hh439684)
    - [**FwpsvSwitchEventsSubscribe0**](https://msdn.microsoft.com/library/windows/hardware/hh439687)
    - [**FwpsvSwitchEventsUnsubscribe0**](https://msdn.microsoft.com/library/windows/hardware/hh439691)
    - [**FwpsvSwitchNotifyComplete0**](https://msdn.microsoft.com/library/windows/hardware/hh439695)
-   新的回调函数：
    - [*FWPS\_CALLOUT\_CLASSIFY\_FN2*](https://msdn.microsoft.com/library/windows/hardware/hh439337)
    - [*FWPS\_CALLOUT\_NOTIFY\_FN2*](https://msdn.microsoft.com/library/windows/hardware/hh439963)
    - [*FWPS\_NET\_BUFFER\_LIST\_NOTIFY\_FN1*](https://msdn.microsoft.com/library/windows/hardware/hh451260)
    - [*FWPS\_VSWITCH\_FILTER\_ENGINE\_REORDER\_CALLBACK0*](https://msdn.microsoft.com/library/windows/hardware/hh451267)
    - [*FWPS\_VSWITCH\_INTERFACE\_EVENT\_CALLBACK0*](https://msdn.microsoft.com/library/windows/hardware/hh451269)
    - [*FWPS\_VSWITCH\_LIFETIME\_EVENT\_CALLBACK0*](https://msdn.microsoft.com/library/windows/hardware/hh451271)
    - [*FWPS\_VSWITCH\_POLICY\_EVENT\_CALLBACK0*](https://msdn.microsoft.com/library/windows/hardware/hh451272)
    - [*FWPS\_VSWITCH\_PORT\_EVENT\_CALLBACK0*](https://msdn.microsoft.com/library/windows/hardware/hh451276)
    - [*FWPS\_VSWITCH\_RUNTIME\_STATE\_RESTORE\_CALLBACK0*](https://msdn.microsoft.com/library/windows/hardware/hh451281)
    - [*FWPS\_VSWITCH\_RUNTIME\_STATE\_SAVE\_CALLBACK0*](https://msdn.microsoft.com/library/windows/hardware/hh451286)
-   新结构：
    - [**FWPS\_FILTER2**](https://msdn.microsoft.com/library/windows/hardware/hh439768)
    - [**FWPS\_VSWITCH\_EVENT\_DISPATCH\_TABLE0**](https://msdn.microsoft.com/library/windows/hardware/hh451263)
-   新枚举：
    - [**FWPS\_连接\_重定向\_状态**](https://msdn.microsoft.com/library/windows/hardware/hh439704)
    - [**FWPS\_FIELDS\_EGRESS\_VSWITCH\_ETHERNET**](https://msdn.microsoft.com/library/windows/hardware/hh439709)
    - [**FWPS\_FIELDS\_EGRESS\_VSWITCH\_TRANSPORT\_V4**](https://msdn.microsoft.com/library/windows/hardware/hh439715)
    - [**FWPS\_FIELDS\_EGRESS\_VSWITCH\_TRANSPORT\_V6**](https://msdn.microsoft.com/library/windows/hardware/hh439721)
    - [**FWPS\_FIELDS\_INBOUND\_MAC\_FRAME\_NATIVE**](https://msdn.microsoft.com/library/windows/hardware/hh439728)
    - [**FWPS\_FIELDS\_INGRESS\_VSWITCH\_ETHERNET**](https://msdn.microsoft.com/library/windows/hardware/hh439733)
    - [**FWPS\_FIELDS\_INGRESS\_VSWITCH\_TRANSPORT\_V4**](https://msdn.microsoft.com/library/windows/hardware/hh439738)
    - [**FWPS\_FIELDS\_INGRESS\_VSWITCH\_TRANSPORT\_V6**](https://msdn.microsoft.com/library/windows/hardware/hh439745)
    - [**FWPS\_FIELDS\_OUTBOUND\_MAC\_FRAME\_NATIVE**](https://msdn.microsoft.com/library/windows/hardware/hh439757)
    - [**FWPS\_VSWITCH\_EVENT\_TYPE**](https://msdn.microsoft.com/library/windows/hardware/hh451265)
-   已重命名的枚举：
    - [**FWPS\_字段\_入站\_MAC\_帧\_以太网**](https://msdn.microsoft.com/library/windows/hardware/ff551291) (已**FWPS\_字段\_入站\_MAC\_帧\_802\_3**)
    - [**FWPS\_字段\_出站\_MAC\_帧\_以太网**](https://msdn.microsoft.com/library/windows/hardware/ff551334) (已**FWPS\_字段\_出站\_MAC\_帧\_802\_3**)

 

 





