---
title: MRxLowIOSubmit \ LOWIO \_ OP \_ WRITE \ 例程
description: RDBSS 调用 MRxLowIOSubmit \ LOWIO \_ OP \_ write \ 例程向网络小型重定向程序发出写入请求。
ms.assetid: b70838e3-4e80-4ec9-88ba-0f608a1af78e
keywords:
- MRxLowIOSubmit LOWIO_OP_WRITE 日常可安装文件系统驱动程序
- PMRX_CALLDOWN
topic_type:
- apiref
api_name:
- MRxLowIOSubmit LOWIO_OP_WRITE
api_location:
- mrx.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff5a3c744ddd4a9745730ffa985dc801479fbf1f
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066142"
---
# <a name="mrxlowiosubmitlowio_op_write-routine"></a>MRxLowIOSubmit \[ LOWIO \_ OP \_ 写入 \] 例程


[RDBSS](./the-rdbss-driver-and-library.md)调用*MRxLowIOSubmit \[ LOWIO \_ OP \_ 写入 \] *例程向网络小型重定向程序发出写入请求。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxLowIOSubmit[LOWIO_OP_WRITE];

NTSTATUS MRxLowIOSubmit[LOWIO_OP_WRITE](
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

*MRxLowIOSubmit \[LOWIO \_ OP \_ WRITE \] *返回成功的状态 \_ 或相应的 NTSTATUS 值，如以下之一：

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
<td align="left"><strong>STATUS_FILE_CLOSED</strong></td>
<td align="left"><p>已获取 FCB 结构，但关联的 SRV_OPEN 结构已关闭。</p></td>
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
<td align="left"><strong>STATUS_INVALID_PARAMETER</strong></td>
<td align="left"><p>在 <em>RxContext</em>中指定了无效的参数。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_NOT_IMPLEMENTED</strong></td>
<td align="left"><p>未实现此例程。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_NOT_SUPPORTED</strong></td>
<td align="left"><p>网络小型重定向程序不支持指定的请求。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

RDBSS 调用*MRxLowIOSubmit \[ LOWIO \_ OP \_ write \] *来接收[**IRP \_ MJ \_ 写入**](irp-mj-write.md)请求。

在调用*MRxLowIOSubmit \[ LOWIO \_ OP \_ WRITE \] *之前，RDBSS 会修改 RxContext 参数所指向的 RX 上下文结构中的以下成员 \_ ： *RxContext*

**LowIoContext**成员设置为 LOWIO \_ OP \_ WRITE。

**LowIoContext. ResourceThreadId**成员设置为在 RDBSS 中启动操作的进程线程。

将 **LowIoContext** 成员设置为 **IrpSp- &gt; Parameters. Read. key**的值。

**ParamsFor.ReadWrite.Flags** \_ \_ \_ 如果**irp &gt; 标志**的 irp \_ 分页 \_ io 位为，则 ParamsFor 成员具有 LOWIO READWRITEFLAG 分页 io 位。

**ParamsFor**成员设置为锁定 IoWriteAccess 的用户缓冲区。

**ParamsFor. ByteCount**成员设置为 IrpSp 的值。 LowIoContext 的值。 ** &gt; **

写入请求通常由网络小型重定向程序作为异步操作来实现，因为这可能需要相当长的时间。 操作通常包含向远程服务器发送网络请求。 当在服务器上完成写入请求时，将获取响应。 这是一个操作示例，网络小型重定向程序可能需要为此操作注册上下文以处理本地启动的取消。

当*MRxLowIOSubmit \[ LOWIO \_ OP \_ 写入 \] *例程正在处理时，将保证 RX 上下文的**LowIoContext**成员 \_ 指示在 RDBSS 中启动操作的进程线程。 **LowIoContext. ResourceThreadId**成员可用于代表其他线程发布 FCB 结构。 异步例程完成后，可以释放从初始线程获取的 FCB 结构。 可以通过调用 [**RxReleaseFcbResourceForThreadInMRx**](/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxreleasefcbresourceforthreadinmrx)来释放 FCB 结构。

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

[**MRxLowIOSubmit \[ LOWIO \_ OP \_ IOCTL\]**](mrxlowiosubmit-lowio-op-ioctl-.md)

[**MRxLowIOSubmit \[ LOWIO \_ OP \_ 通知 \_ 更改 \_ 目录\]**](mrxlowiosubmit-lowio-op-notify-change-directory-.md)

[**MRxLowIOSubmit \[ LOWIO \_ OP \_ READ\]**](mrxlowiosubmit-lowio-op-read-.md)

[**MRxLowIOSubmit \[ LOWIO \_ OP \_ SHAREDLOCK\]**](mrxlowiosubmit-lowio-op-sharedlock-.md)

[**MRxLowIOSubmit \[ LOWIO \_ OP \_\]**](mrxlowiosubmit-lowio-op-unlock-.md)

[**MRxLowIOSubmit \[ LOWIO \_ OP \_ UNLOCK \_ 多个\]**](mrxlowiosubmit-lowio-op-unlock-multiple-.md)

[**RxReleaseFcbResourceForThreadInMRx**](/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxreleasefcbresourceforthreadinmrx)

 

