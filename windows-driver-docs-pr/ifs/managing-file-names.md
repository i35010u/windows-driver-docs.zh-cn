---
title: 管理文件名称
description: 管理文件名称
ms.assetid: 390c3817-e306-4d20-9ec0-9d68ccc8ff1b
keywords:
- 筛选器管理器 WDK 文件系统微筛选器，文件的名称
- 文件名称 WDK 文件系统微筛选器
- 名称 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e49472487be997520fac5bd3d98960ed81d8a48
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357549"
---
# <a name="managing-file-names"></a>管理文件名称


筛选器管理器来减少你的旧的筛选器驱动程序以检索和管理文件的名称所需的工作。 筛选器管理器名称请求时，当前操作提供适当的格式中的引用计数结构中的名称： 规范化名称、 打开的名称或短名称。

微筛选器驱动程序可以调用[ **FltGetDestinationFileNameInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff543003)构造的文件或目录要重命名或为其正在 NTFS 硬链接的完整目标路径名称创建。 此名称可以规范化或打开文件的格式返回。

筛选器管理器还提供了[ **FltGetTunneledName** ](https://msdn.microsoft.com/library/windows/hardware/ff543177)例程用于检索规范化文件名称隧道由于失效的文件名称信息。

若要提高性能，筛选器管理器将放名称在缓存中 （如果可能） 系统中所有微筛选器驱动程序之间共享。 缓存和/或文件系统中，可以查询微筛选器驱动程序。

修改命名空间的微筛选器驱动程序可以利用的筛选器管理器的支持提供商通过注册回调例程以截获名称查询操作，例如由上部微筛选器驱动程序生成或规范化名称的请求。

### <a name="span-idfiltermanagerroutinesfornamemanagementspanspan-idfiltermanagerroutinesfornamemanagementspanspan-idfiltermanagerroutinesfornamemanagementspanfilter-manager-routines-for-name-management"></a><span id="Filter_Manager_Routines_for_Name_Management"></span><span id="filter_manager_routines_for_name_management"></span><span id="FILTER_MANAGER_ROUTINES_FOR_NAME_MANAGEMENT"></span>筛选器的名称管理的管理器例程

筛选器管理器名称管理提供以下支持例程：

[**FltGetDestinationFileNameInformation**](https://msdn.microsoft.com/library/windows/hardware/ff543003)

[**FltGetFileNameInformation**](https://msdn.microsoft.com/library/windows/hardware/ff543032)

[**FltGetFileNameInformationUnsafe**](https://msdn.microsoft.com/library/windows/hardware/ff543035)

[**FltGetTunneledName**](https://msdn.microsoft.com/library/windows/hardware/ff543177)

[**FltParseFileNameInformation**](https://msdn.microsoft.com/library/windows/hardware/ff543417)

[**FltReleaseFileNameInformation**](https://msdn.microsoft.com/library/windows/hardware/ff544320)

### <a name="span-idminifilterdrivercallbackroutinesfornamemanagementspanspan-idminifilterdrivercallbackroutinesfornamemanagementspanspan-idminifilterdrivercallbackroutinesfornamemanagementspanminifilter-driver-callback-routines-for-name-management"></a><span id="Minifilter_Driver_Callback_Routines_for_Name_Management"></span><span id="minifilter_driver_callback_routines_for_name_management"></span><span id="MINIFILTER_DRIVER_CALLBACK_ROUTINES_FOR_NAME_MANAGEMENT"></span>名称管理的微筛选器驱动程序回调例程

下面的回调例程都存储在[ **FLT\_注册**](https://msdn.microsoft.com/library/windows/hardware/ff544811)作为参数传递的结构[ **FltRegisterFilter** ](https://msdn.microsoft.com/library/windows/hardware/ff544305)，修改命名空间的微筛选器驱动程序：

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551087" data-raw-source="[&lt;strong&gt;PFLT_GENERATE_FILE_NAME&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551087)"><strong>PFLT_GENERATE_FILE_NAME</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><em>NormalizeContextCleanupCallback</em></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551100" data-raw-source="[&lt;strong&gt;PFLT_NORMALIZE_CONTEXT_CLEANUP&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551100)"><strong>PFLT_NORMALIZE_CONTEXT_CLEANUP</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>NormalizeNameComponentCallback</em></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551102" data-raw-source="[&lt;strong&gt;PFLT_NORMALIZE_NAME_COMPONENT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551102)"><strong>PFLT_NORMALIZE_NAME_COMPONENT</strong></a></p></td>
</tr>
</tbody>
</table>

 

 

 




