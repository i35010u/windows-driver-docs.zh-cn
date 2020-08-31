---
title: MRxDevFcbXXXControlFile 例程
description: RDBSS 调用 MRxDevFcbXXXControlFile 例程，以将 (IOCTL 或 FSCTL 请求) 的设备 FCB 控制请求传递到网络小型重定向程序。
ms.assetid: d60449d0-17d0-4303-8d0d-cba091de2b07
keywords:
- MRxDevFcbXXXControlFile 例程可安装文件系统驱动程序
- PMRX_CALLDOWN
topic_type:
- apiref
api_name:
- MRxDevFcbXXXControlFile
api_location:
- mrx.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a36340a1d25bee142674dd3ab897a6dbf81bfd45
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063028"
---
# <a name="mrxdevfcbxxxcontrolfile-routine"></a>MRxDevFcbXXXControlFile 例程


[RDBSS](./the-rdbss-driver-and-library.md)调用*MRxDevFcbXXXControlFile*例程，以将 (IOCTL 或 FSCTL 请求) 的设备 FCB 控制请求传递到网络小型重定向程序。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxDevFcbXXXControlFile;

NTSTATUS MRxDevFcbXXXControlFile(
  _Inout_ PRX_CONTEXT RxContext
)
{ ... }
```

<a name="parameters"></a>parameters
----------

*RxContext* \[in、out\]  
指向 RX \_ 上下文结构的指针。 此参数包含请求操作的 IRP。

<a name="return-value"></a>返回值
------------

*MRxDevFcbXXXControlFile* 返回成功的状态 \_ 成功或适当的 NTSTATUS 值，如以下之一：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">返回代码</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>STATUS_ACCESS_DENIED</strong></td>
<td align="left"><p>发出了停止或启动网络微型重定向程序的请求，但调用方缺乏此操作的正确安全性。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_INVALID_DEVICE_REQUEST</strong></td>
<td align="left"><p>向网络小型重定向程序发送了无效的设备请求。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_REDIRECTOR_HAS_OPEN_HANDLES</strong></td>
<td align="left"><p>这是一种停止网络小型重定向程序的请求，但重定向程序具有打开的句柄，阻止此时停止。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_REDIRECTOR_NOT_STARTED</strong></td>
<td align="left"><p>这是一个停止网络小型重定向程序的请求，但重定向程序未启动。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_REDIRECTOR_STARTED</strong></td>
<td align="left"><p>这是启动网络小型重定向程序的请求，但重定向程序已启动。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

*MRxDevFcbXXXControlFile* 处理与发送到网络小型重定向程序的设备 FCB 相关的 IOCTL 和 FSCTL 请求。

在调用 *MRxDevFcbXXXControlFile*之前，RDBSS 会修改 \_ *RXCONTEXT* 参数指向的 RX 上下文结构中的以下成员：

**MajorFunction** 设置为 IRP 的主要功能

如果这是 IRP \_ MJ \_ 文件 \_ 系统 \_ 控制请求，则 RDBSS 会修改 \_ *RxContext* 参数指向的 RX 上下文结构中的以下成员：

**LowIoContext ParamsFor. FsCtl. MinorFunction** 设置为 FsCtl 代码的次要函数代码

**LowIoContext. ParamsFor. FsCtl. FsControlCode** 设置为 IRP 的 FsCtl 代码

如果这是 IRP \_ mj \_ 设备 \_ 控制或 irp \_ mj \_ 内部 \_ 设备 \_ 控制请求，则 RDBSS 会修改 \_ *RxContext* 参数指向的 RX 上下文结构中的以下成员：

**LowIoContext. ParamsFor. FsCtl. FsControlCode** 设置为 IRP 的控制代码。

如果 *MRxDevFcbXXXControlFile* 返回状态 \_ SUCCESS，则例程成功。 任何其他返回值都指示发生了错误。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>目标平台</p></td>
<td align="left">桌面型</td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Mrx (包含 Mrx) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**MRxStart**](/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_calldown_ctx)

[**MRxStop**](mrxstop.md)

 

