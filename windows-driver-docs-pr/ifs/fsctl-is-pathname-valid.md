---
title: FSCTL_IS_PATHNAME_VALID 控制代码
description: FSCTL\_是\_路径名\_有效控制代码对提供的路径名执行静态分析，并返回状态值，指示路径名的格式是否正确（例如，没有非法字符、可接受的路径长度和以此类推）。
ms.assetid: 3f95ae2c-a376-4c68-9e84-dde22aa7e315
keywords:
- FSCTL_IS_PATHNAME_VALID 控制代码可安装的文件系统驱动程序
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
ms.openlocfilehash: 77f44b6cc8c90b69bcd1b2f3b2ff80b561bc1a77
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841297"
---
# <a name="fsctl_is_pathname_valid-control-code"></a>FSCTL\_\_PATHNAME\_有效控制代码


**FSCTL\_是\_路径名\_有效**控制代码对提供的路径名执行静态分析，并返回状态值，指示路径名的格式是否正确（例如，没有非法字符、可接受的路径）长度，等等）。 由于此分析不考虑卷的内容，因此有时会提供 "误报"。 换句话说，分析可能指示路径名的格式正确，即使它不是也是如此。 负的结果更可靠，但不保证是正确的。

Fast FAT 文件系统不支持此控制代码，它在 NTFS 或 UDF 中不是有意义的操作。 NTFS 和 UDF 支持多种不同的代码集，任何字符串都可能是有效的路径名。

若要执行此操作，请调用具有以下参数的[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)或[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462) 。

**Parameters**

<a href="" id="fileobject"></a>*FileObject*  
仅[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 。 不使用。

<a href="" id="filehandle"></a>*FileHandle*  
仅[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 。 不使用。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作的控制代码。 使用 FSCTL\_\_路径名\_对此操作有效。

<a href="" id="inputbuffer"></a>*InputBuffer*  
一个缓冲区，其中包含要检查的以 NULL 结尾的路径名字符串。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
路径名的长度（以字节为单位）。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
不使用。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
不使用。

<a name="status-block"></a>状态块
------------

如果路径名格式正确，则[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)或[**ZWFSCONTROLFILE**](https://msdn.microsoft.com/library/windows/hardware/ff566462)将返回状态\_SUCCESS。 否则，使用的例程将返回相应的 NTSTATUS 错误代码。

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

 

 





