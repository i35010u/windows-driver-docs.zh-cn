---
title: FSCTL_DELETE_EXTERNAL_BACKING 控制代码
description: FSCTL\_删除\_外部\_支持控件代码中删除与外部备份提供程序，包括 Windows 映像格式 (WIM) 提供程序或压缩的文件提供程序的文件关联。
ms.assetid: 5C150899-6BCA-49EB-AEEB-0CBEC7BE60BA
keywords:
- FSCTL_DELETE_EXTERNAL_BACKING 控制代码可安装文件系统驱动程序
topic_type:
- apiref
api_name:
- FSCTL_DELETE_EXTERNAL_BACKING
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ed30e496cbffc0a55f84fb574ef43cd12de7d2f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373963"
---
# <a name="fsctldeleteexternalbacking-control-code"></a>FSCTL\_删除\_外部\_支持控件代码


**FSCTL\_删除\_外部\_备份**控制代码中删除与外部备份提供程序，包括 Windows 映像格式 (WIM) 提供程序或压缩的文件关联文件提供程序。 完成此操作后备份文件的全部内容读取、 解压缩，并写入到文件。

若要执行此操作，调用[ **FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)或[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)使用以下参数。

**Parameters**

<a href="" id="instance--in-"></a>*实例\[中\]*  
[**FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)仅。 调用方不透明实例指针。 此参数是必需的不能为 NULL。

<a href="" id="fileobject--in-"></a>*FileObject \[in\]*  
[**FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)仅。 为其删除备份关联的文件的文件指针对象。 此参数是必需的不能为 NULL。

<a href="" id="filehandle--in-"></a>*FileHandle \[in\]*  
[**ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)仅。 为其删除备份关联的文件句柄。 此参数是必需的不能为 NULL。

<a href="" id="fscontrolcode--in-"></a>*FsControlCode \[in\]*  
操作的控制代码。 使用**FSCTL\_删除\_外部\_备份**对于此操作。

<a href="" id="inputbuffer"></a>*InputBuffer*  
无。 设置为 NULL。

<a href="" id="inputbufferlength--in-"></a>*InputBufferLength \[in\]*  
设置为 0。

<a href="" id="outputbuffer--out-"></a>*OutputBuffer\[出\]*  
无。 设置为 NULL。

<a href="" id="outputbufferlength--out-"></a>*OutputBufferLength\[出\]*  
设置为 0。

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
<tr class="odd">
<td align="left"><p><strong>STATUS_ACCESS_DENIED</strong></p></td>
<td align="left"><p>请求者没有删除该文件的备份关联的权限。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

由于删除操作，而从备份源读取该文件的内容和整个文件写入到卷。

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

 

 






