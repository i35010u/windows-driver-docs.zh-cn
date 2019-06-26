---
title: FSCTL_QUERY_FILE_LAYOUT 控制代码
description: FSCTL\_查询\_文件\_布局控件代码检索文件系统卷的文件布局信息。
ms.assetid: C0094741-72C1-409C-89E6-BAD60A94EFD6
keywords:
- FSCTL_QUERY_FILE_LAYOUT 控制代码可安装文件系统驱动程序
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
ms.openlocfilehash: d3d2619b3e5af645379446a59d76fa86df6aa545
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380090"
---
# <a name="fsctlqueryfilelayout-control-code"></a>FSCTL\_查询\_文件\_布局控件代码


FSCTL\_查询\_文件\_布局控件代码检索文件系统卷的文件布局信息。 此请求的结果是文件布局的信息项的集合。 返回的项的类型由设置包含标志控制[**查询\_文件\_布局\_输入**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_query_file_layout_input)结构。 （可选） 可以通过提供一组文件范围限制在选项中的布局信息来筛选结果。

若要执行此操作，调用[ **FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)或[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)使用以下参数。

**Parameters**

<a href="" id="fileobject"></a>*FileObject*  
[**FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)仅。 文件系统卷文件对象指针。 此参数是必需的不能**NULL**。

<a href="" id="filehandle"></a>*FileHandle*  
[**ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)仅。 文件系统卷的文件句柄。 此参数是必需的不能**NULL**。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作的控制代码。 使用 FSCTL\_查询\_文件\_布局控件代码对于此操作。

<a href="" id="inputbuffer"></a>*InputBuffer*  
指向调用方分配的指针[**查询\_文件\_布局\_输入**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_query_file_layout_input)结构。 此结构包含选择选项。 可选文件范围将包括后**查询\_文件\_布局\_输入**。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
大小 （字节） 通过指向的缓冲区*InputBuffer*参数。 大小*InputBuffer*必须至少**sizeof**(查询\_文件\_布局\_输入) + (**sizeof**(*筛选*) \* (*NumberOfPairs* -1))，当*NumberOfPairs* &gt; 0。 否则，设置*InputBufferLength* = **sizeof**(查询\_文件\_布局\_输入)。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
指向调用方分配的指针[**查询\_文件\_布局\_输出**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_query_file_layout_output)结构。 这是按照此缓冲区中的文件布局项的标头。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
大小 （字节） 通过指向的缓冲区*OutputBuffer*参数。 大小*OutputBuffer*必须足够大，以包含[**查询\_文件\_布局\_输出**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_query_file_layout_output)以及文件返回的布局和流布局结构。

<a name="status-block"></a>状态块
------------

[**FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)或[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)将返回状态\_成功或相应 NTSTATUS 值，如下列值之一：

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
<td align="left"><p>文件系统卷不是一个打开的用户卷，或缓冲区长度值不正确，或者设置了一个无效的查询选项。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_ACCESS_DENIED</strong></p></td>
<td align="left"><p>调用方无法访问文件系统卷。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_INVALID_USER_BUFFER</strong></p></td>
<td align="left"><p>为指针<em>InputBuffer</em>或<em>OutputBuffer</em>没有正确对齐。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_BUFFER_TOO_SMALL</strong></p></td>
<td align="left"><p>中的值<em>OutputBufferLength</em>指示<em>OutputBuffer</em>太小，无法包含至少一个布局条目。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_END_OF_FILE</strong></p></td>
<td align="left"><p>为指针<em>InputBuffer</em>或<em>OutputBuffer</em>没有正确对齐。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

若要检索的卷，FSCTL 的所有布局条目\_查询\_文件\_布局请求发出多个次，直到**状态\_最终\_OF\_文件**返回。 虽然**状态\_成功**会返回，调用方可以继续发送 FSCTL\_查询\_文件\_剩余布局项的布局请求。

布局项的枚举可能会重启在任何时候通过包括**查询\_文件\_布局\_重新启动**标志中**标志**成员[**查询\_文件\_布局\_输入**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_query_file_layout_input)。 此外之后 FSCTL,\_查询\_文件\_布局已返回**状态\_最终\_OF\_文件**，需要包括**查询\_文件\_布局\_重新启动**中下一步 FSCTL 标志\_查询\_文件\_布局请求，若要开始另一个布局条目枚举。

**ReFS:  **不支持此代码。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Version</p></td>
<td align="left"><p>从开始，提供 Windows 8。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ntifs.h （包括 Ntifs.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**查询\_文件\_布局\_输入**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_query_file_layout_input)

[**查询\_文件\_布局\_输出**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_query_file_layout_output)

[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

 

 






