---
title: FSCTL_OFFLOAD_READ 控制代码
description: FSCTL \_ 卸载 \_ 读取控制代码为支持卸载读取基元的存储系统中的数据块启动卸载读取。
ms.assetid: D9A22A8F-9B7E-4BF7-8FBD-267BE4C8DC59
keywords:
- FSCTL_OFFLOAD_READ 控制代码可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- FSCTL_OFFLOAD_READ
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f59edea909b15e5f9438e9448a8a794fc6d0451c
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90105190"
---
# <a name="fsctl_offload_read-control-code"></a>FSCTL \_ 卸载 \_ 读取控制代码


**FSCTL \_ 卸载 \_ 读取**控制代码为支持卸载读取基元的存储系统中的数据块启动卸载读取。

若要执行此操作，请调用具有以下参数的 [**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 或 [**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85)) 。

**参数**

<a href="" id="instance--in-"></a>*实例 \[\]*  
仅[**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 。 调用方的不透明实例指针。 此参数是必需的，不能为 NULL。

<a href="" id="fileobject--in-"></a>*FileObject \[ in\]*  
仅[**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 。 文件指针对象，该对象指定要读取的文件。 此参数是必需的，不能为 NULL。

<a href="" id="filehandle--in-"></a>*FileHandle \[\]*  
仅[**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85)) 。 要读取的文件的文件句柄。 此参数是必需的，不能为 NULL。

<a href="" id="fscontrolcode--in-"></a>*FsControlCode \[\]*  
操作的控制代码。 使用 **FSCTL \_ 卸载 \_ 读取** 此操作。

<a href="" id="inputbuffer"></a>*InputBuffer*  
指向 [**FSCTL \_ 卸载 \_ 读取 \_ 输入**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsctl_offload_read_input) 结构的指针，该结构包含要读取的数据块的大小和偏移量。

<a href="" id="inputbufferlength--in-"></a>*InputBufferLength \[\]*  
*InputBuffer*指向的缓冲区的大小（以字节为单位）。 此值为 **sizeof** (FSCTL \_ 卸载 \_ 读取 \_ 输入) 。

<a href="" id="outputbuffer--out-"></a>*OutputBuffer \[\]*  
指向 [**FSCTL \_ 卸载 \_ 读取 \_ 输出**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsctl_offload_read_output) 结构的指针，该结构接收卸载读取操作的结果。

<a href="" id="outputbufferlength--out-"></a>*OutputBufferLength \[\]*  
*OutputBuffer*参数指向的缓冲区的大小（以字节为单位）。 此值必须至少为 **sizeof** (FSCTL \_ 卸载 \_ 读取 \_ 输出) 。

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
<td align="left"><p><strong>STATUS_INVALID_DEVICE_REQUEST</strong></p></td>
<td align="left"><p>指定的句柄不是有效的文件句柄。</p></td>
</tr>
<tr class="even">
<td align="left"><p> <strong>STATUS_INVALID_PARAMETER</strong></p></td>
<td align="left"><p>文件大小小于 PAGE_SIZE。</p>
<p>- 或 -</p>
<p><em>InputBufferLength</em> &lt;<strong>sizeof</strong> (FSCTL_OFFLOAD_READ_INPUT) 。</p>
<p>- 或 -</p>
<p><a href="/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsctl_offload_read_input" data-raw-source="[&lt;strong&gt;FSCTL_OFFLOAD_READ_INPUT&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsctl_offload_read_input)"><strong>FSCTL_OFFLOAD_READ_INPUT</strong></a>中的一个或多个成员不正确：</p>
<strong>FileOffset</strong> 不是卷的逻辑扇区大小的倍数。
<strong>CopyLength</strong> 不是卷的逻辑扇区大小的倍数。
<strong>大小</strong> 不是 <a href="/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsctl_offload_read_input" data-raw-source="[&lt;strong&gt;FSCTL_OFFLOAD_READ_INPUT&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsctl_offload_read_input)"><strong>FSCTL_OFFLOAD_READ_INPUT</strong></a> 结构的大小。
<strong>FileOffset</strong> + <strong>CopyLength</strong> &gt; <strong>MAXULONGLONG</strong>。</td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_VOLUME_DISMOUNTED</strong></p></td>
<td align="left"><p>文件系统卷已卸除。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_NOT_SUPPORTED</strong></p></td>
<td align="left"><p>此卷上不支持卸载读取操作。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_OFFLOAD_READ_FILE_NOT_SUPPORTED</strong></p></td>
<td align="left"><p>请求的文件类型不受支持。 以下文件类型不支持卸载操作：</p>
<ul>
<li>事务性文件 (TxF) </li>
<li>非用户文件</li>
<li>压缩文件</li>
<li>加密文件</li>
<li>稀疏文件</li>
<li>NTFS 元数据文件</li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_FILE_DELETED</strong></p></td>
<td align="left"><p>此文件的数据流无效。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_FILE_CLOSED</strong></p></td>
<td align="left"><p>文件句柄已关闭。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_INVALID_HANDLE</strong></p></td>
<td align="left"><p>指定的文件句柄无效。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_FILE_LOCK_CONFLICT</strong></p></td>
<td align="left"><p>由于当前文件锁定状态，读取权限不足。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_END_OF_FILE</strong></p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsctl_offload_read_input" data-raw-source="[&lt;strong&gt;FSCTL_OFFLOAD_READ_INPUT&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsctl_offload_read_input)"><strong>FSCTL_OFFLOAD_READ_INPUT</strong></a>的<strong>FileOffset</strong>成员将在文件尾 (EOF) 开始后开始。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_DISMOUNTED_VOLUME</strong></p></td>
<td align="left"><p>卸载卷上不能发生卸载读取。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_INSUFFICIENT_RESOUCES</strong></p></td>
<td align="left"><p>资源不足，无法完成请求。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_BUFFER_TOO_SMALL</strong></p></td>
<td align="left"><p><em>OutputBufferLength</em> 太小， <em>OutputBuffer</em> 无法接收 <a href="/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsctl_offload_read_output" data-raw-source="[&lt;strong&gt;FSCTL_OFFLOAD_READ_OUTPUT&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsctl_offload_read_output)"><strong>FSCTL_OFFLOAD_READ_OUTPUT</strong></a> 结构。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

卸载读取仅适用于普通文件。 有关不支持的文件类型的列表，请参阅 **状态 \_ 卸载 \_ 读取 \_ 文件 \_ \_ ** 的描述。

读取的开始可能超出有效数据长度 (VDL) ，但不能超过 EOF。

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
<td align="left"><p>从 Windows 8 开始可用。</p></td>
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

[**FSCTL \_ 卸载 \_ 读取 \_ 输入**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsctl_offload_read_input)

[**FSCTL \_ 卸载 \_ 读取 \_ 输出**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsctl_offload_read_output)

