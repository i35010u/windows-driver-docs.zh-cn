---
title: FSCTL_GET_REPARSE_POINT 控制代码
description: FSCTL \_ 获取重新 \_ 分析 \_ 点控制代码检索与指定的文件或目录关联的重新分析点数据。
keywords:
- FSCTL_GET_REPARSE_POINT 控制代码可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- FSCTL_GET_REPARSE_POINT
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f4c4dab80cbc79c1efec538a499ba4821272bc7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808379"
---
# <a name="fsctl_get_reparse_point-control-code"></a>FSCTL \_ 获取重新 \_ 分析 \_ 点控制代码


FSCTL \_ 获取重新 \_ 分析 \_ 点控制代码检索与指定的文件或目录关联的重新分析点数据。

若要执行此操作，请调用具有以下参数的 [**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 或 [**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85)) 。

有关重新分析点和 FSCTL \_ 获取重新 \_ 分析点控制代码的详细信息 \_ ，请参阅 Microsoft Windows SDK 文档。

**Parameters**

<a href="" id="fileobject"></a>*FileObject*  
仅 [**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 。 要从中检索重新分析点数据的文件或目录的文件对象指针。 此参数是必需的，不能为 **NULL**。

<a href="" id="filehandle"></a>*FileHandle*  
仅 [**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85)) 。 从中检索重新分析点数据的文件或目录的文件句柄。 此参数是必需的，不能为 **NULL**。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作的控制代码。 使用 FSCTL 获取此操作的重新 **\_ \_ 分析 \_ 点** 。

<a href="" id="inputbuffer"></a>*InputBuffer*  
不与此操作一起使用;设置为 **NULL**。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
不与此操作一起使用;设置为零。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
一个指针，它指向接收了重新分析点数据的调用方分配的重新 [**分析 \_ GUID \_ 数据 \_ 缓冲区**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_reparse_guid_data_buffer) 或重新 [**分析 \_ 数据 \_ 缓冲区**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_reparse_data_buffer) 结构。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
*OutputBuffer* 参数指向的缓冲区的大小（以字节为单位）。 对于重新分析 \_ guid \_ 数据 \_ 缓冲区结构，此值必须至少为重新分析 \_ guid \_ 数据 \_ 缓冲区 \_ 标头 \_ 大小，加上所需的用户定义数据的大小，并且必须小于或等于最大重新 \_ 分析 \_ 数据 \_ 缓冲区 \_ 大小。 对于重新分析 \_ 数据 \_ 缓冲区结构，此值必须至少是重新分析 \_ 数据 \_ 缓冲区 \_ 标头 \_ 大小，加上所需的用户定义数据的大小，并且必须小于或等于最大重新 \_ 分析 \_ 数据 \_ 缓冲区 \_ 大小。

<a name="status-block"></a>状态块
------------

[**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 或 [**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85)) 返回状态 \_ "成功" 或相应的 NTSTATUS 值，如下所示：

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
<td align="left"><p><strong>STATUS_BUFFER_OVERFLOW</strong></p></td>
<td align="left"><p><em>OutputBuffer</em>参数指向的缓冲区足以容纳 REPARSE_GUID_DATA_BUFFER 或 REPARSE_DATA_BUFFER 结构的固定部分，而不是用户定义数据。 在这种情况下，仅在 <em>OutputBuffer</em> 缓冲区中返回重新分析点数据的固定部分。 <a href="/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile" data-raw-source="[&lt;strong&gt;FltFsControlFile&lt;/strong&gt;](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)"><strong>FltFsControlFile</strong></a>的<em>LengthReturned</em>参数接收返回的数据的实际长度（以字节为单位）。 这是警告代码。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_BUFFER_TOO_SMALL</strong></p></td>
<td align="left"><p><em>OutputBuffer</em>参数指向的缓冲区不够大，无法容纳重新分析点数据。 <a href="/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile" data-raw-source="[&lt;strong&gt;FltFsControlFile&lt;/strong&gt;](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)"><strong>FltFsControlFile</strong></a> (的<em>LengthReturned</em>参数，或<a href="/previous-versions/ff566462(v=vs.85)" data-raw-source="[&lt;strong&gt;ZwFsControlFile&lt;/strong&gt;](/previous-versions/ff566462(v=vs.85))"><strong>ZwFsControlFile</strong></a>) 的<em>IoStatus</em>参数的<strong>信息</strong>成员接收所需的缓冲区大小。 在这种情况下，不会返回重新分析点数据。 这是一个错误代码。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_IO_REPARSE_DATA_INVALID</strong></p></td>
<td align="left"><p>指定的参数值之一无效。 这是一个错误代码。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_NOT_A_REPARSE_POINT</strong></p></td>
<td align="left"><p>文件或目录不是重新分析点。 这是一个错误代码。</p></td>
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


[**FLT \_ 回调 \_ 数据**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[**\_IRP \_ MJ \_ 文件 \_ 系统 \_ 控件的 FLT 参数**](flt-parameters-for-irp-mj-file-system-control.md)

[**FLT \_ 标记 \_ 数据 \_ 缓冲区**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_tag_data_buffer)

[**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)

[**FltTagFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-flttagfile)

[**FltUntagFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltuntagfile)

[**FSCTL \_ 删除重新 \_ 分析 \_ 点**](fsctl-delete-reparse-point.md)

[**FSCTL \_ 设置 \_ 重分析 \_ 点**](fsctl-set-reparse-point.md)

[**IRP \_ MJ \_ 文件 \_ 系统 \_ 控制**](irp-mj-file-system-control.md)

[**IsReparseTagMicrosoft**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-isreparsetagmicrosoft)

[**IsReparseTagNameSurrogate**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-isreparsetagnamesurrogate)

[**重新分析 \_ 数据 \_ 缓冲区**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_reparse_data_buffer)

[**重新分析 \_ GUID \_ 数据 \_ 缓冲区**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_reparse_guid_data_buffer)

[**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85))

