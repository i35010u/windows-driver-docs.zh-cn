---
title: 'Irql \_ 杂项 \_ 函数规则 (ndis) '
description: Irql \_ 杂项 \_ 函数规则指定必须在正确的 Irql 级别调用 NDIS 函数。
ms.assetid: ae1d0243-1db9-428f-a112-f438e2322ff2
ms.date: 05/21/2018
keywords:
- 'Irql_Miscellaneous_Function 规则 (ndis) '
topic_type:
- apiref
api_name:
- Irql_Miscellaneous_Function
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b9bfc70a4c22561db7496c0283b2a5e3a22a66f3
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89384915"
---
# <a name="irql_miscellaneous_function-rule-ndis"></a>Irql \_ 杂项 \_ 函数规则 (ndis) 


Irql \_ 杂项 \_ 函数规则指定必须在正确的 Irql 级别调用 NDIS 函数。

此规则验证以下功能：

**KeGetCurrentProcessorNumber** 
**NdisAllocateFromNPagedLookasideList** 
**NdisAllocateGenericObject** 
**NdisAllocateIoWorkItem** 
**NdisAllocateMemoryWithTagPriority** 
**NdisAnsiStringToUnicodeString** 
**NdisCloseConfiguration** 
**NdisCloseFile** 
**NdisDeleteNPagedLookasideList** 
**NdisDeregisterDeviceEx** 
**NdisEqualMemory** 
**NdisEqualUnicodeString** 
**NdisFreeGenericObject** 
**NdisFreeIoWorkItem** 
**NdisFreeMemory** 
**NdisFreeSpinLock** 
**NdisFreeString** 
**NdisFreeToNPagedLookasideList** 
**NdisGeneratePartialCancelId** 
**NdisGetCurrentProcessorCounts** 
**NdisGetDriverHandle** 
**NdisGetRoutineAddress** 
**NdisGetSharedDataAlignment** 
**NdisGetVersion** 
**NdisInitAnsiString** 
**NdisInitializeListHead** 
**NdisInitializeNPagedLookasideList** 
**NdisInitializeSListHead** 
**NdisInitializeString** 
**NdisInitUnicodeString** 
**NdisMapFile** 
**NdisOpenConfigurationEx** 
**NdisOpenConfigurationKeyByIndex** 
**NdisOpenConfigurationKeyByName** 
**NdisOpenFile** 
**NdisQueryAdapterInstanceName** 
**NdisQueryDepthSList** 
**NdisQueueIoWorkItem** 
**NdisReadConfiguration** 
**NdisReadNetworkAddress** 
**NdisReEnumerateProtocolBindings** 
**NdisSetOptionalHandlers** 
**NdisSystemProcessorCount** 
**NdisUnicodeStringToAnsiString** 
**NdisUnmapFile** 
**NdisUpcaseUnicodeString** 
**NdisWaitEvent** 
**NdisWriteConfiguration** 
**NdisWriteErrorLogEntry** 
**NdisWriteEventLogEntry**

**驱动程序模型： NDIS**

<a name="how-to-test"></a>如何测试
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">在编译时</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>运行 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>Irql_Miscellaneous_Function</strong> 规则。</p>
使用以下步骤来运行代码分析：
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](./using-static-driver-verifier-to-find-defects-in-drivers.md#preparing-your-source-code)">准备你的代码 (使用) 的角色类型声明。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](./using-static-driver-verifier-to-find-defects-in-drivers.md#running-static-driver-verifier)">运行静态驱动程序验证程序。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](./using-static-driver-verifier-to-find-defects-in-drivers.md#viewing-and-analyzing-the-results)">查看并分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](./using-static-driver-verifier-to-find-defects-in-drivers.md)">使用静态驱动程序验证器查找驱动程序中的缺陷</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用于
----------

[**NdisAllocateFromNPagedLookasideList**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatefromnpagedlookasidelist)  
[**NdisAllocateGenericObject**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocategenericobject)  
[**NdisAllocateIoWorkItem**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocateioworkitem)  
[**NdisAllocateMemoryWithTagPriority**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatememorywithtagpriority)  
[**NdisAnsiStringToUnicodeString**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisansistringtounicodestring)  
[**NdisCloseConfiguration**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscloseconfiguration)  
[**NdisCloseFile**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclosefile)  
[**NdisDeleteNPagedLookasideList**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisdeletenpagedlookasidelist)  
[**NdisDeregisterDeviceEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisderegisterdeviceex)  
[**NdisEqualMemory**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisequalmemory)  
[**NdisEqualString**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisequalstring)  
[**NdisEqualUnicodeString**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisequalunicodestring)  
[**NdisFreeGenericObject**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreegenericobject)  
[**NdisFreeIoWorkItem**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreeioworkitem)  
[**NdisFreeMemory**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreememory)  
[**NdisFreeString**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreestring)  
[**NdisFreeToNPagedLookasideList**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreetonpagedlookasidelist)  
[**NdisGeneratePartialCancelId**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgeneratepartialcancelid)  
[**NdisGetCurrentProcessorCounts**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgetcurrentprocessorcounts)  
[**NdisGetRoutineAddress**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgetroutineaddress)  
[**NdisGetSharedDataAlignment**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgetshareddataalignment)  
[**NdisGetVersion**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgetversion)  
[**NdisInitAnsiString**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisinitansistring)  
[**NdisInitializeNPagedLookasideList**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisinitializenpagedlookasidelist)  
[**NdisInitializeString**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisinitializestring)  
[**NdisInitUnicodeString**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisinitunicodestring)  
[**NdisMapFile**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismapfile)  
[**NdisOpenConfigurationEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisopenconfigurationex)  
[**NdisOpenConfigurationKeyByIndex**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisopenconfigurationkeybyindex)  
[**NdisOpenConfigurationKeyByName**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisopenconfigurationkeybyname)  
[**NdisOpenFile**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisopenfile)  
[**NdisQueryAdapterInstanceName**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisqueryadapterinstancename)  
[**NdisQueryDepthSList**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisquerydepthslist)  
[**NdisQueueIoWorkItem**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisqueueioworkitem)  
[**NdisReadConfiguration**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreadconfiguration)  
[**NdisReadNetworkAddress**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreadnetworkaddress)  
[**NdisReEnumerateProtocolBindings**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreenumerateprotocolbindings)  
[**NdisRegisterDeviceEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisregisterdeviceex)  
[**NdisSetOptionalHandlers**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissetoptionalhandlers)  
[**NdisSystemProcessorCount**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissystemprocessorcount)  
[**NdisUnicodeStringToAnsiString**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisunicodestringtoansistring)  
[**NdisUnmapFile**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisunmapfile)  
[**NdisUpcaseUnicodeString**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisupcaseunicodestring)  
[**NdisWaitEvent**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiswaitevent)  
[**NdisWriteConfiguration**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiswriteconfiguration)  
[**NdisWriteErrorLogEntry**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiswriteerrorlogentry)  
[**NdisWriteEventLogEntry**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiswriteeventlogentry)  
[**KeGetCurrentProcessorNumber**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-kegetcurrentprocessornumber)