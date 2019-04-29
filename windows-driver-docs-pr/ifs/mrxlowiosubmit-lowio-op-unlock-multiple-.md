---
title: MRxLowIOSubmit\ LOWIO\_OP\_解锁\_多例程
description: MRxLowIOSubmit\ LOWIO\_OP\_解锁\_多例程调用通过 RDBSS 请求网络微型重定向删除多个文件对象持有的锁。
ms.assetid: 50f7abdf-a3f7-4625-ac54-75e80807d05e
keywords:
- MRxLowIOSubmit LOWIO_OP_UNLOCK_MULTIPLE 例程可安装文件系统驱动程序
- PMRX_CALLDOWN
topic_type:
- apiref
api_name:
- MRxLowIOSubmit LOWIO_OP_UNLOCK_MULTIPLE
api_location:
- mrx.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 085d3c72ab7fab2eb651a586030431bd363ed202
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324447"
---
# <a name="mrxlowiosubmitlowioopunlockmultiple-routine"></a>MRxLowIOSubmit\[LOWIO\_OP\_解锁\_多个\]例程


*MRxLowIOSubmit\[LOWIO\_OP\_解锁\_多个\]* 调用例程[RDBSS](https://msdn.microsoft.com/library/windows/hardware/ff556810)请求的网络最小重定向程序中删除多个文件对象持有的锁。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxLowIOSubmit[LOWIO_OP_UNLOCK_MULTIPLE];

NTSTATUS MRxLowIOSubmit[LOWIO_OP_UNLOCK_MULTIPLE](
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

*MRxLowIOSubmit\[LOWIO\_OP\_解锁\_多个\]* 将返回状态\_成功的成功或相应 NTSTATUS 值，如以下项之一：

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

RDBSS 调用*MRxLowIOSubmit\[LOWIO\_OP\_解锁\_多个\]* 接收响应[ **IRP\_MJ\_锁\_控件**](irp-mj-lock-control.md) IRP 的细微的代码请求\_MN\_解锁\_所有或 IRP\_MN\_解锁\_所有\_BY\_密钥。

然后再调用*MRxLowIOSubmit\[LOWIO\_OP\_解锁\_多个\]*，RDBSS 修改 RX 中的以下成员\_上下文结构指向*RxContext*参数：

**LowIoContext.Operation**成员设置为 LOWIO\_OP\_解锁\_多个。

**LowIoContext.ResourceThreadId**成员设置为启动 RDBSS 中的操作的进程线程。

**LowIoContext.ParamsFor.Locks.LockList**成员设置为一系列 LOWIO\_锁\_列表元素。 每个元素指定要将其解锁的范围。

中指定的字节范围，以便能够解锁**LowIoContext.ParamsFor.Locks.LockList** RX 成员\_上下文结构。 LOWIO\_锁\_列表结构如下所示：

``` syntax
typedef struct _LOWIO_LOCK_LIST {
  struct  _LOWIO_LOCK_LIST  *Next;
  ULONG  LockNumber;
  RXVBO  ByteOffset;
  LONGLONG  Length;
  ULONG  Key;
  BOOLEAN  ExclusiveLock;
} LOWIO_LOCK_LIST, *PLOWIO_LOCK_LIST;
```

**LowIoContext.Operation** RX 成员\_上下文指定要执行的较低的 I/O 操作。 可以为多个较低的 I/O 例程，使其指向网络微型重定向中的相同例程，因为**LowIoContext.Operation**成员可用于区分低请求的 I/O 操作。 例如，与文件锁相关的所有 I/O 调用可以在网络微型-重定向程序中都调用相同的低 I/O 例程，可以使用此例程**LowIoContext.Operation**成员区分锁定和解锁请求的操作。

如果*MRxLowIOSubmit\[LOWIO\_OP\_解锁\_多个\]* 例程可能需要很长时间才能完成，网络微型重定向程序驱动程序应释放FCB 之前启动的网络通信的结构。 FCB 结构可以释放通过调用[ **RxReleaseFcbResourceForThreadInMRx**](https://msdn.microsoft.com/library/windows/hardware/ff554694)。 虽然*MRxLowIOSubmit\[LOWIO\_OP\_解锁\_多个\]* 处理例程， **LowIoContext.ResourceThreadId** RX 成员\_上下文保证以指示启动了 RDBSS 中的操作的进程线程。

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


[**MRxLowIOSubmit\[LOWIO\_OP\_EXCLUSIVELOCK\]**](mrxlowiosubmit-lowio-op-exclusivelock-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_FSCTL\]**](mrxlowiosubmit-lowio-op-fsctl-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_IOCTL\]**](mrxlowiosubmit-lowio-op-ioctl-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_NOTIFY\_CHANGE\_DIRECTORY\]**](mrxlowiosubmit-lowio-op-notify-change-directory-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_READ\]**](mrxlowiosubmit-lowio-op-read-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_SHAREDLOCK\]**](mrxlowiosubmit-lowio-op-sharedlock-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_UNLOCK\]**](mrxlowiosubmit-lowio-op-unlock-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_WRITE\]**](mrxlowiosubmit-lowio-op-write-.md)

[**RxReleaseFcbResourceForThreadInMRx**](https://msdn.microsoft.com/library/windows/hardware/ff554694)

 

 






