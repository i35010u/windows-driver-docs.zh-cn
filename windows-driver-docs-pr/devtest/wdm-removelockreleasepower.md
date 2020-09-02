---
title: 'RemoveLockReleasePower 规则 (wdm) '
description: RemoveLockReleasePower 规则验证是否在严格替换中使用对 IoAcquireRemoveLock 和 IoReleaseRemoveLock 的调用。 而且，在调度例程结束时，驱动程序不应持有删除锁定。
ms.assetid: B327CE08-000E-43E1-8E92-BD4961E0C1C5
ms.date: 05/21/2018
keywords:
- 'RemoveLockReleasePower 规则 (wdm) '
topic_type:
- apiref
api_name:
- RemoveLockReleasePower
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7189f6d88514db65fcc599addbb426f1196b9483
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89381802"
---
# <a name="removelockreleasepower-rule-wdm"></a>RemoveLockReleasePower 规则 (wdm) 


**RemoveLockReleasePower**规则验证是否在严格替换中使用对[**IoAcquireRemoveLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)和[**IoReleaseRemoveLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock)的调用。 而且，在调度例程结束时，驱动程序不应持有删除锁定。

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
<td align="left"><p>运行 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>RemoveLockReleasePower</strong> 规则。</p>
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

[**ExInterlockedInsertHeadList**](/previous-versions/ff545397(v=vs.85)) 
[**ExInterlockedInsertTailList**](/previous-versions/ff545402(v=vs.85)) 
[**ExInterlockedPushEntryList**](/previous-versions/ff545418(v=vs.85)) 
[**InsertHeadList**](/windows-hardware/drivers/ddi/wdm/nf-wdm-insertheadlist) 
[**IoAcquireRemoveLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock) 
[**IoCsqInsertIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqinsertirp) 
[**IoCsqInsertIrpEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqinsertirpex) 
[**IoReleaseRemoveLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock) 
[**IoReleaseRemoveLockAndWait**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelockandwait) 
[**RemoveHeadList**](/windows-hardware/drivers/ddi/wdm/nf-wdm-removeheadlist)
 

