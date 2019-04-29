---
title: NdisOpenConfigurationEx 规则 (ndis)
description: 此规则检查备用顺序调用 NdisOpenConfigurationEx 和 NdisCloseConfiguration。 最终目标是确保 MiniportHaltEx 退出时关闭配置句柄。
ms.assetid: 3E23D8AE-5EBC-4C2F-9EE3-42718D86B97C
ms.date: 05/21/2018
keywords:
- NdisOpenConfigurationEx 规则 (ndis)
topic_type:
- apiref
api_name:
- NdisOpenConfigurationEx
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1d61c15cc3fe3d00c79a70fcf13d45ecab0f4c3a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382982"
---
# <a name="ndisopenconfigurationex-rule-ndis"></a>NdisOpenConfigurationEx 规则 (ndis)


此规则检查[ **NdisOpenConfigurationEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563717)并[ **NdisCloseConfiguration** ](https://msdn.microsoft.com/library/windows/hardware/ff561642)备用顺序调用。 请确保配置句柄已关闭时的最终目标是[ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)退出。

此规则使用三个不同的状态。 打开或关闭某个配置时的状态更改。 如果配置句柄仍处于打开状态时[ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)退出后，报告缺陷。

|              |      |
|--------------|------|
| 驱动程序模型 | NDIS |

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>NdisOpenConfigurationEx</strong>规则。</p>
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

[**NdisCloseConfiguration**](https://msdn.microsoft.com/library/windows/hardware/ff561642)
[**NdisOpenConfigurationEx**](https://msdn.microsoft.com/library/windows/hardware/ff563717)
 

 





