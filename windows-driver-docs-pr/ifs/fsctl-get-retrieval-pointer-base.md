---
title: FSCTL_GET_RETRIEVAL_POINTER_BASE 控制代码
description: FSCTL \_ 获取 \_ 检索 \_ 指针 \_ 基准返回相对于卷开头的文件系统 (LCN) 的第一个逻辑群集号的扇区偏移量。
keywords:
- FSCTL_GET_RETRIEVAL_POINTER_BASE 控制代码可安装的文件系统驱动程序
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
ms.openlocfilehash: 93a02407f12bf7d7645af622a02c83ca4dd8867a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808373"
---
# <a name="fsctl_get_retrieval_pointer_base-control-code"></a>FSCTL \_ 获取 \_ 检索 \_ 指针 \_ 基控制代码


**FSCTL \_ 获取 \_ 检索 \_ 指针 \_ 基准** 返回相对于卷开头的文件系统 (LCN) 的第一个逻辑群集号的扇区偏移量。

若要执行此操作，请调用具有以下参数的 [**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 函数或 [**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85)) 函数。

**Parameters**

<a href="" id="fileobject--in-"></a>*FileObject \[ in\]*  
仅 [**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 。 **FSCTL \_ 获取 \_ 检索 \_ 指针 \_ 基** 的卷的文件对象指针。 此参数是必需的，不能为 **NULL**。

<a href="" id="filehandle"></a>*FileHandle*  
仅 [**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85)) 。 **FSCTL \_ 获取 \_ 检索 \_ 指针 \_ 基** 的卷的文件句柄。 此参数是必需的，不能为 **NULL**。

必须使用 SE \_ 管理 \_ 卷 \_ 名访问权限打开此句柄。 有关详细信息，请参阅 [文件安全性和访问权限](/windows/desktop/FileIO/file-security-and-access-rights)。

<a href="" id="fscontrolcode--in-"></a>*FsControlCode \[\]*  
操作的控制代码。 对于此操作，请使用 **FSCTL \_ GET \_ 检索 \_ 指针 \_ 基** 。

<a href="" id="inputbuffer"></a>*InputBuffer*  
不与此操作一起使用。 设置为 **NULL**。

<a href="" id="inputbufferlength--in-"></a>*InputBufferLength \[\]*  
不与此操作一起使用。 设置为零。

<a href="" id="outputbuffer--out-"></a>*OutputBuffer \[\]*  
指向一个大整数的指针 \_ ，该指针接收相对于卷开头的文件系统的第一个 LCN 的扇区偏移量。

<a href="" id="outputbufferlength--in-"></a>*OutputBufferLength \[\]*  
输出缓冲区的大小（以字节为单位）。 此值必须是8。

<a name="status-block"></a>状态块
------------

[**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 或 [**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85)) 返回状态 \_ "成功" 或相应的 NTSTATUS 值，如下所示：

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
<td align="left"><p>操作成功。 OutputBuffer 包含相对于卷开头的文件系统的第一个 LCN 的扇区偏移量。</p></td>
</tr>
<tr class="even">
<td align="left"><p> <strong>STATUS_ACCESS_DENIED</strong></p></td>
<td align="left"><p>用户没有 SE_MANAGE_VOLUME 的访问权限。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_BUFFER_TOO_SMALL</strong></p></td>
<td align="left"><p>OutputBuffer 不够大，无法满足结果。 未将任何信息写入缓冲区。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_INVALID_PARAMETER</strong></p></td>
<td align="left"><p>参数无效;例如，使用的句柄不是有效的卷句柄。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

将 FSCTL 检索指针基检索到的值添加 \_ \_ \_ \_ 到 FSCTL get 检索指针所检索的值， \_ \_ \_ 控制代码会导致卷相对文件区偏移量。

\_ \_ \_ \_ 可在 FastFAT 和 EXFAT 设备上使用 FSCTL GET 检索指针基本控制代码。 此功能支持为闪存驱动器等设备使用 BitLocker。

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
<td align="left"><p>Windows Server 2008 R2，Windows 7</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ntifs</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)

[**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85))

 

