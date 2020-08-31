---
title: MRxLowIOSubmit \ LOWIO \_ OP \_ NOTIFY \_ CHANGE \_ DIRECTORY \ 例程
description: RDBSS 调用 MRxLowIOSubmit \ \_ LOWIO \_ OP \_ \_ notification CHANGE DIRECTORY \ 例程向网络小型重定向程序发出请求，以执行目录更改通知操作。
ms.assetid: a3ac7936-7c46-4e46-929a-dc495187a01b
keywords:
- MRxLowIOSubmit LOWIO_OP_NOTIFY_CHANGE_DIRECTORY 日常可安装文件系统驱动程序
- PMRX_CALLDOWN
topic_type:
- apiref
api_name:
- MRxLowIOSubmit LOWIO_OP_NOTIFY_CHANGE_DIRECTORY
api_location:
- mrx.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e3620f320ceddef9ec4c187231ff843329d9442
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063308"
---
# <a name="mrxlowiosubmitlowio_op_notify_change_directory-routine"></a>MRxLowIOSubmit \[ LOWIO \_ OP \_ 通知 \_ 更改 \_ 目录 \] 例程


[RDBSS](./the-rdbss-driver-and-library.md)调用*MRxLowIOSubmit \[ LOWIO \_ OP notification \_ \_ CHANGE \_ DIRECTORY \] *例程向网络小型重定向程序发出请求，以执行目录更改通知操作。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxLowIOSubmit[LOWIO_OP_NOTIFY_CHANGE_DIRECTORY];

NTSTATUS MRxLowIOSubmit[LOWIO_OP_NOTIFY_CHANGE_DIRECTORY](
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

*MRxLowIOSubmit \[LOWIO \_ OP \_ NOTIFY \_ CHANGE \_ DIRECTORY \] 将*成功返回状态 \_ 成功或使用适当的 NTSTATUS 值，如以下之一：

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

RDBSS 调用*MRxLowIOSubmit \[ LOWIO \_ OP \_ 通知 \_ 更改 \_ 目录 \] *以接收[**IRP \_ MJ \_ 目录 \_ 控制**](irp-mj-directory-control.md)请求。

在调用*MRxLowIOSubmit \[ LOWIO \_ OP \_ 通知 \_ 更改 \_ 目录 \] *之前，RDBSS 会修改 \_ *RxContext*参数指向的 RX 上下文结构中的以下成员：

**LowIoContext**成员设置为 LOWIO \_ OP \_ NOTIFY \_ CHANGE \_ DIRECTORY。

**LowIoContext. ResourceThreadId**成员设置为在 RDBSS 中启动操作的进程线程。

如果**IrpSp &gt; 标记**具有 SL **TRUE**监视树位集，则**LowIoContext. NotifyChangeDirectory. WatchTree**成员设置为 TRUE。 \_ \_

**LowIoContext. ParamsFor. NotifyChangeDirectory. CompletionFilter**成员设置为 IrpSp. NotifyDirectory 的值** &gt; **。

**LowIoContext. ParamsFor. NotifyChangeDirectory. NotificationBufferLength**成员设置为**IrpSp- &gt; NotifyDirectory**的值。

**LowIoContext. ParamsFor. NotifyChangeDirectory. pNotificationBuffer**成员设置为通过调用**和 MmGetSystemAddressForMdlSafe 传入 &gt; **的**MdlAddress**返回的值。 还会探测并锁定用户缓冲区以进行写访问。

目录更改通知操作通常由网络小型重定向程序作为异步操作来实现，因为这可能需要相当长的时间。 此操作通常包含向远程服务器发送请求更改通知的网络请求。 当所需的更改在服务器上受到影响时，将获取响应。 这是一个操作示例，网络小型重定向程序可能需要为此操作注册一个唯一的上下文值，以便处理本地启动的取消。

当*MRxLowIOSubmit \[ LOWIO \_ OP \_ 通知 \_ 更改 \_ 目录 \] *例程正在处理时，将保证 RX 上下文的**LowIoContext**成员 \_ 指示在 RDBSS 中启动操作的进程线程。 **LowIoContext. ResourceThreadId**成员可用于代表其他线程发布 FCB 结构。 异步例程完成后，可以释放从初始线程获取的 FCB 结构。 可以通过调用 [**RxReleaseFcbResourceForThreadInMRx**](/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxreleasefcbresourceforthreadinmrx)来释放 FCB 结构。

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

## <a name="see-also"></a>请参阅


[**MRxLowIOSubmit \[ LOWIO \_ OP \_ EXCLUSIVELOCK\]**](mrxlowiosubmit-lowio-op-exclusivelock-.md)

[**MRxLowIOSubmit \[ LOWIO \_ OP \_ FSCTL\]**](mrxlowiosubmit-lowio-op-fsctl-.md)

[**MRxLowIOSubmit \[ LOWIO \_ OP \_ IOCTL\]**](mrxlowiosubmit-lowio-op-ioctl-.md)

[**MRxLowIOSubmit \[ LOWIO \_ OP \_ READ\]**](mrxlowiosubmit-lowio-op-read-.md)

[**MRxLowIOSubmit \[ LOWIO \_ OP \_ SHAREDLOCK\]**](mrxlowiosubmit-lowio-op-sharedlock-.md)

[**MRxLowIOSubmit \[ LOWIO \_ OP \_\]**](mrxlowiosubmit-lowio-op-unlock-.md)

[**MRxLowIOSubmit \[ LOWIO \_ OP \_ UNLOCK \_ 多个\]**](mrxlowiosubmit-lowio-op-unlock-multiple-.md)

[**MRxLowIOSubmit \[ LOWIO \_ OP \_ WRITE\]**](mrxlowiosubmit-lowio-op-write-.md)

[**RxReleaseFcbResourceForThreadInMRx**](/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxreleasefcbresourceforthreadinmrx)

 

