---
title: StorPortVirtualDevice2 规则 (storport)
description: 此规则验证时退出 HwStorFindAdapter 例程，该端口中的 VirtualDevice 字段\_配置\_信息 (Storport) 结构已设置为 TRUE。 该规则仅适用于虚拟 StorPort 微型端口。
ms.assetid: CBD1FAD0-9D85-4989-9CCA-00F5698F5383
ms.date: 05/21/2018
keywords:
- StorPortVirtualDevice2 规则 (storport)
topic_type:
- apiref
api_name:
- StorPortVirtualDevice2
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6f75b930b1b52a0433f6e3e0172da8dd497bd736
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342442"
---
# <a name="storportvirtualdevice2-rule-storport"></a>StorPortVirtualDevice2 规则 (storport)


此规则验证在从退出时[ **HwStorFindAdapter** ](https://msdn.microsoft.com/library/windows/hardware/ff557390)例程**VirtualDevice**字段中[**端口\_配置\_信息 (Storport)** ](https://msdn.microsoft.com/library/windows/hardware/ff563901)结构已被设置为**TRUE**。 该规则仅适用于虚拟 StorPort 微型端口。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>StorPortVirtualDevice2</strong>规则。</p>
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

 

 





