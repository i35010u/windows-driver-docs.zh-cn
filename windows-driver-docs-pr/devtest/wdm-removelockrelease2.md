---
title: RemoveLockRelease2 规则 (wdm)
description: 规则 RemoveLockRelease2 验证对 IoAcquireRemoveLock 和 IoReleaseRemoveLock 调用可在严格的分支结构。 此外，在调度例程末尾驱动程序不应阻止删除锁。
ms.assetid: 2569120A-9014-44C1-86F9-6C1ABACC2C34
ms.date: 05/21/2018
keywords:
- RemoveLockRelease2 规则 (wdm)
topic_type:
- apiref
api_name:
- RemoveLockRelease2
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 952437bfdc2a75e282b50b81716930684849a833
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368638"
---
# <a name="removelockrelease2-rule-wdm"></a>RemoveLockRelease2 规则 (wdm)


该规则**RemoveLockRelease2**验证的调用[ **IoAcquireRemoveLock** ](https://msdn.microsoft.com/library/windows/hardware/ff548204)并[ **IoReleaseRemoveLock**](https://msdn.microsoft.com/library/windows/hardware/ff549560)严格的分支结构中使用。 此外，在调度例程末尾驱动程序不应阻止删除锁。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>RemoveLockRelease2</strong>规则。</p>
使用以下步骤来分析你的代码：
<ol>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code)">准备你的代码 （使用角色类型声明）。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier)">运行的 Static Driver Verifier。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results)">查看和分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/hh454281" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://msdn.microsoft.com/library/windows/hardware/hh454281)">以找到缺陷驱动程序中使用 Static Driver Verifier</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用对象
----------

[**ExInterlockedInsertHeadList**](https://msdn.microsoft.com/library/windows/hardware/ff545397)
[**ExInterlockedInsertTailList** ](https://msdn.microsoft.com/library/windows/hardware/ff545402) 
 [ **ExInterlockedPushEntryList**](https://msdn.microsoft.com/library/windows/hardware/ff545418)
[**InsertHeadList** ](https://msdn.microsoft.com/library/windows/hardware/ff547820) 
 [ **IoAcquireRemoveLock**](https://msdn.microsoft.com/library/windows/hardware/ff548204)
[**IoReleaseRemoveLock**](https://msdn.microsoft.com/library/windows/hardware/ff549560)
[**RemoveHeadList**](https://msdn.microsoft.com/library/windows/hardware/ff561032)
 

 





