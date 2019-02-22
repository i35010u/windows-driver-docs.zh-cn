---
title: FSCTL_GET_RETRIEVAL_POINTER_BASE 控制代码
description: FSCTL\_获取\_检索\_指针\_基将相对于卷的开始文件系统的第一个逻辑群集数 (LCN) 返回的扇区偏移量。
ms.assetid: 2c342e58-ef9a-487a-beb9-4353dcbc8115
keywords:
- FSCTL_GET_RETRIEVAL_POINTER_BASE 控制代码可安装文件系统驱动程序
topic_type:
- apiref
api_name:
- FSCTL_GET_RETRIEVAL_POINTER_BASE
api_location:
- Ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e74d5378ac92f6698bcbd0e96be9b2305e33e39
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545132"
---
# <a name="fsctlgetretrievalpointerbase-control-code"></a>FSCTL\_获取\_检索\_指针\_基控件代码


**FSCTL\_获取\_检索\_指针\_基本**相对于卷的开始文件系统的第一个逻辑群集数 (LCN) 返回的扇区偏移量。

若要执行此操作，调用[ **FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)函数或[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)以下函数参数。

**参数**

<a href="" id="fileobject--in-"></a>*FileObject \[in\]*  
[**FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)仅。 为其卷的文件对象指针**FSCTL\_获取\_检索\_指针\_基**是检索 base。 此参数是必需的不能**NULL**。

<a href="" id="filehandle"></a>*FileHandle*  
[**ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)仅。 为其卷的文件句柄**FSCTL\_获取\_检索\_指针\_基**是检索 base。 此参数是必需的不能**NULL**。

必须使用 SE 打开此句柄\_管理\_卷\_名称访问权限。 有关详细信息，请参阅[文件安全和访问权限](https://msdn.microsoft.com/library/windows/desktop/aa364399)。

<a href="" id="fscontrolcode--in-"></a>*FsControlCode \[in\]*  
该操作控制代码。 使用**FSCTL\_获取\_检索\_指针\_基本**对于此操作。

<a href="" id="inputbuffer"></a>*InputBuffer*  
不使用与此操作。 设置为**NULL**。

<a href="" id="inputbufferlength--in-"></a>*InputBufferLength \[in\]*  
不使用与此操作。 设置为零。

<a href="" id="outputbuffer--out-"></a>*OutputBuffer\[出\]*  
一个指向大\_接收到文件系统相对于卷的开始的第一个 LCN 的扇区偏移量的整数。

<a href="" id="outputbufferlength--in-"></a>*OutputBufferLength \[in\]*  
输出缓冲区，以字节为单位的大小。 此值必须为 8。

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
<td align="left"><p><strong>STATUS_SUCCESS</strong></p></td>
<td align="left"><p>操作成功。 OutputBuffer 包含到文件系统相对于卷的开始的第一个 LCN 的扇区偏移量。</p></td>
</tr>
<tr class="even">
<td align="left"><p> <strong>STATUS_ACCESS_DENIED</strong></p></td>
<td align="left"><p>用户没有 SE_MANAGE_VOLUME 访问。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_BUFFER_TOO_SMALL</strong></p></td>
<td align="left"><p>OutputBuffer 不足够大的结果。 已向缓冲区不写入任何信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_INVALID_PARAMETER</strong></p></td>
<td align="left"><p>参数不是有效，则为例如，使用的句柄不是有效的批量句柄。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

添加 FSCTL 检索到的值\_获取\_检索\_指针\_FSCTL 检索到的值的基本\_获取\_检索\_指针控制代码结果中的卷相关的文件范围偏移量。

FSCTL\_获取\_检索\_指针\_可 FastFAT 和 exFAT 的设备上使用的基控件的代码。 此功能支持的设备，例如闪存驱动器使用 BitLocker。

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
<td align="left"><p>Windows Server 2008 R2, Windows 7</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ntifs.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**FltFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff542988)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

 

 






