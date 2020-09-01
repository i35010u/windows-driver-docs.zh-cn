---
title: MRxLowIOSubmit \ LOWIO \_ OP \_ FSCTL \ 例程
description: RDBSS 调用 MRxLowIOSubmit \ LOWIO \_ OP \_ FSCTL \ 例程来请求网络小型重定向程序发出文件系统控制请求。
ms.assetid: 6bbb4b65-c447-47d8-9d05-f2adfb607099
keywords:
- MRxLowIOSubmit LOWIO_OP_FSCTL 日常可安装文件系统驱动程序
- PMRX_CALLDOWN
topic_type:
- apiref
api_name:
- MRxLowIOSubmit LOWIO_OP_FSCTL
api_location:
- mrx.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2413214d5ea941e34a9d4510320cd0b127071c2b
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066146"
---
# <a name="mrxlowiosubmitlowio_op_fsctl-routine"></a>MRxLowIOSubmit \[ LOWIO \_ OP \_ FSCTL \] 例程


[RDBSS](./the-rdbss-driver-and-library.md)调用*MRxLowIOSubmit \[ LOWIO \_ OP \_ FSCTL \] *例程来请求网络小型重定向程序发出文件系统控制请求远程文件。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxLowIOSubmit[LOWIO_OP_FSCTL];

NTSTATUS MRxLowIOSubmit[LOWIO_OP_FSCTL](
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

*MRxLowIOSubmit \[LOWIO \_ OP \_ FSCTL \] *将返回 \_ 成功的状态，或者返回相应的 NTSTATUS 值，如以下之一：

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
<td align="left"><strong>STATUS_CONNECTION_DISCONNECTED</strong></td>
<td align="left"><p>连接已断开连接。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_INSUFFICIENT_RESOURCES</strong></td>
<td align="left"><p>资源不足，无法完成请求。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_INVALID_DEVICE_REQUEST</strong></td>
<td align="left"><p>指定了无效的设备请求。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_INVALID_NETWORK_RESPONSE</strong></td>
<td align="left"><p>从远程服务器收到无效的响应。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_INVALID_PARAMETER</strong></td>
<td align="left"><p>在 <em>RxContext</em>中指定了无效的参数。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_LINK_FAILED</strong></td>
<td align="left"><p>尝试重新连接到远程服务器以完成请求失败。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_NOT_IMPLEMENTED</strong></td>
<td align="left"><p>未实现此例程。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_NOT_SUPPORTED</strong></td>
<td align="left"><p>网络小型重定向程序不支持指定的 FSCTL。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_UNSUCCESSFUL</strong></td>
<td align="left"><p>调用失败。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

RDBSS 调用*MRxLowIOSubmit \[ LOWIO \_ OP \_ FSCTL \] * ，以响应接收[**IRP \_ MJ \_ 文件 \_ 系统 \_ 控制**](irp-mj-file-system-control.md)请求。

在调用*MRxLowIOSubmit \[ LOWIO \_ OP \_ FSCTL \] *之前，RDBSS 会修改 RxContext 参数所指向的 RX 上下文结构中的以下成员 \_ ： *RxContext*

**LowIoContext**成员设置为 LOWIO \_ OP \_ FSCTL。

**LowIoContext. ResourceThreadId**成员设置为在 RDBSS 中启动操作的进程线程。

**LowIoContext. ParamsFor. FsCtl. FsControlCode**成员设置为 FsCtl 主要控制代码。

**LowIoContext. ParamsFor. FsCtl. MinorFunction**成员设置为 FsCtl 次要控制代码。

**LowIoContext. ParamsFor. FsCtl. pInputBuffer**成员设置为输入缓冲区。

**LowIoContext. ParamsFor. FsCtl. InputBufferLength**成员设置为输入缓冲区的长度。

**LowIoContext. ParamsFor. FsCtl. pOutputBuffer**成员设置为输出缓冲区。

**LowIoContext. ParamsFor. FsCtl. OutputBufferLength**成员设置为输出缓冲区的长度。

由网络小型重定向程序处理的文件系统控制代码 (FSCTL) 的请求可以分为以下几个类别之一：

-   RDBSS 和网络微型重定向程序实现和使用的 FSCTLs

-   仅由网络小型重定向程序实现和使用的 FSCTLs

-   网络小型重定向程序绝不会看到 FSCTLs。 这些 FSCTLs 仅用于调试辅助。

当*MRxLowIOSubmit \[ LOWIO \_ OP \_ FSCTL \] *例程正在处理时，可保证 RX 上下文的**LowIoContext. ResourceThreadId**成员 \_ 指示在 RDBSS 中启动操作的进程线程。 RX 上下文的 **LowIoContext. ResourceThreadId** 成员 \_ 可用于代表其他线程发布输入资源。 异步例程完成后，可以释放从初始线程获取的输入资源。

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

[**MRxLowIOSubmit \[ LOWIO \_ OP \_ IOCTL\]**](mrxlowiosubmit-lowio-op-ioctl-.md)

[**MRxLowIOSubmit \[ LOWIO \_ OP \_ 通知 \_ 更改 \_ 目录\]**](mrxlowiosubmit-lowio-op-notify-change-directory-.md)

[**MRxLowIOSubmit \[ LOWIO \_ OP \_ READ\]**](mrxlowiosubmit-lowio-op-read-.md)

[**MRxLowIOSubmit \[ LOWIO \_ OP \_ SHAREDLOCK\]**](mrxlowiosubmit-lowio-op-sharedlock-.md)

[**MRxLowIOSubmit \[ LOWIO \_ OP \_\]**](mrxlowiosubmit-lowio-op-unlock-.md)

[**MRxLowIOSubmit \[ LOWIO \_ OP \_ UNLOCK \_ 多个\]**](mrxlowiosubmit-lowio-op-unlock-multiple-.md)

[**MRxLowIOSubmit \[ LOWIO \_ OP \_ WRITE\]**](mrxlowiosubmit-lowio-op-write-.md)

 

