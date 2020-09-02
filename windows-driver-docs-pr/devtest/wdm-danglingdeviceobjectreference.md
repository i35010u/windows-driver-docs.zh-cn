---
title: 'DanglingDeviceObjectReference 规则 (wdm) '
description: DanglingDeviceObjectReference 规则指定驱动程序将 ObDereferenceObject 与 IoGetAttachedDeviceReference 返回的设备对象指针一起调用。
ms.assetid: b2aeaa16-f246-48c7-9e80-719d441a44ef
ms.date: 05/21/2018
keywords:
- 'DanglingDeviceObjectReference 规则 (wdm) '
topic_type:
- apiref
api_name:
- DanglingDeviceObjectReference
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 548041da386241615e8415b56b68e534200b3c9f
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89383141"
---
# <a name="danglingdeviceobjectreference-rule-wdm"></a>DanglingDeviceObjectReference 规则 (wdm) 


**DanglingDeviceObjectReference**规则指定驱动程序将[**ObDereferenceObject**](/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobject)与[**IoGetAttachedDeviceReference**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iogetattacheddevicereference)返回的设备对象指针一起调用。

此规则还指定通过在驱动程序退出之前调用**ObDereferenceObject**来取消引用通过调用**IoGetAttachedDeviceReference**引用的驱动程序的所有设备对象指针。 ObfDereferenceObject

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
<td align="left"><p>运行 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>DanglingDeviceObjectReference</strong> 规则。</p>
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

[**IoGetAttachedDeviceReference**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iogetattacheddevicereference)
 

