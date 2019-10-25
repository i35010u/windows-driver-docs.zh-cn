---
title: FSCTL_SET_REPARSE_POINT 控制代码
description: FSCTL\_将\_重新分析\_点控制代码设置文件或目录的重新分析点。
ms.assetid: db38cc62-845e-4690-a430-a9c834382b56
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
ms.openlocfilehash: f8f775fab2d807a393dfcd0d8663b124eec45c45
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841245"
---
# <a name="fsctl_set_reparse_point-control-code"></a>FSCTL\_设置\_重新分析\_点控制代码


FSCTL\_将\_重新分析\_点控制代码设置文件或目录的重新分析点。

若要执行此操作，请调用具有以下参数的[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462) 。

Minifilters 应使用[**FltTagFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-flttagfile)而不是 FSCTL\_设置\_重新分析\_点来设置重新分析点。

有关重新分析点和 FSCTL\_设置\_重新分析\_点控制代码的详细信息，请参阅 Microsoft Windows SDK 文档。

**Parameters**

<a href="" id="filehandle"></a>*FileHandle*  
要设置重新分析点的文件或目录的文件句柄。 此参数是必需的，不能为**NULL**。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作的控制代码。 使用 FSCTL\_设置此操作\_重新分析\_点。

<a href="" id="inputbuffer"></a>*InputBuffer*  
一个指针，指向分配给调用方的重新[**分析\_GUID\_数据\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_reparse_guid_data_buffer)或重新[**分析\_数据\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_reparse_data_buffer)包含重新分析点数据的缓冲区结构。 如果正在修改现有的重新分析点，则此结构的**ReparseTag**成员中指定的标记必须与要修改的重新分析点的标记相匹配。 此外，如果重新分析点为第三方（非 Microsoft）重新分析点，则结构的**ReparseGuid**成员中指定的 guid 是\_GUID\_数据的重新分析，\_缓冲区结构必须与重新分析点的 guid 匹配。要修改的。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
*InputBuffer*参数指向的缓冲区的大小（以字节为单位）。 对于重新分析\_GUID\_数据\_缓冲结构，此值必须至少是\_GUID\_数据\_缓存\_数据\_缓冲区大小，加上用户定义数据的大小，它必须小于或等于最大\_重新分析\_数据\_缓冲区\_大小。 若要重新分析\_数据\_缓冲区结构，此值必须至少是\_数据的重新分析数据\_缓冲区\_大小，加上用户定义数据的大小，并且必须小于或等于最大值\_\_缓冲区\_大小的重新分析\_数据。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
不与此操作一起使用;设置为**NULL**。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
不与此操作一起使用;设置为零。

<a name="status-block"></a>状态块
------------

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)返回成功\_状态，或使用适当的 NTSTATUS 值（如下所示）：

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
<td align="left">Ntifs （包括 Ntifs 或 Fltkernel）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**用于 IRP\_MJ\_文件\_系统\_控制的 FLT\_参数**](flt-parameters-for-irp-mj-file-system-control.md)

[**FltTagFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-flttagfile)

[**FltUntagFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltuntagfile)

[**FSCTL\_删除\_重新分析\_点**](fsctl-delete-reparse-point.md)

[**FSCTL\_获取\_重新分析\_点**](fsctl-get-reparse-point.md)

[**IRP\_MJ\_文件\_系统\_控件**](irp-mj-file-system-control.md)

[**IsReparseTagMicrosoft**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-isreparsetagmicrosoft)

[**IsReparseTagNameSurrogate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-isreparsetagnamesurrogate)

[ **\_缓冲区\_重新分析数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_reparse_data_buffer)

[ **\_数据\_缓冲区中的重新分析\_GUID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_reparse_guid_data_buffer)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

 

 






