---
title: FSCTL_ADD_OVERLAY 控制代码
description: FSCTL\_添加\_OVERLAY 控件代码将新的外部备份源添加到卷的命名空间。 此备份源可以是 Windows 映像格式 (WIM) 文件。
ms.assetid: 0507ECDE-49C6-4EC4-87D6-76D6475620F4
keywords:
- FSCTL_ADD_OVERLAY 控制代码可安装文件系统驱动程序
topic_type:
- apiref
api_name:
- FSCTL_ADD_OVERLAY
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53b4ceecfa7e9a541a53d8fd28febc1bd1bcb114
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327891"
---
# <a name="fsctladdoverlay-control-code"></a>FSCTL\_添加\_OVERLAY 控件代码


**FSCTL\_添加\_覆盖**控制代码将新的外部备份源添加到卷的命名空间。 此备份源可以是 Windows 映像格式 (WIM) 文件。

若要执行此操作，调用[ **FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)或[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)使用以下参数。

**Parameters**

<a href="" id="instance--in-"></a>*实例\[中\]*  
[**FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)仅。 调用方不透明实例指针。 此参数是必需的不能为 NULL。

<a href="" id="fileobject--in-"></a>*FileObject \[in\]*  
[**FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)仅。 文件指针将覆盖添加到卷的对象。 此参数是必需的不能为 NULL。

<a href="" id="filehandle--in-"></a>*FileHandle \[in\]*  
[**ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)仅。 将覆盖添加到卷的句柄。 此参数是必需的不能为 NULL。

<a href="" id="fscontrolcode--in-"></a>*FsControlCode \[in\]*  
操作的控制代码。 使用**FSCTL\_添加\_覆盖**对于此操作。

<a href="" id="inputbuffer"></a>*InputBuffer*  
指向输入缓冲区，必须包含[ **WOF\_外部\_信息**](https://msdn.microsoft.com/library/windows/hardware/dn632452)结构。 在需要时，其他提供程序特定的数据是包含后立即**WOF\_外部\_信息**。

<a href="" id="inputbufferlength--in-"></a>*InputBufferLength \[in\]*  
设置为**sizeof**([**WOF\_外部\_信息**](https://msdn.microsoft.com/library/windows/hardware/dn632452)) 加上任何其他提供程序输入数据的大小。

<a href="" id="outputbuffer--out-"></a>*OutputBuffer\[出\]*  
指向输出缓冲区，其中包含添加操作的任何结果信息的指针。

<a href="" id="outputbufferlength--out-"></a>*OutputBufferLength\[出\]*  
指向缓冲区的大小*OutputBuffer*。

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
<td align="left"><p>指向输出缓冲区的长度<em>OutputBuffer</em>，并通过指定<em>OutputBufferLength</em>，太小。</p></td>
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

Windows 映像格式 (WIM) 文件添加的后备源时，将包含输入的缓冲区[ **WOF\_外部\_信息**](https://msdn.microsoft.com/library/windows/hardware/dn632452)结构跟[**WIM\_提供程序\_添加\_覆盖\_输入**](https://msdn.microsoft.com/library/windows/hardware/dn632447)结构。 *InputBufferLength*在这种情况下将为**sizeof**(**WOF\_外部\_信息**) + **sizeof**(**WIM\_提供程序\_添加\_覆盖\_输入**)。 请求完成后，数据由指向*OutputBuffer*包含单一大型\_即 WIM 文件的新数据源标识符的整数值。

其他支持提供商将定义他们自己特定的输入的参数的结构和输出数据类型。

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


[**FSCTL\_REMOVE\_OVERLAY**](fsctl-remove-overlay.md)

[**FSCTL\_SUSPEND\_OVERLAY**](fsctl-suspend-overlay.md)

[**FSCTL\_UPDATE\_OVERLAY**](fsctl-update-overlay.md)

[**FSCTL\_GET\_EXTERNAL\_BACKING**](fsctl-get-external-backing.md)

[**FSCTL\_SET\_EXTERNAL\_BACKING**](fsctl-set-external-backing.md)

 

 






