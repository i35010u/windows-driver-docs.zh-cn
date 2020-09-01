---
title: FSCTL_ENUM_OVERLAY 控制代码
description: FSCTL \_ 枚举 \_ 覆盖控制代码枚举指定卷的后备提供程序中的所有数据源。
ms.assetid: 146A7D77-034F-4C06-99B8-8EBA6E7F0A40
keywords:
- FSCTL_ENUM_OVERLAY 控制代码可安装的文件系统驱动程序
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
ms.openlocfilehash: f1774fa8a00d188e3e5ab0368355c93093358e21
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065598"
---
# <a name="fsctl_enum_overlay-control-code"></a>FSCTL \_ 枚举 \_ 重叠控制代码


**FSCTL \_ 枚举 \_ 覆盖**控制代码枚举指定卷的后备提供程序中的所有数据源。

若要执行此操作，请调用具有以下参数的 [**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 或 [**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85)) 。

**参数**

<a href="" id="instance--in-"></a>*实例 \[\]*  
仅[**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 。 调用方的不透明实例指针。 此参数是必需的，不能为 **NULL**。

<a href="" id="fileobject--in-"></a>*FileObject \[ in\]*  
仅[**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 。 文件指针对象，指定要卸除的卷。 此参数是必需的，不能为 **NULL**。

<a href="" id="filehandle--in-"></a>*FileHandle \[\]*  
仅[**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85)) 。 要卸除的卷的文件句柄。 此参数是必需的，不能为 **NULL**。

<a href="" id="fscontrolcode--in-"></a>*FsControlCode \[\]*  
操作的控制代码。 对于此操作，请使用 **FSCTL \_ 删除 \_ 覆盖** 区。

<a href="" id="inputbuffer"></a>*InputBuffer*  
指向输入缓冲区的指针，该缓冲区必须包含 [**WOF \_ 外部 \_ 信息**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wof_external_info) 结构。

<a href="" id="inputbufferlength--in-"></a>*InputBufferLength \[\]*  
设置为 **sizeof** (WOF \_ EXTERNAL \_ INFO) 。

<a href="" id="outputbuffer--out-"></a>*OutputBuffer \[\]*  
指向输出缓冲区的指针，该缓冲区将为支持卷的数据源接收一个或多个 [**WIM \_ 提供程序 \_ 覆盖 \_ 条目**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wim_provider_update_overlay_input) 结构。

<a href="" id="outputbufferlength--out-"></a>*OutputBufferLength \[\]*  
*OutputBuffer*所指向的缓冲区大小（以字节为单位）。

<a href="" id="lengthreturned--out-"></a>*LengthReturned \[\]*  
指定成功完成后写入到 *OutputBuffer* 中的字节数。

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
<td align="left"><p><strong>STATUS_ACCESS_DENIED</strong></p></td>
<td align="left"><p>请求者没有管理权限。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_BUFFER_TOO_SMALL</strong></p></td>
<td align="left"><p><em>OutputBuffer</em>指向的和由<em>OutputBufferLength</em>指定的输出缓冲区的长度太小。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_INTERNAL_ERROR</strong></p></td>
<td align="left"><p>请求的卷不可访问。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_INVALID_DEVICE_REQUEST</strong></p></td>
<td align="left"><p>后备服务不存在或未启动。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

枚举 WIM 提供程序的数据源时，输出缓冲区将包含 [**wim \_ 提供程序 \_ 覆盖 \_ 条目**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wim_provider_update_overlay_input) 结构的数组。 输出缓冲区的大小必须足够大才能包含所有覆盖项，否则调用将返回状态 \_ 缓冲区 \_ 太 \_ 小。

其他支持提供商将定义自己的特定枚举结构。

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

[**FSCTL \_ 添加 \_ 覆盖区**](fsctl-add-overlay.md)

[**WOF \_ 外部 \_ 信息**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wof_external_info)

 

