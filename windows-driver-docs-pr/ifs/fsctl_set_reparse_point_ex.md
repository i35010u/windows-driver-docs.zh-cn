---
title: FSCTL_SET_REPARSE_POINT_EX 控制代码
description: FSCTL_SET_REPARSE_POINT_EX 控制代码设置文件或目录中的重新分析点。
tech.root: ''
ms.assetid: 5867cbe3-5aab-43f8-b5bf-eaa29857359f
keywords:
- FSCTL_SET_REPARSE_POINT_EX 控制代码可安装的文件系统驱动程序
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
ms.openlocfilehash: 44801354f6c37c8540b9e88ca50420f97f782b2c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841237"
---
# <a name="fsctl_set_reparse_point_ex-control-code"></a>FSCTL_SET_REPARSE_POINT_EX 控制代码

FSCTL_SET_REPARSE_POINT_EX 控制代码设置文件或目录中的重新分析点。

Minifilters 应使用[**FltTagFileEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-flttagfileex)而不是 FSCTL_SET_REPARSE_POINT_EX 来设置重新分析点。

有关重新分析点的详细信息，请参阅 Microsoft Windows SDK 文档。

若要执行此操作，请调用具有以下参数的[**ZwFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntfscontrolfile) 。

## <a name="parameters"></a>参数

*FileHandle*  
要设置重新分析点的文件或目录的文件句柄。 此参数是必需的，不能为**NULL**。

*事件*不与此操作一起使用;设置为**NULL**。

*ApcRoutine*不与此操作一起使用;设置为**NULL**。

*ApcContext*不与此操作一起使用;设置为**NULL**。

*IoStatusBlock*指向 IO_STATUS_BLOCK 结构的指针，该结构接收最终完成状态和有关操作的信息。

*FsControlCode*  
操作的控制代码。 使用 FSCTL_SET_REPARSE_POINT_EX 进行此操作。

*InputBuffer*  
指向调用方分配的[REPARSE_DATA_BUFFER_EX](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_reparse_data_buffer_ex)结构的指针，该结构包含重新分析点数据。

*InputBufferLength*  
*InputBuffer*参数指向的缓冲区的大小（以字节为单位）。 此值必须至少为 REPARSE_GUID_DATA_BUFFER_HEADER_SIZE，加上用户定义数据的大小，并且必须小于或等于 MAXIMUM_REPARSE_DATA_BUFFER_SIZE。

*OutputBuffer*  
不与此操作一起使用;设置为**NULL**。

*OutputBufferLength*  
不与此操作一起使用;设置为零。

<a name="status-block"></a>状态块
------------
[**ZwFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntfscontrolfile)返回 STATUS_SUCCESS 或相应的 NTSTATUS 值，如下所示：

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
<td align="left"><p>不能对非空目录设置重新分析点。 这是一个错误代码。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_EAS_NOT_SUPPORTED</strong></p></td>
<td align="left"><p>如果此请求在事务中，则无法对文件设置重新分析点。 这是一个错误代码。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_IO_REPARSE_DATA_INVALID</strong></p></td>
<td align="left"><p>指定的参数值之一无效。 这是一个错误代码。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_IO_REPARSE_TAG_MISMATCH</strong></p></td>
<td align="left"><p>调用方指定的重新分析标记与要修改的重新分析点的标记不匹配。 这是一个错误代码。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_NOT_A_REPARSE_POINT</strong></p></td>
<td align="left"><p>文件或目录不是重新分析点。 这是一个错误代码。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_REPARSE_ATTRIBUTE_CONFLICT</strong></p></td>
<td align="left"><p>重新分析点是第三方重新分析点，调用方指定的重新分析 GUID 与要修改的重新分析点的 GUID 不匹配。 这是一个错误代码。</p></td>
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
<td align="left"><p>标头</p></td>
<td align="left">Ntifs （包括 Ntifs 或 Fltkernel）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅

[**IRP_MJ_FILE_SYSTEM_CONTROL 的 FLT_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ifs/flt-parameters-for-irp-mj-file-system-control)

[**FltTagFileEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-flttagfileex)

[**FltUntagFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltuntagfile)

[**FSCTL\_删除\_重新分析\_点**](fsctl-delete-reparse-point.md)

[**FSCTL\_获取\_重新分析\_点**](fsctl-get-reparse-point.md)

[**IRP\_MJ\_文件\_系统\_控件**](irp-mj-file-system-control.md)

[**IsReparseTagMicrosoft**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-isreparsetagmicrosoft)

[**IsReparseTagNameSurrogate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-isreparsetagnamesurrogate)

[ **\_缓冲区\_重新分析数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_reparse_data_buffer_ex)

[ **\_数据\_缓冲区中的重新分析\_GUID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_reparse_guid_data_buffer)

[**ZwFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntfscontrolfile)