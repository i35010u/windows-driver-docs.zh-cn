---
title: '\_\_RxSynchronizeBlockingOperationsMaybeDroppingFcbLock function'
description: '\_\_RxSynchronizeBlockingOperationsMaybeDroppingFcbLock 将同步到相同的工作队列的阻塞 I/O 请求。'
ms.assetid: 350294ca-9790-4996-bcb5-1423db762c6e
keywords:
- __RxSynchronizeBlockingOperationsMaybeDroppingFcbLock 函数可安装文件系统驱动程序
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
ms.openlocfilehash: 2ea8d4efae6fe18b0134eb7c8d6879bf49db4ea6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381028"
---
# <a name="rxsynchronizeblockingoperationsmaybedroppingfcblock-function"></a>\_\_RxSynchronizeBlockingOperationsMaybeDroppingFcbLock function


**\_\_RxSynchronizeBlockingOperationsMaybeDroppingFcbLock**同步到相同的工作队列的阻塞 I/O 请求。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
NTSTATUS __RxSynchronizeBlockingOperationsMaybeDroppingFcbLock(
  _Inout_ PRX_CONTEXT RxContext,
  _Inout_ PLIST_ENTRY BlockingIoQ,
  _In_    BOOLEAN     DropFcbLock
);
```

<a name="parameters"></a>Parameters
----------

*RxContext* \[in、 out\]  
指向 RX\_正在同步的操作上下文。

*BlockingIoQ* \[in、 out\]  
一个指向列表\_队列的条目。

*DropFcbLock* \[in\]  
一个布尔值，该值指示是否应释放 FCB 资源。 如果此参数为 **，则返回 TRUE**，则将释放 FCB 资源。

<a name="return-value"></a>返回值
------------

**\_\_RxSynchronizeBlockingOperationsMaybeDroppingFcbLock**将返回状态\_成功或适当的 NTSTATUS 值如以下之一成功：

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
<td align="left"><p>已取消 I/O 请求和关联的 RX_CONTEXT。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_PENDING</strong></td>
<td align="left"><p><em>RxContext</em>是针对异步操作并<em>RxContext</em>已添加到队列。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

**\_\_RxSynchronizeBlockingOperationsMaybeDroppingFcbLock** 例程会同步到相同的工作队列的阻塞 I/O 请求。 使用 RDBSS  **\_ \_RxSynchronizeBlockingOperationsMaybeDroppingFcbLock**内部同步名为管道操作。 工作队列是引用文件对象关联的扩展插件 (FOBX) 使用的队列**pFcb** RX 成员\_指向上下文结构*RxContext*。

可以使用网络微型重定向 **\_ \_RxSynchronizeBlockingOperationsMaybeDroppingFcbLock**来同步对单独的队列是由网络微型重定向维护操作。

如果*RxContext*标记的异步操作 **\_ \_RxSynchronizeBlockingOperationsMaybeDroppingFcbLock**将添加*RxContext*队列并返回状态为\_PENDING。 如果*RxContext*标记为同步操作 **\_ \_RxSynchronizeBlockingOperationsMaybeDroppingFcbLock**将阻止和*RxContext*到进行调用时恢复[ **RxResumeBlockedOperations\_串行**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxcontx/nf-rxcontx-rxresumeblockedoperations_serially)。

如果已取消阻塞 I/O 请求，  **\_ \_RxSynchronizeBlockingOperationsMaybeDroppingFcbLock**返回状态\_以指示出错时已取消。

**SyncEvent** RX 成员\_指向上下文结构*RxContext*必须具有已重置之前，先 **\_ \_RxSynchronizeBlockingOperationsMaybeDroppingFcbLock**。 FCB 资源必须锁定，然后再调 **\_ \_RxSynchronizeBlockingOperationsMaybeDroppingFcbLock**如果*DropFcbLock*参数设置为 **，则返回 TRUE**。

在 Windows XP 和 Windows 2000 上为调用定义以下两个宏 **\_ \_RxSynchronizeBlockingOperationsMaybeDroppingFcbLock** :

**RxSynchronizeBlockingOperations** -使用调用*DropFcbLock*参数设置为**FALSE**。

**RxSynchronizeBlockingOperationsAndDropFcbLock** -使用调用*DropFcbLock*参数设置为**TRUE**。

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
<td align="left"><p>Version</p></td>
<td align="left"><p>Windows XP 和 Windows 2000 上才 __RxSynchronizeBlockingOperationsMaybeDroppingFcbLock 例程。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Rxcontx.h （包括 Rxcontx.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**RxCompleteRequest\_Real**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxcompleterequest_real)

[**RxCreateRxContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxcontx/nf-rxcontx-rxcreaterxcontext)

[**RxDereference**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxdereference)

[**RxDereferenceAndDeleteRxContext\_Real**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxcontx/nf-rxcontx-rxdereferenceanddeleterxcontext_real)

[**RxInitializeContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxcontx/nf-rxcontx-rxinitializecontext)

[**RxPrepareContextForReuse**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxcontx/nf-rxcontx-rxpreparecontextforreuse)

[**RxResumeBlockedOperations\_Serially**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxcontx/nf-rxcontx-rxresumeblockedoperations_serially)

**[\_\_RxSynchronizeBlockingOperations](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxcontx/nf-rxcontx-__rxsynchronizeblockingoperations)**

 

 






