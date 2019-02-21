---
title: StorPortMSILock 规则 (storport)
description: 微型端口驱动程序所需，当且仅当，获取一条消息的 MSI 数值调节钮锁定端口 InterruptSynchronizationMode 成员\_配置\_信息 (Storport) 结构设置为InterruptSynchronizePerMessage。
ms.assetid: 99C45ADB-AFCC-4B9E-8EB9-DBD7C7F6D800
ms.date: 05/21/2018
keywords:
- StorPortMSILock 规则 (storport)
topic_type:
- apiref
api_name:
- StorPortMSILock
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 50116c8aeefd5dac4dbe7f37ad8b737d1f7a3953
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523816"
---
# <a name="storportmsilock-rule-storport"></a>StorPortMSILock 规则 (storport)


微型端口驱动程序所需，当且仅当，获取一条消息的 MSI 数值调节钮锁定**InterruptSynchronizationMode**的成员[**端口\_配置\_信息 (Storport)** ](https://msdn.microsoft.com/library/windows/hardware/ff563901)结构设置为**InterruptSynchronizePerMessage**。 此规则验证的调用[ **StorPortAcquireMSISpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff567023)如果同步模式，则仅进行**InterruptSynchronizePerMessage**。

|              |          |
|--------------|----------|
| 驱动程序模型 | Storport |

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>StorPortMSILock</strong>规则。</p>
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

 

 





