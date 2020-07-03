---
title: Irql \_ 杂项 \_ 函数规则（ndis）
description: Irql \_ 杂项 \_ 函数规则指定必须在正确的 Irql 级别调用 NDIS 函数。
ms.assetid: ae1d0243-1db9-428f-a112-f438e2322ff2
ms.date: 05/21/2018
keywords:
- Irql_Miscellaneous_Function 规则（ndis）
topic_type:
- apiref
api_name:
- Irql_Miscellaneous_Function
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 29447d9125eddb33f4ed497ac56ebe504527b3f7
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916530"
---
# <a name="irql_miscellaneous_function-rule-ndis"></a>Irql \_ 杂项 \_ 函数规则（ndis）


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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>Irql_Miscellaneous_Function</strong>规则。</p>
使用以下步骤来运行代码分析：
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">准备你的代码（使用角色类型声明）。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">运行静态驱动程序验证程序。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">查看并分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">使用静态驱动程序验证器查找驱动程序中的缺陷</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用于
----------

[**NdisAllocateFromNPagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatefromnpagedlookasidelist)  
[**NdisAllocateGenericObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocategenericobject)  
[**NdisAllocateIoWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocateioworkitem)  
[**NdisAllocateMemoryWithTagPriority**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatememorywithtagpriority)  
[**NdisAnsiStringToUnicodeString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisansistringtounicodestring)  
[**NdisCloseConfiguration**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscloseconfiguration)  
[**NdisCloseFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclosefile)  
[**NdisDeleteNPagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisdeletenpagedlookasidelist)  
[**NdisDeregisterDeviceEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisderegisterdeviceex)  
[**NdisEqualMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisequalmemory)  
[**NdisEqualString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisequalstring)  
[**NdisEqualUnicodeString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisequalunicodestring)  
[**NdisFreeGenericObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreegenericobject)  
[**NdisFreeIoWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreeioworkitem)  
[**NdisFreeMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreememory)  
[**NdisFreeString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreestring)  
[**NdisFreeToNPagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreetonpagedlookasidelist)  
[**NdisGeneratePartialCancelId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgeneratepartialcancelid)  
[**NdisGetCurrentProcessorCounts**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgetcurrentprocessorcounts)  
[**NdisGetRoutineAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgetroutineaddress)  
[**NdisGetSharedDataAlignment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgetshareddataalignment)  
[**NdisGetVersion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgetversion)  
[**NdisInitAnsiString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisinitansistring)  
[**NdisInitializeNPagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisinitializenpagedlookasidelist)  
[**NdisInitializeString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisinitializestring)  
[**NdisInitUnicodeString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisinitunicodestring)  
[**NdisMapFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismapfile)  
[**NdisOpenConfigurationEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisopenconfigurationex)  
[**NdisOpenConfigurationKeyByIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisopenconfigurationkeybyindex)  
[**NdisOpenConfigurationKeyByName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisopenconfigurationkeybyname)  
[**NdisOpenFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisopenfile)  
[**NdisQueryAdapterInstanceName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisqueryadapterinstancename)  
[**NdisQueryDepthSList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisquerydepthslist)  
[**NdisQueueIoWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisqueueioworkitem)  
[**NdisReadConfiguration**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreadconfiguration)  
[**NdisReadNetworkAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreadnetworkaddress)  
[**NdisReEnumerateProtocolBindings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreenumerateprotocolbindings)  
[**NdisRegisterDeviceEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisregisterdeviceex)  
[**NdisSetOptionalHandlers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissetoptionalhandlers)  
[**NdisSystemProcessorCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissystemprocessorcount)  
[**NdisUnicodeStringToAnsiString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisunicodestringtoansistring)  
[**NdisUnmapFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisunmapfile)  
[**NdisUpcaseUnicodeString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisupcaseunicodestring)  
[**NdisWaitEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiswaitevent)  
[**NdisWriteConfiguration**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiswriteconfiguration)  
[**NdisWriteErrorLogEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiswriteerrorlogentry)  
[**NdisWriteEventLogEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiswriteeventlogentry)  
[**KeGetCurrentProcessorNumber**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-kegetcurrentprocessornumber)  








