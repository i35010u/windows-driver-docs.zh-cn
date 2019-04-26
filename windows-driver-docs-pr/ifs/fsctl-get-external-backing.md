---
title: FSCTL_GET_EXTERNAL_BACKING 控制代码
description: FSCTL\_获取\_外部\_支持控件代码从外部备份提供程序获取文件的备份信息。
ms.assetid: 18A8E71E-CAED-4E0A-95D0-18E99F9733B2
keywords:
- FSCTL_GET_EXTERNAL_BACKING 控制代码可安装文件系统驱动程序
topic_type:
- apiref
api_name:
- FSCTL_GET_EXTERNAL_BACKING
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a84d0b877af59b917b2a1bcbdf0b1d619ca64be
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327883"
---
# <a name="fsctlgetexternalbacking-control-code"></a>FSCTL\_获取\_外部\_支持控件代码


**FSCTL\_获取\_外部\_备份**控件代码从外部备份提供程序获取文件的备份信息。 备份提供程序包括 Windows 映像格式 (WIM) 提供程序或单个压缩的文件提供程序。 从外部备份文件的内容可以驻留以外的其他包含查询的文件的卷上的卷上。

若要执行此操作，调用[ **FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)或[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)使用以下参数。

**Parameters**

<a href="" id="instance--in-"></a>*实例\[中\]*  
[**FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)仅。 调用方不透明实例指针。 此参数是必需的不能为 NULL。

<a href="" id="fileobject--in-"></a>*FileObject \[in\]*  
[**FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)仅。 为其查询支持的信息的文件的文件指针对象。 此参数是必需的不能为 NULL。

<a href="" id="filehandle--in-"></a>*FileHandle \[in\]*  
[**ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)仅。 为其查询支持的信息的文件句柄。 此参数是必需的不能为 NULL。

<a href="" id="fscontrolcode--in-"></a>*FsControlCode \[in\]*  
该操作控制代码。 使用**FSCTL\_获取\_外部\_备份**对于此操作。

<a href="" id="inputbuffer--in-"></a>*InputBuffer\[中\]*  
无。 设置为**NULL**。

<a href="" id="inputbufferlength--in-"></a>*InputBufferLength \[in\]*  
设置为 0。

<a href="" id="outputbuffer--out-"></a>*OutputBuffer\[出\]*  
指向输出缓冲区，其必须具有足够的大小以接收[ **WOF\_外部\_信息**](https://msdn.microsoft.com/library/windows/hardware/dn632452)结构后跟提供程序数据。 WIM 提供支持文件， **WOF\_外部\_信息**后跟[ **WIM\_提供程序\_外部\_信息**](https://msdn.microsoft.com/library/windows/hardware/dn632448)结构。 对于单独压缩文件， **WOF\_外部\_信息**后跟[**文件\_提供程序\_外部\_信息\_V1** ](https://msdn.microsoft.com/library/windows/hardware/mt426732)结构。

<a href="" id="outputbufferlength--out-"></a>*OutputBufferLength\[出\]*  
大小 （字节），指向的缓冲区*OutputBuffer*。

<a href="" id="lengthreturned"></a>*LengthReturned*  
指定写入的字节数*OutputBuffer*在成功完成。

<a name="status-block"></a>状态块
------------

[**FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)或[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)将返回状态\_成功如果操作成功。 否则，相应的函数可能返回以下 NTSTATUS 值之一。

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
<td align="left"><p><strong>STATUS_OBJECT_NOT_EXTERNALLY_BACKED</strong></p></td>
<td align="left"><p>从外部不支持该文件。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_INVALID_DEVICE_REQUEST</strong></p></td>
<td align="left"><p>备份服务不存在或未启动。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

如果数据源的支持提供程序来更新 WIM 文件，将包含输出缓冲区[ **WOF\_外部\_信息**](https://msdn.microsoft.com/library/windows/hardware/dn632452)结构跟[**WIM\_提供程序\_外部\_信息**](https://msdn.microsoft.com/library/windows/hardware/dn632448)结构。 *OutputBufferLength*必须至少**sizeof**(WOF\_外部\_INFO) + **sizeof**(WIM\_提供程序\_外部\_信息)。 当备份提供程序是单独压缩的文件时，将包含输出缓冲区**WOF\_外部\_信息**结构跟[**文件\_提供程序\_外部\_信息\_V1** ](https://msdn.microsoft.com/library/windows/hardware/mt426732)结构。

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
<td align="left"><p>从 Windows 8.1 更新开始可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ntifs.h （包括 Ntifs.h 或 Fltkernel.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**FltFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff542988)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

[**FSCTL\_SET\_EXTERNAL\_BACKING**](fsctl-set-external-backing.md)

[**WIM\_PROVIDER\_EXTERNAL\_INFO**](https://msdn.microsoft.com/library/windows/hardware/dn632448)

[**WOF\_EXTERNAL\_INFO**](https://msdn.microsoft.com/library/windows/hardware/dn632452)

 

 






