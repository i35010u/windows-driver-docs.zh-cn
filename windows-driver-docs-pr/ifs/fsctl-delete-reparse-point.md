---
title: FSCTL_DELETE_REPARSE_POINT 控制代码
description: FSCTL \_ DELETE 重新 \_ 分析 \_ 点控制代码从指定的文件或目录中删除重新分析点。 使用 FSCTL \_ 删除重新 \_ 分析 \_ 点不会删除文件或目录。
ms.assetid: c8a06477-457b-47e5-b5c5-48d798fe08b3
keywords:
- FSCTL_DELETE_REPARSE_POINT 控制代码可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- FSCTL_DELETE_REPARSE_POINT
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 04aaaae46f2caee099a742019c217d2451d23435
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066188"
---
# <a name="fsctl_delete_reparse_point-control-code"></a>FSCTL \_ 删除重新 \_ 分析 \_ 点控制代码


FSCTL \_ DELETE 重新 \_ 分析 \_ 点控制代码从指定的文件或目录中删除重新分析点。 使用 FSCTL \_ 删除重新 \_ 分析 \_ 点不会删除文件或目录。

若要执行此操作，请调用具有以下参数的 [**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85)) 。

Minifilters 应使用 [**FltUntagFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltuntagfile) 而不是 FSCTL \_ 删除重新分析点 \_ \_ 来删除重新分析点。

有关重新分析点和 FSCTL \_ 删除重新 \_ 分析点控制代码的详细信息 \_ ，请参阅 Microsoft Windows SDK 文档。

**参数**

<a href="" id="filehandle"></a>*FileHandle*  
要从中删除重新分析点的文件或目录的文件句柄。 调用方必须对文件或目录具有写入访问权限。 此参数是必需的，不能为 **NULL**。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作的控制代码。 使用 FSCTL \_ 删除重新 \_ 分析 \_ 点进行此操作。

<a href="" id="inputbuffer"></a>*InputBuffer*  
指向重新 [**分析 \_ GUID \_ 数据 \_ 缓冲区**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_reparse_guid_data_buffer) 或重新 [**分析 \_ 数据 \_ 缓冲区**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_reparse_data_buffer) 结构的指针。 此结构的 **ReparseTag** 成员中指定的标记必须匹配要删除的重新分析点的标记，并且 **ReparseDataLength** 成员必须为零。 此外，如果重新分析点为第三方 (非 Microsoft) 重新分析点，则在重新分析 GUID 数据缓冲区结构的 **ReparseGuid** 成员中指定的 guid \_ \_ \_ 必须与要删除的重新分析点的 guid 匹配。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
**InputBuffer**参数指向的缓冲区的大小（以字节为单位）。 对于重新分析 \_ guid \_ 数据 \_ 缓冲区结构，此值必须是完全重新分析 \_ guid \_ 数据 \_ 缓冲区 \_ 标头 \_ 大小。 对于重新分析 \_ 数据 \_ 缓冲区结构，此值必须是完全重新分析 \_ 数据 \_ 缓冲区 \_ 标头 \_ 大小。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
不与此操作一起使用;设置为 **NULL**。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
不与此操作一起使用;设置为零。

<a name="status-block"></a>状态块
------------

[**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85)) 返回状态 \_ "成功" 或相应的 NTSTATUS 值，如下所示：

<a href="" id="status-io-reparse-data-invalid"></a>状态 \_ IO 重新 \_ 分析 \_ 数据 \_ 无效  
指定的参数值之一无效。 这是一个错误代码。

<a href="" id="status-io-reparse-tag-invalid"></a>状态 \_ IO 重新 \_ 分析 \_ 标记 \_ 无效  
调用方指定的重新分析标记无效。 这是一个错误代码。

<a href="" id="status-io-reparse-tag-mismatch"></a>状态 \_ IO 重新 \_ 分析 \_ 标记 \_ 不匹配  
调用方指定的重新分析标记与要删除的重新分析点的标记不匹配。 这是一个错误代码。

<a href="" id="status-reparse-attribute-conflict"></a>状态重新 \_ 分析 \_ 属性 \_ 冲突  
重新分析点是第三方重新分析点，并且调用方指定的重新分析 GUID 与要删除的重新分析点的 GUID 不匹配。 这是一个错误代码。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Ntifs (包含 Ntifs 或 Fltkernel) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**\_IRP \_ MJ \_ 文件 \_ 系统 \_ 控件的 FLT 参数**](flt-parameters-for-irp-mj-file-system-control.md)

[**FltTagFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-flttagfile)

[**FltUntagFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltuntagfile)

[**FSCTL \_ 获取重新 \_ 分析 \_ 点**](fsctl-get-reparse-point.md)

[**FSCTL \_ 设置 \_ 重分析 \_ 点**](fsctl-set-reparse-point.md)

[**IRP \_ MJ \_ 文件 \_ 系统 \_ 控制**](irp-mj-file-system-control.md)

[**IsReparseTagMicrosoft**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-isreparsetagmicrosoft)

[**IsReparseTagNameSurrogate**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-isreparsetagnamesurrogate)

[**重新分析 \_ 数据 \_ 缓冲区**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_reparse_data_buffer)

[**重新分析 \_ GUID \_ 数据 \_ 缓冲区**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_reparse_guid_data_buffer)

[**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85))

 

