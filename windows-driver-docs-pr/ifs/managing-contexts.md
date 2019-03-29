---
title: 管理上下文
description: 管理上下文
ms.assetid: 1ad33c6c-a5dd-4b65-bfcc-a40453d3a6b5
keywords:
- 筛选器管理器 WDK 文件系统微筛选器上下文
- 文件系统微筛选器驱动程序 WDK，上下文
- 微筛选器驱动程序 WDK、 上下文
- 上下文 WDK 文件系统微筛选器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c65bbf49f48528bbf31fa3cf254a92fbcc2f4745
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568508"
---
# <a name="managing-contexts"></a>管理上下文


筛选器管理器使微筛选器驱动程序，以将上下文与要在 I/O 操作之间保留状态的对象相关联。 可以具有上下文的对象包括卷、 实例、 流和流句柄。

必须使用第三方文件系统[ **FSRTL\_高级\_FCB\_标头**](https://msdn.microsoft.com/library/windows/hardware/ff547334)结构 (而不是[ **FSRTL\_常见\_FCB\_标头**](https://msdn.microsoft.com/library/windows/hardware/ff547343)结构) 若要正常使用流和流处理上下文。

可以通过除卷上下文，必须从非分页缓冲池分配的分页或非分页池分配上下文。

已释放所有未完成的引用时，将自动释放上下文。 如果微筛选器驱动程序定义上下文清理回调例程，筛选器管理器将调用例程之前释放上下文。

筛选器管理器负责删除关联的对象时，分离时实例，并卸载微筛选器驱动程序时删除上下文。

如果微筛选器驱动程序支持每个卷只有一个实例，使用实例上下文而不是卷上下文，以提高性能。 此外可以通过将存储在流内的微筛选器驱动程序实例上下文或流句柄上下文的指针来提高性能。

上下文不支持的页面文件或在以下操作：

-   Preoperation 创建请求处理

-   Postoperation 处理关闭请求

-   处理 IRP\_MJ\_网络\_查询\_打开请求

请参阅有关使用上下文的微筛选器驱动程序的示例 CTX 示例。

### <a name="span-idfiltermanagerroutinesforcontextmanagementspanspan-idfiltermanagerroutinesforcontextmanagementspanspan-idfiltermanagerroutinesforcontextmanagementspanfilter-manager-routines-for-context-management"></a><span id="Filter_Manager_Routines_for_Context_Management"></span><span id="filter_manager_routines_for_context_management"></span><span id="FILTER_MANAGER_ROUTINES_FOR_CONTEXT_MANAGEMENT"></span>筛选上下文管理的管理器例程

筛选器管理器用于创建、 注册，并设置上下文提供以下支持例程：

[**FltAllocateContext**](https://msdn.microsoft.com/library/windows/hardware/ff541710)

[**FltRegisterFilter**](https://msdn.microsoft.com/library/windows/hardware/ff544305)

[**FltSetInstanceContext**](https://msdn.microsoft.com/library/windows/hardware/ff544521)

[**FltSetStreamContext**](https://msdn.microsoft.com/library/windows/hardware/ff544543)

[**FltSetStreamHandleContext**](https://msdn.microsoft.com/library/windows/hardware/ff544552)

[**FltSetVolumeContext**](https://msdn.microsoft.com/library/windows/hardware/ff544557)

下面的例程提供用于查询上下文支持：

[**FltSupportsStreamContexts**](https://msdn.microsoft.com/library/windows/hardware/ff544581)

[**FltSupportsStreamHandleContexts**](https://msdn.microsoft.com/library/windows/hardware/ff544586)

下面的例程提供用于获取和引用上下文：

[**FltGetContexts**](https://msdn.microsoft.com/library/windows/hardware/ff542997)

[**FltGetInstanceContext**](https://msdn.microsoft.com/library/windows/hardware/ff543058)

[**FltGetStreamContext**](https://msdn.microsoft.com/library/windows/hardware/ff543144)

[**FltGetStreamHandleContext**](https://msdn.microsoft.com/library/windows/hardware/ff543155)

[**FltGetVolumeContext**](https://msdn.microsoft.com/library/windows/hardware/ff543189)

[**FltReferenceContext**](https://msdn.microsoft.com/library/windows/hardware/ff544291)

下面的例程提供用于发布和删除上下文：

[**FltDeleteContext**](https://msdn.microsoft.com/library/windows/hardware/ff541960)

[**FltDeleteInstanceContext**](https://msdn.microsoft.com/library/windows/hardware/ff541982)

[**FltDeleteStreamContext**](https://msdn.microsoft.com/library/windows/hardware/ff541997)

[**FltDeleteStreamHandleContext**](https://msdn.microsoft.com/library/windows/hardware/ff542016)

[**FltDeleteVolumeContext**](https://msdn.microsoft.com/library/windows/hardware/ff542030)

[**FltReleaseContext**](https://msdn.microsoft.com/library/windows/hardware/ff544314)

[**FltReleaseContexts**](https://msdn.microsoft.com/library/windows/hardware/ff544317)

### <a name="span-idminifilterdrivercallbackroutinesforcontextmanagementspanspan-idminifilterdrivercallbackroutinesforcontextmanagementspanspan-idminifilterdrivercallbackroutinesforcontextmanagementspanminifilter-driver-callback-routines-for-context-management"></a><span id="Minifilter_Driver_Callback_Routines_for_Context_Management"></span><span id="minifilter_driver_callback_routines_for_context_management"></span><span id="MINIFILTER_DRIVER_CALLBACK_ROUTINES_FOR_CONTEXT_MANAGEMENT"></span>用于上下文管理的微筛选器驱动程序回调例程

下面的回调例程都存储在[ **FLT\_注册**](https://msdn.microsoft.com/library/windows/hardware/ff544811)作为参数传递的结构[ **FltRegisterFilter**](https://msdn.microsoft.com/library/windows/hardware/ff544305)微筛选器驱动程序的管理上下文：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">回调例程名称</th>
<th align="left">回调例程类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><em>ContextAllocateCallback</em></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551075" data-raw-source="[&lt;strong&gt;PFLT_CONTEXT_ALLOCATE_CALLBACK&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551075)"><strong>PFLT_CONTEXT_ALLOCATE_CALLBACK</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><em>ContextCleanupCallback</em></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551078" data-raw-source="[&lt;strong&gt;PFLT_CONTEXT_CLEANUP_CALLBACK&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551078)"><strong>PFLT_CONTEXT_CLEANUP_CALLBACK</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>ContextFreeCallback</em></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551082" data-raw-source="[&lt;strong&gt;PFLT_CONTEXT_FREE_CALLBACK&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551082)"><strong>PFLT_CONTEXT_FREE_CALLBACK</strong></a></p></td>
</tr>
</tbody>
</table>

 

 

 




