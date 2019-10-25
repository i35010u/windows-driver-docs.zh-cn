---
title: FSCTL_QUERY_FILE_LAYOUT 控制代码
description: FSCTL\_QUERY\_文件\_布局控制代码检索文件系统卷的文件布局信息。
ms.assetid: C0094741-72C1-409C-89E6-BAD60A94EFD6
keywords:
- FSCTL_QUERY_FILE_LAYOUT 控制代码可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- FSCTL_QUERY_FILE_LAYOUT
api_location:
- Ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f508626bfb7ca07c5ca5545a7329dee5af89ce5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841291"
---
# <a name="fsctl_query_file_layout-control-code"></a>FSCTL\_查询\_文件\_布局控制代码


FSCTL\_QUERY\_文件\_布局控制代码检索文件系统卷的文件布局信息。 此请求的结果是文件布局信息项的集合。 返回的项的类型通过在查询中设置包含标志[ **\_文件\_布局\_输入**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_query_file_layout_input)结构进行控制。 您可以根据需要通过提供一组文件范围来限制布局信息的选择，来筛选结果。

若要执行此操作，请调用具有以下参数的[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)或[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462) 。

**Parameters**

<a href="" id="fileobject"></a>*FileObject*  
仅[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 。 文件系统卷的文件对象指针。 此参数是必需的，不能为**NULL**。

<a href="" id="filehandle"></a>*FileHandle*  
仅[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462) 。 文件系统卷的文件句柄。 此参数是必需的，不能为**NULL**。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作的控制代码。 对于此操作，请使用 FSCTL\_查询\_文件\_布局控制代码。

<a href="" id="inputbuffer"></a>*InputBuffer*  
指向[ **\_文件\_布局\_输入**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_query_file_layout_input)结构的调用方分配的查询的指针。 此结构包含选择选项。 **查询\_文件\_布局\_输入**后，将包括可选的文件范围。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
*InputBuffer*参数指向的缓冲区的大小（以字节为单位）。 *NumberOfPairs* &gt; 0 时， *InputBuffer*的大小必须至少为**sizeof**（查询\_文件\_LAYOUT\_INPUT） + （**sizeof**（*Filter*） \* （*NumberOfPairs* ））。 否则，将*InputBufferLength* = **sizeof**（查询\_文件\_布局\_输入）。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
指向[ **\_文件\_布局\_输出**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_query_file_layout_output)结构的调用方分配查询的指针。 这是此缓冲区中后面的文件布局条目的标头。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
*OutputBuffer*参数指向的缓冲区的大小（以字节为单位）。 *OutputBuffer*的大小必须足够大，以包含[**查询\_文件\_布局\_输出**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_query_file_layout_output)以及返回的文件布局和流布局结构。

<a name="status-block"></a>状态块
------------

[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)或[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)返回状态\_SUCCESS 或适当的 NTSTATUS 值，如以下值之一：

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
<td align="left"><p><strong>STATUS_INVALID_PARAMETER</strong></p></td>
<td align="left"><p>文件系统卷不是打开的用户卷，或者缓冲区长度值不正确，或设置了无效的查询选项。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_ACCESS_DENIED</strong></p></td>
<td align="left"><p>调用方无法访问文件系统卷。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_INVALID_USER_BUFFER</strong></p></td>
<td align="left"><p><em>InputBuffer</em>或<em>OutputBuffer</em>的指针没有正确对齐。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_BUFFER_TOO_SMALL</strong></p></td>
<td align="left"><p><em>OutputBufferLength</em>中的值指示<em>OutputBuffer</em>太小，无法包含至少一个布局条目。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_END_OF_FILE</strong></p></td>
<td align="left"><p><em>InputBuffer</em>或<em>OutputBuffer</em>的指针没有正确对齐。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

若要检索卷的所有布局条目，会多次发出 FSCTL\_QUERY\_FILE\_LAYOUT 请求，直到返回 **\_文件\_结束\_的状态**。 返回**状态\_"成功**" 时，调用方可以继续发送 FSCTL\_查询\_文件\_布局请求，以获取剩余的布局条目。

可以通过在查询的**Flags**成员[ **\_文件\_布局\_输入**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_query_file_layout_input)中包含**查询\_文件\_\_布局**，随时重新启动布局项的枚举。 此外，在 FSCTL\_查询\_文件\_布局返回 **\_文件\_结束\_的状态**之后，必须在下一个 FSCTL 中包含**查询\_** \_\___t_11_ 查询\_文件\_LAYOUT 请求以开始另一个布局条目枚举。

**ReFS：  **此代码不受支持。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>版本</p></td>
<td align="left"><p>从 Windows 8 开始可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ntifs （包括 Ntifs）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**查询\_文件\_布局\_输入**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_query_file_layout_input)

[**查询\_文件\_布局\_输出**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_query_file_layout_output)

[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

 

 






