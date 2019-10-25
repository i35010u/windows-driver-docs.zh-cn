---
title: MRxLowIOSubmit \ LOWIO\_OP\_通知\_更改\_DIRECTORY \ 例程
description: MRxLowIOSubmit \ LOWIO\_OP\_通知\_更改\_DIRECTORY \ 例程由 RDBSS 调用，以向网络小型重定向程序发出目录更改通知操作请求。
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
ms.openlocfilehash: 0f7d2e7aff720b3837cdad446ab48f43bcb9b398
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841105"
---
# <a name="mrxlowiosubmitlowio_op_notify_change_directory-routine"></a>MRxLowIOSubmit\[LOWIO\_OP\_通知\_更改\_DIRECTORY\] 例程


*MRxLowIOSubmit\[LOWIO\_OP\_通知\_更改\_目录\]* 例程由[RDBSS](https://docs.microsoft.com/windows-hardware/drivers/ifs/the-rdbss-driver-and-library)调用，以向网络小型重定向程序发出目录更改通知操作请求。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxLowIOSubmit[LOWIO_OP_NOTIFY_CHANGE_DIRECTORY];

NTSTATUS MRxLowIOSubmit[LOWIO_OP_NOTIFY_CHANGE_DIRECTORY](
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

*MRxLowIOSubmit\[LOWIO\_OP\_通知\_更改\_DIRECTORY*\]返回状态\_成功或适当的 NTSTATUS 值，如以下之一：

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

RDBSS 调用*MRxLowIOSubmit\[LOWIO\_OP\_通知\_更改\_directory*\]，以响应接收[**IRP\_目录\_** ](irp-mj-directory-control.md)的请求。

在调用*MRxLowIOSubmit\[LOWIO\_OP\_通知\_更改\_DIRECTORY\]* 中，RDBSS 修改*RxContext*参数指向的 RX\_上下文结构中的以下成员：

**LowIoContext**成员设置为 LOWIO\_OP\_通知\_更改\_目录。

**LowIoContext. ResourceThreadId**成员设置为在 RDBSS 中启动操作的进程线程。

如果**IrpSp&gt;标志**具有 SL\_WATCH\_树位集，则将**LowIoContext**成员设置为**TRUE** 。

**LowIoContext. ParamsFor. NotifyChangeDirectory. CompletionFilter**成员的值设置为 **&gt;IrpSp**，NotifyDirectory. CompletionFilter。

**LowIoContext. ParamsFor. NotifyChangeDirectory. NotificationBufferLength**成员设置为**IrpSp-&gt;参数**的值。 NotifyDirectory。

**LowIoContext. ParamsFor. NotifyChangeDirectory. pNotificationBuffer**成员设置为**通过调用并传入** **Irp&gt;MmGetSystemAddressForMdlSafe**和 MdlAddress 返回的值。 还会探测并锁定用户缓冲区以进行写访问。

目录更改通知操作通常由网络小型重定向程序作为异步操作来实现，因为这可能需要相当长的时间。 此操作通常包含向远程服务器发送请求更改通知的网络请求。 当所需的更改在服务器上受到影响时，将获取响应。 这是一个操作示例，网络小型重定向程序可能需要为此操作注册一个唯一的上下文值，以便处理本地启动的取消。

尽管*MRxLowIOSubmit\[LOWIO\_OP\_通知\_更改\_DIRECTORY\]* 例程正在处理，但 RX\_上下文的**LowIoContext**成员仍可指示启动 RDBSS 中的操作的进程线程。 **LowIoContext. ResourceThreadId**成员可用于代表其他线程发布 FCB 结构。 异步例程完成后，可以释放从初始线程获取的 FCB 结构。 可以通过调用[**RxReleaseFcbResourceForThreadInMRx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxreleasefcbresourceforthreadinmrx)来释放 FCB 结构。

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

[**MRxLowIOSubmit\[LOWIO\_操作\_读取\]** ](mrxlowiosubmit-lowio-op-read-.md)

[**MRxLowIOSubmit\[LOWIO\_操作\_SHAREDLOCK\]** ](mrxlowiosubmit-lowio-op-sharedlock-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_解锁\]** ](mrxlowiosubmit-lowio-op-unlock-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_\_多个\]** ](mrxlowiosubmit-lowio-op-unlock-multiple-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_写入\]** ](mrxlowiosubmit-lowio-op-write-.md)

[**RxReleaseFcbResourceForThreadInMRx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxreleasefcbresourceforthreadinmrx)

 

 






