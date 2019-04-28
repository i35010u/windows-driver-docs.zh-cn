---
title: ZwRegistryCreate 规则 (storport)
description: 此规则验证对使用 ZwCreateKey 创建一个注册表项句柄随后由其他 ZwXxx 例程的正确使用。
ms.assetid: 38CCE6AA-BA42-4305-B193-CB1B1C0F105B
ms.date: 05/21/2018
keywords:
- ZwRegistryCreate 规则 (storport)
topic_type:
- apiref
api_name:
- ZwRegistryCreate
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5316e681bd5750feac7bd405769e26168adb593b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342461"
---
# <a name="zwregistrycreate-rule-storport"></a>ZwRegistryCreate 规则 (storport)


此规则将验证与创建注册表项的句柄[ **ZwCreateKey** ](https://msdn.microsoft.com/library/windows/hardware/ff566425)随后将由正确其他*ZwXxx*例程。 [ **ZwOpenKey** ](https://msdn.microsoft.com/library/windows/hardware/ff567014)不得在已打开的句柄上调用例程。 例程[ **ZwEnumerateKey**](https://msdn.microsoft.com/library/windows/hardware/ff566447)， [ **ZwEnumerateValueKey**](https://msdn.microsoft.com/library/windows/hardware/ff566453)， [ **ZwFlushKey** ](https://msdn.microsoft.com/library/windows/hardware/ff566457)， [ **ZwQueryKey**](https://msdn.microsoft.com/library/windows/hardware/ff567060)， [ **ZwQueryValueKey**](https://msdn.microsoft.com/library/windows/hardware/ff567069)， [ **ZwSetValueKey**](https://msdn.microsoft.com/library/windows/hardware/ff567109)， [ **ZwClose**](https://msdn.microsoft.com/library/windows/hardware/ff566417)，以及[ **ZwDeleteKey** ](https://msdn.microsoft.com/library/windows/hardware/ff566437)必须在不调用未打开的句柄。 此外必须在返回前关闭句柄。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>ZwRegistryCreate</strong>规则。</p>
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
[**ZwCreateKey**](https://msdn.microsoft.com/library/windows/hardware/ff566425)
[**ZwDeleteKey** ](https://msdn.microsoft.com/library/windows/hardware/ff566437) 
[ **ZwEnumerateKey**](https://msdn.microsoft.com/library/windows/hardware/ff566447)
[**ZwEnumerateValueKey** ](https://msdn.microsoft.com/library/windows/hardware/ff566453) 
 [ **ZwFlushKey**](https://msdn.microsoft.com/library/windows/hardware/ff566457)
[**ZwOpenKey**](https://msdn.microsoft.com/library/windows/hardware/ff567014)
[**ZwQueryKey** ](https://msdn.microsoft.com/library/windows/hardware/ff567060)
 [ **ZwQueryValueKey**](https://msdn.microsoft.com/library/windows/hardware/ff567069)
[**ZwSetValueKey**](https://msdn.microsoft.com/library/windows/hardware/ff567109)
 

 





