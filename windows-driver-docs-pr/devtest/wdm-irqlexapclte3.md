---
title: 'IrqlExApcLte3 规则 (wdm) '
description: IrqlExApcLte3 规则指定驱动程序只调用以下执行程序支持例程，APC_LEVEL。
ms.assetid: 80668699-dfca-4fb9-8ffe-d20be00542dc
ms.date: 05/21/2018
keywords:
- 'IrqlExApcLte3 规则 (wdm) '
topic_type:
- apiref
api_name:
- IrqlExApcLte3
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1e7603644b4885c91ccc4e12eebc5c33aed26f9a
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89382051"
---
# <a name="irqlexapclte3-rule-wdm"></a>IrqlExApcLte3 规则 (wdm) 


**IrqlExApcLte3**规则指定该驱动程序只调用 IRQL &lt; = APC 级别的下列执行程序支持例程 \_ 。

-   [**ExAcquireResourceExclusiveLite**](/previous-versions/ff544351(v=vs.85))

-   [**ExAcquireResourceSharedLite**](/previous-versions/ff544363(v=vs.85))

-   [**ExAcquireSharedStarveExclusive**](/previous-versions/ff544367(v=vs.85))

-   [**ExAcquireSharedWaitForExclusive**](/previous-versions/ff544370(v=vs.85))

-   [**ExConvertExclusiveToSharedLite**](/previous-versions/ff544558(v=vs.85))

-   [**ExDeleteResourceLite**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeleteresourcelite)

具有与 IRQL 相关的错误的驱动程序可能会导致严重问题，并可能导致计算机崩溃。

**驱动程序模型： WDM**

**Bug 检查 () 发现此规则**： [**bug 检查0XC4：驱动程序 \_ 验证器 \_ 检测到 \_ 违反**](../debugger/bug-check-0xc4--driver-verifier-detected-violation.md) (0X20007) ， [**bug 检查0xA： IRQL \_ 不 \_ 小于 \_ 或 \_ 等于**](../debugger/bug-check-0xa--irql-not-less-or-equal.md)


<a name="example"></a>示例
-------

以下代码违反了此规则：

```ManagedCPlusPlus
NTSTATUS
DispatchRequest (
    _In_ PDEVICE_REQUEST DeviceRequest
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
    _In_ PDEVICE_REQUEST DeviceRequest
    )
{
    ERESOURCE Resource;
    NTSTATUS Status;
    ...

    Resource = DeviceRequest->GetTableLock();

    //
    // RULE VIOLATION! - ExAcquireSharedStarveExclusive can be called only at 
    //                   IRQL <= APC_LEVEL. 
    //

    if(!ExAcquireSharedStarveExclusive(&Resource, FALSE)) {
        return STATUS_UNSUCCESSFUL;
    }

    ...

    ExReleaseResourceLite(&Resource);
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
<td align="left"><p>运行 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>IrqlExApcLte3</strong> 规则。</p>
使用以下步骤来运行代码分析：
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](./using-static-driver-verifier-to-find-defects-in-drivers.md#preparing-your-source-code)">准备你的代码 (使用) 的角色类型声明。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](./using-static-driver-verifier-to-find-defects-in-drivers.md#running-static-driver-verifier)">运行静态驱动程序验证程序。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](./using-static-driver-verifier-to-find-defects-in-drivers.md#viewing-and-analyzing-the-results)">查看并分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](./using-static-driver-verifier-to-find-defects-in-drivers.md)">使用静态驱动程序验证器查找驱动程序中的缺陷</a>。</p></td>
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
<td align="left"><p>运行 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](./driver-verifier.md)">驱动程序验证程序</a> ，并选择 " <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking" data-raw-source="[DDI compliance checking](./ddi-compliance-checking.md)">DDI 相容性检查</a> " 选项。</p></td>
</tr>
</tbody>
</table>

 

<a name="applies-to"></a>适用于
----------

[**ExAcquireResourceExclusiveLite**](/previous-versions/ff544351(v=vs.85)) 
[**ExAcquireResourceSharedLite**](/previous-versions/ff544363(v=vs.85)) 
[**ExAcquireSharedStarveExclusive**](/previous-versions/ff544367(v=vs.85)) 
[**ExAcquireSharedWaitForExclusive**](/previous-versions/ff544370(v=vs.85)) 
[**ExConvertExclusiveToSharedLite**](/previous-versions/ff544558(v=vs.85)) 
[**ExDeleteResourceLite**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeleteresourcelite)另请参阅
--------

[管理硬件优先级](../kernel/managing-hardware-priorities.md) 
[使用自旋锁时防止错误和死锁](../kernel/preventing-errors-and-deadlocks-while-using-spin-locks.md)
 

