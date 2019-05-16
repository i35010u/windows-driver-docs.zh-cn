---
title: FSCTL_DELETE_REPARSE_POINT 控制代码
description: FSCTL\_删除\_重新分析\_点控制代码从指定的文件或目录中删除重分析点。 使用 FSCTL\_删除\_重新分析\_点不会删除文件或目录。
ms.assetid: c8a06477-457b-47e5-b5c5-48d798fe08b3
keywords:
- FSCTL_DELETE_REPARSE_POINT 控制代码可安装文件系统驱动程序
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
ms.openlocfilehash: 8cd7ecd75473633dbfd13fbae040fcd76e4c8288
ms.sourcegitcommit: 0c364a5c4947fcfe815de5fb57237c3e36b3ae20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65701995"
---
# <a name="fsctldeletereparsepoint-control-code"></a>FSCTL\_删除\_重新分析\_点控制代码


FSCTL\_删除\_重新分析\_点控制代码从指定的文件或目录中删除重分析点。 使用 FSCTL\_删除\_重新分析\_点不会删除文件或目录。

若要执行此操作，调用[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)使用以下参数。

微筛选器应使用[ **FltUntagFile** ](https://msdn.microsoft.com/library/windows/hardware/ff544608)而不是 FSCTL\_删除\_重新分析\_点删除重新分析点。

有关重新分析点和 FSCTL\_删除\_重新分析\_点控制代码，请参阅 Microsoft Windows SDK 文档。

**Parameters**

<a href="" id="filehandle"></a>*FileHandle*  
文件或目录是要删除重新分析点的文件句柄。 调用方必须具有对文件或目录的写访问权限。 此参数是必需的不能**NULL**。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作的控制代码。 使用 FSCTL\_删除\_重新分析\_点对于此操作。

<a href="" id="inputbuffer"></a>*InputBuffer*  
指向[**重新分析\_GUID\_数据\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff552014)或[**重新分析\_数据\_缓冲区** ](https://msdn.microsoft.com/library/windows/hardware/ff552012)结构。 中指定的标签**ReparseTag**此结构的成员必须与要删除的重新分析点的标记匹配并**ReparseDataLength**成员必须为零。 此外，如果重新分析点是第三方 (非 Microsoft) 重新分析点，GUID 中指定**ReparseGuid**成员的重分析\_GUID\_数据\_缓冲区结构必须匹配GUID 的重新分析点删除。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
大小 （字节），指向的缓冲区**InputBuffer**参数。 进行重新分析\_GUID\_数据\_缓冲区结构，此值必须是完全重新分析\_GUID\_数据\_缓冲区\_标头\_大小。 进行重新分析\_数据\_缓冲区结构，此值必须是完全重新分析\_数据\_缓冲区\_标头\_大小。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
不用于此操作;设置为**NULL**。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
不用于此操作;设置为零。

<a name="status-block"></a>状态块
------------

[**ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)将返回状态\_成功或适当的 NTSTATUS 值如以下之一：

<a href="" id="status-io-reparse-data-invalid"></a>状态\_IO\_重新分析\_数据\_无效  
其中一个指定的参数值无效。 这是一个错误代码。

<a href="" id="status-io-reparse-tag-invalid"></a>状态\_IO\_重新分析\_标记\_无效  
指定由调用方重分析标记无效。 这是一个错误代码。

<a href="" id="status-io-reparse-tag-mismatch"></a>状态\_IO\_重新分析\_标记\_不匹配  
指定由调用方重分析标记与要删除的重新分析点标记不匹配。 这是一个错误代码。

<a href="" id="status-reparse-attribute-conflict"></a>状态\_重新分析\_属性\_冲突  
重分析点是第三方重分析点，并重新分析由调用方指定的 GUID 与要删除的重分析点 GUID 不匹配。 这是一个错误代码。

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

[**FltTagFile**](https://msdn.microsoft.com/library/windows/hardware/ff544589)

[**FltUntagFile**](https://msdn.microsoft.com/library/windows/hardware/ff544608)

[**FSCTL\_GET\_REPARSE\_POINT**](fsctl-get-reparse-point.md)

[**FSCTL\_SET\_REPARSE\_POINT**](fsctl-set-reparse-point.md)

[**IRP\_MJ\_文件\_系统\_控件**](irp-mj-file-system-control.md)

[**IsReparseTagMicrosoft**](https://msdn.microsoft.com/library/windows/hardware/ff549452)

[**IsReparseTagNameSurrogate**](https://msdn.microsoft.com/library/windows/hardware/ff549462)

[**重新分析\_数据\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff552012)

[**REPARSE\_GUID\_DATA\_BUFFER**](https://msdn.microsoft.com/library/windows/hardware/ff552014)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

 

 






