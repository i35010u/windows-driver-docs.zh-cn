---
title: IrqlExAllocatePool 规则 (wdm)
description: IrqlExAllocatePool 规则指定仅当执行在 IRQL 调度时驱动程序可调用 ExAllocatePoolWithTag 和 ExAllocatePoolWithTagPriority\_级别。
ms.assetid: 0bb179c5-e76b-46bc-b497-8639328d2eb2
ms.date: 05/21/2018
keywords:
- IrqlExAllocatePool 规则 (wdm)
topic_type:
- apiref
api_name:
- IrqlExAllocatePool
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2a611bacfb4707c0422febdf401f277640ed5d99
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577274"
---
# <a name="irqlexallocatepool-rule-wdm"></a>IrqlExAllocatePool 规则 (wdm)


**IrqlExAllocatePool**规则指定驱动程序调用[ **ExAllocatePoolWithTag** ](https://msdn.microsoft.com/library/windows/hardware/ff544520)并[ **ExAllocatePoolWithTagPriority** ](https://msdn.microsoft.com/library/windows/hardware/ff544523)仅当执行在 IRQL&lt;= 调度\_级别。

调用方执行调度\_级别必须指定未分页*Xxx*值*PoolType*。 调用方执行在 IRQL &lt;= APC\_级别可以指定任何[**池\_类型**](https://msdn.microsoft.com/library/windows/hardware/ff559707)值。

|              |     |
|--------------|-----|
| 驱动程序模型 | WDM |

|                                   |                                                                                                                                                                                                                                        |
|-----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 使用此规则发现的错误检查 | [**Bug 检查 0xC4:驱动程序\_VERIFIER\_已检测\_冲突**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x00020004) [ **Bug 检查 0xA:IRQL\_不\_较少\_或\_相等**](https://msdn.microsoft.com/library/windows/hardware/ff560129) |

<a name="example"></a>示例
-------

在以下示例中， [ **ExAllocatePoolWithTag** ](https://msdn.microsoft.com/library/windows/hardware/ff544520)后，会调用例程[ **KeAcquireSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff551917)例程，设置调度到的 IRQL\_级别。 **ExAllocatePoolWithTag**与调用例程**PagedPool**，这违反了该规则。

```ManagedCPlusPlus
NTSTATUS
DispatchRequest (
    __in PDEVICE_REQUEST DeviceRequest
    )
{  
    KIRQL OldIrql;
    KSPIN_LOCK SpinLock;
    NTSTATUS Status;
    ...

    KeInitializeSpinLock(&amp;SpinLock);

    //
    // KeAcquireSpinLock sets IRQL to DISPATCH_LEVEL and the previous IRQL is 
    // written to OldIrql after the lock is acquired.
    //

    KeAcquireSpinLock(&amp;SpinLock, &amp;OldIrql);
    ...

    Status = ProcessRequest(DeviceRequest);

    //
    // KeReleaseSpinLock sets IRQL to the OldIrql returned by KeAcquireSpinLock.
    //

    KeReleaseSpinLock(&amp;SpinLock, &amp;OldIrql);
    ...
}

NTSTATUS
ProcessRequest (
    __in PDEVICE_REQUEST DeviceRequest
    )
{
    NTSTATUS Status;
    ...

    //
    // RULE VIOLATION! - IrqlExAllocatePool executing at DISPATCH_LEVEL must specify 
    //                   a NonPagedXxx value for PoolType. 
    //

    DeviceRequest->Context = ExAllocatePool(PagedPool, sizeof(REQUEST_CONTEXT));
    if (DeviceRequest->Context == NULL) {
        Status = STATUS_INSUFFICIENT_RESOURCES;
    }
    ...

    return Status;
}
```

<a name="how-to-test"></a>如何测试
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">在编译时</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>IrqlExAllocatePool</strong>规则。</p>
使用以下步骤来分析你的代码：
<ol>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code)">准备你的代码 （使用角色类型声明）。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier)">运行的 Static Driver Verifier。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results)">查看和分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/hh454281" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://msdn.microsoft.com/library/windows/hardware/hh454281)">以找到缺陷驱动程序中使用 Static Driver Verifier</a>。</p></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">在运行时</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff545448" data-raw-source="[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)">Driver Verifier</a> ，然后选择<a href="https://msdn.microsoft.com/library/windows/hardware/hh454208" data-raw-source="[DDI compliance checking](https://msdn.microsoft.com/library/windows/hardware/hh454208)">DDI 符合性检查</a>选项。</p></td>
</tr>
</tbody>
</table>

 

<a name="applies-to"></a>适用对象
----------

[**ExAllocatePoolWithTag**](https://msdn.microsoft.com/library/windows/hardware/ff544520)
[**ExAllocatePoolWithTagPriority** ](https://msdn.microsoft.com/library/windows/hardware/ff544523)另请参阅
--------

[**管理硬件优先级**](https://msdn.microsoft.com/library/windows/hardware/ff554368)
[**使用自旋锁的同时防止错误和死锁**](https://msdn.microsoft.com/library/windows/hardware/ff559854)
 

 





