---
title: MRxLowIOSubmit\ LOWIO\_OP\_通知\_更改\_目录 \&gt 例程
description: MRxLowIOSubmit\ LOWIO\_OP\_通知\_更改\_目录 \&gt 例程调用通过 RDBSS 网络微型重定向目录更改通知操作向发出请求。
ms.assetid: a3ac7936-7c46-4e46-929a-dc495187a01b
keywords:
- MRxLowIOSubmit LOWIO_OP_NOTIFY_CHANGE_DIRECTORY 例程可安装文件系统驱动程序
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
ms.openlocfilehash: b70fbc346cf6039e070973e4c4c82c3c3e9e5338
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357539"
---
# <a name="mrxlowiosubmitlowioopnotifychangedirectory-routine"></a>MRxLowIOSubmit\[LOWIO\_OP\_通知\_更改\_DIRECTORY\]例程


*MRxLowIOSubmit\[LOWIO\_OP\_通知\_更改\_目录\]* 调用例程[RDBSS](https://msdn.microsoft.com/library/windows/hardware/ff556810)到向网络微型重定向目录更改通知操作发出请求。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxLowIOSubmit[LOWIO_OP_NOTIFY_CHANGE_DIRECTORY];

NTSTATUS MRxLowIOSubmit[LOWIO_OP_NOTIFY_CHANGE_DIRECTORY](
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

*MRxLowIOSubmit\[LOWIO\_OP\_通知\_更改\_DIRECTORY\]* 返回状态\_成功的成功或适当的 NTSTATUS 值，此类为以下值之一：

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

RDBSS 调用*MRxLowIOSubmit\[LOWIO\_OP\_通知\_更改\_目录\]* 接收响应[ **IRP\_MJ\_目录\_控制**](irp-mj-directory-control.md)请求。

然后再调用*MRxLowIOSubmit\[LOWIO\_OP\_通知\_更改\_目录\]*，RDBSS 修改 RX中的以下成员\_指向上下文结构*RxContext*参数：

**LowIoContext.Operation**成员设置为 LOWIO\_OP\_通知\_更改\_目录。

**LowIoContext.ResourceThreadId**成员设置为启动 RDBSS 中的操作的进程线程。

**LowIoContext.ParamsFor.NotifyChangeDirectory.WatchTree**成员设置为**TRUE**如果**IrpSp-&gt;标志**具有 SL\_监视\_树位集。

**LowIoContext.ParamsFor.NotifyChangeDirectory.CompletionFilter**成员设置为值**IrpSp-&gt;Parameters.NotifyDirectory.CompletionFilter**。

**LowIoContext.ParamsFor.NotifyChangeDirectory.NotificationBufferLength**成员设置为值**IrpSp-&gt;Parameters.NotifyDirectory.Length**。

**LowIoContext.ParamsFor.NotifyChangeDirectory.pNotificationBuffer**成员设置为通过调用返回的值**MmGetSystemAddressForMdlSafe**传入**Irp&gt;MdlAddress**和 NormalPagePriority。 用户缓冲区也是探测和锁定以进行写访问。

目录更改通知操作通常由实现网络微型重定向作为异步操作因为它可能需要相当长的时间。 该操作通常组成的网络请求发送到远程服务器请求更改通知。 所需的更改会影响服务器上时，获得响应。 这是网络微型重定向可能需要为其注册唯一的上下文值来处理本地启动取消操作的示例。

虽然*MRxLowIOSubmit\[LOWIO\_OP\_通知\_更改\_目录\]* 处理例程， **LowIoContext.ResourceThreadId** RX 成员\_上下文保证以指示启动了 RDBSS 中的操作的进程线程。 **LowIoContext.ResourceThreadId**成员可用于释放 FCB 结构代表另一个线程。 完成异步例程后，可以释放已获取从初始线程的 FCB 结构。 FCB 结构可以释放通过调用[ **RxReleaseFcbResourceForThreadInMRx**](https://msdn.microsoft.com/library/windows/hardware/ff554694)。

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

[**MRxLowIOSubmit\[LOWIO\_OP\_READ\]**](mrxlowiosubmit-lowio-op-read-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_SHAREDLOCK\]**](mrxlowiosubmit-lowio-op-sharedlock-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_UNLOCK\]**](mrxlowiosubmit-lowio-op-unlock-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_UNLOCK\_MULTIPLE\]**](mrxlowiosubmit-lowio-op-unlock-multiple-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_WRITE\]**](mrxlowiosubmit-lowio-op-write-.md)

[**RxReleaseFcbResourceForThreadInMRx**](https://msdn.microsoft.com/library/windows/hardware/ff554694)

 

 






