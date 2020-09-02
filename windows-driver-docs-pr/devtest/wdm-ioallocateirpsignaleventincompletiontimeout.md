---
title: 'IoAllocateIrpSignalEventInCompletionTimeout 规则 (wdm) '
description: 如果 IoAllocateIrpSignalEventInCompletionTimeout 规则检测到此驱动程序将无限期等待，直到降低驱动程序返回，因为 IRP 的事件需要在完成例程中发出信号。
ms.assetid: 7E00F7EC-3FB9-4BFB-AE10-D846282B37AA
ms.date: 05/21/2018
keywords:
- 'IoAllocateIrpSignalEventInCompletionTimeout 规则 (wdm) '
topic_type:
- apiref
api_name:
- IoAllocateIrpSignalEventInCompletionTimeout
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 52f245834392072ad3453cbb255a571aec643340
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89381737"
---
# <a name="ioallocateirpsignaleventincompletiontimeout-rule-wdm"></a>IoAllocateIrpSignalEventInCompletionTimeout 规则 (wdm) 


如果 **IoAllocateIrpSignalEventInCompletionTimeout** 规则检测到此驱动程序将无限期等待，直到降低驱动程序返回，因为 IRP 的事件需要在完成例程中发出信号。

此规则用于本地创建的异步 Irp。

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
<td align="left"><p>运行 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>IoAllocateIrpSignalEventInCompletionTimeout</strong> 规则。</p>
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

[**IoAllocateIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp) 
[**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) 
[**IoSetCompletionRoutine**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine) 
[**IoSetCompletionRoutineEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutineex) 
[**KeInitializeEvent**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializeevent) 
[**KeWaitForSingleObject**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject) 
[**PoCallDriver**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)
 

