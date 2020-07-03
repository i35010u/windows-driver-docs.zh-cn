---
title: StartIoRecursion 规则（wdm）
description: StartIoRecursion 规则指定如果驱动程序的 StartIo 例程包括对 IoStartNextPacket 的调用，则驱动程序必须先调用 IoSetStartIoAttributes，并将 DeferredStartIo 属性设置为 TRUE。 否则，可能会导致无限递归。
ms.assetid: 997df0a3-1222-435d-9c61-e97a2b6185cf
ms.date: 05/21/2018
keywords:
- StartIoRecursion 规则（wdm）
topic_type:
- apiref
api_name:
- StartIoRecursion
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: cd2c6c795db1ef24ddc82b741d7f5c935e229e76
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917605"
---
# <a name="startiorecursion-rule-wdm"></a>StartIoRecursion 规则（wdm）


**StartIoRecursion**规则指定如果驱动程序的[**StartIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)例程包括对[**IoStartNextPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartnextpacket)的调用，则驱动程序必须先调用[**IoSetStartIoAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iosetstartioattributes) ，并将*DeferredStartIo*属性设置为**TRUE**。 否则，可能会导致无限递归。

**驱动程序模型： WDM**

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>StartIoRecursion</strong>规则。</p>
使用以下步骤来运行代码分析：
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">准备你的代码（使用角色类型声明）。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">运行静态驱动程序验证程序。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">查看并分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">使用静态驱动程序验证器查找驱动程序中的缺陷</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用于
----------

[**IoSetStartIoAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iosetstartioattributes) 
[ **IoStartNextPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartnextpacket)
 

 





