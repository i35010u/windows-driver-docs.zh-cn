---
title: MRxLowIOSubmit\ LOWIO\_OP\_WRITE\ routine
description: MRxLowIOSubmit\ LOWIO\_OP\_WRITE\ 例程调用通过 RDBSS 网络微型重定向到发出写入请求。
ms.assetid: b70838e3-4e80-4ec9-88ba-0f608a1af78e
keywords:
- MRxLowIOSubmit LOWIO_OP_WRITE 例程可安装文件系统驱动程序
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
ms.openlocfilehash: f4ceadbf90a36c517062135cb038e176b30ac36e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370093"
---
# <a name="mrxlowiosubmitlowioopwrite-routine"></a>MRxLowIOSubmit\[LOWIO\_OP\_WRITE\] routine


*MRxLowIOSubmit\[LOWIO\_OP\_编写\]* 调用例程[RDBSS](https://docs.microsoft.com/windows-hardware/drivers/ifs/the-rdbss-driver-and-library)网络微型重定向到发出写入请求。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxLowIOSubmit[LOWIO_OP_WRITE];

NTSTATUS MRxLowIOSubmit[LOWIO_OP_WRITE](
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

*MRxLowIOSubmit\[LOWIO\_OP\_编写\]* 返回状态\_成功的成功或相应 NTSTATUS 值，如以下项之一：

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

RDBSS 调用*MRxLowIOSubmit\[LOWIO\_OP\_编写\]* 接收响应[ **IRP\_MJ\_编写** ](irp-mj-write.md)请求。

然后再调用*MRxLowIOSubmit\[LOWIO\_OP\_编写\]* ，RDBSS 修改 RX 中的以下成员\_上下文结构指向*RxContext*参数：

**LowIoContext.Operation**成员设置为 LOWIO\_OP\_编写。

**LowIoContext.ResourceThreadId**成员设置为启动 RDBSS 中的操作的进程线程。

**LowIoContext.ParamsFor.ReadWrite.Key**成员设置为值**IrpSp-&gt;Parameters.Read.Key**。

**ParamsFor.ReadWrite.Flags**成员具有 LOWIO\_READWRITEFLAG\_分页\_则设置 IO 位**Irp-&gt;标志**具有 IRP\_分页\_位上的 IO。

**ParamsFor.ReadWrite.Buffer**成员设置为用户缓冲区为 IoWriteAccess 锁定了。

**LowIoContext.ParamsFor.ReadWrite.ByteCount**成员设置为值**IrpSp-&gt;Parameters.Write.Length**。

写入请求通常由实现网络微型重定向作为异步操作因为它可能需要相当长的时间。 该操作通常组成的网络请求发送到远程服务器。 在服务器上完成写入请求时获得响应。 这是操作的网络微型重定向可能需要为其注册用于处理取消启动的本地上下文的示例。

虽然*MRxLowIOSubmit\[LOWIO\_OP\_编写\]* 处理例程， **LowIoContext.ResourceThreadId** RX的成员\_保证上下文以指示启动了 RDBSS 中的操作的进程线程。 **LowIoContext.ResourceThreadId**成员可用于释放 FCB 结构代表另一个线程。 完成异步例程后，可以释放已获取从初始线程的 FCB 结构。 FCB 结构可以释放通过调用[ **RxReleaseFcbResourceForThreadInMRx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrxfcb/nf-mrxfcb-rxreleasefcbresourceforthreadinmrx)。

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


[**MRxLowIOSubmit\[LOWIO\_OP\_EXCLUSIVELOCK\]** ](mrxlowiosubmit-lowio-op-exclusivelock-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_FSCTL\]** ](mrxlowiosubmit-lowio-op-fsctl-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_IOCTL\]** ](mrxlowiosubmit-lowio-op-ioctl-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_NOTIFY\_CHANGE\_DIRECTORY\]** ](mrxlowiosubmit-lowio-op-notify-change-directory-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_READ\]** ](mrxlowiosubmit-lowio-op-read-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_SHAREDLOCK\]** ](mrxlowiosubmit-lowio-op-sharedlock-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_UNLOCK\]** ](mrxlowiosubmit-lowio-op-unlock-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_UNLOCK\_MULTIPLE\]** ](mrxlowiosubmit-lowio-op-unlock-multiple-.md)

[**RxReleaseFcbResourceForThreadInMRx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrxfcb/nf-mrxfcb-rxreleasefcbresourceforthreadinmrx)

 

 






