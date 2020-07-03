---
title: TargetRelationNeedsRef 规则（wdm）
description: TargetRelationNeedsRef 规则指定在处理 TargetDeviceRelation 查询时，驱动程序的 DispatchPnP 例程调用以下函数之一来引用子设备的 PDO ObReferenceObjectObReferenceObjectByHandleObReferenceObjectByPointer。
ms.assetid: a341ff7a-1b36-4dfc-9e73-8268ed5b9a78
ms.date: 05/21/2018
keywords:
- TargetRelationNeedsRef 规则（wdm）
topic_type:
- apiref
api_name:
- TargetRelationNeedsRef
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 12e7305958f542e694f525aca7726fb6a1a7384a
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917058"
---
# <a name="targetrelationneedsref-rule-wdm"></a>TargetRelationNeedsRef 规则（wdm）


**TargetRelationNeedsRef**规则指定在处理*TargetDeviceRelation*查询时，驱动程序的[**DispatchPnP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程调用以下函数之一来引用子设备的 PDO：

-   [**ObReferenceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obfreferenceobject)

-   [**ObReferenceObjectByHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle)

-   [**ObReferenceObjectByPointer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbypointer)

仅当驱动程序通过将 `Irp->IoStatus.Information` 指针设置为新的非**空**值来完成 IRP 时，此规则才适用。 当驱动程序将 IRP 传递到较低的驱动程序时，它不会应用。

此规则不指定哪些值是的有效值 `Irp->IoStatus.Information` 。 仅当驱动程序更改值并且新值不为**NULL**时，才应用此规则。 有效的值是指向设备 \_ 关系结构的指针，该结构包含请求的关系信息。

此规则仅适用于总线驱动程序。

**驱动程序模型： WDM**

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>TargetRelationNeedsRef</strong>规则。</p>
使用以下步骤来运行代码分析：
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">准备你的代码（使用角色类型声明）。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">运行静态驱动程序验证程序。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">查看并分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">使用静态驱动程序验证器查找驱动程序中的缺陷</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用于
----------

[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) 
[**ObReferenceObjectByHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle) 
[**ObReferenceObjectByPointer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbypointer) 
[**PoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)另请参阅
--------

[**DanglingDeviceObjectReference**](wdm-danglingdeviceobjectreference.md)
 

 





