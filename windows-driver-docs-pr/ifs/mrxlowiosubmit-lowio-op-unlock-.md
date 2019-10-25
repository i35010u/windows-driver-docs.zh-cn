---
title: MRxLowIOSubmit \ LOWIO\_OP\_UNLOCK \ 例程
description: RDBSS 调用 MRxLowIOSubmit \ LOWIO\_OP\_UNLOCK \ 例程来请求网络小型重定向程序删除文件对象上的单个锁。
ms.assetid: 2985ae12-965d-4871-b56e-2589898932e1
keywords:
- MRxLowIOSubmit LOWIO_OP_UNLOCK 例程可安装文件系统驱动程序
- PMRX_CALLDOWN
topic_type:
- apiref
api_name:
- MRxLowIOSubmit LOWIO_OP_UNLOCK
api_location:
- mrx.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 10967163e096c0137221187c2fd9ca4638ce68f3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841099"
---
# <a name="mrxlowiosubmitlowio_op_unlock-routine"></a>MRxLowIOSubmit\[LOWIO\_OP\_解锁\] 例程


[RDBSS](https://docs.microsoft.com/windows-hardware/drivers/ifs/the-rdbss-driver-and-library)调用*MRxLowIOSubmit\[LOWIO\_OP\_解锁\]* 例程来请求网络小型重定向程序删除文件对象上的单个锁。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxLowIOSubmit[LOWIO_OP_UNLOCK];

NTSTATUS MRxLowIOSubmit[LOWIO_OP_UNLOCK](
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

*MRxLowIOSubmit\[LOWIO\_操作\_解锁\]* 返回状态\_成功或适当的 NTSTATUS 值，如以下之一：

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
<td align="left"><strong>STATUS_INVALID_NETWORK_RESPONSE</strong></td>
<td align="left"><p>从远程服务器收到无效的响应。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_INVALID_PARAMETER</strong></td>
<td align="left"><p>在<em>RxContext</em>中指定了无效的参数。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_LINK_FAILED</strong></td>
<td align="left"><p>尝试重新连接到远程服务器以完成请求失败。</p></td>
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
<td align="left"><p>调用失败。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

RDBSS 调用*MRxLowIOSubmit\[LOWIO\_OP\_锁定\]* ，以响应接收[**irp\_MJ**](irp-mj-lock-control.md)\_使用次代码 irp\_单个.

在调用*MRxLowIOSubmit\[LOWIO\_OP\_解锁\]* 之前，RDBSS 会修改*RxContext*参数指向的 RX\_上下文结构中的以下成员：

**LowIoContext**成员设置为 LOWIO\_OP\_UNLOCK。

**LowIoContext. ResourceThreadId**成员设置为在 RDBSS 中启动操作的进程线程。

**ParamsFor. ByteOffset**成员设置为**IrpSp&gt;** LowIoContext 的值。 LockControl. ByteOffset. QuadPart。

将**LowIoContext**成员设置为**IrpSp-&gt;参数**的值 LockControl。

**LowIoContext**成员设置为**IrpSp-&gt;LockControl. QuadPart**的值。

RX\_的**LowIoContext**成员指定要执行的低 i/o 操作。 由于可以使用此**LowIoContext**成员来区分请求的低 i/o 操作，因此几个低 i/o 例程可能会指向网络小型重定向程序中的同一例程。 例如，所有与文件锁相关的 i/o 调用都可以在网络小型重定向程序中调用相同的低 i/o 例程，此例程可以使用**LowIoContext**成员来区分所请求的锁定和解除锁定操作。

如果*MRxLowIOSubmit\[LOWIO\_OP\_解锁\]* 例程可能需要很长时间才能完成，则网络小型重定向程序驱动程序应在启动网络通信之前释放 FCB 结构。 可以通过调用[**RxReleaseFcbResourceForThreadInMRx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxreleasefcbresourceforthreadinmrx)来释放 FCB 结构。 尽管*MRxLowIOSubmit\[LOWIO\_OP\_解锁\]* 例程正在处理，但 RX\_上下文的**LowIoContext**成员仍可指示已启动的进程的线程RDBSS 中的操作。

RX\_上下文的**ResourceThreadId**成员可用于代表其他线程发布 FCB 结构。 异步例程完成后，可以释放从初始线程获取的 FCB 结构。

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


[**MRxLowIOSubmit\[LOWIO\_操作\_EXCLUSIVELOCK\]** ](mrxlowiosubmit-lowio-op-exclusivelock-.md)

[**MRxLowIOSubmit\[LOWIO\_操作\_FSCTL\]** ](mrxlowiosubmit-lowio-op-fsctl-.md)

[**MRxLowIOSubmit\[LOWIO\_操作\_IOCTL\]** ](mrxlowiosubmit-lowio-op-ioctl-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_通知\_更改\_目录\]** ](mrxlowiosubmit-lowio-op-notify-change-directory-.md)

[**MRxLowIOSubmit\[LOWIO\_操作\_读取\]** ](mrxlowiosubmit-lowio-op-read-.md)

[**MRxLowIOSubmit\[LOWIO\_操作\_SHAREDLOCK\]** ](mrxlowiosubmit-lowio-op-sharedlock-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_\_多个\]** ](mrxlowiosubmit-lowio-op-unlock-multiple-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_写入\]** ](mrxlowiosubmit-lowio-op-write-.md)

[**RxReleaseFcbResourceForThreadInMRx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxreleasefcbresourceforthreadinmrx)

 

 






