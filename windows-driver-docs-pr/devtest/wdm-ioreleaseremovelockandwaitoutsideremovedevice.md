---
title: IoReleaseRemoveLockAndWaitOutsideRemoveDevice 规则 (wdm)
description: IoReleaseRemoveLockAndWaitOutsideRemoveDevice 规则指定，IoReleaseRemoveLockAndWait 不应调用外部 IRP\_MJ\_IRP 与 PNP\_MN\_删除\_的即插即用设备驱动程序。
ms.assetid: 5787B14D-1793-4B39-A569-9A1308257A26
ms.date: 05/21/2018
keywords:
- IoReleaseRemoveLockAndWaitOutsideRemoveDevice 规则 (wdm)
topic_type:
- apiref
api_name:
- IoReleaseRemoveLockAndWaitOutsideRemoveDevice
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4dd594c590b50994bf6799b139bcf24ecbebca55
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325349"
---
# <a name="ioreleaseremovelockandwaitoutsideremovedevice-rule-wdm"></a>IoReleaseRemoveLockAndWaitOutsideRemoveDevice 规则 (wdm)


**IoReleaseRemoveLockAndWaitOutsideRemoveDevice**规则指定[ **IoReleaseRemoveLockAndWait** ](https://msdn.microsoft.com/library/windows/hardware/ff549567)不应调用外部 IRP\_MJ\_PNP IRP 与\_MN\_删除\_设备的即插即用驱动程序。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>IoReleaseRemoveLockAndWaitOutsideRemoveDevice</strong>规则。</p>
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

[**IoReleaseRemoveLockAndWait** ](https://msdn.microsoft.com/library/windows/hardware/ff549567)另请参阅
--------

[使用删除锁定](https://msdn.microsoft.com/library/windows/hardware/ff565504)
 

 





