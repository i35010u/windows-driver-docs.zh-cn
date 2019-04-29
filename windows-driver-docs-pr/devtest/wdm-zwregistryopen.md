---
title: ZwRegistryOpen 规则 (wdm)
ms.assetid: c98682c3-0d38-4d5b-9649-7574106f9ce3
ms.date: 05/21/2018
description: ''
keywords:
- ZwRegistryOpen 规则 (wdm)
topic_type:
- apiref
api_name:
- ZwRegistryOpen
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a61e568b5d3335a9f53741535f633026d59e065e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370781"
---
# <a name="zwregistryopen-rule-wdm"></a>ZwRegistryOpen 规则 (wdm)


[ **ZwRegistryOpen** ](storport-zwregistryopen.md)规则指定后调用[ **ZwOpenKey**](https://msdn.microsoft.com/library/windows/hardware/ff567014)，驱动程序调用的以下注册表函数同时打开的句柄保留到注册表项 (在调用前，即[ **ZwClose** ](https://msdn.microsoft.com/library/windows/hardware/ff566417)或[ **ZwDeleteKey**](https://msdn.microsoft.com/library/windows/hardware/ff566437)):

-   [**ZwClose**](https://msdn.microsoft.com/library/windows/hardware/ff566417)

-   [**ZwDeleteKey**](https://msdn.microsoft.com/library/windows/hardware/ff566437)

-   [**ZwEnumerateKey**](https://msdn.microsoft.com/library/windows/hardware/ff566447)

-   [**ZwEnumerateValueKey**](https://msdn.microsoft.com/library/windows/hardware/ff566453)

-   [**ZwFlushKey**](https://msdn.microsoft.com/library/windows/hardware/ff566457)

-   [**ZwQueryKey**](https://msdn.microsoft.com/library/windows/hardware/ff567060)

-   [**ZwQueryValueKey**](https://msdn.microsoft.com/library/windows/hardware/ff567069)

-   [**ZwSetValueKey**](https://msdn.microsoft.com/library/windows/hardware/ff567109)

此规则还指定驱动程序必须调用[ **ZwOpenKey** ](https://msdn.microsoft.com/library/windows/hardware/ff567014)如果它已保存到该注册表项的打开句柄。

最后，此规则指定驱动程序必须返回从调度例程或保存到注册表项的打开句柄时取消例程。

此规则不会验证，该驱动程序打开的句柄到正确的注册表项时按住它调用[ **ZwClose** ](https://msdn.microsoft.com/library/windows/hardware/ff566417)或[ **ZwDeleteKey** ](https://msdn.microsoft.com/library/windows/hardware/ff566437).

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
[**ZwCreateKey**](https://msdn.microsoft.com/library/windows/hardware/ff566425)
[**ZwDeleteKey** ](https://msdn.microsoft.com/library/windows/hardware/ff566437) 
[ **ZwEnumerateKey**](https://msdn.microsoft.com/library/windows/hardware/ff566447)
[**ZwEnumerateValueKey** ](https://msdn.microsoft.com/library/windows/hardware/ff566453) 
 [ **ZwFlushKey**](https://msdn.microsoft.com/library/windows/hardware/ff566457)
[**ZwOpenKey**](https://msdn.microsoft.com/library/windows/hardware/ff567014)
[**ZwQueryKey** ](https://msdn.microsoft.com/library/windows/hardware/ff567060)
 [ **ZwQueryValueKey**](https://msdn.microsoft.com/library/windows/hardware/ff567069)
[**ZwSetValueKey** ](https://msdn.microsoft.com/library/windows/hardware/ff567109)另请参阅
--------

[**ZwRegistryCreate**](wdm-zwregistrycreate.md)
 

 





