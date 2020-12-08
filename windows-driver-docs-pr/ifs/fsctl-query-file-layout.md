---
title: FSCTL_QUERY_FILE_LAYOUT 控制代码
description: FSCTL \_ 查询 \_ 文件 \_ 布局控制代码检索文件系统卷的文件布局信息。
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
ms.openlocfilehash: 5d310ee9268329d2ba9a1b11193a30a09bfe6022
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816787"
---
# <a name="fsctl_query_file_layout-control-code"></a>FSCTL \_ 查询 \_ 文件 \_ 布局控制代码


FSCTL \_ 查询 \_ 文件 \_ 布局控制代码检索文件系统卷的文件布局信息。 此请求的结果是文件布局信息项的集合。 返回的项的类型是通过在 [**查询 \_ 文件 \_ 布局 \_ 输入**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_query_file_layout_input) 结构中设置包含标志来控制的。 您可以根据需要通过提供一组文件范围来限制布局信息的选择，来筛选结果。

若要执行此操作，请调用具有以下参数的 [**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 或 [**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85)) 。

**Parameters**

<a href="" id="fileobject"></a>*FileObject*  
仅 [**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 。 文件系统卷的文件对象指针。 此参数是必需的，不能为 **NULL**。

<a href="" id="filehandle"></a>*FileHandle*  
仅 [**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85)) 。 文件系统卷的文件句柄。 此参数是必需的，不能为 **NULL**。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作的控制代码。 对于此操作，请使用 FSCTL \_ 查询 \_ 文件 \_ 布局控制代码。

<a href="" id="inputbuffer"></a>*InputBuffer*  
一个指针，指向分配给调用方的 [**查询 \_ 文件 \_ 布局 \_ 输入**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_query_file_layout_input) 结构。 此结构包含选择选项。 可选文件的范围包括在 **查询 \_ 文件 \_ 布局 \_ 输入** 之后。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
*InputBuffer* 参数指向的缓冲区的大小（以字节为单位）。 在 NumberOfPairs 0 时， *InputBuffer* 的大小必须至少为 **sizeof** (查询 \_ 文件 \_ 布局 \_ 输入) + (**Sizeof** (*Filter*)  () \* # A7 *NumberOfPairs* *NumberOfPairs* &gt; 。 否则，请将 *InputBufferLength*  =  **sizeof** (QUERY \_ FILE \_ LAYOUT \_ INPUT) 。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
指向分配给调用方的 [**查询 \_ 文件 \_ 布局 \_ 输出**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_query_file_layout_output) 结构的指针。 这是此缓冲区中后面的文件布局条目的标头。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
*OutputBuffer* 参数指向的缓冲区的大小（以字节为单位）。 *OutputBuffer* 的大小必须足够大，以包含 [**查询 \_ 文件 \_ 布局 \_ 输出**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_query_file_layout_output)以及返回的文件布局和流布局结构。

<a name="status-block"></a>状态块
------------

[**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 或 [**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85)) 返回状态 \_ 成功或适当的 NTSTATUS 值，如以下值之一：

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

若要检索卷的所有布局条目，请在 \_ \_ \_ 返回 **\_ \_ \_ 文件的状态结尾** 之前多次发出 FSCTL 查询文件布局请求。 返回 **状态 \_ 成功** 后，调用方可以继续为 \_ \_ 其余布局条目发送 FSCTL 查询文件 \_ 布局请求。

可以通过在 [**查询 \_ 文件 \_ 布局 \_ 输入**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_query_file_layout_input)的 **Flags** 成员中包含 **查询 \_ 文件 \_ 布局 \_ 重新启动** 标志，随时重新启动布局项的枚举。 此外，在 FSCTL \_ 查询 \_ 文件 \_ 布局返回了 **\_ \_ \_ 文件的状态结尾** 之后，必须在下一个 FSCTL 查询文件布局请求中包含 **查询 \_ 文件 \_ 布局 \_ 重新启动** 标志， \_ \_ \_ 才能开始另一个布局输入枚举。

* * ReFS： * * 此代码不受支持。

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
<td align="left">Ntifs (包含 Ntifs) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**查询 \_ 文件 \_ 布局 \_ 输入**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_query_file_layout_input)

[**查询 \_ 文件 \_ 布局 \_ 输出**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_query_file_layout_output)

[**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)

[**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85))

 

