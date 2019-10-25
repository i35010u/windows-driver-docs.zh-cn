---
title: FSCTL_DELETE_REPARSE_POINT 控制代码
description: FSCTL\_DELETE\_重新分析\_点控制代码从指定的文件或目录删除重新分析点。 使用 FSCTL\_删除\_重新分析\_点不会删除文件或目录。
ms.assetid: c8a06477-457b-47e5-b5c5-48d798fe08b3
keywords:
- FSCTL_DELETE_REPARSE_POINT 控制代码可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- FSCTL_DELETE_REPARSE_POINT
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 303137d7fb5e9ad1f96aa365c0a8a79fe62c54c5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841323"
---
# <a name="fsctl_delete_reparse_point-control-code"></a>FSCTL\_删除\_重新分析\_点控制代码


FSCTL\_DELETE\_重新分析\_点控制代码从指定的文件或目录删除重新分析点。 使用 FSCTL\_删除\_重新分析\_点不会删除文件或目录。

若要执行此操作，请调用具有以下参数的[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462) 。

Minifilters 应使用[**FltUntagFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltuntagfile)而不是 FSCTL\_delete\_重新分析\_点以删除重新分析点。

有关重新分析点和 FSCTL\_删除\_重新分析\_点控制代码的详细信息，请参阅 Microsoft Windows SDK 文档。

**Parameters**

<a href="" id="filehandle"></a>*FileHandle*  
要从中删除重新分析点的文件或目录的文件句柄。 调用方必须对文件或目录具有写入访问权限。 此参数是必需的，不能为**NULL**。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作的控制代码。 使用 FSCTL\_删除此操作\_重新分析\_点。

<a href="" id="inputbuffer"></a>*InputBuffer*  
指向重新[**分析\_GUID\_数据\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_reparse_guid_data_buffer)或重新[**分析\_数据\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_reparse_data_buffer)结构的指针。 此结构的**ReparseTag**成员中指定的标记必须匹配要删除的重新分析点的标记，并且**ReparseDataLength**成员必须为零。 此外，如果重新分析点为第三方（非 Microsoft）重新分析点，则在重新分析\_GUID\_数据\_缓冲区结构的**ReparseGuid**成员中指定的 guid 必须与要删除的重新分析点的 guid 匹配。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
**InputBuffer**参数指向的缓冲区的大小（以字节为单位）。 要使重分析\_GUID\_数据\_缓冲结构，此值必须完全重新分析\_GUID\_数据\_缓冲区\_大小\_大小。 对于\_数据\_缓冲区结构的重新分析，此值必须完全重新分析\_数据\_缓冲区\_标头\_大小。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
不与此操作一起使用;设置为**NULL**。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
不与此操作一起使用;设置为零。

<a name="status-block"></a>状态块
------------

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)返回成功\_状态，或使用适当的 NTSTATUS 值（如下所示）：

<a href="" id="status-io-reparse-data-invalid"></a>状态\_IO\_重新分析\_数据\_无效  
指定的参数值之一无效。 这是一个错误代码。

<a href="" id="status-io-reparse-tag-invalid"></a>状态\_IO\_重新分析\_\_标记无效  
调用方指定的重新分析标记无效。 这是一个错误代码。

<a href="" id="status-io-reparse-tag-mismatch"></a>状态\_IO\_重新分析\_标记\_不匹配  
调用方指定的重新分析标记与要删除的重新分析点的标记不匹配。 这是一个错误代码。

<a href="" id="status-reparse-attribute-conflict"></a>状态\_重新分析\_属性\_冲突  
重新分析点是第三方重新分析点，并且调用方指定的重新分析 GUID 与要删除的重新分析点的 GUID 不匹配。 这是一个错误代码。

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

[**FSCTL\_获取\_重新分析\_点**](fsctl-get-reparse-point.md)

[**FSCTL\_设置\_重新分析\_点**](fsctl-set-reparse-point.md)

[**IRP\_MJ\_文件\_系统\_控件**](irp-mj-file-system-control.md)

[**IsReparseTagMicrosoft**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-isreparsetagmicrosoft)

[**IsReparseTagNameSurrogate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-isreparsetagnamesurrogate)

[ **\_缓冲区\_重新分析数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_reparse_data_buffer)

[ **\_数据\_缓冲区中的重新分析\_GUID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_reparse_guid_data_buffer)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

 

 






