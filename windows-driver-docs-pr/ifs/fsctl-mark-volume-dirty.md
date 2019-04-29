---
title: FSCTL_MARK_VOLUME_DIRTY 控制代码
description: FSCTL\_标记\_卷\_脏控制代码将标记指定的卷为已更新，这会触发 Autochk.exe 在下次系统重新启动过程中在卷上运行。
ms.assetid: 9062b212-fc8a-4467-b32f-047fc3702445
keywords:
- FSCTL_MARK_VOLUME_DIRTY 控制代码可安装文件系统驱动程序
topic_type:
- apiref
api_name:
- FSCTL_MARK_VOLUME_DIRTY
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d90cde19dc53dfc9ebefcd8f876d5643a161afd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391783"
---
# <a name="fsctlmarkvolumedirty-control-code"></a>FSCTL\_标记\_卷\_脏控制代码


**FSCTL\_标记\_卷\_繁琐**控制代码将标记指定的卷为已更新，这会触发 Autochk.exe 在下次系统重新启动过程中在卷上运行。

若要执行此操作，调用[ **FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)或[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)使用以下参数。

**Parameters**

<a href="" id="instance"></a>*实例*  
[**FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)仅。 指向正在启动 FSCTL 请求微筛选器驱动程序实例的不透明实例指针。

<a href="" id="fileobject"></a>*FileObject*  
[**FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)仅。 文件指针对象指定要将标记为已更新的卷。 此参数是必需的不能**NULL**。

<a href="" id="filehandle"></a>*FileHandle*  
[**ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)仅。 若要将标记为已更新的卷句柄。 此参数是必需的不能**NULL**。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作的控制代码。 使用**FSCTL\_标记\_卷\_繁琐**对于此操作。

<a href="" id="inputbuffer"></a>*InputBuffer*  
不使用与此操作。 设置为**NULL**。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
不使用与此操作。 设置为 0。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
不使用与此操作。 设置为**NULL**。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
不使用与此操作。 设置为 0。

<a name="status-block"></a>状态块
------------

[ **FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)或[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)例程将返回状态\_成功或相应 NTSTATUS值。

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
<td align="left"><p><em>的文件对象</em>或<em>FileHandle</em>不表示有效卷句柄或另一个参数无效。</p></td>
</tr>
<tr class="even">
<td align="left"><p> <strong>STATUS_ACCESS_DENIED</strong></p></td>
<td align="left"><p>调用方没有 SE_MANAGE_VOLUME 访问权限。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_VOLUME_DISMOUNTED</strong></p></td>
<td align="left"><p>文件系统卷已卸除。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_TOO_LATE</strong></p></td>
<td align="left"><p>文件系统卷将关闭。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_MEDIA_WRITE_PROTECTED</strong></p></td>
<td align="left"><p>文件系统卷是只读的。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

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
<td align="left"><p>Header</p></td>
<td align="left">Ntifs.h （包括 FltKernel.h 或 Ntifs.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**FltFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff542988)

[**FSCTL\_IS\_卷\_繁琐**](fsctl-is-volume-dirty.md)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

 

 






