---
title: FSCTL_REMOVE_OVERLAY 控制代码
description: FSCTL \_ REMOVE \_ 叠加控制代码从卷中删除后备源。
ms.assetid: 9AB1DD06-AFB3-45AF-8139-14B60076D63A
keywords:
- FSCTL_REMOVE_OVERLAY 控制代码可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- FSCTL_REMOVE_OVERLAY
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c6f8659a8443a92efcf66803e8c06ab2b3f3180
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063376"
---
# <a name="fsctl_remove_overlay-control-code"></a>FSCTL \_ 删除 \_ 覆盖控制代码


**FSCTL \_ REMOVE \_ 叠加**控制代码从卷中删除后备源。

若要执行此操作，请调用具有以下参数的 [**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 或 [**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85)) 。

**参数**

<a href="" id="instance--in-"></a>*实例 \[\]*  
仅[**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 。 调用方的不透明实例指针。 此参数是必需的，不能为 NULL。

<a href="" id="fileobject--in-"></a>*FileObject \[ in\]*  
仅[**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 。 从中删除覆盖的卷的文件指针对象。 此参数是必需的，不能为 NULL。

<a href="" id="filehandle--in-"></a>*FileHandle \[\]*  
仅[**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85)) 。 要为其删除覆盖的卷的句柄。 此参数是必需的，不能为 NULL。

<a href="" id="fscontrolcode--in-"></a>*FsControlCode \[\]*  
操作的控制代码。 对于此操作，请使用 **FSCTL \_ 删除 \_ 覆盖** 区。

<a href="" id="inputbuffer"></a>*InputBuffer*  
指向输入缓冲区的指针，该缓冲区必须包含 [**WOF \_ 外部 \_ 信息**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wof_external_info) 结构。 如果需要，其他提供程序特定的数据将立即包含在 **WOF \_ 外部 \_ 信息**之后。 如果提供程序是 WIM 文件， [**wim \_ 提供程序 \_ 删除 \_ 覆盖 \_ 输入**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wim_provider_remove_overlay_input) 结构将包含在 **WOF \_ 外部 \_ 信息**之后。

<a href="" id="inputbufferlength--in-"></a>*InputBufferLength \[\]*  
设置为 **sizeof** ([**WOF \_ 外部 \_ 信息**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wof_external_info)) 以及任何其他提供程序输入数据的大小。

<a href="" id="outputbuffer--out-"></a>*OutputBuffer \[\]*  
未使用。 设置为 NULL。

<a href="" id="outputbufferlength--in-"></a>*OutputBufferLength \[\]*  
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

如果要删除的后备源为 Windows 映像格式 (WIM) 文件，则输入缓冲区将包含 [**WOF \_ 外部 \_ 信息**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wof_external_info) 结构，后面是 [**wim \_ 提供程序 \_ 删除 \_ 覆盖 \_ 输入**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wim_provider_remove_overlay_input) 结构。 在这种情况下， *InputBufferLength* 将为 **sizeof** (WOF \_ 外部 \_ 信息) + **sizeof** (**WIM \_ 提供程序 \_ 删除 \_ 覆盖 \_ 输入**) 。 Wim 提供程序中的 **DataSourceId** 值 ** \_ \_ 删除 \_ 覆盖 \_ 输入** 对于之前添加到 [**FSCTL \_ 添加 \_ 覆盖**](fsctl-add-overlay.md) 请求中的 WIM 文件必须是。

其他支持提供商将定义自己的特定输入参数结构。

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


[**FSCTL \_ 暂停 \_ 覆盖**](fsctl-suspend-overlay.md)

[**FSCTL \_ 更新 \_ 覆盖**](fsctl-update-overlay.md)

[**FSCTL \_ 获取 \_ 外部 \_ 支持**](fsctl-get-external-backing.md)

[**FSCTL \_ 设置 \_ 外部 \_ 支持**](fsctl-set-external-backing.md)

 

