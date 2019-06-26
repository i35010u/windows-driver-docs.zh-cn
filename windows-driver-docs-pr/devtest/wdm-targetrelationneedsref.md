---
title: TargetRelationNeedsRef 规则 (wdm)
description: TargetRelationNeedsRef 规则指定，在处理 TargetDeviceRelation 查询时，驱动程序的 DispatchPnP 例程调用以下函数以引用子设备 PDO 之一ObReferenceObjectObReferenceObjectByHandleObReferenceObjectByPointer。
ms.assetid: a341ff7a-1b36-4dfc-9e73-8268ed5b9a78
ms.date: 05/21/2018
keywords:
- TargetRelationNeedsRef 规则 (wdm)
topic_type:
- apiref
api_name:
- TargetRelationNeedsRef
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c4937fd1d1f55ad8d264812b736396f92cabee47
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393491"
---
# <a name="targetrelationneedsref-rule-wdm"></a>TargetRelationNeedsRef 规则 (wdm)


**TargetRelationNeedsRef**规则指定的处理时*TargetDeviceRelation*查询，请在驱动程序[ **DispatchPnP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程调用以下函数以引用子设备 PDO 之一：

-   [**ObReferenceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obfreferenceobject)

-   [**ObReferenceObjectByHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obreferenceobjectbyhandle)

-   [**ObReferenceObjectByPointer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obreferenceobjectbypointer)

此规则适用于仅当该驱动程序完成时 IRP 通过设置`Irp->IoStatus.Information`指针，指向新非**NULL**值。 未应用驱动程序将 IRP 传递给较低的驱动程序时。

此规则不指定什么内容可以称为的有效值`Irp->IoStatus.Information`。 此规则适用于仅当该驱动程序更改的值和新值不是**NULL**。 有效的值是指向设备\_关系结构，其中包含请求的关系信息。

此规则仅适用于总线驱动程序。

|              |     |
|--------------|-----|
| 驱动程序模型 | WDM |

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>并指定<strong>TargetRelationNeedsRef</strong>规则。</p>
使用以下步骤来分析你的代码：
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">准备你的代码 （使用角色类型声明）。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">运行的 Static Driver Verifier。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">查看和分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">以找到缺陷驱动程序中使用 Static Driver Verifier</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用对象
----------

[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)
[**ObReferenceObjectByHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obreferenceobjectbyhandle)
[**ObReferenceObjectByPointer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obreferenceobjectbypointer) 
 [ **PoCallDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver)另请参阅
--------

[**DanglingDeviceObjectReference**](wdm-danglingdeviceobjectreference.md)
 

 





