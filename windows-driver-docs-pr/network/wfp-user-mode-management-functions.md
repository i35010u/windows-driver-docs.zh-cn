---
title: WFP 用户模式管理函数
description: 本主题介绍 WFP 用户模式下管理功能。
ms.assetid: 14accd49-5b96-40]()e6-b9d7-6638a4e5c2dc
keywords:
- WFP 用户模式下管理功能的网络驱动程序
ms.date: 11/07/2017
ms.localizationpriority: medium
ms.openlocfilehash: 89e191460ca41a1bac4b29716be72d0f6f4bc60a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370561"
---
# <a name="wfp-user-mode-management-functions"></a>WFP 用户模式管理函数

Windows 筛选平台用户模式下管理功能的语义是完全相同时，从调用标注驱动程序，因为从用户模式应用程序，名为唯一的差别在于返回类型时**NTSTATUS**代码而不是 Win32 错误代码。 

这些函数均记录在[管理功能](https://docs.microsoft.com/windows/desktop/FWP/fwp-mgmt-functions)部分中的用户模式[WFP 函数](https://docs.microsoft.com/windows/desktop/FWP/fwp-functions)文档。 

> [!NOTE]
> 每个函数的内核模式版本 fwpmk.h 中定义。 每个函数的用户模式版本 fwpmu.h 中定义。
 
除这些函数的所有调用方[FwpmFreeMemory0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmfreememory0)必须运行在 IRQL = passive_level 调用。 调用方**FwpmFreeMemory0**必须在 IRQL 运行 < = DISPATCH_LEVEL。

## <a name="callout-management"></a>标注管理

- [FwpmCalloutAdd0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmcalloutadd0) 
- [FwpmCalloutCreateEnumHandle0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmcalloutcreateenumhandle0) 
- [FwpmCalloutDeleteById0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmcalloutdeletebyid0) 
- [FwpmCalloutDeleteByKey0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmcalloutdeletebykey0) 
- [FwpmCalloutDestroyEnumHandle0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmcalloutdestroyenumhandle0) 
- [FwpmCalloutEnum0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmcalloutenum0) 
- [FwpmCalloutGetById0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmcalloutgetbyid0) 
- [FwpmCalloutGetByKey0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmcalloutgetbykey0) 
- [FwpmCalloutGetSecurityInfoByKey0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmcalloutgetsecurityinfobykey0) 
- [FwpmCalloutSetSecurityInfoByKey0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmcalloutsetsecurityinfobykey0) 

## <a name="connection-object-management"></a>连接对象管理

- [FwpmConnectionCreateEnumHandle0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmconnectioncreateenumhandle0) 
- [FwpmConnectionDestroyEnumHandle0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmconnectiondestroyenumhandle0) 
- [FwpmConnectionEnum0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmconnectionenum0) 
- [FwpmConnectionGetById0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmconnectiongetbyid0) 
- [FwpmConnectionGetSecurityInfo0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmconnectiongetsecurityinfo0) 
- [FwpmConnectionSetSecurityInfo0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmconnectionsetsecurityinfo0) 

## <a name="event-management"></a>事件管理

- [FwpmNetEventCreateEnumHandle0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmneteventcreateenumhandle0) 
- [FwpmNetEventDestroyEnumHandle0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmneteventdestroyenumhandle0) 
- FwpmNetEventEnum:
    - [FwpmNetEventEnum0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmneteventenum0) (Windows Vista)
    - [FwpmNetEventEnum1](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmneteventenum1) (Windows 7)
    - [FwpmNetEventEnum2](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmneteventenum2) (Windows 8)
- [FwpmNetEventsGetSecurityInfo0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmneteventsgetsecurityinfo0) 
- [FwpmNetEventsSetSecurityInfo0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmneteventssetsecurityinfo0) 

## <a name="filter-management"></a>筛选器管理

- [FwpmFilterAdd0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmfilteradd0) 
- [FwpmFilterCreateEnumHandle0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmfiltercreateenumhandle0) 
- [FwpmFilterDeleteById0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmfilterdeletebyid0) 
- [FwpmFilterDeleteByKey0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmfilterdeletebykey0) 
- [FwpmFilterDestroyEnumHandle0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmfilterdestroyenumhandle0) 
- [FwpmFilterEnum0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmfilterenum0) 
- [FwpmFilterGetById0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmfiltergetbyid0) 
- [FwpmFilterGetByKey0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmfiltergetbykey0) 
- [FwpmFilterGetSecurityInfoByKey0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmfiltergetsecurityinfobykey0) 
- [FwpmFilterSetSecurityInfoByKey0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmfiltersetsecurityinfobykey0) 

## <a name="layer-management"></a>层管理

- [FwpmLayerCreateEnumHandle0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmlayercreateenumhandle0) 
- [FwpmLayerDestroyEnumHandle0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmlayerdestroyenumhandle0) 
- [FwpmLayerEnum0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmlayerenum0) 
- [FwpmLayerGetById0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmlayergetbyid0) 
- [FwpmLayerGetByKey0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmlayergetbykey0) 
- [FwpmLayerGetSecurityInfoByKey0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmlayergetsecurityinfobykey0) 
- [FwpmLayerSetSecurityInfoByKey0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmlayersetsecurityinfobykey0) 

## <a name="provider-context-management"></a>提供程序上下文管理

- [FwpmProviderContextAdd:
    - [FwpmProviderContextAdd0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidercontextadd0) (Windows Vista)
    - [FwpmProviderContextAdd1](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidercontextadd1) (Windows 7)
    - [FwpmProviderContextAdd2](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidercontextadd2) (Windows 8)
- [FwpmProviderContextCreateEnumHandle0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidercontextcreateenumhandle0) 
- [FwpmProviderContextDeleteById0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidercontextdeletebyid0) 
- [FwpmProviderContextDeleteByKey0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidercontextdeletebykey0) 
- [FwpmProviderContextDestroyEnumHandle0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidercontextdestroyenumhandle0) 
- FwpmProviderContextEnum:
    - [FwpmProviderContextEnum0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidercontextenum0) (Windows Vista)
    - [FwpmProviderContextEnum1](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidercontextenum1) (Windows 7)
    - [FwpmProviderContextEnum2](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidercontextenum2) (Windows 8)
- FwpmProviderContextGetById:
    - [FwpmProviderContextGetById0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidercontextgetbyid0) (Windows Vista)
    - [FwpmProviderContextGetById1](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidercontextgetbyid1) (Windows 7)
    - [FwpmProviderContextGetById2](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidercontextgetbyid2) (Windows 8)
- FwpmProviderContextGetByKey:
    - [FwpmProviderContextGetByKey0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidercontextgetbykey0) (Windows Vista)
    - [FwpmProviderContextGetByKey1](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidercontextgetbykey1) (Windows 7)
    - [FwpmProviderContextGetByKey2](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidercontextgetbykey2) (Windows 8)
- [FwpmProviderContextGetSecurityInfoByKey0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidercontextgetsecurityinfobykey0) 
- [FwpmProviderContextSetSecurityInfoByKey0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidercontextsetsecurityinfobykey0) 

## <a name="provider-management"></a>提供程序管理

- [FwpmProviderAdd0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovideradd0) 
- [FwpmProviderCreateEnumHandle0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidercreateenumhandle0) 
- [FwpmProviderDeleteByKey0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmproviderdeletebykey0) 
- [FwpmProviderDestroyEnumHandle0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmproviderdestroyenumhandle0) 
- [FwpmProviderEnum0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmproviderenum0) 
- [FwpmProviderGetByKey0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidergetbykey0) 
- [FwpmProviderGetSecurityInfoByKey0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidergetsecurityinfobykey0) 
- [FwpmProviderSetSecurityInfoByKey0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidersetsecurityinfobykey0) 

## <a name="session-management"></a>会话管理

- [FwpmEngineClose0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmengineclose0) 
- [FwpmEngineGetOption0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmenginegetoption0) 
- [FwpmEngineGetSecurityInfo0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmenginegetsecurityinfo0) 
- [FwpmEngineOpen0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmengineopen0) 
- [FwpmEngineSetOption0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmenginesetoption0) 
- [FwpmEngineSetSecurityInfo0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmenginesetsecurityinfo0) 
- [FwpmSessionCreateEnumHandle0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmsessioncreateenumhandle0) 
- [FwpmSessionDestroyEnumHandle0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmsessiondestroyenumhandle0) 
- [FwpmSessionEnum0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmsessionenum0) 

## <a name="sublayer-management"></a>子层管理

- [FwpmSubLayerAdd0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmsublayeradd0) 
- [FwpmSubLayerCreateEnumHandle0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmsublayercreateenumhandle0) 
- [FwpmSubLayerDeleteByKey0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmsublayerdeletebykey0) 
- [FwpmSubLayerDestroyEnumHandle0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmsublayerdestroyenumhandle0) 
- [FwpmSubLayerEnum0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmsublayerenum0) 
- [FwpmSubLayerGetByKey0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmsublayergetbykey0) 
- [FwpmSubLayerGetSecurityInfoByKey0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmsublayergetsecurityinfobykey0) 
- [FwpmSubLayerSetSecurityInfoByKey0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmsublayersetsecurityinfobykey0) 

## <a name="transaction-management"></a>事务管理

- [FwpmTransactionAbort0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmtransactionabort0) 
- [FwpmTransactionBegin0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmtransactionbegin0) 
- [FwpmTransactionCommit0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmtransactioncommit0) 

## <a name="vswitch-management"></a>vSwitch 管理

- [FwpmvSwitchEventsGetSecurityInfo0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmvswitcheventsgetsecurityinfo0) 
- [FwpmvSwitchEventsSetSecurityInfo0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmvswitcheventssetsecurityinfo0) 

