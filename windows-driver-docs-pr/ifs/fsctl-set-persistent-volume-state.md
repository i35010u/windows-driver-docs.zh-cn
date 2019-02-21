---
title: FSCTL_SET_PERSISTENT_VOLUME_STATE 控制代码
description: FSCTL\_设置\_的永久\_卷\_状态控制代码设置永久设置文件系统卷。 永久设置保留在计算机的重新启动之间的文件系统卷上。
ms.assetid: 1670f3e9-c2f4-4696-a76e-bcf1bad5dc43
keywords:
- FSCTL_SET_PERSISTENT_VOLUME_STATE 控制代码可安装文件系统驱动程序
topic_type:
- apiref
api_name:
- FSCTL_SET_PERSISTENT_VOLUME_STATE
api_location:
- Ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 697dd8aa46e2f1f83a51f4fb2b59b5d4d14ca875
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533350"
---
# <a name="fsctlsetpersistentvolumestate-control-code"></a>FSCTL\_设置\_的永久\_卷\_状态控制代码


**FSCTL\_设置\_的永久\_卷\_状态**控制代码设置永久设置文件系统卷。 永久设置保留在计算机的重新启动之间的文件系统卷上。

若要执行此操作，调用[ **FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)或[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)使用以下参数。

**参数**

<a href="" id="fileobject"></a>*FileObject*  
[**FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)仅。 文件系统卷文件对象指针。 此参数是必需的不能**NULL**。

<a href="" id="filehandle"></a>*FileHandle*  
[**ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)仅。 文件系统卷的文件句柄。 此参数是必需的不能**NULL**。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作的控制代码。 使用**FSCTL\_设置\_的永久\_卷\_状态**对于此操作。

<a href="" id="inputbuffer"></a>*InputBuffer*  
指向调用方分配的指针[**文件\_FS\_的永久\_卷\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff540280)结构，其中包含永久设置文件系统卷。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
大小 （字节） 通过指向的缓冲区*InputBuffer*参数。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
不用于此操作;设置为**NULL**。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
不用于此操作;设置为零。

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
<td align="left"><p><strong>STATUS_NOT_SUPPORTED</strong></p></td>
<td align="left"><p>请求的注册表设置不是每个卷，或调用方指定的错误中的版本号<strong>版本</strong>的成员<a href="https://msdn.microsoft.com/library/windows/hardware/ff540280" data-raw-source="[&lt;strong&gt;FILE_FS_PERSISTENT_VOLUME_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540280)"> <strong>FILE_FS_PERSISTENT_VOLUME_INFORMATION</strong> </a>.</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_INVALID_PARAMETER</strong></p></td>
<td align="left"><p>文件系统卷不是一个打开的用户卷，或调用方指定中无效的标志<strong>FlagMask</strong>的成员<a href="https://msdn.microsoft.com/library/windows/hardware/ff540280" data-raw-source="[&lt;strong&gt;FILE_FS_PERSISTENT_VOLUME_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540280)"> <strong>FILE_FS_PERSISTENT_VOLUME_INFORMATION</strong></a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_BUFFER_TOO_SMALL</strong></p></td>
<td align="left"><p>缓冲区的<em>InputBuffer</em>参数指向不是大到足以保留永久性设置数据。 在这种情况下，设置没有永久设置数据。 这是一个错误代码。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_ACCESS_DENIED</strong></p></td>
<td align="left"><p>调用方无法访问文件系统卷。</p></td>
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
<td align="left"><p>从 Windows 7 开始可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ntifs.h （包括 Ntifs.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**文件\_FS\_的永久\_卷\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff540280)

[**FltFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff542988)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

 

 






