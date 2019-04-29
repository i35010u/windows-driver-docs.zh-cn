---
title: FSCTL_IS_PATHNAME_VALID 控制代码
description: FSCTL\_IS\_PATHNAME\_有效控制代码执行静态分析提供的路径名，并返回状态值，该值指示是否路径名的格式是否正确 （例如，任何非法字符，可接受的路径长度和等等）。
ms.assetid: 3f95ae2c-a376-4c68-9e84-dde22aa7e315
keywords:
- FSCTL_IS_PATHNAME_VALID 控制代码可安装文件系统驱动程序
topic_type:
- apiref
api_name:
- FSCTL_IS_PATHNAME_VALID
api_location:
- Ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe0bd9f33aab2e45be2b17230cc9da9e03ebe1a4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324603"
---
# <a name="fsctlispathnamevalid-control-code"></a>FSCTL\_IS\_PATHNAME\_有效控制代码


**FSCTL\_IS\_路径名\_有效**控制代码执行静态分析提供的路径名，并返回状态值，该值指示是否路径名的格式正确 （例如，任何非法字符，可接受的路径长度等）。 此分析不会考虑将卷的内容，因为有时会"误报。" 换而言之，分析可能表明，路径名称的格式正确，即使它不是。 负数结果更可靠，但不是保证可正确。

快速 FAT 文件系统不支持此控制代码，它不在 NTFS 或 UDF 中有意义的操作。 NTFS 和 UDF 支持这种广泛的代码集的任何字符串可能是有效的路径名。

若要执行此操作，调用[ **FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)或[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)使用以下参数。

**Parameters**

<a href="" id="fileobject"></a>*FileObject*  
[**FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)仅。 不使用。

<a href="" id="filehandle"></a>*FileHandle*  
[**FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)仅。 不使用。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作的控制代码。 使用 FSCTL\_IS\_PATHNAME\_对此操作的有效。

<a href="" id="inputbuffer"></a>*InputBuffer*  
包含要检查的以 NULL 结尾的路径名字符串的缓冲区。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
路径名的长度，以字节为单位。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
不使用。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
不使用。

<a name="status-block"></a>状态块
------------

[**FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)或[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)将返回状态\_成功如果路径名称的格式是否正确。 否则，使用例程将返回相应的 NTSTATUS 错误代码。

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

 

 





