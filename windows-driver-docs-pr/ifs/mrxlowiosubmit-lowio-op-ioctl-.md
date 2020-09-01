---
title: MRxLowIOSubmit \ LOWIO \_ OP \_ IOCTL \ 例程
description: RDBSS 调用 MRxLowIOSubmit \ LOWIO \_ OP \_ IOCTL \ 例程向网络小型重定向程序发出 i/o 系统控制请求。
ms.assetid: b416e2b4-6024-45ec-adf5-90743d417ad5
keywords:
- MRxLowIOSubmit LOWIO_OP_IOCTL 日常可安装文件系统驱动程序
- PMRX_CALLDOWN
topic_type:
- apiref
api_name:
- MRxLowIOSubmit LOWIO_OP_IOCTL
api_location:
- mrx.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 684ba90cfff3e6f1af82ed58d5013527d79e5b01
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066140"
---
# <a name="mrxlowiosubmitlowio_op_ioctl-routine"></a>MRxLowIOSubmit \[ LOWIO \_ OP \_ IOCTL \] 例程


[RDBSS](./the-rdbss-driver-and-library.md)调用*MRxLowIOSubmit \[ LOWIO \_ OP \_ IOCTL \] *例程向网络小型重定向程序发出 i/o 系统控制请求。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxLowIOSubmit[LOWIO_OP_IOCTL];

NTSTATUS MRxLowIOSubmit[LOWIO_OP_IOCTL](
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

*MRxLowIOSubmit \[LOWIO \_ 操作 \_ IOCTL \] *返回成功的状态 \_ 或相应的 NTSTATUS 值，如以下之一：

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
<td align="left"><strong>STATUS_INSUFFICIENT_RESOURCES</strong></td>
<td align="left"><p>资源不足，无法完成请求。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_INVALID_DEVICE_REQUEST</strong></td>
<td align="left"><p>指定了无效的设备请求。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_INVALID_PARAMETER</strong></td>
<td align="left"><p>在 <em>RxContext</em>中指定了无效的参数。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_NOT_IMPLEMENTED</strong></td>
<td align="left"><p>未实现此例程。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_NOT_SUPPORTED</strong></td>
<td align="left"><p>网络小型重定向程序不支持指定的 IOCTL。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

RDBSS 调用*MRxLowIOSubmit \[ LOWIO \_ OP \_ IOCTL \] * ，以响应接收[**IRP \_ mj \_ 设备 \_ 控制**](irp-mj-device-control.md)或[**IRP \_ mj \_ 内部 \_ 设备 \_ 控制**](irp-mj-internal-device-control.md)请求。

在调用*MRxLowIOSubmit \[ LOWIO \_ OP \_ IOCTL \] *之前，RDBSS 会修改 RxContext 参数所指向的 RX 上下文结构中的以下成员 \_ ： *RxContext*

**LowIoContext**成员设置为 LOWIO \_ OP \_ IOCTL。

**LowIoContext. ResourceThreadId**成员设置为在 RDBSS 中启动操作的进程线程。

IoControlCode 成员设置为 IOCTL 控制代码。 **LowIoContext**

**ParamsFor pInputBuffer**成员设置为输入缓冲区。 LowIoContext

**LowIoContext**成员设置为输入缓冲区的长度。

**ParamsFor pOutputBuffer**成员设置为输出缓冲区。 LowIoContext

**LowIoContext**成员设置为输出缓冲区的长度。

在*MRxLowIOSubmit \[ LOWIO \_ OP \_ IOCTL \] *例程正在处理时，可保证 RX 上下文的**LowIoContext**成员 \_ 指示在 RDBSS 中启动操作的进程线程。 RX 上下文的 **LowIoContext. ResourceThreadId** 成员 \_ 可用于代表其他线程发布输入资源。 异步例程完成后，可以释放从初始线程获取的输入资源。

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


[**MRxLowIOSubmit \[ LOWIO \_ OP \_ EXCLUSIVELOCK\]**](mrxlowiosubmit-lowio-op-exclusivelock-.md)

[**MRxLowIOSubmit \[ LOWIO \_ OP \_ FSCTL\]**](mrxlowiosubmit-lowio-op-fsctl-.md)

[**MRxLowIOSubmit \[ LOWIO \_ OP \_ 通知 \_ 更改 \_ 目录\]**](mrxlowiosubmit-lowio-op-notify-change-directory-.md)

[**MRxLowIOSubmit \[ LOWIO \_ OP \_ READ\]**](mrxlowiosubmit-lowio-op-read-.md)

[**MRxLowIOSubmit \[ LOWIO \_ OP \_ SHAREDLOCK\]**](mrxlowiosubmit-lowio-op-sharedlock-.md)

[**MRxLowIOSubmit \[ LOWIO \_ OP \_\]**](mrxlowiosubmit-lowio-op-unlock-.md)

[**MRxLowIOSubmit \[ LOWIO \_ OP \_ UNLOCK \_ 多个\]**](mrxlowiosubmit-lowio-op-unlock-multiple-.md)

[**MRxLowIOSubmit \[ LOWIO \_ OP \_ WRITE\]**](mrxlowiosubmit-lowio-op-write-.md)

 

