---
title: 'IrqlExAllocatePool 规则 (wdm) '
description: IrqlExAllocatePool 规则指定仅当驱动程序在 IRQL 调度级别执行时，驱动程序才调用 ExAllocatePoolWithTag 和 ExAllocatePoolWithTagPriority \_ 。
ms.date: 05/21/2018
keywords:
- 'IrqlExAllocatePool 规则 (wdm) '
topic_type:
- apiref
api_name:
- IrqlExAllocatePool
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c2f9f057a164da656ad605d8bbccfa26f1ceb8f6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792331"
---
# <a name="irqlexallocatepool-rule-wdm"></a>IrqlExAllocatePool 规则 (wdm) 


**IrqlExAllocatePool** 规则指定仅当驱动程序以 IRQL = 调度级别执行时，驱动程序才调用 [**ExAllocatePoolWithTag**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)和 [**ExAllocatePoolWithTagPriority**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtagpriority) &lt; \_ 。

在调度级别执行的调用方 \_ 必须为 *PoolType* 指定非分页的 *Xxx* 值。 在 IRQL = APC 级别执行的调用方 &lt; \_ 可以指定任何 [**池 \_ 类型**](/windows-hardware/drivers/ddi/wdm/ne-wdm-_pool_type) 值。

**驱动程序模型： WDM**

**Bug 检查 () 发现此规则**： [**bug 检查0XC4：驱动程序 \_ 验证器 \_ 检测到 \_ 违反**](../debugger/bug-check-0xc4--driver-verifier-detected-violation.md) (0X00020004) ， [**bug 检查0xA： IRQL \_ 不 \_ 小于 \_ 或 \_ 等于**](../debugger/bug-check-0xa--irql-not-less-or-equal.md)


<a name="example"></a>示例
-------

在下面的示例中， [**ExAllocatePoolWithTag**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag) 例程在 [**KeAcquireSpinLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock) 例程之后调用，后者将 IRQL 设置为调度 \_ 级别。 **ExAllocatePoolWithTag** 例程由 **PagedPool** 调用，后者违反了规则。

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

    KeInitializeSpinLock(&SpinLock);

    //
    // KeAcquireSpinLock sets IRQL to DISPATCH_LEVEL and the previous IRQL is 
    // written to OldIrql after the lock is acquired.
    //

    KeAcquireSpinLock(&SpinLock, &OldIrql);
    ...

    Status = ProcessRequest(DeviceRequest);

    //
    // KeReleaseSpinLock sets IRQL to the OldIrql returned by KeAcquireSpinLock.
    //

    KeReleaseSpinLock(&SpinLock, &OldIrql);
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
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>IrqlExAllocatePool</strong> 规则。</p>
使用以下步骤来运行代码分析：
<ol>
<li><a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](./using-static-driver-verifier-to-find-defects-in-drivers.md#preparing-your-source-code)">准备你的代码 (使用) 的角色类型声明。</a></li>
<li><a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](./using-static-driver-verifier-to-find-defects-in-drivers.md#running-static-driver-verifier)">运行静态驱动程序验证程序。</a></li>
<li><a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](./using-static-driver-verifier-to-find-defects-in-drivers.md#viewing-and-analyzing-the-results)">查看并分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅 <a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](./using-static-driver-verifier-to-find-defects-in-drivers.md)">使用静态驱动程序验证器查找驱动程序中的缺陷</a>。</p></td>
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
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](./driver-verifier.md)">驱动程序验证程序</a> ，并选择 " <a href="/windows-hardware/drivers/devtest/ddi-compliance-checking" data-raw-source="[DDI compliance checking](./ddi-compliance-checking.md)">DDI 相容性检查</a> " 选项。</p></td>
</tr>
</tbody>
</table>

 

<a name="applies-to"></a>适用于
----------

[**ExAllocatePoolWithTag**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag) 
[**ExAllocatePoolWithTagPriority**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtagpriority)另请参阅
--------

[**管理硬件优先级**](../kernel/managing-hardware-priorities.md) 
[**使用自旋锁时防止错误和死锁**](../kernel/preventing-errors-and-deadlocks-while-using-spin-locks.md)
