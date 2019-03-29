---
title: FSCTL_ENUM_OVERLAY 控制代码
description: FSCTL\_枚举\_OVERLAY 控件代码枚举从指定的卷的备份提供程序的所有数据源。
ms.assetid: 146A7D77-034F-4C06-99B8-8EBA6E7F0A40
keywords:
- FSCTL_ENUM_OVERLAY 控制代码可安装文件系统驱动程序
topic_type:
- apiref
api_name:
- FSCTL_ENUM_OVERLAY
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37404a1e47e980836fc981c080ec2b376f4f3bfc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565752"
---
# <a name="fsctlenumoverlay-control-code"></a>FSCTL\_枚举\_OVERLAY 控件代码


**FSCTL\_枚举\_覆盖**控制代码枚举从指定的卷的备份提供程序的所有数据源。

若要执行此操作，调用[ **FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)或[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)使用以下参数。

**Parameters**

<a href="" id="instance--in-"></a>*实例\[中\]*  
[**FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)仅。 调用方的不透明实例指针。 此参数是必需的不能**NULL**。

<a href="" id="fileobject--in-"></a>*FileObject \[in\]*  
[**FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)仅。 文件指针对象指定要卸除卷。 此参数是必需的不能**NULL**。

<a href="" id="filehandle--in-"></a>*FileHandle \[in\]*  
[**ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)仅。 要卸除的卷的文件句柄。 此参数是必需的不能**NULL**。

<a href="" id="fscontrolcode--in-"></a>*FsControlCode \[in\]*  
操作的控制代码。 使用**FSCTL\_删除\_覆盖**对于此操作。

<a href="" id="inputbuffer"></a>*InputBuffer*  
指向输入缓冲区，必须包含[ **WOF\_外部\_信息**](https://msdn.microsoft.com/library/windows/hardware/dn632452)结构。

<a href="" id="inputbufferlength--in-"></a>*InputBufferLength \[in\]*  
设置为**sizeof**(WOF\_外部\_信息)。

<a href="" id="outputbuffer--out-"></a>*OutputBuffer\[出\]*  
指向将接收一个或多个输出缓冲区的指针[ **WIM\_提供程序\_覆盖\_条目**](https://msdn.microsoft.com/library/windows/hardware/dn632451)支持该卷的数据源的结构。

<a href="" id="outputbufferlength--out-"></a>*OutputBufferLength\[出\]*  
指向缓冲区的大小*OutputBuffer*，以字节为单位。

<a href="" id="lengthreturned--out-"></a>*LengthReturned\[出\]*  
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
<td align="left"><p><strong>STATUS_ACCESS_DENIED</strong></p></td>
<td align="left"><p>请求者不具有管理权限。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_BUFFER_TOO_SMALL</strong></p></td>
<td align="left"><p>指向输出缓冲区的长度<em>OutputBuffer</em>并指定由<em>OutputBufferLength</em>太小。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_INTERNAL_ERROR</strong></p></td>
<td align="left"><p>该请求的卷不可访问。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_INVALID_DEVICE_REQUEST</strong></p></td>
<td align="left"><p>备份服务不存在或未启动。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

输出缓冲区时为 WIM 提供程序枚举数据源，将包含的一组[ **WIM\_提供程序\_覆盖\_条目**](https://msdn.microsoft.com/library/windows/hardware/dn632451)结构。 输出缓冲区的大小必须足够大以包含所有覆盖项或调用将返回状态\_缓冲区\_过\_小。

其他支持提供程序将定义他们自己特定的枚举的结构。

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

[**FSCTL\_ADD\_OVERLAY**](fsctl-add-overlay.md)

[**WOF\_EXTERNAL\_INFO**](https://msdn.microsoft.com/library/windows/hardware/dn632452)

 

 






