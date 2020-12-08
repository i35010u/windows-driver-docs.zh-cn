---
title: FSCTL_SET_REPARSE_POINT 控制代码
description: FSCTL \_ SET 重新 \_ 分析 \_ 点控制代码设置文件或目录的重新分析点。
keywords:
- FSCTL_SET_REPARSE_POINT 控制代码可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- FSCTL_SET_REPARSE_POINT
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3687dcc06a3b42f8513c8d5006824da0d2589882
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788713"
---
# <a name="fsctl_set_reparse_point-control-code"></a>FSCTL \_ 设置重新 \_ 分析 \_ 点控制代码


FSCTL \_ SET 重新 \_ 分析 \_ 点控制代码设置文件或目录的重新分析点。

若要执行此操作，请调用具有以下参数的 [**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85)) 。

Minifilters 应使用 [**FltTagFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-flttagfile) 而不是 FSCTL 集的重新 \_ \_ 分析 \_ 点来设置重新分析点。

有关重新分析点和 FSCTL \_ 设置重新 \_ 分析点控制代码的详细信息 \_ ，请参阅 Microsoft Windows SDK 文档。

**Parameters**

<a href="" id="filehandle"></a>*FileHandle*  
要设置重新分析点的文件或目录的文件句柄。 此参数是必需的，不能为 **NULL**。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作的控制代码。 使用 FSCTL \_ 设置 \_ \_ 此操作的重新分析点。

<a href="" id="inputbuffer"></a>*InputBuffer*  
一个指针，指向分配给调用方的重新分析 [**\_ GUID \_ 数据 \_ 缓冲区**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_reparse_guid_data_buffer) 或重新 [**分析 \_ 数据 \_ 缓冲区**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_reparse_data_buffer) 结构，其中包含重新分析点数据。 如果正在修改现有的重新分析点，则此结构的 **ReparseTag** 成员中指定的标记必须与要修改的重新分析点的标记相匹配。 此外，如果重新分析点为第三方 (非 Microsoft) 重新分析点，则结构的 **ReparseGuid** 成员中指定的 guid 是重新分析 \_ GUID \_ 数据 \_ 缓冲区结构，必须与要修改的重新分析点的 guid 匹配。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
*InputBuffer* 参数指向的缓冲区的大小（以字节为单位）。 对于重新分析 \_ guid \_ 数据 \_ 缓冲区结构，此值必须至少为重新分析 \_ guid \_ 数据 \_ 缓冲区 \_ 标头 \_ 大小，加上用户定义数据的大小，并且必须小于或等于最大重新 \_ 分析 \_ 数据 \_ 缓冲区 \_ 大小。 对于重新分析 \_ 数据 \_ 缓冲区结构，此值必须至少为重新分析 \_ 数据 \_ 缓冲区 \_ 标头 \_ 大小，加上用户定义数据的大小，并且必须小于或等于最大重新 \_ 分析 \_ 数据 \_ 缓冲区 \_ 大小。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
不与此操作一起使用;设置为 **NULL**。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
不与此操作一起使用;设置为零。

<a name="status-block"></a>状态块
------------

[**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85)) 返回状态 \_ "成功" 或相应的 NTSTATUS 值，如下所示：

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

 

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Ntifs (包含 Ntifs 或 Fltkernel) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**\_IRP \_ MJ \_ 文件 \_ 系统 \_ 控件的 FLT 参数**](flt-parameters-for-irp-mj-file-system-control.md)

[**FltTagFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-flttagfile)

[**FltUntagFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltuntagfile)

[**FSCTL \_ 删除重新 \_ 分析 \_ 点**](fsctl-delete-reparse-point.md)

[**FSCTL \_ 获取重新 \_ 分析 \_ 点**](fsctl-get-reparse-point.md)

[**IRP \_ MJ \_ 文件 \_ 系统 \_ 控制**](irp-mj-file-system-control.md)

[**IsReparseTagMicrosoft**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-isreparsetagmicrosoft)

[**IsReparseTagNameSurrogate**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-isreparsetagnamesurrogate)

[**重新分析 \_ 数据 \_ 缓冲区**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_reparse_data_buffer)

[**重新分析 \_ GUID \_ 数据 \_ 缓冲区**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_reparse_guid_data_buffer)

[**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85))

 

