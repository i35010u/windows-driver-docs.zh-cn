---
title: WFP 用户模式管理函数
description: 本主题介绍 WFP 用户模式管理功能。
ms.assetid: 14accd49-5b96-40]()e6-b9d7-6638a4e5c2dc
keywords:
- WFP 用户模式管理功能网络驱动程序
ms.date: 11/07/2017
ms.localizationpriority: medium
ms.openlocfilehash: c236d2a1c3422c8e4a2b8117f3a2b5baf2c99821
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217477"
---
# <a name="wfp-user-mode-management-functions"></a>WFP 用户模式管理函数

在从标注驱动程序调用时，Windows 筛选平台用户模式管理函数的语义与从用户模式应用程序调用时完全相同，不同之处在于返回类型是 **NTSTATUS** 代码而不是 Win32 错误代码。 

这些函数记录在用户模式[WFP 函数](/windows/desktop/FWP/fwp-functions)文档的 "[管理函数](/windows/desktop/FWP/fwp-mgmt-functions)" 部分中。 

> [!NOTE]
> 每个函数的内核模式版本是在 fwpmk 中定义的。 Fwpmu 中定义了每个函数的用户模式版本。
 
除 [FwpmFreeMemory0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmfreememory0) 以外的所有这些函数的调用方必须在 IRQL = PASSIVE_LEVEL 上运行。 **FwpmFreeMemory0**的调用方必须以 IRQL <= DISPATCH_LEVEL 运行。

## <a name="callout-management"></a>标注管理

- [FwpmCalloutAdd0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmcalloutadd0) 
- [FwpmCalloutCreateEnumHandle0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmcalloutcreateenumhandle0) 
- [FwpmCalloutDeleteById0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmcalloutdeletebyid0) 
- [FwpmCalloutDeleteByKey0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmcalloutdeletebykey0) 
- [FwpmCalloutDestroyEnumHandle0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmcalloutdestroyenumhandle0) 
- [FwpmCalloutEnum0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmcalloutenum0) 
- [FwpmCalloutGetById0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmcalloutgetbyid0) 
- [FwpmCalloutGetByKey0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmcalloutgetbykey0) 
- [FwpmCalloutGetSecurityInfoByKey0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmcalloutgetsecurityinfobykey0) 
- [FwpmCalloutSetSecurityInfoByKey0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmcalloutsetsecurityinfobykey0) 

## <a name="connection-object-management"></a>连接对象管理

- [FwpmConnectionCreateEnumHandle0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmconnectioncreateenumhandle0) 
- [FwpmConnectionDestroyEnumHandle0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmconnectiondestroyenumhandle0) 
- [FwpmConnectionEnum0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmconnectionenum0) 
- [FwpmConnectionGetById0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmconnectiongetbyid0) 
- [FwpmConnectionGetSecurityInfo0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmconnectiongetsecurityinfo0) 
- [FwpmConnectionSetSecurityInfo0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmconnectionsetsecurityinfo0) 

## <a name="event-management"></a>事件管理

- [FwpmNetEventCreateEnumHandle0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmneteventcreateenumhandle0) 
- [FwpmNetEventDestroyEnumHandle0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmneteventdestroyenumhandle0) 
- FwpmNetEventEnum:
    - [FwpmNetEventEnum0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmneteventenum0) (Windows Vista) 
    - [FwpmNetEventEnum1](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmneteventenum1) (Windows 7) 
    - [FwpmNetEventEnum2](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmneteventenum2) (Windows 8) 
- [FwpmNetEventsGetSecurityInfo0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmneteventsgetsecurityinfo0) 
- [FwpmNetEventsSetSecurityInfo0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmneteventssetsecurityinfo0) 

## <a name="filter-management"></a>筛选器管理

- [FwpmFilterAdd0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmfilteradd0) 
- [FwpmFilterCreateEnumHandle0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmfiltercreateenumhandle0) 
- [FwpmFilterDeleteById0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmfilterdeletebyid0) 
- [FwpmFilterDeleteByKey0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmfilterdeletebykey0) 
- [FwpmFilterDestroyEnumHandle0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmfilterdestroyenumhandle0) 
- [FwpmFilterEnum0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmfilterenum0) 
- [FwpmFilterGetById0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmfiltergetbyid0) 
- [FwpmFilterGetByKey0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmfiltergetbykey0) 
- [FwpmFilterGetSecurityInfoByKey0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmfiltergetsecurityinfobykey0) 
- [FwpmFilterSetSecurityInfoByKey0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmfiltersetsecurityinfobykey0) 

## <a name="layer-management"></a>层管理

- [FwpmLayerCreateEnumHandle0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmlayercreateenumhandle0) 
- [FwpmLayerDestroyEnumHandle0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmlayerdestroyenumhandle0) 
- [FwpmLayerEnum0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmlayerenum0) 
- [FwpmLayerGetById0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmlayergetbyid0) 
- [FwpmLayerGetByKey0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmlayergetbykey0) 
- [FwpmLayerGetSecurityInfoByKey0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmlayergetsecurityinfobykey0) 
- [FwpmLayerSetSecurityInfoByKey0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmlayersetsecurityinfobykey0) 

## <a name="provider-context-management"></a>提供程序上下文管理

- [FwpmProviderContextAdd:
    - [FwpmProviderContextAdd0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidercontextadd0) (Windows Vista) 
    - [FwpmProviderContextAdd1](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidercontextadd1) (Windows 7) 
    - [FwpmProviderContextAdd2](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidercontextadd2) (Windows 8) 
- [FwpmProviderContextCreateEnumHandle0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidercontextcreateenumhandle0) 
- [FwpmProviderContextDeleteById0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidercontextdeletebyid0) 
- [FwpmProviderContextDeleteByKey0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidercontextdeletebykey0) 
- [FwpmProviderContextDestroyEnumHandle0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidercontextdestroyenumhandle0) 
- FwpmProviderContextEnum:
    - [FwpmProviderContextEnum0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidercontextenum0) (Windows Vista) 
    - [FwpmProviderContextEnum1](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidercontextenum1) (Windows 7) 
    - [FwpmProviderContextEnum2](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidercontextenum2) (Windows 8) 
- FwpmProviderContextGetById:
    - [FwpmProviderContextGetById0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidercontextgetbyid0) (Windows Vista) 
    - [FwpmProviderContextGetById1](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidercontextgetbyid1) (Windows 7) 
    - [FwpmProviderContextGetById2](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidercontextgetbyid2) (Windows 8) 
- FwpmProviderContextGetByKey:
    - [FwpmProviderContextGetByKey0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidercontextgetbykey0) (Windows Vista) 
    - [FwpmProviderContextGetByKey1](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidercontextgetbykey1) (Windows 7) 
    - [FwpmProviderContextGetByKey2](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidercontextgetbykey2) (Windows 8) 
- [FwpmProviderContextGetSecurityInfoByKey0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidercontextgetsecurityinfobykey0) 
- [FwpmProviderContextSetSecurityInfoByKey0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidercontextsetsecurityinfobykey0) 

## <a name="provider-management"></a>提供程序管理

- [FwpmProviderAdd0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovideradd0) 
- [FwpmProviderCreateEnumHandle0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidercreateenumhandle0) 
- [FwpmProviderDeleteByKey0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmproviderdeletebykey0) 
- [FwpmProviderDestroyEnumHandle0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmproviderdestroyenumhandle0) 
- [FwpmProviderEnum0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmproviderenum0) 
- [FwpmProviderGetByKey0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidergetbykey0) 
- [FwpmProviderGetSecurityInfoByKey0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidergetsecurityinfobykey0) 
- [FwpmProviderSetSecurityInfoByKey0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidersetsecurityinfobykey0) 

## <a name="session-management"></a>会话管理

- [FwpmEngineClose0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmengineclose0) 
- [FwpmEngineGetOption0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmenginegetoption0) 
- [FwpmEngineGetSecurityInfo0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmenginegetsecurityinfo0) 
- [FwpmEngineOpen0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmengineopen0) 
- [FwpmEngineSetOption0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmenginesetoption0) 
- [FwpmEngineSetSecurityInfo0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmenginesetsecurityinfo0) 
- [FwpmSessionCreateEnumHandle0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmsessioncreateenumhandle0) 
- [FwpmSessionDestroyEnumHandle0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmsessiondestroyenumhandle0) 
- [FwpmSessionEnum0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmsessionenum0) 

## <a name="sublayer-management"></a>子层管理

- [FwpmSubLayerAdd0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmsublayeradd0) 
- [FwpmSubLayerCreateEnumHandle0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmsublayercreateenumhandle0) 
- [FwpmSubLayerDeleteByKey0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmsublayerdeletebykey0) 
- [FwpmSubLayerDestroyEnumHandle0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmsublayerdestroyenumhandle0) 
- [FwpmSubLayerEnum0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmsublayerenum0) 
- [FwpmSubLayerGetByKey0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmsublayergetbykey0) 
- [FwpmSubLayerGetSecurityInfoByKey0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmsublayergetsecurityinfobykey0) 
- [FwpmSubLayerSetSecurityInfoByKey0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmsublayersetsecurityinfobykey0) 

## <a name="transaction-management"></a>事务管理

- [FwpmTransactionAbort0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmtransactionabort0) 
- [FwpmTransactionBegin0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmtransactionbegin0) 
- [FwpmTransactionCommit0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmtransactioncommit0) 

## <a name="vswitch-management"></a>vSwitch 管理

- [FwpmvSwitchEventsGetSecurityInfo0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmvswitcheventsgetsecurityinfo0) 
- [FwpmvSwitchEventsSetSecurityInfo0](/windows/desktop/api/fwpmu/nf-fwpmu-fwpmvswitcheventssetsecurityinfo0)