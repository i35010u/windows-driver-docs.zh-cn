---
title: MRxLowIOSubmit\ LOWIO\_OP\_READ\ routine
description: MRxLowIOSubmit\ LOWIO\_OP\_RDBSS 网络微型重定向到发出读取的请求通过调用读例程。
ms.assetid: 26a173d8-e3ab-4c63-8390-133afd35b51a
keywords:
- MRxLowIOSubmit LOWIO_OP_READ 例程可安装文件系统驱动程序
- PMRX_CALLDOWN
topic_type:
- apiref
api_name:
- MRxLowIOSubmit LOWIO_OP_READ
api_location:
- mrx.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1e825f72cec4c1a82ea493e236cd423ed431c87
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541547"
---
# <a name="mrxlowiosubmitlowioopread-routine"></a>MRxLowIOSubmit\[LOWIO\_OP\_读取\]例程


*MRxLowIOSubmit\[LOWIO\_OP\_读取\]* 调用例程[RDBSS](https://msdn.microsoft.com/library/windows/hardware/ff556810)网络微型重定向到发出读取的请求。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxLowIOSubmit[LOWIO_OP_READ];

NTSTATUS MRxLowIOSubmit[LOWIO_OP_READ](
  _Inout_ PRX_CONTEXT RxContext
)
{ ... }
```

<a name="parameters"></a>参数
----------

*RxContext* \[in、 out\]  
指向 RX\_上下文结构。 此参数包含 IRP 请求该操作。

<a name="return-value"></a>返回值
------------

*MRxLowIOSubmit\[LOWIO\_OP\_读取\]* 返回状态\_成功的成功或相应 NTSTATUS 值，如以下项之一：

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
<td align="left"><p>FCB 结构被获得，但已关闭关联的 SRV_OPEN 结构。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_INSUFFICIENT_RESOURCES</strong></td>
<td align="left"><p>没有资源不足，无法完成请求。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_INVALID_DEVICE_REQUEST</strong></td>
<td align="left"><p>指定了无效的设备请求。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_INVALID_PARAMETER</strong></td>
<td align="left"><p>在指定的参数无效<em>RxContext</em>。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_NOT_IMPLEMENTED</strong></td>
<td align="left"><p>未实现此例程。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_NOT_SUPPORTED</strong></td>
<td align="left"><p>指定的请求不受网络微型重定向。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

RDBSS 调用*MRxLowIOSubmit\[LOWIO\_OP\_读取\]* 接收响应[ **IRP\_MJ\_读取** ](irp-mj-read.md)请求。

然后再调用*MRxLowIOSubmit\[LOWIO\_OP\_读取\]*，RDBSS 修改 RX 中的以下成员\_上下文结构指向*RxContext*参数：

**LowIoContext.Operation**成员设置为 LOWIO\_OP\_读取。

**LowIoContext.ResourceThreadId**成员设置为启动 RDBSS 中的操作的进程线程。

**LowIoContext.ParamsFor.ReadWrite.Key**成员设置为值**IrpSp-&gt;Parameters.Read.Key**。

**ParamsFor.ReadWrite.Flags**成员具有 LOWIO\_READWRITEFLAG\_分页\_则设置 IO 位**Irp-&gt;标志**具有 IRP\_分页\_位上的 IO。

**ParamsFor.ReadWrite.Buffer**成员设置为用户缓冲区为 IoReadAccess 锁定了。

**LowIoContext.ParamsFor.ReadWrite.ByteCount**成员设置为值为 IrpSp-&gt;Parameters.Read.Length。

读取的请求通常由实现网络微型重定向作为异步操作因为它可能需要相当长的时间。 该操作通常组成的网络请求发送到远程服务器。 在服务器上完成读取的请求时获得响应。 这是操作的网络微型重定向可能需要为其注册用于处理取消启动的本地上下文的示例。

虽然*MRxLowIOSubmit\[LOWIO\_OP\_读取\]* 处理例程， **LowIoContext.ResourceThreadId** RX的成员\_保证上下文以指示启动了 RDBSS 中的操作的进程线程。 **LowIoContext.ResourceThreadId**成员可用于释放 FCB 结构代表另一个线程。 完成异步例程后，可以释放已获取从初始线程的 FCB 结构。 FCB 结构可以释放通过调用[ **RxReleaseFcbResourceForThreadInMRx**](https://msdn.microsoft.com/library/windows/hardware/ff554694)。

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
<td align="left"><p>标头</p></td>
<td align="left">Mrx.h （包括 Mrx.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**MRxLowIOSubmit\[LOWIO\_OP\_EXCLUSIVELOCK\]**](mrxlowiosubmit-lowio-op-exclusivelock-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_FSCTL\]**](mrxlowiosubmit-lowio-op-fsctl-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_IOCTL\]**](mrxlowiosubmit-lowio-op-ioctl-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_NOTIFY\_CHANGE\_DIRECTORY\]**](mrxlowiosubmit-lowio-op-notify-change-directory-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_SHAREDLOCK\]**](mrxlowiosubmit-lowio-op-sharedlock-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_UNLOCK\]**](mrxlowiosubmit-lowio-op-unlock-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_UNLOCK\_MULTIPLE\]**](mrxlowiosubmit-lowio-op-unlock-multiple-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_WRITE\]**](mrxlowiosubmit-lowio-op-write-.md)

[**RxReleaseFcbResourceForThreadInMRx**](https://msdn.microsoft.com/library/windows/hardware/ff554694)

 

 






