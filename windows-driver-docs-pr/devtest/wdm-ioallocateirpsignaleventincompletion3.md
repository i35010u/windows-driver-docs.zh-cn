---
title: 'IoAllocateIrpSignalEventInCompletion3 规则 (wdm) '
description: IoAllocateIrpSignalEventInCompletion3 规则指定在设置了 Irp-PendingReturned 标志并且完成例程正在处理本地创建的异步 IRP 时，需要在完成例程中调用 KeSetEvent。
ms.assetid: 3B9D546D-9CBB-46A8-9F1F-9908D1548556
ms.date: 05/21/2018
keywords:
- 'IoAllocateIrpSignalEventInCompletion3 规则 (wdm) '
topic_type:
- apiref
api_name:
- IoAllocateIrpSignalEventInCompletion3
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9b835f6bdbf94604158893afbfcd4ef38530fc3e
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90103102"
---
# <a name="ioallocateirpsignaleventincompletion3-rule-wdm"></a>IoAllocateIrpSignalEventInCompletion3 规则 (wdm) 


**IoAllocateIrpSignalEventInCompletion3**规则指定在设置了**Irp- &gt; PendingReturned**标志并且完成例程正在处理本地创建的异步 Irp 时，需要在完成例程中调用[**KeSetEvent**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent) 。

在这种情况下，将不会调用完成例程。

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
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>IoAllocateIrpSignalEventInCompletion3</strong> 规则。</p>
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

<a name="applies-to"></a>适用于
----------

[**IoAllocateIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp) 
[**IoBuildDeviceIoControlRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest) 
[**IoSetCompletionRoutine**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine) 
[**IoSetCompletionRoutineEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutineex) 
[**KeInitializeEvent**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializeevent)
