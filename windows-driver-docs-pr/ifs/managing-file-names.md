---
title: 管理文件名称
description: 管理文件名称
ms.assetid: 390c3817-e306-4d20-9ec0-9d68ccc8ff1b
keywords:
- 筛选器管理器 WDK 文件系统微筛选器，文件名
- 文件名称 WDK 文件系统微筛选器
- 命名 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: af6e56f3585fd618d18091c3783869c8f8f19c53
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841128"
---
# <a name="managing-file-names"></a>管理文件名称


筛选器管理器消除了旧筛选器驱动程序检索和管理文件名所需的大部分工作。 当请求名称时，筛选器管理器会以适用于当前操作的适当格式在引用计数结构中提供名称：规范化名称、已打开名称或短名称。

微筛选器驱动程序可以调用[**FltGetDestinationFileNameInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetdestinationfilenameinformation)来构造要重命名或正在为其创建 NTFS 硬链接的文件或目录的完整目标路径名。 此名称可以以规范化或打开的格式返回。

筛选器管理器还提供了[**FltGetTunneledName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgettunneledname)例程，用于检索因文件名隧道而失效的规范化文件名信息。

为了提高性能，筛选器管理器会在系统中的所有微筛选器驱动程序之间共享名称（如果可能）。 微筛选器驱动程序可以查询缓存或文件系统，或同时查询两者。

修改命名空间的微筛选器驱动程序可以通过注册回调例程来截获名称查询操作（例如，由大小写微筛选器驱动程序来生成或规范化名称）来利用筛选器管理器对名称提供程序的支持。

### <a name="span-idfilter_manager_routines_for_name_managementspanspan-idfilter_manager_routines_for_name_managementspanspan-idfilter_manager_routines_for_name_managementspanfilter-manager-routines-for-name-management"></a><span id="Filter_Manager_Routines_for_Name_Management"></span><span id="filter_manager_routines_for_name_management"></span><span id="FILTER_MANAGER_ROUTINES_FOR_NAME_MANAGEMENT"></span>用于名称管理的筛选器管理器例程

筛选器管理器为名称管理提供以下支持例程：

[**FltGetDestinationFileNameInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetdestinationfilenameinformation)

[**FltGetFileNameInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetfilenameinformation)

[**FltGetFileNameInformationUnsafe**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetfilenameinformationunsafe)

[**FltGetTunneledName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgettunneledname)

[**FltParseFileNameInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltparsefilenameinformation)

[**FltReleaseFileNameInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltreleasefilenameinformation)

### <a name="span-idminifilter_driver_callback_routines_for_name_managementspanspan-idminifilter_driver_callback_routines_for_name_managementspanspan-idminifilter_driver_callback_routines_for_name_managementspanminifilter-driver-callback-routines-for-name-management"></a><span id="Minifilter_Driver_Callback_Routines_for_Name_Management"></span><span id="minifilter_driver_callback_routines_for_name_management"></span><span id="MINIFILTER_DRIVER_CALLBACK_ROUTINES_FOR_NAME_MANAGEMENT"></span>名称管理的微筛选器驱动程序回调例程

对于修改命名空间的微微筛选器驱动程序，以下回调例程存储在作为参数传递给[**FltRegisterFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltregisterfilter)的[**FLT\_注册**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_registration)结构中：

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
<td align="left"><p><em>GenerateFileNameCallback</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_generate_file_name" data-raw-source="[&lt;strong&gt;PFLT_GENERATE_FILE_NAME&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_generate_file_name)"><strong>PFLT_GENERATE_FILE_NAME</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><em>NormalizeContextCleanupCallback</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_normalize_context_cleanup" data-raw-source="[&lt;strong&gt;PFLT_NORMALIZE_CONTEXT_CLEANUP&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_normalize_context_cleanup)"><strong>PFLT_NORMALIZE_CONTEXT_CLEANUP</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>NormalizeNameComponentCallback</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_normalize_name_component" data-raw-source="[&lt;strong&gt;PFLT_NORMALIZE_NAME_COMPONENT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_normalize_name_component)"><strong>PFLT_NORMALIZE_NAME_COMPONENT</strong></a></p></td>
</tr>
</tbody>
</table>

 

 

 




