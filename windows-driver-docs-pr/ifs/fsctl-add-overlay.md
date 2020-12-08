---
title: FSCTL_ADD_OVERLAY 控制代码
description: FSCTL \_ ADD \_ 叠加控制代码将新的外部后备源添加到卷的命名空间。 此后备源可以是 Windows 映像格式 (WIM) 文件。
keywords:
- FSCTL_ADD_OVERLAY 控制代码可安装的文件系统驱动程序
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
ms.openlocfilehash: 301281089927163a88cfa032d54a7376592b3cd5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826853"
---
# <a name="fsctl_add_overlay-control-code"></a>FSCTL \_ 添加 \_ 覆盖控制代码


**FSCTL \_ ADD \_ 叠加** 控制代码将新的外部后备源添加到卷的命名空间。 此后备源可以是 Windows 映像格式 (WIM) 文件。

若要执行此操作，请调用具有以下参数的 [**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 或 [**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85)) 。

**Parameters**

<a href="" id="instance--in-"></a>*实例 \[\]*  
仅 [**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 。 调用方的不透明实例指针。 此参数是必需的，不能为 NULL。

<a href="" id="fileobject--in-"></a>*FileObject \[ in\]*  
仅 [**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 。 要向其添加覆盖的卷的文件指针对象。 此参数是必需的，不能为 NULL。

<a href="" id="filehandle--in-"></a>*FileHandle \[\]*  
仅 [**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85)) 。 要向其添加覆盖的卷的句柄。 此参数是必需的，不能为 NULL。

<a href="" id="fscontrolcode--in-"></a>*FsControlCode \[\]*  
操作的控制代码。 使用 FSCTL 为此操作 **\_ 添加 \_ 覆盖** 区。

<a href="" id="inputbuffer"></a>*InputBuffer*  
指向输入缓冲区的指针，该缓冲区必须包含 [**WOF \_ 外部 \_ 信息**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wof_external_info) 结构。 如果需要，其他提供程序特定的数据将立即包含在 **WOF \_ 外部 \_ 信息** 之后。

<a href="" id="inputbufferlength--in-"></a>*InputBufferLength \[\]*  
设置为 **sizeof** ([**WOF \_ 外部 \_ 信息**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wof_external_info)) 以及任何其他提供程序输入数据的大小。

<a href="" id="outputbuffer--out-"></a>*OutputBuffer \[\]*  
指向输出缓冲区的指针，其中包含来自添加操作的所有结果信息。

<a href="" id="outputbufferlength--out-"></a>*OutputBufferLength \[\]*  
*OutputBuffer* 所指向的缓冲区大小。

<a name="status-block"></a>状态块
------------

如果操作成功，则 [**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)或 [**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85))返回状态 \_ SUCCESS。 否则，相应的函数可能会返回以下 NTSTATUS 值之一。

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
<td align="left"><p>请求者没有管理权限。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_BUFFER_TOO_SMALL</strong></p></td>
<td align="left"><p><em>OutputBuffer</em>（由<em>OutputBufferLength</em>指定）指向的输出缓冲区的长度太小。</p></td>
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

如果添加的后备源为 Windows 映像格式 (WIM) 文件，则输入缓冲区将包含 [**WOF \_ 外部 \_ 信息**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wof_external_info) 结构，后面是 [**wim \_ 提供程序 \_ 添加 \_ 覆盖 \_ 输入**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wim_provider_add_overlay_input) 结构。 在这种情况下， *InputBufferLength* 将为 **sizeof** (**WOF \_ 外部 \_ 信息**) + **sizeof** (**WIM \_ 提供程序 \_ 添加 \_ 覆盖 \_ 输入**) 。 完成请求后， *OutputBuffer* 指向的数据包含一个大 \_ 整数值，该值是 WIM 文件的新数据源标识符。

其他支持提供商将定义自己的特定输入参数结构和输出数据类型。

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

## <a name="see-also"></a>请参阅


[**FSCTL \_ 删除 \_ 覆盖**](fsctl-remove-overlay.md)

[**FSCTL \_ 暂停 \_ 覆盖**](fsctl-suspend-overlay.md)

[**FSCTL \_ 更新 \_ 覆盖**](fsctl-update-overlay.md)

[**FSCTL \_ 获取 \_ 外部 \_ 支持**](fsctl-get-external-backing.md)

[**FSCTL \_ 设置 \_ 外部 \_ 支持**](fsctl-set-external-backing.md)

 

