---
title: ZwRegistryOpen 规则 (storport)
description: 此规则验证到通过 ZwOpenKey 打开注册表项句柄随后由其他 ZwXxx 例程的正确使用。
ms.assetid: E423616B-C990-4D26-ABB4-6061BF3B6A21
ms.date: 05/21/2018
keywords:
- ZwRegistryOpen 规则 (storport)
topic_type:
- apiref
api_name:
- ZwRegistryOpen
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 97961ad3554ff0236738beb392232e2a4d90a9f2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342466"
---
# <a name="zwregistryopen-rule-storport"></a>ZwRegistryOpen 规则 (storport)


此规则验证通过打开的句柄的注册表项**ZwOpenKey**的随后使用由其他 ZwXxx 例程的正确无误。 例程**ZwEnumerateKey**， **ZwEnumerateValueKey**， **ZwFlushKey**， **ZwQueryKey**， **ZwQueryValueKey**， **ZwSetValueKey**， **ZwClose**，并且**ZwDeleteKey**不得在未打开的句柄上调用。 此外必须在返回前关闭句柄。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>ZwRegistryOpen</strong>规则。</p>
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

[**ZwClose**](https://msdn.microsoft.com/library/windows/hardware/ff566417)
[**ZwDeleteKey**](https://msdn.microsoft.com/library/windows/hardware/ff566437)
[**ZwEnumerateKey** ](https://msdn.microsoft.com/library/windows/hardware/ff566447)
 [ **ZwEnumerateValueKey**](https://msdn.microsoft.com/library/windows/hardware/ff566453)
[**ZwFlushKey** ](https://msdn.microsoft.com/library/windows/hardware/ff566457) 
 [**ZwOpenKey**](https://msdn.microsoft.com/library/windows/hardware/ff567014)
[**ZwQueryKey**](https://msdn.microsoft.com/library/windows/hardware/ff567060)
[**ZwQueryValueKey** ](https://msdn.microsoft.com/library/windows/hardware/ff567069) 
 [ **ZwSetValueKey**](https://msdn.microsoft.com/library/windows/hardware/ff567109)
 

 





