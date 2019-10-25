---
title: FSCTL_GET_REPARSE_POINT 控制代码
description: FSCTL\_获取\_重新分析\_点控制代码检索与指定的文件或目录关联的重新分析点数据。
ms.assetid: 8d56a4c5-46c3-42b7-a532-eaf0d792b519
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
ms.openlocfilehash: e53ba6d929805baa9d704f532fd0d12870814851
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841307"
---
# <a name="fsctl_get_reparse_point-control-code"></a>FSCTL\_获取\_重新分析\_点控制代码


FSCTL\_获取\_重新分析\_点控制代码检索与指定的文件或目录关联的重新分析点数据。

若要执行此操作，请调用具有以下参数的[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)或[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462) 。

有关重新分析点和 FSCTL\_获取\_重新分析\_点控制代码的详细信息，请参阅 Microsoft Windows SDK 文档。

**Parameters**

<a href="" id="fileobject"></a>*FileObject*  
仅[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 。 要从中检索重新分析点数据的文件或目录的文件对象指针。 此参数是必需的，不能为**NULL**。

<a href="" id="filehandle"></a>*FileHandle*  
仅[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462) 。 从中检索重新分析点数据的文件或目录的文件句柄。 此参数是必需的，不能为**NULL**。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作的控制代码。 使用**FSCTL\_获取此操作\_重新分析\_点**。

<a href="" id="inputbuffer"></a>*InputBuffer*  
不与此操作一起使用;设置为**NULL**。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
不与此操作一起使用;设置为零。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
一个指针，指向分配给调用方的重新[**分析\_GUID\_数据\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_reparse_guid_data_buffer)或[**重分析\_数据\_缓存**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_reparse_data_buffer)接收重新分析点数据。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
*OutputBuffer*参数指向的缓冲区的大小（以字节为单位）。 对于重新分析\_GUID\_数据\_缓冲结构，此值必须至少是\_GUID\_数据\_缓存\_数据\_缓冲区大小，以及所需的用户定义数据的大小，它必须小于或等于最大\_重新分析\_数据\_缓冲区\_大小。 对于\_数据\_缓冲区结构的重新分析，此值必须至少是\_数据的重新分析数据\_缓冲区\_大小，加上所需的用户定义数据的大小，并且必须小于或等于最大值\_6_ 重新分析\_数据\_缓冲区\_大小。

<a name="status-block"></a>状态块
------------

[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)或[**ZWFSCONTROLFILE**](https://msdn.microsoft.com/library/windows/hardware/ff566462)将返回状态\_SUCCESS 或适当的 NTSTATUS 值，如以下之一：

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
<td align="left"><p><em>OutputBuffer</em>参数指向的缓冲区足以容纳 REPARSE_GUID_DATA_BUFFER 或 REPARSE_DATA_BUFFER 结构的固定部分，而不是用户定义数据。 在这种情况下，仅在<em>OutputBuffer</em>缓冲区中返回重新分析点数据的固定部分。 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile" data-raw-source="[&lt;strong&gt;FltFsControlFile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)"><strong>FltFsControlFile</strong></a>的<em>LengthReturned</em>参数接收返回的数据的实际长度（以字节为单位）。 这是警告代码。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_BUFFER_TOO_SMALL</strong></p></td>
<td align="left"><p><em>OutputBuffer</em>参数指向的缓冲区不够大，无法容纳重新分析点数据。 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile" data-raw-source="[&lt;strong&gt;FltFsControlFile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)"><strong>FltFsControlFile</strong></a>的<em>LengthReturned</em>参数（或<a href="https://msdn.microsoft.com/library/windows/hardware/ff566462" data-raw-source="[&lt;strong&gt;ZwFsControlFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566462)"><strong>ZwFsControlFile</strong></a>的<em>IoStatus</em>参数的<strong>信息</strong>成员）接收所需的缓冲区大小。 在这种情况下，不会返回重新分析点数据。 这是一个错误代码。</p></td>
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
<td align="left">Ntifs （包括 Ntifs 或 Fltkernel）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**FLT\_回调\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[**用于 IRP\_MJ\_文件\_系统\_控制的 FLT\_参数**](flt-parameters-for-irp-mj-file-system-control.md)

[**FLT\_标记\_数据\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_tag_data_buffer)

[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)

[**FltTagFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-flttagfile)

[**FltUntagFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltuntagfile)

[**FSCTL\_删除\_重新分析\_点**](fsctl-delete-reparse-point.md)

[**FSCTL\_设置\_重新分析\_点**](fsctl-set-reparse-point.md)

[**IRP\_MJ\_文件\_系统\_控件**](irp-mj-file-system-control.md)

[**IsReparseTagMicrosoft**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-isreparsetagmicrosoft)

[**IsReparseTagNameSurrogate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-isreparsetagnamesurrogate)

[ **\_缓冲区\_重新分析数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_reparse_data_buffer)

[ **\_数据\_缓冲区中的重新分析\_GUID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_reparse_guid_data_buffer)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

 

 






