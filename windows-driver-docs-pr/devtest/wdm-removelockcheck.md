---
title: RemoveLockCheck 规则（wdm）
description: RemoveLockCheck 规则验证在 \_ \_ 使用 MinorFunction IRP \_ MN \_ REMOVE 设备处理 IRP MJ PNP 时，对 IoAcquireRemoveLock 和 IoReleaseRemoveLockAndWait 的调用是否正确使用 \_ 。
ms.assetid: 837E94CC-9BEF-45B9-AADE-6BD21063034D
ms.date: 05/21/2018
keywords:
- RemoveLockCheck 规则（wdm）
topic_type:
- apiref
api_name:
- RemoveLockCheck
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5c6246ce98528534a4c86b9673b57d2879f94c10
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917359"
---
# <a name="removelockcheck-rule-wdm"></a>RemoveLockCheck 规则（wdm）


**RemoveLockCheck**规则验证在[**IoAcquireRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock) [**IoReleaseRemoveLockAndWait**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelockandwait) \_ \_ 使用 MinorFunction IRP \_ MN \_ REMOVE \_ 设备处理 IRP MJ PNP 时，对 IoAcquireRemoveLock 和 IoReleaseRemoveLockAndWait 的调用是否正确使用。

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>RemoveLockCheck</strong>规则。</p>
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

[**ExInterlockedInsertHeadList**](https://msdn.microsoft.com/library/windows/hardware/ff545397) 
[**ExInterlockedInsertTailList**](https://msdn.microsoft.com/library/windows/hardware/ff545402) 
[**ExInterlockedPushEntryList**](https://msdn.microsoft.com/library/windows/hardware/ff545418) 
[**InsertHeadList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-insertheadlist) 
[**IoAcquireRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock) 
[**IoCsqInsertIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqinsertirp) 
[**IoCsqInsertIrpEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqinsertirpex) 
[**IoDeleteDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodeletedevice) 
[**IoDetachDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodetachdevice) 
[**IoReleaseRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock) 
[**IoReleaseRemoveLockAndWait**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelockandwait) 
[**RemoveHeadList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-removeheadlist)另请参阅
--------

[使用删除锁](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-remove-locks)
 

 





