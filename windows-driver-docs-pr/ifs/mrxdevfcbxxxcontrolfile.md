---
title: MRxDevFcbXXXControlFile 例程
description: MRxDevFcbXXXControlFile 例程由 RDBSS 调用，以将设备 FCB 控制请求（IOCTL 或 FSCTL 请求）传递到网络小型重定向程序。
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
ms.openlocfilehash: d2085a7720f06477f14a9dc73edc8c65064fb1a8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841113"
---
# <a name="mrxdevfcbxxxcontrolfile-routine"></a>MRxDevFcbXXXControlFile 例程


*MRxDevFcbXXXControlFile*例程由[RDBSS](https://docs.microsoft.com/windows-hardware/drivers/ifs/the-rdbss-driver-and-library)调用，以将设备 FCB 控制请求（IOCTL 或 FSCTL 请求）传递到网络小型重定向程序。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxDevFcbXXXControlFile;

NTSTATUS MRxDevFcbXXXControlFile(
  _Inout_ PRX_CONTEXT RxContext
)
{ ... }
```

<a name="parameters"></a>参数
----------

*RxContext* \[in，out\]  
指向 RX\_上下文结构的指针。 此参数包含请求操作的 IRP。

<a name="return-value"></a>返回值
------------

*MRxDevFcbXXXControlFile*返回成功的状态\_成功或使用适当的 NTSTATUS 值，如以下之一：

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

*MRxDevFcbXXXControlFile*处理与发送到网络小型重定向程序的设备 FCB 相关的 IOCTL 和 FSCTL 请求。

在调用*MRxDevFcbXXXControlFile*之前，RDBSS 会修改 RX\_由*RxContext*参数指向的上下文结构中的以下成员：

**MajorFunction**设置为 IRP 的主要功能

如果这是 IRP\_MJ\_文件\_系统\_控制请求，则 RDBSS 会在\_RX 中修改*RxContext*参数指向的以下成员：

**LowIoContext ParamsFor. FsCtl. MinorFunction**设置为 FsCtl 代码的次要函数代码

**LowIoContext. ParamsFor. FsCtl. FsControlCode**设置为 IRP 的 FsCtl 代码

如果这是 IRP\_MJ\_设备\_控制或 IRP\_MJ\_内部\_设备\_控制请求，则 RDBSS 会修改 RxContext 指向的 RX\_上下文结构中的以下成员。参数：

**LowIoContext. ParamsFor. FsCtl. FsControlCode**设置为 IRP 的控制代码。

如果*MRxDevFcbXXXControlFile*返回 STATUS\_SUCCESS，则例程成功。 任何其他返回值都指示发生了错误。

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
<td align="left">桌面</td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Mrx （包括 Mrx）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**MRxStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_calldown_ctx)

[**MRxStop**](mrxstop.md)

 

 






