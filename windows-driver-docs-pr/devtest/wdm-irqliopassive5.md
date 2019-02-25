---
title: IrqlIoPassive5 规则 (wdm)
description: IrqlIoPassive5 规则指定仅当在 IRQL 被动执行时，驱动程序，调用特定的 I/O 管理器例程\_级别。
ms.assetid: 07037cf2-37eb-4045-9588-ac10e79b9c5c
ms.date: 05/21/2018
keywords:
- IrqlIoPassive5 规则 (wdm)
topic_type:
- apiref
api_name:
- IrqlIoPassive5
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fe2f152f467b186398895aabb1d41be3788d81a2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544446"
---
# <a name="irqliopassive5-rule-wdm"></a>IrqlIoPassive5 规则 (wdm)


**IrqlIoPassive5**规则指定驱动程序调用特定的 I/O 管理器例程，仅当执行在 IRQL = 被动\_级别。

|              |     |
|--------------|-----|
| 驱动程序模型 | WDM |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| 使用此规则发现的错误检查 | [**Bug 检查 0xC4:驱动程序\_VERIFIER\_已检测\_冲突**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x0002000E) |

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>IrqlIoPassive5</strong>规则。</p>
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

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">在运行时</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff545448" data-raw-source="[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)">Driver Verifier</a> ，然后选择<a href="https://msdn.microsoft.com/library/windows/hardware/hh454208" data-raw-source="[DDI compliance checking](https://msdn.microsoft.com/library/windows/hardware/hh454208)">DDI 符合性检查</a>选项。</p></td>
</tr>
</tbody>
</table>

 

<a name="applies-to"></a>适用于
----------

[**IoGetConfigurationInformation**](https://msdn.microsoft.com/library/windows/hardware/ff549157)
[**IoGetDeviceObjectPointer**](https://msdn.microsoft.com/library/windows/hardware/ff549198)
[**IoGetDmaAdapter** ](https://msdn.microsoft.com/library/windows/hardware/ff549220) 
 [ **IoGetFileObjectGenericMapping**](https://msdn.microsoft.com/library/windows/hardware/ff549231)
[**最好**](https://msdn.microsoft.com/library/windows/hardware/ff549344) 
 [ **IoIsWdmVersionAvailable**](https://msdn.microsoft.com/library/windows/hardware/ff549382)
[**IoRegisterDriverReinitialization**](https://msdn.microsoft.com/library/windows/hardware/ff549511) 
 [ **IoRegisterShutdownNotification**](https://msdn.microsoft.com/library/windows/hardware/ff549541)
[**IoRemoveShareAccess** ](https://msdn.microsoft.com/library/windows/hardware/ff549587)
 [ **IoSetShareAccess**](https://msdn.microsoft.com/library/windows/hardware/ff550324)
[**IoUnregisterShutdownNotification** ](https://msdn.microsoft.com/library/windows/hardware/ff550409)
 [ **IoUpdateShareAccess**](https://msdn.microsoft.com/library/windows/hardware/ff550412)
[**IoWMIAllocateInstanceIds**](https://msdn.microsoft.com/library/windows/hardware/ff550429) 
 [ **IoWMIRegistrationControl**](https://msdn.microsoft.com/library/windows/hardware/ff550480)
 

 





