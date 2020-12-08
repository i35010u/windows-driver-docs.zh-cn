---
title: '\_\_RxSynchronizeBlockingOperationsMaybeDroppingFcbLock 函数'
description: '\_\_RxSynchronizeBlockingOperationsMaybeDroppingFcbLock 将阻塞 i/o 请求同步到相同的工作队列。'
keywords:
- __RxSynchronizeBlockingOperationsMaybeDroppingFcbLock 功能可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- __RxSynchronizeBlockingOperationsMaybeDroppingFcbLock
api_location:
- rxcontx.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 09cdc487f815de9ac4bc82a0f682b2e139a598d2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789957"
---
# <a name="__rxsynchronizeblockingoperationsmaybedroppingfcblock-function"></a>\_\_RxSynchronizeBlockingOperationsMaybeDroppingFcbLock 函数


**\_ \_ RxSynchronizeBlockingOperationsMaybeDroppingFcbLock** 将阻塞 i/o 请求同步到相同的工作队列。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
NTSTATUS __RxSynchronizeBlockingOperationsMaybeDroppingFcbLock(
  _Inout_ PRX_CONTEXT RxContext,
  _Inout_ PLIST_ENTRY BlockingIoQ,
  _In_    BOOLEAN     DropFcbLock
);
```

<a name="parameters"></a>参数
----------

*RxContext* \[in、out\]  
指向正在同步的操作的 RX 上下文的指针 \_ 。

*BlockingIoQ* \[in、out\]  
指向队列的列表项的指针 \_ 。

*DropFcbLock* \[中\]  
指示是否应释放 FCB 资源的布尔值。 如果此参数为 **TRUE**，则将释放 FCB 资源。

<a name="return-value"></a>返回值
------------

**\_ \_ RxSynchronizeBlockingOperationsMaybeDroppingFcbLock** 返回 \_ 成功或适当的 NTSTATUS 值（如下所示）：

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
<td align="left"><strong>STATUS_CANCELLED</strong></td>
<td align="left"><p>I/o 请求和关联的 RX_CONTEXT 已取消。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_PENDING</strong></td>
<td align="left"><p><em>RxContext</em>用于异步操作， <em>RxContext</em>已添加到队列中。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

**\_ \_ RxSynchronizeBlockingOperationsMaybeDroppingFcbLock** 例程将阻塞 i/o 请求同步到相同的工作队列。 RDBSS 在内部使用 **\_ \_ RxSynchronizeBlockingOperationsMaybeDroppingFcbLock** 来同步命名管道操作。 工作队列是文件对象扩展所引用的队列 (FOBX) 与 RxContext 指向的 RX 上下文结构的 **pFcb** 成员关联 \_ 。 *RxContext*

网络小型重定向程序可能使用 **\_ \_ RxSynchronizeBlockingOperationsMaybeDroppingFcbLock** 来同步网络小型重定向器维护的单独队列上的操作。

如果 *RxContext* 标记为异步操作，则 **\_ \_ RxSynchronizeBlockingOperationsMaybeDroppingFcbLock** 会将 *RxContext* 添加到队列并返回状态 " \_ 挂起"。 如果 *RxContext* 被标记为同步操作，则当调用 [**RxResumeBlockedOperations \_ 串行**](/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxresumeblockedoperations_serially)时， **\_ \_ RxSynchronizeBlockingOperationsMaybeDroppingFcbLock** 将会阻止和 *RxContext* 。

如果已取消阻塞 i/o 请求，则 **\_ \_ RxSynchronizeBlockingOperationsMaybeDroppingFcbLock** 将返回 "状态已 \_ 取消" 以指示错误。

在 **SyncEvent** \_ 调用 **\_ \_ RxSynchronizeBlockingOperationsMaybeDroppingFcbLock** 之前，必须重置 *RxContext* 指向的 RX 上下文结构的 SyncEvent 成员。 如果 *DropFcbLock* 参数设置为 **TRUE**，则必须在调用 **\_ \_ RxSynchronizeBlockingOperationsMaybeDroppingFcbLock** 之前锁定 FCB 资源。

以下两个宏在 windows XP 和 windows 2000 上定义，以便调用 **\_ \_ RxSynchronizeBlockingOperationsMaybeDroppingFcbLock** ：

**RxSynchronizeBlockingOperations** -将 *DropFcbLock* 参数设置为 **FALSE** 时调用。

**RxSynchronizeBlockingOperationsAndDropFcbLock** -将 *DropFcbLock* 参数设置为 **TRUE** 时调用。

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
<td align="left">台式机</td>
</tr>
<tr class="even">
<td align="left"><p>版本</p></td>
<td align="left"><p>__RxSynchronizeBlockingOperationsMaybeDroppingFcbLock 例程只能在 Windows XP 和 Windows 2000 上使用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Rxcontx (包含 Rxcontx) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**RxCompleteRequest \_ Real**](/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxcompleterequest_real)

[**RxCreateRxContext**](/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxcreaterxcontext)

[**RxDereference**](/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxdereference)

[**RxDereferenceAndDeleteRxContext \_ Real**](/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxdereferenceanddeleterxcontext_real)

[**RxInitializeContext**](/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxinitializecontext)

[**RxPrepareContextForReuse**](/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxpreparecontextforreuse)

[**RxResumeBlockedOperations \_ 串行**](/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxresumeblockedoperations_serially)

[**\_\_RxSynchronizeBlockingOperations**](/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-__rxsynchronizeblockingoperations)

 

