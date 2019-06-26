---
title: MRxDevFcbXXXControlFile routine
description: MRxDevFcbXXXControlFile 例程调用 RDBSS 将传递给网络微型重定向的设备 FCB 控件请求 （IOCTL 或 FSCTL 请求）。
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
ms.openlocfilehash: 471f315bfdfdf1d4e9db4b29da31e13377a9175e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355536"
---
# <a name="mrxdevfcbxxxcontrolfile-routine"></a>MRxDevFcbXXXControlFile routine


*MRxDevFcbXXXControlFile*由调用例程[RDBSS](https://docs.microsoft.com/windows-hardware/drivers/ifs/the-rdbss-driver-and-library)将传递给网络微型重定向的设备 FCB 控件请求 （IOCTL 或 FSCTL 请求）。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxDevFcbXXXControlFile;

NTSTATUS MRxDevFcbXXXControlFile(
  _Inout_ PRX_CONTEXT RxContext
)
{ ... }
```

<a name="parameters"></a>Parameters
----------

*RxContext* \[in、 out\]  
指向 RX\_上下文结构。 此参数包含 IRP 请求该操作。

<a name="return-value"></a>返回值
------------

*MRxDevFcbXXXControlFile*将返回状态\_成功的成功或相应 NTSTATUS 值，如以下项之一：

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
<td align="left"><p>已请求停止或启动网络微型重定向，但调用方不具备适当的安全，此操作。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_INVALID_DEVICE_REQUEST</strong></td>
<td align="left"><p>无效的设备请求发送到网络微型重定向。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_REDIRECTOR_HAS_OPEN_HANDLES</strong></td>
<td align="left"><p>这是请求以停止网络最小化重定向程序，但重定向程序已打开的句柄会阻止这一次停止的。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_REDIRECTOR_NOT_STARTED</strong></td>
<td align="left"><p>这是请求以停止网络最小化重定向程序，但未启动重定向程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_REDIRECTOR_STARTED</strong></td>
<td align="left"><p>这是请求启动网络最小化重定向程序，但已启动重定向程序。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

*MRxDevFcbXXXControlFile*处理 IOCTL 和 FSCTL 发送到网络微型重定向的请求与设备 FCB 相关。

然后再调用*MRxDevFcbXXXControlFile*，RDBSS 修改 RX 中的以下成员\_指向上下文结构*RxContext*参数：

**MajorFunction**将设置为 IRP 主要函数

如果这是 IRP\_MJ\_文件\_系统\_控制请求，然后 RDBSS 修改 RX 中的以下成员\_指向上下文结构*RxContext*参数：

**LowIoContext.ParamsFor.FsCtl.MinorFunction**设置为 FSCTL 代码的小函数代码

**LowIoContext.ParamsFor.FsCtl.FsControlCode**设 IRP FSCTL 代码

如果这是 IRP\_MJ\_设备\_控件或 IRP\_MJ\_内部\_设备\_控制请求，然后 RDBSS 修改 RX中的以下成员\_指向上下文结构*RxContext*参数：

**LowIoContext.ParamsFor.FsCtl.FsControlCode**设 IRP 的控制代码。

如果*MRxDevFcbXXXControlFile*将返回状态\_成功，则例程是否成功。 任何其他返回值指示发生了错误。

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
<td align="left">桌面设备</td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Mrx.h （包括 Mrx.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**MRxStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_calldown_ctx)

[**MRxStop**](mrxstop.md)

 

 






