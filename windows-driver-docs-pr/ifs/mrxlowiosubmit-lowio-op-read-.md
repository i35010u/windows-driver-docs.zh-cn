---
title: MRxLowIOSubmit \ LOWIO\_OP\_READ \ 例程
description: RDBSS 调用 MRxLowIOSubmit \ LOWIO\_OP\_READ \ 例程向网络小型重定向程序发出读取请求。
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
ms.openlocfilehash: 1749ba0d0b811df68876538a3a885688b3832b6c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841102"
---
# <a name="mrxlowiosubmitlowio_op_read-routine"></a>MRxLowIOSubmit\[LOWIO\_操作\_读取\] 例程


[RDBSS](https://docs.microsoft.com/windows-hardware/drivers/ifs/the-rdbss-driver-and-library)调用*MRxLowIOSubmit\[LOWIO\_OP\_read\]* 例程向网络小型重定向程序发出读取请求。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxLowIOSubmit[LOWIO_OP_READ];

NTSTATUS MRxLowIOSubmit[LOWIO_OP_READ](
  _Inout_ PRX_CONTEXT RxContext
)
{ ... }
```

<a name="parameters"></a>parameters
----------

*RxContext* \[in，out\]  
指向 RX\_上下文结构的指针。 此参数包含请求操作的 IRP。

<a name="return-value"></a>返回值
------------

*MRxLowIOSubmit\[LOWIO\_OP\_读取\]* 返回状态\_成功或适当的 NTSTATUS 值，如以下之一：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">返回代码</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>STATUS_FILE_CLOSED</strong></td>
<td align="left"><p>已获取 FCB 结构，但已关闭关联的 SRV_OPEN 结构。</p></td>
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
<td align="left"><p>在<em>RxContext</em>中指定了无效的参数。</p></td>
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

RDBSS 调用*MRxLowIOSubmit\[LOWIO\_OP\_读取\]* 以响应接收[**IRP\_MJ\_读取**](irp-mj-read.md)请求。

在调用*MRxLowIOSubmit\[LOWIO\_OP\_读取\]* 之前，RDBSS 会修改*RxContext*参数指向的 RX\_上下文结构中的以下成员：

**LowIoContext**成员设置为 LOWIO\_OP\_读取。

**LowIoContext. ResourceThreadId**成员设置为在 RDBSS 中启动操作的进程线程。

**LowIoContext**成员设置为**IrpSp-&gt;参数的值。 Read. key**。

**ParamsFor**成员具有 LOWIO\_READWRITEFLAG\_分页\_io 位设置为，前提是**Irp-&gt;标志**在上有 irp\_分页。\_

**ParamsFor**成员设置为锁定 IoReadAccess 的用户缓冲区。

**LowIoContext**成员设置为 IrpSp-&gt;参数的值。读取的长度。

读取请求通常由网络小型重定向程序作为异步操作来实现，因为这可能需要相当长的时间。 操作通常包含向远程服务器发送网络请求。 当读取请求在服务器上完成时，将获取响应。 这是一个操作示例，网络小型重定向程序可能需要为此操作注册上下文以处理本地启动的取消。

尽管*MRxLowIOSubmit\[LOWIO\_OP\_读取\]* 例程正在处理，但 RX\_上下文的**LowIoContext**成员仍可保证指示启动了RDBSS 中的操作。 **LowIoContext. ResourceThreadId**成员可用于代表其他线程发布 FCB 结构。 异步例程完成后，可以释放从初始线程获取的 FCB 结构。 可以通过调用[**RxReleaseFcbResourceForThreadInMRx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxreleasefcbresourceforthreadinmrx)来释放 FCB 结构。

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
<td align="left">Mrx （包括 Mrx）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**MRxLowIOSubmit\[LOWIO\_操作\_EXCLUSIVELOCK\]** ](mrxlowiosubmit-lowio-op-exclusivelock-.md)

[**MRxLowIOSubmit\[LOWIO\_操作\_FSCTL\]** ](mrxlowiosubmit-lowio-op-fsctl-.md)

[**MRxLowIOSubmit\[LOWIO\_操作\_IOCTL\]** ](mrxlowiosubmit-lowio-op-ioctl-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_通知\_更改\_目录\]** ](mrxlowiosubmit-lowio-op-notify-change-directory-.md)

[**MRxLowIOSubmit\[LOWIO\_操作\_SHAREDLOCK\]** ](mrxlowiosubmit-lowio-op-sharedlock-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_解锁\]** ](mrxlowiosubmit-lowio-op-unlock-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_\_多个\]** ](mrxlowiosubmit-lowio-op-unlock-multiple-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_写入\]** ](mrxlowiosubmit-lowio-op-write-.md)

[**RxReleaseFcbResourceForThreadInMRx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxreleasefcbresourceforthreadinmrx)

 

 






