---
title: FSCTL_SET_REPARSE_POINT 控制代码
description: FSCTL\_设置\_重新分析\_点控制代码设置重分析点上的文件或目录。
ms.assetid: db38cc62-845e-4690-a430-a9c834382b56
keywords:
- FSCTL_SET_REPARSE_POINT 控制代码可安装文件系统驱动程序
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
ms.openlocfilehash: de4d978a6c2cc57370599c020430371cf7dfd98c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366238"
---
# <a name="fsctlsetreparsepoint-control-code"></a>FSCTL\_设置\_重新分析\_点控制代码


FSCTL\_设置\_重新分析\_点控制代码设置重分析点上的文件或目录。

若要执行此操作，调用[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)使用以下参数。

微筛选器应使用[ **FltTagFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-flttagfile)而不是 FSCTL\_设置\_重新分析\_点若要设置重分析点。

有关重新分析点和 FSCTL\_设置\_重新分析\_点控制代码，请参阅 Microsoft Windows SDK 文档。

**Parameters**

<a href="" id="filehandle"></a>*FileHandle*  
文件或目录在其上设置重分析点的文件句柄。 此参数是必需的不能**NULL**。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作的控制代码。 使用 FSCTL\_设置\_重新分析\_点对于此操作。

<a href="" id="inputbuffer"></a>*InputBuffer*  
指向调用方分配[**重新分析\_GUID\_数据\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_reparse_guid_data_buffer)或[**重新分析\_数据\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_reparse_data_buffer)结构，其中包含重新分析点数据。 如果正在修改现有的重分析点，该标记中指定**ReparseTag**此结构的成员必须与要修改的重新分析点标记匹配。 此外，如果重新分析点是第三方 (非 Microsoft) 重新分析点，GUID 中指定**ReparseGuid**结构中的成员是重新分析\_GUID\_数据\_缓冲区结构必须匹配要修改的重新分析点的 GUID。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
大小 （字节），指向的缓冲区*InputBuffer*参数。 进行重新分析\_GUID\_数据\_缓冲区结构，此值必须至少重新分析\_GUID\_数据\_缓冲区\_标头\_大小，加上其大小用户定义的数据，并且它必须是小于或等于最大\_重新分析\_数据\_缓冲区\_大小。 进行重新分析\_数据\_缓冲区结构，此值必须至少重新分析\_数据\_缓冲区\_标头\_plus 的用户定义的数据大小的大小，并且它必须是小于或等于最大值\_重新分析\_数据\_缓冲区\_大小。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
不用于此操作;设置为**NULL**。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
不用于此操作;设置为零。

<a name="status-block"></a>状态块
------------

[**ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)将返回状态\_成功或适当的 NTSTATUS 值如以下之一：

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

 

<a name="requirements"></a>要求
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


[**FLT\_IRP 的参数\_MJ\_文件\_系统\_控件**](flt-parameters-for-irp-mj-file-system-control.md)

[**FltTagFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-flttagfile)

[**FltUntagFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltuntagfile)

[**FSCTL\_DELETE\_REPARSE\_POINT**](fsctl-delete-reparse-point.md)

[**FSCTL\_GET\_REPARSE\_POINT**](fsctl-get-reparse-point.md)

[**IRP\_MJ\_文件\_系统\_控件**](irp-mj-file-system-control.md)

[**IsReparseTagMicrosoft**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-isreparsetagmicrosoft)

[**IsReparseTagNameSurrogate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-isreparsetagnamesurrogate)

[**重新分析\_数据\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_reparse_data_buffer)

[**REPARSE\_GUID\_DATA\_BUFFER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_reparse_guid_data_buffer)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

 

 






