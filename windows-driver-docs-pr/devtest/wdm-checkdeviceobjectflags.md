---
title: 'CheckDeviceObjectFlags 规则 (wdm) '
description: CheckDeviceObjectFlags 规则指定总线驱动程序必须检查用于 DO power PAGABLE 的设备对象标志 \_ \_ ，并 \_ \_ 为 FDO 和子 PDOs 一致地设置电源浪涌。 此规则仅适用于总线驱动程序。
ms.assetid: E229D3A2-30CE-433A-9889-F762CA923803
ms.date: 05/21/2018
keywords:
- 'CheckDeviceObjectFlags 规则 (wdm) '
topic_type:
- apiref
api_name:
- CheckDeviceObjectFlags
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5c8b985ff98a3225ce24b60837276e5f006fb483
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89382757"
---
# <a name="checkdeviceobjectflags-rule-wdm"></a>CheckDeviceObjectFlags 规则 (wdm) 


**CheckDeviceObjectFlags**规则指定总线驱动程序必须检查用于 do power PAGABLE 的设备对象标志 \_ \_ ，并 \_ \_ 为 FDO 和子 PDOs 一致地设置电源浪涌。 此规则仅适用于总线驱动程序。

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
<td align="left"><p>运行 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>CheckDeviceObjectFlags</strong> 规则。</p>
使用以下步骤来运行代码分析：
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](./using-static-driver-verifier-to-find-defects-in-drivers.md#preparing-your-source-code)">准备你的代码 (使用) 的角色类型声明。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](./using-static-driver-verifier-to-find-defects-in-drivers.md#running-static-driver-verifier)">运行静态驱动程序验证程序。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](./using-static-driver-verifier-to-find-defects-in-drivers.md#viewing-and-analyzing-the-results)">查看并分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](./using-static-driver-verifier-to-find-defects-in-drivers.md)">使用静态驱动程序验证器查找驱动程序中的缺陷</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用于
----------

[**ExAllocatePoolWithTag**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag) 
[ **IoCreateDevice**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)
 

