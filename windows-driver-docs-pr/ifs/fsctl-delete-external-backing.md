---
title: FSCTL_DELETE_EXTERNAL_BACKING 控制代码
description: FSCTL\_DELETE\_外部\_后备控制代码删除文件与外部支持提供商（包括 Windows 映像格式（WIM）提供程序或压缩文件提供程序）的关联。
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
ms.openlocfilehash: 6a2072c3a3efd9ecf93f418a4e49bfc2caee5956
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841324"
---
# <a name="fsctl_delete_external_backing-control-code"></a>FSCTL\_删除\_外部\_后备控制代码


**FSCTL\_DELETE\_外部\_后备**控制代码删除文件与外部支持提供商（包括 Windows 映像格式（WIM）提供程序或压缩文件提供程序）的关联。 作为此操作的结果，将读取、解压缩并写入到文件中的已备份文件的全部内容。

若要执行此操作，请调用具有以下参数的[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)或[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462) 。

**Parameters**

<a href="" id="instance--in-"></a>*实例 \[\]*  
仅[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 。 调用方的不透明实例指针。 此参数是必需的，不能为 NULL。

<a href="" id="fileobject--in-"></a>*FileObject \[\]*  
仅[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 。 要为其删除后备关联的文件的文件指针对象。 此参数是必需的，不能为 NULL。

<a href="" id="filehandle--in-"></a> *\]中的 FileHandle \[*  
仅[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462) 。 要为其删除后备关联的文件的句柄。 此参数是必需的，不能为 NULL。

<a href="" id="fscontrolcode--in-"></a> *\]中的 FsControlCode \[*  
操作的控制代码。 使用**FSCTL\_删除\_外部\_** 为此操作提供支持。

<a href="" id="inputbuffer"></a>*InputBuffer*  
无。 设置为 NULL。

<a href="" id="inputbufferlength--in-"></a> *\]中的 InputBufferLength \[*  
设置为0。

<a href="" id="outputbuffer--out-"></a>*OutputBuffer \[out\]*  
无。 设置为 NULL。

<a href="" id="outputbufferlength--out-"></a>*OutputBufferLength \[out\]*  
设置为0。

<a name="status-block"></a>状态块
------------

如果操作成功，则[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)或[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)返回状态\_成功。 否则，相应的函数可能会返回以下 NTSTATUS 值之一。

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
<td align="left">Ntifs （包括 Ntifs 或 Fltkernel）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

[**FSCTL\_设置\_外部\_后备**](fsctl-set-external-backing.md)

 

 






