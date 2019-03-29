---
title: MRxLowIOSubmit\ LOWIO\_OP\_EXCLUSIVELOCK\ 例程
description: MRxLowIOSubmit\ LOWIO\_OP\_EXCLUSIVELOCK\ 例程调用通过 RDBSS 请求网络微型重定向，打开文件对象的排他锁。
ms.assetid: 7f6613d1-63fb-4505-966d-155dc2b80ffe
keywords:
- MRxLowIOSubmit LOWIO_OP_EXCLUSIVELOCK 例程可安装文件系统驱动程序
- PMRX_CALLDOWN
topic_type:
- apiref
api_name:
- MRxLowIOSubmit LOWIO_OP_EXCLUSIVELOCK
api_location:
- mrx.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d10dd35f5d52ba77677d486f1783546671f4515
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564675"
---
# <a name="mrxlowiosubmitlowioopexclusivelock-routine"></a>MRxLowIOSubmit\[LOWIO\_OP\_EXCLUSIVELOCK\] routine


*MRxLowIOSubmit\[LOWIO\_OP\_EXCLUSIVELOCK\]* 调用例程[RDBSS](https://msdn.microsoft.com/library/windows/hardware/ff556810)以请求微型重定向程序打开的网络文件对象的排他锁。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxLowIOSubmit[LOWIO_OP_EXCLUSIVELOCK];

NTSTATUS MRxLowIOSubmit[LOWIO_OP_EXCLUSIVELOCK](
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

*MRxLowIOSubmit\[LOWIO\_OP\_EXCLUSIVELOCK\]* 返回状态\_成功的成功或相应 NTSTATUS 值，如以下项之一：

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
<td align="left"><p>没有资源不足，无法完成请求。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_INVALID_NETWORK_RESPONSE</strong></td>
<td align="left"><p>从远程服务器收到了无效的响应。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_INVALID_PARAMETER</strong></td>
<td align="left"><p>在指定的参数无效<em>RxContext</em>。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_LINK_FAILED</strong></td>
<td align="left"><p>尝试重新连接到远程服务器来完成该请求失败。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_NOT_IMPLEMENTED</strong></td>
<td align="left"><p>未实现此例程。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_SHARING_VIOLATION</strong></td>
<td align="left"><p>发生共享冲突。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_UNSUCCESSFUL</strong></td>
<td align="left"><p>在调用不成功。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

RDBSS 调用*MRxLowIOSubmit\[LOWIO\_OP\_EXCLUSIVELOCK\]* 接收响应[ **IRP\_MJ\_锁\_控制**](irp-mj-lock-control.md) IRP 的细微的代码请求\_MN\_锁定**IrpSp-&gt;标志**具有 SL\_独占\_锁位集。

然后再调用*MRxLowIOSubmit\[LOWIO\_OP\_EXCLUSIVELOCK\]*，RDBSS 修改 RX 中的以下成员\_指向上下文结构*RxContext*参数：

**LowIoContext.Operation**成员设置为 LOWIO\_OP\_EXCLUSIVELOCK。

**LowIoContext.ResourceThreadId**成员设置为启动 RDBSS 中的操作的进程线程。

**LowIoContext.ParamsFor.Locks.ByteOffset**成员设置为值**IrpSp-&gt;Parameters.LockControl.ByteOffset.QuadPart**。

**LowIoContext.ParamsFor.Locks.Key**成员设置为值**IrpSp-&gt;Parameters.LockControl.Key**。

**LowIoContext.ParamsFor.Locks.Flags**成员设置为值**IrpSp-&gt;标志**。

**LowIoContext.ParamsFor.Locks.Length**成员设置为值**IrpSp-&gt;Parameters.LockControl.Length.QuadPart**。

**LowIoContext.Operation** RX 成员\_上下文结构指定要执行的较低的 I/O 操作。 可以为多个较低的 I/O 例程，使其指向网络微型重定向中的相同例程，因为这**LowIoContext.Operation**成员可用于区分低请求的 I/O 操作。 例如，与文件锁相关的所有 I/O 调用可以在网络微型-重定向程序中都调用相同的低 I/O 例程，该例程可以使用**LowIoContext.Operation**成员区分锁定和解锁请求的操作。

如果*MRxLowIOSubmit\[LOWIO\_OP\_EXCLUSIVELOCK\]* 例程可能需要很长时间才能完成，网络微型重定向程序驱动程序应释放之前的 FCB 结构启动网络通信。 FCB 结构可以释放通过调用[ **RxReleaseFcbResourceForThreadInMRx**](https://msdn.microsoft.com/library/windows/hardware/ff554694)。 虽然*MRxLowIOSubmit\[LOWIO\_OP\_EXCLUSIVELOCK\]* 处理例程， **LowIoContext.ResourceThreadId** RX 的成员\_上下文保证以指示启动了 RDBSS 中的操作的进程线程。

**LowIoContext.ResourceThreadId** RX 成员\_上下文可用于释放 FCB 结构代表另一个线程。 完成异步例程后，可以释放已获取从初始线程的 FCB 结构。

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


[**MRxLowIOSubmit\[LOWIO\_OP\_FSCTL\]**](mrxlowiosubmit-lowio-op-fsctl-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_IOCTL\]**](mrxlowiosubmit-lowio-op-ioctl-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_NOTIFY\_CHANGE\_DIRECTORY\]**](mrxlowiosubmit-lowio-op-notify-change-directory-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_READ\]**](mrxlowiosubmit-lowio-op-read-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_SHAREDLOCK\]**](mrxlowiosubmit-lowio-op-sharedlock-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_UNLOCK\]**](mrxlowiosubmit-lowio-op-unlock-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_UNLOCK\_MULTIPLE\]**](mrxlowiosubmit-lowio-op-unlock-multiple-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_WRITE\]**](mrxlowiosubmit-lowio-op-write-.md)

[**RxReleaseFcbResourceForThreadInMRx**](https://msdn.microsoft.com/library/windows/hardware/ff554694)

 

 






