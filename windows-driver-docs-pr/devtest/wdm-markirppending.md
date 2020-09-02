---
title: 'MarkIrpPending 规则 (wdm) '
description: MarkIrpPending 规则指定每当驱动程序调度例程调用也时，驱动程序在 \_ 调度例程结束时返回状态 "挂起"。 有关免费规范，请参阅 MarkIrpPending2。
ms.assetid: cbf5484e-2806-4df6-bdfb-98acfe5d214c
ms.date: 05/21/2018
keywords:
- 'MarkIrpPending 规则 (wdm) '
topic_type:
- apiref
api_name:
- MarkIrpPending
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fb32f86f8bdab65de8fe695057949fd4ecca088e
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89383293"
---
# <a name="markirppending-rule-wdm"></a>MarkIrpPending 规则 (wdm) 


**MarkIrpPending**规则指定每当驱动程序调度例程调用[**也**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)时，驱动程序在 \_ 调度例程结束时返回状态 "挂起"。 有关免费规范，请参阅 [**MarkIrpPending2**](wdm-markirppending2.md) 。

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
<td align="left"><p>运行 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>MarkIrpPending</strong> 规则。</p>
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

<a name="applies-to"></a>适用于
----------

[**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) 
[**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) 
[**也**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending) 
[**PoCallDriver**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver) 
[**RemoveHeadList**](/windows-hardware/drivers/ddi/wdm/nf-wdm-removeheadlist)另请参阅
--------

[**MarkingInterlockedQueuedIrps**](wdm-markinginterlockedqueuedirps.md) 
[**正在同步 IRP 取消**](../kernel/synchronizing-irp-cancellation.md)
 

