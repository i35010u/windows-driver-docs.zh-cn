---
title: FSCTL_SET_REPARSE_POINT_EX 控制代码
description: FSCTL_SET_REPARSE_POINT_EX 控制代码上的文件或目录设置重分析点。
tech.root: ''
ms.assetid: 5867cbe3-5aab-43f8-b5bf-eaa29857359f
keywords:
- FSCTL_SET_REPARSE_POINT_EX 控制代码可安装文件系统驱动程序
topic_type:
- apiref
api_name:
- FSCTL_SET_REPARSE_POINT_EX
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 05/31/2019
ms.localizationpriority: medium
ms.openlocfilehash: 459efeede95677838391c5f4c918a900d2c3f8f6
ms.sourcegitcommit: 2b60304fb0e33fd978ae01be95d04321a0af09b5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/06/2019
ms.locfileid: "66748455"
---
# <a name="fsctlsetreparsepointex-control-code"></a>FSCTL_SET_REPARSE_POINT_EX 控制代码

FSCTL_SET_REPARSE_POINT_EX 控制代码上的文件或目录设置重分析点。

微筛选器应使用[ **FltTagFileEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-flttagfileex)而不是 FSCTL_SET_REPARSE_POINT_EX 设置重分析点。

有关重新分析点的详细信息，请参阅 Microsoft Windows SDK 文档。

若要执行此操作，调用[ **ZwFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntfscontrolfile)使用以下参数。

## <a name="parameters"></a>Parameters

*FileHandle*  
文件或目录在其上设置重分析点的文件句柄。 此参数是必需的不能**NULL**。

*事件*不用于此操作; 设置为**NULL**。

*ApcRoutine*不用于此操作; 设置为**NULL**。

*ApcContext*不用于此操作; 设置为**NULL**。

*IoStatusBlock*向 IO_STATUS_BLOCK 结构接收最终的完成状态和操作的相关信息的指针。

*FsControlCode*  
操作的控制代码。 FSCTL_SET_REPARSE_POINT_EX 用于此操作。

*InputBuffer*  
指向调用方分配[REPARSE_DATA_BUFFER_EX](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_reparse_data_buffer_ex)结构，其中包含重新分析点数据。

*InputBufferLength*  
大小 （字节），指向的缓冲区*InputBuffer*参数。 此值必须至少为 REPARSE_GUID_DATA_BUFFER_HEADER_SIZE，加上用户定义的数据，和它的大小必须小于或等于 MAXIMUM_REPARSE_DATA_BUFFER_SIZE。

*OutputBuffer*  
不用于此操作;设置为**NULL**。

*OutputBufferLength*  
不用于此操作;设置为零。

<a name="status-block"></a>状态块
------------
[**ZwFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntfscontrolfile)返回 STATUS_SUCCESS 或适当的 NTSTATUS 值如以下之一：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">术语</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>STATUS_DIRECTORY_NOT_EMPTY</strong></p></td>
<td align="left"><p>不能对非空的目录设置重分析点。 这是一个错误代码。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_EAS_NOT_SUPPORTED</strong></p></td>
<td align="left"><p>如果此请求是在事务中，无法对文件设置重分析点。 这是一个错误代码。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_IO_REPARSE_DATA_INVALID</strong></p></td>
<td align="left"><p>其中一个指定的参数值无效。 这是一个错误代码。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_IO_REPARSE_TAG_MISMATCH</strong></p></td>
<td align="left"><p>指定由调用方重分析标记与要修改的重新分析点标记不匹配。 这是一个错误代码。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_NOT_A_REPARSE_POINT</strong></p></td>
<td align="left"><p>文件或目录不是一个重新分析点。 这是一个错误代码。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_REPARSE_ATTRIBUTE_CONFLICT</strong></p></td>
<td align="left"><p>重分析点是第三方重分析点，并重新分析由调用方指定的 GUID 与要修改的重新分析点 GUID 不匹配。 这是一个错误代码。</p></td>
</tr>
</tbody>
</table>

## <a name="requirements"></a>要求
------------
<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ntifs.h （包括 Ntifs.h 或 Fltkernel.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅

[**有关 IRP_MJ_FILE_SYSTEM_CONTROL FLT_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ifs/flt-parameters-for-irp-mj-file-system-control)

[**FltTagFileEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-flttagfileex)

[**FltUntagFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltuntagfile)

[**FSCTL\_DELETE\_REPARSE\_POINT**](fsctl-delete-reparse-point.md)

[**FSCTL\_GET\_REPARSE\_POINT**](fsctl-get-reparse-point.md)

[**IRP\_MJ\_文件\_系统\_控件**](irp-mj-file-system-control.md)

[**IsReparseTagMicrosoft**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-isreparsetagmicrosoft)

[**IsReparseTagNameSurrogate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-isreparsetagnamesurrogate)

[**重新分析\_数据\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_reparse_data_buffer_ex)

[**REPARSE\_GUID\_DATA\_BUFFER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_reparse_guid_data_buffer)

[**ZwFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntfscontrolfile)