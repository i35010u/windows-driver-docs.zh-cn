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
ms.openlocfilehash: d068cb31d80a16df8c9049b6b632b3ad0752ff2e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375978"
---
# <a name="managing-contexts"></a>管理上下文


筛选器管理器使微筛选器驱动程序，以将上下文与要在 I/O 操作之间保留状态的对象相关联。 可以具有上下文的对象包括卷、 实例、 流和流句柄。

必须使用第三方文件系统[ **FSRTL\_高级\_FCB\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_fsrtl_advanced_fcb_header)结构 (而不是[ **FSRTL\_常见\_FCB\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_fsrtl_common_fcb_header)结构) 若要正常使用流和流处理上下文。

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

[**FltAllocateContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltallocatecontext)

[**FltRegisterFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltregisterfilter)

[**FltSetInstanceContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltsetinstancecontext)

[**FltSetStreamContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltsetstreamcontext)

[**FltSetStreamHandleContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltsetstreamhandlecontext)

[**FltSetVolumeContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltsetvolumecontext)

下面的例程提供用于查询上下文支持：

[**FltSupportsStreamContexts**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltsupportsstreamcontexts)

[**FltSupportsStreamHandleContexts**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltsupportsstreamhandlecontexts)

下面的例程提供用于获取和引用上下文：

[**FltGetContexts**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltgetcontexts)

[**FltGetInstanceContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltgetinstancecontext)

[**FltGetStreamContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltgetstreamcontext)

[**FltGetStreamHandleContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltgetstreamhandlecontext)

[**FltGetVolumeContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltgetvolumecontext)

[**FltReferenceContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltreferencecontext)

下面的例程提供用于发布和删除上下文：

[**FltDeleteContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltdeletecontext)

[**FltDeleteInstanceContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltdeleteinstancecontext)

[**FltDeleteStreamContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltdeletestreamcontext)

[**FltDeleteStreamHandleContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltdeletestreamhandlecontext)

[**FltDeleteVolumeContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltdeletevolumecontext)

[**FltReleaseContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltreleasecontext)

[**FltReleaseContexts**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltreleasecontexts)

### <a name="span-idminifilterdrivercallbackroutinesforcontextmanagementspanspan-idminifilterdrivercallbackroutinesforcontextmanagementspanspan-idminifilterdrivercallbackroutinesforcontextmanagementspanminifilter-driver-callback-routines-for-context-management"></a><span id="Minifilter_Driver_Callback_Routines_for_Context_Management"></span><span id="minifilter_driver_callback_routines_for_context_management"></span><span id="MINIFILTER_DRIVER_CALLBACK_ROUTINES_FOR_CONTEXT_MANAGEMENT"></span>用于上下文管理的微筛选器驱动程序回调例程

下面的回调例程都存储在[ **FLT\_注册**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_registration)作为参数传递的结构[ **FltRegisterFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltregisterfilter)微筛选器驱动程序的管理上下文：

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_context_allocate_callback" data-raw-source="[&lt;strong&gt;PFLT_CONTEXT_ALLOCATE_CALLBACK&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_context_allocate_callback)"><strong>PFLT_CONTEXT_ALLOCATE_CALLBACK</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><em>ContextCleanupCallback</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_context_cleanup_callback" data-raw-source="[&lt;strong&gt;PFLT_CONTEXT_CLEANUP_CALLBACK&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_context_cleanup_callback)"><strong>PFLT_CONTEXT_CLEANUP_CALLBACK</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>ContextFreeCallback</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_context_free_callback" data-raw-source="[&lt;strong&gt;PFLT_CONTEXT_FREE_CALLBACK&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_context_free_callback)"><strong>PFLT_CONTEXT_FREE_CALLBACK</strong></a></p></td>
</tr>
</tbody>
</table>

 

 

 




