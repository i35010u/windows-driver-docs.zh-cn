---
title: '\_\_RxSynchronizeBlockingOperationsMaybeDroppingFcbLock 函数'
description: '\_\_RxSynchronizeBlockingOperationsMaybeDroppingFcbLock 将阻塞 i/o 请求同步到相同的工作队列。'
ms.assetid: 350294ca-9790-4996-bcb5-1423db762c6e
keywords:
- __RxSynchronizeBlockingOperationsMaybeDroppingFcbLock 函数可安装的文件系统驱动程序
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
ms.openlocfilehash: fbc10cb53121c8a017fdaaca50f49466abd2dc32
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841521"
---
# <a name="__rxsynchronizeblockingoperationsmaybedroppingfcblock-function"></a>\_\_RxSynchronizeBlockingOperationsMaybeDroppingFcbLock 函数


**\_\_RxSynchronizeBlockingOperationsMaybeDroppingFcbLock**将阻塞 i/o 请求同步到相同的工作队列。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
NTSTATUS __RxSynchronizeBlockingOperationsMaybeDroppingFcbLock(
  _Inout_ PRX_CONTEXT RxContext,
  _Inout_ PLIST_ENTRY BlockingIoQ,
  _In_    BOOLEAN     DropFcbLock
);
```

<a name="parameters"></a>参数
----------

*RxContext* \[in，out\]  
一个指针，指向正在同步的操作的 RX\_上下文。

*BlockingIoQ* \[in，out\]  
指向队列的列表\_项的指针。

\] 中的*DropFcbLock* \[  
指示是否应释放 FCB 资源的布尔值。 如果此参数为**TRUE**，则将释放 FCB 资源。

<a name="return-value"></a>返回值
------------

**\_\_RxSynchronizeBlockingOperationsMaybeDroppingFcbLock**返回\_成功成功的状态，或者返回相应的 NTSTATUS 值，如以下之一：

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
<td align="left"><p>已取消 i/o 请求和关联的 RX_CONTEXT。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_PENDING</strong></td>
<td align="left"><p><em>RxContext</em>用于异步操作， <em>RxContext</em>已添加到队列中。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

**\_\_RxSynchronizeBlockingOperationsMaybeDroppingFcbLock**例程将阻塞 i/o 请求同步到相同的工作队列。 RDBSS 在内部使用 **\_RxSynchronizeBlockingOperationsMaybeDroppingFcbLock\_** 来同步命名管道操作。 工作队列是文件对象扩展（FOBX）所引用的队列，与*RxContext*指向的 RX\_上下文结构的**pFcb**成员关联。

网络小型重定向程序可能使用 **\_\_RxSynchronizeBlockingOperationsMaybeDroppingFcbLock**来同步网络小型重定向程序维护的单独队列上的操作。

如果*RxContext*被标记为异步操作， **\_\_RxSynchronizeBlockingOperationsMaybeDroppingFcbLock**将*RxContext*添加到队列，并返回状态\_"挂起"。 如果*RxContext*被标记为同步操作，则当调用 RxResumeBlockedOperations 时，将阻止 **\_\_RxSynchronizeBlockingOperationsMaybeDroppingFcbLock**和*RxContext*恢复[ **\_顺序**](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxresumeblockedoperations_serially)。

如果已取消阻塞 i/o 请求，则 **\_\_RxSynchronizeBlockingOperationsMaybeDroppingFcbLock**返回状态\_"已取消" 以指示错误。

**\_RxSynchronizeBlockingOperationsMaybeDroppingFcbLock\_** 调用之前 *，必须先*重置**SyncEvent**的 RX\_上下文结构的成员。 如果*DropFcbLock*参数设置为**TRUE**，则必须先锁定 FCB 资源，然后才能调用 **\_\_RxSynchronizeBlockingOperationsMaybeDroppingFcbLock** 。

以下两个宏在 Windows XP 和 Windows 2000 上定义，以便调用 **\_\_RxSynchronizeBlockingOperationsMaybeDroppingFcbLock** ：

**RxSynchronizeBlockingOperations** -将*DropFcbLock*参数设置为**FALSE**时调用。

**RxSynchronizeBlockingOperationsAndDropFcbLock** -将*DropFcbLock*参数设置为**TRUE**时调用。

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
<td align="left"><p>版本</p></td>
<td align="left"><p>__RxSynchronizeBlockingOperationsMaybeDroppingFcbLock 例程仅在 Windows XP 和 Windows 2000 上可用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Rxcontx （包括 Rxcontx）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**RxCompleteRequest\_Real**](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxcompleterequest_real)

[**RxCreateRxContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxcreaterxcontext)

[**RxDereference**](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxdereference)

[**RxDereferenceAndDeleteRxContext\_Real**](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxdereferenceanddeleterxcontext_real)

[**RxInitializeContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxinitializecontext)

[**RxPrepareContextForReuse**](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxpreparecontextforreuse)

[**RxResumeBlockedOperations\_串行**](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxresumeblockedoperations_serially)

[ **\_\_RxSynchronizeBlockingOperations**](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-__rxsynchronizeblockingoperations)

 

 






