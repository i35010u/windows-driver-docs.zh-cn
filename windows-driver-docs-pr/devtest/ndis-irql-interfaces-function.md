---
title: Irql\_接口\_函数规则 (ndis)
description: Irql\_接口\_函数规则指定必须在正确的 IRQL 级别上名为的 NDIS 网络接口功能。
ms.assetid: cea79975-4b14-4c7e-acfe-0bb10679e25b
ms.date: 05/21/2018
keywords:
- Irql_Interfaces_Function 规则 (ndis)
topic_type:
- apiref
api_name:
- Irql_Interfaces_Function
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 64a96fba71af802fb2ae93bc8cedd5ceb539dcad
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325095"
---
# <a name="irqlinterfacesfunction-rule-ndis"></a>Irql\_接口\_函数规则 (ndis)


Irql\_接口\_函数规则指定必须在正确的 IRQL 级别上名为的 NDIS 网络接口功能。

此规则验证的以下的 NDIS 网络接口功能：

**NdisIfAddIfStackEntry**
**NdisIfAllocateNetLuidIndex**
**NdisIfDeleteIfStackEntry** 
 **NdisIfDeregisterInterface**
**NdisIfDeregisterProvider**
**NdisIfFreeNetLuidIndex** 
 **NdisIfGetInterfaceIndexFromNetLuid**
**NdisIfGetNetLuidFromInterfaceIndex**
**NdisIfQueryBindingIfIndex** 
 **NdisIfRegisterInterface**
**NdisIfRegisterProvider**

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>Irql_Interfaces_Function</strong>规则。</p>
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

[**NdisIfAddIfStackEntry**](https://msdn.microsoft.com/library/windows/hardware/ff562693)
[**NdisIfAllocateNetLuidIndex** ](https://msdn.microsoft.com/library/windows/hardware/ff562695) 
 [ **NdisIfDeleteIfStackEntry**](https://msdn.microsoft.com/library/windows/hardware/ff562698)
[**NdisIfDeregisterInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff562700) 
 [ **NdisIfDeregisterProvider**](https://msdn.microsoft.com/library/windows/hardware/ff562703)
[**NdisIfFreeNetLuidIndex** ](https://msdn.microsoft.com/library/windows/hardware/ff562706) 
 [ **NdisIfGetInterfaceIndexFromNetLuid**](https://msdn.microsoft.com/library/windows/hardware/ff562707)
[**NdisIfGetNetLuidFromInterfaceIndex** ](https://msdn.microsoft.com/library/windows/hardware/ff562711) 
 [**NdisIfQueryBindingIfIndex**](https://msdn.microsoft.com/library/windows/hardware/ff562713)
[**NdisIfRegisterInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff562715) 
 [ **NdisIfRegisterProvider**](https://msdn.microsoft.com/library/windows/hardware/ff562716)








