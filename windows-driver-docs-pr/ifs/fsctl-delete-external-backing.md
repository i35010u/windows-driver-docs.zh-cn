---
title: FSCTL_DELETE_EXTERNAL_BACKING 控制代码
description: FSCTL \_ 删除 \_ 外部 \_ 后备控制代码会删除文件与外部支持提供程序的关联，包括 Windows 映像格式 (WIM) 提供程序或压缩文件提供程序。
ms.assetid: 5C150899-6BCA-49EB-AEEB-0CBEC7BE60BA
keywords:
- FSCTL_DELETE_EXTERNAL_BACKING 控制代码可安装的文件系统驱动程序
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
ms.openlocfilehash: bc899d471d281f6f9ab32a656f8038464cbd3171
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065288"
---
# <a name="fsctl_delete_external_backing-control-code"></a>FSCTL \_ 删除 \_ 外部 \_ 后备控制代码


**FSCTL \_ 删除 \_ 外部 \_ 后备**控制代码会删除文件与外部支持提供程序的关联，包括 Windows 映像格式 (WIM) 提供程序或压缩文件提供程序。 作为此操作的结果，将读取、解压缩并写入到文件中的已备份文件的全部内容。

若要执行此操作，请调用具有以下参数的 [**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 或 [**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85)) 。

**参数**

<a href="" id="instance--in-"></a>*实例 \[\]*  
仅[**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 。 调用方的不透明实例指针。 此参数是必需的，不能为 NULL。

<a href="" id="fileobject--in-"></a>*FileObject \[ in\]*  
仅[**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 。 要为其删除后备关联的文件的文件指针对象。 此参数是必需的，不能为 NULL。

<a href="" id="filehandle--in-"></a>*FileHandle \[\]*  
仅[**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85)) 。 要为其删除后备关联的文件的句柄。 此参数是必需的，不能为 NULL。

<a href="" id="fscontrolcode--in-"></a>*FsControlCode \[\]*  
操作的控制代码。 使用 **FSCTL 删除此操作的 \_ \_ 外部 \_ 支持** 。

<a href="" id="inputbuffer"></a>*InputBuffer*  
无。 设置为 NULL。

<a href="" id="inputbufferlength--in-"></a>*InputBufferLength \[\]*  
设置为0。

<a href="" id="outputbuffer--out-"></a>*OutputBuffer \[\]*  
无。 设置为 NULL。

<a href="" id="outputbufferlength--out-"></a>*OutputBufferLength \[\]*  
设置为0。

<a name="status-block"></a>状态块
------------

如果操作成功，则[**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)或[**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85))返回状态 \_ SUCCESS。 否则，相应的函数可能会返回以下 NTSTATUS 值之一。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">术语</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>STATUS_OBJECT_NOT_EXTERNALLY_BACKED</strong></p></td>
<td align="left"><p>文件未从外部获得支持。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_INVALID_DEVICE_REQUEST</strong></p></td>
<td align="left"><p>后备服务不存在或未启动。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_ACCESS_DENIED</strong></p></td>
<td align="left"><p>请求者没有删除文件的后备关联的权限。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

作为删除操作的结果，将从备份源读取文件的内容，并将整个文件写入该卷。

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
<td align="left"><p>标头</p></td>
<td align="left">Ntifs (包含 Ntifs 或 Fltkernel) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)

[**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85))

[**FSCTL \_ 设置 \_ 外部 \_ 支持**](fsctl-set-external-backing.md)

 

