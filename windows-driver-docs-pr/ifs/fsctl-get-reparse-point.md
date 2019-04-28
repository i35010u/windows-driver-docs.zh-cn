---
title: FSCTL_GET_REPARSE_POINT 控制代码
description: FSCTL\_获取\_重新分析\_点控制代码会检索与指定的文件或目录关联的重新分析点数据。
ms.assetid: 8d56a4c5-46c3-42b7-a532-eaf0d792b519
keywords:
- FSCTL_GET_REPARSE_POINT 控制代码可安装文件系统驱动程序
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
ms.openlocfilehash: 0c935357f6ce270037409c71e57e3324945098f8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327893"
---
# <a name="fsctlgetreparsepoint-control-code"></a>FSCTL\_获取\_重新分析\_点控制代码


FSCTL\_获取\_重新分析\_点控制代码会检索与指定的文件或目录关联的重新分析点数据。

若要执行此操作，调用[ **FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)或[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)使用以下参数。

有关重新分析点和 FSCTL\_获取\_重新分析\_点控制代码，请参阅 Microsoft Windows SDK 文档。

**Parameters**

<a href="" id="fileobject"></a>*FileObject*  
[**FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)仅。 要从其中检索重新分析点数据的目录的文件的文件对象指针。 此参数是必需的不能**NULL**。

<a href="" id="filehandle"></a>*FileHandle*  
[**ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)仅。 文件或要从中检索重新分析点数据的目录的文件句柄。 此参数是必需的不能**NULL**。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
该操作控制代码。 使用**FSCTL\_获取\_重新分析\_点**对于此操作。

<a href="" id="inputbuffer"></a>*InputBuffer*  
不用于此操作;设置为**NULL**。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
不用于此操作;设置为零。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
指向调用方分配[**重新分析\_GUID\_数据\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff552014)或[**重新分析\_数据\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff552012)接收重分析点数据的结构。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
大小 （字节），指向的缓冲区*OutputBuffer*参数。 进行重新分析\_GUID\_数据\_缓冲区结构，此值必须是至少**sizeof**(重新分析\_GUID\_数据\_缓冲区\_标头\_大小)，以及预期的用户定义数据，和它的大小必须小于或等于最大\_重新分析\_数据\_缓冲区\_大小。 进行重新分析\_数据\_缓冲区结构，此值必须是至少**sizeof**(重新分析\_数据\_缓冲区\_标头\_大小)，加上的大小预期的用户定义数据，并且它必须是小于或等于最大\_重新分析\_数据\_缓冲区\_大小。

<a name="status-block"></a>状态块
------------

[**FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)或[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)将返回状态\_成功或适当的 NTSTATUS 值如以下之一：

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
<td align="left"><p>缓冲区的<em>OutputBuffer</em>参数指向有足够空间来存放 REPARSE_GUID_DATA_BUFFER 或 REPARSE_DATA_BUFFER 结构而不是用户定义的数据的固定的部分。 在这种情况下，在返回仅重新分析点数据的固定的部分<em>OutputBuffer</em>缓冲区。 <em>LengthReturned</em>参数<a href="https://msdn.microsoft.com/library/windows/hardware/ff542988" data-raw-source="[&lt;strong&gt;FltFsControlFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542988)"> <strong>FltFsControlFile</strong> </a>接收的实际长度，以字节为单位，返回的数据。 这是警告代码。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_BUFFER_TOO_SMALL</strong></p></td>
<td align="left"><p>缓冲区的<em>OutputBuffer</em>参数指向不是足够大以保存重新分析点数据。 <em>LengthReturned</em>参数<a href="https://msdn.microsoft.com/library/windows/hardware/ff542988" data-raw-source="[&lt;strong&gt;FltFsControlFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542988)"> <strong>FltFsControlFile</strong> </a> (或<strong>信息</strong>隶属<em>IoStatus</em>参数<a href="https://msdn.microsoft.com/library/windows/hardware/ff566462" data-raw-source="[&lt;strong&gt;ZwFsControlFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566462)"> <strong>ZwFsControlFile</strong></a>) 接收所需的缓冲区大小。 在这种情况下，未不返回任何重分析点数据。 这是一个错误代码。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_IO_REPARSE_DATA_INVALID</strong></p></td>
<td align="left"><p>其中一个指定的参数值无效。 这是一个错误代码。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_NOT_A_REPARSE_POINT</strong></p></td>
<td align="left"><p>文件或目录不是一个重新分析点。 这是一个错误代码。</p></td>
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


[**FLT\_CALLBACK\_DATA**](https://msdn.microsoft.com/library/windows/hardware/ff544620)

[**FLT\_IRP 的参数\_MJ\_文件\_系统\_控件**](flt-parameters-for-irp-mj-file-system-control.md)

[**FLT\_TAG\_DATA\_BUFFER**](https://msdn.microsoft.com/library/windows/hardware/ff544820)

[**FltFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff542988)

[**FltTagFile**](https://msdn.microsoft.com/library/windows/hardware/ff544589)

[**FltUntagFile**](https://msdn.microsoft.com/library/windows/hardware/ff544608)

[**FSCTL\_DELETE\_REPARSE\_POINT**](fsctl-delete-reparse-point.md)

[**FSCTL\_SET\_REPARSE\_POINT**](fsctl-set-reparse-point.md)

[**IRP\_MJ\_文件\_系统\_控件**](irp-mj-file-system-control.md)

[**IsReparseTagMicrosoft**](https://msdn.microsoft.com/library/windows/hardware/ff549452)

[**IsReparseTagNameSurrogate**](https://msdn.microsoft.com/library/windows/hardware/ff549462)

[**重新分析\_数据\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff552012)

[**REPARSE\_GUID\_DATA\_BUFFER**](https://msdn.microsoft.com/library/windows/hardware/ff552014)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

 

 






