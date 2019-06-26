---
title: MRxLowIOSubmit\ LOWIO\_OP\_FSCTL\ 例程
description: MRxLowIOSubmit\ LOWIO\_OP\_FSCTL\ 例程 RDBSS 来请求通过网络微型重定向问题文件系统控制请求上调用远程文件。
ms.assetid: 6bbb4b65-c447-47d8-9d05-f2adfb607099
keywords:
- MRxLowIOSubmit LOWIO_OP_FSCTL 例程可安装文件系统驱动程序
- PMRX_CALLDOWN
topic_type:
- apiref
api_name:
- MRxLowIOSubmit LOWIO_OP_FSCTL
api_location:
- mrx.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21b2b38d9071598388585ae99886ee0a5aa10962
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363527"
---
# <a name="mrxlowiosubmitlowioopfsctl-routine"></a>MRxLowIOSubmit\[LOWIO\_OP\_FSCTL\] routine


*MRxLowIOSubmit\[LOWIO\_OP\_FSCTL\]* 调用例程[RDBSS](https://docs.microsoft.com/windows-hardware/drivers/ifs/the-rdbss-driver-and-library)请求网络微型重定向问题文件系统控制对远程文件的请求。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxLowIOSubmit[LOWIO_OP_FSCTL];

NTSTATUS MRxLowIOSubmit[LOWIO_OP_FSCTL](
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

*MRxLowIOSubmit\[LOWIO\_OP\_FSCTL\]* 返回状态\_成功的成功或相应 NTSTATUS 值，如以下项之一：

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
<td align="left"><strong>STATUS_INVALID_DEVICE_REQUEST</strong></td>
<td align="left"><p>指定了无效的设备请求。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_INVALID_NETWORK_RESPONSE</strong></td>
<td align="left"><p>从远程服务器收到了无效的响应。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_INVALID_PARAMETER</strong></td>
<td align="left"><p>在指定的参数无效<em>RxContext</em>。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_LINK_FAILED</strong></td>
<td align="left"><p>尝试重新连接到远程服务器来完成该请求失败。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_NOT_IMPLEMENTED</strong></td>
<td align="left"><p>未实现此例程。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_NOT_SUPPORTED</strong></td>
<td align="left"><p>指定了 FSCTL 不受网络微型重定向。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_UNSUCCESSFUL</strong></td>
<td align="left"><p>在调用不成功。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

RDBSS 调用*MRxLowIOSubmit\[LOWIO\_OP\_FSCTL\]* 接收响应[ **IRP\_MJ\_文件\_系统\_控制**](irp-mj-file-system-control.md)请求。

然后再调用*MRxLowIOSubmit\[LOWIO\_OP\_FSCTL\]* ，RDBSS 修改 RX 中的以下成员\_上下文结构指向*RxContext*参数：

**LowIoContext.Operation**成员设置为 LOWIO\_OP\_FSCTL。

**LowIoContext.ResourceThreadId**成员设置为启动 RDBSS 中的操作的进程线程。

**LowIoContext.ParamsFor.FsCtl.FsControlCode**成员设置为 FSCTL 主要控制代码。

**LowIoContext.ParamsFor.FsCtl.MinorFunction**成员设置为 FSCTL 细微的控制代码。

**LowIoContext.ParamsFor.FsCtl.pInputBuffer**成员设置为输入缓冲区。

**LowIoContext.ParamsFor.FsCtl.InputBufferLength**成员设置为输入的缓冲区长度。

**LowIoContext.ParamsFor.FsCtl.pOutputBuffer**成员设置为输出缓冲区。

**LowIoContext.ParamsFor.FsCtl.OutputBufferLength**成员设置为输出缓冲区长度。

由网络微型重定向处理文件系统控制 (FSCTL) 的代码请求可划分为几个类别之一：

-   FSCTLs 实现并由 RDBSS 和网络的最小重定向程序

-   FSCTLs 实现并只由网络微型重定向

-   应永远不会出现由网络微型重定向的 FSCTLs。 这些 FSCTLs 仅用作调试帮助。

虽然*MRxLowIOSubmit\[LOWIO\_OP\_FSCTL\]* 处理例程， **LowIoContext.ResourceThreadId** RX的成员\_保证上下文以指示启动了 RDBSS 中的操作的进程线程。 **LowIoContext.ResourceThreadId** RX 成员\_上下文可用于代表另一个线程释放输入的资源。 完成异步例程后，可以释放已获取从初始线程的输入的资源。

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

[**MRxLowIOSubmit\[LOWIO\_OP\_IOCTL\]** ](mrxlowiosubmit-lowio-op-ioctl-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_NOTIFY\_CHANGE\_DIRECTORY\]** ](mrxlowiosubmit-lowio-op-notify-change-directory-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_READ\]** ](mrxlowiosubmit-lowio-op-read-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_SHAREDLOCK\]** ](mrxlowiosubmit-lowio-op-sharedlock-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_UNLOCK\]** ](mrxlowiosubmit-lowio-op-unlock-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_UNLOCK\_MULTIPLE\]** ](mrxlowiosubmit-lowio-op-unlock-multiple-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_WRITE\]** ](mrxlowiosubmit-lowio-op-write-.md)

 

 






