---
title: 'WithinCriticalRegion 规则 (storport) '
description: 此规则验证是否只有在禁用正常内核 APC 传递时才对驱动程序的某些同步函数进行调用。
ms.assetid: 338E6995-0EB2-476D-B5F5-504DC8FF8609
ms.date: 05/21/2018
keywords:
- 'WithinCriticalRegion 规则 (storport) '
topic_type:
- apiref
api_name:
- WithinCriticalRegion
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 60dab54457a57106e284540752af0aff9830155f
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89383331"
---
# <a name="withincriticalregion-rule-storport"></a>WithinCriticalRegion 规则 (storport) 


此规则验证是否只有在禁用正常内核 APC 传递时才对驱动程序的某些同步函数进行调用。

**驱动程序模型： Storport**

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
<td align="left"><p>运行 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>WithinCriticalRegion</strong> 规则。</p>
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

[**ExAcquireResourceExclusiveLite**](/previous-versions/ff544351(v=vs.85)) 
[**ExAcquireResourceSharedLite**](/previous-versions/ff544363(v=vs.85)) 
[**ExAcquireSharedStarveExclusive**](/previous-versions/ff544367(v=vs.85)) 
[**ExAcquireSharedWaitForExclusive**](/previous-versions/ff544370(v=vs.85)) 
[**ExReleaseResourceForThreadLite**](/previous-versions/ff545585(v=vs.85)) 
[**ExReleaseResourceLite**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exreleaseresourcelite) 
[**KeEnterCriticalRegion**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keentercriticalregion) 
[**KeLeaveCriticalRegion**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keleavecriticalregion)
 

